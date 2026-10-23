---
order: 12
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8138-bba8-e11a4ba342d3
title: ERD
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
    title: 대규모 시스템 설계
  - id: 1c3eda9b-0fe1-8151-a9bf-f4bde443f283
    title: 대규모 시스템 설계 - 게시판
  - id: 1c3eda9b-0fe1-8138-bba8-e11a4ba342d3
    title: ERD
excerpt: ERD --- 분산 DB를 가정하기 때문에 게시글이 N 개의 샤드 로 분산되는 상황을 고려한다. - 샤딩을 직접 구현하지는 않지만 ( 추가로 진행 하기 ) Shard Key = board_id ( 게시판 ID )로 가정한다. - 게시글 테이블 생성 sql CREATE TABLE article ( articleid BIGI
cover: null
icon: null
notionProperties:
  소분류: ERD
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8151-a9bf-f4bde443f283
created: 2025-03-27T07:52:18.662Z
updated: 2025-03-27T07:52:18.662Z
legacy_path: Main/대규모 시스템 설계-d6a1706fbaf8/대규모 시스템 설계 - 게시판-f4bde443f283/ERD-e11a4ba342d3/index.md
legacy_category: 대규모 시스템 설계
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18138bba8e11a4ba342d3
---
<a id="1c3eda9b0fe181e1b111dab59d4bd6c1"></a>

### ERD

---

![‣](b9d7f749d7e1f17f.webp)

<a id="1c3eda9b0fe181fba58ad32d844c056c"></a>

분산 DB를 가정하기 때문에 게시글이   N 개의 샤드 로 분산되는 상황을 고려한다&#46; 

- 샤딩을 직접 구현하지는 않지만 ( 추가로 진행 하기 )<br><strong><u>Shard Key</u></strong> = <strong><u>board&#95;id</u></strong> ( 게시판 ID )로 가정한다&#46; 

- 게시글 테이블 생성
    <a id="1c3eda9b0fe181348ec9f403fd27e0fe"></a>

    ```sql
    CREATE TABLE article (
        article_id BIGINT NOT NULL PRIMARY KEY,
        title VARCHAR(100) NOT NULL,
        content VARCHAR(3000) NOT NULL,
        board_id BIGINT NOT NULL,
        writer_id BIGINT NOT NULL,
        created_at DATETIME NOT NULL,
        modified_at DATETIME NOT NULL
    );
    ```
