---
order: 3
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 203eda9b-0fe1-80d5-a8f0-eaf556d5e7f5
title: DevOps 템플릿 프로젝트
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 206eda9b-0fe1-8063-9f3b-f5406da4ca5b
    title: Nginx
  - id: 203eda9b-0fe1-80df-8b2e-d73c44927eb7
    title: 비전공자도 이해할 수 있는 Nginx 입문/실전
  - id: 203eda9b-0fe1-80d5-a8f0-eaf556d5e7f5
    title: DevOps 템플릿 프로젝트
excerpt: "ecs-devops-template.zip 📁 포함된 주요 파일 - .env.sample: 환경변수 샘플 - docker-compose.yml: 전체 서비스 정의 - backend/Dockerfile: 백엔드 컨테이너 설정 - nginx/nginx.conf: 프록시 + HTTPS + API 프록시 - monitoring"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 203eda9b-0fe1-80df-8b2e-d73c44927eb7
created: 2025-05-30T15:06:17.673Z
updated: 2025-06-12T11:13:50.261Z
legacy_path: Main/Nginx-f5406da4ca5b/비전공자도 이해할 수 있는 Nginx 입문-실전-d73c44927eb7/DevOps 템플릿 프로젝트-eaf556d5e7f5/index.md
legacy_category: Nginx
source_url: https://beautiful-college-c84.notion.site/203eda9b0fe180d5a8f0eaf556d5e7f5
---
[ecs-devops-template.zip](84c689b7c105303b.zip)

> 📁 
> 
> <a id="203eda9b0fe180559292f12c00a109bd"></a>
> 
> <strong>포함된 주요 파일</strong>
> 
> - &#46;env&#46;sample&#58; 환경변수 샘플
> 
> - docker&#45;compose&#46;yml&#58; 전체 서비스 정의
> 
> - backend/Dockerfile&#58; 백엔드 컨테이너 설정
> 
> - nginx/nginx&#46;conf&#58; 프록시 &#43; HTTPS &#43; API 프록시
> 
> - monitoring/&#58; Prometheus &#43; Grafana 설정
> 
> - alertmanager/alertmanager&#46;yml&#58; Slack 알림 설정
> 
> - &#46;github/workflows/deploy&#46;yml&#58; CI/CD 파이프라인
> 
> - appspec&#46;yaml, taskdef&#46;json&#58; AWS ECS 배포 설정
> 
> - README&#46;md&#58; 전체 문서 가이드

<a id="203eda9b0fe180879cdbfd8dff04e1b0"></a>

<strong><br>디렉토리 구조 정리</strong>

<a id="203eda9b0fe180eaa71ac93f9711c2f1"></a>

```yaml
ecs-devops-template/
├── .env.sample
├── docker-compose.yml
├── backend/
│   └── Dockerfile
├── nginx/
│   ├── nginx.conf
│   └── certbot/
├── monitoring/
│   ├── prometheus.yml
│   ├── rules.yml
│   └── grafana-dashboard.json
├── alertmanager/
│   └── alertmanager.yml
├── .github/
│   └── workflows/
│       └── deploy.yml
├── appspec.yaml
├── taskdef.json
└── README.md
```

<a id="203eda9b0fe180239f63db27eee7b7c5"></a>

<strong><br>README&#46;md 예시</strong>

<a id="203eda9b0fe180ae9808eacf212f16b2"></a>

```yaml
# AWS ECS + Docker 기반 DevOps 템플릿

이 템플릿은 다음 기능을 제공합니다:

- [x] ECS + CodeDeploy 기반 Blue/Green 배포
- [x] GitHub Actions 기반 CI/CD 자동화
- [x] Let's Encrypt HTTPS 자동 발급
- [x] Prometheus + Grafana 모니터링
- [x] Slack AlertManager 알림 연동
- [x] Nginx 리버스 프록시 설정
- [x] .env 파일 기반 환경변수 관리

## 사용 방법

1. `Use this template` 버튼 클릭
2. `.env.sample`을 복사해 `.env` 파일 생성
3. GitHub Secrets에 다음 항목 추가:
   - `EC2_HOST`
   - `EC2_SSH_KEY`
   - `AWS_ACCESS_KEY_ID`
   - `AWS_SECRET_ACCESS_KEY`
4. `docker-compose up -d` 로 로컬 테스트 가능

## 디렉토리 구조

- `backend/`: Spring 또는 Node 백엔드
- `nginx/`: 리버스 프록시 + HTTPS
- `monitoring/`: Prometheus 설정
- `alertmanager/`: 슬랙 경고 설정
- `.github/workflows`: GitHub Actions CI/CD

```
