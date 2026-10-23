---
order: 1
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-814a-b668-c07fc66f8ab3
title: "로그인 오류 - ERROR 1045 (28000): Access denied …"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
    title: DBMS
  - id: 1c3eda9b-0fe1-81ef-9506-cdc300921ef3
    title: MySQL
  - id: 1c3eda9b-0fe1-814a-b668-c07fc66f8ab3
    title: "로그인 오류 - ERROR 1045 (28000): Access denied …"
excerpt: Reference https://passing-story.tistory.com/entry/MySQL-mysql로그인-오류-mysql-비밀번호-재설정 https://velog.io/@security_code/ERROR-1045-28000-Access-denied-for-user-rootlocalhost-using-passw
cover: null
icon: null
notionProperties:
  상태: 진행 중
schema_version: 1
parent_id: 1c3eda9b-0fe1-81ef-9506-cdc300921ef3
created: 2025-03-27T07:47:52.778Z
updated: 2025-03-27T07:47:52.778Z
legacy_path: Main/DBMS-e8c2debc9fa0/MySQL-cdc300921ef3/로그인 오류 - ERROR 1045 (28000)- Access denied …-c07fc66f8ab3/index.md
legacy_category: DBMS
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1814ab668c07fc66f8ab3
---
<details>
<summary>Reference</summary>

<a id="1c3eda9b0fe1816c80afd075c8ba1aec"></a>

<a href="https://passing-story.tistory.com/entry/MySQL-mysql%EB%A1%9C%EA%B7%B8%EC%9D%B8-%EC%98%A4%EB%A5%98-mysql-%EB%B9%84%EB%B0%80%EB%B2%88%ED%98%B8-%EC%9E%AC%EC%84%A4%EC%A0%95">https&#58;//passing&#45;story&#46;tistory&#46;com/entry/MySQL&#45;mysql로그인&#45;오류&#45;mysql&#45;비밀번호&#45;재설정</a>

<a id="1c3eda9b0fe181038602e080d1d7acea"></a>

<a href="https://velog.io/@security_code/ERROR-1045-28000-Access-denied-for-user-rootlocalhost-using-password-YES">https&#58;//velog&#46;io/&#64;security&#95;code/ERROR&#45;1045&#45;28000&#45;Access&#45;denied&#45;for&#45;user&#45;rootlocalhost&#45;using&#45;password&#45;YES</a><br><a href="https://velog.io/@taelee/mysql-user%ED%99%95%EC%9D%B8-%EB%B0%8F-%EC%B6%94%EA%B0%80">https&#58;//velog&#46;io/&#64;taelee/mysql&#45;user확인&#45;및&#45;추가</a>

<a id="1c3eda9b0fe181a1a37cfd03463484ba"></a>

<a href="https://vkein.tistory.com/entry/MySQL-%EC%A0%91%EC%86%8D-%EB%AA%85%EB%A0%B9%EC%96%B4">https&#58;//vkein&#46;tistory&#46;com/entry/MySQL&#45;접속&#45;명령어</a>

</details>

<a id="1c3eda9b0fe181b997edd813961d03be"></a>

### 오류

> ⚠️ <strong>ERROR 1045 (28000)&#58; Access denied for user &#39;root&#39;&#64;&#39;localhost&#39; (using password&#58; YES)</strong>
> 
> > <strong>root의 비번이 설정되지 않</strong>아 발생되는 오류이다&#46; 

<a id="1c3eda9b0fe1819fae98ed7a315001f3"></a>

<code>mysql &#45;u root &#45;p</code> 입력 후, 비밀번호 없이 접속(<code>Enter</code>) 시 정상 접속된다&#46; 

![](0aefd076b9179d7a.webp)

<a id="1c3eda9b0fe18116bb43ee4733e80bf9"></a>

### 비밀번호 설정하기
