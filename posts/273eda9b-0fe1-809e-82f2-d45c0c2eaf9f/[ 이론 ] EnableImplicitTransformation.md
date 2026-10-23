---
order: 4
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 273eda9b-0fe1-809e-82f2-d45c0c2eaf9f
title: "[ 이론 ] EnableImplicitTransformation"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 260eda9b-0fe1-801b-836b-c2e229a88ff9
    title: 한 번에 끝내는 NestJS 패키지 - Part 1. 기초
  - id: 26feda9b-0fe1-8079-9060-e36e01d3f411
    title: 페이지네이션( Pagination )
  - id: 273eda9b-0fe1-809e-82f2-d45c0c2eaf9f
    title: "[ 이론 ] EnableImplicitTransformation"
excerpt: 목차 - [[ 옵션 ] EnableImplicitTransformation 설정](273eda9b0fe180f1b538f2314aff01c1) - [ [ 문제점 ] Query Parameter 타입 오류](290eda9b0fe180e98e13e916c3944884) - [ [ 해결 ] EnableImplicitTransf
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 26feda9b-0fe1-8079-9060-e36e01d3f411
created: 2025-09-19T11:41:07.696Z
updated: 2025-10-18T15:31:59.861Z
legacy_path: Main/Nest.js-c3a886768c4d/한 번에 끝내는 NestJS 패키지 - Part 1. 기초-c2e229a88ff9/페이지네이션( Pagination )-e36e01d3f411/[ 이론 ] EnableImplicitTransformation-d45c0c2eaf9f/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/273eda9b0fe1809e82f2d45c0c2eaf9f
---
> 
> 
> <a id="273eda9b0fe18059bbccc2f8fef07e3b"></a>
> 
> <strong>목차</strong>
> 
> - [[ 옵션 ] EnableImplicitTransformation 설정](#273eda9b0fe180f1b538f2314aff01c1)
> - [ [ 문제점 ] Query Parameter 타입 오류](#290eda9b0fe180e98e13e916c3944884)
> - [ [ 해결 ] EnableImplicitTransformation](#273eda9b0fe180189268c8e33fc488a4)

<a id="273eda9b0fe180f1b538f2314aff01c1"></a>

## &#91; 옵션 &#93; EnableImplicitTransformation 설정

---

<a id="290eda9b0fe180e98e13e916c3944884"></a>

###  &#91; 문제점 &#93; Query Parameter 타입 오류

<a id="290eda9b0fe180b28e06e4212b097b33"></a>

모든 Query는 URL인 string 값으로 넘어온다&#46; 따라서 DTO의 검증을 통과하지 못한다&#46; 

- page, size → <code>&#64;IsInt()</code>  오류 발생

<a id="273eda9b0fe180189268c8e33fc488a4"></a>

###  &#91; 해결 &#93; EnableImplicitTransformation

<a id="290eda9b0fe18038b84cda0039407258"></a>

```typescript
// main.ts
async function bootstrap() {
	const app = await NestFactory.create(AppModule);
	app.useGlobalPipes(new ValidationPipe({
		whitelist: true,
		forbidNonWhiteliseted: true,
		transformOptions: {
			enableImplicitConversion: true,
		}
	}));
	await app.listen(3000);
}
bootstrap();
```

<a id="273eda9b0fe180c09d2bd603ce1ff240"></a>

Global Pipe의 <code>transformOptions</code> &#45; <code>enableImplicitConversion&#58; true</code>  옵션을 설정하면 <strong><u>DTO에 정의한 타입으로 자동 타입 변환</u></strong>을 한다&#46;

<a id="290eda9b0fe180079a16d33ec406833c"></a>

이로 인해 Query Parameter로 받아오는 <code>page</code>, <code>size</code> 값을 int 형으로 자동 변환시켜 해결할 수 있다&#46;
