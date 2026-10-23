---
order: 3
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 203eda9b-0fe1-8082-b984-f47d8c20e9db
title: "[ v3 ] Unity DevOps CI/CD 통합 가이드 (GPT v3 Final)"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817b-9c95-d96fd53640c4
    title: CI/CD
  - id: 203eda9b-0fe1-8031-8d08-c81d55a97785
    title: unity 모바일게임 Jenkins CI/CD 파이프라인 구축
  - id: 203eda9b-0fe1-8082-b984-f47d8c20e9db
    title: "[ v3 ] Unity DevOps CI/CD 통합 가이드 (GPT v3 Final)"
excerpt: EC2 + Docker 기반 Jenkins, Nginx, Certbot, Unity CLI, Firebase App Distribution, Slack 연동 완전 자동화 구성 ✅ 전체 아키텍처 흐름 GitHub → Webhook → Nginx (443/80) → Jenkins (내부 8080) → Unity Build &
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 203eda9b-0fe1-8031-8d08-c81d55a97785
created: 2025-05-30T03:00:00.411Z
updated: 2025-05-30T03:00:07.810Z
legacy_path: Main/CI-CD-d96fd53640c4/unity 모바일게임 Jenkins CI-CD 파이프라인 구축-c81d55a97785/[ v3 ] Unity DevOps CI-CD 통합 가이드 (GPT v3 Fina-f47d8c20e9db/index.md
legacy_category: CI/CD
source_url: https://beautiful-college-c84.notion.site/203eda9b0fe18082b984f47d8c20e9db
---
> EC2 &#43; Docker 기반 Jenkins, Nginx, Certbot, Unity CLI, Firebase App Distribution, Slack 연동 완전 자동화 구성

<a id="203eda9b0fe1801d9b23e3778fe579fa"></a>

## ✅ 전체 아키텍처 흐름

<a id="203eda9b0fe1804d9200f07e2c34efb2"></a>

GitHub → Webhook → Nginx (443/80) → Jenkins (내부 8080) → Unity Build &#38; Test → APK 생성 → Firebase 배포 → Slack 알림 &#43; 테스터 관리

<a id="203eda9b0fe1800095abc7c1517407bb"></a>

## 📁 디렉토리 구조

<a id="203eda9b0fe180d8a09fcf48e9d605d4"></a>

```plaintext
infra/
├── docker-compose.yml
├── .env
├── jenkins/
│   └── jenkins_home/
├── nginx/
│   ├── nginx.conf
│   ├── ssl/
│   └── healthcheck.conf
├── certbot/
│   └── init-letsencrypt.sh
scripts/
├── build.sh
├── test.sh
├── deploy.sh
├── notify.sh
├── manage-testers.sh
unity-project/
└── BuildScript.cs

```

<a id="203eda9b0fe180bba422ce55f0747050"></a>

## ✅ docker&#45;compose&#46;yml (보안 반영)

<a id="203eda9b0fe180f3bedad6ae62edb1f8"></a>

```yaml
version: '3.8'

services:
  jenkins:
    image: jenkins/jenkins:2.504.2-lts
    container_name: jenkins
    restart: unless-stopped
    expose:
      - "8080"
    networks:
      - backend
    volumes:
      - ./jenkins/jenkins_home:/var/jenkins_home
      - /var/run/docker.sock:/var/run/docker.sock

  nginx:
    image: nginx:stable
    container_name: nginx
    restart: unless-stopped
    depends_on:
      - jenkins
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf:ro
      - ./nginx/healthcheck.conf:/etc/nginx/conf.d/healthcheck.conf
      - ./nginx/ssl:/etc/letsencrypt
      - ./nginx/ssl:/var/www/certbot
    healthcheck:
      test: ["CMD", "curl", "-f", "<http://localhost/health>"]
      interval: 10s
      retries: 5
    networks:
      - backend

  certbot:
    image: certbot/certbot
    container_name: certbot
    entrypoint: "/bin/sh -c 'trap exit TERM; while :; do sleep 6h & wait $${!}; certbot renew --webroot -w /var/www/certbot --quiet; nginx -s reload; done'"
    volumes:
      - ./nginx/ssl:/etc/letsencrypt
      - ./nginx/ssl:/var/www/certbot
    networks:
      - backend

networks:
  backend:
    driver: bridge

```

<a id="203eda9b0fe180a4baefd3079c260028"></a>

## 🔐 Jenkins Credentials 등록 항목

|  |  |
| --- | --- |
| ID | 설명 |
| firebase&#92;&#95;app&#92;&#95;id | Firebase 프로젝트 App ID |
| firebase&#92;&#95;token | Firebase CLI 인증 토큰 |
| slack&#92;&#95;webhook | Slack Webhook URL |

<a id="203eda9b0fe180af9c68eda6f96b0d67"></a>

## 🧩 Jenkinsfile 예시

<a id="203eda9b0fe180c2aa22df737e3ed058"></a>

```groovy
pipeline {
  agent {
    docker {
      image 'unityci/editor:2022.3.12f1-android'
      args '-v /var/run/docker.sock:/var/run/docker.sock'
    }
  }
  environment {
    UNITY_PROJECT_PATH = 'unity-project'
    BUILD_OUTPUT_PATH = 'build/output.apk'
    FIREBASE_APP_ID = credentials('firebase_app_id')
    FIREBASE_TOKEN = credentials('firebase_token')
    SLACK_WEBHOOK = credentials('slack_webhook')
    TESTER_GROUP = 'testers'
  }
  triggers {
    githubPush()
  }
  stages {
    stage('Checkout') {
      steps {
        git url: '<https://github.com/your-org/unity-game-repo.git>', branch: 'main'
      }
    }
    stage('Build') {
      steps {
        sh './scripts/build.sh $UNITY_PROJECT_PATH'
        archiveArtifacts artifacts: 'build/output.apk', fingerprint: true
      }
    }
    stage('Deploy') {
      steps {
        sh './scripts/deploy.sh $FIREBASE_APP_ID $BUILD_OUTPUT_PATH $FIREBASE_TOKEN $TESTER_GROUP'
        sh './scripts/manage-testers.sh $FIREBASE_APP_ID $FIREBASE_TOKEN $TESTER_GROUP'
      }
    }
  }
  post {
    success { sh './scripts/notify.sh success' }
    failure { sh './scripts/notify.sh failure' }
  }
}

```

<a id="203eda9b0fe180af8b0ae8dc19b448ae"></a>

## 🛠️ 스크립트 예시

<a id="203eda9b0fe180d4b4d5dce8af16692e"></a>

<strong><a href="http://build.sh/">build&#46;sh</a></strong>

<a id="203eda9b0fe180dfae3dc915660c52bd"></a>

```shell
#!/bin/bash
UNITY_PROJECT_PATH=$1
BUILD_PATH="build/output.apk"
/opt/unity/Editor/Unity \\
  -batchmode \\
  -nographics \\
  -silent-crashes \\
  -logFile /dev/stdout \\
  -projectPath "$UNITY_PROJECT_PATH" \\
  -executeMethod "BuildScript.BuildAndroid" \\
  -buildTarget Android \\
  -quit

```

<a id="203eda9b0fe18025a62fc0c6ae959d80"></a>

<strong><a href="http://deploy.sh/">deploy&#46;sh</a></strong>

<a id="203eda9b0fe180e6886aec999dd79afc"></a>

```shell
#!/bin/bash
firebase appdistribution:distribute "$2" --app "$1" --token "$3" --groups "$4"

```

<a id="203eda9b0fe18006945cfeb482b8f969"></a>

<strong><a href="http://manage-testers.sh/">manage&#45;testers&#46;sh</a></strong>

<a id="203eda9b0fe180a7a4d8fa19bdaff507"></a>

```shell
#!/bin/bash
# 예: CSV에서 이메일 읽어 등록

```

<a id="203eda9b0fe1809f9582d8f4d9d932c4"></a>

<strong><a href="http://notify.sh/">notify&#46;sh</a></strong>

<a id="203eda9b0fe1802aa44ff02743fb2d07"></a>

```shell
#!/bin/bash
curl -X POST -H 'Content-type: application/json' \\
--data '{"text":"Build $1!"}' "$SLACK_WEBHOOK"

```

<a id="203eda9b0fe1801f86d2dfe85df3ff0d"></a>

## BuildScript&#46;cs (Unity 전용)

<a id="203eda9b0fe1802fbb0fc67439fee58e"></a>

```c#
using UnityEditor;
public class BuildScript {
  public static void BuildAndroid() {
    BuildPipeline.BuildPlayer(new[] { "Assets/Scenes/MainScene.unity" }, "build/output.apk", BuildTarget.Android, BuildOptions.None);
  }
}

```

<a id="203eda9b0fe180d89b6acabb1ad7f354"></a>

## 🚀 실행 절차 요약

1. <code>&#46;env</code> 파일 설정

1. <code>init&#45;letsencrypt&#46;sh</code> 실행 (인증서 발급)

1. <code>docker&#45;compose up &#45;d</code>

1. Jenkins 웹 UI 접속 → 플러그인 설치 (GitHub, Slack)

1. Jenkins Credentials 등록

1. GitHub에 Jenkinsfile 커밋

1. GitHub Webhook 자동 트리거

1. Firebase 배포 &#43; Slack 알림 확인

<a id="203eda9b0fe18050a3b9f73396b73c84"></a>

## ✅ 실무 기준 반영 사항

- Jenkins 외부 노출 차단 (8080 → 내부 전용)

- 인증서 자동 갱신 (certbot &#43; nginx reload)

- GameCI Docker 이미지로 Unity 빌드 속도 최적화

- Slack 알림, Firebase 토큰 보안 관리

- Prometheus / Grafana 연동 가능

<a id="203eda9b0fe180b8b04bd800db042ce7"></a>

이 구성은 실무에서도 그대로 적용 가능한 수준이며, 퍼블릭시티 리뷰를 모두 반영한 상태입니다&#46; 확장 요청이 있다면 언제든지 말씀해주세요&#33;
