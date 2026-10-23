---
order: 30
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 230eda9b-0fe1-8081-9f0b-fd00744b10ff
title: "[ 실습 ] 인증 ( 로그인 API, Guard )"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
    title: 탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )
  - id: 230eda9b-0fe1-8081-9f0b-fd00744b10ff
    title: "[ 실습 ] 인증 ( 로그인 API, Guard )"
excerpt: 목차 - 1. 기본 세팅 - 3. Guard를 통한 인가 처리 - Reference 1. 기본 세팅 1. auth 모듈, 서비스 생성 bash nest g module auth nest g service auth 1. JWT 패키지 설치 bash pnpm add --save @nestjs/jwt 3. Guard를 통한 인
cover: 56e5888dccc92997.webp
icon: 382f05f3a103d06c.webp
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
created: 2025-07-14T12:19:46.437Z
updated: 2025-07-15T02:57:26.876Z
legacy_path: Main/Nest.js-c3a886768c4d/탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )-d4fc3e106054/[ 실습 ] 인증 ( 로그인 API, Guard )-fd00744b10ff/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/230eda9b0fe180819f0bfd00744b10ff
---
> 
> 
> <a id="230eda9b0fe1814e9339f03a334753a1"></a>
> 
> <strong>목차</strong>
> 
> - [1. 기본 세팅](#230eda9b0fe1812799efc05f56ac8080)
> - [3. Guard를 통한 인가 처리](#230eda9b0fe180f19488f34e08c91e3b)
> - [Reference](#231eda9b0fe1802db307fd2c3ebe252b)

<a id="230eda9b0fe1812799efc05f56ac8080"></a>

### 1&#46; 기본 세팅

1. <code>auth</code> 모듈, 서비스 생성

<a id="230eda9b0fe1803f9a39d5f355eef1c7"></a>

```bash
nest g module auth
nest g service auth
```

1. JWT 패키지 설치

<a id="230eda9b0fe180dc93d2f797e79af501"></a>

```bash
pnpm add --save @nestjs/jwt
```

<a id="230eda9b0fe180f19488f34e08c91e3b"></a>

### 3&#46; Guard를 통한 인가 처리

> ✏️ 
> 
> <a id="231eda9b0fe18045ae21ef57cf16286e"></a>
> 
> <strong>NestJS에서 인증(Authentication)을 전역으로 적용</strong>하면서, <strong>일부 API만 인증 없이 허용(Public)</strong>
> 
> <a id="231eda9b0fe18048bed3f176a0e1f257"></a>
> 
> ```typescript
> // 전체 흐름
> 1. 'APP_GUARD'를 통해 'AuthGuard'를 전역으로 등록 ⇒ 모든 요청에 인증 적용
> 2. '@Public()' 데코레이터를 만들어 특정 라우트를 예외로 지정
> 3. 'AuthGuard' 내부에서 'Reflector'를 사용해 '@Public()'여부 판단
> 4. 인증이 필요한 경우, JWT 토큰 검증 및 사용자 정보 요청 객체에 할당
> ```

<details>
<summary><strong>1&#46; </strong><strong><code>APP&#95;GUARD</code></strong><strong>로 </strong><strong><code>AuthGuard</code></strong><strong> 전</strong><strong>역 적용</strong></summary>

> ✏️ 
> 
> <a id="231eda9b0fe180fba913f64d96dc209e"></a>
> 
> 아래와 같이 전역 설정 시, 모든 라우터에 <code>&#64;UseGuards(AuthGuard)</code>를 안 붙여도 자동으로 적용된다&#46;

<a id="231eda9b0fe180e5bc1df34d1f185277"></a>

```typescript
// auth.module.ts 또는 app.module.ts
import { Module } from '@nestjs/common';
import { APP_GUARD } from '@nestjs/core';
import { AuthGuard } from './auth.guard'; // 아래 정의
import { JwtModule } from '@nestjs/jwt';

@Module({
  imports: [JwtModule.register({ secret: process.env.SECRET_KEY })],  // SECRET_KEY, 환경변수 등록 필요
  providers: [
    {
      provide: APP_GUARD,
      useClass: AuthGuard,
    },
  ],
})
export class AuthModule {}
```

</details>

<details>
<summary><strong>2&#46; </strong><strong><code>&#64;Public()</code></strong><strong> 데코레이터 정의</strong></summary>

> ✏️ 
> 
> <a id="231eda9b0fe1804d8da1e04ddbc99e62"></a>
> 
> <code>SetMetadata()</code>는 Nest의 메타데이터 시스템에 <code>&#34;isPublic&#34;&#58; true</code> 값을 저장한다&#46;

<a id="231eda9b0fe1802fbb7cf9100943a485"></a>

```typescript
// public.decorator.ts
import { SetMetadata } from '@nestjs/common';

export const IS_PUBLIC_KEY = 'isPublic';
export const Public = () => SetMetadata(IS_PUBLIC_KEY, true);
```

</details>

<details>
<summary>3&#46; <strong><code>AuthGuard</code></strong> 구현</summary>

<a id="231eda9b0fe180eea301db196ba35aaa"></a>

```typescript
// auth.guard.ts
import {
  CanActivate,
  ExecutionContext,
  Injectable,
  UnauthorizedException,
} from '@nestjs/common';
import { Reflector } from '@nestjs/core';
import { JwtService } from '@nestjs/jwt';
import { Request } from 'express';
import { IS_PUBLIC_KEY } from './public.decorator';

@Injectable()
export class AuthGuard implements CanActivate {
  constructor(
    private jwtService: JwtService,
    private reflector: Reflector,
  ) {}

  async canActivate(context: ExecutionContext): Promise<boolean> {
    // 1. 메서드 또는 클래스에 @Public()이 붙었는지 확인
    const isPublic = this.reflector.getAllAndOverride<boolean>(IS_PUBLIC_KEY, [
      context.getHandler(), // 메서드 수준
      context.getClass(),   // 클래스 수준
    ]);
    if (isPublic) return true; // @Public() 이면 인증 패스

    // 2. JWT 인증 처리
    const request = context.switchToHttp().getRequest<Request>();
    const token = this.extractTokenFromHeader(request);
    if (!token) {
      throw new UnauthorizedException('No token provided');
    }

    try {
      const payload = await this.jwtService.verifyAsync(token, {
        secret: process.env.SECRET_KEY, // SECRET_KEY, 환경변수 등록 필요
      });
      request['user'] = payload; // 요청에 사용자 정보 저장
    } catch {
      throw new UnauthorizedException('Invalid token');
    }

    return true;
  }

  private extractTokenFromHeader(request: Request): string | undefined {
    const [type, token] = request.headers.authorization?.split(' ') ?? [];
    return type === 'Bearer' ? token : undefined;
  }
}
```

</details>

<details>
<summary><strong>4&#46; API에 </strong><strong><code>&#64;Public()</code></strong><strong> 적용</strong></summary>

<a id="231eda9b0fe180b5b230f044e67ce0c5"></a>

```typescript
// example.controller.ts
import { Controller, Get } from '@nestjs/common';
import { Public } from './auth/public.decorator';

@Controller('example')
export class ExampleController {
  @Public()
  @Get('open')
  getOpenData() {
    return { message: '이 API는 인증 없이 접근 가능' };
  }

  @Get('private')
  getPrivateData() {
    return { message: '이 API는 인증 필요' };
  }
}
```

</details>

<a id="231eda9b0fe1802db307fd2c3ebe252b"></a>

### Reference

[Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()

[Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()

[Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()
