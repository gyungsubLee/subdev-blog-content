---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 27deda9b-0fe1-8132-ba2a-ce3ec6ce4f7e
title: "[ 실습 ] Mapped Type 적용"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 260eda9b-0fe1-801b-836b-c2e229a88ff9
    title: 한 번에 끝내는 NestJS 패키지 - Part 1. 기초
  - id: 27deda9b-0fe1-80a6-a020-ffa3bb1ef371
    title: Mapped Types
  - id: 27deda9b-0fe1-8132-ba2a-ce3ec6ce4f7e
    title: "[ 실습 ] Mapped Type 적용"
excerpt: "목차 - Mapped Type 적용 - 1. Partial Type Mapped Type 적용 --- ✏️ Create → Update 1. Partial Type typescript export class CreateMoviceDto { @IsNotEmpty() @IsString() title: string; @IsNo"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 27deda9b-0fe1-80a6-a020-ffa3bb1ef371
created: 2025-09-29T11:09:23.264Z
updated: 2025-10-03T22:53:04.815Z
legacy_path: Main/Nest.js-c3a886768c4d/한 번에 끝내는 NestJS 패키지 - Part 1. 기초-c2e229a88ff9/Mapped Types-ffa3bb1ef371/[ 실습 ] Mapped Type 적용-ce3ec6ce4f7e/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/27deda9b0fe18132ba2ace3ec6ce4f7e
---
> 
> 
> <a id="27deda9b0fe181b2ac51d41b508589cc"></a>
> 
> <strong>목차</strong>
> 
> - [ Mapped Type 적용](#27deda9b0fe1815eb048f1ee4af54770)
> - [1. Partial Type](#27deda9b0fe18107a214df21ccc4a0a7)

<a id="27deda9b0fe1815eb048f1ee4af54770"></a>

##  Mapped Type 적용

---

> ✏️ 
> 
> <a id="27deda9b0fe1808996d7eed3992cf1ce"></a>
> 
> Create → Update

<a id="27deda9b0fe18107a214df21ccc4a0a7"></a>

### 1&#46; Partial Type

<a id="27deda9b0fe18115b963da024fd36d2d"></a>

```typescript
export class CreateMoviceDto {
		@IsNotEmpty()
		@IsString()
		title: string;
		
		@IsNotEmpty()
		@IsString()
		detail: string;
		
		@IsNotEmpty()
		@IsString()
		derectorId: number;
		
		@IsNotEmpty()
		@ArrayNotEmpty()
		@IsNumber({}, {
				each: true,
		})
		genreIds: number[];
}
```

<details>
<summary>적용 전</summary>

<a id="27deda9b0fe18061a66cff3e6fe8f341"></a>

```typescript
export class UpdateMoviceDto {
		@IsNotEmpty()
		@IsString()
		@IsOptional()
		title: string;
		
		@IsNotEmpty()
		@IsString()
		@IsOptional()
		detail: string;
		
		@IsNotEmpty()
		@IsString()
		@IsOptional()
		derectorId: number;
		
		@IsNotEmpty()
		@ArrayNotEmpty()
		@IsNumber({}, {
				each: true,
		})
		@IsOptional()
		genreIds: number[];
}
```

</details>

<a id="27deda9b0fe18062942ee629fe421e09"></a>

```typescript
export class UpdateMoviceDto 
  extends PartialType(
		  CreateMoviceDto
	) {}
```

- <code>Optional</code>이 적용된 프로퍼티(필드)들을 생성

- 나머지 내용도 방식은 동일하므로 생략
