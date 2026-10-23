---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 819eda9b-0fe1-830b-9744-01a5ecd072d9
title: Go의 생성자 패턴 (feat. Java 생성자 패턴)
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-805b-a5ac-c76c9ecfc302
    title: Golang
  - id: 3d0eda9b-0fe1-8029-b3f2-dd8560b1d377
    title: Go 의문점 정리
  - id: 819eda9b-0fe1-830b-9744-01a5ecd072d9
    title: Go의 생성자 패턴 (feat. Java 생성자 패턴)
excerpt: "목차 - Go의 생성자 패턴, Java 개발자 눈으로 뜯어보기 - 배경 - 1. 이 코드는 무엇을 하는가 - 2. 필드 선언부: struct vs class - 2.1. 접근 제어자가 없다 — 대신 이름의 대소문자로 구분 - 2.2 final 키워드가 없다 - 3. 생성자 함수: NewUserUsecase vs Java "
cover: null
icon: null
notionProperties:
  AE<<: 🧐 질문,복습
  상태: 완료
schema_version: 1
parent_id: 3d0eda9b-0fe1-8029-b3f2-dd8560b1d377
created: 2026-09-03T02:23:00.088Z
updated: 2026-10-04T01:57:00.825Z
legacy_path: Main/Golang-c76c9ecfc302/Go 의문점 정리-dd8560b1d377/Go의 생성자 패턴 (feat. Java 생성자 패턴)-01a5ecd072d9/index.md
legacy_category: Golang
source_url: https://beautiful-college-c84.notion.site/819eda9b0fe1830b974401a5ecd072d9
---
> 
> 
> <a id="3d0eda9b0fe1804989eecdb13828e06d"></a>
> 
> <strong>목차</strong>
> 
> - [Go의 생성자 패턴, Java 개발자 눈으로 뜯어보기](#3d0eda9b0fe180d29247c5806246af52)
> - [배경](#3d0eda9b0fe18091a44aeb06cc920830)
> - [ 1. 이 코드는 무엇을 하는가](#3d0eda9b0fe180bf90b5cdce42a5407b)
> - [ 2. 필드 선언부: struct vs class](#3d0eda9b0fe18013bc0de8949d08b2bc)
> - [2.1. 접근 제어자가 없다 — 대신 이름의 대소문자로 구분](#3d0eda9b0fe1806aa48bc8839a725afe)
> - [ 2.2 final 키워드가 없다](#3d0eda9b0fe180d591a6cd1d4c9685a8)
> - [ 3. 생성자 함수: NewUserUsecase vs Java 생성자](#3d0eda9b0fe18077a202eb9c12573f40)
> - [ 4. 의존성 주입 방식의 근본적 차이](#3d0eda9b0fe1803fabfae326a5a53cfb)
> - [ 4.1. Java + Spring: 컨테이너가 자동으로 연결](#3d0eda9b0fe18044bf99c715ab97e45e)
> - [ 4.2. Go: 개발자가 직접, 명시적으로 연결](#3d0eda9b0fe180acb577e831d997746f)
> - [ 5. 왜 구체 타입이 아니라 인터페이스(UserService)를 받는가](#3d0eda9b0fe180dfaa76f85e127692dd)
> - [ 정리](#3d0eda9b0fe180b78a95d9a977b1d1b6)

<a id="3d0eda9b0fe180d29247c5806246af52"></a>

# Go의 생성자 패턴, Java 개발자 눈으로 뜯어보기

---

<a id="3d0eda9b0fe18091a44aeb06cc920830"></a>

## 배경

<a id="3d0eda9b0fe18008bc33f49108c539b5"></a>

Spring 개발자가 Go 코드를 처음 보면 당황스러울 수 있다&#46; 

<a id="3d0eda9b0fe180278c1ef05c53df889c"></a>

```go
type UserUsecase struct {
	UserService service.UserService
	JWTSecret   string
}

func NewUserUsecase(userService service.UserService, jwtSecret string) *UserUsecase {
	return &UserUsecase{
		UserService: userService,
		JWTSecret:   jwtSecret,
	}
}
```

<a id="3d0eda9b0fe18087a12ef02696bd53db"></a>

위 코드를 보자 생성자 주입을 통해 외부에서 의존성을 넣는 코드이다&#46;  

<a id="3d0eda9b0fe1808ebb41e80aa0da71a4"></a>

이와 동일한 자바 코드는 아래와 같다&#46; 

<a id="3d0eda9b0fe180db89b7dfac37a49e44"></a>

```java
public class UserUsecase {
    private final UserService userService;
    private final String jwtSecret;

    public UserUsecase(UserService userService, String jwtSecret) {
        this.userService = userService;
        this.jwtSecret = jwtSecret;
    }
}
```

<a id="3d0eda9b0fe180d696bfc10d48e46bf0"></a>

다시 Go 코드로 돌아가보면 

<a id="3d0eda9b0fe18084bd42f4fec73fcc32"></a>

```go
type UserUsecase struct {
	UserService service.UserService
	JWTSecret   string
}

func NewUserUsecase(userService service.UserService, jwtSecret string) *UserUsecase {
	return &UserUsecase{
		UserService: userService,
		JWTSecret:   jwtSecret,
	}
}
```

<a id="3d0eda9b0fe1806f9b0de5d783dd41d9"></a>

Java와 다르게 클래스도 없고, <code>&#64;Autowired</code>도 없고, <code>new</code> 키워드조차 안 보인다&#46; 

<a id="3d0eda9b0fe18034bac1e58d131d3c2d"></a>

그렇다면 어떻게 의존성을 주입이 가능한 것인가? 

<a id="3d0eda9b0fe180fab948caea7caec588"></a>

이 글에서는 위 짧은 Go 코드를 기반으로, Java의 생성자 주입 패턴과 비교하며 Go의 방식을 살펴본다&#46;

<a id="3d0eda9b0fe180bf90b5cdce42a5407b"></a>

##  1&#46; 이 코드는 무엇을 하는가

<a id="3d0eda9b0fe180fd9d40dc47c149e068"></a>

```go
type UserUsecase struct {
	UserService service.UserService
	JWTSecret   string
}

func NewUserUsecase(userService service.UserService, jwtSecret string) *UserUsecase {
	return &UserUsecase{
		UserService: userService,
		JWTSecret:   jwtSecret,
	}
}
```

<a id="3d0eda9b0fe180afa21cf755157228e5"></a>

위 예시 코드를 한 문장으로 요약하면 이렇다&#46; 

> ✏️ 
> 
> <a id="3d0eda9b0fe180e4994ffe99831da565"></a>
> 
> <strong><code>UserUsecase</code></strong><strong>라는 구조체를 정의하고, 그 구조체를 만들 때 필요한 의존성을 생성자 함수로 주입한다&#46; </strong>
> 
> - <strong><code>UserService</code></strong><strong> , </strong><strong><code>JWTSecret</code></strong><strong>을 생성자 함수로 주입</strong>

<a id="3d0eda9b0fe18027879acd8962af31f0"></a>

이는 <strong><u>Clean Architecture</u></strong>나 <strong><u>Hexagonal Architecture</u></strong>에서 흔히 보이는 <strong>Usecase 계층</strong>의 전형적인 형태이다&#46;

<a id="3d0eda9b0fe180a3a915daf9ab1e6799"></a>

 <code>UserUsecase</code>는 회원가입, 로그인, 토큰 발급 같은 실제 비즈니스 로직을 담당하고, 그 로직을 수행하기 위해 아래 두 가지를 필요로 한다&#46;

- <code>UserService</code>&#58; 사용자 데이터를 다루는 하위 계층 (인터페이스)

- <code>JWTSecret</code>&#58; 토큰 서명에 쓸 비밀 키 (설정값)

<a id="3d0eda9b0fe180d1884ae9b7d336c9f3"></a>

이 둘을 구조체 필드로 들고, 생성 시점에 외부에서 주입받는다&#46; 

<a id="3d0eda9b0fe18013bc0de8949d08b2bc"></a>

##  2&#46; 필드 선언부&#58; <code>struct</code> vs <code>class</code>

<a id="3d0eda9b0fe1806f8e15d180a253ff4f"></a>

```go
type UserUsecase struct {
    UserService service.UserService
    JWTSecret   string
}
```

<a id="3d0eda9b0fe1808ea00bf6387e7ab9d3"></a>

Java로 옮기면 필드 선언부는 이렇습니다&#46;

<a id="3d0eda9b0fe1801d8421f31c8f75135e"></a>

```java
public class UserUsecase {
    private final UserService userService;
    private final String jwtSecret;
}
```

<a id="3d0eda9b0fe18090bb42f3f0b7922d70"></a>

여기서 눈여겨볼 두 가지 차이가 있습니다&#46;

<a id="3d0eda9b0fe1806aa48bc8839a725afe"></a>

### 2&#46;1&#46; 접근 제어자가 없다 — 대신 이름의 대소문자로 구분

> 자세한 내용은 해당 포스팅 참조&#58; <a href="#/post/3d0eda9b-0fe1-8072-a39d-f8fb0b030547">페이지</a> 

<a id="3d0eda9b0fe180c0a4b9e99606ce04f0"></a>

Java는 <code>private</code>, <code>public</code> 같은 키워드로 접근 범위를 명시한다&#46;

<a id="3d0eda9b0fe180a19413ff026c61ab2a"></a>

그러나<strong> Go에는 그런 키워드가 없</strong>다&#46; 

<a id="3efeda9b0fe18095abd0e8b42cfc45e2"></a>

대신 <strong><u>필드명의 첫 글자</u></strong><strong>가 </strong><strong><code>대문자</code></strong><strong>면</strong><strong> 외부 패키지에서도 접근 가능(export)</strong><strong>, </strong><code>소문자</code>면 <strong>같은 패키지 내에서만 접근 가능</strong>하다&#46;

<a id="3d0eda9b0fe180ebaf1ad3bf0ef66832"></a>

```go
type UserUsecase struct {
    UserService service.UserService // 대문자 시작 → public
    jwtSecret   string              // 소문자 시작 → private (패키지 내부 전용)
}
```

<a id="3d0eda9b0fe1806385becf3a5acc46c7"></a>

예시 코드에서는 <code>JWTSecret</code>이 대문자로 시작하므로 사실상 public 필드이다&#46; 

<a id="3d0eda9b0fe180018d85d79c328d0d0f"></a>

민감한 값이라면 Go에서도 관례상 소문자로 낮추고 Getter를 별도로 두는 경우가 많다&#46;

<a id="3d0eda9b0fe180d591a6cd1d4c9685a8"></a>

###  2&#46;2 <code>final</code> 키워드가 없다

<a id="3d0eda9b0fe18052b9edfce24bbefb22"></a>

Java는 <code>private final</code>로 <strong><u>생성 이후 </u></strong><strong><u>재할당 금지</u></strong>를 <strong>컴파일러 차원에서 강제</strong>할 수 있다&#46;

<a id="3d0eda9b0fe1802cbac2f9c7603af776"></a>

Go 구조체 필드는 이런 불변성 강제 수단이 없다&#46; 대신 아래처럼 관례로 우회한다&#46; 

> ✏️ 
> 
> - 필드를 소문자(비공개)로 감춘다
> 
> - 생성자 함수(<code>NewXxx</code>)를 통해서만 값을 채우도록 유도한다
> 
> - 재할당이 필요 없다는 걸 코드 리뷰와 팀 컨벤션으로 지킨다

<a id="3d0eda9b0fe1802cb4fdf579e1fbb4f9"></a>

즉, Java는 <strong>언어가 불변성을 강제</strong>하고, <strong><u>Go는 관례</u></strong>가 <strong><u>불변성을 유도</u></strong>한다는 차이가 있다&#46;

<a id="3d0eda9b0fe18077a202eb9c12573f40"></a>

##  3&#46; 생성자 함수&#58; <code>NewUserUsecase</code> vs Java 생성자

<a id="3d0eda9b0fe18077b162f1f23d5f83fb"></a>

```go
func NewUserUsecase(userService service.UserService, jwtSecret string) *UserUsecase {
    return &UserUsecase{
        UserService: userService,
        JWTSecret:   jwtSecret,
    }
}
```

<a id="3d0eda9b0fe1806c9621ccaf2a4409da"></a>

Go에는 Java의 <code>public UserUsecase(&#46;&#46;&#46;)</code> 같은 전용 생성자 문법이 없다&#46; 

<a id="3d0eda9b0fe180beab69f76afd6fe102"></a>

대신 <strong><code>New</code></strong><strong> &#43; 타입명</strong>으로 이름 붙인 평범한 함수를 만들어 생성자처럼 사용하는 것이 커뮤니티 관례이다&#46;

<a id="3d0eda9b0fe180bea4a3ce44d262a674"></a>

```java
public class UserUsecase {
    private final UserService userService;
    private final String jwtSecret;

    public UserUsecase(UserService userService, String jwtSecret) {
        this.userService = userService;
        this.jwtSecret = jwtSecret;
    }
}
```

<a id="3d0eda9b0fe18064a22ef78910f81b57"></a>

두 코드가 하는 일은 사실상 동일하다&#46;

| 단계 | Go | Java |
| --- | --- | --- |
| 객체 생성 | <code>&#38;UserUsecase{&#46;&#46;&#46;}</code> <br>(구조체 리터럴 &#43; 포인터) | <code>new UserUsecase(&#46;&#46;&#46;)</code> |
| 필드 채우기 | 구조체 리터럴 내에서 직접 대입 | <code>this&#46;필드 = 매개변수</code> |
| 반환 | <code>&#42;UserUsecase</code> (포인터) | 객체 참조 (Java는 객체가 원래 참조 타입) |

<a id="3d0eda9b0fe18017ba2fda3fed6fe8dc"></a>

<code>&#38;UserUsecase{&#46;&#46;&#46;}</code>의 <code>&#38;</code>는 &#34;이 구조체의 메모리 주소를 가리키는 포인터를 만든다&#34;는 뜻이다&#46; 

<a id="3d0eda9b0fe1800f945fdc5e9439236a"></a>

Java 객체는 애초에 참조(reference)로 다뤄지기 때문에 별도 문법이 필요 없지만, Go는 값 타입(value type)과 포인터 타입을 명확히 구분하는 언어라서 <code>&#42;UserUsecase</code>처럼 포인터임을 명시해야 한다&#46;

<a id="3d0eda9b0fe1803fabfae326a5a53cfb"></a>

##  4&#46; 의존성 주입 방식의 근본적 차이

<a id="3d0eda9b0fe18078bb40defab174400b"></a>

여기가 이 코드에서 가장 중요한 지점이다&#46; <strong>&#34;누가 의존성을 연결해주는가?&#34;</strong>

<a id="3d0eda9b0fe18044bf99c715ab97e45e"></a>

###  4&#46;1&#46; Java &#43; Spring&#58; 컨테이너가 자동으로 연결

<a id="3d0eda9b0fe180268db1fbf94adb7163"></a>

```java
@Service
public class UserUsecase {

    private final UserService userService;
    private final String jwtSecret;

    public UserUsecase(UserService userService,
                        @Value("${jwt.secret}") String jwtSecret) {
        this.userService = userService;
        this.jwtSecret = jwtSecret;
    }
}
```

<a id="3d0eda9b0fe180f99e4ce8939c8f77f1"></a>

<code>&#64;Service</code>, <code>&#64;Value</code>, <code>&#64;Autowired</code> 같은 애노테이션을 붙여두면, <strong>Spring IoC 컨테이너</strong>가 애플리케이션 구동 시점에 알아서 <code>UserService</code> 구현체를 찾아 주입하며<br><code>application&#46;yml</code>에서 <code>jwt&#46;secret</code> 값을 읽어온다&#46;

<a id="3d0eda9b0fe180c490d0dbd14487f215"></a>

 개발자는 &#34;무엇이 필요한지&#34;만 선언하면 되고, &#34;어떻게 연결할지&#34;는 프레임워크가 대신한다&#46;

<a id="3d0eda9b0fe180acb577e831d997746f"></a>

###  4&#46;2&#46; Go&#58; 개발자가 직접, 명시적으로 연결

<a id="3d0eda9b0fe180ca97b6de23a213d1aa"></a>

Go 표준 생태계에는 이런 자동 DI 컨테이너가 기본 내장되어 있지 않다&#46; 

- Wire, Fx 같은 서드파티 도구가 있긴 하지만, 예시 코드 자체는 순수 수동 방식이다&#46;

<a id="3d0eda9b0fe18029b165c961420241f4"></a>

그래서 보통 아래와 같이 <code>main&#46;go</code> 같은 진입점에서 이렇게 <strong>직접 조립한다&#46; </strong>

<a id="3d0eda9b0fe18060ad0fc98388e01b04"></a>

```go
func main() {
    // 1. 하위 계층부터 순서대로 생성
    db := database.Connect(os.Getenv("DB_DSN"))
    userRepo := repository.NewUserRepository(db)
    userService := service.NewUserService(userRepo)

    // 2. 앞서 만든 것들을 주입해 Usecase 생성
    jwtSecret := os.Getenv("JWT_SECRET")
    userUsecase := usecase.NewUserUsecase(userService, jwtSecret)

    // 3. 상위 계층(HTTP 핸들러)에 주입
    userHandler := handler.NewUserHandler(userUsecase)

    // 4. 라우터에 등록
    router := gin.Default()
    router.POST("/signup", userHandler.SignUp)
    router.Run(":8080")
}
```

<a id="3d0eda9b0fe1804faf67fb5950c8a1b6"></a>

이렇게 아래에서 위로(리포지토리 → 서비스 → 유즈케이스 → 핸들러) <strong>손으로 하나씩 엮어 올라가는 방식</strong>을 흔히 <code>수동 의존성 주입(Manual DI)</code> 또는 <code>생성자 기반 조립(Constructor Wiring)</code>이라고 부른다&#46;

> 💬 
> 
> <a id="3d0eda9b0fe180009efadf4db9756a45"></a>
> 
> <strong>비유하자면&#58;</strong>
> 
> <a id="3d0eda9b0fe18089ae9af3d539c9d408"></a>
> 
> Spring은 레고 조립 설명서를 보고 로봇이 알아서 블록을 끼워주는 것이고, <br>Go는 사람이 직접 블록을 하나씩 손으로 끼워 맞추는 것과 비슷하다&#46;
> 
> <a id="3d0eda9b0fe180dbb44bcabae4bc8dd5"></a>
> 
> 느리고 번거로워 보이지만, 그만큼 &#34;지금 이 객체가 정확히 어떻게 만들어졌는지&#34;가 코드에 다 드러나 있어 추적이 쉽다&#46;

<a id="3d0eda9b0fe180dfaa76f85e127692dd"></a>

##  5&#46; 왜 구체 타입이 아니라 인터페이스(<code>UserService</code>)를 받는가

<a id="3d0eda9b0fe180be8c9acac0aad874db"></a>

```go
UserService service.UserService  // 구체 구현체가 아니라 인터페이스
```

<a id="3d0eda9b0fe1801ab042dc044f33106c"></a>

이 부분은 Java의 <strong><u>DIP(의존 역전 원칙, Dependency Inversion Principle)</u></strong>와 정확히 같은 이유로 존재한다&#46; 

<a id="3d0eda9b0fe18025b1c0c26763aec82b"></a>

<code>UserUsecase</code>가 <code>MySQLUserService</code> 같은 구체 구현체를 직접 알고 있으면, 나중에 DB를 바꾸거나 테스트용 Mock으로 교체할 때 <code>UserUsecase</code> 코드 자체를 건드려야 한다&#46;

<a id="3d0eda9b0fe180589c89cb6f9367c7c4"></a>

대신 인터페이스를 참조하면 아래와 같은 이점이 생긴다&#46; 

<a id="3d0eda9b0fe180958972c21fd516ded1"></a>

```go
// 테스트 코드에서는 실제 DB 대신 Mock을 주입
mockUserService := &MockUserService{}
usecase := NewUserUsecase(mockUserService, "test-secret")
```

<a id="3d0eda9b0fe1809e8442d6e6557e05a1"></a>

Java에서 Mockito로 <code>&#64;Mock UserService userService</code>를 주입하는 것과 완전히 동일한 발상이다&#46; 

<a id="3d0eda9b0fe1802f8fdcef2246156adb"></a>

다만 Go 인터페이스는 <strong><u>암묵적(implicit)</u></strong>이다&#46; 

<a id="3d0eda9b0fe180c2a2bac5e7ab4ad8f6"></a>

Java처럼 <code>implements UserService</code>라고 명시할 필요 없이, 해당 메서드들을 구현하기만 하면 자동으로 그 인터페이스를 만족한 것으로 간주된다&#46;

<a id="3d0eda9b0fe1806f805fe26a6b4a75f1"></a>

이 점은 Go 인터페이스의 가장 독특한 특징 중 하나입니다&#46;

<a id="3d0eda9b0fe180b78a95d9a977b1d1b6"></a>

##  정리

> 💬 
> 
> <a id="3d0eda9b0fe1807fad94cb7f8c51e30f"></a>
> 
> <code>Go</code> vs <code>Java</code>
> 
> | 관점 | Go | Java (Spring 기준) |
> | --- | --- | --- |
> | 클래스 정의 | <code>struct</code> | <code>class</code> |
> | 생성자 | <code>NewXxx</code> 함수 (관례) | 전용 생성자 문법 |
> | 접근 제어 | 이름의 대소문자 | <code>public</code>/<code>private</code> 키워드 |
> | 불변성 강제 | 없음 (관례로 유도) | <code>final</code> 키워드로 강제 |
> | 의존성 주입 | 대부분 수동 (직접 조립) | 프레임워크가 자동 처리 |
> | 인터페이스 구현 | 암묵적 (덕 타이핑에 가까움) | <code>implements</code> 명시 필요 |
> | 객체 참조 | 포인터(<code>&#42;T</code>) 명시 필요 | 항상 참조 타입 |

<a id="3d0eda9b0fe1801c87dadc89d90041ae"></a>

```go
func NewUserUsecase(userService service.UserService, jwtSecret string) *UserUsecase {
    return &UserUsecase{
        UserService: userService,
        JWTSecret:   jwtSecret,
    }
}
```

<a id="3d0eda9b0fe180a8ba92d2fbcbb390ef"></a>

<code>NewUserUsecase</code> 함수는 내부에는 Go 생태계가 의존성을 다루는 철학이 압축되어 있다&#46;

- <strong>명시성(explicitness)을 우선한다</strong>
    - 마법 애노테이션 대신, 코드를 읽으면 무엇이 어떻게 조립되는지 확인 가능

- <strong>관례가 규칙을 대신한다</strong>
    - <code>final</code> 같은 강제 장치 대신 <code>NewXxx</code> 네이밍 같은 커뮤니티 컨벤션으로 일관성유지

- <strong>작은 표준 라이브러리, 얇은 프레임워크</strong>
    - Spring처럼 거대한 프레임워크가 대신 해주는 일을, <br>Go는 개발자가 직접 코드로 드러내는 쪽을 선호한다&#46;

<a id="3d0eda9b0fe180e29b52cfc80fd6e0c0"></a>

Java/Spring에 익숙한 개발자라면 처음엔 &#34;이걸 다 손으로 해야 해?&#34;라는 생각이 들 수 있지만, 프로젝트가 커질수록 &#34;이 객체가 왜, 어떻게 이렇게 만들어졌는지&#34;를 코드만 보고 바로 추적할 수 있다는 장점이 있다&#46;
