---
order: 29
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-817a-accd-e09433b6369d
title: WebMvcConfigurer- CORS
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-812e-b8ac-c13c536efd00
    title: Spring Boot를 활용한 채팅 서비스 만들어보기
  - id: 1c3eda9b-0fe1-817a-accd-e09433b6369d
    title: WebMvcConfigurer- CORS
excerpt: WebMvcConfigurer --- 📖 스프링 프레임워크에서 Spring MVC 앱 설정을 사용자 정의(커스터마이징) 할 수 있도록 도와주는 인터페이스 WebMvcConfigurer - WebMvcConfigurer는 Spring Framework에서 제공하는 인터페이스로, - Spring MVC 앱 설정을 커스터마이
cover: null
icon: null
notionProperties:
  Point: WebMvcConfigurer 사용법 정리 중
  상태: 진행 중
schema_version: 1
parent_id: 1c3eda9b-0fe1-812e-b8ac-c13c536efd00
created: 2025-03-27T07:53:11.123Z
updated: 2025-03-27T07:53:11.123Z
legacy_path: Main/Spring ( Java )-cd1f71740107/Spring Boot를 활용한 채팅 서비스 만들어보기-c13c536efd00/WebMvcConfigurer- CORS-e09433b6369d/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1817aaccde09433b6369d
---
<a id="1c3eda9b0fe181478fb1dc9901cf3fb1"></a>

## WebMvcConfigurer

---

> 📖 
> 
> <a id="1c3eda9b0fe181d28778f6183b20bda9"></a>
> 
> 스프링 프레임워크에서 <strong>Spring MVC 앱</strong> 설정을 사용자 정의(커스터마이징) 할 수 있도록 도와주는 인터페이스

<details>
<summary>WebMvcConfigurer</summary>

- WebMvcConfigurer는 Spring Framework에서 제공하는 인터페이스로,

- <strong><u>Spring MVC 앱 설정을 커스터마이징 </u></strong>할 수 있도록 도와준다&#46; 

- 이를 통해 불필요한 보일러플레이트 코드를 작성하거나 특정 프레임워크 클래스를 확장하지 않고도 추가적인 설정을 구현할 수 있다&#46;

- 특히, Spring Boot의 기본 설정이나 <code>&#64;EnableWebMvc</code>로 제공되는 기본 동작 외에 추가 구성이 필요할 때 유용하다&#46;

</details>

<details>
<summary>주요 기능 </summary>

<details>
<summary> Spring MVC 설정 커스터마이징</summary>

- WebMvcConfigurer를 사용하면 <code>&#64;EnabeWebMvc</code>가 제공하는 기본 설정을 재정의하거나,

- 인터셉터, 뷰 리졸버(View Resolver), 정적 리소스 핸들러 등과 같은 MVC 컴포넌트를 커스터마이징할 수 있다&#46; 

- 기본 설정을 유지하면서 특정 부분만 변경 및 추가 설정 가능하다&#46;

</details>

<details>
<summary>디폴트 메서드</summary>

- Java 8의 디폴트 메서드 기능을 활용하여, 필요한 메서드만 선택적으로 재정의

</details>

</details>

<details>
<summary>사용법</summary>

- <code>configurePathMatch(PathMatchConfigurer configurer)</code>
    - URL 경로 매칭 옵션을 설정 

</details>

> ☝🏻 
> 
> <a id="1c3eda9b0fe181d48b52fbac4889a0c4"></a>
> 
> 기본 값을 변경 시, 유지보수 측면이 늘어난다, 따라서 웬만해서는 기본 설정을 사용하는 것이 좋다&#46; 

<details>
<summary>CORS 설정</summary>

- 프론트 연동 시, 기본적인 CORS 도메인에 대해 설정을 해주어야 한다&#46; 

- 아래와 같은 형태로 거의 모든 서버에서 사용한다&#46; 

- 커스텀하게 설정할 필요가 크게 없다&#46; ( 거의 없다 )

<a id="1c3eda9b0fe181809e98dde37d8a9bac"></a>

```java
@Configuration
public class WebConfig implements WebMvcConfigurer {

    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")  // 모든 경로 허용
                .allowedOriginPatterns("http://localhost:*")
                .allowedMethods("GET", "POST", "PUT", "DELETE")
                .allowedHeaders("*")
                .allowCredentials(true)  // 자격 증명 허용
                .maxAge(3600); // prefligjt 요청 캐시 시간
    }
}
```

</details>
