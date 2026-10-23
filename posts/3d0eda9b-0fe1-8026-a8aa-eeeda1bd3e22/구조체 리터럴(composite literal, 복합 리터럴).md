---
order: 4
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 3d0eda9b-0fe1-8026-a8aa-eeeda1bd3e22
title: 구조체 리터럴(composite literal, 복합 리터럴)
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-805b-a5ac-c76c9ecfc302
    title: Golang
  - id: 3d0eda9b-0fe1-8029-b3f2-dd8560b1d377
    title: Go 의문점 정리
  - id: 3d0eda9b-0fe1-8026-a8aa-eeeda1bd3e22
    title: 구조체 리터럴(composite literal, 복합 리터럴)
excerpt: 목차 - [ [의문점] Go 언어에서의 인스턴스 생성 방법](3d0eda9b0fe1800cb0f5fb49c6aa5958) - [ [설명 1] new를 사용하지 않고 생성되는 인스턴스 ](3d0eda9b0fe1803c8bd6ec68bc9c0cbf) - [ [설명 2] composite literal(복합 리터럴) ](3d0
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 3d0eda9b-0fe1-8029-b3f2-dd8560b1d377
created: 2026-09-03T04:49:59.639Z
updated: 2026-09-03T07:31:24.974Z
legacy_path: Main/Golang-c76c9ecfc302/Go 의문점 정리-dd8560b1d377/구조체 리터럴(composite literal, 복합 리터럴)-eeeda1bd3e22/index.md
legacy_category: Golang
source_url: https://beautiful-college-c84.notion.site/3d0eda9b0fe18026a8aaeeeda1bd3e22
---
> 
> 
> <a id="3d0eda9b0fe1809e8efeedf23cb56369"></a>
> 
> <strong>목차</strong>
> 
> - [ [의문점] Go 언어에서의 인스턴스 생성 방법](#3d0eda9b0fe1800cb0f5fb49c6aa5958)
> - [ [설명 1] new를 사용하지 않고 생성되는 인스턴스 ](#3d0eda9b0fe1803c8bd6ec68bc9c0cbf)
> - [ [설명 2]  composite literal(복합 리터럴) ](#3d0eda9b0fe180ad83fcd5e3e522c2d1)
> - [[번외] 필드명 지정 vs 순서 지정](#3d0eda9b0fe180a2af1acc252b714776)
> - [&Type{...}의 의미](#3d0eda9b0fe1802d91ede04166bc2fda)
> - [ [해답]](#3d0eda9b0fe180ce8f02d032ce732dd5)

<a id="3d0eda9b0fe1800cb0f5fb49c6aa5958"></a>

##  &#91;의문점&#93; Go 언어에서의 인스턴스 생성 방법

---

> 
> 
> <a id="3d0eda9b0fe1809c809fee65622c3c8c"></a>
> 
> 해당 문서는 아래 문서 정리 중 해당 예제에서 의문점이 생겨 추가 정리한다&#46; 
> 
> - <a href="#/post/3d0eda9b-0fe1-80ce-b73a-ff32d5bae76e">페이지</a> 

<a id="3d0eda9b0fe1802dab1af49402fde1f6"></a>

```go
package main

import "fmt"

type UserUsecase struct {
    JWTSecret string
}

type UserHandler struct {
    UserUsecase UserUsecase // 일부러 값 타입으로 선언
}

func NewUserUsecase(secret string) UserUsecase {
    return UserUsecase{JWTSecret: secret}
}

func main() {
    uc := NewUserUsecase("old-secret")

    handlerA := &UserHandler{UserUsecase: uc} // uc가 복사되어 들어감
    handlerB := &UserHandler{UserUsecase: uc} // uc가 또 복사되어 들어감

    // 시크릿 로테이션 로직이 있다고 가정
    handlerA.UserUsecase.JWTSecret = "new-secret"

    fmt.Println(handlerA.UserUsecase.JWTSecret) // new-secret
    fmt.Println(handlerB.UserUsecase.JWTSecret) // old-secret ← 버그!
}
```

<a id="3d0eda9b0fe180efae93c1f857dd87d6"></a>

위 Go 예제 코드에서는 생성자에 대한 정의가 없는데 <code>UserHandler</code> 인스턴스가 생성된다&#46;

<a id="3d0eda9b0fe1803c88b9e6688d403e5c"></a>

이에 대해 의문점이 해당 글을 정리한다&#46; 

> 🤔 
> 
> <a id="3d0eda9b0fe1804db6cfcc9dc6b23395"></a>
> 
> <strong>의문점</strong>
> 
> - [ ] 생성자 정의도 없는데 <code>&#38;UserHandler{&#46;&#46;&#46;}</code>는 어떻게 동작하는가?

<a id="3d0eda9b0fe1803c8bd6ec68bc9c0cbf"></a>

##  &#91;설명 1&#93; <code>new</code>를 사용하지 않고 생성되는 인스턴스 

---

<a id="3d0eda9b0fe18001afcbcde6426ff998"></a>

Go에도 <code>new</code>라는 built&#45;in 함수가 있다&#46;

<a id="3d0eda9b0fe180199345f9ad63c7cf46"></a>

```go
h := new(UserHandler) // *UserHandler, 모든 필드가 zero value
```

- <code>new(T)</code>는 <strong><u>해당 타입의 zero value를 할당하고 그 포인터를 반환</u></strong>한다&#46;

- 또한Java/C&#43;&#43;의 생성자처럼 &#34;이 타입은 반드시 이런 초기화 로직을 거쳐야 한다&#34;는 걸 강제하지 않는다&#46; 

- <code>new(UserHandler)</code>를 호출해도 <code>JWTSecret</code>에 초기값 할당 없이 빈 구조체의 포인터만 반환된다&#46;  즉, <code>new</code>는 메모리 공간에 해당 구조체를 초기화만 하며 초기값 할당까지는 이뤄지지 않는다&#46; 

<a id="3d0eda9b0fe18049b688d10e2d93e0cc"></a>

```go
handlerA := &UserHandler{UserUsecase: uc}
```

<a id="3d0eda9b0fe18039b266db61bb434a83"></a>

그런데 <code>UserHandler</code>코드를 다시 보면 <strong><u>생성 헬퍼 함수도 없</u></strong>으며  <strong><u><code>new</code></u></strong><strong><u> 키워드 또한 사용하지 않</u></strong>는다&#46; 

- <code>UserUsecase</code>에는 <code>NewUserUsecase</code>라는 헬퍼 함수가 정의되어 있는 반면 <code>UserHandler</code>에는 그런 함수가 전혀 없다&#46;

<a id="3d0eda9b0fe180f78917cc989028fa0b"></a>

그렇다면 어떻게 위 한 줄만으로 <strong><u>🧐 필드 값이 채워진 </u></strong><strong><u><code>&#42;UserHandler</code></u></strong><strong><u> 인스턴스</u></strong>가 만들어 질 수 있는가?

<a id="3d0eda9b0fe180ad83fcd5e3e522c2d1"></a>

##  &#91;설명 2&#93;  <strong>composite literal(복합 리터럴)</strong> 

---

<a id="3d0eda9b0fe1801493c6e028e229ade1"></a>

<code>&#38;UserHandler{UserUsecase&#58; uc}</code> 같은 문법을 <strong><u>composite literal(복합 리터럴)</u></strong> 이라고 부른다&#46; 

<a id="3d0eda9b0fe18015a3ebc730a405cc51"></a>

이는함수 호출이 아닌 <strong><u>타입 &#43; {}</u></strong> 조합으로 <strong><u>값을 즉석에서 만드는 Go 고유의 문법</u></strong>이다&#46;

<a id="3d0eda9b0fe1801c88a2fc109d40d9b3"></a>

```go
type Point struct {
    X, Y int
}

p := Point{X: 1, Y: 2} // composite literal
```

<a id="3d0eda9b0fe180bf8db8c175a0bd1983"></a>

<code>&#34;hello&#34;</code>가 <strong><u>string 리터럴</u></strong>이듯, <code>Point{X&#58; 1, Y&#58; 2}</code>는 <strong><u>struct 리터럴</u></strong>이다&#46; 

<a id="3d0eda9b0fe1804c99bdfca35c795435"></a>

<strong><u>컴파일러가 타입 정보를 보고 그 자리에서 메모리에 값을 채워 넣는 방식</u></strong>이다&#46;

<a id="3d0eda9b0fe18051bee2cc5c7faf1910"></a>

이 문법은 struct 전용이 아니라 <strong><u>배열, 슬라이스, 맵 등 Go의 복합 타입 전반에 동일하게 적용</u></strong>된다&#46;

<a id="3d0eda9b0fe180f0967de36158391cbf"></a>

```go
arr := [3]int{1, 2, 3}
slice := []int{1, 2, 3}
m := map[string]int{"a": 1, "b": 2}
```

<a id="3d0eda9b0fe180a2af1acc252b714776"></a>

### &#91;번외&#93; 필드명 지정 vs 순서 지정

<a id="3d0eda9b0fe180728075e9d4470c7ef8"></a>

```go
// 필드명 지정 (권장)
p := Point{X: 1, Y: 2}

// 선언 순서대로 (필드명 생략)
p := Point{1, 2}
```

<a id="3d0eda9b0fe1804eb99be251d228344c"></a>

생성 방식에서 인자 변수명을 무시하고 선언 순서대로 할당 가능하다&#46; ( 순서지정 방식 )

<a id="3d0eda9b0fe1801c9733c019f0a91b90"></a>

그러나  순서 지정 방식은 구조체 필드 순서가 바뀌면 코드가 깨지고, 필드를 하나라도 생략할 수 없다&#46; 

<a id="3d0eda9b0fe18009b080e82743b0aca0"></a>

반면 <strong><u>필드명 지정 방식</u></strong>은 <strong>원하는 필드만 채우고 나머지는 zero value로 남</strong>겨둘 수 있어 <strong><u>더 안전</u></strong>하다&#46;

<a id="3d0eda9b0fe180969ba9e2f4f9219452"></a>

```go
type Config struct {
    Host string
    Port int
    TLS  bool
}

c := Config{Host: "localhost"} // Port: 0, TLS: false로 자동 채워짐
```

<a id="3d0eda9b0fe1802d91ede04166bc2fda"></a>

### <code>&#38;Type{&#46;&#46;&#46;}</code>의 의미

<a id="3d0eda9b0fe180c5a42fedc438aa89f8"></a>

<code>&#38;</code>가 붙으면 <em><u>&#34;해당 리터럴로 만든 값의 주소 반환한다&#34;</u></em><em> </em>는 뜻이다&#46; 

<a id="3d0eda9b0fe180f1bceec1b196e939a8"></a>

Go는 값을 임시 변수에 담았다가 주소를 취하는 과정을 언어 차원에서 자동 처리해주므로, 별도로 변수를 선언하고 <code>&#38;변수</code>를 할 필요가 없다&#46;

<a id="3d0eda9b0fe180ce8f02d032ce732dd5"></a>

##  &#91;해답&#93;

<a id="3d0eda9b0fe1803080d9e823c9d5bbc2"></a>

이제 의문점에 해서 답할 수 있게 되었다&#46;

<a id="3d0eda9b0fe180da8740df0dd3236049"></a>

```go
handlerA := &UserHandler{UserUsecase: uc}
```

<a id="3d0eda9b0fe1803cb047cdaea0a7aa69"></a>

위 코드가 <code>new</code>도 안 쓰고 <code>NewUserHandler</code> 같은 생성 헬퍼 함수도 없이 동작했던 이유는, <strong><u>composite literal 문법</u></strong><strong> 때문이었으며, </strong>이는 Go에서 제공되는 값을 만드는 고유한 기본 문법이다&#46;

<a id="3d0eda9b0fe180f397e2dbeb3e634800"></a>

Go에는 Java, C 와 달리&#34;이 타입은 반드시 이 생성 경로를 거쳐야 한다&#34;를 강제하는 언어 차원의 장치가 없다&#46; 

<a id="3d0eda9b0fe18072b024cd302ff989cd"></a>

<code>new()</code>는 제로값 할당 이상의 역할을 못 하고, 결국 원하는 <strong>초기값으로 인스턴스를 만드는 실질적인 방법은 composite literal</strong>이다&#46; 

<a id="3d0eda9b0fe180ae82cadab63257d299"></a>

코드에 있는 <code>NewUserUsecase</code> 함수도 언어가 강제한 게 아니라 이 composite literal을 감싸서 재사용 가능하게 만든 관례일 뿐이며, 그래서 <code>UserHandler</code>에는 이런 헬퍼 함수가 아예 없어도 <code>&#38;UserHandler{&#46;&#46;&#46;}</code>로 바로 인스턴스를 만들 수 있었던 것이다&#46;

> 📝 
> 
> <a id="3d0eda9b0fe1801abab7c6ce4412283c"></a>
> 
> 정리
> 
> - Go의 <code>&#38;Type{&#46;&#46;&#46;}</code> 문법은 생성자 함수가 아니라 언어 차원에서 제공하는 <strong>composite literal</strong>이다&#46;
> 
> - composite literal로 필드를 채울 때 <strong>값 타입은 항상 복사</strong>된다는 점을 놓치면, <br>여러 인스턴스가 &#34;같은 걸 참조하고 있다&#34;고 착각하기 쉽다&#46;
> 
> - 상태를 공유해야 하는 의존성(예&#58; 시크릿 로테이션이 필요한 유스케이스, 커넥션 풀, 캐시 등)은 값 타입이 아니라 <strong>포인터 타입</strong>으로 주입해야 한다&#46;
