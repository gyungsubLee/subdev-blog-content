---
order: 4
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 203eda9b-0fe1-8099-9b1f-c7f557aec443
title: docker compose로 Nginx 실행
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 206eda9b-0fe1-8063-9f3b-f5406da4ca5b
    title: Nginx
  - id: 203eda9b-0fe1-80df-8b2e-d73c44927eb7
    title: 비전공자도 이해할 수 있는 Nginx 입문/실전
  - id: 203eda9b-0fe1-8099-9b1f-c7f557aec443
    title: docker compose로 Nginx 실행
excerpt: "yaml version: '3.8' services: nginx: image: nginx:stable containername: nginx restart: always ports: - \"80:80\" - \"443:443\" volumes: - ./nginx/nginx.conf:/etc/nginx/nginx.conf:ro ro"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 203eda9b-0fe1-80df-8b2e-d73c44927eb7
created: 2025-05-30T14:41:11.395Z
updated: 2025-06-12T11:13:50.261Z
legacy_path: Main/Nginx-f5406da4ca5b/비전공자도 이해할 수 있는 Nginx 입문-실전-d73c44927eb7/docker compose로 Nginx 실행-c7f557aec443/index.md
legacy_category: Nginx
source_url: https://beautiful-college-c84.notion.site/203eda9b0fe180999b1fc7f557aec443
---
<a id="203eda9b0fe180e591caca6a050a9cff"></a>

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
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf:ro       # ro: readOnly
      # - ./static:/usr/share/nginx/html:ro               # 정적 파일 서빙
      # - ./nginx/certs:/etc/nginx/certs:ro               # SSL 인증서
    depends_on:
      - backend

  backend:
    image: your-backend-image    # ex: junhyunny/my-spring-app
    container_name: backend
    restart: always
    ports:
      - "8080:8080"              # 내부 통신용
    environment:
      - SPRING_PROFILES_ACTIVE=prod
```

- nginx&#46;conig
