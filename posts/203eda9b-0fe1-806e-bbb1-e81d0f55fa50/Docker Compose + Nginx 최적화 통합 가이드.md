---
order: 2
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 203eda9b-0fe1-806e-bbb1-e81d0f55fa50
title: Docker Compose + Nginx 최적화 통합 가이드
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 206eda9b-0fe1-8063-9f3b-f5406da4ca5b
    title: Nginx
  - id: 203eda9b-0fe1-80df-8b2e-d73c44927eb7
    title: 비전공자도 이해할 수 있는 Nginx 입문/실전
  - id: 203eda9b-0fe1-806e-bbb1-e81d0f55fa50
    title: Docker Compose + Nginx 최적화 통합 가이드
excerpt: 1. 파일 구조 yaml your-project/ ├── docker-compose.yml ├── nginx/ │ ├── nginx.conf │ ├── certs/ │ │ ├── fullchain.pem │ │ └── privkey.pem │ └── logs/ 로그 디렉토리 (마운트됨) ├── static/ │ └── i
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 203eda9b-0fe1-80df-8b2e-d73c44927eb7
created: 2025-05-30T14:47:22.697Z
updated: 2025-06-12T11:13:50.261Z
legacy_path: Main/Nginx-f5406da4ca5b/비전공자도 이해할 수 있는 Nginx 입문-실전-d73c44927eb7/Docker Compose + Nginx 최적화 통합 가이드-e81d0f55fa50/index.md
legacy_category: Nginx
source_url: https://beautiful-college-c84.notion.site/203eda9b0fe1806ebbb1e81d0f55fa50
---
<a id="203eda9b0fe180299adcc652db7a1482"></a>

1&#46; 파일 구조

<a id="203eda9b0fe180dab830f9a6eb730392"></a>

```yaml
your-project/
├── docker-compose.yml
├── nginx/
│   ├── nginx.conf
│   ├── certs/
│   │   ├── fullchain.pem
│   │   └── privkey.pem
│   └── logs/                  # 로그 디렉토리 (마운트됨)
├── static/
│   └── index.html
└── backend/
    ├── Dockerfile
    └── (Spring 소스 코드 등)
```

1. docker&#45;compose&#46;yml

<a id="203eda9b0fe18085bf07d20e9c3414a5"></a>

```yaml
version: '3.8'

services:
  nginx:
    image: nginx:stable
    container_name: nginx
    restart: always
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf:ro
      - ./static:/usr/share/nginx/html:ro
      - ./nginx/certs:/etc/nginx/certs:ro
      - ./nginx/logs:/var/log/nginx
    depends_on:
      backend:
        condition: service_healthy
    networks:
      - frontend

  backend:
    image: your-backend-image   # 예: junhyunny/my-spring-app
    container_name: backend
    restart: always
    ports:
      - "8080:8080"              # 필요시 외부 접근 허용, 내부만 사용시 expose로 변경 가능
    environment:
      - SPRING_PROFILES_ACTIVE=prod
    healthcheck:
			test: ["CMD", "curl", "--fail", "--silent", "--connect-timeout", "5", "http://localhost:8080/actuator/health"]
      interval: 30s
      timeout: 10s
      retries: 3
    networks:
      - frontend

networks:
  frontend:
    driver: bridge
```

1. nginx&#46;conf

<a id="203eda9b0fe1802388e5f899d0d8f7bc"></a>

```yaml
worker_processes auto;

events {
    worker_connections 1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile      on;

    # Gzip 압축
    gzip on;
    gzip_types text/plain text/css application/json application/javascript text/xml application/xml text/javascript;

    # 캐시 처리 (정적 리소스)
    open_file_cache max=1000 inactive=20s;
    open_file_cache_valid 30s;
    open_file_cache_min_uses 2;
    open_file_cache_errors on;

    # HTTP → HTTPS 리디렉션
    server {
        listen 80;
        server_name localhost;
        return 301 https://$host$request_uri;
    }

    # HTTPS 메인 서버
    server {
        listen 443 ssl http2;
        server_name localhost;

        ssl_certificate     /etc/nginx/certs/fullchain.pem;
        ssl_certificate_key /etc/nginx/certs/privkey.pem;

        location / {
            root   /usr/share/nginx/html;
            index  index.html;
            try_files $uri $uri/ /index.html;  # SPA 라우팅 대응
        }

        location /api/ {
            rewrite ^/api(/.*)$ $1 break;      # prefix 유지
            proxy_pass http://backend:8080;
            proxy_http_version 1.1;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }

        location ~* \.(js|css|png|jpg|jpeg|gif|ico|svg)$ {
            expires 7d;
            add_header Cache-Control "public";
        }
    }
}
```

|  |  |  |
| --- | --- | --- |
| <strong>항목</strong> | <strong>Perplexity 예제</strong> | <strong>개선된 버전 (GPT)</strong> |
| API 경로 proxy | /api/ → /로 prefix 손실 | rewrite로 prefix 유지 |
| gzip 압축 | ❌ 없음 | ✅ 실무에서 필수 적용 |
| 정적 파일 캐싱 | ❌ 없음 | ✅ Cache&#45;Control, expires |
| HTTP/2 지원 | ❌ 없음 | ✅ listen 443 ssl http2; |
| healthcheck | 기본 curl만 | &#45;&#45;silent, &#45;&#45;connect&#45;timeout 추가 |
| 로그 디렉토리 | 폴더 유무 확인 안됨 | &#58;rw 권한 명시 및 폴더 구성 제안 |
| SPA 지원 | ❌ 없음 | ✅ try&#95;files &#36;uri /index&#46;html |
| 설정 유효성 검사 | ❌ 없음 | 📌 운영 시 nginx &#45;t 필수 검증 필요 |

<a id="203eda9b0fe18005a036e46ff6fb0e1a"></a>

 주요 피드백 반영 포인트

- 네트워크 분리&#58; 서비스 간 네트워크를 명시적으로 분리하여 관리 및 보안 강화

- HTTP → HTTPS 자동 리다이렉트&#58; 80포트 접속 시 443으로 리다이렉트하여 보안 강화

- 워커 프로세스 자동화&#58; <code>worker&#95;processes auto;</code>로 CPU 코어 수에 맞춰 성능 최적화

- 백엔드 health check&#58; 백엔드 서비스가 실제로 준비될 때까지 nginx가 대기

- 로그 볼륨 마운트&#58; nginx 로그를 외부에서 확인할 수 있도록 볼륨 마운트

- 정적 파일, 인증서, 설정 파일 볼륨 마운트&#58; 변경사항 반영이 쉽고, 읽기 전용으로 보안 강화

1. 실행 방법
    1. 필요한 파일 준비
        - <code>nginx/certs/fullchain&#46;pem</code>, <code>nginx/certs/privkey&#46;pem</code> (SSL 인증서)

        - <code>static/</code> 디렉토리 (정적 파일)

        - <code>nginx/nginx&#46;conf</code> (위 예시 참고)

        - <code>docker&#45;compose&#46;yml</code> (위 예시 참고)

    1. 실행
        <a id="203eda9b0fe1801ca294d3d275bde750"></a>

        ```yaml
        docker-compose up -d
        ```

    1. 확인
        - 브라우저에서 <code>https&#58;//localhost</code> 접속 시 정적 파일 서빙 확인

        - <code>https&#58;//localhost/api/</code> 접속 시 백엔드 프록시 확인

<a id="203eda9b0fe180229cebf4dba895c41b"></a>

<br><br><br>• Jenkins나 CI/CD에서 자동 배포 시 Nginx 핫 리로드 방법<br>
