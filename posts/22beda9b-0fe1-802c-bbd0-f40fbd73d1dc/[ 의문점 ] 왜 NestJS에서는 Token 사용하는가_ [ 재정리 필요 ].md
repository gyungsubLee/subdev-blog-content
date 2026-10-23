---
order: 41
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 22beda9b-0fe1-802c-bbd0-f40fbd73d1dc
title: "[ 의문점 ] 왜 NestJS에서는 Token 사용하는가? [ 재정리 필요 ]"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
    title: 탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )
  - id: 22beda9b-0fe1-802c-bbd0-f40fbd73d1dc
    title: "[ 의문점 ] 왜 NestJS에서는 Token 사용하는가? [ 재정리 필요 ]"
excerpt: 목차 - 1. 토큰이란 무엇인가? - 2. Spring 과 비교 - 3. 왜 NestJS는 토큰이 필요한가? - 4. 예외) Spring에서의 토큰 명시 - 5. 동작 흐름 - 6. 정리 - Reference 1. 토큰이란 무엇인가? --- ✏️ Nest에서 토큰(token)은 의존성을 주입하기 위한 ‘식별자’를 말한다.
cover: null
icon: 🧐
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
created: 2025-07-09T09:22:48.081Z
updated: 2025-07-10T04:15:47.407Z
legacy_path: Main/Nest.js-c3a886768c4d/탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )-d4fc3e106054/[ 의문점 ] 왜 NestJS에서는 Token 사용하는가- [ 재정리 필요 ]-f40fbd73d1dc/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/22beda9b0fe1802cbbd0f40fbd73d1dc
---
> 
> 
> <a id="22beda9b0fe1810ca557eeff334c2c0c"></a>
> 
> <strong>목차</strong>
> 
> - [1. 토큰이란 무엇인가?](#22beda9b0fe18037a9e4f270316e7187)
> - [2. Spring 과 비교](#22beda9b0fe180ddb3f7ff8def48b947)
> - [3. 왜 NestJS는 토큰이 필요한가?](#22beda9b0fe180b59474efafe59deeff)
> - [4. 예외) Spring에서의 토큰 명시](#22beda9b0fe1805ca64aded205fc8eda)
> - [5. 동작 흐름](#22beda9b0fe18089a1baec56c316f5dc)
> - [6. 정리](#22beda9b0fe180b6bbc8cb70dca43810)
> - [Reference](#22beda9b0fe18006bc49eb08d989389d)

<a id="22beda9b0fe18037a9e4f270316e7187"></a>

## 1&#46; 토큰이란 무엇인가?

---

> ✏️ 
> 
> <a id="22beda9b0fe1805bb13acfd6ac6e09fd"></a>
> 
> Nest에서 토큰(token)은 의존성을 주입하기 위한 ‘식별자’를 말한다&#46;
> 
> - 인스턴스가 아니다&#46;

<a id="22beda9b0fe180cf87ceccf8b95f2a27"></a>

```typescript
// 등록 (app.module.ts)
providers: [CatsService] // == 토큰: CatsService, 값: CatsService 클래스
```

- NestJS에서는 이 토큰을 기반으로 IoC 컨테이너가 해당 서비스를 인스턴스화하고 <code>&#64;Injectable()</code>로 선언된 곳에 주입한다&#46;

<a id="22beda9b0fe180ddb3f7ff8def48b947"></a>

## 2&#46; Spring 과 비교

---

> 📖 
> 
> <a id="22beda9b0fe1802fac83dbeee755f6c2"></a>
> 
> <code>S</code><strong><code>pring</code></strong><strong>은 </strong><u>컴파일 타임에 타입 정보를 유지</u><strong>하며, 클래스 이름 자체를 토큰처럼 사용하는 반면</strong>,
> 
> <a id="22beda9b0fe1802199bccb8cd00b3221"></a>
> 
> <strong><code>NestJS</code></strong><strong>는 </strong><strong><u>런타임에서 DI를 처리</u></strong>하기 때문에<u> </u><strong><u>‘토큰(Token)’ 개념이 필수</u></strong><strong>이다&#46;</strong>
> 
> <a id="22beda9b0fe180deab42cea492133541"></a>
> 
> 즉, 둘 다 비슷한 구조지만 <strong>실행 타이밍, 언어 특성, 런타임 반영 수준에서 차이점을 보인다&#46; </strong>

| <strong>구분</strong> | <strong>Spring (Java)</strong> | <strong>NestJS (TypeScript)</strong> |
| --- | --- | --- |
| 언어 | Java (정적 타입) | TypeScript (런타임에 타입 사라짐) |
| DI 방식 | 클래스명 기반 주입 (타입으로 추론) | 런타임 토큰 기반 주입 |
| 컨테이너 식별자 | 클래스 or &#64;Qualifier(“이름”) | 클래스 or 문자열 or symbol |
| 컴파일 시 타입 유지 | ✅ (리플렉션 불필요) | ❌ (런타임에서 타입 정보 필요) |
| DI 등록 | &#64;Component, &#64;Service 자동 탐지 | &#64;Injectable &#43; &#64;Module&#46;providers 수동 등록 |
| DI 해석 방식 | 리플렉션 없이 컴파일러가 결정 | 리플렉션(Metadata)과 토큰 |

<details>
<summary>ex) Spring</summary>

> ✏️ 
> 
> <a id="22beda9b0fe18061b490f715e95cc971"></a>
> 
> Spring은 UserService 클래스 타입을 기준으로 DI을 한다&#46;
> 
> - &#64;ComponentScan을 통해 자동으로 Bean 등록
> 
> - 컴파일 타임에 타입이 정해지므로 <strong>추가 토큰 필요 없음</strong>

<a id="22beda9b0fe180ab9fc2d8c4e12e233b"></a>

```java
@Service
public class UserService {}

@RestController
public class UserController {

    private final UserService userService;

    public UserController(UserService userService) {
        this.userService = userService; // 타입으로 자동 주입
    }
}
```

</details>

<details>
<summary>ex) NestJS</summary>

> ✏️ 
> 
> <a id="22beda9b0fe1800e8923e0b2a5cc201d"></a>
> 
> <strong>Nest는 런타임에 DI를 해석한다&#46;</strong>
> 
> - 타입스크립트의 reflect&#45;metadata를 사용하여<br>&#34;UserService&#34;가 어떤 클래스인지 런타임에서 추적한다&#46;

<a id="22beda9b0fe180a8a697c5ae97b849ef"></a>

```typescript
@Injectable()
export class UserService {}

@Controller()
export class UserController {
  constructor(private userService: UserService) {}
}
```

</details>

<a id="22beda9b0fe180b59474efafe59deeff"></a>

## 3&#46; 왜 NestJS는 토큰이 필요한가?

---

<a id="22beda9b0fe180b9b7aae9033cedcde5"></a>

```typescript
// TypeScript
constructor(private userService: UserService) {}

// 컴파일 후 JS
constructor(userService) { }
```

<a id="22beda9b0fe18028b791e382ae61964f"></a>

TypeScript는 컴파일 후 JavaScript로 변환되면서 타입 정보가 사라진다&#46;

<a id="22beda9b0fe180889851d60a2000c9d3"></a>

```typescript
Reflect.getMetadata('design:paramtypes', UserController) 
// => [UserService]
```

<a id="22beda9b0fe18045803df803dc8792c8"></a>

따라서 Nest는 <strong><u>런타임</u></strong>에 위와 같이<strong> </strong><u>메타데이터를 읽어 어떤 타입인지 추적</u>한다&#46;

<a id="22beda9b0fe18005b724d1bf10ce76a9"></a>

그러나 <strong><u>타입(인터페이스)에 대한 정보는 남지 않기 때문</u></strong>에 <strong><u>토큰 기반으로 의존성을 주입</u></strong>하여 해결한다&#46; 

<a id="22beda9b0fe1805ca64aded205fc8eda"></a>

### 4&#46; 예외) Spring에서의 토큰 명시

<a id="22beda9b0fe1804e888ecb4dd938f0c5"></a>

```java
@Autowired
@Qualifier("tossPayService")
private PaymentService paymentService;
```

- 다형성을 사용하는 경우, <code>&#64;Qualifier</code>, <code>&#64;Primary</code>으로 토큰(이름)을 명시한다&#46;

<a id="22beda9b0fe18089a1baec56c316f5dc"></a>

### 5&#46; 동작 흐름

<a id="22beda9b0fe18019beb7e51837256b8a"></a>

```typescript
  ┌───────────────────────────────┐                        ┌───────────────────────────────┐
  │        Spring (Java)          │                        │       NestJS (TypeScript)     │
  └───────────────────────────────┘                        └───────────────────────────────┘

    [1] @Component/@Service 등록                                   [1] @Injectable 등록
             ↓                                                             ↓
┌─────────────────────────────────────────┐                  ┌────────────────────────────┐
│ Spring ApplicationContext( IoC 컨테이너 ) │                  │     Nest IoC Container     │
└─────────────────────────────────────────┘                  └────────────────────────────┘
             ↓                                                             ↓
   [2] 컴파일 시 타입 유지 (Class info 존재)                          [2] 런타임에 타입 정보 없음
             ↓                                                             ↓
   [3] 생성자 파라미터 타입 추론 가능                                   [3] reflect-metadata로 param 타입 추적
             ↓                                                             ↓
   [4] 타입(Class) 기반으로 자동 주입                                 [4] 토큰(Token) 기반으로 주입
             ↓                                                             ↓
   [5] Bean 인스턴스 생성 및 주입                                    [5] Provider 인스턴스 생성 및 주입
             ↓                                                             ↓
   [6] 최종 객체 완성                                               [6] 최종 객체 완성

   ✅ 타입 기반 자동 주입                                             ✅ 토큰 기반 DI 시스템

```

<a id="22beda9b0fe180b6bbc8cb70dca43810"></a>

### 6&#46; 정리

| <strong>질문</strong> | <strong>답변</strong> |
| --- | --- |
| Spring은 토큰 없이도 동작하는데, Nest는 왜 필요한가? | Spring은 Java의 정적 타입 시스템을 활용해 <strong>컴파일 타임에 타입이 확정</strong>되므로 추가 토큰 없이도 주입이 가능하다&#46;<br>반면 NestJS는 <strong>런타임 DI</strong>를 하기 때문에 타입을 식별할 수 있는 토큰이 필요하다&#46; |
| Nest는 무조건 토큰을 써야 하나? | 대부분은 클래스 자체를 토큰으로 자동 추론하지만, <u>인터페이스나 커스텀 주입 시에는 명시적 토큰이 반드시 필요</u><strong>하다&#46;</strong> |
| Spring도 토큰을 쓰는 경우가 있나? | 다형성(인터페이스 주입, Bean 다중 구현체) 상황에서는 <code>&#64;Qualifier</code>, <code>&#64;Primary</code>로 토큰(이름) 지정이 필요하다&#46; |

<a id="22beda9b0fe18006bc49eb08d989389d"></a>

### Reference

[The IoC Container &#58;&#58; Spring Framework]()

[Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()

[What is reflect&#45;metadata in typescript]()
