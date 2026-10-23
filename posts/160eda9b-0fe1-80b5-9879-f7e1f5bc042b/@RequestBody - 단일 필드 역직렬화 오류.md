---
order: 1
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 160eda9b-0fe1-80b5-9879-f7e1f5bc042b
title: "@RequestBody - 단일 필드 역직렬화 오류"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 158eda9b-0fe1-80fa-96f1-eb2bd6377a5c
    title: 9.  플러스 주차 개인 프로젝트
  - id: 160eda9b-0fe1-80b5-9879-f7e1f5bc042b
    title: "@RequestBody - 단일 필드 역직렬화 오류"
excerpt: 오류 --- java @PatchMapping("/{id}/update-status") public ResponseEntity updateReservation(@PathVariable Long id, @RequestBody String status) { reservationService.updateReservationSt
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 158eda9b-0fe1-80fa-96f1-eb2bd6377a5c
created: 2024-12-18T20:16:24.954Z
updated: 2026-04-04T15:47:35.625Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/9.  플러스 주차 개인 프로젝트-eb2bd6377a5c/@RequestBody - 단일 필드 역직렬화 오류-f7e1f5bc042b/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/160eda9b0fe180b59879f7e1f5bc042b
---
<a id="160eda9b0fe18047892fc99a594ebc32"></a>

### 오류

---

<a id="160eda9b0fe180d7ad78fbf1e9b19880"></a>

```java
@PatchMapping("/{id}/update-status")
public ResponseEntity<String> updateReservation(@PathVariable Long id, @RequestBody String status) {
		reservationService.updateReservationStatus(id, status)
    return ResponseEntity.ok().body("정삭적으로 수정 되었습니다.");
}
```

<a id="160eda9b0fe180ac8f9bc540c3d78648"></a>

디버깅을 해보니 status 하나를 가져오는 &#64;RequestBody에서 역직렬화 오류가 발생되어 JSON 형태의 문자열을 그대로 받아온다는 것을 확인함

<a id="160eda9b0fe1800aad90cb9344f76518"></a>

```java
status = "{ "status": "APPROVED" }"
```

<a id="338eda9b0fe180578ff0f16e179ca2fa"></a>

### 원인 파악

---

<a id="338eda9b0fe180ba8cb9fab2902a8b34"></a>

&#64;RequestBody → JSON → DTO 변환  시, <strong>Jackson이 리플렉션으로 “어떤 생성자를 호출할지 결정”해야 하는데, 그 선택 기준에 걸리지 않아서 실패하는 것이다&#46;</strong>

<a id="338eda9b0fe180edb1edfbd74f0a3e37"></a>

즉, <strong>Jackson이 사용할 생성자를 찾지 못했기 때문이다&#46;</strong>

<a id="338eda9b0fe18032bc30f21151359715"></a>

따라서 기본 생성자를 명시해야 정상 객체 생성이 가능하다&#46;

<a id="160eda9b0fe18017b924f0f8af2b284e"></a>

### 해결

---

> 단일 필드를 받아올 DTO 생성 후, 해당 DTO에 기본 생성자 정의

- controller
    <a id="160eda9b0fe180be87f3e4568ae7c78a"></a>

    ```java
    @PatchMapping("/{id}/update-status")
    public ResponseEntity<String> updateReservation(@PathVariable Long id, @RequestBody updateReservationRequestDto requestDto) {
    	  reservationService.updateReservationStatus(id, requestDto.getStatus());
    	  return ResponseEntity.ok().body("정삭적으로 수정 되었습니다.");
    }
    ```

- DTO
    <a id="160eda9b0fe18030890cf5722bedf597"></a>

    ```java
    package com.example.demo.dto;

    import lombok.Getter;
    import lombok.NoArgsConstructor;

    @Getter
    @NoArgsConstructor
    public class updateReservationRequestDto {
        private String status;
    }

    ```

    - 기본 생성자 정의
