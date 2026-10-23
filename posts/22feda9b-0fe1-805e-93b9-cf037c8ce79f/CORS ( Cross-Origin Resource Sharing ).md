---
order: 10
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 22feda9b-0fe1-805e-93b9-cf037c8ce79f
title: CORS ( Cross-Origin Resource Sharing )
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
    title: 탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )
  - id: 22feda9b-0fe1-805e-93b9-cf037c8ce79f
    title: CORS ( Cross-Origin Resource Sharing )
excerpt: 목차 - Same-Origin Policy ( SOP ) - CORS ( Cross-Origin Resource Sharing ) - CORS 요청의 흐름 - NestJS CORS 허용 설정 - Reference Same-Origin Policy ( SOP ) --- 📖 브라우저 보안 정책으로, 출처(origin)가 다
cover: fb3b1ee7da4a15e0.webp
icon: 9bed2eae1e079b4b.avif
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
created: 2025-07-13T10:28:58.444Z
updated: 2025-07-31T06:23:32.625Z
legacy_path: Main/Nest.js-c3a886768c4d/탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )-d4fc3e106054/CORS ( Cross-Origin Resource Sharing )-cf037c8ce79f/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/22feda9b0fe1805e93b9cf037c8ce79f
---
> 
> 
> <a id="22feda9b0fe1819aa044cffd4ab2f5eb"></a>
> 
> <strong>목차</strong>
> 
> - [Same-Origin Policy ( SOP )](#22feda9b0fe180619ef6d25ee9a1c6ef)
> - [CORS ( Cross-Origin Resource Sharing )](#22feda9b0fe1816e87bac12bd731cc09)
> - [CORS 요청의 흐름](#22feda9b0fe18094ba68fb1603998f70)
> - [NestJS CORS 허용 설정](#22feda9b0fe18033bc8efc834f3cbb7a)
> - [Reference](#22feda9b0fe180c5a0c4f9f8f9d15f6a)

<a id="22feda9b0fe180619ef6d25ee9a1c6ef"></a>

## Same&#45;Origin Policy ( SOP )

---

> 📖 
> 
> <a id="22feda9b0fe180ff9f92d10f4cea9d70"></a>
> 
> 브라우저 보안 정책으로, <strong><code>출처(origin)</code></strong>가 다르면 리소스를 공유할 수 없다&#46; 
> 
> > <strong><code>출처(origin)</code></strong><strong>는  프로토콜 &#43; 도메인 &#43; 포트</strong>가 모두 같아야 한다&#46;

<details>
<summary>ex)</summary>

- ✅ 동일 출처
    - <code>http&#58;//example&#46;com&#58;3000</code> ↔ <code>http&#58;//example&#46;com&#58;3000</code>

- ❌ 동일하지 않은 출처
    - <code>http&#58;//example&#46;com&#58;3000</code> ↔ <code>http</code><u><code>s</code></u><code>&#58;//example&#46;com&#58;3000</code>

    <a id="22feda9b0fe180bf916acb5472c124ea"></a>

       →  프로토콜이 다름

</details>

<a id="22feda9b0fe1816e87bac12bd731cc09"></a>

## CORS ( Cross&#45;Origin Resource Sharing )

---

> 📖 
> 
> <a id="22feda9b0fe181108eeee2840859a71c"></a>
> 
> SOP를 완화해서 <u>특정 조건 하에 리소스 공유를 허용</u><strong>하는 정책이다&#46;</strong>
> 
> - 서버가 응답 헤더에 <code>Access&#45;Control&#45;Allow&#45;&#42;</code> 를 설정해서 허용 여부를 명시한다&#46;

<a id="22feda9b0fe18094ba68fb1603998f70"></a>

### <strong>CORS 요청의 흐름</strong>

> ✏️ 
> 
> <a id="22feda9b0fe180ac81a8c76423e04841"></a>
> 
> <code>&#91; 라우저 → 서버 &#93;</code> 요청에는 두 가지 형태의 흐름이 있다&#46;

<details>
<summary><strong>1&#46; Simple Request (단순 요청)</strong></summary>

> 
> 
> <a id="22feda9b0fe180dea62cc4bc2a0935c4"></a>
> 
> 조건
> 
> - <code>메서드</code>&#58; GET, POST, HEAD
> 
> - <code>헤더</code>
>     - Content&#45;Type 아래 조건만 허용
>         - <code>application/x&#45;www&#45;form&#45;urlencoded</code>
> 
>         - <code>multipart/form&#45;data</code>
> 
>         -  <code>text/plain</code>

<a id="22feda9b0fe180cab29bc2b539a0349f"></a>

```json
Access-Control-Allow-Origin: http://localhost:3000
```

- 서버가 응답 시 위 헤더를 포함해야 함<br>

</details>

<details>
<summary>2&#46; <strong>Preflight Request (사전 요청)</strong></summary>

> 
> 
> 1.  조건을 벗어나면 브라우저는 OPTIONS 요청을 먼저 보냄
> 
> 1. 서버가 허용하는지 체크

<a id="22feda9b0fe180db8598da469bf8e272"></a>

```typescript
Access-Control-Allow-Origin: http://localhost:3000
Access-Control-Allow-Methods: POST, GET, OPTIONS
Access-Control-Allow-Headers: Content-Type, Authorization
```

<a id="22feda9b0fe1803987ebe95dc90a9ad0"></a>

<br>

</details>

<a id="22feda9b0fe18033bc8efc834f3cbb7a"></a>

## <strong>NestJS CORS 허용 설정</strong>

---

1. <strong>모든 요청 허용 (개발 환경에서만 사용 권장)</strong>
    <a id="22feda9b0fe18035b80ecd36f7d051fe"></a>

    ```typescript
    // main.ts
    async function bootstrap() {
      const app = await NestFactory.create(AppModule);
      app.enableCors(); // 기본적으로 모든 origin 허용
      await app.listen(3000);
    }
    ```

1. 특정 도메인만 허용
    <a id="22feda9b0fe180988fd2eb38eb6225c7"></a>

    ```typescript
    // main.ts
    app.enableCors({
      origin:
        process.env.Mode === 'dev' ? '*' : process.env.CORS_ORIGIN?.split(','),
      methods: 'GET,HEAD,PUT,PATCH,POST,DELETE',
      credentials: true,
    });
    ```

    <a id="22feda9b0fe180c4b195faa64e8c2247"></a>

    ```json
    // .env
    MODE="dev"
    CORS_ORIGIN=http://localhost:3000,http://172.29.49.124:3000
    ```

    - 환경변수 설정에 대한 자세한 내용은 해당 포스팅 참조&#58; <a href="#/post/22deda9b-0fe1-8083-960b-faeeff88659d">페이지</a> 

<a id="22feda9b0fe180c5a0c4f9f8f9d15f6a"></a>

## Reference

[Cross&#45;Origin Resource Sharing (CORS) &#45; HTTP &#124; MDN]()

[Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()

[npm&#58; cors]()
