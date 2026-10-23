---
order: 1
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 312eda9b-0fe1-806e-86d7-f34cfc05ed83
title: "MoAI-ADK (테디노트 라이브: 26.02.25)"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 3efeda9b-0fe1-80b6-940d-e56cb496cf28
    title: Agent
  - id: 2f7eda9b-0fe1-80e2-a643-cd387204f4e4
    title: 에이전트
  - id: 312eda9b-0fe1-806e-86d7-f34cfc05ed83
    title: "MoAI-ADK (테디노트 라이브: 26.02.25)"
excerpt: "reference [[모두의 AI Goos Kim x 테디노트] #Agentic Coding w/ #MoAI ADK🔥]() moai-adk [MoAI-ADK Documentation | MoAI-ADK]() 핵심 가치 [소개 | MoAI-ADK]() - 스펙 기반 워크플로우 (Spec-based Workflow) - 개"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 2f7eda9b-0fe1-80e2-a643-cd387204f4e4
created: 2026-02-25T16:06:00.919Z
updated: 2026-03-19T03:27:20.472Z
legacy_path: Main/Agent-e56cb496cf28/에이전트-cd387204f4e4/MoAI-ADK (테디노트 라이브- 26.02.25)-f34cfc05ed83/index.md
legacy_category: Agent
source_url: https://beautiful-college-c84.notion.site/312eda9b0fe1806e86d7f34cfc05ed83
---
<details>
<summary>reference</summary>

[&#91;모두의 AI Goos Kim x 테디노트&#93; &#35;Agentic Coding w/ &#35;MoAI ADK🔥]()

[moai-adk](https://github.com/modu-ai/moai-adk)

[MoAI&#45;ADK Documentation &#124; MoAI&#45;ADK]()

</details>

<a id="313eda9b0fe180d1ac7ed70717060002"></a>

## 핵심 가치

[소개 &#124; MoAI&#45;ADK]()

- <strong><code>스펙 기반 워크플로우 (Spec&#45;based Workflow)</code></strong>
    - 개발의 시작을 코드가 아닌 &#39;스펙 문서&#39;에서 시작

    -  AI가 문서를 기반으로 <u>설계(Plan)</u>하고, <u>구현(Run)</u>하며, <br>최종적으로<u> 코드와 문서의 동기화(Sync</u>)를 맞추는 단계를 거친다&#46;

    <details>
    <summary><strong><code>SPEC 기반 TDD/DDD</code></strong>&#58; </summary>

    - 프로젝트 특성에 따라 <code>테스트 주도 개발(TDD)</code> 또는 <code>도메인 주도 설계(DDD)</code> 방법론을 선택하여 진행 가능 

    - 요구사항을 문서화하고 점진적으로 개발하는 구조화된 방법론 <br>(신규 프로젝트는 TDD, 레거시 코드는 DDD)

    </details>

    <details>
    <summary><strong><code>TRUST 5 품질 프레임워크</code></strong>&#58; </summary>

    - 테스트, 가독성, 통합, 보안, 추적성을 보장하는 5가지 원칙

    </details>

- <strong><code>28개 전문 에이전트 및 멀티 에이전트 협업</code></strong>&#58; 
    - 각 개발 단계에 특화된 AI 에이전트 팀

    - 메인 에이전트와 서브 에이전트, 그리고 팀 단위의 에이전트가 병렬로 작업을 수행하며 복잡한 프로젝트 해결

- <strong><code>52개 스킬</code></strong>&#58; 
    - 다양한 개발 시나리오를 지원하는 확장 가능한 스킬 라이브러리

- <strong><code>다국어 지원</code></strong>&#58; 
    - 한국어, 영어, 일본어, 중국어 4개 언어 지원

- <strong><code>Sequential Thinking MCP</code></strong>&#58;
    -  단계별 추론을 통한 구조화된 문제 해결

- <strong><code>Ralph&#45;Style LSP Integration</code></strong>&#58; 
    - LSP 기반 자율 워크플로우와 실시간 품질 피드백

<a id="313eda9b0fe180f7887cf8178e039d33"></a>

## 주요 장점 (Advantages)

- <code>코드&#45;문서 동기화</code>
    - 코드가 수정될 때 초기 스펙 문서가 낙후되는 문제를 <code>sync</code> 기능을 통해 해결

    - 항상 최신 상태의 문서를 유지 가능

- <code>비용 및 성능 최적화</code>
    - 사용자의 예산이나 필요 성능에 따라 모델 수준(High, Medium, Low) 선택

    - 클로드(Claude) 외에도 가성비 좋은 GLM 모델 등을 혼합하여 사용 가능

- <code>강력한 자동 수정 (Loop)</code>
    - 오류가 발생했을 때 해결될 때까지 무한 반복하며 수정을 시도하는 루프 모드를 통해 개발자의 개입 최소화

- <code>크로스 플랫폼 및 언어 유연성</code>
    - Go 언어로 제작되어 다양한 OS(특히 윈도우)에서 안정적으로 동작

    - 개발자가 익숙하지 않은 언어도 개념만 알면 AI와 함께 개발하며 학습 가능

<a id="313eda9b0fe180d189d5e08fce732ff2"></a>

## 주요 CLI

- <strong><code>moai init</code></strong>&#58; 프로젝트 초기화 및 언어, 모델 레벨(High/Medium/Low) 등 기본 환경 설정&#46;

- <strong><code>moai project</code></strong>&#58; 프로젝트의 스택, 폴더 구조 등 메타데이터 정의 및 업데이트&#46;

- <strong><code>moai plan</code></strong>&#58; 프로젝트 문서(PRD, 설계서 등)를 기반으로 상세 구현 계획 생성&#46;

- <strong><code>moai run</code></strong>&#58; 생성된 플랜에 따라 실제 코드 구현 및 개발 작업 수행&#46;

- <strong><code>moai sync</code></strong>&#58; 구현된 코드를 분석하여 초기 스펙 문서를 최신화하고 동기화&#46;

- <strong><code>moai loop</code></strong>&#58; 오류가 해결되거나 작업이 완료될 때까지 에이전트가 자율적으로 반복 작업 수행&#46;

- <strong><code>moai cg</code></strong>&#58; 클로드(Claude)와 GLM 모델을 동시에 사용하여 작업 효율 극대화&#46;

- <strong><code>moai codemap</code></strong>&#58; 기존 프로젝트의 구조와 DB 구성 등을 분석하여 에이전트가 이해하기 쉬운 맵 생성&#46;

- <strong><code>moai review</code></strong><strong> / </strong><strong><code>moai coverage</code></strong>&#58; (v2&#46;5 신규) 코드 리뷰 및 테스트 커버리지 확인&#46;
