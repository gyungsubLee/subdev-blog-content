---
order: 36
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 22beda9b-0fe1-80a9-aeaa-eb1f12cff2e4
title: NestJs의 예외 처리 - Exception Filter
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
    title: 탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )
  - id: 22beda9b-0fe1-80a9-aeaa-eb1f12cff2e4
    title: NestJs의 예외 처리 - Exception Filter
excerpt: "목차 - 1. 기본 예외 클래스: HttpException - 2. 기본 내장 HTTP Exception - 3. 커스텀 Exception - 4. Exception Filter - Filter 정의 - 필터 바인딩 - 5. Spring과 비교 보류 [Documentation | NestJS - A progressive "
cover: fb3b1ee7da4a15e0.webp
icon: 9bed2eae1e079b4b.avif
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
created: 2025-07-09T11:15:14.102Z
updated: 2025-07-12T07:43:00.799Z
legacy_path: Main/Nest.js-c3a886768c4d/탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )-d4fc3e106054/NestJs의 예외 처리 - Exception Filter-eb1f12cff2e4/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/22beda9b0fe180a9aeaaeb1f12cff2e4
---
> 
> 
> <a id="22beda9b0fe18047886ccd818aeedf01"></a>
> 
> <strong>목차</strong>
> 
> - [1. 기본 예외 클래스: HttpException](#22ceda9b0fe180c6bee2e81a2766ebc3)
> - [2. 기본 내장 HTTP Exception](#22ceda9b0fe180b8a637e458b235006e)
> - [3. 커스텀 Exception](#22ceda9b0fe180d8ba43c351f97a3e2b)
> - [4. Exception Filter](#22ceda9b0fe180f8946ac0f81f582939)
> - [Filter 정의](#22eeda9b0fe180468a0bd1a08313b258)
> - [필터 바인딩](#22deda9b0fe1804385bfe4d79f7a8c04)
> - [5. Spring과 비교](#22ceda9b0fe180e1a774d104dd2305b7)

[보류](#/post/22ceda9b-0fe1-8006-845f-f1357b4c2ae5)

[Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()

> 📖 
> 
> <a id="22ceda9b0fe180ac86e0ca1bbc879638"></a>
> 
> NestJS는 구조적인 서버 사이드 프레임워크로, <strong>예외 처리(Exception Handling)</strong> 또한 강력한 기능을 제공한다&#46;
> 
> - Spring의 <code>&#64;ControllerAdvice</code>, <code>&#64;ExceptionHandler</code>, <code>ResponseStatusException</code>, <code>Custom Exception</code>과 유사하게 구성된다&#46;

<a id="22ceda9b0fe180c6bee2e81a2766ebc3"></a>

### 1&#46; 기본 예외 클래스&#58; <code>HttpException</code>

> ✏️ 
> 
> <a id="22ceda9b0fe1809ca3eef3e58cb155c1"></a>
> 
> NestJS의 모든 예외는 <code>HttpException</code>을 기반으로 동작한다&#46;

- 예제
    <a id="22ceda9b0fe1804babfefc5a4c43faa1"></a>

    ```typescript
    import { HttpException, HttpStatus } from '@nestjs/common';

    throw new HttpException('Forbidden', HttpStatus.FORBIDDEN);
    ```

- 생성자 시그니처
    <details>
    <summary>&#91; 전체코드 &#93;</summary>

    <a id="22deda9b0fe18098817ac67c952c4778"></a>

    ```typescript
    import { HttpExceptionBody, HttpExceptionBodyMessage } from '../interfaces/http/http-exception-body.interface';
    import { IntrinsicException } from './intrinsic.exception';
    export interface HttpExceptionOptions {
        /** original cause of the error */
        cause?: unknown;
        description?: string;
    }
    export interface DescriptionAndOptions {
        description?: string;
        httpExceptionOptions?: HttpExceptionOptions;
    }

    export declare class HttpException extends IntrinsicException {
        private readonly response;
        private readonly status;
        private readonly options?;
       
        cause: unknown;
        
        constructor(response: string | Record<string, any>, status: number, options?: HttpExceptionOptions | undefined);
        
        initCause(): void;
        initMessage(): void;
        initName(): void;
        getResponse(): string | object;
        getStatus(): number;
        static createBody(nil: null | '', message: HttpExceptionBodyMessage, statusCode: number): HttpExceptionBody;
        static createBody(message: HttpExceptionBodyMessage, error: string, statusCode: number): HttpExceptionBody;
        static createBody<Body extends Record<string, unknown>>(custom: Body): Body;
        static getDescriptionFrom(descriptionOrOptions: string | HttpExceptionOptions): string;
        static getHttpExceptionOptionsFrom(descriptionOrOptions: string | HttpExceptionOptions): HttpExceptionOptions;
        
        static extractDescriptionAndOptionsFrom(descriptionOrOptions: string | HttpExceptionOptions): DescriptionAndOptions;
    }
    ```

    </details>

    <a id="22ceda9b0fe180bb9c96f01a357243e2"></a>

    ```typescript
    new HttpException(response: string | object, status: HttpStatus)
    ```

    - <code>response</code>&#58; 문자열(메시지) or 객체(상세 오류)

    - <code>status</code>&#58; HTTP 상태 코드 ( ex&#46; <code>HttpStatus&#46;BAD&#95;REQUEST</code> )

<a id="22ceda9b0fe180b8a637e458b235006e"></a>

### 2&#46; 기본 내장 HTTP Exception

[Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()

> ✏️ 
> 
> <a id="22ceda9b0fe1801e8ea7f56dada31335"></a>
> 
> NestJS는 자주 사용하는 HTTP 오류 상황을 위한 기본 예외 클래스를 제공한다&#46; ( 모두 <code>HttpException</code>을 상속한다&#46; )

- <strong>핵심 Exception</strong>
    | 예외 클래스 | 상태 코드 | 설명 |
    | --- | --- | --- |
    | <code>BadRequestException</code> | 400 | 잘못된 요청 |
    | <code>UnauthorizedException</code> | 401 | 인증 실패 |
    | <code>ForbiddenException</code> | 403 | 권한 없음 |
    | <code>NotFoundException</code> | 404 | 리소스 없음 |
    | <code>ConflictException</code> | 409 | 리소스 충돌 |
    | <code>InternalServerErrorException</code> | 500 | 서버 오류 |

<details>
<summary>ex) 사용 예시</summary>

<a id="22ceda9b0fe180b088caf19c99fcec02"></a>

기본 내장 HTTP Exception &#45; NotFoundException

<a id="22ceda9b0fe180e2a2a8fa6beb207314"></a>

```typescript
import { NotFoundException } from '@nestjs/common';

throw new NotFoundException('해당 유저를 찾을 수 없습니다');
```

<a id="22ceda9b0fe180fdb251f5f157117815"></a>

응답 예시

<a id="22ceda9b0fe1808091e9ed28eab2d825"></a>

```typescript
{
  "statusCode": 404,
  "message": "해당 유저를 찾을 수 없습니다",
  "error": "Not Found"
}
```

</details>

<a id="22ceda9b0fe180d8ba43c351f97a3e2b"></a>

### 3&#46; 커스텀 Exception

> ✏️ 
> 
> <a id="22ceda9b0fe1803c918bc78799c59904"></a>
> 
> 도메인 로직에 맞는 예외 처리를 위해 <code>HttpException</code>을 상속하여 사용자 정의 예외 클래스를 만들 수 있다&#46;

<a id="22ceda9b0fe180c7b725e2fc3a757303"></a>

```typescript
// 예제: 유저 리소스 없음 
import { HttpException, HttpStatus } from '@nestjs/common';

export class UserNotFoundException extends HttpException {
  constructor(userId: string) {
    super(`User with ID ${userId} not found`, HttpStatus.NOT_FOUND);
  }
}
```

<a id="22ceda9b0fe1806e9e67cbc9d5e150db"></a>

```typescript
// 사용
throw new UserNotFoundException('1234');
```

<a id="22ceda9b0fe180f8946ac0f81f582939"></a>

### 4&#46; Exception Filter

> ✏️ 
> 
> <a id="22ceda9b0fe180a58379f011fc479aa4"></a>
> 
> NestJS는 예외가 발생하면 자동으로 Exception Filter를 통해 응답을 처리한다&#46;
> 
> - 사용자 정의 예외 처리나, 공통 에러 포맷, 로그 기록, 메시지 변환 등에 사용

<a id="22eeda9b0fe180468a0bd1a08313b258"></a>

### Filter 정의

<a id="22ceda9b0fe1808b8582c21fe19e191a"></a>

<strong>1&#46; Exception Filter 기본 구조 정의</strong>

> 💬 
> 
> - 모든 예외 필터는 <code>ExceptionFilter&#60;T&#62;</code> 인터페이스를 구현해야한다&#46; 
>     - <code>catch(exception&#58; T, host&#58; ArgumentsHost)</code>오버라이드
> 
> - <code>&#64;Catch()</code> 데코레이터에 Exception의 scope 지정 가능
>     - 지정하지 않으면 모든 unhandled exception을 catch 한다&#46;

<a id="22ceda9b0fe180e09f1fcd7256da04a2"></a>

```typescript
import {
  ExceptionFilter,
  Catch,
  ArgumentsHost,
  HttpException,
} from '@nestjs/common';
import { Request, Response } from 'express';

@Catch(HttpException)
export class HttpErrorFilter implements ExceptionFilter {
  catch(exception: HttpException, host: ArgumentsHost) {
    const ctx = host.switchToHttp();
    const response = ctx.getResponse<Response>();
    const request = ctx.getRequest<Request>();
    const status = exception.getStatus();
    const errorResponse = exception.getResponse();

    response.status(status).json({
      success: false,
      path: request.url,
      timestamp: new Date().toISOString(),
      ...(typeof errorResponse === 'string'
        ? { message: errorResponse }
        : errorResponse),
    });
  }
}
```

<a id="22deda9b0fe1804385bfe4d79f7a8c04"></a>

### 필터 바인딩

<a id="22ceda9b0fe180458c13e7bae6fe661f"></a>

<strong>2&#46; 부분적으로 필터 적용 &#45; </strong><strong><code>&#64;UserFilters(&#46;&#46;&#46;)</code></strong>

> 💬 
> 
> <a id="22deda9b0fe18084ac77e153f76e8a5b"></a>
> 
> 가능하면 인스턴스 대신 <strong><u>클래스를 사용(의존성 주입)</u></strong>하여 필터를 적용하는 것이 좋다&#46;
> 
> <a id="22deda9b0fe180c4b36ed0511e815c60"></a>
> 
> Nest가 전체 모듈에서 <strong><u>동일한 클래스의 인스턴스를 쉽게 재사용</u></strong>할 수 있으므로 <strong><u>메모리 사용량이 줄어든다&#46;</u></strong>

<a id="22deda9b0fe18025852ce2349dc8b2b0"></a>

```typescript
import { UseFilters } from '@@nestjs/common';

// 1. 인스턴스 전달 인스턴스 직접 생성
@Post()
@UseFilters(new HttpExceptionFilter())
async create(@Body() createCatDto: CreateCatDto) {
  throw new ForbiddenException();
}

// 2. 클래스 전달 - 의존성 주입 
@Post()
@UseFilters(HttpExceptionFilter)
async create(@Body() createCatDto: CreateCatDto) {
  throw new ForbiddenException();
}
```

<a id="22ceda9b0fe180acb8eaddb0eb8400c4"></a>

3&#46; <strong>전역 범위로 필터 적용 &#45; </strong><strong><code>app&#46;useGlobalFilters(&#46;&#46;&#46;)</code></strong>

<a id="22ceda9b0fe1809097dcc966082e1200"></a>

```typescript
// main.ts
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import { HttpErrorFilter } from './common/filters/http-error.filter';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  app.useGlobalFilters(new HttpErrorFilter());
  await app.listen(3000);
}
bootstrap();
```

<a id="22ceda9b0fe180e1a774d104dd2305b7"></a>

### 5&#46; Spring과 비교

| 항목 | Spring | NestJS |
| --- | --- | --- |
| 기본 예외 클래스 | <code>ResponseStatusException</code> | <code>HttpException</code> |
| 내장 예외 | <code>BadRequestException</code> 등 | <code>BadRequestException</code> 등 |
| 커스텀 예외 | <code>&#64;ResponseStatus</code> &#43; <code>RuntimeException</code> | <code>extends HttpException</code> |
| 예외 처리기 | <code>&#64;ControllerAdvice</code> &#43;<code> &#64;ExceptionHandler</code> | <code>&#64;Catch</code> &#43; <code>ExceptionFilter</code> |
| 전역 등록 방식 | <code>Bean</code> 등록 | <code>useGlobalFilters()</code> |
