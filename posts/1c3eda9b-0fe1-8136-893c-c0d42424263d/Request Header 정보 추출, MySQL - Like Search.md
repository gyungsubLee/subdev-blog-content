---
order: 25
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8136-893c-c0d42424263d
title: Request Header 정보 추출, MySQL - Like Search
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-812e-b8ac-c13c536efd00
    title: Spring Boot를 활용한 채팅 서비스 만들어보기
  - id: 1c3eda9b-0fe1-8136-893c-c0d42424263d
    title: Request Header 정보 추출, MySQL - Like Search
excerpt: "MySQL - LOCATE ✏️ MySQL에서 문자열 내에서 특정 하위 문자열의 위치를 반환하는 함수 - 주로 문자열 검색에 사용 sql LOCATE(substring, string, [startposition]) - substring: 찾고자 하는 하위 문자열 - string: 검색 대상이 되는 문자열 - start_p"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 1c3eda9b-0fe1-812e-b8ac-c13c536efd00
created: 2025-03-27T07:53:11.124Z
updated: 2025-03-27T07:53:11.124Z
legacy_path: Main/Spring ( Java )-cd1f71740107/Spring Boot를 활용한 채팅 서비스 만들어보기-c13c536efd00/Request Header 정보 추출, MySQL - Like Search-c0d42424263d/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18136893cc0d42424263d
---
<details>
<summary>MySQL &#45; LOCATE</summary>

> ✏️ 
> 
> <a id="1c3eda9b0fe181d78bdece22e408e6a2"></a>
> 
> MySQL에서 문자열 내에서 특정 하위 문자열의 위치를 반환하는 함수
> 
> - 주로 문자열 검색에 사용

<a id="1c3eda9b0fe18189bb53d8ffdcfc65d0"></a>

```sql
LOCATE(substring, string, [start_position])
```

- <code>substring</code>&#58; 찾고자 하는 하위 문자열

- <code>string</code>&#58; 검색 대상이 되는 문자열

- <code>start&#95;position</code>(선택)&#58; 검색을 시작할 위치(기본값&#58; <code>1</code> )

- 동작 방식
    - LOCATE는 string에서 substring의 첫 번째 위치를 1부터 시작하는 인덱스로 반환한다&#46;

    - substring이 존재하지 않으면 0을 반환

    - start&#95;position이 지정되면 해당 위치부터 검색을 시작

- 활용 예제
    <details>
    <summary>1) 이메일 주소에서 &#64; 뒤의 도메인 이름을 가져오기</summary>

    <a id="1c3eda9b0fe1813c9239d914aae93814"></a>

    ```sql
    SELECT SUBSTRING(email, LOCATE('@', email) + 1) AS domain
    FROM users;
    ```

    - LOCATE(&#39;&#64;&#39;, email)은 &#64;의 위치를 반환하며, &#43;1은 그 이후의 문자열을 가져온다&#46;

    </details>

    <details>
    <summary>2) 문자열이 특정 단어를 포함하는지 확인</summary>

    <a id="1c3eda9b0fe181ecbf5bc4a9998a311b"></a>

    ```sql
    SELECT *
    FROM products
    WHERE LOCATE('special', description) > 0;
    ```

    - description 필드에 special이라는 단어가 포함된 행만 반환

    </details>

    <details>
    <summary>3) <strong>URL에서 쿼리 파라미터 추출</strong></summary>

    <a id="1c3eda9b0fe18154a013d91ed602e4bc"></a>

    ```sql
    SELECT SUBSTRING(url, LOCATE('?', url) + 1) AS query_params
    FROM requests
    WHERE LOCATE('?', url) > 0;
    ```

    </details>

    <details>
    <summary>4) 강의 예시, 툭정 패턴을 가지는 유저 정보 검색</summary>

    <a id="1c3eda9b0fe1816a8652ec02b74fd1fb"></a>

    ```sql

    ```

    </details>

</details>
