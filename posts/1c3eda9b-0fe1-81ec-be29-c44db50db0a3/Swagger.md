---
order: 10
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81ec-be29-c44db50db0a3
title: Swagger
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-812e-b8ac-c13c536efd00
    title: Spring Boot를 활용한 채팅 서비스 만들어보기
  - id: 1c3eda9b-0fe1-81ec-be29-c44db50db0a3
    title: Swagger
excerpt: Swagger --- 📖 Swagger는 REST API 문서를 자동 생성하는 도구이다. Java에서는 SpringDoc OpenAPI 또는 SpringFox를 사용하여 Swagger와 통합하는 것이 일반적이다. 🧐 recode 선언 ✏️ record는 주로 DTO(Data Transfer Object), VO(Val
cover: null
icon: null
notionProperties:
  Point: recode, swagger, auth api 기본
  상태: 완료
  Tags: 2. Auth - HTTP Router
schema_version: 1
parent_id: 1c3eda9b-0fe1-812e-b8ac-c13c536efd00
created: 2025-03-27T07:53:11.124Z
updated: 2025-03-27T07:53:11.124Z
legacy_path: Main/Spring ( Java )-cd1f71740107/Spring Boot를 활용한 채팅 서비스 만들어보기-c13c536efd00/Swagger-c44db50db0a3/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181ecbe29c44db50db0a3
---
<a id="1c3eda9b0fe181dc965dd6e59eb8a684"></a>

## Swagger

---

> 📖 
> 
> <a id="1c3eda9b0fe181a1b5a5e37a2e672166"></a>
> 
> Swagger는 REST API 문서를 자동 생성하는 도구이다&#46;  Java에서는 <strong>SpringDoc OpenAPI</strong> 또는 <strong>SpringFox</strong>를 사용하여 Swagger와 통합하는 것이 일반적이다&#46; 

<details>
<summary>🧐 <code>recode</code> 선언</summary>

> ✏️ 
> 
> <a id="1c3eda9b0fe181c9aeb7d5512e3a3c1f"></a>
> 
> <code>record</code>는 주로 <code>DTO(Data Transfer Object)</code>, <code>VO(Value Object)</code> 등을 정의할 때 유용하다&#46;
> 
> - API 요청/응답 모델
> 
> - 이벤트 객체
> 
> - 단순 데이터 전달 구조

<details>
<summary>recode란 무엇인가?</summary>

<a id="1c3eda9b0fe18140aa77fcf7e4aaae54"></a>

record는 <strong><u>Java 14에서 소개된 기능(정식 도입은 Java 16)</u></strong>으로, 

<a id="1c3eda9b0fe1817cad6ae91792171033"></a>

<strong><u>불변 데이터 객체</u></strong><strong><u>를 간결하게 정의</u></strong>하기 위해 사용된다&#46; 

- 데이터를 저장하는 목적의 클래스를 간단하게 정의

- 불변(immutable)한 데이터 구조 제공

<a id="1c3eda9b0fe181aebd50fd786162e2c2"></a>

recode를 사용하면 <strong><u>필요한 필드를 선언</u></strong>하는 것만으로 <strong><u>데이터 객체를 효율적으로 정의</u></strong>할 수 있다&#46; 

</details>

<details>
<summary>recode로 선언 시, 어떠한 장점이 있는가?</summary>

<details>
<summary>간결함</summary>

<details>
<summary>클래스 &#43; final 키워드</summary>

<a id="1c3eda9b0fe181afabbac00f46b915af"></a>

```java
public class CreateUserRequest {
    private final String name;
    private final String password;

    public CreateUserRequest(String name, String password) {
        this.name = name;
        this.password = password;
    }

    public String getName() {
        return name;
    }

    public String getPassword() {
        return password;
    }

    @Override
    public boolean equals(Object o) { ... }

    @Override
    public int hashCode() { ... }

    @Override
    public String toString() { ... }
}
```

</details>

<details>
<summary>recode </summary>

<a id="1c3eda9b0fe1819e81f2c4079a67de63"></a>

```java
public record CreateUserRequest(String name, String password) {}
```

</details>

</details>

<details>
<summary><strong>불변성(Immutable)</strong></summary>

> record로 선언된 객체는 <strong>불변성</strong>을 가지며, <strong><u>필드 값은 생성 이후 변경할 수 없</u></strong>다&#46;

<a id="1c3eda9b0fe181239f0cf4620eddf6df"></a>

```java
public record CreateUserRequest(String name, String password) {}
```

<a id="1c3eda9b0fe181009a04ed3a902182f9"></a>

```java
CreateUserRequest request = new CreateUserRequest("Alice", "securePass");

request.name = "Bob"; // 컴파일 에러: 필드는 변경 불가
```

</details>

<details>
<summary><strong> 자동 메서드 생성</strong></summary>

> 아래의 메서드 자동으로 제공

- <code>getter</code> (필드 이름으로 제공됨)

- <code>equals(Object o)</code>

- <code>hashCode()</code>

- <code>toString()</code>

</details>

</details>

<details>
<summary><code>final</code> 키워드 와의 차이점</summary>

- final 키워드를 사용하는 방식은 <u>더 많은 코드를 요구</u>하며, <u>불변성을 직접 보장</u>해야 한다&#46;

<details>
<summary>ex)  <code>recode</code> vs <code>final</code></summary>

- recode 선언
    <a id="1c3eda9b0fe1818f9f4bcb7ccf3f3d65"></a>

    ```java
    public record CreateUserRequest(String name, String password) {}
    ```

- final 키워드
    <a id="1c3eda9b0fe1810383a4e158d0c98dd0"></a>

    ```java
    public final class CreateUserRequest {
        private final String name;
        private final String password;

        public CreateUserRequest(String name, String password) {
            this.name = name;
            this.password = password;
        }

        public String getName() {
            return name;
        }

        public String getPassword() {
            return password;
        }

        @Override
        public boolean equals(Object o) {
            if (this == o) return true;
            if (o == null || getClass() != o.getClass()) return false;
            CreateUserRequest that = (CreateUserRequest) o;
            return Objects.equals(name, that.name) && Objects.equals(password, that.password);
        }

        @Override
        public int hashCode() {
            return Objects.hash(name, password);
        }

        @Override
        public String toString() {
            return "CreateUserRequest{" +
                    "name='" + name + '\'' +
                    ", password='" + password + '\'' +
                    '}';
        }
    }
    ```

</details>

</details>

</details>

<details>
<summary>Swagger 의존성 추가 </summary>

<a id="1c3eda9b0fe181b6aeb9e21e61344006"></a>

```groovy
dependencies {
    implementation 'org.springdoc:springdoc-openapi-starter-webmvc-ui:2.1.0'
}
```

</details>

<details>
<summary>Swagger 주요 Annotation</summary>

<details>
<summary><code>&#64;Schema</code> &#45; 엔티티, DTO, 필드 등 설명</summary>

- <strong><code>모델 클래스</code></strong>나 <strong><code>필드</code></strong>에 대한 <u>설명을 추가</u>하는 데 사용

- ex ) DTO 클래스에서 각 필드의 의미
    <a id="1c3eda9b0fe181f79707caef9b045aad"></a>

    ```groovy
    import io.swagger.v3.oas.annotations.media.Schema;

    @Schema(description = "사용자 생성 요청 모델")
    public record CreateUserRequest(
            @Schema(description = "사용자 이름", example = "john_doe", required = true)
            String name,
            
            @Schema(description = "사용자 비밀번호", example = "securePassword123", required = true)
            String password
    ) {}
    ```

    - <code>description</code>&#58; 필드, 클래스 설명

    - <code>example</code>&#58; 필드에 대한 예제 값 제공

    - <code>required</code>&#58; 필수 여부 지정

</details>

<details>
<summary><code>&#64;Tag</code> &#45; Controller 계층 ( 여러 API ) 설명</summary>

- API 그룹화 및 설명에 사용
    - 컨트롤러 클래스에 주로 사용

    - 특정 API 를 태그로 분류함

- ex) 
    <a id="1c3eda9b0fe181d88bc6e212cd3e06e8"></a>

    ```groovy
    import io.swagger.v3.oas.annotations.tags.Tag;

    @RestController
    @RequestMapping("/users")
    @Tag(name = "User API", description = "사용자 관련 API")
    public class UserController {

        @GetMapping("/{id}")
        public String getUser(@PathVariable Long id) {
            return "User details";
        }
    }
    ```

    - <code>name</code>&#58; 태그 이름

    - <code>description</code>&#58; 태그에 대한 설명

</details>

<details>
<summary><code>&#64;Operation</code> &#45;  API ( Controller 메서드) 단위 설명</summary>

- API 메서드의 세부 정보를 문서화하는 데 사용

- ex)
    <a id="1c3eda9b0fe181b39593c8536a76d3cc"></a>

    ```groovy
    import io.swagger.v3.oas.annotations.Operation;
    import io.swagger.v3.oas.annotations.responses.ApiResponse;
    import io.swagger.v3.oas.annotations.responses.ApiResponses;

    @RestController
    @RequestMapping("/users")
    public class UserController {

        @Operation(summary = "사용자 조회", description = "ID를 기반으로 사용자를 조회합니다.")
        @ApiResponses({
            @ApiResponse(responseCode = "200", description = "성공적으로 사용자 조회"),
            @ApiResponse(responseCode = "404", description = "사용자를 찾을 수 없음")
        })
        @GetMapping("/{id}")
        public String getUser(@PathVariable Long id) {
            return "User details";
        }
    }
    ```

    - <code>summary</code>&#58; API 메서드 요약 설명

    - <code>description</code>&#58; API 메서드에 대한 상세 설명

    - <code>&#64;ApiResponses</code>&#58; HTTP 응답 코드에 대한 설명 정의 ( 아래에서 다시 설명 ) 

</details>

<details>
<summary><code>&#64;Parameter</code></summary>

- 메서드 파라미터에 대한 추가 정보 문서화

- ex)
    <a id="1c3eda9b0fe181d49bc8fce0647538f2"></a>

    ```groovy
    import io.swagger.v3.oas.annotations.Parameter;

    @GetMapping("/users")
    public String getUsers(
        @Parameter(description = "페이지 번호", example = "1") @RequestParam int page,
        @Parameter(description = "페이지 크기", example = "10") @RequestParam int size
    ) {
        return "User list";
    }
    ```

- PathVariable
    - Swagger는 경로 변수를 자동으로 인식한다&#46;

    - 매개변수에 대한 자세한 설명을 추가
        - <code>&#64;Operation</code>, <code>&#64;Parameter</code>

    <a id="1c3eda9b0fe181f58cc0e92427ab85c3"></a>

    ```java
    @RestController
    public class UserController {

        @Operation(
    		    summary = "Get User by ID", 
    		    description = "Fetch a user's details using their ID."
        )
        @GetMapping("/users/{id}")
        public String getUserById(
            @Parameter(description = "ID of the user to retrieve", required = true)
            @PathVariable("id") Long id
        ) {
            return "User ID: " + id;
        }
    }
    ```

</details>

<details>
<summary><code>&#64;RequestBody</code>, <code>&#64;RequestParam</code></summary>

- 요청 데이터에 대한 문서를 작성 시, 활용

- ex) 
    <a id="1c3eda9b0fe1811195a5f884ecf5662e"></a>

    ```groovy
    import io.swagger.v3.oas.annotations.Operation;
    import io.swagger.v3.oas.annotations.parameters.RequestBody;

    @RestController
    @RequestMapping("/users")
    public class UserController {

        @Operation(summary = "사용자 생성", description = "새로운 사용자를 생성합니다.")
        @PostMapping
        public String createUser(
            @RequestBody(description = "생성할 사용자 정보", required = true) CreateUserRequest request
        ) {
            return "User created";
        }
    }
    ```

</details>

<details>
<summary> <code>&#64;ApiResponses</code>   &#45; response 정의 (HTTP 응답 코드, 결과)</summary>

- HTTP 응답 코드와 결과에 대한 설명 정의

<a id="1c3eda9b0fe1819d8bdbdbdacf3c2371"></a>

```groovy
@Operation(summary = "사용자 삭제", description = "ID를 기반으로 사용자를 삭제합니다.")
@ApiResponses({
    @ApiResponse(responseCode = "200", description = "성공적으로 사용자 삭제"),
    @ApiResponse(responseCode = "404", description = "사용자를 찾을 수 없음")
})
@DeleteMapping("/{id}")
public String deleteUser(@PathVariable Long id) {
    return "User deleted";
```

</details>

---

<details>
<summary>&#91; 전체 코드 &#93;</summary>

<a id="1c3eda9b0fe181fbad65cfef18d1bd8c"></a>

```groovy
import io.swagger.v3.oas.annotations.Operation;
import io.swagger.v3.oas.annotations.media.Schema;
import io.swagger.v3.oas.annotations.responses.ApiResponse;
import io.swagger.v3.oas.annotations.tags.Tag;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/users")
@Tag(name = "User API", description = "사용자 관리 API")
public class UserController {

    @Operation(summary = "사용자 생성", description = "새로운 사용자를 생성합니다.")
    @ApiResponse(responseCode = "201", description = "사용자 생성 성공")
    @PostMapping
    public String createUser(
            @RequestBody(description = "생성할 사용자 정보", required = true)
            CreateUserRequest request) {
        return "User created";
    }

    @Operation(summary = "사용자 조회", description = "ID를 기반으로 사용자를 조회합니다.")
    @ApiResponse(responseCode = "200", description = "성공적으로 사용자 조회")
    @GetMapping("/{id}")
    public String getUser(@PathVariable Long id) {
        return "User details";
    }
}

@Schema(description = "사용자 생성 요청 모델")
public record CreateUserRequest(
        @Schema(description = "사용자 이름", example = "john_doe", required = true)
        String name,
        @Schema(description = "사용자 비밀번호", example = "securePassword123", required = true)
        String password
) {}
```

- <strong><code>&#64;Schema</code></strong>&#58; 모델 클래스와 필드 설명 추가

- <strong><code>&#64;Tag</code></strong>&#58; 컨트롤러를 태그로 분류

- <strong><code>&#64;Operation</code></strong>&#58; 각 API 엔드포인트 설명

- <strong><code>&#64;ApiResponse</code></strong>&#58; 응답 코드와 결과에 대한 설명

- <strong><code>&#64;Parameter</code></strong>&#58; 메서드 파라미터에 설명 추가

</details>

</details>

<details>
<summary><strong>Swagger UI 접근</strong></summary>

<a id="1c3eda9b0fe181d79c48ddeda39d48fd"></a>

SpringDoc OpenAPI를 설정한 경우, 애플리케이션 실행 후 기본적으로 해당 URL에서 Swagger UI 확인 가능

- Swagger UI&#58; <a href="http://localhost:8080/swagger-ui.html">http&#58;//localhost&#58;8080/swagger&#45;ui&#46;html</a>

- OpenAPI JSON&#58; <a href="http://localhost:8080/v3/api-docs">http&#58;//localhost&#58;8080/v3/api&#45;docs</a>

</details>

---

<details>
<summary><code>코드</code>&#58; auth API </summary>

- DTO
    <details>
    <summary>&#91; 코드 &#93; CreateUserRequest</summary>

    > /domain/auth/model/request

    <a id="1c3eda9b0fe181cd90ffee6b22c99b2e"></a>

    ```java
    package com.example.lecture_prac.domain.auth.model.request;

    import io.swagger.v3.oas.annotations.media.Schema;
    import jakarta.validation.constraints.NotBlank;
    import jakarta.validation.constraints.NotNull;

    @Schema(description = "User를 생성합니다.")
    public record CreateUserRequest(

            @Schema(description = "유저 이름")
            @NotBlank
            @NotNull
            String name,

            @Schema(description = "유저 비밀번호")
            @NotBlank
            @NotNull
            String password

    ) {}
    ```

    </details>

    <details>
    <summary>&#91; 코드 &#93; CreateUserResponse</summary>

    > /domain/auth/model/response

    <a id="1c3eda9b0fe18176b02ecf75cf2f0fd5"></a>

    ```java
    package com.example.lecture_prac.domain.auth.model.response;


    import io.swagger.v3.oas.annotations.media.Schema;

    @Schema(description = "유저 생성 Response")
    public record CreateUserResponse(
            @Schema(description = "성공 유무")
            String code
    ) {
    }

    ```

    </details>

- Controller
    <details>
    <summary>&#91; 코드 &#93; AuthControllerV1</summary>

    <a id="1c3eda9b0fe1817d97f3ebf3c48af0c3"></a>

    ```java
    package com.example.lecture_prac.domain.auth.controller;


    import com.example.lecture_prac.domain.auth.model.request.CreateUserRequest;
    import com.example.lecture_prac.domain.auth.model.response.CreateUserResponse;
    import com.example.lecture_prac.domain.auth.service.AuthService;
    import io.swagger.v3.oas.annotations.Operation;
    import io.swagger.v3.oas.annotations.tags.Tag;
    import jakarta.validation.Valid;
    import lombok.RequiredArgsConstructor;
    import org.springframework.web.bind.annotation.PostMapping;
    import org.springframework.web.bind.annotation.RequestBody;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RestController;

    @Tag(name = "Auth API", description = "V1 Auth API")
    @RestController
    @RequestMapping("/api/v1/auth")
    @RequiredArgsConstructor
    public class AuthControllerV1 {

        private final AuthService authService;

        @Operation(
                summary = "새로운 유저를 생성합니다.",
                description = "새로운 유저 생성"
        )
        @PostMapping("/create-user")
        public CreateUserResponse createUser(@RequestBody @Valid CreateUserRequest request) {

            return authService.createUser(request);
        }
    }

    ```

    </details>

- Service
    <details>
    <summary>&#91; 코드 &#93; AuthService</summary>

    > repository 계층 설계 전

    <a id="1c3eda9b0fe181fcac0dc8cc68843152"></a>

    ```java
    @Slf4j
    @Service
    @RequiredArgsConstructor
    public class AuthService {


        public CreateUserResponse createUser(CreateUserRequest request) {


            return new CreateUserResponse(request.name());
        }
    }
    ```

    </details>

</details>
