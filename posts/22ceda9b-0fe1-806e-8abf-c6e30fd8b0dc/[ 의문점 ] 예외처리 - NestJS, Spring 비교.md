---
order: 1
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 22ceda9b-0fe1-806e-8abf-c6e30fd8b0dc
title: "[ 의문점 ] 예외처리 - NestJS, Spring 비교"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
    title: 탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )
  - id: 22ceda9b-0fe1-806e-8abf-c6e30fd8b0dc
    title: "[ 의문점 ] 예외처리 - NestJS, Spring 비교"
excerpt: 목차 - Spring의 GlobalExceptionHandler와 비교 - NestJS vs Spring - 글로벌 예외 처리 비교 - 코드 예제 - 예제) NestJS의 Exception 처리 - 코드 - 실습 Spring의 GlobalExceptionHandler와 비교 --- ✏️ NestJS의 Exception L
cover: null
icon: 🧐
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
created: 2025-07-10T10:06:15.261Z
updated: 2026-01-31T03:39:02.043Z
legacy_path: Main/Nest.js-c3a886768c4d/탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )-d4fc3e106054/[ 의문점 ] 예외처리 - NestJS, Spring 비교-c6e30fd8b0dc/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/22ceda9b0fe1806e8abfc6e30fd8b0dc
---
> 
> 
> <a id="2f9eda9b0fe180c8a53de8d48a0973e1"></a>
> 
> <strong>목차</strong>
> 
> - [Spring의 GlobalExceptionHandler와 비교](#22ceda9b0fe1801fb155e78742e0dcb2)
> - [NestJS vs Spring - 글로벌 예외 처리 비교](#22ceda9b0fe18075b85ad5a6b0306ada)
> - [코드 예제](#22ceda9b0fe1800db993cc2653436441)
> - [예제) NestJS의 Exception 처리 ](#22ceda9b0fe180d89b2dc0a54c440afa)
> - [코드](#22ceda9b0fe18055b42fc549092677da)
> - [실습](#22ceda9b0fe180598525fe86988f4f69)

<a id="22ceda9b0fe1801fb155e78742e0dcb2"></a>

## Spring의 <code>GlobalExceptionHandler</code>와 비교

---

> ✏️ 
> 
> <a id="22ceda9b0fe180588440d5e2ade6d332"></a>
> 
> <strong><code>NestJS</code></strong>의 <code>Exception Layer &#43; Global Filter</code>와   <strong><code>Spring</code></strong>의 <code>&#64;ControllerAdvice &#43; &#64;ExceptionHandler</code>은 조합 및 개념적으로 거의 동일하다&#46;

<a id="22ceda9b0fe18075b85ad5a6b0306ada"></a>

### <strong><code>NestJS</code></strong><strong> vs </strong><strong><code>Spring</code></strong><strong> &#45; 글로벌 예외 처리 비교</strong>

| <strong>항목</strong> | <strong>NestJS</strong> | <strong>Spring</strong> |
| --- | --- | --- |
| 예외 처리 계층 이름 | Exception Layer &#43; Global Exception Filter | GlobalExceptionHandler (&#64;ControllerAdvice) |
| 필터 등록 방법 | app&#46;useGlobalFilters() | &#64;RestControllerAdvice 클래스 자동 등록 |
| 예외 클래스 계층 | HttpException, BadRequestException, 등 Nest 제공 클래스 사용 | ResponseStatusException,IllegalArgumentException, 커스텀 예외 등 |
| 커스텀 핸들러 작성 | &#64;Catch() &#43; ExceptionFilter 구현 | &#64;ExceptionHandler 메서드 |
| 기본 처리기 | BaseExceptionFilter | ResponseEntityExceptionHandler |
| 응답 형태 자동 변환 | JSON으로 자동 변환 | &#64;ResponseBody 사용 시 JSON으로 자동 변환 |

<a id="22ceda9b0fe1800db993cc2653436441"></a>

### <strong>코드 예제</strong>

<details>
<summary>Spring</summary>

<a id="22ceda9b0fe180e88c90fbbd1aca8c7c"></a>

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(UserNotFoundException.class)
    public ResponseEntity<?> handleUserNotFound(UserNotFoundException ex) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND)
                             .body(Map.of("message", ex.getMessage()));
    }
}
```

</details>

<details>
<summary>NestJS</summary>

<a id="22ceda9b0fe18008ab7be2c2a742b799"></a>

```typescript
@Catch(UserNotFoundException)
export class UserNotFoundFilter implements ExceptionFilter {
  catch(exception: UserNotFoundException, host: ArgumentsHost) {
    const ctx = host.switchToHttp();
    const res = ctx.getResponse();

    res.status(404).json({ message: exception.message });
  }
}
```

<a id="22ceda9b0fe180a18685cbf4536ed3d2"></a>

```java
app.useGlobalFilters(new UserNotFoundFilter());
```

</details>

> 🗒️ 
> 
> <a id="22ceda9b0fe18016900ef34994e82171"></a>
> 
> <strong>정리</strong>
> 
> <a id="22ceda9b0fe1802ea2d6d28a556860df"></a>
> 
> <strong>NestJS</strong>의 <code>Exception Layer</code>는 <strong>Spring의 </strong><strong><code>&#64;ControllerAdvice &#43; &#64;ExceptionHandler</code></strong><strong> 구조와 유사한 책임과 역할</strong>을 한다&#46;

<a id="22ceda9b0fe180d89b2dc0a54c440afa"></a>

## 예제) NestJS의 Exception 처리 

---

> /icons/target_gray.svg 
> 
> <a id="22ceda9b0fe18083a79cd1c7706c75c5"></a>
> 
> 구성요소
> 
> - <code>ErrorCode(enum</code>)&#58; 코드/메세지/상태코드 정의
> 
> - <code>BusinessException</code>&#58; 공통 비지니스 예외 클래스
> 
> - <code>GlobalExceptionFilter</code>&#58; 모든 예외를 catch 하여, statusCode, code, message, timestamp 형식으로 반환

<a id="22ceda9b0fe18055b42fc549092677da"></a>

### 코드

<a id="22ceda9b0fe18046b1a7cac7a8da1968"></a>

```java
src/
├── common/
│   ├── exceptions/
│   │   ├── error-code.enum.ts
│   │   ├── business.exception.ts
│   │   └── global-exception.filter.ts
```

<details>
<summary>&#91; 코드 &#93; <code>ErrorCode</code></summary>

<a id="22ceda9b0fe180ac8817d41e818944ac"></a>

```typescript
// error-code.enum.ts
import { HttpStatus } from '@nestjs/common';

export enum ErrorCode {
  USER_NOT_FOUND = 'USER_NOT_FOUND',
  INVALID_INPUT = 'INVALID_INPUT',
  INTERNAL_ERROR = 'INTERNAL_ERROR',
}

export const ErrorCodeMessageMap: Record<ErrorCode, { message: string; status: HttpStatus }> = {
  [ErrorCode.USER_NOT_FOUND]: {
    message: '사용자를 찾을 수 없습니다.',
    status: HttpStatus.NOT_FOUND,
  },
  [ErrorCode.INVALID_INPUT]: {
    message: '입력값이 잘못되었습니다.',
    status: HttpStatus.BAD_REQUEST,
  },
  [ErrorCode.INTERNAL_ERROR]: {
    message: '서버 내부 오류입니다.',
    status: HttpStatus.INTERNAL_SERVER_ERROR,
  },
};
```

</details>

<details>
<summary>&#91; 코드 &#93; <code>BusinessException</code></summary>

<a id="22ceda9b0fe180919018cd1b289c91a2"></a>

```typescript
// business.exception.ts
import { ErrorCode, ErrorCodeMessageMap } from './error-code.enum';

export class BusinessException extends Error {
  readonly code: ErrorCode;
  readonly status: number;

  constructor(code: ErrorCode) {
    super(ErrorCodeMessageMap[code].message);
    this.code = code;
    this.status = ErrorCodeMessageMap[code].status;
  }
}
```

</details>

<details>
<summary>&#91; 코드 &#93; <code>GlobalExceptionFilter</code></summary>

<a id="22ceda9b0fe180b9b6aacfed2fb81dd5"></a>

```typescript
// global-exception.filter.ts
import {
  ExceptionFilter,
  Catch,
  ArgumentsHost,
  HttpException,
  HttpStatus,
} from '@nestjs/common';
import { Response } from 'express';
import { BusinessException } from './business.exception';

@Catch()
export class GlobalExceptionFilter implements ExceptionFilter {
  catch(exception: unknown, host: ArgumentsHost) {
    const ctx = host.switchToHttp();
    const res = ctx.getResponse<Response>();

    let status = HttpStatus.INTERNAL_SERVER_ERROR;
    let message = 'Internal server error';
    let code = 'INTERNAL_ERROR';

    if (exception instanceof BusinessException) {
      status = exception.status;
      message = exception.message;
      code = exception.code;
    } else if (exception instanceof HttpException) {
      status = exception.getStatus();
      const resBody = exception.getResponse();
      message = typeof resBody === 'string' ? resBody : (resBody as any).message;
      code = 'HTTP_EXCEPTION';
    }

    res.status(status).json({
      timestamp: new Date().toISOString(),
      statusCode: status,
      code,
      message,
    });
  }
}
```

</details>

<details>
<summary>&#91; 코드 &#93; <code>main&#46;ts</code><strong> &#45; 필터 전역 등록</strong></summary>

<a id="22ceda9b0fe180cc9baefb7c94af2176"></a>

```typescript

// main.ts
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import { GlobalExceptionFilter } from './common/exceptions/global-exception.filter';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  app.useGlobalFilters(new GlobalExceptionFilter());

  await app.listen(3000);
}
bootstrap();
```

</details>

<a id="22ceda9b0fe180598525fe86988f4f69"></a>

### 실습

<details>
<summary><strong>사용 예시 </strong></summary>

<a id="22ceda9b0fe18017b3a9e4af34c78e16"></a>

```typescript
// {...}.controller.ts
@Get(':id')
getUser(@Param('id') id: string) {
  const user = this.userService.findUserById(id);
  if (!user) {
    throw new BusinessException(ErrorCode.USER_NOT_FOUND);
  }
  return user;
}
```

</details>

<details>
<summary><strong>결과 응답</strong></summary>

<a id="22ceda9b0fe180188493fea67fd0c67e"></a>

```typescript
{
  "timestamp": "2025-07-10T02:23:45.123Z",
  "statusCode": 404,
  "code": "USER_NOT_FOUND",
  "message": "사용자를 찾을 수 없습니다."
}
```

</details>
