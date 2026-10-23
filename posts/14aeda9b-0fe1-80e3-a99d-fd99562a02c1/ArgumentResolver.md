---
order: 8
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 14aeda9b-0fe1-80e3-a99d-fd99562a02c1
title: ArgumentResolver
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 149eda9b-0fe1-8010-9b0f-dc35331888ed
    title: "[sparta] 스프링 심화"
  - id: 14aeda9b-0fe1-80e3-a99d-fd99562a02c1
    title: ArgumentResolver
excerpt: RequestMappingHandlerAdapter --- 📖 Spring MVC에서 HTTP 요청을 컨트롤러 메서드에 매핑하고 실행하는 핵심 구성요소이다. - 클라이언트 요청을 적절한 컨트롤러 메서드와 연결한 후, 메서드를 호출하여 결과로 반환하는 역할을 수행한다. Spring MVC 구조 - 요청 데이터 변환 - H
cover: null
icon: null
notionProperties:
  subchapter: |-
    • RequestMappingHandlerAdapter
    • ArgumentResolver**
    • **ReturnValueHandler
  상태: 완료
schema_version: 1
parent_id: 149eda9b-0fe1-8010-9b0f-dc35331888ed
created: 2024-11-26T03:56:55.254Z
updated: 2026-04-04T07:52:01.631Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/[sparta] 스프링 심화-dc35331888ed/ArgumentResolver-fd99562a02c1/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/14aeda9b0fe180e3a99dfd99562a02c1
---
<a id="a1396bf214ff440cb3de0ba7216e5709"></a>

## RequestMappingHandlerAdapter

---

> 📖 
> 
> <a id="c8667011dd8d461cbf8a4d35ce6c227c"></a>
> 
> Spring MVC에서 <strong>HTTP 요청을 컨트롤러 메서드에 매핑하고 실행</strong>하는 핵심 구성요소이다&#46;
> 
> -  <strong><u>클라이언트 요청</u></strong>을 적절한 컨트롤러 메서드와 연결한 후, <strong>메서드를 호출하여 결과로 반환</strong>하는 역할을 수행한다&#46;

<details>
<summary>Spring MVC 구조</summary>

![](f62e10a9ab285cc9.webp)

- 요청 데이터 변환  &#45; <code>HttpMessageConverter</code>

</details>

<details>
<summary><strong><code>RequestMappingHandlerAdapter</code></strong></summary>

> ✏️ 
> 
> <a id="1f1eda9b0fe1809db08afce824352dde"></a>
> 
> <code>&#64;RequestMapping</code> 을 처리하는 <code>HandlerAdapter</code>의 구현체 이다&#46; 
> 
> - 아래 모두 <code>&#64;RequestMapping</code>의 일종이다&#46;
>     - <code>&#64;PostMapping</code>
> 
>     -  <code>&#64;GetMapping</code>
> 
>     - <code>&#64;PutMapping</code>
> 
>     - <code>&#64;PatchMapping</code>
> 
>     - <code>&#64;DeleteMapping</code>

![](89bc81a9d7b32703.webp)

![](bc3e2d1d68a95683.webp)

</details>

<details>
<summary><strong><code>ArgumentResolver</code></strong></summary>

![](0a36f62fbc8fe7fd.webp)

- <code>RequestMappingHandlerAdapter</code>는 <code>ArgumentResolver</code>를 호출하여 Controller가 필요한 다양한 파라미터의 값을 생성한다&#46;
    - 이를 통해 <strong><code>HttpServletRequest</code></strong>, <strong><code>Model</code></strong>, <strong><code>HttpEntity</code></strong>,<strong><code>&#64;ModelAttribute</code></strong>, <strong><code>&#64;RequestBody</code></strong>, <strong><code>&#64;RequestParam</code></strong> 등 <strong><u>다양한 파라미터 바인딩</u></strong>을 할 수 있다&#46;

- <code>ArgumentResolver</code>를 통하여 값이 준비되면 해당값을 가지고 실제 Controller를 호출한다&#46; 

</details>

<a id="14aeda9b0fe18021beb7d29924aa2444"></a>

## <strong>ArgumentResolver</strong>

---

> 📖 
> 
> <a id="ee649857b62d45fdba49a93423d5a8c4"></a>
> 
> Spring MVC에서 <strong>컨트롤러 메서드의 파라미터를 자동으로 바인딩</strong>하는 역할을 하는 <strong>인터페이스</strong>로 <strong><u>컨트롤러 메서드에 전달</u></strong>될 때, <strong><u>각 파라미터를 적절한 객체로 변환하여 주입</u></strong>하는 것을 담당한다&#46;

<details>
<summary>ArgumentResolver 종류</summary>

> ✏️ 
> 
> <a id="1f1eda9b0fe1801a9a41eb5a6556d357"></a>
> 
> 스프링에서 다양한 Argument Resolver들을 기본적으로 제공한다&#46;

1. <code>&#64;RequestBody</code>  → <code>RequestBodyArgumentResolver</code> 
    ![](46367c8bb8257dc2.webp)

1. <code>&#64;RequestHeader</code> &#45;&#62; <code>RequestHeaderArgumentResolver</code>
    ![](a298f164318efd15.webp)

</details>

<details>
<summary><strong><code>HandlerMethodArgumentResolver</code></strong></summary>

![](aa5c02d5fdc7910a.webp)

- <code>ArgumentResolver</code>의 실제 이름
    - 인터페이스 로 구성

    - implements 하여 커스텀하게 파라미터를 만들 수 있다 &#46; ( 확장 가능)

- <code>supportsParameter( MethodParameter parameter );</code>
    - 컨트롤러가 필요로하는 메서드의 파라미터를 지원하는지 여부를 검사

- 지원하다면 <code>resolverArgument()</code> 메서드 통해, Object(객체)로 생성
    - 만들어진 Object(객체)가 Controller 호출시 메서드의 파라미터로 전달된다&#46;

- <code>supportsParameter()</code> 를 사용하는 다양한 <code>ArgumentResolver</code> 구현체
    ![](adf06b60d6899631.webp)

</details>

<details>
<summary>사용 가능한 파라미터 목록  &#45; 공식 문서</summary>

[Method Arguments &#58;&#58; Spring Framework]()

- 사용 가능한 파라미터 목록

</details>

<a id="14aeda9b0fe180e38bbbf8e4ddfde370"></a>

## ReturnValueHandler

---

> 📖 
> 
> <a id="b592c23af63d42bf8dd41b667a0b120e"></a>
> 
> Spring MVC에서<strong> </strong><strong>컨트롤러 메서드가 반환하는 값을 처리하여 HTTP 응답에 맞게 변환하는 역할</strong>을 하는 <strong>인터페이스</strong>로 <strong><u>컨트롤러 메서드가 실행된 후 그 반환값을 HTTP 응답의 본문에 적절히 담아 전송</u></strong>할 수 있도록 도와준다&#46; 

<details>
<summary><strong>ReturnValueHandler</strong></summary>

1. <code>ModelAndView</code>, <code>&#64;ResponseBody</code>, <code>HttpEntity&#60;&#62;</code> 등이 있으면 응답에 필요한 값으로 변환
    - Controller에서 Stirng 으로 <code>ViewName</code>을  반환하여도 View가 동작하는 이유

1. Spring은 다양한 ReturnValueHandler를 기본적으로 제공한다&#46; 
    - ModelAndViewMethodReturnValueHandler( ModelAndView 객체 반환 )
        ![](e38b2b4c1375edf4.webp)

    - HttpEntityMethodProcessor( HttpEntity 객체 변환 )
        ![](7ffc2a733424035b.webp)

</details>

<details>
<summary><strong>HandlerMethodReturnValueHandler</strong></summary>

> <code>ReturnValueHandler</code>의 실제 이름

- 인터페이스로 구성되어 있다&#46; 즉, 확장이 가능하다&#46;
    ![](57206870969d77a3.webp)

- 다양한 ReturnValueHandler 구현체
    ![](2451339a18a7b21c.webp)

</details>
