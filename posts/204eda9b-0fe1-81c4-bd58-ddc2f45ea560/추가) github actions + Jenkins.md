---
order: 7
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 204eda9b-0fe1-81c4-bd58-ddc2f45ea560
title: 추가) github actions + Jenkins
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817b-9c95-d96fd53640c4
    title: CI/CD
  - id: 203eda9b-0fe1-80d5-8c37-c693a491e2cd
    title: 애플리케이션 배포 자동화와 CI/CD -Jenkins
  - id: 204eda9b-0fe1-81c4-bd58-ddc2f45ea560
    title: 추가) github actions + Jenkins
excerpt: 🧱 아키텍처 bash [GitHub] --- push / pr 등 이벤트 발생 | | Webhook ▼ [GitHub Actions] ├─ Slack 알림 ├─ Firebase App Distribution ├─ Code Signing, APK upload └─ Jenkins 트리거 (REST API) | ▼ [Jenk
cover: null
icon: null
notionProperties:
  상태: 작성 중
schema_version: 1
parent_id: 203eda9b-0fe1-80d5-8c37-c693a491e2cd
created: 2025-05-31T10:36:46.770Z
updated: 2025-05-31T10:36:46.770Z
legacy_path: Main/CI-CD-d96fd53640c4/애플리케이션 배포 자동화와 CI-CD -Jenkins-c693a491e2cd/추가) github actions + Jenkins-ddc2f45ea560/index.md
legacy_category: CI/CD
source_url: https://beautiful-college-c84.notion.site/204eda9b0fe181c4bd58ddc2f45ea560
---
<a id="204eda9b0fe1815293bcd19419b2b78a"></a>

<strong><br>🧱 아키텍처</strong>

<a id="204eda9b0fe181a7953ac8dc86f12caf"></a>

```bash
[GitHub]  --- push / pr 등 이벤트 발생
   |
   | Webhook
   ▼
[GitHub Actions]
   ├─ Slack 알림
   ├─ Firebase App Distribution
   ├─ Code Signing, APK upload
   └─ Jenkins 트리거 (REST API)
                         |
                         ▼
                  [Jenkins 서버]
                  ├─ 대규모 빌드
                  ├─ 테스트 실행
                  └─ 모니터링 / 상태 집계
```

| <strong>구분</strong> | <strong><code>Jenkins</code></strong> | <strong><code>GitHub Actions</code></strong> |
| --- | --- | --- |
| <strong>주요 목적</strong> | 무거운 빌드, 통합 테스트, 모니터링 | 경량 자동화, 이벤트 알림, Firebase 등 외부 연동 |
| <strong>모니터링</strong> | Prometheus, Grafana, Email 등 | ❌ (기본 미지원) |
| <strong>Slack 연동</strong> | 가능 (복잡, 별도 플러그인 필요) | 매우 간단 (action&#45;slack 사용) |
| <strong>Webhooks</strong> | 수신 가능 (GitHub → Jenkins) | 송신 가능 (Slack, S3, Firebase) |
| <strong>배포 자동화</strong> | 가능 (EC2, S3, EKS, etc) | 가능 (Firebase, Play Store, Vercel 등) |

<a id="204eda9b0fe1815d87ebd4eaf8e0cbbf"></a>

### 연동 예시&#58; Github Actions → Jenkins 트리거 

<a id="204eda9b0fe181b495e0ec81471f6374"></a>

```yaml
# .github/workflows/deploy.yml
name: Trigger Jenkins

on:
  push:
    branches: [ main ]

jobs:
  trigger-jenkins:
    runs-on: ubuntu-latest
    steps:
      - name: Trigger Jenkins Build
        run: |
          curl -X POST "http://jenkins.example.com/job/my-job/buildWithParameters" \
            --user "${{ secrets.JENKINS_USER }}:${{ secrets.JENKINS_TOKEN }}" \
            --data "param1=value1&param2=value2"
```

> <strong>Jenkins → Slack / Firebase 알림은 GitHub Actions로 넘기기</strong>

- Jenkins 빌드 스크립트 내부에서 GitHub Actions를 repository&#95;dispatch로 호출
    <a id="204eda9b0fe1810fba11df73add289c2"></a>

    ```bash
    curl -X POST https://api.github.com/repos/OWNER/REPO/dispatches \
      -H "Accept: application/vnd.github+json" \
      -H "Authorization: Bearer $GITHUB_TOKEN" \
      -d '{"event_type":"firebase_deploy","client_payload":{"version":"1.2.3"}}'
    ```

- 그리고 GitHub Actions에서는 다음과 같이 Slack &#43; Firebase 처리&#58;
    <a id="204eda9b0fe181ef93e9e0784258ccf0"></a>

    ```yaml
    on:
      repository_dispatch:
        types: [firebase_deploy]

    jobs:
      deploy:
        runs-on: ubuntu-latest
        steps:
          - name: Notify Slack
            uses: 8398a7/action-slack@v3
            with:
              status: custom
              fields: workflow,job,commit
            env:
              SLACK_WEBHOOK_URL: ${{ secrets.SLACK_WEBHOOK }}

          - name: Upload to Firebase
            uses: wzieba/Firebase-Distribution-Github-Action@v1
            with:
              appId: ${{ secrets.FIREBASE_APP_ID }}
              token: ${{ secrets.FIREBASE_TOKEN }}
              groups: testers
              file: ./build/app-release.apk
    ```
