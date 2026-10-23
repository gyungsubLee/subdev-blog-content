---
order: 39
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 22ceda9b-0fe1-808d-aca9-f0c4915b0314
title: Pipes - 유효성 검사, 파싱 [ 정리 중 ]
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
    title: 탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )
  - id: 22ceda9b-0fe1-808d-aca9-f0c4915b0314
    title: Pipes - 유효성 검사, 파싱 [ 정리 중 ]
excerpt: 목차 - Pipes - 기본 제공되는 파이프 ( Built-in Pipe ) - 종류 및 설명 - 예시 - 사용자 정의 파이프 ( Custom Pipe ) - 기본 구조 - 예시 - PipeTransform.transform(value, metadata) - 예시 - Pipes 및 Filters 패턴 Pipes --- [
cover: fb3b1ee7da4a15e0.webp
icon: 9bed2eae1e079b4b.avif
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
created: 2025-07-10T07:09:19.229Z
updated: 2025-07-11T07:19:16.887Z
legacy_path: Main/Nest.js-c3a886768c4d/탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )-d4fc3e106054/Pipes - 유효성 검사, 파싱 [ 정리 중 ]-f0c4915b0314/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/22ceda9b0fe1808daca9f0c4915b0314
---
> 
> 
> <a id="22ceda9b0fe1819c9b2be5e840940ca7"></a>
> 
> <strong>목차</strong>
> 
> - [Pipes](#22ceda9b0fe18066ab93e8e464db5990)
> - [기본 제공되는 파이프 ( Built-in Pipe )](#22deda9b0fe180d78104e9ae47cc885b)
> - [종류 및 설명 ](#22deda9b0fe18088896deb144070605d)
> - [예시](#22deda9b0fe180feaafec66d5596aded)
> - [사용자 정의 파이프 ( Custom Pipe )](#22deda9b0fe18029a0a1d8d1a8458166)
> - [기본 구조](#22deda9b0fe180aca673c5d44d9fbe34)
> - [예시 ](#22deda9b0fe180d18f60c38543c7dd6e)
> - [PipeTransform.transform(value, metadata)](#22deda9b0fe18003a8efd8c02fcb03f3)
> - [예시](#22deda9b0fe180909c70e5c5aed25b1d)
> - [Pipes 및 Filters 패턴](#22ceda9b0fe18054a846ce5f22c0d481)

<a id="22ceda9b0fe18066ab93e8e464db5990"></a>

## Pipes

---

[Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()

> 📖 
> 
> <a id="22deda9b0fe18098af1ed051781b9149"></a>
> 
> NestJS에서 제공하는 <strong><code>파이프(Pipes)</code></strong>는 주로 <strong><u>유효성 검사(validation)</u></strong>와 <strong><u>타입 변환(transformation)</u></strong>을 담당하며 <code>&#64;Body()</code>, <code>&#64;Param()</code>, <code>&#64;Query()</code> 등과 함께 사용된다&#46;
> 
> - Pipe는 <code>PipeTransform</code> 인터페이스를 구현하는 <code>&#64;Injectable()</code>  데코레이터가 붙은 클래스이다&#46;

> ✏️ 
> 
> <a id="22deda9b0fe1801b9918e862bfc6d068"></a>
> 
> 두 경우(검증, 변환) 모두, 컨트롤러 라우트 핸들러가 처리하는 <code>arguments</code>에 대해 작동된다&#46;
> 
> <a id="22deda9b0fe180e197d2eb894116a4ec"></a>
> 
> Nest는 메서드가 호출되기 직전에 파이프를 삽입하고, 파이프는 해당 메서드로 전달되는 인수를 받아 처리한다&#46;
> 
> <a id="22deda9b0fe1800fa42ffc3dd3b65fd9"></a>
> 
> 모든 변환 또는 유효성 검사 작업은 이 시점에 수행되며, 그 후 라우트 핸들러는 (잠재적으로) 변환된 인수와 함께 호출된다&#46;

> 💬 
> 
> <a id="22deda9b0fe18009b8f2f8b320c9aaf7"></a>
> 
> 파이프는 <code>exception zone</code> 내에서 실행된다&#46; <br>즉, 파이프에서 예외가 발생되면 예외 필터에서 처리가 가능하다&#46; 

<a id="22deda9b0fe180d78104e9ae47cc885b"></a>

### 기본 제공되는 파이프 ( Built&#45;in Pipe )

> ✏️ 
> 
> <a id="22deda9b0fe18067a8cef2139b71792e"></a>
> 
> Nest에서는 아래와 같이 기본 내장 파이프 클래스를 지원한다&#46; 

<a id="22deda9b0fe18088896deb144070605d"></a>

### 종류 및 설명 

| <strong>파이프 이름</strong> | <strong>주요 역할</strong> | <strong>주요 사용 위치</strong> | <strong>실패 시 동작</strong> | <strong>주요 옵션/특이사항</strong> |
| --- | --- | --- | --- | --- |
| <strong><code>ValidationPipe</code></strong> | DTO에 정의된 class&#45;validator 데코레이터를 기반으로 <strong>전체 유효성 검증</strong> 수행 | &#64;Body(), &#64;Query(), &#64;Param() 등 | 유효성 실패 시 400 Bad Request | transform, whitelist, forbidNonWhitelisted, skipMissingProperties |
| <strong><code>ParseIntPipe</code></strong> | 문자열을 정수 number로 파싱 | &#64;Param(), &#64;Query() | 숫자 변환 실패 시 400 | { exceptionFactory }로 커스터마이징 가능 |
| <strong><code>ParseFloatPipe</code></strong> | 문자열을 부동소수점 number로 파싱 | &#64;Query(), &#64;Body() | 숫자 변환 실패 시 400 | 거의 사용 예시 없음 |
| <strong><code>ParseBoolPipe</code></strong> | &#39;true&#39;, &#39;false&#39; 문자열을 boolean으로 파싱 | &#64;Query() 등 | 변환 실패 시 400 | &#39;true&#39;, &#39;false&#39;만 허용됨 |
| <strong><code>ParseArrayPipe</code></strong> | 문자열 또는 JSON 배열을 배열로 파싱 | &#64;Query(), &#64;Body() | 형식이 맞지 않으면 400 | { items, separator, optional } 옵션 제공 |
| <strong><code>ParseUUIDPipe</code></strong> | 문자열이 UUID 형식인지 확인 | &#64;Param(), &#64;Query() | UUID 포맷이 아니면 400 |  |
| <strong><code>ParseEnumPipe</code></strong> | 문자열이 enum 값인지 확인 | &#64;Param(), &#64;Query() | enum 값 미포함 시 400 | enum, { errorHttpStatusCode } |
| <strong><code>DefaultValuePipe</code></strong> | 값이 undefined인 경우 기본값으로 대체 | 주로 &#64;Query() | 해당 없음 (실패 아님) | 다른 Pipe와 조합 필요 (ex&#46; &#43; ParseIntPipe) |
| <strong><code>ParseFilePipe</code></strong> | 업로드된 파일의 유효성 검증 | &#64;UploadedFile(), &#64;UploadedFiles() | 조건 미달 시 400 | MaxFileSizeValidator, FileTypeValidator 등 조합 |
| <strong><code>ParseDatePipe</code></strong> | 문자열을 Date 객체로 파싱 | &#64;Query(), &#64;Param( |  |  |

<a id="22deda9b0fe180feaafec66d5596aded"></a>

### 예시

<details>
<summary>ex 1) Path Variable / Int 변환(<code>ParseIntPipe</code>)  &#45;   클래스 전달 (의존성 주입)</summary>

- <strong>route handler &#45; </strong><strong><code>&#64;Param</code></strong><strong>&#58;  int 타입 변환</strong>
    <a id="22deda9b0fe1800db52ce21f38c03313"></a>

    ```typescript

    @Get(':id')
    async findOne(@Param('id', ParseIntPipe) id: number) {
      return this.catsService.findOne(id);
    }
    ```

- <strong>요청</strong>
    <a id="22deda9b0fe180deaa5fe2ad61301996"></a>

    ```typescript
    GET localhost:3000/abc
    ```

- <strong>응답 &#45; </strong><strong><code>400</code></strong><strong>&#58; 파싱 오류 발생</strong>
    <a id="22deda9b0fe1802eae36dcbf1b59a242"></a>

    ```typescript
    {
      "statusCode": 400,
      "message": "Validation failed (numeric string is expected)",
      "error": "Bad Request"
    }
    ```

</details>

<details>
<summary>ex 2) Path Variable / Int 변환( <code>ParseIntPipe</code> ) &#45; 인스턴스 전달, Http StatusCode 지정</summary>

- <strong>route handler &#45; </strong><strong><code>&#64;Param</code></strong><strong>&#58;  int 타입 변환</strong>
    <a id="22deda9b0fe180dc9d19e5d08d4e4aa2"></a>

    ```typescript
    @Get(':id')
    async findOne(
      @Param('id', new ParseIntPipe({ errorHttpStatusCode: HttpStatus.NOT_ACCEPTABLE }))
      id: number,
    ) {
      return this.catsService.findOne(id);
    }

    ```

</details>

<details>
<summary>ex 3) Query Parameter / Int 변환( <code>ParseIntPipe</code> ) &#45; 클래스 전달 (의존성 주입)</summary>

- <strong>route handler &#45; </strong><strong><code>&#64;Param</code></strong><strong>&#58;  int 타입 변환</strong>
    <a id="22deda9b0fe180cc852ed5cc3dcbdae0"></a>

    ```typescript

    @Get()
    async findOne(@Query('id', ParseIntPipe) id: number) {
      return this.catsService.findOne(id);
    }

    ```

</details>

<details>
<summary>ex 4) Path Variable / UUID 변환( <code>ParseUUIDPipe</code> ) &#45; 인스턴스 전달</summary>

- <strong>route handler &#45; </strong><strong><code>&#64;Param</code></strong><strong>&#58;  int 타입 변환</strong>
    <a id="22deda9b0fe1807394d8de41fe28026e"></a>

    ```typescript

    @Get(':uuid')
    async findOne(@Param('uuid', new ParseUUIDPipe()) uuid: string) {
      return this.catsService.findOne(uuid);
    }
    ```

</details>

<a id="22deda9b0fe18029a0a1d8d1a8458166"></a>

### 사용자 정의 파이프 ( Custom Pipe )

> ✏️ 
> 
> <a id="22deda9b0fe180fb9866dc9b5f092f2c"></a>
> 
> Nest의 기본 파이프(ex&#46; <code>ParseIntPipe</code>, <code>ValidationPipe</code>)로는 <strong><u>복잡한 검증이나 비즈니스 검사가 어렵</u></strong>다&#46;
> 
> <a id="22deda9b0fe18001aff4ebcd705eaa75"></a>
> 
> 이를 해결하기 위해, Nest에서는 <strong><code>Custom Pipe(사용자 정의 파이프)</code></strong>를 지원한다&#46; 
> 
> - <code>PipeTransform</code> 인터페이스 구현, <code>transform()</code> 메서드 내부에 변환 및 검증 로직 작성
> 
> - <code>&#64;Injectable()</code>을 명시하여 의존성 주입 처리

<a id="22deda9b0fe180aca673c5d44d9fbe34"></a>

### <strong>기본 구조</strong>

<a id="22deda9b0fe18067a7a5d4722ca17eab"></a>

```typescript
import { PipeTransform, Injectable, ArgumentMetadata } from '@nestjs/common';

@Injectable()
export class CustomPipe implements PipeTransform {
  transform(value: any, metadata: ArgumentMetadata): any {
    // value: 요청 데이터 (예: 파라미터, 쿼리, 바디)
    // metadata: 타입 정보, 키, 위치 등 메타데이터
    return value;
  }
}
```

<a id="22deda9b0fe180d18f60c38543c7dd6e"></a>

### 예시 

<details>
<summary>ex 1)<strong> 문자열을 정수로 변환 &#43; 숫자 검증</strong></summary>

<a id="22deda9b0fe18092927ae231ee0dff7a"></a>

<strong>커스텀 필터</strong>

<a id="22deda9b0fe180b9a60fcfbb46333578"></a>

```typescript
@Injectable()
export class ParsePositiveIntPipe implements PipeTransform {
	
	// 수자 타입 변환 + 값 유효성 검사
  transform(value: any, metadata: ArgumentMetadata): number {
    const val = parseInt(value, 10);
    if (isNaN(val) || val <= 0) {
      throw new BadRequestException(`${metadata.data} must be a positive integer`);
    }
    return val;
  }
}
```

<a id="22deda9b0fe180829329f4f11bca56f9"></a>

<strong>사용</strong>

<a id="22deda9b0fe1803497b8c570956986a2"></a>

```typescript
@Get(':id')
getById(@Param('id', ParsePositiveIntPipe) id: number) {
  return id;
}
```

</details>

<details>
<summary>ex 2)<strong> 유저 ID 존재 여부 검증 (DI 필요)</strong></summary>

<a id="22deda9b0fe1804e85ecef0cc6aedc79"></a>

<strong>커스텀 필터</strong>

<a id="22deda9b0fe180cfb308ff7f9d43fa4f"></a>

```typescript
@Injectable()
export class UserExistsPipe implements PipeTransform {
	// 의존성 주입
  constructor(private readonly userService: UserService) {}
	
	// 유저 id 유효성 검사
  async transform(value: string) {
    const user = await this.userService.findById(value);
    if (!user) {
      throw new BadRequestException('User does not exist');
    }
    return user; // 또는 ID만 리턴할 수도 있음
  }
}
```

</details>

<a id="22deda9b0fe18003a8efd8c02fcb03f3"></a>

### <code>PipeTransform&#46;transform(value, metadata)</code>

> ✏️ 
> 
> <a id="22deda9b0fe180368086e1f2ef8deb73"></a>
> 
> <code>PipeTransform</code> 인터페이스의 스펙으로 정의된 <code>transform()</code>메서드는 아래 2개의 인자를 받는다&#46; 
> 
> - <code>value</code>
> 
> - <code>metadata</code>

1. <strong><code>value</code></strong>
    <a id="22deda9b0fe180c4a545d7bcfb7cb40f"></a>

    <strong><code>value</code></strong> 파라미터는 현재 처리 중인 인자를 의미한다&#46; ( route handler에서 수신되기 전 )

1. <strong><code>metadata</code></strong>
    <a id="22deda9b0fe180248a68d0e05d54ca93"></a>

    <strong><code>metadata</code></strong>는 현재 처리 중인 인자의 메타데이터이다&#46; 

    <a id="22deda9b0fe180c0a61af2adc6020a7f"></a>

    ```typescript

    export interface ArgumentMetadata {
      type: 'body' | 'query' | 'param' | 'custom';
      metatype?: Type<unknown>;
      data?: string;
    }
    ```

    | ArgumentMetadata(속성 이름<strong>)</strong> | <strong>설명</strong> | <strong>예시</strong> | <strong>값이 없는 경우</strong> |
    | --- | --- | --- | --- |
    | <code>type</code> | 파라미터의 위치를 나타냄 | <code>&#39;body&#39;</code>, <code>&#39;query&#39;</code>, <code>&#39;param&#39;</code>, <code>&#39;custom</code>&#39; | 없음 – 항상 설정됨 |
    | <code>metatype</code> | 파라미터의 타입 정보 <br>(클래스, 기본 타입 등) | <code>String</code>, <code>Number</code>, <code>CreateUserDto</code>, <code>Boolean</code> | 타입 명시가 없으면 undefined |
    | <code>data</code> | 데코레이터에 전달된 키 이름<br>(<code>&#64;Param(&#39;id&#39;)</code>의 <code>id</code>) | <code>&#39;id&#39;</code>, <code>&#39;username&#39;</code>, <code>&#39;limit&#39;</code> 등 | 데코레이터 괄호가 비어 있으면 undefined |

<a id="22deda9b0fe180909c70e5c5aed25b1d"></a>

### 예시

<details>
<summary><strong>ex1 ) </strong></summary>

<a id="22deda9b0fe180ac9517e6b129faf017"></a>

```typescript
@Get(':id')
getUser(@Param('id') id: number) {}
```

- <code>type</code>&#58; param

- <code>metatype</code>&#58; Number

- <code>data</code>&#58; id

<a id="22deda9b0fe180a9a9d2c759128ea63f"></a>

  

</details>

<details>
<summary><strong>ex2 )</strong></summary>

<a id="22deda9b0fe180fc98cfd0db83948090"></a>

```typescript
@Post()
createUser(@Body() dto: CreateUserDto) {}
```

- <code>type</code>&#58; body

- <code>metatype</code>&#58; Create

- <code>data</code>&#58; undefined

<a id="22deda9b0fe1803c947ac0178e2e6176"></a>

  

</details>

<details>
<summary><strong>ex3 ) </strong></summary>

<a id="22deda9b0fe1803cb7eef4e79f7e08e6"></a>

```typescript
@Get()
search(@Query('q') query: string) {}
```

- <code>type</code>&#58; query

- <code>metatype</code>&#58; String

- <code>data</code>&#58; q

<a id="22deda9b0fe1806caaacfef289c5853f"></a>

  

</details>

> ☝🏻 
> 
> <a id="22deda9b0fe180d78a07fbc85da3b0b3"></a>
> 
> 파이프 체이닝은 필드 단위로만 동작이 가능하다&#46; <br>따라서 복잡한 요구사항을 DTO 단위로 적용하고 싶다면 Custom Pipe를 사용해야한다&#46;

<a id="22ceda9b0fe18054a846ce5f22c0d481"></a>

## <strong>Pipes 및 Filters 패턴</strong>

[Pipes and Filters pattern &#45; Azure Architecture Center]()
