---
order: 1
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 26eeda9b-0fe1-8072-83bc-d3258aeaba03
title: "커스텀 데코레이터 생성: Reflector.createDecorator()"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 260eda9b-0fe1-801b-836b-c2e229a88ff9
    title: 한 번에 끝내는 NestJS 패키지 - Part 1. 기초
  - id: 26eeda9b-0fe1-8072-83bc-d3258aeaba03
    title: "커스텀 데코레이터 생성: Reflector.createDecorator()"
excerpt: 📖 Reflector.createDecorator()는 NestJS에서 커스텀 데코레이터를 간편하게 만드는 메서드로, 특정 타입의 매개변수를 받아 라우트 핸들러 등에 메타데이터 형태로 값을 저장할 수 있게 한다. ✏️ 동작 과정 - Reflector.createDecorator()는 typescript generic 타
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 260eda9b-0fe1-801b-836b-c2e229a88ff9
created: 2025-09-14T11:55:57.583Z
updated: 2025-10-31T23:57:51.066Z
legacy_path: Main/Nest.js-c3a886768c4d/한 번에 끝내는 NestJS 패키지 - Part 1. 기초-c2e229a88ff9/커스텀 데코레이터 생성- Reflector.createDecorator()-d3258aeaba03/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/26eeda9b0fe1807283bcd3258aeaba03
---
> 📖 
> 
> <a id="26eeda9b0fe180dbae59cd824f62e11e"></a>
> 
> <code>Reflector&#46;createDecorator()</code>는 NestJS에서 커스텀 데코레이터를 간편하게 만드는 메서드로, 특정 타입의 매개변수를 받아 라우트 핸들러 등에 메타데이터 형태로 값을 저장할 수 있게 한다&#46; 

> ✏️ 
> 
> <a id="26eeda9b0fe1802b8d57c9fe7de3d406"></a>
> 
> 동작 과정
> 
> - <code>Reflector&#46;createDecorator()</code>는 typescript generic 타입을 받으며, 데코레이터 함수를 생성한다&#46; 
> 
> - 이렇게 만든 데코레이터는 라우트 핸들러(컨트롤러 메서드)에 붙여 해당 값(ex&#46; 역할 리스트, 권한 등)을 메타데이터로 저장한다&#46; 
> 
> - <strong><code>런타임</code></strong><strong> 시 </strong><strong><u>Reflector 인스턴스</u></strong><strong>를 통해 </strong><strong><u>해당 핸들러의 메타데이터를 접근</u></strong>하여 검사하거나, 인증/인가 등 다양한 용도로 활용
> 

<details>
<summary>코드 예시</summary>

<a id="26eeda9b0fe180e9aa28fc30f949380c"></a>

```typescript
// roles.decorator.ts
import { Reflector } from '@nestjs/core';

// string[] 타입을 받는 커스텀 Roles 데코레이터 생성
export const Roles = Reflector.createDecorator<string[]>();
```

<a id="26eeda9b0fe180a19316ce873da9ea55"></a>

```typescript
// auth.controller.ts
@Post()
@Roles(['admin'])
async create(@Body() dto: CreateCatDto) { ... }
```

</details>

> 🧐 
> 
> <a id="26eeda9b0fe180728c6de9abeb694c13"></a>
> 
> <code>&#64;SetMetadata()</code> 와 비교
> 
> - <code>&#64;SetMetadata(’roles’, ‘admin’)</code> 위 예시 코드와 동일 목적으로 메타데이터를 첨부하지만, <code>createDecorator()</code> 방식이 더 타입 안전과 재사용성을 높이는 권장 방법이다&#46; 
> 
> - <code>Reflector&#46;createDecorator</code> 방식은<strong><u> 직접적인 데코레이터 함수를 만</u></strong>들어 코드 일관성이 높고, NestJS 9&#46;x 이후에서 공식적으로 지원되는 패턴  이다&#46;
