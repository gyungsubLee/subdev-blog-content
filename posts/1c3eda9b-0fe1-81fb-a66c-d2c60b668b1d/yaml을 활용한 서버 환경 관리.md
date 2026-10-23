---
order: 27
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81fb-a66c-d2c60b668b1d
title: yaml을 활용한 서버 환경 관리
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-812e-b8ac-c13c536efd00
    title: Spring Boot를 활용한 채팅 서비스 만들어보기
  - id: 1c3eda9b-0fe1-81fb-a66c-d2c60b668b1d
    title: yaml을 활용한 서버 환경 관리
excerpt: 'applications.yml + 환경변수 설정 - application.yml yaml server.port: 7002 springdoc: swagger-ui: enabled: true operation-sorter: method spring: config: import: "optional:file:.env[.prope'
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-812e-b8ac-c13c536efd00
created: 2025-03-27T07:53:11.123Z
updated: 2025-03-27T07:53:11.123Z
legacy_path: Main/Spring ( Java )-cd1f71740107/Spring Boot를 활용한 채팅 서비스 만들어보기-c13c536efd00/yaml을 활용한 서버 환경 관리-d2c60b668b1d/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181fba66cd2c60b668b1d
---
<a id="1c3eda9b0fe181908c58e839bb24d50d"></a>

### <code>applications&#46;yml</code> &#43; 환경변수 설정

- application&#46;yml
    <a id="1c3eda9b0fe18150a3e9c657e324cc95"></a>

    ```yaml
    server.port: 7002
    springdoc:
      swagger-ui:
        enabled: true
        operation-sorter: method
    spring:
      config:
        import: "optional:file:.env[.properties]"  # .env 프로젝트 root에 위치 
      datasource:
        url: ${DB_URL}
        username: ${DB_USERNAME}
        password: ${DB_PASSWORD}
        driver-class-name: ${DB_DRIVER}
      jpa:
        show-sql: true
    token:
      secret-key: ${TOKEN_SECRET_KEY}
      refresh-secret-key: ${REFRESH_SECRET_KEY}
      token-time: ${TOKEN_TIME}
      refresh-token-time: ${REFRESH_TOKEN_TIME}
    ```

- env
    <a id="1c3eda9b0fe181c78f58f9f53940f290"></a>

    ```yaml
    # Database Configuration
    DB_URL=jdbc:mysql://localhost:3306/spring_chatting
    DB_USERNAME=root
    DB_PASSWORD=12345678
    DB_DRIVER=com.mysql.cj.jdbc.Driver

    # Token Configuration
    TOKEN_SECRET_KEY=SECRET
    REFRESH_SECRET_KEY=REFRESH-SECRET
    TOKEN_TIME=300
    REFRESH_TOKEN_TIME=300
    ```
