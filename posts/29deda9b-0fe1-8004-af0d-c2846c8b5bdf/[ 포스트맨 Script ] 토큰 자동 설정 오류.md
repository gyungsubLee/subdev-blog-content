---
order: 2
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 29deda9b-0fe1-8004-af0d-c2846c8b5bdf
title: "[ 포스트맨 Script ] 토큰 자동 설정 오류"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 260eda9b-0fe1-801b-836b-c2e229a88ff9
    title: 한 번에 끝내는 NestJS 패키지 - Part 1. 기초
  - id: 29deda9b-0fe1-8004-af0d-c2846c8b5bdf
    title: "[ 포스트맨 Script ] 토큰 자동 설정 오류"
excerpt: 목차 - 문제점 - 원인 - 해결 문제점 --- ❗ 포스트맨으로 API 테스트 시, Role 기반 접근 제어 기능(RBAC)이 제대로 동작하지 않음 강의 학습 중, API 테스트 시 설계한 동작과 다르게 오류가 발생됨 해당 API의 Header에 직접 token 값을 할당하여 call 한 결과 정상 실행되는 것이 확인되어
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 260eda9b-0fe1-801b-836b-c2e229a88ff9
created: 2025-10-31T12:15:17.436Z
updated: 2025-10-31T12:33:06.692Z
legacy_path: Main/Nest.js-c3a886768c4d/한 번에 끝내는 NestJS 패키지 - Part 1. 기초-c2e229a88ff9/[ 포스트맨 Script ] 토큰 자동 설정 오류-c2846c8b5bdf/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/29deda9b0fe18004af0dc2846c8b5bdf
---
> 
> 
> <a id="29deda9b0fe180258677d6d000e1caf7"></a>
> 
> <strong>목차</strong>
> 
> - [문제점](#29deda9b0fe1800cbd9ec291eff9b9b6)
> - [원인](#29deda9b0fe1808287a6e4a70b44c5e0)
> - [해결](#29deda9b0fe18095b364d373ce32581d)

<a id="29deda9b0fe1800cbd9ec291eff9b9b6"></a>

## 문제점

---

> ❗ 
> 
> <a id="29deda9b0fe180e9aa9bca7b6098c302"></a>
> 
> 포스트맨으로 API 테스트 시, Role 기반 접근 제어 기능(<code>RBAC</code>)이 제대로 동작하지 않음

<a id="29deda9b0fe180f2bd77eff6d226de5b"></a>

강의 학습 중, API 테스트 시 설계한 동작과 다르게 오류가 발생됨

<a id="29deda9b0fe18094b4d9cd1fd454cc76"></a>

해당 API의 Header에 직접 token 값을 할당하여 call 한 결과 정상 실행되는 것이 확인되어 console 값을 확인 했더니 아래와 같이 null 으로 들어가는 것을 확인함

![](e2e15f9491195528.webp)

<a id="29deda9b0fe1808287a6e4a70b44c5e0"></a>

## 원인

---

<a id="29deda9b0fe180cc8387faa89497f575"></a>

```typescript
pm.test("Status code is 201", function () {
    pm.response.to.have.status(201);

    const body = pm.response.json();

    pm.environment.set('refreshToken', body.refreshToken)
    pm.environment.set('accessToken', body.accessToken)
});
```

기존 스크립트

<a id="29deda9b0fe1805ea015c81d9bac8501"></a>

```typescript
{
    "success": true,
    "data": {
        "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOjIsInJvbGUiOjAsInR5cGUiOiJyZWZyZXNoIiwiaWF0IjoxNzYxOTEyODc2LCJleHAiOjE3NjE5OTkyNzZ9.maLYp2wg9u_Zdh0-e58jmYbYtFJ9_hU58zdcqgeBVpo",
        "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOjIsInJvbGUiOjAsInR5cGUiOiJhY2Nlc3MiLCJpYXQiOjE3NjE5MTI4NzYsImV4cCI6MTc2MTkxMzE3Nn0.YIX5NYY0P2WFaolReuxmKWrP0tU9cHHiymjelNrNwAw"
    },
    "requestId": "50d00a93-a2c9-4b60-a1e6-e9631cb2206d",
    "timestamp": "2025-10-31T12:14:36.243Z"
}
```

응답 예시

<a id="29deda9b0fe180518979d8fdcd7b7eec"></a>

공통 응답 형식을 Interceptor를  추가하여 정의함

<a id="29deda9b0fe180e684b8eb7835bff3f2"></a>

따라서 응답에 대한 depth가 추가되어 <code>body&#46;refreshToken</code> 가 아닌 <code>body&#46;data&#46;refreshToken</code>가 되었어야 헀음

<a id="29deda9b0fe18095b364d373ce32581d"></a>

## 해결

---

> ✏️ 
> 
> <a id="29deda9b0fe180a58f35c85b4c6c3fdb"></a>
> 
> <strong>안전 파싱, 다중 경로 지원, 상태 코드 유연 처리, 로그</strong>

<a id="29deda9b0fe1806a9bf4c3804890120a"></a>

```typescript
pm.test("Status is 200/201", function () {
  pm.expect(pm.response.code).to.be.oneOf([200, 201]);
});

let text = pm.response.text();
let body = null;

try {
  body = pm.response.json();
} catch (e) {
  console.error("[Tests] JSON parse failed:", e);
  console.info("[Tests] Raw response text:", text);
}

if (!body) {
  // JSON이 아닐 때는 여기서 종료
  pm.test("Response has JSON body", function () {
    pm.expect(body, "JSON body should exist").to.not.be.null;
  });
} else {
  console.log("[Tests] Response JSON:", body);

  // 여러 경로 중 하나라도 있으면 세팅
  const accessToken =
    body.accessToken ??
    body.token ??
    body?.data?.accessToken ??
    body?.tokens?.access ??
    body?.jwt?.accessToken;

  const refreshToken =
    body.refreshToken ??
    body?.data?.refreshToken ??
    body?.tokens?.refresh ??
    body?.jwt?.refreshToken;

  if (accessToken) {
    pm.environment.set("accessToken", accessToken);
    console.log(`[Tests] accessToken set: ${accessToken}`);
  } else {
    console.warn("[Tests] accessToken not found in response JSON");
  }

  if (refreshToken) {
    pm.environment.set("refreshToken", refreshToken);
    console.log(`[Tests] refreshToken set: ${refreshToken}`);
  } else {
    console.warn("[Tests] refreshToken not found in response JSON");
  }
}
```

수정된 스크립트

![](66f4f72804ddedc6.webp)

<a id="29deda9b0fe180ad93d1e8a856702ece"></a>

스크립트는 위와 같이 Postman script 섹션에 정의함
