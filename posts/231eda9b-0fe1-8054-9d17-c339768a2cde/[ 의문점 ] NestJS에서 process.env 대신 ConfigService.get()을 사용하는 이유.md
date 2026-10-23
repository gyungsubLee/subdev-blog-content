---
order: 29
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 231eda9b-0fe1-8054-9d17-c339768a2cde
title: "[ 의문점 ] NestJS에서 process.env 대신 ConfigService.get()을 사용하는 이유"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
    title: 탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )
  - id: 231eda9b-0fe1-8054-9d17-c339768a2cde
    title: "[ 의문점 ] NestJS에서 process.env 대신 ConfigService.get()을 사용하는 이유"
excerpt: 목차 - [[의문점]](231eda9b0fe181cca2a4dbe2411aa9d8) - 예시 - Config 방식의 장점 - 비교 - 정리 - 언제 ConfigService.get()을 써야 하는가? - Reference [의문점] 🧐 NestJS에서 process.env 대신 ConfigService.get()을 사용
cover: null
icon: 🧐
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
created: 2025-07-15T07:48:09.734Z
updated: 2025-07-15T07:57:00.960Z
legacy_path: Main/Nest.js-c3a886768c4d/탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )-d4fc3e106054/[ 의문점 ] NestJS에서 process.env 대신 ConfigService-c339768a2cde/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/231eda9b0fe180549d17c339768a2cde
---
> 
> 
> <a id="231eda9b0fe181f8b6cdebcbbf680645"></a>
> 
> 목차
> 
> - [[의문점]](#231eda9b0fe181cca2a4dbe2411aa9d8)
> - [예시](#231eda9b0fe180c0aaf4c37a8abb55f0)
> - [Config 방식의 장점](#231eda9b0fe1809f9945d156606cd4bb)
> - [비교](#231eda9b0fe180ac9e77f7972f330b65)
> - [정리 - 언제 ConfigService.get()을 써야 하는가?](#231eda9b0fe1808f895fd4ed47fab755)
> - [Reference](#231eda9b0fe1807dad43e99d141bbb4c)

<a id="231eda9b0fe181cca2a4dbe2411aa9d8"></a>

### &#91;의문점&#93;

> 🧐 
> 
> <a id="231eda9b0fe181b2887fd1df2d20a817"></a>
> 
> NestJS에서 <code>process&#46;env</code> 대신 <code>ConfigService&#46;get()</code>을 사용하는 이유

<a id="231eda9b0fe180c0aaf4c37a8abb55f0"></a>

### 예시

<details>
<summary><strong>1&#46; </strong><strong><code>process&#46;env</code></strong><strong> 방식</strong></summary>

<a id="231eda9b0fe180b6be71e28d22347458"></a>

```typescript
const accessKey = process.env.AWS_S3_ACCESS_KEY;
```

- 직접 접근하므로 Nest의 DI 컨테이너 밖에서 관리됨 → 테스트, 환경 전환에 불리함

</details>

<details>
<summary><strong>2&#46; </strong><strong><code>ConfigService&#46;get()</code></strong><strong> 방식</strong></summary>

<a id="231eda9b0fe180e98b63c117e744f5aa"></a>

```typescript
const accessKey = this.configService.get('AWS_S3_ACCESS_KEY');
```

- Nest의 DI 컨테이너가 관리 → 다양한 환경, 유닛 테스트에서도 유연하게 대응 가능

</details>

<a id="231eda9b0fe180b98ab1c15eb111a4da"></a>

<br>

<a id="231eda9b0fe1809f9945d156606cd4bb"></a>

### <strong><code>Config</code></strong><strong> 방식의 장점</strong>

<details>
<summary>1&#46; <strong>테스트 코드에서 Mocking 쉬움</strong></summary>

<a id="231eda9b0fe1804bb34dd43d8da0bce9"></a>

```typescript
const mockConfigService = {
  get: jest.fn((key) => {
    if (key === 'AWS_S3_ACCESS_KEY') return 'mock-access-key';
  }),
};
```

- 유닛 테스트 시 process&#46;env는 별도 조작이 까다로움

- ConfigService는 DI로 주입되므로 쉽게 Mock 처리 가능

</details>

<details>
<summary>2&#46; <strong>환경 구성 분리 (</strong><strong><code>&#46;env&#46;dev</code></strong><strong>, </strong><strong><code>&#46;env&#46;prod</code></strong><strong>)</strong></summary>

<a id="231eda9b0fe18065ac44eb393617fec1"></a>

```typescript
ConfigModule.forRoot({
  isGlobal: true,
  envFilePath: ['.env.dev', '.env'],
});
```

- <code>&#46;env</code> 파일을 구분하고 싶을 때 <code>ConfigModule&#46;forRoot()</code>에서 설정 가능

- 이렇게 하면 <code>process&#46;env</code> 직접 접근이 아니라 <code>ConfigService</code>를 통해 통합 관리 가능

</details>

<details>
<summary>3&#46; <strong>모듈 간 종속성 제거</strong></summary>

<a id="231eda9b0fe180e4a289fb89613e3199"></a>

```typescript
MongooseModule.forRootAsync({
  useFactory: (configService: ConfigService) => ({
    uri: configService.get<string>('MONGO_URI'),
  }),
  inject: [ConfigService],
});
```

- DB 모듈에서 위처럼 동적으로 구성 가능
    - <code>process&#46;env</code>를 쓰면 DI 불가

- <code>ConfigService</code>는 NestJS가 관리하므로 다른 모듈에서도 안전하게 의존 가능<br><br>

---

</details>

<a id="231eda9b0fe180ac9e77f7972f330b65"></a>

### 비교

| <strong>항목</strong> | process&#46;env&#46;XXX | configService&#46;get(&#39;XXX&#39;) |
| --- | --- | --- |
| <strong>직접 접근 방식</strong> | 환경변수에 직접 접근 | ConfigModule이 관리 |
| <strong>테스트 환경에서 유연성</strong> | 불편함 (수동 세팅 필요) | ✅ Mocking 용이 |
| <strong>DI(의존성 주입)</strong> | ❌ 불가 | ✅ 가능 |
| <strong>동적 구성 (예&#58; DB URL 구성)</strong> | ❌ 불편함 | ✅ 가능 |
| <strong>모듈 간 공유</strong> | ❌ 어려움 | ✅ 전역 모듈로 가능 |
| <strong>런타임 변경 감지</strong> | ❌ 불가능 | (보통 없음) |
| <strong>권장 여부</strong> | ❌ NestJS에서는 비권장 | ✅ 공식 권장 방식 |

<a id="231eda9b0fe1808f895fd4ed47fab755"></a>

### 정리 &#45; <strong>언제 </strong><strong><code>ConfigService&#46;get()</code></strong><strong>을 써야 하는가?</strong>

| <strong>상황</strong> | <strong>사용 권장</strong> |
| --- | --- |
| 단순한 설정값만 읽는 작은 스크립트 | <code>process&#46;env</code>로도 충분 |
| NestJS 앱에서 구성, 유연성, 테스트 고려 | ✅ <code>ConfigService&#46;get()</code> 강력 추천 |
| 유닛 테스트에서 환경을 모킹해야 할 때 | ✅ <code>ConfigService&#46;get()</code> |

<a id="231eda9b0fe1807dad43e99d141bbb4c"></a>

### Reference

[Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()

[Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()
