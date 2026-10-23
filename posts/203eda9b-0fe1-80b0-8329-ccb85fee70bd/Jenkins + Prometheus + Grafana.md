---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 203eda9b-0fe1-80b0-8329-ccb85fee70bd
title: Jenkins + Prometheus + Grafana
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817b-9c95-d96fd53640c4
    title: CI/CD
  - id: 203eda9b-0fe1-8031-8d08-c81d55a97785
    title: unity 모바일게임 Jenkins CI/CD 파이프라인 구축
  - id: 203eda9b-0fe1-80b0-8329-ccb85fee70bd
    title: Jenkins + Prometheus + Grafana
excerpt: Unity 빌드는 Jenkins Job 내부에서 따로 실행된다고 가정하고, 모니터링 환경만 도커 기반으로 완성한다. 📌 목적 - Jenkins는 /prometheus 엔드포인트를 통해 Prometheus에 메트릭을 노출 - Prometheus는 Jenkins로부터 메트릭을 수집 - Grafana는 Prometheus 데
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 203eda9b-0fe1-8031-8d08-c81d55a97785
created: 2025-05-30T08:12:58.057Z
updated: 2025-05-30T08:24:20.404Z
legacy_path: Main/CI-CD-d96fd53640c4/unity 모바일게임 Jenkins CI-CD 파이프라인 구축-c81d55a97785/Jenkins + Prometheus + Grafana-ccb85fee70bd/index.md
legacy_category: CI/CD
source_url: https://beautiful-college-c84.notion.site/203eda9b0fe180b08329ccb85fee70bd
---
<a id="203eda9b0fe1805297ebd5033b1fae4a"></a>

Unity 빌드는 Jenkins Job 내부에서 따로 실행된다고 가정하고, 모니터링 환경만 도커 기반으로 완성한다&#46;

> 📌 
> 
> <a id="203eda9b0fe1805396f3c4801891f889"></a>
> 
> <strong>목적</strong>
> 
> - Jenkins는 /prometheus 엔드포인트를 통해 Prometheus에 메트릭을 노출
> 
> - Prometheus는 Jenkins로부터 메트릭을 수집
> 
> - Grafana는 Prometheus 데이터를 시각화
> 
> - 모두 같은 Docker 네트워크에서 동작

<a id="203eda9b0fe18074adb3d13eccef33a6"></a>

<strong><br>📁 디렉토리 구조 예시</strong>

<a id="203eda9b0fe180ddbe16e2f43f6fd5b8"></a>

```yaml
monitoring/
├─ docker-compose.yml
├─ prometheus/
│   └─ prometheus.yml
```

<a id="203eda9b0fe18015be4ce03c7cc929f4"></a>

<strong><br> <br><br>📄 monitoring/docker&#45;compose&#46;yml</strong>

<a id="203eda9b0fe180c2bf44c0ea7753558f"></a>

```yaml
version: '3.8'

services:
  jenkins:
    image: jenkins/jenkins:lts
    container_name: jenkins
    ports:
      - "8080:8080"
    volumes:
      - jenkins_home:/var/jenkins_home
    networks:
      - monitoring-net

  prometheus:
    image: prom/prometheus
    container_name: prometheus
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus/prometheus.yml:/etc/prometheus/prometheus.yml
    networks:
      - monitoring-net

  grafana:
    image: grafana/grafana
    container_name: grafana
    ports:
      - "3000:3000"
    networks:
      - monitoring-net

volumes:
  jenkins_home:

networks:
  monitoring-net:
  
```

<details>
<summary><strong>🧐 compose로 구성하면 jenkins 내부에서 plugin 연동은 필요없는 건가 ?</strong></summary>

> ❌ <strong>Docker Compose로 Jenkins를 실행해도, Jenkins 내부에서 Prometheus 플러그인은 여전히 직접 설치해야 한다&#46;</strong>
> 
> <a id="203eda9b0fe180b1b6bbd71301b9caeb"></a>
> 
> 단, 플러그인을 <strong>자동으로 설치하도록 Dockerfile을 커스터마이징 해야한다&#46;</strong>

<a id="203eda9b0fe180d4a58ed5b049e9ce66"></a>

<strong>✅ 왜 Jenkins 내부 플러그인은 필요할까?</strong>

<a id="203eda9b0fe18030a7bff007b178c264"></a>

Jenkins가 Prometheus 메트릭을 <code>/prometheus</code> 엔드포인트로 노출하려면, <strong>Prometheus Metrics Plugin</strong> 이 반드시 설치되어 있어야 한다&#46;

<a id="203eda9b0fe18067b402de327f5b84af"></a>

해당 플러그인은 Jenkins의 Job 상태, 큐 상태, 빌드 시간 등을 Prometheus 형식으로 출력해주는 역할을 한다&#46;

- 아무 플러그인 없이 http&#58;//jenkins&#58;8080/prometheus 접속하면 <strong>404 오류</strong> 발생

- 즉, Jenkins가 도커로 실행되더라도 플러그인 설치는 <strong>Jenkins 내부의 작업이다&#46;</strong>

<a id="203eda9b0fe180a3a6b3da9f656ae568"></a>

<br><strong><br>✅ 해결 방법&#58; Dockerfile로 커스터마이징하여 자동 설치</strong><br><strong><br>📁 구조 예시</strong>

<a id="203eda9b0fe180d48386c5b60cd6f659"></a>

```yaml
monitoring/
├─ jenkins/
│   ├─ Dockerfile
│   └─ plugins.txt
├─ docker-compose.yml
├─ prometheus/
│   └─ prometheus.yml
```

<a id="203eda9b0fe1804ba7c1ccb596cee7cd"></a>

<strong><br>📄 jenkins/Dockerfile</strong>

<a id="203eda9b0fe1801a9708d56d6cc669f2"></a>

```docker
FROM jenkins/jenkins:lts

# Install plugins automatically
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt

RUN jenkins-plugin-cli --plugin-file /usr/share/jenkins/ref/plugins.txt
```

<a id="203eda9b0fe18000b2ded1d1797c34de"></a>

<strong><br>📄 jenkins/plugins&#46;tx</strong>

<a id="203eda9b0fe1805b98c4f58c6845656a"></a>

```docker
prometheus:2.0.10
# 다른 플러그인도 필요하면 추가 가능
```

<a id="203eda9b0fe180ea8b59f0e1b18a938d"></a>

<br><strong><br>📄 docker&#45;compose&#46;yml 수정</strong>

<a id="203eda9b0fe1804193f0d9ec8a6a83d1"></a>

```yaml
services:
  jenkins:
    build:
      context: ./jenkins
    container_name: jenkins
    ports:
      - "8080:8080"
    volumes:
      - jenkins_home:/var/jenkins_home
    networks:
      - monitoring-net
```

<a id="203eda9b0fe180a1a185ce8331ff13eb"></a>

<strong><br>✅ 실행 명령</strong>

<a id="203eda9b0fe18047ad93e1a43efc8896"></a>

```yaml
cd monitoring
docker compose up --build -d
```

> ✏️ 
> 
> <a id="203eda9b0fe180c5ac38fa767bb232fc"></a>
> 
> <code>Jenkins</code>는 <u>플러그인 기반 구조</u>이기 때문에, <strong>기능 사용을 위해서는 항상 관련 플러그인을 설치해야 한다</strong>

</details>

<a id="203eda9b0fe180fda985e6dc19f9af3b"></a>

<strong><br>📄 monitoring/prometheus/prometheus&#46;yml</strong>

<a id="203eda9b0fe1803797adf24d5cc892ae"></a>

```yaml
global:
  scrape_interval: 30s

scrape_configs:
  - job_name: 'jenkins'
    metrics_path: '/prometheus'
    static_configs:
      - targets: ['jenkins:8080']
```

<a id="203eda9b0fe1800bb6e7dca56fd86464"></a>

실행

<a id="203eda9b0fe1800faaefc5eca9067814"></a>

```yaml
cd monitoring
docker compose up -d
```

<a id="203eda9b0fe180cfb44fedb991721195"></a>

<strong><br>🔗 접속 URL</strong>

|  |  |
| --- | --- |
| <strong>서비스</strong> | <strong>URL</strong> |
| Jenkins | http&#58;//localhost&#58;8080 |
| Prometheus | http&#58;//localhost&#58;9090 |
| Grafana | http&#58;//localhost&#58;3000 (기본 ID&#58; admin / PW&#58; admin) |

<a id="203eda9b0fe180bfa624e4a932aa9e97"></a>

### <strong>🧩 Grafana 설정 요약</strong>

1. Grafana 접속 → Configuration &#62; Data Sources &#62; Add data source

1. Prometheus 선택

1. URL&#58; http&#58;//prometheus&#58;9090

1. Save &#38; Test

1. 좌측 &#43; &#62; Import → Dashboard ID 9964 입력

<a id="203eda9b0fe180f2b1d9c65ae52a71e0"></a>

→ Jenkins 메트릭이 실시간 대시보드로 표시됩니다&#46;
