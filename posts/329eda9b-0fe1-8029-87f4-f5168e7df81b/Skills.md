---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 329eda9b-0fe1-8029-87f4-f5168e7df81b
title: Skills
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 305eda9b-0fe1-80cb-881b-e0f1ba2b631b
    title: Tool
  - id: 329eda9b-0fe1-8021-834c-d75821a7b099
    title: Antigravity
  - id: 329eda9b-0fe1-8029-87f4-f5168e7df81b
    title: Skills
excerpt: --- ⚠️ 안티그래비티 스킬을 관리하기 위해 주로 사용하는 CLI 도구는 Gemini CLI 혹은 커뮤니티에서 널리 쓰이는 skills CLI이다. | | | | --- | --- | | 명령어 | 설명 | | npx skills list | 현재 인식된 모든 글로벌/워크스페이스 스킬 목록 확인 | | npx skill
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 329eda9b-0fe1-8021-834c-d75821a7b099
created: 2026-03-20T15:32:08.399Z
updated: 2026-03-21T00:27:05.006Z
legacy_path: Main/Tool-e0f1ba2b631b/Antigravity-d75821a7b099/Skills-f5168e7df81b/index.md
legacy_category: Tool
source_url: https://beautiful-college-c84.notion.site/329eda9b0fe1802987f4f5168e7df81b
---
---

> ⚠️ 
> 
> <a id="329eda9b0fe1800cae99dd2ae996a889"></a>
> 
> 안티그래비티 스킬을 관리하기 위해 주로 사용하는 CLI 도구는 <strong><code>Gemini CLI</code></strong> 혹은 커뮤니티에서 널리 쓰이는 <strong><code>skills</code></strong><strong> CLI이다&#46;</strong>

|  |  |
| --- | --- |
| <strong>명령어</strong> | <strong>설명</strong> |
| <strong><code>npx skills list</code></strong> | 현재 인식된 모든 글로벌/워크스페이스 스킬 목록 확인 |
| <strong><code>npx skills find &#91;키워드&#93;</code></strong> | 레지스트리에서 새로운 스킬 검색 (예&#58; <code>find firebase</code>) |
| <strong><code>npx skills add &#91;이름&#93;</code></strong> | 특정 스킬을 자동으로 다운로드하여 설치 |
| <strong><code>npx skills doctor</code></strong> | 스킬 설정 경로가 올바른지, 충돌은 없는지 진단 |

<a id="32aeda9b0fe1809fb94be9c1055f86d6"></a>

### Scope

---

- 전역 설정 (Global)
    <a id="32aeda9b0fe1803aa0bcd3268ffd8902"></a>

    ```bash
    ~/.gemini/antigravity/skills/
    ```

    - 어떤 프로젝트를 열어도 에이전트가 항상 인지합니다&#46; (예&#58; 개인적인 코딩 스타일, 커밋 규칙)

- <strong>프로젝트 설정 (Workspace)&#58;</strong> 
    <a id="32aeda9b0fe180c483c2db49520d65a7"></a>

    ```bash
    [프로젝트 경로]/.agent/skills/
    ```

    - 해당 폴더를 열었을 때만 활성화됩니다&#46;

    -  팀 공통 컨벤션이나 특정 앱의 배포 스크립트를 넣기에 좋습니다&#46;

<a id="32aeda9b0fe180fb8f2edf04a9af6d89"></a>

### 스킬 적용 확인

---

1. 터미널에서 <code>npx skills list</code> 입력

1. 안티그래비티 채팅창에 <code>&#64;</code>를 입력하여 목록에 뜨는지 확인
