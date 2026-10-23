---
order: 42
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 22aeda9b-0fe1-806b-88b0-ce68b3e415bb
title: "[ 의문점 ] State sharing ( 동기화 문제 ) [ 보류 ]"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
    title: 탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )
  - id: 22aeda9b-0fe1-806b-88b0-ce68b3e415bb
    title: "[ 의문점 ] State sharing ( 동기화 문제 ) [ 보류 ]"
excerpt: 목차 - NestJS의 State sharing ( 동기화 문제 ) - Node.js의 싱글 스레드 모델 - 🤬 문제 - 멀티 인스턴스( 분산 환경)에서의 동기화 문제 - ✅ 해결 1 - NestJS의 State sharing ( 동기화 문제 ) --- [Documentation | NestJS - A progressi
cover: null
icon: 🧐
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
created: 2025-07-08T10:39:21.112Z
updated: 2025-07-10T04:15:43.229Z
legacy_path: Main/Nest.js-c3a886768c4d/탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )-d4fc3e106054/[ 의문점 ] State sharing ( 동기화 문제 ) [ 보류 ]-ce68b3e415bb/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/22aeda9b0fe1806b88b0ce68b3e415bb
---
> 
> 
> <a id="22aeda9b0fe18086aacccb93d1fa0cff"></a>
> 
> <strong>목차</strong>
> 
> - [NestJS의 State sharing ( 동기화 문제 )](#22aeda9b0fe1807a9e74ebef80373fd2)
> - [Node.js의 싱글 스레드 모델](#22aeda9b0fe180cba6dee02ece94fe80)
> - [🤬 문제 - 멀티 인스턴스( 분산 환경)에서의 동기화 문제](#22aeda9b0fe180a4881dfb776effe9a9)
> - [✅ 해결 1 - ](#22aeda9b0fe1800fa44fe5aff13b4f64)

<a id="22aeda9b0fe1807a9e74ebef80373fd2"></a>

## <strong>NestJS의 State sharing ( 동기화 문제 )</strong>

---

[Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()

> “using singleton instances in Nest is completely safe for our applications&#46;”

<a id="22aeda9b0fe180cba6dee02ece94fe80"></a>

### <strong>Node&#46;js의 싱글 스레드 모델</strong>

> ✏️ 
> 
> <a id="22aeda9b0fe180a28042e1094aa8d4e0"></a>
> 
> <code>Node&#46;js</code>는 <strong><u>이벤트 루프 기반의 Non&#45;blocking I/O</u></strong>와 <strong><u>싱글 스레드 이벤트 루프</u></strong>를 사용한다&#46;
> 
> - Java처럼 각 요청마다 새로운 스레드가 만들어지는 구조가 아니다&#46; 따라서 <strong><u> 공유 메모리에서의 동시성 문제가 일어나지 않</u></strong>는다&#46;
> 
> <a id="22aeda9b0fe1803a9401eb4573f0b9fd"></a>
> 
> 따라서 <strong><u>NestJS의 싱글톤 서비스</u></strong>는 기본적으로 <strong><u>모든 요청에 대해 공유</u></strong><strong>되며 </strong><strong><u>안전하게 재사용</u></strong>된다&#46;

<a id="22aeda9b0fe180a4881dfb776effe9a9"></a>

### 🤬 문제 &#45; 멀티 인스턴스( 분산 환경)에서의 동기화 문제

<a id="22aeda9b0fe180938a8fe45991db78b7"></a>

<strong> 단일 인스턴스</strong>에서는 <strong><u>동기화 문제가 없</u></strong>지만, 

- <code>JS</code>는 <u>싱글 스레드</u>이고, <code>Nest</code>는 <strong><u>싱글톤 DI</u></strong>를 기본으로 하기 때문에 <strong>멀티스레드에서 발생하는 race condition이나 동기화 이슈가 없다&#46;</strong>

<a id="22aeda9b0fe180d18e57e372505768a6"></a>

<strong><br></strong><strong><u>멀티 인스턴스 (분산 환경)</u></strong><strong>에서는 </strong><strong>동기화 문제가 발생</strong><strong>된다&#46;</strong>

<details>
<summary>ex 1) <strong>글로벌 캐시 동기화 문제</strong></summary>

- <code>A 서버</code>&#58; <code>사용자 ID&#58; 1</code>의 정보를 캐시에 저장

- <code> B 서버</code>&#58; <code>사용자 ID&#58; 1</code>의 DB를 수정했지만 A 서버는 여전히 이전 캐시 보유

<a id="22aeda9b0fe18025bb8ad01acfb69ff5"></a>

<strong> ⇒ Stale Cache</strong>

</details>

<details>
<summary>ex 2) <strong>세션, 로그인 상태 공유 문제</strong></summary>

- <code>A 서버</code>에서 로그인 → 세션이 메모리에 저장됨

- <code>B 서버</code>에서 다음 요청 → 로그인 정보 없음 

<a id="22aeda9b0fe180d2bd22e4d55dce5287"></a>

⇒  <strong>로그아웃 상태로 인식</strong>

</details>

<details>
<summary>ex 3) <strong>요청별 상태 저장 (Request Scope)</strong></summary>

- 요청마다 다른 테넌트(DB 커넥션 등)를 써야 하는 경우 
    <a id="22aeda9b0fe18009924fd1a468241884"></a>

    → 싱글톤 서비스는 공유되므로 문제가 발생

</details>

<a id="22aeda9b0fe1800fa44fe5aff13b4f64"></a>

### ✅ 해결 1 &#45; 

<a id="22aeda9b0fe180ecbaf6dc8be5571a57"></a>

<strong>1&#46; NestJS의 확장 구조</strong>

<a id="22aeda9b0fe180b8936bcb8b172ebcb9"></a>

```javascript
@Injectable({ scope: Scope.REQUEST })
export class RequestScopedService {
  constructor(@Inject(REQUEST) private readonly request: Request) {}
}
```

<a id="22aeda9b0fe180458164edb7e2e413bb"></a>

NestJS는 이런 문제들을 대비해서 다음을 지원<br>

<a id="22aeda9b0fe1809787c0f769eb9c1ab7"></a>

<br><br><br>
