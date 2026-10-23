---
order: 3
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 3d0eda9b-0fe1-8072-a39d-f8fb0b030547
title: export 규칙과 패키지 경계 (부제. 접근 제어자)
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-805b-a5ac-c76c9ecfc302
    title: Golang
  - id: 3d0eda9b-0fe1-8029-b3f2-dd8560b1d377
    title: Go 의문점 정리
  - id: 3d0eda9b-0fe1-8072-a39d-f8fb0b030547
    title: export 규칙과 패키지 경계 (부제. 접근 제어자)
excerpt: "목차 - export 규칙과 패키지 경계 - Go의 대소문자 하나가 컴파일 에러를 가르는 이유 - 들어가며 - [ [설명 1] public / private 키워드 ❌ → 대/소문자를 통한 접근 제어](3d0eda9b0fe180e0a951fde924a59f82) - [ [설명 2] 예제: 설정값을 다루는 config 패키"
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 3d0eda9b-0fe1-8029-b3f2-dd8560b1d377
created: 2026-09-03T05:51:22.301Z
updated: 2026-09-03T07:31:35.288Z
legacy_path: Main/Golang-c76c9ecfc302/Go 의문점 정리-dd8560b1d377/export 규칙과 패키지 경계 (부제. 접근 제어자)-f8fb0b030547/index.md
legacy_category: Golang
source_url: https://beautiful-college-c84.notion.site/3d0eda9b0fe18072a39df8fb0b030547
---
> 
> 
> <a id="3d0eda9b0fe180f6843ee4332233efd1"></a>
> 
> <strong>목차</strong>
> 
> - [export 규칙과 패키지 경계 - Go의 대소문자 하나가 컴파일 에러를 가르는 이유](#3d0eda9b0fe1802991aafed3a8839647)
> - [ 들어가며](#3d0eda9b0fe1805aafa2e46906daf1ec)
> - [ [설명 1] public / private 키워드 ❌ → 대/소문자를 통한 접근 제어](#3d0eda9b0fe180e0a951fde924a59f82)
> - [ [설명 2] 예제: 설정값을 다루는 config 패키지](#3d0eda9b0fe1801881f7cfedc839f679)
> - [ [설명 3] 다른 패키지에서 접근](#3d0eda9b0fe18094b88cd9116f54630e)
> - [ [설명 4] 같은 패키지 안은 가능](#3d0eda9b0fe18038a5f5dac81d43a10b)
> - [ [설명 5] 해당 규칙의 의미 ](#3d0eda9b0fe180dcbb85f25bc93a90e3)
> - [ 1. 패키지가 곧 캡슐화의 단위다. ](#3d0eda9b0fe18053a35cc98a2191ec9d)
> - [ 2. NewXxx() 생성자 패턴이 자주 쓰이는 이유이기도 하다. ](#3d0eda9b0fe180409a5fe6bba0471348)
> - [ 3. 테스트 코드에도 영향을 준다.](#3d0eda9b0fe180eeacead86562c4518f)

<a id="3d0eda9b0fe1802991aafed3a8839647"></a>

# <strong>export 규칙과 패키지 경계 &#45; Go의 </strong><strong><u>대소문자 하나</u></strong><strong>가 컴파일 에러를 가르는 이유</strong>

---

<a id="3d0eda9b0fe1805aafa2e46906daf1ec"></a>

##  들어가며

<a id="3d0eda9b0fe180aa844afa0b88d3ba0b"></a>

Go로 여러 패키지에 걸친 코드를 작성하다 보면 다음과 같은 컴파일 에러를 한 번쯤 마주치게 된다&#46;

<a id="3d0eda9b0fe180db96fbc85a0c1bd0a1"></a>

```plaintext
unknown field 'maxRetries' in struct literal of type config.Options
```

<a id="3d0eda9b0fe1802892ebf2bee53d4184"></a>

분명 구조체에 존재하는 필드인데 왜 <strong>&#34;unknown field&#34;</strong>라고 나오는가? 

<a id="3d0eda9b0fe180029608e96ee5a186b3"></a>

이 글에서는 <strong><u>Go의 접근 제어 규칙</u></strong>과, <strong><u>그 규칙이 구조체 리터럴 작성 시 어떻게 작동</u></strong>하는지를 정리한다&#46;

<a id="3d0eda9b0fe180e0a951fde924a59f82"></a>

##  &#91;설명 1&#93; <code>public</code> / <code>private</code> 키워드 ❌ → 대/소문자를 통한 접근 제어

<a id="3d0eda9b0fe1806e864cc75100f84df6"></a>

Java, C&#35;, TypeScript 등 대부분의 언어는 <code>public</code>, <code>private</code>, <code>protected</code> 같은 키워드로 접근 범위를 명시한다&#46; 

<a id="3d0eda9b0fe1807bb477f796878cae94"></a>

Go에는 이런 <strong>키워드를 사용하지 않</strong>는다&#46; 대신 아주 단순한 규칙 하나로 접근 범위를 결정한다&#46;

> ✏️ 
> 
> <a id="3d0eda9b0fe180639a6df0ea22112ad3"></a>
> 
> <strong>식별자(변수, 함수, 타입, 구조체 필드 등) 이름이</strong>
> 
> - <strong><u>대문자</u></strong><strong>로 시작 → </strong><strong><code>exported</code></strong><strong>, </strong>다른 패키지에서도 접근 가능<br><strong><u>M</u></strong>axRetries
> 
> - <strong><u>소문자</u></strong><strong>로 시작 →  </strong><strong><code>unexported</code></strong><strong>, </strong>선언된 패키지 내부에서만 접근 가능

<a id="3d0eda9b0fe1801c9c32d795f956e11b"></a>

이 규칙은 구조체 필드뿐 아니라 함수, 메서드, 타입, 상수, 변수 등 Go의 모든 최상위 식별자에 동일하게 적용된다&#46;

<details>
<summary>ex)</summary>

<a id="3d0eda9b0fe180a38c9ec4a6a4336db1"></a>

```go
// 대문자 시작 -> exported, 다른 패키지에서도 접근 가능
MaxRetries

// 소문자 시작 -> unexported, 선언된 패키지 내부에서만 접근 가능
maxRetries
```

</details>

<a id="3d0eda9b0fe1801881f7cfedc839f679"></a>

##  &#91;설명 2&#93; 예제&#58; 설정값을 다루는 <code>config</code> 패키지

<a id="3d0eda9b0fe18011aabae3ce4d8fd62c"></a>

아래와 같은 <code>config</code> 패키지가 있다고 하자&#46;

<a id="3d0eda9b0fe18046899be91032813777"></a>

```go
package config

type Options struct {
    Endpoint   string // exported
    Timeout    int    // exported
    maxRetries int    // unexported: 내부적으로만 관리하고 싶은 값
}

func NewOptions(endpoint string, timeout int) Options {
    return Options{
        Endpoint:   endpoint,
        Timeout:    timeout,
        maxRetries: 3, // 패키지 내부에서는 기본값을 자유롭게 설정
    }
}
```

<a id="3d0eda9b0fe18016834ef67cac8f1347"></a>

<code>maxRetries</code>는 소문자로 시작하므로 unexported다&#46; 이 필드는 &#34;외부에서 마음대로 건드리지 말고, 패키지 내부의 기본 정책(<code>NewOptions</code>)을 통해서만 설정되게 하고 싶다&#34;는 의도로 설계된 것이다&#46;

<a id="3d0eda9b0fe18094b88cd9116f54630e"></a>

##  &#91;설명 3&#93; 다른 패키지에서 접근

<a id="3d0eda9b0fe1808cbd3ace884dfb1117"></a>

이 패키지를 가져다 쓰는 <code>main</code> 패키지에서 composite literal로 값을 만들어보자&#46;

<a id="3d0eda9b0fe1806b807fe99be5af158a"></a>

```go
package main

import "myapp/config"

func main() {
    opt := config.Options{
        Endpoint: "https://api.example.com",
        Timeout:  30,
        // maxRetries: 5, // 컴파일 에러!
        // unknown field 'maxRetries' in struct literal of type config.Options
    }
    _ = opt
}
```

<a id="3d0eda9b0fe180e2bb4ac4882c6aedc7"></a>

<code>maxRetries</code>를 채우려는 줄의 주석을 풀면 컴파일이 실패한다&#46; 

<a id="3d0eda9b0fe18016b94ed69119adc3b1"></a>

<code>config</code> 패키지 바깥에서는 <code>maxRetries</code>라는 필드가 애초에 &#34;보이지 않는&#34; 것처럼 취급되기 때문이다&#46; 

<a id="3d0eda9b0fe180499eeefafb1adcce99"></a>

<code>Endpoint</code>, <code>Timeout</code>처럼 대문자로 시작하는 필드만 리터럴에 채울 수 있다&#46;

<a id="3d0eda9b0fe180ef83dee3eaa759f819"></a>

이건 composite literal에만 적용되는 특별 규칙이 아니라, <code>opt&#46;maxRetries</code>처럼 필드에 직접 접근하려는 시도에도 동일하게 적용된다&#46;

<a id="3d0eda9b0fe1809d8e91f476b634c859"></a>

```go
fmt.Println(opt.maxRetries) // 컴파일 에러: opt.maxRetries undefined
```

<a id="3d0eda9b0fe18038a5f5dac81d43a10b"></a>

##  &#91;설명 4&#93; 같은 패키지 안은 가능

<a id="3d0eda9b0fe180099107d60dee8a20cc"></a>

반대로, <code>config</code> 패키지 <strong>내부</strong>에 있는 코드라면 unexported 필드도 아무 제약 없이 다룰 수 있다&#46;

<a id="3d0eda9b0fe18029b923dc5e7d8e3c6b"></a>

```go
package config

func Debug(o Options) string {
    // 같은 패키지이므로 maxRetries에 자유롭게 접근 가능
    return fmt.Sprintf("endpoint=%s timeout=%d retries=%d",
        o.Endpoint, o.Timeout, o.maxRetries)
}

func WithMaxRetries(o Options, n int) Options {
    o.maxRetries = n // 같은 패키지이므로 수정도 가능
    return o
}
```

<a id="3d0eda9b0fe180709e2ce93c048bc7bb"></a>

즉 <em><strong><u>Go의 접근 제어</u></strong></em><em><strong>는 &#34;타입 단위&#34;가 아니라 </strong></em><em><strong><u>&#34;패키지 단위&#34;</u></strong></em><em><u>로 작동 </u></em>한다&#46; 

<a id="3d0eda9b0fe1800d8663ea75031fc2a7"></a>

같은 패키지 안에 있는 코드끼리는 서로 다른 파일에 있어도, 심지어 서로 다른 타입에 속해 있어도 unexported 식별자를 자유롭게 주고받을 수 있다&#46; 

<a id="3d0eda9b0fe180c39447d736392814a2"></a>

반대로 패키지 경계를 넘는 순간, 소문자로 시작하는 모든 것은 접근 불가능한 영역이 된다&#46;

<a id="3d0eda9b0fe180dcbb85f25bc93a90e3"></a>

##  &#91;설명 5&#93; 해당 규칙의 의미 

<a id="3d0eda9b0fe18053a35cc98a2191ec9d"></a>

#### <strong> 1&#46; 패키지가 곧 캡슐화의 단위다&#46;</strong> 

<a id="3d0eda9b0fe180bc9b72df4bbd004575"></a>

클래스나 구조체 단위로 <code>private</code>을 지정하는 언어와 달리, Go는 &#34;이 패키지 밖으로는 내보내지 않겠다&#34;는 설계를 강제한다&#46; 

<a id="3d0eda9b0fe18014b3dafc86eeb7c77c"></a>

그래서 패키지를 어떻게 나누느냐가 곧 캡슐화 설계 그 자체가 된다&#46;

<a id="3d0eda9b0fe180409a5fe6bba0471348"></a>

#### <strong> 2&#46; </strong><strong><code>NewXxx()</code></strong><strong> 생성자 패턴이 자주 쓰이는 이유이기도 하다&#46;</strong> 

<a id="3d0eda9b0fe1808c97e3f29f87f445a1"></a>

위 예제의 <code>NewOptions</code>처럼, 외부에는 필수 필드만 노출하고 내부 정책이 필요한 필드(<code>maxRetries</code> 같은)는 unexported로 감춘 뒤 생성자 함수로만 초기화하게 만드는 패턴이 Go에서 흔한 이유가 여기에 있다&#46; 

<a id="3d0eda9b0fe180ef8dcfd15e7b451ee8"></a>

다만 이건 어디까지나 관례일 뿐, 언어가 생성자를 강제하는 것은 아니다&#46; 

<a id="3d0eda9b0fe180f2a91afafeb7b7c745"></a>

같은 패키지 안이라면 언제든 <code>Options{&#46;&#46;&#46;}</code> 리터럴로 직접 값을 만들 수 있다는 점은 변하지 않는다&#46;

<a id="3d0eda9b0fe180eeacead86562c4518f"></a>

#### <strong> 3&#46; 테스트 코드에도 영향을 준다&#46;</strong>

<a id="3d0eda9b0fe18072b055c7f9d0a01eb3"></a>

테스트 파일이 <code>package config</code>(내부 테스트)로 선언되어 있다면 unexported 필드에 접근할 수 있지만, <code>package config&#95;test</code>(외부 테스트)로 선언되어 있다면 exported 필드만 접근 가능하다&#46; 

<a id="3d0eda9b0fe180b7a94af0ce35811e85"></a>

어떤 접근 수준을 테스트하고 싶은지에 따라 테스트 패키지 선언 방식을 의도적으로 선택하게 된다&#46;

> 📝 
> 
> <a id="3d0eda9b0fe1806e9368e7a0e8098dd5"></a>
> 
> 정리
> 
> - Go는 <code>public</code>/<code>private</code> 키워드 대신 <strong>식별자 첫 글자의 대소문자</strong>로 접근 범위를 결정한다&#46;
> 
> - 이 규칙은 구조체 필드뿐 아니라 함수, 타입, 변수 등 모든 최상위 식별자에 동일하게 적용되며, composite literal로 값을 채울 때도 예외 없이 작동한다&#46;
> 
> - 접근 제어의 단위는 타입이 아니라 <strong>패키지</strong>다&#46; 같은 패키지 안에서는 unexported 식별자도 자유롭게 다룰 수 있고, 패키지 경계를 넘는 순간 접근이 차단된다&#46;
> 
> - 이 특성 때문에 &#34;필수 필드는 exported로 노출하고, 내부 정책이 필요한 필드는 unexported로 감춘 뒤 생성자 함수를 제공&#34;하는 패턴이 Go 생태계에서 자주 쓰인다
> 
> <a id="3d0eda9b0fe1808a80d8f01dba0984b1"></a>
> 
> 대소문자 하나 차이가 &#34;어떤 필드를 API로 노출할지&#34;를 결정짓는다는 점에서, Go의 export 규칙은 문법이라기보다 하나의 설계 철학에 가깝다&#46;
