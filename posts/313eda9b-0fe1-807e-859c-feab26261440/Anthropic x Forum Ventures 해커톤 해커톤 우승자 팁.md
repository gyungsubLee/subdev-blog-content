---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 313eda9b-0fe1-807e-859c-feab26261440
title: Anthropic x Forum Ventures 해커톤 해커톤 우승자 팁
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 3efeda9b-0fe1-80b6-940d-e56cb496cf28
    title: Agent
  - id: 2f7eda9b-0fe1-80e2-a643-cd387204f4e4
    title: 에이전트
  - id: 2efeda9b-0fe1-80d6-8674-cb28381cddf4
    title: "컨텍스트 엔지니어링, Agent Harness (테디노트 라이브: 26.01.2x)"
  - id: 313eda9b-0fe1-807e-859c-feab26261440
    title: Anthropic x Forum Ventures 해커톤 해커톤 우승자 팁
excerpt: "[The Claude Code setup that won a hackathon]() 해당 블로그 글은 Anthropic x Forum Ventures 해커톤에서 zenith.chat이라는 프로젝트로 우승을 차지한 개발자(Affaan 및 JP Caparas 등 관련 커뮤니티에서 공유된 내용)의 'Claude Code' 최적"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 2efeda9b-0fe1-80d6-8674-cb28381cddf4
created: 2026-02-26T02:59:06.386Z
updated: 2026-02-26T03:01:52.521Z
legacy_path: Main/Agent-e56cb496cf28/에이전트-cd387204f4e4/컨텍스트 엔지니어링, Agent Harness (테디노트 라이브- 26.01.2x-cb28381cddf4/Anthropic x Forum Ventures 해커톤 해커톤 우승자 팁-feab26261440/index.md
legacy_category: Agent
source_url: https://beautiful-college-c84.notion.site/313eda9b0fe1807e859cfeab26261440
---
[The Claude Code setup that won a hackathon]()

<a id="313eda9b0fe1806782fbc3c4050d1a4f"></a>

해당 블로그 글은 Anthropic x Forum Ventures 해커톤에서 <strong>zenith&#46;chat</strong>이라는 프로젝트로 우승을 차지한 개발자(Affaan 및 JP Caparas 등 관련 커뮤니티에서 공유된 내용)의 <strong>&#39;Claude Code&#39; 최적화 설정</strong>을 다루고 있다&#46;

- 핵심 철학&#58;  <strong>Claude를 단순한 챗봇이 아닌, 다역할을 수행하는 &#39;에이전트 팀&#39;으로 운영하라</strong>

<a id="313eda9b0fe180349a36f4e1b9121c5f"></a>

### 1&#46; 핵심 요약 (Core Summary)

<a id="313eda9b0fe180b79c95e62100550015"></a>

이 프로젝트의 성공 비결은 Claude Code를 고도로 구조화된 워크플로우와 결합하여 <strong>완전한 개발 파이프라인</strong>을 구축한 데 있습니다&#46;

- <strong>에이전트 팀 구성</strong>&#58; 메인 세션을 &#39;프로젝트 매니저(PM)&#39;로 두고, 세부 작업은 병렬로 실행되는 &#39;서브 에이전트&#39;들에게 위임합니다&#46;

- <strong>표준화된 프로세스</strong>&#58; <code>/plan</code>, <code>/tdd</code>, <code>/code&#45;review</code> 등의 커스텀 명령어를 통해 개발 루틴을 자동화했습니다&#46;

- <strong>품질 가드레일</strong>&#58; 코드 스타일, 보안, 테스트 통과 여부를 강제하는 Rules와 Hooks를 설정하여 AI가 실수를 줄이도록 설계했습니다&#46;

---

<a id="313eda9b0fe1803b8161e1562cfef55a"></a>

### 2&#46; 중요 부분 상세 설명 및 기술적 분석

<a id="313eda9b0fe18026b04afcd046b43ab1"></a>

### ① MCP (Model Context Protocol) &#45; AI의 &#39;USB&#45;C 포트&#39;

<a id="313eda9b0fe180dea8f0c013a49f9782"></a>

이 설정에서 가장 중요한 기술적 기반은 Anthropic이 발표한 <strong>MCP</strong>입니다&#46;

- <strong>상세 내용</strong>&#58; MCP는 AI 모델이 외부 데이터 소스(GitHub, Google Drive, 데이터베이스 등)나 로컬 도구와 통신하기 위한 공개 표준 프로토콜입니다&#46;

- <strong>활용법</strong>&#58; 우승자는 GitHub, Supabase, Vercel 등을 MCP로 연결하여 Claude가 직접 이슈를 읽고, DB 스키마를 확인하며, 배포 상태를 체크하게 했습니다&#46;

- <strong>주의점</strong>&#58; MCP 서버를 너무 많이 활성화(20개 이상)하면 컨텍스트 윈도우가 급격히 줄어들 수 있으므로, 프로젝트당 10개 미만으로 제한하여 <strong>토큰 효율</strong>을 높이는 것이 중요합니다&#46;

<a id="313eda9b0fe1801da35bf8deb1e0ed50"></a>

### ② Skills &#38; Slash Commands (커스텀 명령어 자동화)

<a id="313eda9b0fe1803f8ba7f4a6a984d50d"></a>

Claude Code의 기능을 확장하는 핵심 수단입니다&#46;

- <strong>Skills</strong>&#58; 특정 작업(예&#58; API 문서 작성, 보안 리뷰)에 대한 전문 지식을 담은 Markdown 파일(<code>&#46;claude/skills/</code>)입니다&#46; Claude가 필요할 때 자동으로 호출합니다&#46;

- <strong>Slash Commands</strong>&#58; 사용자가 직접 실행하는 단축키입니다&#46;
    - <code>/tdd</code>&#58; 테스트 케이스를 먼저 작성하고 코드를 수정하는 워크플로우 시작&#46;

    - <code>/refactor&#45;clean</code>&#58; 사용하지 않는 코드나 임시 파일을 정리&#46;

    - <code>/catchup</code>&#58; 현재 Git 브랜치의 변경 사항을 요약하여 문맥 파악&#46;

<a id="313eda9b0fe180a3b3aad83953e6713a"></a>

### ③ Hooks (이벤트 기반 자동화)

<a id="313eda9b0fe180ccb24dcd3d658bedb2"></a>

개발 과정에서 특정 시점에 자동으로 실행되는 스크립트입니다&#46;

- <strong>차단 훅(Block&#45;at&#45;Submit)</strong>&#58; <code>git commit</code> 전 테스트가 실패하면 커밋을 원천 차단하도록 설정합니다&#46; 이를 통해 Claude가 &#34;테스트 통과 → 수정&#34; 루프를 스스로 반복하게 강제합니다&#46;

- <strong>힌트 훅(Hint Hook)</strong>&#58; 에이전트가 비효율적인 방식을 선택할 때 즉각적인 피드백을 주어 경로를 수정합니다&#46;

<a id="313eda9b0fe180cb9dd9f3807fa0e978"></a>

### ④ 최적화된 개발 환경 (Zed, tmux, Git Worktrees)

<a id="313eda9b0fe1801aaae2e3894e408fcb"></a>

AI 에이전트와 협업하기 위해 하드웨어/소프트웨어 설정을 최적화했습니다&#46;

- <strong>Zed Editor</strong>&#58; AI 에이전트 패널이 통합되어 있어 Claude의 편집 과정을 실시간으로 모니터링하기 좋습니다&#46; 성능이 가볍고 즉각적입니다&#46;

- <strong>tmux</strong>&#58; 여러 개의 Claude 세션을 동시에 띄워 병렬 작업을 수행할 때 필수적입니다&#46;

- <strong>Git Worktrees</strong>&#58; 서로 다른 기능을 개발하는 에이전트들이 충돌 없이 여러 브랜치에서 동시에 작업할 수 있게 해줍니다&#46;

---

<a id="313eda9b0fe180608beaccac5cd488dd"></a>

### 3&#46; 실전 적용을 위한 팁

- <strong>CLAUDE&#46;md 활용</strong>&#58; 프로젝트 루트에 이 파일을 만들고 코딩 스타일, 아키텍처 규칙을 적어두세요&#46; Claude가 세션을 시작할 때마다 이 정보를 읽어 &#39;기억&#39;의 기준점으로 삼습니다&#46;

- <strong>컨텍스트 관리</strong>&#58; 컨텍스트가 너무 비대해지면 <code>/compact</code> 명령어를 쓰기보다, 중요한 진행 상황을 별도 파일에 덤프하고 세션을 새로 시작하는(<code>/clear</code>) 방식이 더 정확도가 높습니다&#46;

<a id="313eda9b0fe180329ea6cdd6104e06bc"></a>

이 설정은 단순히 도구를 쓰는 수준을 넘어, <strong>AI가 스스로를 교정하고 검증하는 시스템</strong>을 구축했다는 점에서 해커톤 우승의 결정적 요인이 되었습니다&#46;
