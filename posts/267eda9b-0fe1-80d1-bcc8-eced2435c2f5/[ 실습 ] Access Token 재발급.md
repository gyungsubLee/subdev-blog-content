---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 267eda9b-0fe1-80d1-bcc8-eced2435c2f5
title: "[ 실습 ] Access Token 재발급"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 260eda9b-0fe1-801b-836b-c2e229a88ff9
    title: 한 번에 끝내는 NestJS 패키지 - Part 1. 기초
  - id: 266eda9b-0fe1-80c6-ac72-d9ab723eb5e7
    title: 인증 / 인가 ( Authentication / Authrization )
  - id: 267eda9b-0fe1-80d1-bcc8-eced2435c2f5
    title: "[ 실습 ] Access Token 재발급"
excerpt: Access Token 재발급 --- 1. 의존성 설치 @nestjs/jwt, passport, @nestjs/passport, passport-local ( strategy ), passport-jwt ( strategy ) bash pnpm i @nestjs/jwt @nestjs/passport passport pas
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 266eda9b-0fe1-80c6-ac72-d9ab723eb5e7
created: 2025-09-07T14:13:10.927Z
updated: 2025-09-13T04:36:17.080Z
legacy_path: Main/Nest.js-c3a886768c4d/한 번에 끝내는 NestJS 패키지 - Part 1. 기초-c2e229a88ff9/인증 - 인가 ( Authentication - Authrization )-d9ab723eb5e7/[ 실습 ] Access Token 재발급-eced2435c2f5/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/267eda9b0fe180d1bcc8eced2435c2f5
---
<a id="267eda9b0fe1812b9e1cf2440e7d43fe"></a>

## Access Token 재발급

---

<a id="267eda9b0fe181c08a68fd422c3e9f58"></a>

### 1&#46; 의존성 설치

<details>
<summary><code>&#64;nestjs/jwt</code>, <code>passport</code>, <code>&#64;nestjs/passport</code>, <code>passport&#45;local</code> ( strategy ), <code>passport&#45;jwt</code> ( strategy )</summary>

<a id="267eda9b0fe181a1a3d6ca4059036268"></a>

```bash
pnpm i @nestjs/jwt @nestjs/passport passport passport-local passport-jwt
pnpm i -D @types/passport-local @types/passport-jwt
```

</details>

<a id="267eda9b0fe181869d9ed86a5b153822"></a>

### 2&#46; Access token 재발급

> ✏️ 
> 
> <a id="269eda9b0fe180f9833fcc235b9a017b"></a>
> 
> 흐름
> 
> 1. &#91;클라이언트&#93; 만료된 access token을 담아 요청을 보냄
> 
> 1. &#91;서버&#93; 토큰의 만료 여부를 확인하고 예외 응답처리
> 
> 1. &#91;클라이언트&#93; 예외 응답을 확인하고 refresh token을 담아 access token 재발급 요청
> 
> 1. &#91;서버&#93; refresh token 검증 후, access token 재발급
> 
> 1. &#91;클라이언트&#93; 재발급된 토큰으로 인가 요청 → 정상 응답 

<details>
<summary><strong>&#91; 코드 &#93; AuthService </strong>&#45; <code>parseBearerToken(…)</code>&#58; 토큰</summary>

<a id="267eda9b0fe18151ba5dd615ea61cfb9"></a>

```typescript
async parseBearerToken(rawToken: string, isRefreshToken: boolean) {
  // 1. 토큰 포맷 예외처리
  const basicSplit = rawToken.split(' ');

  if (basicSplit.length !== 2) {
    throw new BadRequestException('토큰 포맷이 유효하지 않습니다.');
  }

  const [bearer, token] = basicSplit;

  if (bearer.toLowerCase() !== 'bearer') {
    throw new BadRequestException('토큰 포맷이 유효하지 않습니다.');
  }
	
	// 2. 검증
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
```

<details>
<summary>&#91; 코드 &#93; auth&#46;service&#46;ts</summary>

<a id="269eda9b0fe18028b2aad7a5ca1f3c51"></a>

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

  /// rawToken: Basic $token
  async register(rawToken: string) {
    const { email, password } = this.parseBasicToken(rawToken);

    const user = await this.userRepository.findOne({
      where: { email },
    });

    if (user) {
      throw new BadRequestException('이미 가입한 이메일입니다.');
    }

    // 환경변수 처리: 해시 강도(HASH_ROUNDS) 기본값 10
    const saltRounds = Number(
      this.configService.get<number | string>('HASH_ROUNDS', 10),
    );

    const hash = await bcrypt.hash(password, saltRounds);

    await this.userRepository.save({
      email,
      password: hash,
    });

    return this.userRepository.findOne({
      where: { email },
    });
  }

  /// rawToken: Basic $token
  async login(rawToken: string) {
    const { email, password } = this.parseBasicToken(rawToken);

    const user = await this.authenticate(email, password);

    return {
      refreshToken: await this.issueToken(user, true),
      accessToken: await this.issueToken(user, false),
    };
  }

  async issueToken(user: { id: number; role: Role }, isRefreshToken: boolean) {
    const refreshTokenSecret = this.configService.get<string>(
      'REFRESH_TOKEN_SECRET',
    );
    const accessTokenSecret = this.configService.get<string>(
      'ACCESS_TOKEN_SECRET',
    );

    return this.jwtService.signAsync(
      {
        sub: user.id,
        role: user.role,
        type: isRefreshToken ? 'refresh' : 'access',
      },
      {
        secret: isRefreshToken ? refreshTokenSecret : accessTokenSecret,
        expiresIn: isRefreshToken ? '24h' : '300s',
      },
    );
  }

  async authenticate(email: string, password: string) {
    const user = await this.userRepository.findOne({
      where: { email },
    });

    if (!user) {
      throw new BadRequestException('잘못된 로그인 정보입니다.'); // 보안적 취약점이 될 수 있기 때문에, 이메일이라는 구체적 정보를 명시하지 않음
    }

    const passOk = await bcrypt.compare(password, user.password);

    if (!passOk) {
      throw new BadRequestException('잘못된 로그인 정보입니다.'); // 보안적 취약점이 될 수 있기 때문에, 이메일이라는 구체적 정보를 명시하지 않음
    }

    return user;
  }

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

<a id="269eda9b0fe180b49c19c3191d232eb8"></a>

 

</details>

</details>

<details>
<summary><strong>&#91; 코드 &#93;  AuthController &#45; </strong><code>rotateAccessToken()</code>&#58; 토큰 재발급</summary>

<a id="269eda9b0fe180e49e6fd4a1d4740daa"></a>

```typescript
@Post('token/access')
async rotateAccessToken(@Headers('authorization') token: string) {
  const payload = await this.authService.parseBearerToken(token, true);  // 토큰 파싱 -> payload 추출

  return {
    accessToken: await this.authService.issueToken(payload, false), // 토큰 재발급
  };
}
```

</details>
