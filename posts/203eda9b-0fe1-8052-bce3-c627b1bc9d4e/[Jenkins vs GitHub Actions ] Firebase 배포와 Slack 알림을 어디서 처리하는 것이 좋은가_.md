---
order: 1
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 203eda9b-0fe1-8052-bce3-c627b1bc9d4e
title: "[Jenkins vs GitHub Actions ] Firebase 배포와 Slack 알림을 어디서 처리하는 것이 좋은가?"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817b-9c95-d96fd53640c4
    title: CI/CD
  - id: 203eda9b-0fe1-8031-8d08-c81d55a97785
    title: unity 모바일게임 Jenkins CI/CD 파이프라인 구축
  - id: 203eda9b-0fe1-8052-bce3-c627b1bc9d4e
    title: "[Jenkins vs GitHub Actions ] Firebase 배포와 Slack 알림을 어디서 처리하는 것이 좋은가?"
excerpt: Unity로 만든 모바일 게임을 Android에 배포하는 자동화 시스템을 구축을 하고 있다 . 그러면서 아래와 같은 고민점이 생겼다. 🧐 Firebase 배포와 Slack 알림을 Jenkins에서 처리하는게 좋을까? 아니면 GitHub Actions로 넘기는 게 좋을까? 결론 먼저 Firebase 배포와 Slack 알림
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 203eda9b-0fe1-8031-8d08-c81d55a97785
created: 2025-05-30T07:59:52.529Z
updated: 2025-05-30T08:07:00.286Z
legacy_path: Main/CI-CD-d96fd53640c4/unity 모바일게임 Jenkins CI-CD 파이프라인 구축-c81d55a97785/[Jenkins vs GitHub Actions ] Firebase 배포와 Sla-c627b1bc9d4e/index.md
legacy_category: CI/CD
source_url: https://beautiful-college-c84.notion.site/203eda9b0fe18052bce3c627b1bc9d4e
---
<a id="203eda9b0fe18028b73fdc763ebd8e80"></a>

Unity로 만든 모바일 게임을 Android에 배포하는 자동화 시스템을 구축을 하고 있다 &#46;

<a id="203eda9b0fe180ce8965d7f1253c7403"></a>

그러면서 아래와 같은 고민점이 생겼다&#46; 

> 🧐 
> 
> <a id="203eda9b0fe180a39090cf611c7120f2"></a>
> 
> Firebase 배포와 Slack 알림을 Jenkins에서 처리하는게 좋을까?
> 
> <a id="203eda9b0fe1804cb70ade60ebb89af6"></a>
> 
> 아니면 GitHub Actions로 넘기는 게 좋을까?

<a id="203eda9b0fe180d8aa46cadb96767770"></a>

### 결론 먼저

<a id="203eda9b0fe180a7bd89fe53b44c8bbc"></a>

Firebase 배포와 Slack 알림은 <strong>GitHub Actions에서 처리하는 것이 실무적으로 더 적합하다&#46;</strong>

<a id="203eda9b0fe1802eb3ace880167cedaa"></a>

### 시스템 아키텍처

<a id="203eda9b0fe180148263ddff55e1150c"></a>

```yaml
GitHub (Unity 프로젝트)
↓
GitHub Actions
├─ Slack 알림 (빌드 시작)
├─ Jenkins Unity Build 트리거
└─ Firebase 배포 트리거 (repository_dispatch)
↓
Jenkins (EC2)
├─ Unity Android 빌드
├─ APK → S3 업로드
├─ Prometheus 메트릭 노출
└─ GitHub Actions 호출 (배포 지시)
↓
GitHub Actions (firebase_deploy)
├─ Firebase App Distribution
└─ Slack 알림 (성공/실패)
```

<a id="203eda9b0fe180269fbee615bb31c9f6"></a>

### ✅ 왜 GitHub Actions에서 Firebase 배포를 처리하는가?

<details>
<summary>1&#46; 보안 관리가 용이</summary>

- Firebase Token, Slack Webhook 등을 <strong>GitHub Secrets에서 안전하게 관리</strong> 가능

- Jenkins는 EC2에 직접 토큰을 보관해야 하므로 <strong>보안 이슈 발생 가능성 높음</strong>

</details>

<details>
<summary>2&#46; SaaS 연동에 특화된 GitHub Actions</summary>

|  |  |
| --- | --- |
| 서비스 | GitHub Actions 지원 |
| Firebase | ✅ 공식 액션 존재 (<code>wzieba/Firebase&#45;Distribution&#45;Github&#45;Action</code>) |
| Slack | ✅ 공식 액션 존재 (<code>8398a7/action&#45;slack</code>) |
| Google Play | ✅ <code>r0adkll/upload&#45;google&#45;play</code> 등 활용 가능 |

<a id="203eda9b0fe180228c43ed81bc7260a8"></a>

→ Jenkins는 대부분 스크립트 또는 별도 플러그인 의존 (관리 복잡도 ↑)

</details>

<details>
<summary>3&#46; CI (빌드) 와 CD (배포)의 분리 가능</summary>

- Jenkins = 빌드와 테스트 (CI)에 집중

- GitHub Actions = 배포와 통합 알림 (CD)에 집중
    <a id="203eda9b0fe1802f95c5fa1c68452e5f"></a>

    → 책임 명확, 실패 원인 추적 쉬움

</details>

<details>
<summary>4&#46; 경량 배포 트리거에 적합</summary>

- GitHub Actions는 빠르고 리소스 걱정 없음

- Jenkins는 빌드 큐, 에이전트 리소스, 병렬 실행 등 부담 있음

</details>

<details>
<summary>5&#46; Slack 알림도 Actions가 훨씬 단순</summary>

<a id="203eda9b0fe18021b412f65c905dfa0c"></a>

```yaml
- name: Slack Notification
  uses: 8398a7/action-slack@v3
  with:
    status: success
  env:
    SLACK_WEBHOOK_URL: ${{ secrets.SLACK_WEBHOOK }}
```

<a id="203eda9b0fe1802d84a8db2a92f11981"></a>

→ Jenkins에서는 Webhook 설정 &#43; 플러그인 설치 &#43; job 구성 필요

</details>

<a id="203eda9b0fe180909cb5d36af31b7ee5"></a>

<strong><br></strong>

<a id="203eda9b0fe180babebfd200f96324c6"></a>

### <strong>❓ 그냥 Jenkins에서 다 처리하면 안 되는가?</strong>

|  |  |  |
| --- | --- | --- |
| <strong>항목</strong> | <strong>Jenkins에서 처리</strong> | <strong>GitHub Actions에서 분리</strong> |
| 유지보수 | ❌ 복잡 | ✅ 단순 |
| 보안 관리 | ❌ EC2에 키 저장 | ✅ GitHub Secrets 사용 |
| SaaS 연동 | ❌ 직접 구현 | ✅ 공식 액션으로 간단 처리 |
| 실패 원인 추적 | ❌ 파이프라인 혼합 | ✅ CI/CD 분리로 명확 |
| 리소스 관리 | ❌ Jenkins 빌드 큐 소모 | ✅ GitHub Actions에서 분산 처리 |

<a id="203eda9b0fe180dc9e38e306f5ddf78c"></a>

### <strong>✅ 실무 결론</strong>

- <code>Jenkins</code>는 <strong>무거운 빌드, 테스트, 모니터링</strong>에 집중

- <code>GitHub Actions</code>는 <strong>SaaS 연동, Slack 알림, Firebase 배포</strong> 등 <strong>경량 CD</strong>에 특화

<a id="203eda9b0fe180518d16d0fa5c6442dc"></a>

이 둘을 <strong>하이브리드로 조합하면 유지보수성과 생산성이 모두 향상된다&#46;</strong>

<a id="203eda9b0fe1807db7cbd530a730f0d0"></a>

### <strong>🔗 참고 링크</strong>

- <a href="https://github.com/wzieba/Firebase-Distribution-Github-Action">GitHub Actions Firebase 배포 액션</a>

- <a href="https://github.com/8398a7/action-slack">Slack Notification GitHub Action</a>

- <a href="https://www.jenkins.io/doc/book/using/remote-access-api/">Jenkins Remote API</a>

- <a href="https://circleci.com/blog/github-actions-vs-jenkins/">Jenkins vs GitHub Actions</a>
