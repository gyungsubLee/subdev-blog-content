---
order: 1
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 371eda9b-0fe1-80a1-914c-c59a1e7cb26f
title: N8N 핵심 노드
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 26deda9b-0fe1-8020-9b16-fdc2892a939e
    title: n8n
  - id: 370eda9b-0fe1-80f5-a06a-e13297a970f7
    title: "바이브코딩 + 자동화 풀 패키지: 21개 프로젝트로 내 인생 자동화 (w. n8n x Claude Code)"
  - id: 371eda9b-0fe1-80a1-914c-c59a1e7cb26f
    title: N8N 핵심 노드
excerpt: reference - 페이지 N8N 핵심 노드 --- --- ✏️ 시나리오 고객 데이터를 수집하여 분석하고, 결과를 이메일과 스프레드시트로 저장하는 완전한 자동화 워크플로우 데이터 흐름 1. 트리거 (3가지 방법) 1. 데이터 수집 (HTTP Request) 1. 데이터 가공 (Code) 1. 검증 (IF) 1. 분할 (
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 370eda9b-0fe1-80f5-a06a-e13297a970f7
created: 2026-05-31T01:48:08.417Z
updated: 2026-06-10T15:32:03.984Z
legacy_path: Main/n8n-fdc2892a939e/바이브코딩 + 자동화 풀 패키지- 21개 프로젝트로 내 인생 자동화 (w. n8n-e13297a970f7/N8N 핵심 노드-c59a1e7cb26f/index.md
legacy_category: n8n
source_url: https://beautiful-college-c84.notion.site/371eda9b0fe180a1914cc59a1e7cb26f
---
<details>
<summary>reference</summary>

- <a href="https://beautiful-college-c84.notion.site/26bccaf841aa80c4975fd448e5f50c27">페이지</a> 

</details>

<a id="37beda9b0fe180219a70ccdf05a9f63a"></a>

## N8N 핵심 노드

---

---

![](8d48443b32da9aa6.webp)

> ✏️ 
> 
> > 시나리오
> 
> <a id="37beda9b0fe180ccb47ae3377bd97397"></a>
> 
> 고객 데이터를 수집하여 분석하고, 결과를 이메일과 스프레드시트로 저장하는 완전한 자동화 워크플로우
> 
> > 데이터 흐름
> 
> 1. 트리거 (3가지 방법)
> 
> 1. 데이터 수집 (HTTP Request)
> 
> 1. 데이터 가공 (Code)
> 
> 1. 검증 (IF)
> 
> 1. 분할 (Split Out)
> 
> 1. 필터링 (Filter)
> 
> 1. 라우팅 (Switch)
> 
> 1. 변환 (Set)
> 
> 1. 집계 (Aggregate)
> 
> 1. 병합 (Merge)
> 
> 1. 대기 (Wait)
> 
> 1. 반복 (Loop)
> 
> 1. 저장 (Google Sheets)
> 
> 1. 알림 (Gmail)
> 
> 1. 응답 (Respond to Webhook)

<a id="371eda9b0fe180249a81c0e5f6a77c83"></a>

### <code>트리거</code> 노드

1. Manual Trigger
    ![](ac64fdf0630f724d.webp)

    - N8N UI 내 클릭 버튼으로 트리거

1. Webhook Trigger
    ![](6fa7a43a0084b79d.webp)

    - 외부 시스템 연동 시 필수

    - 마지막 <code>respond to webhook</code> 필수
        ![](2ec119fa0d6f69ef.webp)

1. Schedule Trigger
    ![](ed4ada8489225c4d.webp)

    - cron job

    - 특정 시간에 실행되도록 트리거 가능

1. Merge Triggers
    ![](585dc246b293c5c7.webp)

    - 여러 트리거를 묶는 중간 노드

    - 위 3개 중 옵션으로 트리거 가능

<a id="371eda9b0fe18003ab9bd07772191db8"></a>

### <code>HTTP Request</code> 노드

![](485437a6f15b88ac.webp)

- 외부 API 콜 가능

<a id="37beda9b0fe18049851ad37f3a402892"></a>

### <code>Code</code> 노드

![](767fad6d20dc2058.webp)

- output 정형화 가능

- input 값을 원하는 output 형태로 데이터 변형

<a id="37beda9b0fe180e2aa70eea6a539bfc0"></a>

### <code>IF</code> 노드 (분기, 조건문 실행)

![](348e38b2c2657a03.webp)

- 조건에 따라 분기 처리

<a id="37beda9b0fe1801db53edcf6b1bf2ca7"></a>

### <code>Split Out</code> 노드

![](62dd6110898c32b6.webp)

- 한 덩어리였던 데이터를 여러 조각으로 쪼갤 수 있음

<a id="37beda9b0fe18007bbb9d14c577cf5ab"></a>

### <code>Filter</code> 노드

![](653023c908c0b327.webp)

- 원하는 데이터만 필터링 가능

- ex) <code>userType = 비지니스, 일반</code> 구분해서 필터링

<a id="37beda9b0fe1800a88a4fabb65511255"></a>

### <code>Switch</code> 노드

![](97018adaed9eead5.webp)

- 다중 분기

- <code>switch</code> 문 과 동일
    - 특정 조건들에 따라서 여러 분기처리

<a id="37beda9b0fe180479c8ded35ed0a9977"></a>

### <code>Set</code> 노드

![](19e1bcd545940c4a.webp)

- 각 등급에 맞는 라벨링 부여 가능

<a id="37beda9b0fe180e3833ac03c596afe3b"></a>

### <code>Merge</code> 노드

![](456263bc9995bac8.webp)

- 다양한 값들을 하나로 합칠 때 사용 

<a id="37beda9b0fe180a0ae3cfc660846a5cc"></a>

### <code>Aggregate</code> 노드

![](84d00edb8cce0084.webp)

- merge를 통해 들어오는 다양한 값들을 input로 받아 하나로 합치는데 사용

- 데이터 분석
    - 합계, 평균, 그룹화

<a id="37beda9b0fe180fab33ecd7bc706b55e"></a>

### <code>Wait</code> 노드

![](9d9491126989525b.webp)

- 대기 처리

- sleep 처리
    - 동영상 등 오래 걸리는 작업을 만드는데 <code>중요</code>

<a id="37beda9b0fe1800484d4d9bd55cdc375"></a>

### <code>Loop Over Items</code> 노드

![](618a7eb6bd2272d9.webp)

- 반복 처리 

- batch size를 설정하여 대용량 데이터를 나눠서 처리

- 엄청 많은 데이터를 한꺼번에 처리하면 워크플로우에서 오류가 발생됨<br>따라서 이를 쪼개면서 사용하면 오류없이 사용 가능

<a id="37beda9b0fe1806bb023e2175f50fb5b"></a>

### <code>Google Sheets</code> 노드

![](283426d34ecea044.webp)

- db 대신 google sheets로 데이터 저장 및 조회 가능

<a id="37beda9b0fe180d5afe0c0ef0be19ca7"></a>

### <code>Gmail</code> 노드

![](76c818f133941485.webp)

- gmail로 알림 보내기 가능

<a id="37beda9b0fe18056982bdda0139d2bdf"></a>

### <code>Response to Webhook</code> 노드

![](f177bc42b6faf332.webp)

- webhook 트리거 시 꼭 <code>respond to webhook</code>으로 <strong><u>end 노드</u></strong> 설정을 해야한다&#46;
