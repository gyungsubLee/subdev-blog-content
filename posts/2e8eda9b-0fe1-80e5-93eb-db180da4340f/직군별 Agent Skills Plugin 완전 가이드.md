---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 2e8eda9b-0fe1-80e5-93eb-db180da4340f
title: 직군별 Agent Skills Plugin 완전 가이드
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 258eda9b-0fe1-809a-a190-f424aca7c530
    title: 클로드코드
  - id: 2e7eda9b-0fe1-802f-b883-f70dea4cf374
    title: 스킬 플러그인
  - id: 2e8eda9b-0fe1-80e5-93eb-db180da4340f
    title: 직군별 Agent Skills Plugin 완전 가이드
excerpt: "작성일: 2026-01-14 대상: 1인 개발자, 스타트업 팀 목적: Claude Code에서 Skills Plugin을 활용한 멀티 에이전트 시스템 구축 --- - 1. 핵심 개념: Skills vs MCP Connectors - 비교표 - 핵심 차이점 - Agent Skills 특징 - 2. Skills Plugin "
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 2e7eda9b-0fe1-802f-b883-f70dea4cf374
created: 2026-01-14T06:13:49.003Z
updated: 2026-01-14T06:14:08.585Z
legacy_path: Main/클로드코드-f424aca7c530/스킬 플러그인-f70dea4cf374/직군별 Agent Skills Plugin 완전 가이드-db180da4340f/index.md
legacy_category: 클로드코드
source_url: https://beautiful-college-c84.notion.site/2e8eda9b0fe180e593ebdb180da4340f
---
> 작성일&#58; 2026&#45;01&#45;14
> 
> <a id="2e8eda9b0fe180f9a0f6eb5724cd6cf5"></a>
> 
> <strong>대상</strong>&#58; 1인 개발자, 스타트업 팀
> 
> <a id="2e8eda9b0fe1805c965bc676c10c76c2"></a>
> 
> <strong>목적</strong>&#58; Claude Code에서 Skills Plugin을 활용한 멀티 에이전트 시스템 구축

---

- [1. 핵심 개념: Skills vs MCP Connectors](#2e8eda9b0fe18028977ec353db97db6e)
- [비교표](#2e8eda9b0fe180c5b27ed58bd882face)
- [핵심 차이점](#2e8eda9b0fe18069b648caada23515ad)
- [Agent Skills 특징](#2e8eda9b0fe180ac83a2f4345700bb3d)
- [2. Skills Plugin Marketplace 설정법](#2e8eda9b0fe18056aa0ff33171e6ec8c)
- [2.1 Anthropic 공식 마켓플레이스 (Claude Code)](#2e8eda9b0fe180539fa9d89b2d58c799)
- [2.2 커뮤니티 마켓플레이스](#2e8eda9b0fe1805cbc51d5275c30f585)
- [2.3 CLI로 빠른 설치 (npx)](#2e8eda9b0fe180398aa4c9e4324a43f7)
- [2.4 Claude.ai 웹에서](#2e8eda9b0fe180dcae35ce5f1a382b30)
- [2.5 Skills 저장 위치](#2e8eda9b0fe1802cbf70eed9e422305b)
- [3. 직군별 에이전트 구성](#2e8eda9b0fe18057b8fbebe88f397693)
- [3.1 PM Agent (Product Manager)](#2e8eda9b0fe1800e97b2e5a9cb022dcb)
- [설치 명령어](#2e8eda9b0fe18062a79cc8d028e83f7a)
- [구성 Skills](#2e8eda9b0fe180e9b6dfd80aeb05524c)
- [MCP Connectors 연동](#2e8eda9b0fe18067a80adb103a023def)
- [실전 워크플로우](#2e8eda9b0fe180c28bdfeb4d09c4f9b2)
- [3.2 Developer Agent](#2e8eda9b0fe180c6bfbfc98815b0b8ab)
- [설치 명령어](#2e8eda9b0fe180449187d9743621799b)
- [구성 Skills](#2e8eda9b0fe180d1899ade9f353cfde7)
- [MCP Connectors 연동](#2e8eda9b0fe18012be51e9cd98bc790e)
- [실전 워크플로우](#2e8eda9b0fe1804fa27cdad18fd13d5d)
- [3.3 Designer Agent](#2e8eda9b0fe180daa2cfd16c688f21f3)
- [설치 명령어](#2e8eda9b0fe18026bfedee0f42909ff8)
- [구성 Skills](#2e8eda9b0fe18086be28d9a493b23c80)
- [MCP Connectors 연동](#2e8eda9b0fe180e2ac68c3b48172b8c1)
- [실전 워크플로우](#2e8eda9b0fe1803eacf2e3c73ca18601)
- [3.4 QA Agent](#2e8eda9b0fe180a583f8ea9841b0d6d3)
- [설치 명령어](#2e8eda9b0fe180f4a3a1cfe15edba94d)
- [구성 Skills](#2e8eda9b0fe180bfa4b3c425d119254c)
- [MCP Connectors 연동](#2e8eda9b0fe180ccbd0ccad02ae7d6b8)
- [실전 워크플로우](#2e8eda9b0fe180399372dfbf2b48d210)
- [3.5 Technical Writer Agent](#2e8eda9b0fe180b9ba3add39c20cd5a3)
- [설치 명령어](#2e8eda9b0fe18076904dca5685b48aa7)
- [구성 Skills](#2e8eda9b0fe18092b9edd91ffe66506a)
- [실전 워크플로우](#2e8eda9b0fe1804587c5fe79be663e49)
- [3.6 Data Analyst Agent](#2e8eda9b0fe18076b7dbf436c27d5f9c)
- [설치 명령어](#2e8eda9b0fe1804eafb7d05e9b099ae5)
- [구성 Skills](#2e8eda9b0fe1808dba7fdc430c9a6e06)
- [MCP Connectors 연동](#2e8eda9b0fe180ea9026dd5fa1817f9f)
- [실전 워크플로우](#2e8eda9b0fe1807dacf6d5145c4bce9e)
- [3.7 Researcher Agent (BioRAG용)](#2e8eda9b0fe18070b10ce7f98ef41587)
- [설치 명령어](#2e8eda9b0fe1805983ffdf7bbc1e47c8)
- [MCP Connectors (핵심!)](#2e8eda9b0fe180f69ae1f23edf42b7c9)
- [실전 워크플로우](#2e8eda9b0fe18064b93ee99522881c05)
- [4. 1인 개발자 전체 설치 스크립트](#2e8eda9b0fe1808183fadeab5cde9c96)
- [최소 설치 (필수만)](#2e8eda9b0fe18027b42ae0e298048651)
- [5. 트리거 키워드 요약](#2e8eda9b0fe180cf85eed796c217383e)
- [📎 참고 자료](#2e8eda9b0fe18016b3c0de15ac0c76e8)
- [공식 문서](#2e8eda9b0fe180b29984d5a8e384580d)
- [GitHub 저장소](#2e8eda9b0fe180789894de2375ff947e)
- [커뮤니티](#2e8eda9b0fe180289cbbca210f21798b)
- [📝 SKILL.md 기본 템플릿](#2e8eda9b0fe180559c2bdf366b9969be)

<a id="2e8eda9b0fe18028977ec353db97db6e"></a>

## 1&#46; 핵심 개념&#58; Skills vs MCP Connectors

<a id="2e8eda9b0fe180c5b27ed58bd882face"></a>

### 비교표

| 구분 | <strong>Skills (Plugin)</strong> | <strong>MCP Connectors</strong> |
| --- | --- | --- |
| 트리거 | <strong>자동</strong> (Claude가 판단) | 사용자 요청 시 |
| 용도 | 작업 방법/워크플로우 지침 | 외부 서비스 연동 |
| 설치 위치 | <code>&#126;/&#46;claude/skills/</code> | Settings → Connectors |
| 예시 | PRD 작성법, 코드 리뷰 가이드 | Notion API, GitHub API |

<a id="2e8eda9b0fe18069b648caada23515ad"></a>

### 핵심 차이점

- <strong>Skills</strong> = &#34;Claude에게 <strong>어떻게</strong> 작업할지 가르치는 것&#34;

- <strong>MCP</strong> = &#34;Claude에게 <strong>무엇을</strong> 연결할지 제공하는 것&#34;

<a id="2e8eda9b0fe180ac83a2f4345700bb3d"></a>

### Agent Skills 특징

- <strong>Model&#45;invoked</strong>&#58; Claude가 자동으로 관련 Skill 판단 및 활성화

- <strong>Progressive Disclosure</strong>&#58; 메타데이터 스캔 &#126;100 토큰, 활성화 시 &#60;5k 토큰

- <strong>Cross&#45;platform</strong>&#58; Claude&#46;ai, Claude Code, API에서 동일하게 작동

- <strong>Open Standard</strong>&#58; 2025년 12월 Anthropic이 오픈 표준으로 공개

---

<a id="2e8eda9b0fe18056aa0ff33171e6ec8c"></a>

## 2&#46; Skills Plugin Marketplace 설정법

<a id="2e8eda9b0fe180539fa9d89b2d58c799"></a>

### 2&#46;1 Anthropic 공식 마켓플레이스 (Claude Code)

<a id="2e8eda9b0fe1807cb1cdef2fa62c9fc5"></a>

```bash
# Step 1: 마켓플레이스 등록
/plugin marketplace add anthropics/skills

# Step 2: Plugin 목록 확인
/plugin
# → Discover 탭에서 브라우징

# Step 3: 원하는 Skills 설치
/plugin install document-skills@anthropic-agent-skills
/plugin install example-skills@anthropic-agent-skills

```

<a id="2e8eda9b0fe1805cbc51d5275c30f585"></a>

### 2&#46;2 커뮤니티 마켓플레이스

<a id="2e8eda9b0fe1803ab9e0c1fb11f8b2d8"></a>

```bash
# Engineering Workflows (Git, 테스트, 코드리뷰)
/plugin marketplace add mhattingpete/claude-skills-marketplace

# Netresearch (PHP, Go, Jira 통합)
/plugin marketplace add netresearch/claude-code-marketplace

# Project Planner (기획 문서 자동화)
/plugin marketplace add adrianpuiu/claude-skills-marketplace

# Superpowers (TDD, 디버깅, 27+ skills)
/plugin marketplace add obra/superpowers-marketplace

```

<a id="2e8eda9b0fe180398aa4c9e4324a43f7"></a>

### 2&#46;3 CLI로 빠른 설치 (npx)

<a id="2e8eda9b0fe1809f97add3af2fe444d7"></a>

```bash
# 프론트엔드 디자인
npx claude-plugins install @anthropics/claude-code-plugins/frontend-design

# UI 디자이너
npx claude-plugins install @ananddtyagi/claude-code-marketplace/ui-designer

# 복합 엔지니어링 (27 에이전트 + 20 커맨드 + 12 스킬)
npx claude-plugins install @EveryInc/every-marketplace/compound-engineering

```

<a id="2e8eda9b0fe180dcae35ce5f1a382b30"></a>

### 2&#46;4 Claude&#46;ai 웹에서

<a id="2e8eda9b0fe1801b83e7e37aef921e96"></a>

```plaintext
Settings → Skills → Upload Custom Skill
또는
유료 플랜: 기본 Skills 자동 활성화 (docx, xlsx, pptx, pdf 등)

```

<a id="2e8eda9b0fe1802cbf70eed9e422305b"></a>

### 2&#46;5 Skills 저장 위치

<a id="2e8eda9b0fe18071a28ede9747f1388e"></a>

```plaintext
~/.claude/
├── skills/                    # 개인 Skills (모든 프로젝트에서 사용)
│   ├── pm-agent/
│   │   └── SKILL.md
│   └── developer-agent/
│       └── SKILL.md
│
├── plugins/                   # 설치된 Plugins
│   └── marketplaces/
│       ├── anthropics-skills/
│       └── mhattingpete-claude-skills/
│
└── commands/                  # 슬래시 커맨드

프로젝트별:
.claude/
└── skills/                    # 프로젝트 Skills (팀 공유)
    └── project-specific-skill/
        └── SKILL.md

```

---

<a id="2e8eda9b0fe18057b8fbebe88f397693"></a>

## 3&#46; 직군별 에이전트 구성

---

<a id="2e8eda9b0fe1800e97b2e5a9cb022dcb"></a>

### 3&#46;1 PM Agent (Product Manager)

<a id="2e8eda9b0fe18062a79cc8d028e83f7a"></a>

### 설치 명령어

<a id="2e8eda9b0fe180a78451d1a38edc74cb"></a>

```bash
# Step 1: Anthropic 공식 마켓플레이스 등록
/plugin marketplace add anthropics/skills

# Step 2: Document Skills 설치
/plugin install document-skills@anthropic-agent-skills

# Step 3: Example Skills 설치 (internal-comms 포함)
/plugin install example-skills@anthropic-agent-skills

# Step 4: Project Planner 설치
/plugin marketplace add adrianpuiu/claude-skills-marketplace
/plugin install project-planner-skill@claude-skills-marketplace

```

<a id="2e8eda9b0fe180e9b6dfd80aeb05524c"></a>

### 구성 Skills

| Skill | 출처 | 자동 트리거 |
| --- | --- | --- |
| <strong>docx</strong> | anthropics/skills | &#34;문서 작성해줘&#34;, &#34;PRD 만들어줘&#34; |
| <strong>pptx</strong> | anthropics/skills | &#34;발표자료 만들어줘&#34;, &#34;슬라이드 생성&#34; |
| <strong>xlsx</strong> | anthropics/skills | &#34;스프레드시트 만들어줘&#34;, &#34;우선순위 매트릭스&#34; |
| <strong>internal&#45;comms</strong> | anthropics/skills | &#34;3P 업데이트&#34;, &#34;상태 보고서&#34;, &#34;뉴스레터&#34; |
| <strong>project&#45;planner</strong> | adrianpuiu | &#34;기능 기획해줘&#34;, &#34;요구사항 정리&#34; |

<a id="2e8eda9b0fe18067a80adb103a023def"></a>

### MCP Connectors 연동

<a id="2e8eda9b0fe180cb924bfba7be791491"></a>

```plaintext
Settings → Connectors 에서 연결:
✅ Notion - PRD, 위키, 로드맵
✅ Linear - 이슈 트래킹, 스프린트
✅ Google Calendar - 미팅 스케줄링
✅ Jira (선택) - 엔터프라이즈 환경

```

<a id="2e8eda9b0fe180c28bdfeb4d09c4f9b2"></a>

### 실전 워크플로우

<a id="2e8eda9b0fe180729efbc191d5a796b6"></a>

<strong>예시 1&#58; PRD 작성</strong>

<a id="2e8eda9b0fe180df9024d268abb08a73"></a>

```plaintext
User: "사용자 인증 기능 PRD 작성해줘"

[자동 활성화]
→ project-planner-skill: 요구사항 분석, 수용기준 생성
→ docx skill: Word 문서로 변환
→ Notion connector: Notion에 자동 업로드

```

<a id="2e8eda9b0fe1804ab317e7f60af9e911"></a>

<strong>예시 2&#58; 주간 업데이트</strong>

<a id="2e8eda9b0fe18080b08bcce9c99427dd"></a>

```plaintext
User: "이번 주 3P 업데이트 작성해줘"

[자동 활성화]
→ internal-comms skill: 3P 포맷 적용
  - Progress: 완료 항목
  - Plans: 다음 주 계획
  - Problems: 이슈/블로커

```

<a id="2e8eda9b0fe180a9b5d7da9216550daf"></a>

<strong>예시 3&#58; 우선순위 결정</strong>

<a id="2e8eda9b0fe1809cbc4fe88d3101a426"></a>

```plaintext
User: "백로그 우선순위 정리해줘 RICE 스코어로"

[자동 활성화]
→ xlsx skill: RICE 매트릭스 스프레드시트 생성
  - Reach, Impact, Confidence, Effort 계산
  - 자동 정렬 및 차트 생성

```

---

<a id="2e8eda9b0fe180c6bfbfc98815b0b8ab"></a>

### 3&#46;2 Developer Agent

<a id="2e8eda9b0fe180449187d9743621799b"></a>

### 설치 명령어

<a id="2e8eda9b0fe18088817cdf2ee049b3a7"></a>

```bash
# Step 1: Engineering Workflow (핵심!)
/plugin marketplace add mhattingpete/claude-skills-marketplace

# Step 2: 개별 Plugin 설치
/plugin install engineering-workflow-plugin@mhattingpete
/plugin install code-operations-plugin@mhattingpete

# Step 3: Superpowers (TDD, 디버깅, 27+ skills)
/plugin marketplace add obra/superpowers-marketplace

# Step 4: Frontend Design
/plugin install example-skills@anthropic-agent-skills

# Step 5: MCP Builder (API 연동 서버 구축)
/plugin install example-skills@anthropic-agent-skills

# 또는 CLI로 한번에
npx claude-plugins install @anthropics/claude-code-plugins/frontend-design

```

<a id="2e8eda9b0fe180d1899ade9f353cfde7"></a>

### 구성 Skills

| Skill | 출처 | 자동 트리거 |
| --- | --- | --- |
| <strong>feature&#45;planning</strong> | mhattingpete | &#34;새 기능 구현해줘&#34;, &#34;기능 추가&#34; |
| <strong>git&#45;push</strong> | mhattingpete | &#34;커밋해줘&#34;, &#34;푸시해줘&#34;, &#34;변경사항 저장&#34; |
| <strong>fix&#45;failing&#45;tests</strong> | mhattingpete | &#34;테스트 실패했어&#34;, &#34;테스트 고쳐줘&#34; |
| <strong>code&#45;review&#45;impl</strong> | mhattingpete | &#34;리뷰 피드백 반영해줘&#34;, &#34;PR 코멘트 처리&#34; |
| <strong>plan&#45;implementer</strong> | mhattingpete | (자동) 계획 수립 후 실행 |
| <strong>frontend&#45;design</strong> | anthropics | &#34;UI 만들어줘&#34;, &#34;컴포넌트 디자인&#34; |
| <strong>mcp&#45;builder</strong> | anthropics | &#34;MCP 서버 만들어줘&#34;, &#34;API 연동&#34; |
| <strong>superpowers</strong> | obra | TDD, 디버깅, 리팩토링 등 27&#43; skills |

<a id="2e8eda9b0fe18012be51e9cd98bc790e"></a>

### MCP Connectors 연동

<a id="2e8eda9b0fe18004b55ddf5ba0a53409"></a>

```plaintext
Settings → Connectors 에서 연결:
✅ GitHub - 코드, PR, 이슈
✅ Linear - 태스크 관리
✅ Sentry - 에러 모니터링
✅ Vercel (선택) - 배포

```

<a id="2e8eda9b0fe1804fa27cdad18fd13d5d"></a>

### 실전 워크플로우

<a id="2e8eda9b0fe180399d99e1a10d6f8dbf"></a>

<strong>예시 1&#58; 기능 개발 전체 사이클</strong>

<a id="2e8eda9b0fe18098b1b0fd6060c3b567"></a>

```plaintext
User: "실시간 채팅 기능 만들어줘"

[자동 활성화 순서]
1️⃣ feature-planning skill
   → 기능 분해, 태스크 목록 생성

2️⃣ plan-implementer agent
   → 각 태스크 순차 실행
   → WebSocket 서버 구현
   → React 클라이언트 구현

3️⃣ fix-failing-tests skill
   → 테스트 작성 및 수정

4️⃣ git-push skill
   → 커밋 메시지 생성
   → feature 브랜치에 푸시

5️⃣ GitHub connector
   → PR 자동 생성

```

<a id="2e8eda9b0fe180d692a6c028dbe5b733"></a>

<strong>예시 2&#58; 버그 수정</strong>

<a id="2e8eda9b0fe1803c88bef5298e369f03"></a>

```plaintext
User: "이 에러 고쳐줘" + 에러 로그

[자동 활성화]
→ superpowers (디버깅 skill)
   - 스택 트레이스 분석
   - 원인 파악
   - 수정 코드 제안
→ fix-failing-tests: 관련 테스트 수정
→ git-push: 수정 커밋

```

<a id="2e8eda9b0fe180b8b8f7f50dbdd2c414"></a>

<strong>예시 3&#58; 코드 리뷰 반영</strong>

<a id="2e8eda9b0fe18035a409f0edcdcfda67"></a>

```plaintext
User: "PR에 달린 리뷰 피드백 반영해줘"

[자동 활성화]
→ code-review-implementation skill
   - 피드백별 TODO 생성
   - 순차적 수정
   - 리뷰어 코멘트에 답변 작성
→ git-push: 수정사항 커밋

```

---

<a id="2e8eda9b0fe180daa2cfd16c688f21f3"></a>

### 3&#46;3 Designer Agent

<a id="2e8eda9b0fe18026bfedee0f42909ff8"></a>

### 설치 명령어

<a id="2e8eda9b0fe180d7ad24ed142299de1e"></a>

```bash
# Step 1: Frontend Design (Production-grade UI)
/plugin install example-skills@anthropic-agent-skills

# Step 2: Canvas Design (포스터, 비주얼)
/plugin install example-skills@anthropic-agent-skills

# Step 3: Visual Documentation
/plugin marketplace add mhattingpete/claude-skills-marketplace
/plugin install visual-documentation-plugin@mhattingpete

# Step 4: Algorithmic Art (생성 아트)
/plugin install example-skills@anthropic-agent-skills

# CLI 대안
npx claude-plugins install @anthropics/claude-code-plugins/frontend-design
npx claude-plugins install @ananddtyagi/claude-code-marketplace/ui-designer

```

<a id="2e8eda9b0fe18086be28d9a493b23c80"></a>

### 구성 Skills

| Skill | 출처 | 자동 트리거 |
| --- | --- | --- |
| <strong>frontend&#45;design</strong> | anthropics | &#34;UI 만들어줘&#34;, &#34;랜딩페이지&#34;, &#34;대시보드&#34; |
| <strong>canvas&#45;design</strong> | anthropics | &#34;포스터 만들어줘&#34;, &#34;비주얼 디자인&#34; |
| <strong>visual&#45;documentation</strong> | mhattingpete | &#34;다이어그램&#34;, &#34;플로우차트&#34;, &#34;아키텍처&#34; |
| <strong>algorithmic&#45;art</strong> | anthropics | &#34;생성 아트&#34;, &#34;p5&#46;js 아트&#34; |
| <strong>pptx</strong> | anthropics | &#34;발표자료 디자인&#34; |

<a id="2e8eda9b0fe180e2ac68c3b48172b8c1"></a>

### MCP Connectors 연동

<a id="2e8eda9b0fe1806d8a81d30d610e90c7"></a>

```plaintext
Settings → Connectors 에서 연결:
✅ Figma - 디자인 파일 참조
✅ Notion - 디자인 시스템 문서화

```

<a id="2e8eda9b0fe1803eacf2e3c73ca18601"></a>

### 실전 워크플로우

<a id="2e8eda9b0fe180ceb78bd834242d9e7f"></a>

<strong>예시 1&#58; 랜딩 페이지</strong>

<a id="2e8eda9b0fe18093b6cbc0814a4fe0b3"></a>

```plaintext
User: "SaaS 제품 랜딩페이지 만들어줘"

[자동 활성화]
→ frontend-design skill
   - 독특한 폰트 선택 (Inter, Arial 지양)
   - 대담한 컬러 팔레트
   - 미세 애니메이션
   - Production-ready React/HTML 코드

```

<a id="2e8eda9b0fe180529131cb11569f196a"></a>

<strong>예시 2&#58; 시스템 아키텍처 다이어그램</strong>

<a id="2e8eda9b0fe180b99b70c7dd45762cfa"></a>

```plaintext
User: "마이크로서비스 아키텍처 다이어그램 만들어줘"

[자동 활성화]
→ visual-documentation skill
   - SVG 다이어그램 생성
   - 인터랙티브 HTML 문서
   - 컴포넌트 관계도

```

<a id="2e8eda9b0fe180708366d18acfbe91d6"></a>

<strong>예시 3&#58; 마케팅 비주얼</strong>

<a id="2e8eda9b0fe18092a0d1e375947bdf32"></a>

```plaintext
User: "제품 출시 포스터 만들어줘"

[자동 활성화]
→ canvas-design skill
   - PNG/PDF 출력
   - 디자인 철학 적용

```

---

<a id="2e8eda9b0fe180a583f8ea9841b0d6d3"></a>

### 3&#46;4 QA Agent

<a id="2e8eda9b0fe180f4a3a1cfe15edba94d"></a>

### 설치 명령어

<a id="2e8eda9b0fe180088087ded5c795fc15"></a>

```bash
# Step 1: Engineering Workflow (테스트 관련)
/plugin marketplace add mhattingpete/claude-skills-marketplace
/plugin install engineering-workflow-plugin@mhattingpete

# Step 2: Document Skills (버그 리포트)
/plugin install document-skills@anthropic-agent-skills

# Step 3: Superpowers (TDD)
/plugin marketplace add obra/superpowers-marketplace

```

<a id="2e8eda9b0fe180bfa4b3c425d119254c"></a>

### 구성 Skills

| Skill | 출처 | 자동 트리거 |
| --- | --- | --- |
| <strong>fix&#45;failing&#45;tests</strong> | mhattingpete | &#34;테스트 실패&#34;, &#34;테스트 수정&#34; |
| <strong>code&#45;review&#45;impl</strong> | mhattingpete | &#34;리뷰 피드백&#34; |
| <strong>superpowers (TDD)</strong> | obra | &#34;TDD로 작성해줘&#34; |
| <strong>xlsx</strong> | anthropics | &#34;테스트 케이스 매트릭스&#34; |
| <strong>docx</strong> | anthropics | &#34;버그 리포트 작성&#34; |

<a id="2e8eda9b0fe180ccbd0ccad02ae7d6b8"></a>

### MCP Connectors 연동

<a id="2e8eda9b0fe1801b8e4de09ba7984eb2"></a>

```plaintext
Settings → Connectors 에서 연결:
✅ GitHub - PR, CI 결과 확인
✅ Jira/Linear - 버그 티켓 생성
✅ Sentry - 에러 모니터링

```

<a id="2e8eda9b0fe180399372dfbf2b48d210"></a>

### 실전 워크플로우

<a id="2e8eda9b0fe180f78964dbfa450a68f9"></a>

<strong>예시 1&#58; 테스트 실패 수정</strong>

<a id="2e8eda9b0fe180da90f9de42db18ca56"></a>

```plaintext
User: "CI에서 테스트 5개 실패했어"

[자동 활성화]
→ fix-failing-tests skill
   - 에러 그룹핑 (같은 원인별)
   - 우선순위 지정
   - 순차적 수정
   - 재실행 확인

```

<a id="2e8eda9b0fe180f58cf4e16b3eda01db"></a>

<strong>예시 2&#58; 테스트 케이스 작성</strong>

<a id="2e8eda9b0fe1802fbe95fd0a78c2acdd"></a>

```plaintext
User: "인증 모듈 테스트 케이스 정리해줘"

[자동 활성화]
→ xlsx skill: 테스트 매트릭스 생성
   - 시나리오 | 입력값 | 기대결과 | 상태
→ superpowers (TDD): 테스트 코드 생성

```

<a id="2e8eda9b0fe180878f76ea001c680b1e"></a>

<strong>예시 3&#58; 버그 리포트</strong>

<a id="2e8eda9b0fe1803b8524d0c99b3d11ea"></a>

```plaintext
User: "이 버그 Jira 티켓으로 만들어줘"

[자동 활성화]
→ docx skill: 버그 리포트 문서화
→ Jira connector: 티켓 자동 생성

```

---

<a id="2e8eda9b0fe180b9ba3add39c20cd5a3"></a>

### 3&#46;5 Technical Writer Agent

<a id="2e8eda9b0fe18076904dca5685b48aa7"></a>

### 설치 명령어

<a id="2e8eda9b0fe18031889bd4d3eac017ea"></a>

```bash
# Step 1: Document Skills (핵심)
/plugin install document-skills@anthropic-agent-skills

# Step 2: Visual Documentation
/plugin marketplace add mhattingpete/claude-skills-marketplace
/plugin install visual-documentation-plugin@mhattingpete

# Step 3: Doc Coauthoring (협업)
/plugin install example-skills@anthropic-agent-skills

```

<a id="2e8eda9b0fe18092b9edd91ffe66506a"></a>

### 구성 Skills

| Skill | 출처 | 자동 트리거 |
| --- | --- | --- |
| <strong>docx</strong> | anthropics | &#34;문서 작성&#34;, &#34;가이드 만들어줘&#34; |
| <strong>pdf</strong> | anthropics | &#34;PDF 생성&#34;, &#34;PDF 병합&#34; |
| <strong>pptx</strong> | anthropics | &#34;온보딩 자료&#34; |
| <strong>visual&#45;documentation</strong> | mhattingpete | &#34;API 문서&#34;, &#34;아키텍처 문서&#34; |
| <strong>doc&#45;coauthoring</strong> | anthropics | &#34;문서 검토&#34;, &#34;트래킹 변경&#34; |
| <strong>internal&#45;comms</strong> | anthropics | &#34;FAQ&#34;, &#34;릴리즈 노트&#34; |

<a id="2e8eda9b0fe1804587c5fe79be663e49"></a>

### 실전 워크플로우

<a id="2e8eda9b0fe1800bbe7ec6f2095f9981"></a>

<strong>예시 1&#58; API 문서 작성</strong>

<a id="2e8eda9b0fe18060b352c81cc24bde0d"></a>

```plaintext
User: "REST API 문서 작성해줘"

[자동 활성화]
→ visual-documentation skill
   - OpenAPI 스펙 기반
   - 엔드포인트별 예시
   - 에러 코드 정리
→ docx skill: Word 문서 변환

```

<a id="2e8eda9b0fe180f5b83ed2147d3049bb"></a>

<strong>예시 2&#58; 온보딩 가이드</strong>

<a id="2e8eda9b0fe180618276eeb03ea68589"></a>

```plaintext
User: "신규 개발자 온보딩 가이드 만들어줘"

[자동 활성화]
→ pptx skill: 프레젠테이션 형태
→ docx skill: 상세 문서
→ visual-documentation: 아키텍처 다이어그램

```

<a id="2e8eda9b0fe1803fb8ddc2601649ae6f"></a>

<strong>예시 3&#58; 문서 리뷰</strong>

<a id="2e8eda9b0fe1801d9862e5164d986050"></a>

```plaintext
User: "이 문서 검토하고 수정해줘"

[자동 활성화]
→ doc-coauthoring skill
   - 트래킹 변경 활성화
   - 코멘트 추가
   - 수정 제안

```

---

<a id="2e8eda9b0fe18076b7dbf436c27d5f9c"></a>

### 3&#46;6 Data Analyst Agent

<a id="2e8eda9b0fe1804eafb7d05e9b099ae5"></a>

### 설치 명령어

<a id="2e8eda9b0fe180de8c6bfdd7f698faca"></a>

```bash
# Step 1: Document Skills (xlsx 핵심)
/plugin install document-skills@anthropic-agent-skills

# Step 2: Visual Documentation
/plugin marketplace add mhattingpete/claude-skills-marketplace
/plugin install visual-documentation-plugin@mhattingpete

```

<a id="2e8eda9b0fe1808dba7fdc430c9a6e06"></a>

### 구성 Skills

| Skill | 출처 | 자동 트리거 |
| --- | --- | --- |
| <strong>xlsx</strong> | anthropics | &#34;데이터 분석&#34;, &#34;차트 만들어줘&#34;, &#34;피벗&#34; |
| <strong>pdf</strong> | anthropics | &#34;리포트 PDF로&#34; |
| <strong>visual&#45;documentation</strong> | mhattingpete | &#34;대시보드&#34;, &#34;시각화&#34; |

<a id="2e8eda9b0fe180ea9026dd5fa1817f9f"></a>

### MCP Connectors 연동

<a id="2e8eda9b0fe180d9a63ad3f5481d67a8"></a>

```plaintext
Settings → Connectors 에서 연결:
✅ Google Sheets - 스프레드시트
✅ Google Drive - 파일 관리
✅ Notion - 리포트 공유

```

<a id="2e8eda9b0fe1807dacf6d5145c4bce9e"></a>

### 실전 워크플로우

<a id="2e8eda9b0fe180f78d3fd6c5dc9da554"></a>

<strong>예시&#58; 매출 분석</strong>

<a id="2e8eda9b0fe180f28c55ed6c65b4f0ea"></a>

```plaintext
User: "이 매출 데이터 분석해줘"

[자동 활성화]
→ xlsx skill
   - 데이터 정제
   - 피벗 테이블 생성
   - 추세 차트
   - 인사이트 요약
→ visual-documentation: 대시보드 HTML
→ pdf skill: 리포트 PDF 변환

```

---

<a id="2e8eda9b0fe18070b10ce7f98ef41587"></a>

### 3&#46;7 Researcher Agent (BioRAG용)

<a id="2e8eda9b0fe1805983ffdf7bbc1e47c8"></a>

### 설치 명령어

<a id="2e8eda9b0fe180d8ae2ae0fa64a5bb4d"></a>

```bash
# Step 1: Document Skills
/plugin install document-skills@anthropic-agent-skills

# Step 2: MCP Builder (커스텀 연동 필요시)
/plugin install example-skills@anthropic-agent-skills

```

<a id="2e8eda9b0fe180f69ae1f23edf42b7c9"></a>

### MCP Connectors (핵심&#33;)

<a id="2e8eda9b0fe180d4a6b6fb0a06232522"></a>

```plaintext
Settings → Connectors 에서 연결:
✅ PubMed - 바이오메디컬 논문 검색
✅ BioRender - 과학 일러스트
✅ Notion - 문헌 정리
✅ Google Drive - PDF 저장

```

<a id="2e8eda9b0fe18064b93ee99522881c05"></a>

### 실전 워크플로우

<a id="2e8eda9b0fe180e3b305ed71dd1e852d"></a>

<strong>예시&#58; 문헌 조사</strong>

<a id="2e8eda9b0fe1801c9c53ca16d5c3e72f"></a>

```plaintext
User: "CRISPR 치료제 최신 논문 조사해줘"

[자동 활성화]
→ PubMed connector: 논문 검색
→ pdf skill: 논문 텍스트 추출
→ xlsx skill: 논문 메타데이터 정리
→ docx skill: 문헌 리뷰 문서 작성
→ BioRender connector: 메커니즘 다이어그램
→ Notion connector: 정리된 내용 업로드

```

---

<a id="2e8eda9b0fe1808183fadeab5cde9c96"></a>

## 4&#46; 1인 개발자 전체 설치 스크립트

<a id="2e8eda9b0fe180a78a63d5e41352ff5e"></a>

```bash
#!/bin/bash
# 1인 개발자용 Agent Skills 전체 설치

echo "=== Anthropic 공식 Skills 설치 ==="
/plugin marketplace add anthropics/skills
/plugin install document-skills@anthropic-agent-skills
/plugin install example-skills@anthropic-agent-skills

echo "=== Engineering Workflow 설치 ==="
/plugin marketplace add mhattingpete/claude-skills-marketplace

echo "=== Project Planning 설치 ==="
/plugin marketplace add adrianpuiu/claude-skills-marketplace
/plugin install project-planner-skill@claude-skills-marketplace

echo "=== Superpowers (TDD, 디버깅) 설치 ==="
/plugin marketplace add obra/superpowers-marketplace

echo "=== 설치 확인 ==="
/plugin
# → Installed 탭에서 확인

echo "✅ 설치 완료!"

```

<a id="2e8eda9b0fe18027b42ae0e298048651"></a>

### 최소 설치 (필수만)

<a id="2e8eda9b0fe180e59b6ace5774454a95"></a>

```bash
# Document Skills만 (PM, Writer용)
/plugin marketplace add anthropics/skills
/plugin install document-skills@anthropic-agent-skills

# Engineering Workflow만 (Developer용)
/plugin marketplace add mhattingpete/claude-skills-marketplace

```

---

<a id="2e8eda9b0fe180cf85eed796c217383e"></a>

## 5&#46; 트리거 키워드 요약

| 키워드 | 활성화되는 Agent/Skill |
| --- | --- |
| &#34;PRD&#34;, &#34;요구사항&#34;, &#34;기획&#34; | PM → project&#45;planner |
| &#34;3P&#34;, &#34;주간 업데이트&#34;, &#34;상태 보고&#34; | PM → internal&#45;comms |
| &#34;발표자료&#34;, &#34;슬라이드&#34;, &#34;프레젠테이션&#34; | PM/Writer → pptx |
| &#34;기능 구현&#34;, &#34;개발해줘&#34;, &#34;만들어줘&#34; | Dev → feature&#45;planning → plan&#45;implementer |
| &#34;커밋&#34;, &#34;푸시&#34;, &#34;저장&#34; | Dev → git&#45;push |
| &#34;테스트 실패&#34;, &#34;테스트 수정&#34; | QA → fix&#45;failing&#45;tests |
| &#34;리뷰 피드백&#34;, &#34;PR 코멘트&#34; | Dev/QA → code&#45;review&#45;implementation |
| &#34;UI&#34;, &#34;컴포넌트&#34;, &#34;랜딩페이지&#34; | Designer → frontend&#45;design |
| &#34;다이어그램&#34;, &#34;아키텍처&#34;, &#34;플로우차트&#34; | Designer/Writer → visual&#45;documentation |
| &#34;포스터&#34;, &#34;비주얼&#34; | Designer → canvas&#45;design |
| &#34;문서 작성&#34;, &#34;Word&#34;, &#34;가이드&#34; | Writer → docx |
| &#34;PDF&#34;, &#34;병합&#34;, &#34;추출&#34; | Writer → pdf |
| &#34;데이터 분석&#34;, &#34;차트&#34;, &#34;피벗&#34; | Analyst → xlsx |
| &#34;논문 검색&#34;, &#34;문헌 조사&#34; | Researcher → PubMed connector |

---

<a id="2e8eda9b0fe18016b3c0de15ac0c76e8"></a>

## 📎 참고 자료

<a id="2e8eda9b0fe180b29984d5a8e384580d"></a>

### 공식 문서

- <a href="https://support.claude.com/en/articles/12512176-what-are-skills">What are Skills?</a>

- <a href="https://support.claude.com/en/articles/12512180-using-skills-in-claude">Using Skills in Claude</a>

- <a href="https://support.claude.com/en/articles/12512198-creating-custom-skills">Creating Custom Skills</a>

- <a href="https://anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills">Agent Skills Blog</a>

<a id="2e8eda9b0fe180789894de2375ff947e"></a>

### GitHub 저장소

- <a href="https://github.com/anthropics/skills">anthropics/skills</a> &#45; Anthropic 공식

- <a href="https://github.com/mhattingpete/claude-skills-marketplace">mhattingpete/claude&#45;skills&#45;marketplace</a> &#45; Engineering Workflow

- <a href="https://github.com/obra/superpowers">obra/superpowers</a> &#45; TDD, 디버깅

- <a href="https://github.com/travisvn/awesome-claude-skills">travisvn/awesome&#45;claude&#45;skills</a> &#45; 큐레이션 목록

<a id="2e8eda9b0fe180289cbbca210f21798b"></a>

### 커뮤니티

- <a href="https://skillsmp.com/">SkillsMP&#46;com</a> &#45; Skills 마켓플레이스

- <a href="https://claude-plugins.dev/">claude&#45;plugins&#46;dev</a> &#45; Plugin CLI

---

<a id="2e8eda9b0fe180559c2bdf366b9969be"></a>

## 📝 SKILL&#46;md 기본 템플릿

<a id="2e8eda9b0fe18083a2ccef00c63d26d5"></a>

```yaml
---
name: my-skill-name
description: A clear description of what this skill does and when to use it.
  Use when [trigger conditions].
---

# My Skill Name

## Instructions
[Add your instructions here that Claude will follow when this skill is active]

## Examples
- Example usage 1
- Example usage 2

## Guidelines
- Guideline 1
- Guideline 2

```

---

> 문서 버전&#58; v1&#46;0
> 
> <a id="2e8eda9b0fe18091bf6dfb55cd9c14f8"></a>
> 
> <strong>마지막 업데이트</strong>&#58; 2026&#45;01&#45;14
