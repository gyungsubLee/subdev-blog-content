---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 348eda9b-0fe1-8044-aaed-d734ae733cb6
title: Elastic Cloud를 활용한 구축
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 346eda9b-0fe1-8009-8dce-dab63413d77f
    title: ElasticSearch
  - id: 346eda9b-0fe1-805b-bb2f-c81770700aff
    title: "[인프런] 실전에서 바로 써먹는 Elasticsearch 입문 (검색 최적화편)"
  - id: 348eda9b-0fe1-8044-aaed-d734ae733cb6
    title: Elastic Cloud를 활용한 구축
excerpt: 목차 - Elastic Cloud를 활용한 구축 - AWS OpenSearch vs Elastic Cloud - Elastic Cloud에서 Elasticsearch 생성 - Spring Boot에 Elasitc Cloud의 Elasticsearch 연결 Elastic Cloud를 활용한 구축 --- 🤔 현업에서는 El
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 346eda9b-0fe1-805b-bb2f-c81770700aff
created: 2026-04-20T01:37:31.413Z
updated: 2026-04-29T14:39:43.641Z
legacy_path: Main/ElasticSearch-dab63413d77f/[인프런] 실전에서 바로 써먹는 Elasticsearch 입문 (검색 최적화편)-c81770700aff/Elastic Cloud를 활용한 구축-d734ae733cb6/index.md
legacy_category: ElasticSearch
source_url: https://beautiful-college-c84.notion.site/348eda9b0fe18044aaedd734ae733cb6
---
> 
> 
> <a id="348eda9b0fe180398d58d9606c1c9206"></a>
> 
> 목차
> 
> - [Elastic Cloud를 활용한 구축](#348eda9b0fe180d6956ac55be1fd508b)
> - [AWS OpenSearch vs Elastic Cloud](#34deda9b0fe180aabba4d0d12905bef0)
> - [Elastic Cloud에서 Elasticsearch 생성](#34eeda9b0fe180fbafd0e313e2e84697)
> - [Spring Boot에 Elasitc Cloud의 Elasticsearch 연결](#34eeda9b0fe180848a12f16902042a2e)

<a id="348eda9b0fe180d6956ac55be1fd508b"></a>

## <strong>Elastic Cloud를 활용한 구축</strong>

---

> 🤔 
> 
> <a id="34deda9b0fe1803fbc16e04bfae8e24a"></a>
> 
> <strong>현업에서는 Elasticsearch를 어떻게 운영하는가?</strong>
> 
> <a id="34deda9b0fe1807ab849e647bb24c734"></a>
> 
> 현업에서는 Elasticsearch를 직접 설치해서 운영하기도 하지만, 많은 경우 <strong><code>AWS OpenSearch</code></strong>나 <strong><code>Elastic Cloud</code></strong> 같은 서비스를 활용해 구축한다&#46;
> 
> - Elasticsearch를 구축하려면 단순히 설치만 하면 끝나는 게 아니라, 운영과 모니터링, 장애 대응, 확장, 보안 설정 등 많은 요소를 신경써서 구축하고 관리해야한다&#46; 
> 
> - 따라서 이를 알아서 관리해주는 외부 서비스도 많이 사용한다&#46;

> 
> 
> <a id="34eeda9b0fe180efa92dc7df06a0f2ff"></a>
> 
> <strong>Elastic Cloud 비용</strong>
> 
> - 시간당 0&#46;0311 USD (24시간당 약 1000원)
> 
> - Elastic Cloud를 처음 사용하는 유저 → 14일 간 무료 사용 가능

<a id="34deda9b0fe180aabba4d0d12905bef0"></a>

### <code>AWS OpenSearch</code> vs <code>Elastic Cloud</code>

<a id="34deda9b0fe18033a294d4cd74556f03"></a>

Elasticsearch는 처음에는 ‘오픈소스’였으나 2021년 1월 이후로 새로운 라이선스를 부과하면서 자유로운 활용이 금지되었다&#46;

<a id="34deda9b0fe1805ab4f7ff61b8509cef"></a>

따라서 AWS에서는 오픈소스로 활용 가능했던 Elasticsearch 7&#46;10&#46;2 버전을 포크(fork)하여 자체적인 검색엔진을 개발하기 시작하였고 그게 바로 <code>OpenSearch</code>이다&#46; 

- Elasticsearch와 OpenSearch가 가진 대부분의 기능은 비슷하다&#46; <br>하지만 시간이 흐르면서 버전이 업데이트 됨에 따라 기능이나 사용법의 차이가 조금씩 생기게 됐다&#46; 

<a id="34deda9b0fe180d7b922fd69cb92177e"></a>

이런 배경에 의해 AWS Opensearch Service는 Opensearch라는 독자적인 검색 엔진을 사용하고, Elastic Cloud는 지금까지 배운 Elasticsearch의 검색 엔진을 사용한다&#46;

<a id="34eeda9b0fe180fbafd0e313e2e84697"></a>

### Elastic Cloud에서 Elasticsearch 생성

[Elastic Cloud&#58; 호스트형 Elasticsearch, 호스트형 Search &#124; Elastic]()

> 💬 
> 
> <a id="34eeda9b0fe180b2b143f8a9e0fca191"></a>
> 
> 현재(26&#46;04&#46;26) 2가지 유형의 인스턴스가 존재한다&#46; 
> 
> - <code>Hosted Deployments</code>
> 
> - <code>Serverless</code>

<details>
<summary><strong>회원가입</strong></summary>

![](7f02a92110041161.webp)

<a id="34eeda9b0fe18051b659e06de0220908"></a>

<strong>기본 정보 입력</strong>

![](af091bdf6631efd6.webp)

</details>

<details>
<summary><strong>인스턴스 생성 1 &#45; </strong><strong><code>hosted deployments</code></strong></summary>

![](186241b2a9de9560.webp)

![](029222e69a0899f5.webp)

![](ce5bf3cfc312c266.webp)

<a id="34eeda9b0fe180af82e9f06d4c948a96"></a>

원하는 옵션을 선택하여 인스턴스 생성이 가능하다&#46; 

![](fbafbcb729ac279c.webp)

<a id="34eeda9b0fe180fbb417c97b08c600a3"></a>

위 화면과 같이 elasticsearch 연결 시 필요한 <code>user</code>, <code>password</code>를 알려준다&#46; <br>이를 통해 이후 spring에서의 인증 정보로써 접속하면 된다&#46;

- 생성 후, initialize가 되기까지 약간의 시간이 걸린다&#46; 
    ![](1c8b17e03815e182.webp)

    ![](43dba63a514ffdeb.webp)

    - <code>pending</code> → <code>healthy</code>

</details>

<details>
<summary><strong>인스턴스 생성 2&#45; </strong><strong><code>Serverless</code></strong></summary>

![](f175f60cf74455ec.webp)

![](3f743f15b5163608.webp)

<a id="34eeda9b0fe180509e91d9b7d9e1f838"></a>

원하는 옵션을 선택하여 인스턴스 생성

![](8320e735477bc1e4.webp)

<a id="34eeda9b0fe180c68676eb0687e6c906"></a>

초기화까지 1 &#126; 2분 정도의 시간이 걸린다&#46; 

![](803c542b52e0ecc7.webp)

![](9e044d100ef6fba0.webp)

<a id="34eeda9b0fe18074badfc7297028a433"></a>

초기화 완료(<code>general</code>) 후 kinbana 대시보드에 접속하여 관리할 수 있다&#46;

</details>

<details>
<summary><strong><code>hosted deployments</code></strong><strong> 비밀번호 관리</strong></summary>

> ✏️ 
> 
> <a id="34eeda9b0fe18028a3ece5ef7dc4770f"></a>
> 
> <code>hosted deployments</code>는 초기화 시 인증 정보를 알려준다&#46; <br>이를 <strong><u>해당 인스턴스 연결</u></strong>에 대한 <strong><u>인증 정보로 활용</u></strong>한다&#46; 
> 
> - 초기화 가능

![](fbafbcb729ac279c.webp)

<a id="34eeda9b0fe1802f9ddaefc280498a1e"></a>

<strong>Password 초기화 </strong>

![](d94c0d7ac17b769e.webp)

![](8faebed224e3b54d.webp)

</details>

<details>
<summary><strong>인스턴스 삭제</strong></summary>

![](963361d355dd6194.webp)

![](32968c5c985c6812.webp)

![](587b0605bd4e8fc8.webp)

</details>

<a id="34eeda9b0fe180848a12f16902042a2e"></a>

### Spring Boot에 Elasitc Cloud의 Elasticsearch 연결

> ✏️ 
> 
> <a id="34eeda9b0fe18056a914fbb3710377cd"></a>
> 
> Spring Boot에 Elastic Cloud의 Elasicsearch를 연결하기 위해서는 아래 3가지가 필요하다&#46; 
> 
> - <code>endpoint</code>
> 
> - <code>username</code>
> 
> - <code>password</code>

<details>
<summary><strong>1&#46; nori analyzer 플러그인 셋팅</strong></summary>

![](14bf62b153872a84.webp)

- 해당 인스턴스의 setting 화면 접속 후 위 클릭

![](64a7b5f9eb1bec46.webp)

- <code>extensions</code> 선택 후 <code>analysis&#45;nori</code> 추가

![](488ac162d75482b9.webp)

- <code>save</code> 필수

</details>

<details>
<summary><strong>2&#46; Elasticsearch 주소(Endpoint) 확인</strong></summary>

![](6f47922615c0bed9.webp)

</details>

<details>
<summary><strong>3&#46; username, password 확인</strong></summary>

![](fbafbcb729ac279c.webp)

<a id="34eeda9b0fe180fcab11d93fd845c379"></a>

<code>uesrname</code>과 <code>password</code>는 인스터스 초기 생성 시 확인 가능하다&#46;

<details>
<summary>만약 잃어버렸다면 reset 하면 된다&#46; </summary>

![](d94c0d7ac17b769e.webp)

![](8faebed224e3b54d.webp)

- reset 시, 새로운 비밀번호가 생성되며 화면과 같이 확인할 수 있다&#46; 

</details>

</details>

<details>
<summary><strong>4&#46; Spring Boot 프로젝트에 생성한 Elasticsearch 정보 입력</strong></summary>

<a id="34eeda9b0fe180058527c7c3cded1e4c"></a>

<strong>application&#46;yml</strong>

<a id="34eeda9b0fe180e68541f02d6427eded"></a>

```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/coupang
    username: root
    password: password123
    driver-class-name: com.mysql.cj.jdbc.Driver
  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
  elasticsearch:
    uris: https://test-679299.es.ap-northeast-2.aws.elastic-cloud.com
    username: elastic
    password: 9osL2aevaESTBbvAASObPcnu

logging:
  level:
    org.elasticsearch.client: TRACE
```

- 위에서 확인한 <code>endpoint</code>, <code>username</code>, <code>password</code>를 <code>application&#46;yml</code>에 설정

</details>

<details>
<summary><strong>5&#46; Elasticsearch에 잘 연결됐는 지 테스트</strong></summary>

- spring boot 서버 실행
    <a id="34eeda9b0fe180988802e7da57d085db"></a>

    ```yaml
    ./gradlew bootRun
    ```

    ![](70b8ff33f6abcacc.webp)

- <strong>Kibana에서 인덱스 조회</strong>
    ![](381733fd59ffb27d.webp)

    <a id="34eeda9b0fe180d5b2a9d31ba56a2443"></a>

    정상 연결되어 조회되는 것을 확인할 수 있다&#46; 

</details>
