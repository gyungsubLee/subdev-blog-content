---
order: 25
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 152eda9b-0fe1-802c-8efc-de91dbcf258a
title: 예외처리 - 각 레이어에서 분리해서 관리하기 및 enum 값으로 각 단일 클래스에서 공통으로 처리하기
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 14aeda9b-0fe1-80f2-a26e-d08048767e3b
    title: 8. 아웃소싱 프로젝트
  - id: 152eda9b-0fe1-802c-8efc-de91dbcf258a
    title: 예외처리 - 각 레이어에서 분리해서 관리하기 및 enum 값으로 각 단일 클래스에서 공통으로 처리하기
excerpt: 예외처리 코드 --- java package com.example.koobaeyo.stores.exception; import com.example.koobaeyo.stores.exception.code.StoreErrorCode; public class StoreBaseException extends RuntimeExc
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 14aeda9b-0fe1-80f2-a26e-d08048767e3b
created: 2024-12-04T07:25:05.022Z
updated: 2024-12-04T07:41:01.342Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/8. 아웃소싱 프로젝트-d08048767e3b/예외처리 - 각 레이어에서 분리해서 관리하기 및 enum 값으로 각 단일 클래스에-de91dbcf258a/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/152eda9b0fe1802c8efcde91dbcf258a
---
<a id="152eda9b0fe180d9a4e1e32afbc84699"></a>

### 예외처리 코드 

---

<a id="152eda9b0fe180dab619d7ed7ecf44cf"></a>

```java
package com.example.koobaeyo.stores.exception;

import com.example.koobaeyo.stores.exception.code.StoreErrorCode;

public class StoreBaseException extends RuntimeException {
    private final StoreErrorCode errorCode;

    public StoreBaseException(StoreErrorCode errorCode) {
        super(errorCode.getMessage());
        this.errorCode = errorCode;
    }

    public StoreBaseException(String message, StoreErrorCode errorCode) {
        super(message);
        this.errorCode = errorCode;
    }
}

```

- enum

<a id="152eda9b0fe180a4b46ad4156753ce4d"></a>

```java
package com.example.koobaeyo.stores.exception.code;

import lombok.AllArgsConstructor;
import lombok.Getter;
import org.springframework.http.HttpStatus;

@Getter
@AllArgsConstructor
public enum StoreErrorCode {


    /**
     * Server
     */
    VALIDATION_ERROR(HttpStatus.BAD_REQUEST, "유효성 검사 실패"),
    CONSTRAINT_VIOLATION(HttpStatus.CONFLICT, "제약 조건 위반"),
    INTERNAL_SERVER_ERROR(HttpStatus.INTERNAL_SERVER_ERROR, "내부 서버 오류가 발생하였습니다."),

    /**
     * Common
     */
    NOT_FOUND_ENUM_CONSTANT(HttpStatus.NOT_FOUND, "열거형 상수값을 찾을 수 없습니다."),
    IS_NULL(HttpStatus.BAD_REQUEST, "NULL 값이 들어왔습니다."),
    COMMON_INVALID_PARAM(HttpStatus.BAD_REQUEST, "요청한 값이 올바르지 않습니다."),
    NO_SUCH_METHOD(HttpStatus.BAD_REQUEST, "메소드를 찾을 수 없습니다."),

    /**
     * Store
     */
     IS_NOT_OWNER(HttpStatus.FORBIDDEN, "사장 권한이 없습니다!"),
     CANNOT_OPEN_STORE(HttpStatus.FORBIDDEN, "가게를 열수 없습니다!"),
     CANNOT_REMODEL_OTHERS(HttpStatus.FORBIDDEN, "타인의 가게를 리모델링할 수 없습니다!"),
     CANNOT_CLOSEDOWN_OTHERS(HttpStatus.FORBIDDEN,"타인의 가게를 폐업할 수 없습니다!"),
     NOT_FOUND_STORE(HttpStatus.NOT_FOUND, "가게를 찾을 수 없습니다!");



    private final HttpStatus httpStatus;
    private final String message;
}

```

- 사용

<a id="152eda9b0fe180dcb943de9190c47098"></a>

```java
Store store = storeRepository.findById(storeId).orElseThrow(
        () -> new StoreBaseException(StoreErrorCode.NOT_FOUND_STORE));
```

<a id="152eda9b0fe180beb052f1d151e7fcb9"></a>

```java

if(!Objects.equals(store.getOwner().getId(), user.getId())){
    throw new StoreBaseException(StoreErrorCode.CANNOT_CLOSEDOWN_OTHERS);
}
```
