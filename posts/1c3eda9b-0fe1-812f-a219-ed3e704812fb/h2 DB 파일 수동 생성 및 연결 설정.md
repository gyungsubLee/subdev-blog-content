---
order: 11
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-812f-a219-ed3e704812fb
title: h2 DB 파일 수동 생성 및 연결 설정
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-8103-b16c-ff13884ad0ba
    title: 자바 ORM 표준 JPA 프로그래밍 - 기본
  - id: 1c3eda9b-0fe1-812f-a219-ed3e704812fb
    title: h2 DB 파일 수동 생성 및 연결 설정
excerpt: 강의를 따라하다가 2번째 DB(jpashop)를 생성 및 연결에서 자꾸 오류가 나서 수동으로 파일 생성해서 해결함 DB 파일 수동 생성 /Users/igyeongseob/ (기본 시작) 경로에 수동으로 DB 파일(jpashop.mv.db) 생성 shell touch jpashop.mv.db h2 DB 시작 설정 - ini
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8103-b16c-ff13884ad0ba
created: 2025-03-27T07:53:11.120Z
updated: 2025-03-27T07:53:11.120Z
legacy_path: Main/Spring ( Java )-cd1f71740107/자바 ORM 표준 JPA 프로그래밍 - 기본-ff13884ad0ba/h2 DB 파일 수동 생성 및 연결 설정-ed3e704812fb/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1812fa219ed3e704812fb
---
<a id="1c3eda9b0fe18103a2caf2bb6de30eca"></a>

강의를 따라하다가 2번째 DB(jpashop)를 생성 및 연결에서 자꾸 오류가 나서 수동으로 파일 생성해서 해결함 

<a id="1c3eda9b0fe18179be0dc40729a853ea"></a>

### DB 파일 수동 생성

<a id="1c3eda9b0fe1817dbebee4506874d72b"></a>

<strong><code>/Users/igyeongseob/</code></strong> (기본 시작) 경로에 <strong><u>수동으로 DB 파일(</u></strong><strong><u><code>jpashop&#46;mv&#46;db</code></u></strong><strong>) </strong><strong><u>생성</u></strong>

<a id="1c3eda9b0fe1816f9fe3fefa797e2a9d"></a>

```shell
touch jpashop.mv.db
```

<a id="1c3eda9b0fe181938fd8c27b58d68c8b"></a>

### h2 DB 시작 설정

- initialize 설정

![](5ee79028ffa41457.webp)

- 이후 접속 시 설정

![](88e31bf8fb51ab30.webp)

<a id="1c3eda9b0fe181bd8271f9f18bab86bd"></a>

### hibernate &#45; DB 경로 설정하기

> 두 경로 동일하게 작성 후 접속 

![](0f6c2bf907a210bb.webp)

![](e91cd09afb003dac.webp)

> JapMain 실행 시, 아래와 같이 정상적으로 쿼리 날림

![](64af1127bc883adb.webp)
