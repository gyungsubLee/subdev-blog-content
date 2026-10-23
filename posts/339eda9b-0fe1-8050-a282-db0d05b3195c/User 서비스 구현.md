---
order: 2
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 339eda9b-0fe1-8050-a282-db0d05b3195c
title: User 서비스 구현
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
    title: 대규모 시스템 설계
  - id: 32eeda9b-0fe1-800b-a369-d0769871b739
    title: 1티어 패션 커머스의 세일 도메인 프로젝트로 배우는 대규모 트래픽을 견디는 실전 백엔드의 모든 것
  - id: 339eda9b-0fe1-8050-a282-db0d05b3195c
    title: User 서비스 구현
excerpt: 목차 - User 서비스 구현 - 스펙 문서 - 개요 - API - 데이터베이스 스키마 - 마이크로서비스 통합 - 코드 - User 모듈 - 강의 코드 - 직접 구현 User 서비스 구현 --- 스펙 문서 📖 User 서비스는 사용자 관리, 인증, 그리고 권한 관리를 담당하는 마이크로서비스이다. [fastcampus-p
cover: fb3b1ee7da4a15e0.webp
icon: 9bed2eae1e079b4b.avif
notionProperties: {}
schema_version: 1
parent_id: 32eeda9b-0fe1-800b-a369-d0769871b739
created: 2026-04-05T07:21:36.970Z
updated: 2026-04-10T14:20:01.264Z
legacy_path: Main/대규모 시스템 설계-d6a1706fbaf8/1티어 패션 커머스의 세일 도메인 프로젝트로 배우는 대규모 트래픽을 견디는 실전 -d0769871b739/User 서비스 구현-db0d05b3195c/index.md
legacy_category: 대규모 시스템 설계
source_url: https://beautiful-college-c84.notion.site/339eda9b0fe18050a282db0d05b3195c
---
> 
> 
> <a id="339eda9b0fe180399585e4a8656bb155"></a>
> 
> <strong>목차</strong>
> 
> - [User 서비스 구현](#339eda9b0fe1806cbcb1e1ac8f650e80)
> - [스펙 문서](#339eda9b0fe18066a2cdced01e6d9bb6)
> - [개요](#339eda9b0fe180d2b48bc8830e19865b)
> - [API ](#339eda9b0fe1809e89c7e703e198aed0)
> - [데이터베이스 스키마](#339eda9b0fe180338e9ce1493bcfe1d1)
> - [마이크로서비스 통합](#339eda9b0fe18024b14fe2109c469dc8)
> - [코드 - User 모듈](#339eda9b0fe180beb000ffe2763e6150)
> - [강의 코드](#339eda9b0fe18099b5c0fbe6a6d576dc)
> - [직접 구현](#339eda9b0fe18070bd06d60a5c043c16)

<a id="339eda9b0fe1806cbcb1e1ac8f650e80"></a>

# User 서비스 구현

---

<a id="339eda9b0fe18066a2cdced01e6d9bb6"></a>

## 스펙 문서

> 📖 
> 
> <a id="339eda9b0fe180acb81cc04b572b4a89"></a>
> 
> User 서비스는 <strong><u>사용자 관리, 인증, 그리고 권한 관리</u></strong>를 담당하는 마이크로서비스이다&#46;

[fastcampus&#45;promotion&#45;project/PROJECT&#45;PROMOTION/docs/P02/CH03&#95;01&#46; User 서비스 구현&#46;md at main · dobby&#45;teacher/fastcampus&#45;promotion&#45;project]()

<a id="339eda9b0fe180d2b48bc8830e19865b"></a>

### 개요

<details>
<summary>주요 기능</summary>

- 사용자 등록 및 관리

- 로그인 및 인증

- JWT 토큰 관리

- 사용자 프로필 관리

- 로그인 이력 관리

</details>

<details>
<summary>의존성</summary>

<a id="33eeda9b0fe1805bb971fcff3504871a"></a>

```groovy
dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-actuator'
	implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
	implementation 'org.springframework.boot:spring-boot-starter-web'
	implementation 'org.springframework.cloud:spring-cloud-starter-netflix-eureka-client'
	implementation 'org.springframework.boot:spring-boot-starter-validation'
	runtimeOnly 'com.h2database:h2'
	compileOnly 'org.projectlombok:lombok'
	annotationProcessor 'org.projectlombok:lombok'
	implementation 'jakarta.validation:jakarta.validation-api:3.0.2'
	
	// JWT
	implementation 'io.jsonwebtoken:jjwt-api:0.12.5'
	runtimeOnly 'io.jsonwebtoken:jjwt-impl:0.12.5'
	runtimeOnly 'io.jsonwebtoken:jjwt-jackson:0.12.5'

	testImplementation 'org.springframework.boot:spring-boot-starter-test'
	testRuntimeOnly 'org.junit.platform:junit-platform-launcher'
}
```

- Spring Boot Actuator

- Spring Data JPA

- Spring web

- Eureka Discovery Client

- H2 Database

- Lombok

- Validation

- JWT (JSON Web Token)

</details>

<a id="339eda9b0fe1809e89c7e703e198aed0"></a>

### API 

<details>
<summary><strong>인증</strong></summary>

- 로그인&#58; <code>POST /api/v1/users/login</code>

-  토큰 검증&#58; <code>POST /api/v1/users/validate&#45;token</code>

- 토큰 갱신&#58; <code>POST /api/v1/users/refresh&#45;token</code>

</details>

<details>
<summary>사용자 관리</summary>

- 회원가입&#58; <code>POST /api/v1/users/signup</code>

- 프로필 조회&#58; <code>GET /api/v1/users/me</code>

- 프로필 수정&#58; <code>PUT /api/v1/users/me</code>

- 비밀번호 변경&#58; <code>POST /api/v1/users/me/password</code>

- 로그인 이력 조회&#58; <code>GET /api/v1/users/me/login&#45;history</code>

</details>

<a id="339eda9b0fe180338e9ce1493bcfe1d1"></a>

### 데이터베이스 스키마

<details>
<summary>Users 테이블</summary>

<a id="339eda9b0fe1808f9f3de8ca34363676"></a>

```sql
CREATE TABLE users (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    email VARCHAR(255) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    name VARCHAR(255) NOT NULL,
    created_at TIMESTAMP,
    updated_at TIMESTAMP
);
```

</details>

<details>
<summary>User Login History 테이블</summary>

<a id="339eda9b0fe1809cb08acef59c4b754d"></a>

```sql
CREATE TABLE user_login_history (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    user_id BIGINT,
    login_at TIMESTAMP,
    ip_address VARCHAR(45),
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

</details>

<a id="339eda9b0fe18024b14fe2109c469dc8"></a>

### <strong>마이크로서비스 통합</strong>

<details>
<summary>서비스 디스커버리</summary>

- Eureka Client 등록

- 서비스 이름&#58; USER&#45;SERVICE

- 로드밸런싱 지원

</details>

<details>
<summary>API Gateway 연동</summary>

- 라우팅 설정

- 인증 필터 적용

- 속도 제한 설정

</details>

<a id="339eda9b0fe180beb000ffe2763e6150"></a>

## 코드 &#45; User 모듈

<a id="339eda9b0fe18099b5c0fbe6a6d576dc"></a>

### <strong>강의 코드</strong>

[fastcampus&#45;promotion&#45;project/PROJECT&#45;PROMOTION/promotion/user&#45;service at main · dobby&#45;teacher/fastcampus&#45;promotion&#45;project]()

- config
    <details>
    <summary>&#91;코드&#93; PasswordEncoderConfig</summary>

    <a id="33eeda9b0fe18098ae5cdfb2f3d4eda7"></a>

    ```java
    package com.fastcampus.userservice.config;

    import org.springframework.context.annotation.Bean;
    import org.springframework.context.annotation.Configuration;
    import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
    import org.springframework.security.crypto.password.PasswordEncoder;

    @Configuration
    public class PasswordEncoderConfig {

        @Bean
        public PasswordEncoder passwordEncoder() {
            return new BCryptPasswordEncoder();
        }
    }
    ```

    </details>

- controller
    <details>
    <summary>🧐 UserController 내부에 <strong><u>ExceptionHandler도 같이 처리</u></strong>한다&#46; 그 이유가 무엇인가?</summary>

    <details>
    <summary>의문점 코드</summary>

    <a id="33eeda9b0fe18018b77eeaf53e4b2e79"></a>

    ```java
    @RestController
    @RequestMapping("/api/v1/users")
    public class UserController {

    	. . .
    	
    		@ExceptionHandler(UserNotFoundException.class)
        public ResponseEntity<String> handleUserNotFound(UserNotFoundException exception) {
            return ResponseEntity.status(HttpStatus.NOT_FOUND).body(exception.getMessage());
        }

        @ExceptionHandler(DuplicateUserException.class)
        public ResponseEntity<String> handleDuplicateUser(DuplicateUserException exception) {
            return ResponseEntity.status(HttpStatus.CONFLICT).body(exception.getMessage());
        }

        @ExceptionHandler(UnauthorizedAccessException.class)
        public ResponseEntity<String> handleUnauthorizedAccess(UnauthorizedAccessException exception) {
            return ResponseEntity.status(HttpStatus.FORBIDDEN).body(exception.getMessage());
        }
    } 
    ```

    - 단일 모듈에서는 GlobalExceptionHandler로 중복 로직을 제거하고 단일 지점을 관리했다&#46;

    - 멀티 모듈에서도 common 모듈에 GlobalExceptionHandler 관리하거나

    - 모듈마다 따로 GlobalExceptionHandler 계층을 두어 관리하는 방법도 있을 텐데 왜 controller 계층에서 처리하는가?

    </details>

    <details>
    <summary><strong>이유</strong></summary>

    > <strong><u>모듈 독립성을 유지</u></strong>하려는 의도이다&#46;

    - user 모듈이 다른 모듈과 의존성 없이 독립적으로 동작 가능하다&#46;

    - 자기 에러 정책

    - 여러 모듈마다 정책이 다를 경우 해당 방식 알맞다&#46;

    ---

    <details>
    <summary>예시</summary>

    <a id="33eeda9b0fe180ef987fec9c179b6937"></a>

    ```java
    user-service
    order-service
    payment-service
    ```

    - 위와 같이 3개의 모듈을 가진다고 가정했을 때, <code>각각 에러 포맷,</code> <code>HTTP status 정책</code>, <code>메시지 정책</code><strong> 등이 </strong><strong><u>다룰 수 있</u></strong>다&#46; 

    - 따라서 모듈 내부에서 처리하면 의존성(coupling)이 줄어들고 독립적으로 설계할 수 있다&#46; 

    </details>

    </details>

    <details>
    <summary>다른 방법) <strong>Global Exception Handler</strong></summary>

    <a id="33eeda9b0fe180bd9863da79c24134b1"></a>

    ```java
    @RestControllerAdvice
    public class GlobalExceptionHandler {
    }
    ```

    - Global Exception Handler 도 많이 사용한다&#46; 

    - 사용 상황
        - 단일 서비스 (monolith)

        - 모든 모듈이 동일한 에러 정책 사용

        - API 응답 표준이 강하게 정의됨

    - 장점
        - 중복 제거

        - 응답 포맷 통일

        - 유지보수 쉬움

    - 단점
        - global handler가 common 모듈, 각 모듈이 common 모듈에 의존성을 가진다&#46; <br>따라서 common 변경 시 전체 서비스에 영향을 준다&#46; 

        - 도메인별 에러 정책이 다를 경우 오히려 global로 처리하면 로직이 복잡해진다&#46; 

        - 마이크로서비스로 확장할 경우, global handler(common)는 공유 불가능하다&#46;
            - jar는 공유 가능하지만 정책 충돌 발생

        -  또한 각 서비스별 customization 필요하다&#46;

    </details>

    </details>

    <details>
    <summary>&#91;코드&#93; AuthController</summary>

    <a id="33eeda9b0fe180ce8719f6f60d154186"></a>

    ```java
    package com.fastcampus.userservice.controller;

    import com.fastcampus.userservice.dto.UserDto;
    import com.fastcampus.userservice.entity.User;
    import com.fastcampus.userservice.service.JWTService;
    import com.fastcampus.userservice.service.UserService;
    import io.jsonwebtoken.Claims;
    import org.springframework.http.ResponseEntity;
    import org.springframework.web.bind.annotation.PostMapping;
    import org.springframework.web.bind.annotation.RequestBody;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RestController;

    import java.util.Collections;
    import java.util.Map;

    @RestController
    @RequestMapping("/api/v1/users")
    public class AuthController {

        private final JWTService jwtService;
        private final UserService userService;

        public AuthController(JWTService jwtService, UserService userService) {
            this.jwtService = jwtService;
            this.userService = userService;
        }

        @PostMapping("/login")
        public ResponseEntity<?> login(
                @RequestBody UserDto.LoginRequest request) {
            User user = userService.authenticate(request.getEmail(), request.getPassword());
            String token = jwtService.generateToken(user);
            return ResponseEntity.ok(UserDto.LoginResponse.builder()
                    .token(token)
                    .user(UserDto.Response.from(user))
                    .build());
        }

        @PostMapping("/validate-token")
        public ResponseEntity<?> validateToken(
                @RequestBody UserDto.TokenRequest request) {
            Claims claims = jwtService.validateToken(request.getToken());
            return ResponseEntity.ok(UserDto.TokenResponse.builder()
                    .email(claims.getSubject())
                    .valid(true)
                    .role(claims.get("role", String.class))
                    .build());
        }

        @PostMapping("/refresh-token")
        public ResponseEntity<Map<String, String>> refreshToken(
                @RequestBody UserDto.TokenRequest tokenRequest) {
            String newToken = jwtService.refreshToken(tokenRequest.getToken());
            return ResponseEntity.ok(Collections.singletonMap("token", newToken));
        }
    }
    ```

    </details>

    <details>
    <summary>&#91;코드&#93; UserController</summary>

    <a id="33eeda9b0fe1800492b4cdf8dcfa7e07"></a>

    ```java
    package com.fastcampus.userservice.controller;

    import com.fastcampus.userservice.dto.UserDto;
    import com.fastcampus.userservice.entity.User;
    import com.fastcampus.userservice.entity.UserLoginHistory;
    import com.fastcampus.userservice.exception.DuplicateUserException;
    import com.fastcampus.userservice.exception.UnauthorizedAccessException;
    import com.fastcampus.userservice.exception.UserNotFoundException;
    import com.fastcampus.userservice.service.UserService;
    import org.springframework.http.HttpStatus;
    import org.springframework.http.ResponseEntity;
    import org.springframework.web.bind.annotation.*;

    import java.util.List;

    @RestController
    @RequestMapping("/api/v1/users")
    public class UserController {

        private final UserService userService;

        public UserController(UserService userService) {
            this.userService = userService;
        }

        @PostMapping("/signup")
        public ResponseEntity<?> createUser(
                @RequestBody UserDto.SignupRequest request) {
            User user = userService.createUser(request.getEmail(), request.getPassword(), request.getName());
            return ResponseEntity.status(HttpStatus.CREATED).body(UserDto.Response.from(user));
        }

        @GetMapping("/me")
        public ResponseEntity<?> getProfile(
                @RequestHeader("X-USER-ID") Integer userId) {
            User user = userService.getUserById(userId);
            return ResponseEntity.ok(UserDto.Response.from(user));
        }

        @PutMapping("/me")
        public ResponseEntity<?> updateProfile(
                @RequestHeader("X-USER-ID") Integer userId,
                @RequestBody UserDto.UpdateRequest request) {
            User user = userService.updateUser(userId, request.getName());
            return ResponseEntity.ok(UserDto.Response.from(user));
        }

        @PostMapping("/me/password")
        public ResponseEntity<?> changePassword(
                @RequestHeader("X-USER-ID") Integer userId,
                @RequestBody UserDto.PasswordChangeRequest request) {
            userService.changePassword(userId, request.getCurrentPassword(), request.getNewPassword());
            return ResponseEntity.ok().build();
        }

        @GetMapping("/me/login-history")
        public ResponseEntity<List<UserLoginHistory>> getLoginHistory(
                @RequestHeader("X-USER-ID") Integer userId) {
            List<UserLoginHistory> history = userService.getUserLoginHistory(userId);
            return ResponseEntity.ok(history);
        }

        @ExceptionHandler(UserNotFoundException.class)
        public ResponseEntity<String> handleUserNotFound(UserNotFoundException exception) {
            return ResponseEntity.status(HttpStatus.NOT_FOUND).body(exception.getMessage());
        }

        @ExceptionHandler(DuplicateUserException.class)
        public ResponseEntity<String> handleDuplicateUser(DuplicateUserException exception) {
            return ResponseEntity.status(HttpStatus.CONFLICT).body(exception.getMessage());
        }

        @ExceptionHandler(UnauthorizedAccessException.class)
        public ResponseEntity<String> handleUnauthorizedAccess(UnauthorizedAccessException exception) {
            return ResponseEntity.status(HttpStatus.FORBIDDEN).body(exception.getMessage());
        }
    }
    ```

    </details>

- dto
    <details>
    <summary>&#91;코드&#93; UserDto</summary>

    <a id="33eeda9b0fe18015b84ad71e73442431"></a>

    ```java
    package com.fastcampus.userservice.dto;

    import com.fastcampus.userservice.entity.User;
    import jakarta.validation.constraints.Email;
    import jakarta.validation.constraints.NotBlank;
    import jakarta.validation.constraints.Pattern;
    import lombok.*;

    import java.time.LocalDateTime;

    public class UserDto {

        @Getter
        @Builder
        @NoArgsConstructor(access = AccessLevel.PRIVATE)
        @AllArgsConstructor(access = AccessLevel.PRIVATE)
        public static class SignupRequest {
            @NotBlank(message = "Email is required")
            @Email(message = "Invalid email format")
            private String email;

            @NotBlank(message = "Password is required")
            @Pattern(regexp = "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
                    message = "Password must be at least 8 characters long and contain both letters and numbers")
            private String password;

            @NotBlank(message = "Name is required")
            private String name;
        }

        @Getter
        @Builder
        @NoArgsConstructor(access = AccessLevel.PRIVATE)
        @AllArgsConstructor(access = AccessLevel.PRIVATE)
        public static class LoginRequest {
            @NotBlank(message = "Email is required")
            @Email(message = "Invalid email format")
            private String email;

            @NotBlank(message = "Password is required")
            private String password;
        }

        @Getter
        @Builder
        @NoArgsConstructor(access = AccessLevel.PRIVATE)
        @AllArgsConstructor(access = AccessLevel.PRIVATE)
        public static class UpdateRequest {
            @NotBlank(message = "Name is required")
            private String name;
        }

        @Getter
        @Builder
        @NoArgsConstructor(access = AccessLevel.PRIVATE)
        @AllArgsConstructor(access = AccessLevel.PRIVATE)
        public static class PasswordChangeRequest {
            @NotBlank(message = "Current password is required")
            private String currentPassword;

            @NotBlank(message = "New password is required")
            @Pattern(regexp = "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
                    message = "Password must be at least 8 characters long and contain both letters and numbers")
            private String newPassword;
        }

        @Getter
        @Builder
        @NoArgsConstructor(access = AccessLevel.PRIVATE)
        @AllArgsConstructor(access = AccessLevel.PRIVATE)
        public static class TokenRequest {
            @NotBlank(message = "Token is required")
            private String token;
        }

        @Getter
        @Builder
        @NoArgsConstructor(access = AccessLevel.PRIVATE)
        @AllArgsConstructor(access = AccessLevel.PRIVATE)
        public static class TokenResponse {
            private String email;
            private boolean valid;
            private String role;
        }

        @Getter
        @Builder
        @NoArgsConstructor(access = AccessLevel.PRIVATE)
        @AllArgsConstructor(access = AccessLevel.PRIVATE)
        public static class Response {
            private Integer id;
            private String email;
            private String name;
            private LocalDateTime createdAt;
            private LocalDateTime updatedAt;

            public static Response from(User user) {
                return Response.builder()
                        .id(user.getId())
                        .email(user.getEmail())
                        .name(user.getName())
                        .createdAt(user.getCreatedAt())
                        .updatedAt(user.getUpdatedAt())
                        .build();
            }
        }

        @Getter
        @Builder
        @NoArgsConstructor(access = AccessLevel.PRIVATE)
        @AllArgsConstructor(access = AccessLevel.PRIVATE)
        public static class LoginResponse {
            private String token;
            private Response user;
        }
    }
    ```

    </details>

- entity
    <details>
    <summary>&#91;코드&#93; User</summary>

    <a id="33eeda9b0fe18021934ec795f07f3d7b"></a>

    ```java
    package com.fastcampus.userservice.entity;

    import com.fasterxml.jackson.annotation.JsonBackReference;
    import com.fasterxml.jackson.annotation.JsonIgnore;
    import jakarta.persistence.*;
    import lombok.Getter;
    import lombok.Setter;
    import org.hibernate.annotations.CreationTimestamp;
    import org.hibernate.annotations.UpdateTimestamp;

    import java.time.LocalDateTime;
    import java.util.List;

    @Getter
    @Setter
    @Entity
    @Table(name = "users")
    public class User {

        @Id
        @GeneratedValue(strategy = GenerationType.IDENTITY)
        @Column(name = "id")
        private Integer id;

        @Column(name = "name", nullable = false, length = 100)
        private String name;

        @Column(name = "email", nullable = false, unique = true, length = 100)
        private String email;

        @Column(name = "password_hash", nullable = false, length = 255)
        @JsonIgnore
        private String passwordHash;

        @Column(name = "created_at", nullable = false, columnDefinition = "DATETIME DEFAULT CURRENT_TIMESTAMP")
        @CreationTimestamp
        private LocalDateTime createdAt;

        @Column(name = "updated_at", nullable = false, columnDefinition = "DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP")
        @UpdateTimestamp
        private LocalDateTime updatedAt;

        @OneToMany(mappedBy = "user", fetch = FetchType.LAZY, cascade = CascadeType.ALL)
        @JsonBackReference
        private List<UserLoginHistory> loginHistories;
    }
    ```

    </details>

    <details>
    <summary>&#91;코드&#93; UserLoginHistory</summary>

    <a id="33eeda9b0fe180cabcb0c3decb97e49b"></a>

    ```java
    package com.fastcampus.userservice.entity;

    import com.fasterxml.jackson.annotation.JsonBackReference;
    import jakarta.persistence.*;
    import lombok.Getter;
    import lombok.Setter;

    import java.time.LocalDateTime;

    @Getter
    @Setter
    @Entity
    @Table(name = "user_login_histories")
    public class UserLoginHistory {

        @Id
        @GeneratedValue(strategy = GenerationType.IDENTITY)
        @Column(name = "id")
        private Integer id;

        @ManyToOne(fetch = FetchType.LAZY)
        @JoinColumn(name = "user_id", nullable = false)
        @JsonBackReference
        private User user;

        @Column(name = "login_time", columnDefinition = "DATETIME DEFAULT CURRENT_TIMESTAMP")
        private LocalDateTime loginTime;

        @Column(name = "ip_address", length = 45)
        private String ipAddress;
    }
    ```

    </details>

- exception
    <details>
    <summary>&#91;코드&#93; DuplicateUserException</summary>

    <a id="33eeda9b0fe1800097eafcafbe349e7f"></a>

    ```java
    package com.fastcampus.userservice.exception;

    public class DuplicateUserException extends RuntimeException {
        public DuplicateUserException(String message) {
            super(message);
        }
    }
    ```

    </details>

    <details>
    <summary>&#91;코드&#93; UnauthorizedAccessException</summary>

    <a id="33eeda9b0fe18025b9c1eba5d1860305"></a>

    ```java
    package com.fastcampus.userservice.exception;

    public class UnauthorizedAccessException extends RuntimeException {
        public UnauthorizedAccessException(String message) {
            super(message);
        }
    }
    ```

    </details>

    <details>
    <summary>&#91;코드&#93; UserNotFoundException</summary>

    <a id="33eeda9b0fe180479f4ac51cb0460005"></a>

    ```java
    package com.fastcampus.userservice.exception;

    public class UserNotFoundException extends RuntimeException {
        public UserNotFoundException(String message) {
            super(message);
        }
    }
    ```

    </details>

- repository
    <details>
    <summary>&#91;코드&#93; UserLoginHistoryRepository</summary>

    <a id="33eeda9b0fe1802eb8b9f11e8fec52bf"></a>

    ```java
    package com.fastcampus.userservice.repository;

    import com.fastcampus.userservice.entity.User;
    import com.fastcampus.userservice.entity.UserLoginHistory;
    import org.springframework.data.jpa.repository.JpaRepository;

    import java.util.List;

    public interface UserLoginHistoryRepository extends JpaRepository<UserLoginHistory, Integer> {
        List<UserLoginHistory> findByUserOrderByLoginTimeDesc(User user);
    }
    ```

    </details>

    <details>
    <summary>&#91;코드&#93; UserRepository</summary>

    <a id="33eeda9b0fe180598646d96439bdb99b"></a>

    ```java
    package com.fastcampus.userservice.repository;

    import com.fastcampus.userservice.entity.User;
    import org.springframework.data.jpa.repository.JpaRepository;

    import java.util.Optional;

    public interface UserRepository extends JpaRepository<User, Integer> {
        Optional<User> findByEmail(String email);
    }
    ```

    </details>

- service
    <details>
    <summary>&#91;코드&#93; JWTService</summary>

    <a id="33eeda9b0fe180dfa591fd85341db9b5"></a>

    ```java
    package com.fastcampus.userservice.service;

    import com.fastcampus.userservice.entity.User;
    import io.jsonwebtoken.Claims;
    import io.jsonwebtoken.Jwts;
    import io.jsonwebtoken.security.Keys;
    import lombok.extern.slf4j.Slf4j;
    import org.springframework.beans.factory.annotation.Value;
    import org.springframework.security.crypto.password.PasswordEncoder;
    import org.springframework.stereotype.Service;

    import java.nio.charset.StandardCharsets;
    import java.util.Date;

    @Service
    @Slf4j
    public class JWTService {

        private final PasswordEncoder passwordEncoder;

        @Value("${jwt.secret}")
        private String secretKey;

        public JWTService(PasswordEncoder passwordEncoder) {
            this.passwordEncoder = passwordEncoder;
        }

        public String generateToken(User user) {
            long currentTimeMillis = System.currentTimeMillis();
            return Jwts.builder()
                    .subject(user.getEmail())
                    .claim("role", "USER")
                    .issuedAt(new Date(currentTimeMillis))
                    .expiration(new Date(currentTimeMillis + 3600000)) // Token expires in 1 hour
                    .signWith(Keys.hmacShaKeyFor(secretKey.getBytes(StandardCharsets.UTF_8)))
                    .compact();
        }

        public Claims validateToken(String token) {
            try {
                return parseJwtClaims(token);
            } catch (Exception e) {
                log.error("Token validation error: ", e);
                throw new IllegalArgumentException("Invalid token");
            }
        }

        public Claims parseJwtClaims(String token) {
            return Jwts.parser()
                    .verifyWith(Keys.hmacShaKeyFor(secretKey.getBytes(StandardCharsets.UTF_8)))
                    .build()
                    .parseSignedClaims(token)
                    .getPayload();
        }

        public String refreshToken(String token) {
            Claims claims = parseJwtClaims(token);
            long currentTimeMillis = System.currentTimeMillis();
            return Jwts.builder()
                    .subject(claims.getSubject())
                    .claims(claims)
                    .issuedAt(new Date(currentTimeMillis))
                    .expiration(new Date(currentTimeMillis + 3600000))
                    .signWith(Keys.hmacShaKeyFor(secretKey.getBytes(StandardCharsets.UTF_8)))
                    .compact();
        }
    }
    ```

    </details>

    <details>
    <summary>&#91;코드&#93; UserService</summary>

    <a id="33eeda9b0fe180b6ae3df7b8526cb054"></a>

    ```java
    package com.fastcampus.userservice.service;

    import com.fastcampus.userservice.entity.User;
    import com.fastcampus.userservice.entity.UserLoginHistory;
    import com.fastcampus.userservice.exception.DuplicateUserException;
    import com.fastcampus.userservice.exception.UnauthorizedAccessException;
    import com.fastcampus.userservice.exception.UserNotFoundException;
    import com.fastcampus.userservice.repository.UserLoginHistoryRepository;
    import com.fastcampus.userservice.repository.UserRepository;
    import org.springframework.security.crypto.password.PasswordEncoder;
    import org.springframework.stereotype.Service;
    import org.springframework.transaction.annotation.Transactional;

    import java.util.List;

    @Service
    public class UserService {

        private final UserRepository userRepository;
        private final UserLoginHistoryRepository userLoginHistoryRepository;
        private final PasswordEncoder passwordEncoder;

        public UserService(UserRepository userRepository,
                          UserLoginHistoryRepository userLoginHistoryRepository,
                          PasswordEncoder passwordEncoder) {
            this.userRepository = userRepository;
            this.userLoginHistoryRepository = userLoginHistoryRepository;
            this.passwordEncoder = passwordEncoder;
        }

        @Transactional
        public User createUser(String email, String password, String name) {
            if (userRepository.findByEmail(email).isPresent()) {
                throw new DuplicateUserException("User already exists with email: " + email);
            }

            User user = new User();
            user.setEmail(email);
            user.setPasswordHash(passwordEncoder.encode(password));
            user.setName(name);

            return userRepository.save(user);
        }

        public User authenticate(String email, String password) {
            User user = userRepository.findByEmail(email)
                    .orElseThrow(() -> new UserNotFoundException("User not found with email: " + email));

            if (!passwordEncoder.matches(password, user.getPasswordHash())) {
                throw new UnauthorizedAccessException("Invalid credentials");
            }

            return user;
        }

        public User getUserById(Integer userId) {
            return userRepository.findById(userId)
                    .orElseThrow(() -> new UserNotFoundException("User not found with ID: " + userId));
        }

        @Transactional
        public User updateUser(Integer userId, String name) {
            User user = getUserById(userId);
            user.setName(name);
            return userRepository.save(user);
        }

        @Transactional
        public void changePassword(Integer userId, String currentPassword, String newPassword) {
            User user = getUserById(userId);

            if (!passwordEncoder.matches(currentPassword, user.getPasswordHash())) {
                throw new UnauthorizedAccessException("Current password is incorrect");
            }

            user.setPasswordHash(passwordEncoder.encode(newPassword));
            userRepository.save(user);
        }

        public List<UserLoginHistory> getUserLoginHistory(Integer userId) {
            User user = getUserById(userId);
            return userLoginHistoryRepository.findByUserOrderByLoginTimeDesc(user);
        }
    }
    ```

    </details>

<a id="339eda9b0fe18070bd06d60a5c043c16"></a>

### <strong>직접 구현</strong>

[bookmark]()

> 🤔 
> 
> <a id="33eeda9b0fe18023a9bffa4ba12fa0c0"></a>
> 
> 차이점
> 
> - 폴더 구조 다름
> 
> - jwt 로직 util 클래스로 분리함 ( 강의 코드는 service 계층으로 처리함)
> 
> - exception handling ❌
>     - exception 처리 어느 계층에서 할지 정하고 추가 필요함

- config
    <details>
    <summary>&#91;코드&#93; PasswordEncoderConfig</summary>

    <a id="33eeda9b0fe180678f80ceec5fe89e30"></a>

    ```java
    package com.fastcampus.userservice.config;

    import org.springframework.context.annotation.Bean;
    import org.springframework.context.annotation.Configuration;
    import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
    import org.springframework.security.crypto.password.PasswordEncoder;

    @Configuration
    public class PasswordEncoderConfig {

        @Bean
        public PasswordEncoder passwordEncoder() {
            return new BCryptPasswordEncoder();
        }
    }
    ```

    </details>

- controller
    <details>
    <summary>&#91;코드&#93; AuthController</summary>

    <a id="33eeda9b0fe1803d9097f87bb47ae0d8"></a>

    ```java
    package com.example.userservice.controller;

    import org.springframework.http.ResponseEntity;
    import org.springframework.web.bind.annotation.PostMapping;
    import org.springframework.web.bind.annotation.RequestBody;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RestController;

    import com.example.userservice.dto.request.TokenRefreshRequest;
    import com.example.userservice.dto.request.TokenValidateRequest;
    import com.example.userservice.dto.request.UserLoginRequest;
    import com.example.userservice.dto.response.TokenResponse;
    import com.example.userservice.service.UserService;

    import jakarta.servlet.http.HttpServletRequest;
    import jakarta.validation.Valid;
    import lombok.RequiredArgsConstructor;

    @RestController
    @RequestMapping("/api/v1/users")
    @RequiredArgsConstructor
    public class AuthController {

        private final UserService userService;

        // Authentication
        @PostMapping("/login")
        public ResponseEntity<TokenResponse> login(@Valid @RequestBody UserLoginRequest request,
                HttpServletRequest servletRequest) {
            // Simple way to get client IP
            String ipAddress = servletRequest.getHeader("X-Forwarded-For");
            if (ipAddress == null) {
                ipAddress = servletRequest.getRemoteAddr();
            }
            return ResponseEntity.ok(userService.login(request, ipAddress));
        }

        @PostMapping("/validate-token")
        public ResponseEntity<Void> validateToken(@Valid @RequestBody TokenValidateRequest request) {
            userService.validateToken(request);
            return ResponseEntity.ok().build();
        }

        @PostMapping("/refresh-token")
        public ResponseEntity<TokenResponse> refreshToken(@Valid @RequestBody TokenRefreshRequest request) {
            return ResponseEntity.ok(userService.refreshToken(request));
        }

    }
    ```

    </details>

    <details>
    <summary>&#91;코드&#93; UserController</summary>

    <a id="33eeda9b0fe18034a46cf0ca31e38743"></a>

    ```java
    package com.example.userservice.controller;

    import com.example.userservice.dto.request.UserPasswordUpdateRequest;
    import com.example.userservice.dto.request.UserProfileUpdateRequest;
    import com.example.userservice.dto.request.UserSignupRequest;

    import com.example.userservice.dto.response.UserLoginHistoryResponse;
    import com.example.userservice.dto.response.UserProfileResponse;
    import com.example.userservice.dto.response.UserSignupResponse;
    import com.example.userservice.service.UserService;

    import jakarta.validation.Valid;
    import java.util.List;
    import lombok.RequiredArgsConstructor;
    import org.springframework.http.HttpStatus;
    import org.springframework.http.ResponseEntity;
    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.PostMapping;
    import org.springframework.web.bind.annotation.PutMapping;
    import org.springframework.web.bind.annotation.RequestBody;
    import org.springframework.web.bind.annotation.RequestHeader;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RestController;

    @RestController
    @RequestMapping("/api/v1/users")
    @RequiredArgsConstructor
    public class UserController {

        private final UserService userService;

        // User Management
        @PostMapping("/signup")
        public ResponseEntity<UserSignupResponse> signup(@Valid @RequestBody UserSignupRequest request) {
            return ResponseEntity.status(HttpStatus.CREATED).body(userService.signup(request));
        }

        // Extracting user ID from header assuming API Gateway passes it,
        // or placeholder until Spring Security integrates with @AuthenticationPrincipal
        @GetMapping("/me")
        public ResponseEntity<UserProfileResponse> getProfile(@RequestHeader("X-User-Id") Long userId) {
            return ResponseEntity.ok(userService.getProfile(userId));
        }

        @PutMapping("/me")
        public ResponseEntity<UserProfileResponse> updateProfile(
                @RequestHeader("X-User-Id") Long userId,
                @Valid @RequestBody UserProfileUpdateRequest request) {
            return ResponseEntity.ok(userService.updateProfile(userId, request));
        }

        @PostMapping("/me/password")
        public ResponseEntity<Void> updatePassword(
                @RequestHeader("X-User-Id") Long userId,
                @Valid @RequestBody UserPasswordUpdateRequest request) {
            userService.updatePassword(userId, request);
            return ResponseEntity.ok().build();
        }

        @GetMapping("/me/login-history")
        public ResponseEntity<List<UserLoginHistoryResponse>> getLoginHistory(@RequestHeader("X-User-Id") Long userId) {
            return ResponseEntity.ok(userService.getLoginHistory(userId));
        }
    }
    ```

    </details>

- domain
    - entity
        <details>
        <summary>&#91;코드&#93; User</summary>

        <a id="33eeda9b0fe180f9973cf3812599e1ce"></a>

        ```java
        package com.example.userservice.domain.entity;

        import jakarta.persistence.Column;
        import jakarta.persistence.Entity;
        import jakarta.persistence.EntityListeners;
        import jakarta.persistence.GeneratedValue;
        import jakarta.persistence.GenerationType;
        import jakarta.persistence.Id;
        import jakarta.persistence.Table;
        import java.time.LocalDateTime;
        import lombok.AccessLevel;
        import lombok.Builder;
        import lombok.Getter;
        import lombok.NoArgsConstructor;
        import org.springframework.data.annotation.CreatedDate;
        import org.springframework.data.annotation.LastModifiedDate;
        import org.springframework.data.jpa.domain.support.AuditingEntityListener;

        import com.fasterxml.jackson.annotation.JsonIgnore;

        @Getter
        @NoArgsConstructor(access = AccessLevel.PROTECTED)
        @EntityListeners(AuditingEntityListener.class)
        @Entity
        @Table(name = "users")
        public class User {

            @Id
            @GeneratedValue(strategy = GenerationType.IDENTITY)
            private Long id;

            @Column(nullable = false, unique = true)
            private String email;

            @Column(name = "password_hash", nullable = false)
            @JsonIgnore
            private String passwordHash;

            @Column(nullable = false)
            private String name;

            @CreatedDate
            @Column(name = "created_at", updatable = false)
            private LocalDateTime createdAt;

            @LastModifiedDate
            @Column(name = "updated_at")
            private LocalDateTime updatedAt;

            @Builder
            public User(String email, String passwordHash, String name) {
                this.email = email;
                this.passwordHash = passwordHash;
                this.name = name;
            }

            public void updateProfile(String name) {
                this.name = name;
            }

            public void updatePassword(String newPasswordHash) {
                this.passwordHash = newPasswordHash;
            }
        }
        ```

        </details>

        <details>
        <summary>&#91;코드&#93; UserLoginHistory</summary>

        <a id="33eeda9b0fe1806090e8d61dbef75074"></a>

        ```java
        package com.example.userservice.domain.entity;

        import jakarta.persistence.Column;
        import jakarta.persistence.Entity;
        import jakarta.persistence.EntityListeners;
        import jakarta.persistence.FetchType;
        import jakarta.persistence.GeneratedValue;
        import jakarta.persistence.GenerationType;
        import jakarta.persistence.Id;
        import jakarta.persistence.JoinColumn;
        import jakarta.persistence.ManyToOne;
        import jakarta.persistence.Table;
        import java.time.LocalDateTime;
        import lombok.AccessLevel;
        import lombok.Builder;
        import lombok.Getter;
        import lombok.NoArgsConstructor;
        import org.springframework.data.annotation.CreatedDate;
        import org.springframework.data.jpa.domain.support.AuditingEntityListener;

        @Getter
        @NoArgsConstructor(access = AccessLevel.PROTECTED)
        @EntityListeners(AuditingEntityListener.class)
        @Entity
        @Table(name = "user_login_histories")
        public class UserLoginHistory {

            @Id
            @GeneratedValue(strategy = GenerationType.IDENTITY)
            private Long id;

            @ManyToOne(fetch = FetchType.LAZY)
            @JoinColumn(name = "user_id", nullable = false)
            private User user;

            @CreatedDate
            @Column(name = "login_at", updatable = false)
            private LocalDateTime loginAt;

            @Column(name = "ip_address", length = 45)
            private String ipAddress;

            @Builder
            public UserLoginHistory(User user, String ipAddress) {
                this.user = user;
                this.ipAddress = ipAddress;
            }
        }
        ```

        </details>

    - repository
        <details>
        <summary>&#91;코드&#93; UserLoginHistoryRepository</summary>

        <a id="33eeda9b0fe18076919ff59f10b75af3"></a>

        ```java
        package com.example.userservice.domain.repository;

        import com.example.userservice.domain.entity.UserLoginHistory;
        import java.util.List;
        import org.springframework.data.jpa.repository.JpaRepository;

        public interface UserLoginHistoryRepository extends JpaRepository<UserLoginHistory, Long> {
            List<UserLoginHistory> findByUserIdOrderByLoginAtDesc(Long userId);
        }
        ```

        </details>

        <details>
        <summary>&#91;코드&#93; UserRepository</summary>

        <a id="33eeda9b0fe18083adbac44c8300f078"></a>

        ```java
        package com.example.userservice.domain.repository;

        import com.example.userservice.domain.entity.User;
        import java.util.Optional;
        import org.springframework.data.jpa.repository.JpaRepository;

        public interface UserRepository extends JpaRepository<User, Long> {
            Optional<User> findByEmail(String email);
            boolean existsByEmail(String email);
        }
        ```

        </details>

- dto
    <details>
    <summary>request</summary>

    <details>
    <summary>&#91;코드&#93; TokenRefreshRequest</summary>

    <a id="33eeda9b0fe180c1a703c91bfd58857e"></a>

    ```java
    package com.example.userservice.dto.request;

    import jakarta.validation.constraints.NotBlank;
    import lombok.Getter;
    import lombok.NoArgsConstructor;

    @Getter
    @NoArgsConstructor
    public class TokenRefreshRequest {
        @NotBlank(message = "Refresh token is required")
        private String refreshToken;
    }
    ```

    </details>

    <details>
    <summary>&#91;코드&#93; TokenValidateRequest</summary>

    <a id="33eeda9b0fe180a586becf2751eefd7b"></a>

    ```java
    package com.example.userservice.dto.request;

    import jakarta.validation.constraints.NotBlank;
    import lombok.Getter;
    import lombok.NoArgsConstructor;

    @Getter
    @NoArgsConstructor
    public class TokenValidateRequest {
        @NotBlank(message = "Token is required")
        private String token;
    }
    ```

    </details>

    <details>
    <summary>&#91;코드&#93; UserLoginRequest</summary>

    <a id="33eeda9b0fe180d9ac06d0f22ec04cb0"></a>

    ```java
    package com.example.userservice.dto.request;

    import jakarta.validation.constraints.Email;
    import jakarta.validation.constraints.NotBlank;
    import lombok.Getter;
    import lombok.NoArgsConstructor;

    @Getter
    @NoArgsConstructor
    public class UserLoginRequest {
        @NotBlank(message = "Email is required")
        @Email(message = "Invalid email format")
        private String email;

        @NotBlank(message = "Password is required")
        private String password;
    }
    ```

    </details>

    <details>
    <summary>&#91;코드&#93; UserPasswordUpdateRequest</summary>

    <a id="33eeda9b0fe180ff8979cec32f93e56e"></a>

    ```java
    package com.example.userservice.dto.request;

    import jakarta.validation.constraints.NotBlank;
    import lombok.Getter;
    import lombok.NoArgsConstructor;

    @Getter
    @NoArgsConstructor
    public class UserPasswordUpdateRequest {
        @NotBlank(message = "Current password is required")
        private String currentPassword;

        @NotBlank(message = "New password is required")
        private String newPassword;
    }
    ```

    </details>

    <details>
    <summary>&#91;코드&#93; UserProfileUpdateRequest</summary>

    <a id="33eeda9b0fe1805787bac782e1fcb010"></a>

    ```java
    package com.example.userservice.dto.request;

    import jakarta.validation.constraints.NotBlank;
    import lombok.Getter;
    import lombok.NoArgsConstructor;

    @Getter
    @NoArgsConstructor
    public class UserProfileUpdateRequest {
        @NotBlank(message = "Name is required")
        private String name;
    }
    ```

    </details>

    <details>
    <summary>&#91;코드&#93; UserSignupRequest</summary>

    <a id="33eeda9b0fe180ad9418df23c393c906"></a>

    ```java
    package com.example.userservice.dto.request;

    import jakarta.validation.constraints.Email;
    import jakarta.validation.constraints.NotBlank;
    import lombok.Getter;
    import lombok.NoArgsConstructor;

    @Getter
    @NoArgsConstructor
    public class UserSignupRequest {
        @NotBlank(message = "Email is required")
        @Email(message = "Invalid email format")
        private String email;

        @NotBlank(message = "Password is required")
        private String password;

        @NotBlank(message = "Name is required")
        private String name;
    }
    ```

    </details>

    </details>

    <details>
    <summary>response</summary>

    <details>
    <summary>&#91;코드&#93; TokenResponse</summary>

    <a id="33eeda9b0fe180508760f351ef75ac59"></a>

    ```java
    package com.example.userservice.dto.response;

    import lombok.AllArgsConstructor;
    import lombok.Builder;
    import lombok.Getter;
    import lombok.NoArgsConstructor;

    @Getter
    @Builder
    @NoArgsConstructor
    @AllArgsConstructor
    public class TokenResponse {
        private String accessToken;
        private String refreshToken;
    }
    ```

    </details>

    <details>
    <summary>&#91;코드&#93; UserLoginHistoryResponse</summary>

    <a id="33eeda9b0fe180e893f1db37e15c22ba"></a>

    ```java
    package com.example.userservice.dto.response;

    import java.time.LocalDateTime;
    import lombok.AllArgsConstructor;
    import lombok.Builder;
    import lombok.Getter;
    import lombok.NoArgsConstructor;

    @Getter
    @Builder
    @NoArgsConstructor
    @AllArgsConstructor
    public class UserLoginHistoryResponse {
        private Long id;
        private LocalDateTime loginAt;
        private String ipAddress;
    }
    ```

    </details>

    <details>
    <summary>&#91;코드&#93; UserProfileResponse</summary>

    <a id="33eeda9b0fe18022a6ffeea4b85caa42"></a>

    ```java
    package com.example.userservice.dto.response;

    import java.time.LocalDateTime;
    import lombok.AllArgsConstructor;
    import lombok.Builder;
    import lombok.Getter;
    import lombok.NoArgsConstructor;

    @Getter
    @Builder
    @NoArgsConstructor
    @AllArgsConstructor
    public class UserProfileResponse {
        private Long id;
        private String email;
        private String name;
        private LocalDateTime createdAt;
        private LocalDateTime updatedAt;
    }
    ```

    </details>

    <details>
    <summary>&#91;코드&#93; UserSignupResponse</summary>

    <a id="33eeda9b0fe180b49f60db0fd201d8ed"></a>

    ```java
    package com.example.userservice.dto.response;

    import java.time.LocalDateTime;
    import lombok.AllArgsConstructor;
    import lombok.Builder;
    import lombok.Getter;
    import lombok.NoArgsConstructor;

    @Getter
    @Builder
    @NoArgsConstructor
    @AllArgsConstructor
    public class UserSignupResponse {
        private Long id;
        private String email;
        private String name;
        private LocalDateTime createdAt;
    }
    ```

    </details>

    </details>

- service
    <details>
    <summary>&#91;코드&#93; UserService</summary>

    <a id="33eeda9b0fe180768637df9553e50a10"></a>

    ```java
    package com.example.userservice.service;

    import com.example.userservice.dto.request.TokenRefreshRequest;
    import com.example.userservice.dto.request.TokenValidateRequest;
    import com.example.userservice.dto.request.UserLoginRequest;
    import com.example.userservice.dto.request.UserPasswordUpdateRequest;
    import com.example.userservice.dto.request.UserProfileUpdateRequest;
    import com.example.userservice.dto.request.UserSignupRequest;
    import com.example.userservice.dto.response.TokenResponse;
    import com.example.userservice.dto.response.UserLoginHistoryResponse;
    import com.example.userservice.dto.response.UserProfileResponse;
    import com.example.userservice.dto.response.UserSignupResponse;
    import java.util.List;

    public interface UserService {
        UserSignupResponse signup(UserSignupRequest request);
        TokenResponse login(UserLoginRequest request, String ipAddress);
        void validateToken(TokenValidateRequest request);
        TokenResponse refreshToken(TokenRefreshRequest request);
        
        UserProfileResponse getProfile(Long userId);
        UserProfileResponse updateProfile(Long userId, UserProfileUpdateRequest request);
        void updatePassword(Long userId, UserPasswordUpdateRequest request);
        List<UserLoginHistoryResponse> getLoginHistory(Long userId);
    }
    ```

    </details>

    <details>
    <summary>&#91;코드&#93; UserServiceImpl</summary>

    <a id="33eeda9b0fe180f3814bef7ce3f9e890"></a>

    ```java
    package com.example.userservice.service;

    import com.example.userservice.domain.entity.User;
    import com.example.userservice.domain.entity.UserLoginHistory;
    import com.example.userservice.domain.repository.UserLoginHistoryRepository;
    import com.example.userservice.domain.repository.UserRepository;
    import com.example.userservice.dto.request.TokenRefreshRequest;
    import com.example.userservice.dto.request.TokenValidateRequest;
    import com.example.userservice.dto.request.UserLoginRequest;
    import com.example.userservice.dto.request.UserPasswordUpdateRequest;
    import com.example.userservice.dto.request.UserProfileUpdateRequest;
    import com.example.userservice.dto.request.UserSignupRequest;
    import com.example.userservice.dto.response.TokenResponse;
    import com.example.userservice.dto.response.UserLoginHistoryResponse;
    import com.example.userservice.dto.response.UserProfileResponse;
    import com.example.userservice.dto.response.UserSignupResponse;
    import com.example.userservice.util.JwtUtil;
    import java.util.List;
    import java.util.stream.Collectors;
    import lombok.RequiredArgsConstructor;
    import org.springframework.security.crypto.password.PasswordEncoder;
    import org.springframework.stereotype.Service;
    import org.springframework.transaction.annotation.Transactional;

    @Service
    @RequiredArgsConstructor
    public class UserServiceImpl implements UserService {

        private final UserRepository userRepository;
        private final UserLoginHistoryRepository userLoginHistoryRepository;
        private final PasswordEncoder passwordEncoder;
        private final JwtUtil jwtUtil;

        @Override
        @Transactional
        public UserSignupResponse signup(UserSignupRequest request) {
            if (userRepository.existsByEmail(request.getEmail())) {
                throw new IllegalArgumentException("Email already exists");
            }

            User user = User.builder()
                    .email(request.getEmail())
                    .passwordHash(passwordEncoder.encode(request.getPassword()))
                    .name(request.getName())
                    .build();

            User savedUser = userRepository.save(user);

            return UserSignupResponse.builder()
                    .id(savedUser.getId())
                    .email(savedUser.getEmail())
                    .name(savedUser.getName())
                    .createdAt(savedUser.getCreatedAt())
                    .build();
        }

        @Override
        @Transactional
        public TokenResponse login(UserLoginRequest request, String ipAddress) {
            User user = userRepository.findByEmail(request.getEmail())
                    .orElseThrow(() -> new IllegalArgumentException("Invalid email or password"));

            if (!passwordEncoder.matches(request.getPassword(), user.getPasswordHash())) {
                throw new IllegalArgumentException("Invalid email or password");
            }

            // Saving login history
            UserLoginHistory history = UserLoginHistory.builder()
                    .user(user)
                    .ipAddress(ipAddress)
                    .build();
            userLoginHistoryRepository.save(history);

            // Generate tokens
            return TokenResponse.builder()
                    .accessToken(jwtUtil.generateAccessToken(user.getEmail(), user.getId()))
                    .refreshToken(jwtUtil.generateRefreshToken(user.getEmail(), user.getId()))
                    .build();
        }

        @Override
        public void validateToken(TokenValidateRequest request) {
            if (!jwtUtil.validateToken(request.getToken())) {
                throw new IllegalArgumentException("Invalid or expired token");
            }
        }

        @Override
        public TokenResponse refreshToken(TokenRefreshRequest request) {
            if (!jwtUtil.validateToken(request.getRefreshToken())) {
                throw new IllegalArgumentException("Invalid refresh token");
            }

            String email = jwtUtil.getEmailFromToken(request.getRefreshToken());
            Long userId = jwtUtil.getUserIdFromToken(request.getRefreshToken());

            // Validate user still exists
            userRepository.findById(userId)
                    .orElseThrow(() -> new IllegalArgumentException("User not found"));

            return TokenResponse.builder()
                    .accessToken(jwtUtil.generateAccessToken(email, userId))
                    .refreshToken(jwtUtil.generateRefreshToken(email, userId))
                    .build();
        }

        @Override
        @Transactional(readOnly = true)
        public UserProfileResponse getProfile(Long userId) {
            User user = userRepository.findById(userId)
                    .orElseThrow(() -> new IllegalArgumentException("User not found"));

            return UserProfileResponse.builder()
                    .id(user.getId())
                    .email(user.getEmail())
                    .name(user.getName())
                    .createdAt(user.getCreatedAt())
                    .updatedAt(user.getUpdatedAt())
                    .build();
        }

        @Override
        @Transactional
        public UserProfileResponse updateProfile(Long userId, UserProfileUpdateRequest request) {
            User user = userRepository.findById(userId)
                    .orElseThrow(() -> new IllegalArgumentException("User not found"));

            user.updateProfile(request.getName());

            return UserProfileResponse.builder()
                    .id(user.getId())
                    .email(user.getEmail())
                    .name(user.getName())
                    .createdAt(user.getCreatedAt())
                    .updatedAt(user.getUpdatedAt())
                    .build();
        }

        @Override
        @Transactional
        public void updatePassword(Long userId, UserPasswordUpdateRequest request) {
            User user = userRepository.findById(userId)
                    .orElseThrow(() -> new IllegalArgumentException("User not found"));

            if (!passwordEncoder.matches(request.getCurrentPassword(), user.getPasswordHash())) {
                throw new IllegalArgumentException("Current password does not match");
            }

            user.updatePassword(passwordEncoder.encode(request.getNewPassword()));
        }

        @Override
        @Transactional(readOnly = true)
        public List<UserLoginHistoryResponse> getLoginHistory(Long userId) {
            return userLoginHistoryRepository.findByUserIdOrderByLoginAtDesc(userId)
                    .stream()
                    .map(history -> UserLoginHistoryResponse.builder()
                            .id(history.getId())
                            .loginAt(history.getLoginAt())
                            .ipAddress(history.getIpAddress())
                            .build())
                    .collect(Collectors.toList());
        }
    }
    ```

    </details>

- util
    <details>
    <summary>&#91;코드&#93; JwtUtil</summary>

    <a id="33eeda9b0fe180258e73ed1cd658740b"></a>

    ```java
    package com.example.userservice.util;

    import io.jsonwebtoken.Claims;
    import io.jsonwebtoken.JwtException;
    import io.jsonwebtoken.Jwts;
    import io.jsonwebtoken.security.Keys;
    import java.nio.charset.StandardCharsets;
    import java.util.Date;
    import javax.crypto.SecretKey;
    import org.springframework.beans.factory.annotation.Value;
    import org.springframework.stereotype.Component;

    @Component
    public class JwtUtil {

        private final SecretKey key;
        private final long accessTokenValidityInMs;
        private final long refreshTokenValidityInMs;

        public JwtUtil(
                @Value("${jwt.secret}") String secret,
                @Value("${jwt.access-token-validity-in-seconds}") long accessTokenValidityInSeconds,
                @Value("${jwt.refresh-token-validity-in-seconds}") long refreshTokenValidityInSeconds) {
            this.key = Keys.hmacShaKeyFor(secret.getBytes(StandardCharsets.UTF_8));
            this.accessTokenValidityInMs = accessTokenValidityInSeconds * 1000;
            this.refreshTokenValidityInMs = refreshTokenValidityInSeconds * 1000;
        }

        public String generateAccessToken(String email, Long userId) {
            return Jwts.builder()
                    .subject(email)
                    .claim("userId", userId)
                    .issuedAt(new Date())
                    .expiration(new Date(System.currentTimeMillis() + accessTokenValidityInMs))
                    .signWith(key)
                    .compact();
        }

        public String generateRefreshToken(String email, Long userId) {
            return Jwts.builder()
                    .subject(email)
                    .claim("userId", userId)
                    .issuedAt(new Date())
                    .expiration(new Date(System.currentTimeMillis() + refreshTokenValidityInMs))
                    .signWith(key)
                    .compact();
        }

        public boolean validateToken(String token) {
            try {
                Jwts.parser().verifyWith(key).build().parseSignedClaims(token);
                return true;
            } catch (JwtException | IllegalArgumentException e) {
                return false;
            }
        }

        public Claims getClaims(String token) {
            return Jwts.parser()
                    .verifyWith(key)
                    .build()
                    .parseSignedClaims(token)
                    .getPayload();
        }

        public String getEmailFromToken(String token) {
            return getClaims(token).getSubject();
        }

        public Long getUserIdFromToken(String token) {
            return getClaims(token).get("userId", Long.class);
        }
    }
    ```

    </details>
