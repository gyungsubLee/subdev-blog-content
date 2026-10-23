---
order: 35
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 22eeda9b-0fe1-80e5-bf33-d8b1901445f0
title: 데이터 암호화 - bcrypt
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
    title: 탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )
  - id: 22eeda9b-0fe1-80e5-bf33-d8b1901445f0
    title: 데이터 암호화 - bcrypt
excerpt: 목차 - Hashing ( 데이터 암호화, 해싱 ) [Documentation | NestJS - A progressive Node.js framework]() Hashing ( 데이터 암호화, 해싱 ) 1. 패키지 설치 bash npm npm i bcrypt npm i -D @types/bcryp pnpm pnpm ad
cover: b177c3dbe712a575.webp
icon: null
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
created: 2025-07-12T08:45:30.370Z
updated: 2025-07-12T09:21:32.637Z
legacy_path: Main/Nest.js-c3a886768c4d/탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )-d4fc3e106054/데이터 암호화 - bcrypt-d8b1901445f0/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/22eeda9b0fe180e5bf33d8b1901445f0
---
> 
> 
> <a id="22eeda9b0fe18166bb35fcb8355c5cf7"></a>
> 
> <strong>목차</strong>
> 
> - [Hashing ( 데이터 암호화, 해싱 )](#22eeda9b0fe181cc9b18fd3512fe2327)

[Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()

<a id="22eeda9b0fe181cc9b18fd3512fe2327"></a>

### Hashing ( 데이터 암호화, 해싱 )

1. 패키지 설치

<a id="22eeda9b0fe180049e06f9bcb60eae19"></a>

```bash
# npm 
npm i bcrypt
npm i -D @types/bcryp

# pnpm
pnpm add bcrypt
pnpm add -D @types/bcrypt

# 설치 확인
pnpm list bcrypt
```

1. 암호화 ( 해시 처리 )

<a id="22eeda9b0fe18069839ee916cba5cfd1"></a>

```typescript

import * as bcrypt from 'bcrypt';

const saltOrRounds = 10;
const password = 'random_password';
const hash = await bcrypt.hash(password, saltOrRounds);
```

1. 비밀번호 와 해시 값 비교 ( 인증 시 사용 )

<a id="22eeda9b0fe18030a533ce64e53534b6"></a>

```typescript
const isMatch = await bcrypt.compare(password, hash);
```
