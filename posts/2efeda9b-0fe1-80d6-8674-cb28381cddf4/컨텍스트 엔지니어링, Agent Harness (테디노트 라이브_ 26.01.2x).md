---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 2efeda9b-0fe1-80d6-8674-cb28381cddf4
title: "컨텍스트 엔지니어링, Agent Harness (테디노트 라이브: 26.01.2x)"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 3efeda9b-0fe1-80b6-940d-e56cb496cf28
    title: Agent
  - id: 2f7eda9b-0fe1-80e2-a643-cd387204f4e4
    title: 에이전트
  - id: 2efeda9b-0fe1-80d6-8674-cb28381cddf4
    title: "컨텍스트 엔지니어링, Agent Harness (테디노트 라이브: 26.01.2x)"
excerpt: reference - ‣ - ‣ - ‣ - 컨텍스트 엔지니어링 참고할 만한 레퍼런스 Anthropic x Forum Ventures 해커톤 해커톤 우승자 팁 - ‣ - ‣ - ‣ - ‣ - ‣ - ‣ - ‣ 추가 팁 프론트 - playright agent - vercel 에이전트 브라우저 agent-browser - e2
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 2f7eda9b-0fe1-80e2-a643-cd387204f4e4
created: 2026-01-21T13:26:03.131Z
updated: 2026-03-19T03:27:23.171Z
legacy_path: Main/Agent-e56cb496cf28/에이전트-cd387204f4e4/컨텍스트 엔지니어링, Agent Harness (테디노트 라이브- 26.01.2x-cb28381cddf4/index.md
legacy_category: Agent
source_url: https://beautiful-college-c84.notion.site/2efeda9b0fe180d68674cb28381cddf4
---
<details>
<summary>reference</summary>

- ‣

- ‣

- ‣

- 

</details>

<a id="313eda9b0fe1802c9d2ac90616d26673"></a>

## 컨텍스트 엔지니어링

![](ab4d33907b15908b.webp)

<a id="2efeda9b0fe180fb885bea0f96a5ec8c"></a>

## 참고할 만한 레퍼런스

[Anthropic x Forum Ventures 해커톤 해커톤 우승자 팁](#/post/313eda9b-0fe1-807e-859c-feab26261440)

- ‣

- ‣

- ‣

- ‣

- ‣

- ‣

- ‣

<a id="313eda9b0fe180328e22d61dc8aa100e"></a>

## 추가 팁

<a id="2efeda9b0fe180b48274f337ed8b953c"></a>

### 프론트

- playright agent

- vercel 에이전트 브라우저
    [agent-browser](https://github.com/vercel-labs/agent-browser)

    - e2e 테스트 

- vercel react best pratice
    [agent-skills](https://github.com/vercel-labs/agent-skills)

- stitch&#45;ai&#45;mcp
    [stitch-ai-mcp](https://github.com/StitchAI/stitch-ai-mcp)

    - stich로 디자인을 하고 mcp로 입힌다&#46; 
        - 구글 &#45; 공짜로 이용 가능

<a id="2efeda9b0fe18057beb0ffc80a8be67f"></a>

### 데브옵스

> ✏️ 
> 
> <a id="313eda9b0fe180cba86fec5d8f25bc72"></a>
> 
> 코드 레퍼를 주고 가져오라고 지시 후 <strong><u>내부 SDK를 가져와 스킬로 생성</u></strong>

[azure-pipelines-agent](https://github.com/microsoft/azure-pipelines-agent)

- 공식 스킬들

- GCP MCP 지원

- AWS MCP 지원

<a id="2efeda9b0fe180e4814dee311326a733"></a>

### TDD

<a id="2efeda9b0fe180edb3a3d194729fbe3c"></a>

켄트백 스킬을 프롬프트로 

- 코드 전체 아키텍처를 판단하는 스킬을 만들고,
    - 백엔드 성격에 따른 트래픽 구성 및 발전 아키텍처를 물어본다&#46;

- AskUserQuestionTool
    ![](b0b48d6a32c91f24.webp)

<a id="2efeda9b0fe18033b651fe36d4b50a13"></a>

### 서칭

[Code Search &#124; Grep by Vercel]()

- 코드의 핵심 기능 바로 서칭 가능
    - 굉장히 빠름

> ☝🏻 
> 
> <a id="313eda9b0fe180cdbf1acad57e2997bf"></a>
> 
> 클로드 코드 기본 웹서치가 별로다
> 
> <a id="313eda9b0fe180119c0fe6ac15a6f5d3"></a>
> 
> 기본 웹서치 사용 x 
> 
> <a id="313eda9b0fe18068b500ed4ab684c3db"></a>
> 
> 클로드 전역 시스템 프롬프트에  2개 실행하도록 처리 ( 파이썬 실행 )

<a id="2efeda9b0fe180c2bf7acd038fae054e"></a>

### tavilly search

[Tavily]()

- 기본 웹서치 툴 &#45; 일반적인 지식

- 클로드 코디 웹서치  &#45; 디나이

<a id="2efeda9b0fe1802c8f39fc8eff3dfda2"></a>

### exa search

[Exa]()

- exa search mcp &#45; 일부 무료

- 1000건까지 무료

- api 키를 아에 안넣고도 무료로 사용가능하다&#46;
    <a id="2efeda9b0fe180f6b6e8ed261763d811"></a>

    ‣

- 코드 스니펫 검색

-  코드 서칭
    - context(exa code)

    - 1차 exa 서칭 → tavily 웹서치 대용으로 사용 중이다&#46;

    - context7는 공식 문서만 가져온다&#46; 
        - 정확한 키워드를 아는 경우 exa가 더 좋았다&#46;

<a id="2efeda9b0fe18010942fc0ad3370818b"></a>

### gemini

[gemini-cli](https://github.com/google-gemini/gemini-cli)

<a id="2efeda9b0fe18041b26ed2f4762447b0"></a>

재미니 모델에 기본적으로 웹서치가 포함되어 있다&#46; 

- raddit, 유튜브 서칭 가능

> 🤔 
> 
> <a id="313eda9b0fe180d0aff1f820b7f6004a"></a>
> 
> cli 도구들을 잘 엮어서 써야한다&#46; 
> 
> <a id="313eda9b0fe180888dc0c00a9db7200a"></a>
> 
> 결국은 구글을 통해 탐색 → 구글 주식? 구매?

<a id="2efeda9b0fe1802782c6c98adc260e13"></a>

### agent&#45;council

[agent-council](https://github.com/team-attention/agent-council)

- 코덱스, 재미니

- qwen&#45;code 
    - 퀄리티 좋다&#46; sonet 비슷

    - GLM이 좀더 좋다&#46;

    - 가진 기능이 좋다&#46; 

    - gemini cli 기반으로 만들어져 웹서칭 기능이 좋다&#46; 

    - 다 가져올 수 있다? 

<a id="2efeda9b0fe18043b161db5864dea546"></a>

### 대한민국 하네스

<a id="2efeda9b0fe1804b9129c17ef3edabbc"></a>

MoAI&#45;ADK

[moai-adk](https://github.com/modu-ai/moai-adk)

- 클로드 코드에 GLM을 세팅해서 사용하고 있다&#46; 

- 자세한 내용&#58; <a href="#/post/312eda9b-0fe1-806e-86d7-f34cfc05ed83">페이지</a>
