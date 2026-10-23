---
order: 46
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 3a0eda9b-0fe1-8366-8827-8159a8fe5ab2
title: 이미지 업로드 url 생성
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 150eda9b-0fe1-80f6-a291-ebca5668faf2
    title: 11.  최종 프로젝트
  - id: 4a8eda9b-0fe1-820f-a7ac-81d28aefb5a9
    title: API 명세서
  - id: 3a0eda9b-0fe1-8366-8827-8159a8fe5ab2
    title: 이미지 업로드 url 생성
excerpt: "요청 응답 예시 --- 해당하는 값이 없는 경우, 테이블 삭제 후 None 명시 요청 - Path Variable: None - Parameter : None - Header: | - | 이름 | 타입 | 설명 | | --- | --- | --- | --- | | 1 | Authorization | String | Bea"
cover: null
icon: null
notionProperties:
  대분류: 파일
  확인: 완료
  URL: /api/file-url
  개발: 완료
  method: POST
schema_version: 1
parent_id: 4a8eda9b-0fe1-820f-a7ac-81d28aefb5a9
created: 2026-04-01T05:37:27.150Z
updated: 2026-04-01T05:37:27.150Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/11.  최종 프로젝트-ebca5668faf2/API 명세서-81d28aefb5a9/이미지 업로드 url 생성-8159a8fe5ab2/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/3a0eda9b0fe1836688278159a8fe5ab2
---
<a id="ab5eda9b0fe182d3826f81adc74829cb"></a>

## 요청 응답 예시

---

> 해당하는 값이 없는 경우,  테이블 삭제 후 <code>None</code> 명시

<a id="238eda9b0fe18230a40b0171be92c6b6"></a>

### 요청 

- Path Variable&#58; <code>None</code>

- Parameter &#58; <code>None</code>

- Header&#58;
    | &#45; | 이름 | 타입 | 설명 |
    | --- | --- | --- | --- |
    | 1 | Authorization  | String | Bearer token, 토큰 헤더 |
    | 2 | Content&#45;Type | application/json | 컨텐츠 타입 |

- Body&#58; 
    | &#45; | 이름 | 타입 | Nullable | 설명 |
    | --- | --- | --- | --- | --- |
    | 1 | fileName | String |  | 파일 이름 |

- HTTP 요청
    <a id="71feda9b0fe182eaa92981763158ffbe"></a>

    ```plaintext
    [ Method ] [ URI ] [ HTTP Version ] 

    ex) POST /api/file-url  HTTP1.1
    ```

    <details>
    <summary>요청 예시 </summary>

    <a id="b76eda9b0fe18212ad3e8134204f4830"></a>

    ```json
    {
        "fileName": "asd.png"
    }
    ```

    </details>

<a id="e4deda9b0fe182248dc481e4f96961c0"></a>

### 응답

- Header&#58;
    | &#45; | 이름 | 타입 | 설명 |
    | --- | --- | --- | --- |
    | 1 | Content&#45;Type | application/json | 컨텐츠 타입 |

- Body&#58; 
    | &#45; | 이름 | 타입 | Nullable | 설명 |
    | --- | --- | --- | --- | --- |
    | 1 | message | String | None | 응답 메세지 |
    | 2 | data |  | None | 응답 Dto |

    <details>
    <summary>DTO&#58; </summary>

    | &#45; | 이름 | 타입 | Nullable | 설명 |
    | --- | --- | --- | --- | --- |
    | 1 | id | Long | None | — 식별자 |
    |  | createdAt | Timestamp | None | 생성 일자 |
    |  | updatedAt | Timestamp | None | 수정 일자 |

    </details>

    <details>
    <summary>응답 예시 </summary>

    <a id="f6beda9b0fe182a8aa588113a6050a5a"></a>

    ```json
    {
        "message": "url 생성 완료",
        "data": {
            "url": "https://connect-images1.s3.ap-northeast-2.amazonaws.com/f7544a42-c6cf-4169-ae59-626b1a68ae8b_asd.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20250107T065007Z&X-Amz-SignedHeaders=host&X-Amz-Credential=AKIAQQABDRWEFXHHKE5M%2F20250107%2Fap-northeast-2%2Fs3%2Faws4_request&X-Amz-Expires=600&X-Amz-Signature=7f53d57583d8f109709b0bcd7ca1a8f4701650428f3a0ebaeabf62726ba232f2",
            "fileName": "f7544a42-c6cf-4169-ae59-626b1a68ae8b_asd.png"
        }
    }
    ```

    </details>

- HTTP Status
    |  &#45; | 상태코드  | 상태 메세지 | 설명 |
    | --- | --- | --- | --- |
    | 1 | <code>200 </code> | <code>OK</code> | 성공 |
    | 2 | <code>400</code> | <code>Bad Request</code> | 잘못된 요청 |
    | 3 | <code>401</code> | <code>Unauthorized</code> | 인가되지 않은 요청 |
    | 4 | <code>404</code> | <code>Not Found</code> | 해당 정보 찾을 수 없음 |

<a id="c18eda9b0fe183de87f301925f953174"></a>

### Exception
