---
order: 2
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 3d0eda9b-0fe1-80ce-b73a-ff32d5bae76e
title: 🧐 Go의 NewXxx()가 왜 항상 포인터를 리턴하는가
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-805b-a5ac-c76c9ecfc302
    title: Golang
  - id: 3d0eda9b-0fe1-8029-b3f2-dd8560b1d377
    title: Go 의문점 정리
  - id: 3d0eda9b-0fe1-80ce-b73a-ff32d5bae76e
    title: 🧐 Go의 NewXxx()가 왜 항상 포인터를 리턴하는가
excerpt: 목차 - Go의 NewXxx()가 왜 항상 포인터를 리턴하는가 - [ [의문점] 왜 포인터를 리턴하는가?](3d0eda9b0fe180528189ea764cf91bf7) - Type{...}와 &Type{...}의 차이 - [ [이유 1] 복사 비용 회피](3d0eda9b0fe180d7b0e2d64fcabc94f5) - [
cover: null
icon: null
notionProperties:
  중요도: Yes
  상태: 완료
schema_version: 1
parent_id: 3d0eda9b-0fe1-8029-b3f2-dd8560b1d377
created: 2026-09-03T03:56:38.627Z
updated: 2026-09-03T07:51:24.284Z
legacy_path: Main/Golang-c76c9ecfc302/Go 의문점 정리-dd8560b1d377/🧐 Go의 NewXxx()가 왜 항상 포인터를 리턴하는가-ff32d5bae76e/index.md
legacy_category: Golang
source_url: https://beautiful-college-c84.notion.site/3d0eda9b0fe180ceb73aff32d5bae76e
---
> 
> 
> <a id="3d0eda9b0fe18092b641dadf57eadefc"></a>
> 
> <strong>목차</strong>
> 
> - [Go의 NewXxx()가 왜 항상 포인터를 리턴하는가](#3d0eda9b0fe1807cb80fd6ed35796962)
> - [ [의문점] 왜 포인터를 리턴하는가?](#3d0eda9b0fe180528189ea764cf91bf7)
> - [Type{...}와 &Type{...}의 차이](#3d0eda9b0fe180d4972bddc356dc7fbb)
> - [ [이유 1] 복사 비용 회피](#3d0eda9b0fe180d7b0e2d64fcabc94f5)
> - [ [이유 2] 인스턴스 공유 (값 타입 사용 시 생기는 버그)](#3d0eda9b0fe1806692c2ff17545b5fc2)
> - [[🤬 오류] 값 타입 선언](#3d0eda9b0fe180b18757c75b789ee58a)
> - [[✅ 성공] 포인터로 수정](#3d0eda9b0fe1806bb06bdb6d0389811d)
> - [ [이유 3] Go 커뮤니티 관례](#3d0eda9b0fe1802dbe94d6d572c5ffda)
> - [ 정리 — 언제 값, 포인터를 사용하는가](#3d0eda9b0fe180c0b206f626dffda2cd)

<a id="3d0eda9b0fe1807cb80fd6ed35796962"></a>

# Go의 NewXxx()가 왜 항상 포인터를 리턴하는가

---

<a id="3d0eda9b0fe180528189ea764cf91bf7"></a>

##  &#91;의문점&#93; 왜 포인터를 리턴하는가?

<a id="3d0eda9b0fe1808684f6dc2e4b591014"></a>

Go로 구현된 백엔드 코드를 읽다보면 아래와 같은 패턴이 계속 등장한다&#46; 

<a id="3d0eda9b0fe18084be20d02b858bca5c"></a>

```go
func NewUserUsecase(userService UserService, jwtSecret string) *UserUsecase {
	return &UserUsecase{
		UserService: userService,
		JWTSecret:   jwtSecret,
	}
}
```

<a id="3d0eda9b0fe1803f82add9f2ed6c7c97"></a>

이를 보며 아래와 같은 의문점이 들었다&#46; 이에 대해 원인 및 해결책을 학습하고 이를 해당 포스팅에 정리한 한다&#46;

> 🤔 
> 
> <a id="3d0eda9b0fe1803fa7aad193f9bfd7fd"></a>
> 
> <code>UserUsecase</code>를 리턴하면 될 것 같은데 <strong><u>왜 </u></strong><strong><u><code>&#42;UserUsecase</code></u></strong><strong><u>, 즉 포인터를 리턴</u></strong>하는가? <code>&#38;</code>를 붙이는 이유는 무엇인가?

<a id="3d0eda9b0fe180d4972bddc356dc7fbb"></a>

## <code>Type{&#46;&#46;&#46;}</code>와 <code>&#38;Type{&#46;&#46;&#46;}</code>의 차이

> 🤔 
> 
> <a id="3d0eda9b0fe180d08924d75f467a3afa"></a>
> 
> 해당 예제에서 사용하는 구조체 생성 문법은 아래 포스팅 참조 바람
> 
> - <a href="#/post/3d0eda9b-0fe1-8026-a8aa-eeeda1bd3e22">페이지</a> 

<a id="3d0eda9b0fe180c58ecad96b00f34fe1"></a>

```go
type Point struct {
	X, Y int
}

a := Point{X: 1, Y: 2}    // 값 생성
b := &Point{X: 1, Y: 2}   // 포인터 생성

fmt.Println(a)              // {1 2}
fmt.Println(b)              // &{1 2}
fmt.Printf("%p\n", b)       // 0xc0000140a0  ← 실제 메모리 주소
```

- <code>&#38;</code> 는 <strong><u>해당 값의 주소를 할당</u></strong>하는 연산자이다&#46;

- 즉, <code>&#38;Point{&#46;&#46;&#46;}</code>는 <code>Point</code> 값을 하나 만들고, 그 값이 저장된 메모리 주소를 즉시 취하는 표현식이다&#46;

<a id="3d0eda9b0fe180d7b0e2d64fcabc94f5"></a>

##  &#91;이유 1&#93; 복사 비용 회피

<a id="3d0eda9b0fe180cba693eec460c6534c"></a>

```go
type BigStruct struct {
	Data [1000]int // 8000바이트
}

// Case 1) 값으로 받음 → 호출 시 8000바이트 전체 복사
func processValue(b BigStruct) {    
	b.Data[0] = 999
}

// Case 2) 포인터로 받음 → 호출 시 주소값(8바이트)만 복사
func processPointer(b *BigStruct) { 
	b.Data[0] = 999
}
```

<a id="3d0eda9b0fe180c4a460c5392356ea5c"></a>

위 예제의 <code>Case 1</code>과 같아 값 타입을 함수에 넘기면 <strong><u>구조체 전체가 그대로 복사</u></strong>된다&#46;

<a id="3d0eda9b0fe180c5acf0d3aaadf6f5f4"></a>

```go
// Case 1) processValue(big) 호출 시
┌───────────────────┐   복사(8000B)   ┌───────────────────┐
│ big [1000]int     │ ─────────────> │ processValue의 b   │
└───────────────────┘                └───────────────────┘

// Case 2) processPointer(&big) 호출 시
┌───────────────────┐                ┌───────────────────┐
│ big [1000]int     │ <───────────── │ 주소값(8B)만 전달    │
└───────────────────┘     가리킴       └───────────────────┘
```

<a id="3d0eda9b0fe18075b0c5f61998dc9907"></a>

<code>Case 1</code>의 경우, 구조체가 작으면 복사 비용은 무시할 수 있다&#46;  

<a id="3d0eda9b0fe180dea6becc275433f6b1"></a>

그러나 서비스/유즈케이스 계층처럼 필드가 계속 늘어나는 구조체를 함수 인자로 계속 주고받으면 복사 비용이 누적된다&#46; 

<a id="3d0eda9b0fe180b5ac62e9949c953b8c"></a>

<code>Case 2</code> 같이 <strong><u>포인터</u></strong>를 쓰면 <strong><u>구조체 크기와 무관하게 항상 </u></strong><strong><u>8바이트</u></strong>만 오간다&#46;

<a id="3d0eda9b0fe1806692c2ff17545b5fc2"></a>

##  &#91;이유 2&#93; 인스턴스 공유 (값 타입 사용 시 생기는 버그)

<a id="3d0eda9b0fe180249adacbb1fdea98bd"></a>

<a href="https://go.dev/play/">Go Playground에서 직접 실행해보기</a>

[Go Playground &#45; The Go Programming Language]()

<a id="3d0eda9b0fe1801c8d9bd560c4ebe889"></a>

이게 실무에서 더 중요한 이유다&#46; 직접 버그를 재현해보자&#46;

<a id="3d0eda9b0fe180b18757c75b789ee58a"></a>

### &#91;🤬 오류&#93; 값 타입 선언

<a id="3d0eda9b0fe1807fa2f5c63c6bb3e992"></a>

```go
package main

import "fmt"

type UserUsecase struct {
	JWTSecret string
}

type UserHandler struct {
	UserUsecase UserUsecase // 일부러 값 타입으로 선언
}

func NewUserUsecase(secret string) UserUsecase { // 값 타입 리턴
	return UserUsecase{JWTSecret: secret}
}

func main() {
	uc := NewUserUsecase("old-secret")

	handlerA := &UserHandler{UserUsecase: uc} // uc가 복사되어 들어감
	handlerB := &UserHandler{UserUsecase: uc} // uc가 또 복사되어 들어감

	// 시크릿 로테이션 로직이 있다고 가정
	handlerA.UserUsecase.JWTSecret = "new-secret"

	fmt.Println(handlerA.UserUsecase.JWTSecret) // new-secret
	fmt.Println(handlerB.UserUsecase.JWTSecret) // old-secret, 버그
}
```

<a id="3d0eda9b0fe180658edad6bcb3b667fb"></a>

<code>handlerA</code>와 <code>handlerB</code>는 <code>uc</code>를 &#34;복사&#34;해서 <strong><u>각자 독립된 사본을 갖</u></strong>는다&#46; 그래서 한쪽 값을 바꿔도 다른 쪽엔 반영되지 않는다&#46;

<a id="3d0eda9b0fe1800e9a67f008cf3f7d25"></a>

```go
uc := NewUserUsecase("old-secret")

┌───────────────┐
│  old-secret   │
└───────────────┘


handlerA := &UserHandler{UserUsecase: uc}   // 복사

┌────────────────┐   복사    ┌──────────────────────┐
│ uc: old-secret │ ───────> │ handlerA.UserUsecase │ (별개의 사본)
└────────────────┘          └──────────────────────┘


handlerB := &UserHandler{UserUsecase: uc}   // 또 복사

┌────────────────┐    복사    ┌──────────────────────┐
│ uc: old-secret │ ────────> │ handlerB.UserUsecase │ (또다른 별개 사본)
└────────────────┘           └──────────────────────┘
```

<a id="3d0eda9b0fe1806bb06bdb6d0389811d"></a>

### &#91;✅ 성공&#93; 포인터로 수정

<a id="3d0eda9b0fe18004a426c4e080f24e20"></a>

```go
 ...

type UserHandler struct {
	UserUsecase *UserUsecase // 포인터로 보관
}

func NewUserUsecase(secret string) *UserUsecase { // 포인터 리턴
	return &UserUsecase{JWTSecret: secret}
}

func main() {
	uc := NewUserUsecase("old-secret")

	handlerA := &UserHandler{UserUsecase: uc}
	handlerB := &UserHandler{UserUsecase: uc}

	handlerA.UserUsecase.JWTSecret = "new-secret"

	fmt.Println(handlerA.UserUsecase.JWTSecret) // new-secret
	fmt.Println(handlerB.UserUsecase.JWTSecret) // new-secret, 정상 반영
}
```

<a id="3d0eda9b0fe180f8a04ef1cabdf1d60f"></a>

```go
uc := NewUserUsecase("old-secret")

                  ┌───────────────────┐
uc(주소) ────────> │  실제 UserUsecase  │
                  │    old-secret     │
                  └───────────────────┘
                            ▲
handlerA.UserUsecase ───────┤ (같은 곳을 가리킴)
handlerB.UserUsecase ───────┘ (같은 곳을 가리킴)
```

<a id="3d0eda9b0fe1805fb74fffddaed085b2"></a>

```go
handlerA.UserUsecase.JWTSecret = "new-secret"

                  ┌───────────────────┐
                  │  실제 UserUsecase  │  ← 이 "하나의 실체"가 바뀜
                  │     new-secret    │
                  └───────────────────┘
                            ▲
                            ∣
handlerA, handlerB 모두 같은 곳을 보므로 둘 다 반영됨
```

<a id="3d0eda9b0fe1801095dcd935b81adbd6"></a>

값 타입은 대입할 때마다 복사본이 새로 생기지만, 포인터는 대입해도 &#34;원본을 가리키는 화살표&#34;만 늘어날 뿐 원본은 하나다&#46; 

<a id="3d0eda9b0fe180eea2cac0f17bc3dc42"></a>

DB 커넥션, 설정값, 캐시처럼 애플리케이션 전체에서 하나만 존재해야 하는 컴포넌트를 다룰 때 포인터를 쓰는 이유가 여기에 있다&#46;

<a id="3d0eda9b0fe1802dbe94d6d572c5ffda"></a>

##  &#91;이유 3&#93; Go 커뮤니티 관례

<a id="3d0eda9b0fe1803695cfc547b54bc45c"></a>

표준 라이브러리만 봐도 <code>NewXxx</code> 함수는 거의 예외 없이 포인터를 리턴한다&#46;

<a id="3d0eda9b0fe180699a51e8013cf6685c"></a>

```go
func NewReader(r io.Reader) *bufio.Reader
func NewWriter(w io.Writer) *bufio.Writer
func NewServeMux() *http.ServeMux
```

<a id="3d0eda9b0fe180148c94d01b2dd0ff86"></a>

이게 관례로 굳어진 이유는 결국 위 두 이유가 대부분의 실무 상황에서 함께 성립하기 때문이다&#46; 

- 서비스/유즈케이스/핸들러 같은 컴포넌트는 필드가 많아지는 경향이 있다 &#45; <code>복사 비용 ↑</code>

- 동시에 애플리케이션 전체에서 하나만 만들어 여러 곳에 공유하는 게 자연스럽다 &#45; <code>공유 필요성 ↑</code>

<a id="3d0eda9b0fe1807c8a24f09a7f3efba6"></a>

따라서 ‘생성자는 포인터를 리턴한다’가  Go의 기본 스타일로 자리 잡았다&#46;

<a id="3d0eda9b0fe180c0b206f626dffda2cd"></a>

##  정리 — 언제 <code>값</code>, <code>포인터</code>를 사용하는가

| 상황 | 선택 |
| --- | --- |
| 여러 곳에서 상태를 공유해야 함 (서비스, 유즈케이스, 핸들러) | <code>포인터</code> |
| 작고 불변에 가까운 데이터 (좌표, 설정 스냅샷) | <code>값</code> |
| 구조체가 크고 자주 전달됨 | <code>포인터</code> |
| <code>nil</code>로 &#34;값 없음&#34;을 표현해야 함 | <code>포인터</code> |

<a id="3d0eda9b0fe18058a024c488f470336a"></a>

<code>&#38;Type{&#46;&#46;&#46;}</code>은 단순한 문법이 아니라, &#34;이 객체를 여러 곳에서 하나의 실체로 공유하겠다&#34;는 설계 의도를 코드로 드러내는 방법이다&#46;
