---
order: 2
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81d1-b646-c18c81213091
title: IntelliJ에서의 환경변수 설정
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 305eda9b-0fe1-80cb-881b-e0f1ba2b631b
    title: Tool
  - id: 1c3eda9b-0fe1-8170-a8d2-f7ba2392ba91
    title: IntelliJ
  - id: 1c3eda9b-0fe1-81d1-b646-c18c81213091
    title: IntelliJ에서의 환경변수 설정
excerpt: "- run - edit configuration - Modify options - 환경 변수로 등록할 key, value 입력 - 직접 동시에 입력 javascript DATABASEHOST=localhost;DATABASENAME=connect;DATABASEPASSWORD=12345678;DATABASEPORT=330"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 1c3eda9b-0fe1-8170-a8d2-f7ba2392ba91
created: 2025-03-27T08:23:20.621Z
updated: 2025-03-27T08:23:20.621Z
legacy_path: Main/Tool-e0f1ba2b631b/IntelliJ-f7ba2392ba91/IntelliJ에서의 환경변수 설정-c18c81213091/index.md
legacy_category: Tool
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181d1b646c18c81213091
---
- run &#45; edit configuration
    ![](2c4c12bcff313e61.webp)

- Modify options
    ![](98c76abc8bd9ad02.webp)

- 환경 변수로 등록할 key, value 입력
    ![](634ef74216a8a5c5.webp)

- 직접 동시에 입력
    ![](874ef593d6b7c116.webp)



<a id="1c3eda9b0fe181c58994d878e0d70442"></a>

```javascript
DATABASE_HOST=localhost;DATABASE_NAME=connect;DATABASE_PASSWORD=12345678;DATABASE_PORT=3306;DATABASE_USERNAME=root;
```



- applications&#46;properties
    <a id="1c3eda9b0fe1816bbd53d3970f40cb32"></a>

    ```javascript
    spring.application.name=Connect
    spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
    spring.datasource.url=jdbc:mysql://${DATABASE_HOST}:${DATABASE_PORT}/${DATABASE_NAME}
    spring.datasource.username=${DATABASE_USERNAME}
    spring.datasource.password=${DATABASE_PASSWORD}
    spring.jpa.show-sql=true
    spring.jpa.database-platform=org.hibernate.dialect.MySQL8Dialect
    # create, update, none, creat-drop
    spring.jpa.database=mysql
    spring.jpa.hibernate.ddl-auto=create
    spring.jpa.hibernate.naming.physical-strategy=org.hibernate.boot.model.naming.CamelCaseToUnderscoresNamingStrategy
    spring.jpa.generate-ddl=false
    spring.jpa.properties.hibernate.format_sql=true
    spring.jpa.properties.hibernate.enable_lazy_load_no_trans=true
    jwt.secret=jwt-secret-have-to-be-longer-than-32-characters
    jwt.expiry-millis=36000000
    jwt.refresh-expiry-millis=604800000
    aws.access-key=${AWS_ACCESS_KEY}
    aws.secret-key=${AWS_SECRET_KEY}
    aws.s3.bucket-name=${AWS_BUCKET_NAME}
    aws.s3.region=ap-northeast-2

    ```
