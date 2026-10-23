---
order: 1
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 26feda9b-0fe1-81fa-b235-f193a6f6f03d
title: "[ 이론 ] RBAC"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 260eda9b-0fe1-801b-836b-c2e229a88ff9
    title: 한 번에 끝내는 NestJS 패키지 - Part 1. 기초
  - id: 26feda9b-0fe1-807a-9de4-e43c4e2f7faf
    title: RBAC ( Role Based Access Control )
  - id: 26feda9b-0fe1-81fa-b235-f193a6f6f03d
    title: "[ 이론 ] RBAC"
excerpt: "목차 - RBAC ( Role Based Access Control ) - 구현 방식 RBAC ( Role Based Access Control ) --- 📖 RBAC은 Role Based Access Control의 약자로, 역할(Role) 기반으로 권한(Permission)을 나눠서 특정 리소스 CRUD 작업 가능 "
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 26feda9b-0fe1-807a-9de4-e43c4e2f7faf
created: 2025-09-15T13:29:40.840Z
updated: 2025-09-18T17:06:10.708Z
legacy_path: Main/Nest.js-c3a886768c4d/한 번에 끝내는 NestJS 패키지 - Part 1. 기초-c2e229a88ff9/RBAC ( Role Based Access Control )-e43c4e2f7faf/[ 이론 ] RBAC-f193a6f6f03d/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/26feda9b0fe181fab235f193a6f6f03d
---
> 
> 
> <a id="26feda9b0fe181e7981bef89f51be31d"></a>
> 
> <strong>목차</strong>
> 
> - [RBAC ( Role Based Access Control )](#26feda9b0fe181819fa8dbe0b6c90a88)
> - [ 구현 방식](#26feda9b0fe181069501c4695fcb2110)

<a id="26feda9b0fe181819fa8dbe0b6c90a88"></a>

## RBAC ( Role Based Access Control )

---

> 📖 
> 
> <a id="26feda9b0fe18111ab0fe9354bb6531d"></a>
> 
> <code>RBAC</code>은 <code>Role Based Access Control</code>의 약자로,<strong><u> </u></strong><strong><u>역할(</u></strong><strong><u><code>Role</code></u></strong><strong><u>) 기반으로 권한(</u></strong><strong><u><code>Permission</code></u></strong><strong><u>)을 나눠</u></strong>서 <strong><u>특정 리소스 CRUD 작업 가능 여부를 판</u></strong>단한다&#46; 

> ❗ 
> 
> <a id="26feda9b0fe18127be71e0db3ae93804"></a>
> 
> RBAC을 복잡하게 설계하면 서비스의 복잡도가 비약적으로 높아져 버린다&#46; <br>웬만하면 간단하게 설계하는 것을 권장한다&#46; 

<a id="26feda9b0fe181069501c4695fcb2110"></a>

###  구현 방식

> ✏️ 
> 
> 1. 데코레이터 정의
> 
> 1. Enum 정의
> 
> 1. Guard 정의

![](2524a5264725c3c4.webp)

<details>
<summary>&#91; 코드 &#93;  Role ( <code>데코레이터</code> )</summary>

<a id="26feda9b0fe180d3af59f05993631bca"></a>

```typescript
import { Reflector } from '@nestjs/core';

export const Role = Reflector.createDecorator();
```

</details>

![](6f4f6dd25aa9d6cd.webp)

<details>
<summary>&#91; 코드 &#93;  Rolse ( <code>enum</code> )</summary>

<a id="26feda9b0fe18082910ad605f8c9619d"></a>

```typescript
export enum Roles {
  Admin = 'admin',
  User = 'user',
  Guest = 'guest',
}
```

</details>

![](94098bf21577ea3f.webp)

<details>
<summary>&#91; 코드 &#93;  RolesGuard</summary>

<a id="26feda9b0fe1808ca4f1f9954b73b074"></a>

```typescript
import { CanActivate, ExecutionContext } from '@nestjs/common';
import { Reflector } from '@nestjs/core';
import { Observable } from 'rxjs';
import { Role } from '../decorator/role.decorator';

export enum Roles {
  Admin = 'admin',
  User = 'user',
  Guest = 'guest',
}

export class RolesGuard implements CanActivate {
  constructor(private readonly reflector: Reflector) {}

  canActivate(
    context: ExecutionContext,
  ): boolean | Promise<boolean> | Observable<boolean> {
    const roles = this.reflector.get<Roles[]>(Role, context.getHandler());
    if (!roles) {
      return true;
    }

    const request = context.switchToHttp().getRequest();
    const user = request.user;
    return roles.some((role) => user.roles?.includes(role));
  }
}
```

</details>
