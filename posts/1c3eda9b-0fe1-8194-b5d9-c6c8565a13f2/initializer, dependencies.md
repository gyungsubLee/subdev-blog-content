---
order: 8
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8194-b5d9-c6c8565a13f2
title: initializer, dependencies
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-812e-b8ac-c13c536efd00
    title: Spring Boot를 활용한 채팅 서비스 만들어보기
  - id: 1c3eda9b-0fe1-8194-b5d9-c6c8565a13f2
    title: initializer, dependencies
excerpt: 의존성 - build.gradle groovy dependencies { implementation 'org.springframework.boot:spring-boot-starter-web' // wss implementation 'org.springframework.boot:spring-boot-starter-webso
cover: null
icon: null
notionProperties:
  상태: 완료
  Tags: 1. 프로젝트 구성
schema_version: 1
parent_id: 1c3eda9b-0fe1-812e-b8ac-c13c536efd00
created: 2025-03-27T07:53:11.124Z
updated: 2025-03-27T07:53:11.124Z
legacy_path: Main/Spring ( Java )-cd1f71740107/Spring Boot를 활용한 채팅 서비스 만들어보기-c13c536efd00/initializer, dependencies-c6c8565a13f2/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18194b5d9c6c8565a13f2
---
<a id="1c3eda9b0fe181cf9f64c3b31bac638b"></a>

### 의존성 &#45; <code>build&#46;gradle</code>

<a id="1c3eda9b0fe181de86bbd3c385d90c16"></a>

```groovy
dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-web'

	// wss
	implementation 'org.springframework.boot:spring-boot-starter-websocket'
	implementation 'org.webjars:stomp-websocket:2.3.3-1'
	
	// lombok
	compileOnly 'org.projectlombok:lombok'
	annotationProcessor 'org.projectlombok:lombok'
	annotationProcessor 'org.projectlombok:lombok-mapstruct-binding:0.2.0'

	implementation 'org.springframework.boot:spring-boot-starter-jdbc'

	// redis
	implementation 'org.springframework.boot:spring-boot-starter-data-redis'

	// jwt
	implementation 'com.auth0:java-jwt:3.12.0'

	// Hashing
	implementation 'org.springframework.security:spring-security-core:5.8.3'
	
	// swagger
	implementation 'org.springdoc:springdoc-openapi-starter-webmv체 코 전c-ui:2.2.0'

	// mysql
	implementation 'com.mysql:mysql-connector-j:8.0.31'
	implementation 'org.springframework.boot:spring-boot-starter-data-jpa' 
    implementation 'mysql:mysql-connector-java:8.0.28'

	testImplementation 'org.springframework.boot:spring-boot-starter-test'
	testRuntimeOnly 'org.junit.platform:junit-platform-launcher'
}
```

<a id="1c3eda9b0fe1819d9531e1bc3e651304"></a>

<br>

<details>
<summary>전체 파일</summary>

<a id="1c3eda9b0fe1816bb5e6ec2bdef771a4"></a>

```java
plugins {
    id 'java'
    id 'org.springframework.boot' version '3.4.0'
    id 'io.spring.dependency-management' version '1.1.6'
}

group = 'com.example'
version = '0.0.1-SNAPSHOT'

java {
    toolchain {
        languageVersion = JavaLanguageVersion.of(17)
    }
}

configurations {
    compileOnly {
        extendsFrom annotationProcessor
    }
}

repositories {
    mavenCentral()
}

dependencies {
    // wss
    implementation 'org.springframework.boot:spring-boot-starter-websocket'
    implementation 'org.webjars:stomp-websocket:2.3.3-1'

//    // lombok
//    compileOnly 'org.projectlombok:lombok'
//    annotationProcessor 'org.projectlombok:lombok'
//    annotationProcessor 'org.projectlombok:lombok-mapstruct-binding:0.2.0'

    // redis
//    implementation 'org.springframework.boot:spring-boot-starter-data-redis'

    // jwt
    implementation 'com.auth0:java-jwt:3.12.0'

    // Hashing
    implementation 'org.springframework.security:spring-security-core:5.8.3'

    // swagger
    implementation 'org.springdoc:springdoc-openapi-ui:1.7.0'

    // jdbc
//    implementation 'org.springframework.boot:spring-boot-starter-jdbc'

    implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
    implementation 'org.springframework.boot:spring-boot-starter-validation'
    implementation 'org.springframework.boot:spring-boot-starter-web'
    compileOnly 'org.projectlombok:lombok'
    annotationProcessor 'org.projectlombok:lombok'

    runtimeOnly 'com.mysql:mysql-connector-j'

    testImplementation 'org.springframework.boot:spring-boot-starter-test'

    testRuntimeOnly 'org.junit.platform:junit-platform-launcher'
}

tasks.named('test') {
    useJUnitPlatform()
}


```

</details>

<a id="1c3eda9b0fe1810fb4f4ff7abdc60f87"></a>

### HTTP, 웹 소캣 Configuration

<details>
<summary>&#91; 코드 &#93; WebConfig</summary>

<a id="1c3eda9b0fe1819895dfefab5564522b"></a>

```java
package com.example.demo.config;

import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.CorsRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

@Configuration
public class WebConfig implements WebMvcConfigurer {
    
    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**") // 모든 경로 허용
                .allowedOriginPatterns("http://localhost:*")
                .allowedMethods("GET", "POST", "PUT", "DELETE")
                .allowedHeaders("*")
                .allowCredentials(true) // 자격 증명 허용
                .maxAge(3600); // preflight 요청 캐시 시간
    }
}
```

</details>

<details>
<summary>&#91; 코드 &#93; WssConfig</summary>

<a id="1c3eda9b0fe1816aadd6e5612ad04a13"></a>

```java
package com.example.demo.config;

import org.springframework.context.annotation.Configuration;
import org.springframework.messaging.simp.config.MessageBrokerRegistry;
import org.springframework.web.socket.config.annotation.EnableWebSocket;
import org.springframework.web.socket.config.annotation.EnableWebSocketMessageBroker;
import org.springframework.web.socket.config.annotation.StompEndpointRegistry;
import org.springframework.web.socket.config.annotation.WebSocketConfigurer;
import org.springframework.web.socket.config.annotation.WebSocketHandlerRegistry;
import org.springframework.web.socket.config.annotation.WebSocketMessageBrokerConfigurer;

import lombok.RequiredArgsConstructor;

@Configuration
@EnableWebSocketMessageBroker
public class WssConfig implements WebSocketMessageBrokerConfigurer {

    @Override
    public void configureMessageBroker(MessageBrokerRegistry registry) {
        registry.enableSimpleBroker("/sub");
        registry.setApplicationDestinationPrefixes("/pub");
    }

    @Override
    public void registerStompEndpoints(StompEndpointRegistry register ) {
        register.addEndpoint("/ws-stomp")
            .setAllowedOrigins("*");
    }


    // @Override
    // public void registerWebSocketHandlers(WebSocketHandlerRegistry registry) {
    //     registry.addHandler(null, "/ws/v1/chat")
    //         .setAllowedOrigins("*");  
    // }

    
}

```

</details>
