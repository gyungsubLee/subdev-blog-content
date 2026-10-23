---
order: 6
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 204eda9b-0fe1-8133-a81c-e671345f99ba
title: Jenkins + Nginx 환경에서의 병목 현상 발생
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817b-9c95-d96fd53640c4
    title: CI/CD
  - id: 203eda9b-0fe1-80d5-8c37-c693a491e2cd
    title: 애플리케이션 배포 자동화와 CI/CD -Jenkins
  - id: 204eda9b-0fe1-8133-a81c-e671345f99ba
    title: Jenkins + Nginx 환경에서의 병목 현상 발생
excerpt: ✏️ 개요 (Problem Summary) --- EC2 인스턴스에 Docker 기반으로 Jenkins와 Nginx를 구성한 후, 웹 UI 접속 시 비정상적으로 느린 응답 속도가 지속적으로 발생했다. 특히 Jenkins 자체는 실행되었음에도 Nginx Reverse Proxy를 통한 접근이 심각하게 지연되었고, 심지어 t
cover: null
icon: null
notionProperties:
  Tags: 트러블슈팅
  상태: 완료
schema_version: 1
parent_id: 203eda9b-0fe1-80d5-8c37-c693a491e2cd
created: 2025-05-31T10:36:46.771Z
updated: 2025-05-31T10:36:46.771Z
legacy_path: Main/CI-CD-d96fd53640c4/애플리케이션 배포 자동화와 CI-CD -Jenkins-c693a491e2cd/Jenkins + Nginx 환경에서의 병목 현상 발생-e671345f99ba/index.md
legacy_category: CI/CD
source_url: https://beautiful-college-c84.notion.site/204eda9b0fe18133a81ce671345f99ba
---
<a id="204eda9b0fe1815eab7eeee579551d15"></a>

### <strong>✏️  개요 (Problem Summary)</strong>

---

<a id="204eda9b0fe1811bab1be75fa6b7c724"></a>

EC2 인스턴스에 Docker 기반으로 Jenkins와 Nginx를 구성한 후,

<a id="204eda9b0fe181ebb32ad67ae509cf38"></a>

웹 UI 접속 시 비정상적으로 느린 응답 속도가 지속적으로 발생했다&#46;

<a id="204eda9b0fe181f3afdcf0a764ef4891"></a>

특히 Jenkins 자체는 실행되었음에도 Nginx Reverse Proxy를 통한 접근이 <strong>심각하게 지연</strong>되었고,

<a id="204eda9b0fe181eabf15fb7164ef5d39"></a>

심지어 <code>t3&#46;small</code> → <code>m5&#46;large</code>로 인스턴스 스펙을 <strong>상향</strong>했음에도 증상이 개선되지 않았다&#46;

<a id="204eda9b0fe181618522f8ba7bca4899"></a>

### <strong>🔍 원인 분석 (Root Cause)</strong>

---

<a id="204eda9b0fe181c58a08d52588eb2224"></a>

<strong>1&#46; Docker Named Volume → OverlayFS I/O 병목</strong>

<a id="204eda9b0fe181d39c4cd2f008d45d72"></a>

```yaml
// 문제 있는 설정
volumes:
  - jenkins_home:/var/jenkins_home
```

- Docker Named Volume은 내부적으로 OverlayFS 사용 → 대량 I/O에 비효율적
    - <code>jenkins&#95;home&#58;/var/jenkins&#95;hom</code>e 형태의 <strong>named volume</strong>은 overlay2 스토리지 드라이버 사용 시 성능 저하가 발생할 수 있음&#46;

- 디스크 사용률이 낮더라도, 내부적인 파일 시스템 병목이 원인일 수 있음
    - Jenkins는 <code>&#46;xml</code>, <code>&#46;log</code>, <code>&#46;config</code> 파일을 지속적으로 읽고 씀

    - Jenkins는 파일 I/O가 빈번하게 발생하기 때문에, <strong>디스크 성능이 곧 전체 응답 속도</strong>에 영향을 줌

<a id="204eda9b0fe181e3b2adc6411a4d3169"></a>

<strong><br>2&#46;  Nginx 설정이 Jenkins 특성에 비해 과도하거나 누락</strong>

<a id="204eda9b0fe1813fac46e81c0ff36a22"></a>

```groovy
// 문제 있는 nginx.conf 설정 예
worker_processes 1;

http {
    limit_req_zone $binary_remote_addr zone=req_limit:10m rate=5r/s;

    server {
        listen 80;

        location / {
            limit_req zone=req_limit burst=10 nodelay;

            proxy_pass http://jenkins:8080;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
        }
    }
}
```

- 다음 설정들이 병목 원인으로 의심됨&#58;
    - worker&#95;processes 1 → 다중 요청 처리 병목

    - proxy&#95;buffering on(기본값) → Jenkins 스트리밍 로그에 비효율

    - limit&#95;req 과도하게 설정 → 일반 사용자 요청도 제한됨

    - client&#95;max&#95;body&#95;size 누락 → 플러그인 업로드 시 오류 유발 가능

<a id="204eda9b0fe1818482e2e3361ac0ccc4"></a>

### <strong>🔧 해결 방법 (Fix)</strong>

---

1. <strong> Docker Volume 전략 변경</strong>
    <details>
    <summary><strong>✅ 변경된 </strong><strong><code>docker&#45;compose&#46;yml</code></strong></summary>

    <a id="204eda9b0fe18168ba52fb3168c37231"></a>

    ```yaml
    version: '3.8'

    services:
      jenkins:
        image: jenkins/jenkins:2.504.2-lts
        container_name: jenkins
        restart: always
        user: root
        volumes:
          - /opt/jenkins_home:/var/jenkins_home  // Host 경로로 변경
        expose:
          - 8080
        healthcheck:
          test: ["CMD", "curl", "-f", "http://localhost:8080/login"]
          interval: 30s
          timeout: 5s
          retries: 5
          start_period: 40s

      nginx:
        image: nginx:latest
        container_name: nginx
        restart: always
        ports:
          - "80:80"
        volumes:
          - ./nginx/nginx.conf:/etc/nginx/nginx.conf:ro
        depends_on:
          jenkins:
            condition: service_healthy

    // 명시적 호스트 볼륨
    volumes:
      // 제거됨. 대신 바인드 마운트 사용
    ```

    </details>

    <details>
    <summary><br></summary>



    </details>

    - <strong>Named Volume → Host Bind Mount</strong> 방식으로 전환

    - 구성 예시&#58;
        <a id="204eda9b0fe181a0b2d9d0b556021a5c"></a>

        ```groovy
        volumes:
          - /opt/jenkins_home:/var/jenkins_home
        ```

    - 호스트에서 권한 설정&#58;
        <a id="204eda9b0fe181bd916af039379dc228"></a>

        ```groovy
        sudo mkdir -p /opt/jenkins_home
        sudo chown -R 1000:1000 /opt/jenkins_home
        ```

1. <strong>Nginx 설정 최적화</strong>
    <a id="204eda9b0fe1813984a7e4c297ed3f2c"></a>

    ```groovy
    worker_processes auto;

    events {
        worker_connections 2048;
    }

    http {
        limit_req_zone $binary_remote_addr zone=req_limit:10m rate=10r/s;

        map $http_user_agent $block_bot {
            default 0;
            ~*(curl|wget|python|Go-http-client|sqlmap) 1;
        }

        server {
            listen 80;

            location / {
                if ($block_bot) {
                    return 403;
                }

                limit_req zone=req_limit burst=20 nodelay;
                proxy_pass http://jenkins:8080;

                proxy_http_version 1.1;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

                proxy_buffering off;
                client_max_body_size 50M;
            }
        }
    }
    ```

    - proxy&#95;buffering off로 Jenkins 로그/출력이 지연 없이 반영

    - worker&#95;processes auto&#58; 멀티 코어 환경에서 성능 최적화

    - client&#95;max&#95;body&#95;size&#58; 대용량 플러그인/아티팩트 업로드 오류 방지

<a id="204eda9b0fe1813cba1feacc67ef5811"></a>

### <strong>✅  적용 결과</strong>

| <strong>항목</strong> | <strong>변경 전</strong> | <strong>변경 후</strong> |
| --- | --- | --- |
| Jenkins 초기화 시간 | 5초 이상 (Nginx 경유 시) | 1초 이내 |
| 브라우저 UI 반응 속도 | 느리고 멈추는 수준 | 실시간 반응 가능 |
| 인스턴스 리소스 사용률 | CPU/Memory 여유 있지만 느림 | 동일 자원에서 성능 완전 정상화 |

- 특히 m5&#46;large 인스턴스에서도 CPU 사용률 1% 미만에서 <strong>정상 동작 확인</strong>

- 병목 원인이 리소스 부족이 아닌 <strong>디스크 I/O 구조와 프록시 설정</strong>임을 검증

- Named Volume → 바인드 마운트, Nginx reverse proxy 최적화를 통해 해결

- Jenkins는 “실제 디스크 접근 성능”과 “스트리밍 HTTP 처리 방식”에 민감한 구조임

<a id="204eda9b0fe181c0847ec21a4cffe97f"></a>

### <strong>📑 결론</strong>

> Jenkins는 CI 도구 특성상 디스크 I/O에 민감하며, Docker 내부 볼륨 구조와 Nginx Reverse Proxy 설정은 실질적인 성능에 직접적인 영향을 미친다&#46;

- <strong>Named Volume은 빠르게 구축 가능하지만, Jenkins에는 비효율적</strong>

- <strong>Nginx는 proxy 설정이 복잡한 어플리케이션에 맞춰 세밀하게 조정되어야 한다</strong>

- 단순 스펙 업그레이드보다는, <strong>구조적 병목 원인을 먼저 파악하는 것이 핵심</strong>

<a id="204eda9b0fe181d6a984e1af7facfb41"></a>

### <strong>📚 참고 문서</strong>

- https&#58;//www&#46;jenkins&#46;io/doc/book/installing/docker/

- https&#58;//docs&#46;docker&#46;com/storage/bind&#45;mounts/

- https&#58;//docs&#46;nginx&#46;com/nginx/admin&#45;guide/web&#45;server/reverse&#45;proxy/

- https&#58;//aws&#46;amazon&#46;com/ec2/instance&#45;types/
