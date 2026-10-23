---
order: 1
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 26deda9b-0fe1-8118-bfba-d6685fee395f
title: "[ 실습 ] JWT 토큰 파싱 미들웨어 계층에서 처리"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 260eda9b-0fe1-801b-836b-c2e229a88ff9
    title: 한 번에 끝내는 NestJS 패키지 - Part 1. 기초
  - id: 26deda9b-0fe1-8055-ab0b-e18fc733ed0a
    title: 미들웨어 ( middleware )
  - id: 26deda9b-0fe1-8118-bfba-d6685fee395f
    title: "[ 실습 ] JWT 토큰 파싱 미들웨어 계층에서 처리"
excerpt: "목차 - [[문제점] ](26deda9b0fe18053a47fc2263e90ff49) - [[해결]](26deda9b0fe180b5a5dee2f651a37fc0) [문제점] ❗ 매번 JWT 토큰을 파싱하기 위해서는 AuthSerice.parseBearerToken(...)을 호출 해야한다. 이를 인가 처리가 필요한 모든 "
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 26deda9b-0fe1-8055-ab0b-e18fc733ed0a
created: 2025-09-13T04:31:05.534Z
updated: 2025-09-13T09:09:01.706Z
legacy_path: Main/Nest.js-c3a886768c4d/한 번에 끝내는 NestJS 패키지 - Part 1. 기초-c2e229a88ff9/미들웨어 ( middleware )-e18fc733ed0a/[ 실습 ] JWT 토큰 파싱 미들웨어 계층에서 처리-d6685fee395f/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/26deda9b0fe18118bfbad6685fee395f
---
> 
> 
> <a id="26deda9b0fe1812a9ff8d5141ba82c13"></a>
> 
> <strong>목차</strong>
> 
> - [[문제점] ](#26deda9b0fe18053a47fc2263e90ff49)
> - [[해결]](#26deda9b0fe180b5a5dee2f651a37fc0)

<a id="26deda9b0fe18053a47fc2263e90ff49"></a>

### &#91;문제점&#93; 

> ❗ 
> 
> <a id="26deda9b0fe180069c1bc053eb46692e"></a>
> 
> 매번 JWT 토큰을 파싱하기 위해서는 <code>AuthSerice&#46;parseBearerToken(&#46;&#46;&#46;)</code>을 호출 해야한다&#46; 
> 
> <a id="26deda9b0fe1804492fff25727f78035"></a>
> 
>  이를 인가 처리가 필요한 모든 router 계층에서 처리하면 중복 코드 발생 및 유지보수 측면에서도 매우 비효율적이다&#46; 
> 
> <a id="26deda9b0fe180c5b44cddae176dd512"></a>
> 
> 이를 middlware 계층에서 처리하여 해당 문제점을 해결한다&#46; 

<details>
<summary><strong>&#91; 코드 &#93;  AuthService</strong></summary>

<a id="26deda9b0fe1803898f7f03d7fcdd5a8"></a>

```typescript
import { BadRequestException, Injectable } from '@nestjs/common';
import { ConfigService } from '@nestjs/config';
import { InjectRepository } from '@nestjs/typeorm';
import { Role, User } from 'src/user/entities/user.entity';
import { Repository } from 'typeorm';
import * as bcrypt from 'bcrypt';
import { JwtService } from '@nestjs/jwt';

@Injectable()
export class AuthService {
  constructor(
    @InjectRepository(User)
    private readonly userRepository: Repository<User>,
    private readonly configService: ConfigService,
    private readonly jwtService: JwtService,
  ) {}

  async register(rawToken: string) { ... }
  async login(rawToken: string) { ... }
  async issueToken(user: { id: number; role: Role }, isRefreshToken: boolean) { ... }
  async authenticate(email: string, password: string) { ... }


  parseBasicToken(rawToken: string) {
    /**
     * 1) 토큰을 ' ' 기준으로 스플릿 한 후 토큰 값만 추출하기
     *  * Basic $token  ->  ['Basic', $token]
     */
    const basicSplit = rawToken.split(' ');

    if (basicSplit.length !== 2) {
      throw new BadRequestException('토큰 포맷이 유효하지 않습니다.');
    }

    const [basic, token] = basicSplit;

    if (basic.toLowerCase() !== 'basic') {
      throw new BadRequestException('토큰 포맷이 잘못됐습니다.');
    }

    /**
     * 2) 추출한 토큰을 base64 디코딩해서 이메일과 비밀번호로 나눈다.
     *  * base64  ->  email:password  ->  ['email', 'password']
     */
    const decoded = Buffer.from(token, 'base64').toString('utf-8');

    const inputInfo = decoded.split(':');

    console.log(inputInfo);

    if (inputInfo.length !== 2) {
      throw new BadRequestException('토큰 포맷이 유효하지 않습니다.');
    }

    const [email, password] = inputInfo;

    return {
      email,
      password,
    };
  }
  

  async parseBearerToken(rawToken: string, isRefreshToken: boolean) {
    /// 1) 토큰 ' ' 기준으로 스플릿
    const basicSplit = rawToken.split(' ');

    if (basicSplit.length !== 2) {
      throw new BadRequestException('토큰 포맷이 유효하지 않습니다.');
    }

    const [bearer, token] = basicSplit;

    if (bearer.toLowerCase() !== 'bearer') {
      throw new BadRequestException('토큰 포맷이 유효하지 않습니다.');
    }

    const payload = await this.jwtService.verifyAsync(token, {
      secret: this.configService.get<string>('REFRESH_TOKEN_SECRET'),
    });

    if (isRefreshToken) {
      if (payload.type !== 'refresh') {
        throw new BadRequestException('Refresh Token 입력 바랍니다.');
      }
    } else {
      if (payload.type !== 'access') {
        throw new BadRequestException('Access Token 입력 바랍니다.');
      }
    }

    return payload;
  }
}

```

</details>

<a id="26deda9b0fe180b5a5dee2f651a37fc0"></a>

### &#91;해결&#93;

> ✏️ 
> 
> <a id="26deda9b0fe1808f9051cffd27cf6458"></a>
> 
> Token 파싱을 미들웨어 계층에서 처리하여 <strong><u>모든 router에서 </u></strong><strong><u><code>req&#46;user</code></u></strong><strong><u>를 통해 JWT를 파싱한 payload 값을 가져</u></strong>올 수 있다&#46; 

<details>
<summary>1&#46; 미들웨어 계층에서 <strong><u>JWT 토큰 디코딩</u></strong> 및 <code>req&#46;user</code>에 <code>payload</code> 담기</summary>

> ❗ 
> 
> <a id="26deda9b0fe1804ab2e3de2f1aa7f259"></a>
> 
> middleware의 <code>use()</code> 함수에서 <code>next()</code>를 호출하지 않으면 <strong>요청이 다음 동작으로 넘어가지 않고 멈춘다&#46;</strong>

<details>
<summary><strong>&#91; 코드 &#93; </strong>BearerTokenMiddleware</summary>

<a id="26deda9b0fe18103808acac75046c902"></a>

```typescript
import {
  BadRequestException,
  Injectable,
  NestMiddleware,
  UnauthorizedException,
} from '@nestjs/common';
import { ConfigService } from '@nestjs/config';
import { JwtService } from '@nestjs/jwt';
import { Request, Response, NextFunction } from 'express';

@Injectable()
export class BearerTokenMiddleware implements NestMiddleware {
  constructor(
    private readonly jwtService: JwtService,
    private readonly configService: ConfigService,
  ) {}

  async use(req: Request, res: Response, next: NextFunction) {
    try {
      // Basic $token
      // Bearer $token
      const authHeader = req.headers['authorization'];

      if (!authHeader) {
        next();
        return;
      }

      const payload = await this.parseBearerToken(authHeader);

      req.user = payload;
      next();
    } catch (e) {
      if (e.name === 'TokenExpiredError') {
          throw new UnauthorizedException('토큰이 만료됐습니다.');
      }
      next();
    }
  }

  async parseBearerToken(rawToken: string) {
    const token = this.validateBearerToken(rawToken);
    const decodedPayload = this.isDecodedPayload(token);
    const isRefreshToken = this.isRefreshToken(decodedPayload);

    const secretKey = isRefreshToken
      ? this.configService.get<string>('REFRESH_TOKEN_SECRET')
      : this.configService.get<string>('ACCESS_TOKEN_SECRET');

    const payload = await this.jwtService.verifyAsync(token, {
      secret: secretKey,
    });

    return payload;
  }

  private isRefreshToken(payload: any): boolean {
    if (payload.type === 'refresh') {
      return true;
    } else if (payload.type === 'access') {
      return false;
    } else {
      throw new UnauthorizedException('잘못된 토큰입니다.');
    }
  }

  private isDecodedPayload(token: string) {
    return this.jwtService.decode(token);
  }

  private validateBearerToken(rawToken: string) {
    const basicSplit = rawToken.split(' ');

    if (basicSplit.length !== 2) {
      throw new BadRequestException('토큰 포맷이 유효하지 않습니다.');
    }

    const [bearer, token] = basicSplit;

    if (bearer.toLowerCase() !== 'bearer') {
      throw new BadRequestException('토큰 포맷이 유효하지 않습니다.');
    }

    return token;
  }
}

```

</details>

</details>

<details>
<summary>2&#46; 정의한 미들웨어의 DI를  위한 필요한 의존성 export</summary>

> ✏️ 
> 
> <a id="26deda9b0fe18096b855d09281a2339b"></a>
> 
> <code>BearerTokenMiddleware</code> 에서 <code>JwtService</code>를 DI 받는다&#46; <br>따라서 이를 처리하기 위해 <code>JwtModule</code>을 export 할 필요가 있다&#46;
> 
> - 환경변수를 받아오기 위해 <code>ConfigService</code>도 주입받지만, 이미 글로벌로 등록했기 때문에 따로 추가할 필요가 없다&#46;

> ❗ 
> 
> <a id="26deda9b0fe18049812ada6cc33a01b5"></a>
> 
> <code>JwtModule</code>은 JWT 생성, 검증, 파싱을 위해 <code>&#64;nestjs/jwt</code> 패키지에서 제공하는 모듈이다&#46; 사용할 Module 계층에서 정의하여 JwtService를 DI 받아 JWT 생성, 검증, 파싱을 할 수 있다 &#46;

<details>
<summary>&#91; 코드 &#93; AuthModule &#45; <code>JwtModule</code> export 처리</summary>

<a id="26deda9b0fe1807d85bfc749530ad351"></a>

```typescript
import { Module } from '@nestjs/common';
import { AuthService } from './auth.service';
import { AuthController } from './auth.controller';
import { TypeOrmModule } from '@nestjs/typeorm';
import { User } from 'src/user/entities/user.entity';
import { JwtModule } from '@nestjs/jwt';
import { LocalStrategy } from './strategy/local.strategy';
import { JwtStrategy } from './strategy/jwt.strategy';

@Module({
  imports: [TypeOrmModule.forFeature([User]), JwtModule.register({})],
  controllers: [AuthController],
  providers: [AuthService, LocalStrategy, JwtStrategy],
  exports: [AuthService, JwtModule],
})
export class AuthModule {}

```

</details>

</details>

<details>
<summary>3&#46; 루트 모듈(<code>AppModule</code>)에 해당하는 미들웨어 등록</summary>

<a id="26deda9b0fe18033a38bffc462c0f205"></a>

<strong>&#91; 코드 &#93;  </strong>AppModule

<a id="26deda9b0fe1809da2d9c7afce65fa00"></a>

```typescript
import {
  MiddlewareConsumer,
  Module,
  NestModule,
  RequestMethod,
} from '@nestjs/common';
import { TypeOrmModule } from '@nestjs/typeorm';
import { User } from './user/entities/user.entity';
import { AuthModule } from './auth/auth.module';
import { UserModule } from './user/user.module';
import { ConfigModule, ConfigService } from '@nestjs/config';
import { SnakeNamingStrategy } from 'typeorm-naming-strategies';
import * as Joi from 'joi';
import { BearerTokenMiddleware } from './auth/middlware/bearer-token.middleware';

@Module({  . . . })
export class AppModule implements NestModule {
  configure(consumer: MiddlewareConsumer) {
    consumer
      .apply(BearerTokenMiddleware)  // 미들웨어 적용
      .exclude(  // 예외 처리할 라우터 설정
        { path: '/auth/register', method: RequestMethod.POST },
        { path: '/auth/login', method: RequestMethod.POST },
      )
      .forRoutes('*'); // 모든 라우터 계층에 적용
  }
}

```

</details>

<details>
<summary>4&#46; router 에서 디코딩된 JWT payload 불러오기</summary>

<a id="26deda9b0fe1803c842ef313c517385f"></a>

<strong>&#91; 코드 &#93;  </strong>AuthController<strong>&#46;</strong>rotateAccessToken()

<a id="26deda9b0fe1801dac35eb07dc4346d7"></a>

```typescript

export class AuthController {
  constructor(private readonly authService: AuthService) {}
  
	  . . .

  @Post('token/access')
  async rotateAccessToken(@Req() req) {
    const payload = await Promise.resolve(req.user); // 혹시 모를 Promise 방지
    if (!payload || payload.type !== 'refresh') {
      throw new UnauthorizedException('잘못된 토큰입니다.');
    }
    return {
      accessToken: await this.authService.issueToken(payload, false),
    };
  }
}
```

</details>
