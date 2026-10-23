---
order: 3
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81ec-9c29-c627d7933597
title: "[ 실습 1 ] Redis 적용 전후, 성능 비교 ( postman )"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81b8-a968-f6b1b2a79b94
    title: Redis
  - id: 1c3eda9b-0fe1-81c7-ae23-cfbc9fd6e83a
    title: 비전공자도 이해할 수 있는 Redis - 캐싱 [ 리펙토링 필요 ]
  - id: 1c3eda9b-0fe1-81ec-9c29-c627d7933597
    title: "[ 실습 1 ] Redis 적용 전후, 성능 비교 ( postman )"
excerpt: Redis 적용 전후, 성능 비교 --- 📖 성능 개선을 할 때는 반드시 수치를 측정하여 비교해야 한다. 실제로 얼마나 느린지, 개선한 뒤 얼마나 빨라졌는 지를 측정해야 한다. 즉, 정확한 데이터(수치)로 표현해야 한다. Redis 적용 전 java @Service public class BoardService { ..
cover: null
icon: null
notionProperties:
  중요도: Yes
  상태: 중요!!
schema_version: 1
parent_id: 1c3eda9b-0fe1-81c7-ae23-cfbc9fd6e83a
created: 2025-03-27T07:47:52.772Z
updated: 2025-03-27T07:47:52.772Z
legacy_path: Main/Redis-f6b1b2a79b94/비전공자도 이해할 수 있는 Redis - 캐싱 [ 리펙토링 필요 ]-cfbc9fd6e83a/[ 실습 1 ] Redis 적용 전후, 성능 비교 ( postman )-c627d7933597/index.md
legacy_category: Redis
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181ec9c29c627d7933597
---
<a id="1c3eda9b0fe181ac8050c7d72a5c4335"></a>

## Redis 적용 전후, 성능 비교

---

> 📖 
> 
> <a id="1c3eda9b0fe181b6ba4dd2ff15cfcfbd"></a>
> 
> 성능 개선을 할 때는 반드시 <strong><u>수치를 측정하여 비교</u></strong>해야 한다&#46; 
> 
> <a id="1c3eda9b0fe181048d70e0e5abc4cf97"></a>
> 
> 실제로 얼마나 느린지, 개선한 뒤 얼마나 빨라졌는 지를  측정해야 한다&#46; 
> 
> <a id="1c3eda9b0fe181bfb7cceeeef040033e"></a>
> 
> 즉, <strong><u>정확한 데이터(수치)로 표현</u></strong>해야 한다&#46; 

<details>
<summary> Redis 적용 전</summary>

<a id="1c3eda9b0fe1816db337c570a2eafe8c"></a>

```java
@Service
public class BoardService {
  ...
  //  @Cacheable(cacheNames = "getBoards", key = "'boards:page:' + #page + ':size:' + #size", cacheManager = "boardCacheManager")
  public List<Board> getBoards(int page, int size) {
    Pageable pageable = PageRequest.of(page - 1, size);
    Page<Board> pageOfBoards = boardRepository.findAllByOrderByCreatedAtDesc(pageable);
    return pageOfBoards.getContent();
  }
}
```

<details>
<summary> Postman 측정&#58; <code>평균 413ms</code></summary>

![](46d1f566d08caf64.webp)

![](b18d74879e354103.webp)

![](c07842c8f527043f.webp)

</details>

</details>

<details>
<summary>Redis 적용 후 &#45; 처리속도 <code>약 40배</code> 개선</summary>

<a id="1c3eda9b0fe18138b6b1d4da34e76b6a"></a>

```java
@Service
public class BoardService {
  ...
  
  @Cacheable(cacheNames = "getBoards", key = "'boards:page:' + #page + ':size:' + #size", cacheManager = "boardCacheManager")
  public List<Board> getBoards(int page, int size) {
    Pageable pageable = PageRequest.of(page - 1, size);
    Page<Board> pageOfBoards = boardRepository.findAllByOrderByCreatedAtDesc(pageable);
    return pageOfBoards.getContent();
  }
}
```

<details>
<summary>처음 캐시에 데이터 등록&#58; <code>893ms</code></summary>

![](1c0f067c4c7a522b.webp)

- 처음 API를 호출하여 캐싱 처리 시, 기존 API 응답 속도보다 더 느리다&#46; 

</details>

<details>
<summary>캐싱 데이터 응답&#58; <code>평균 10ms 이내</code>  ⇒ <u>응답 처리 속도</u>가 <strong>약 40배 정도 개선</strong></summary>

![](66bc6834bd8095a3.webp)

![](17b5ea33a66e670e.webp)

![](ee3728bc57a12aea.webp)

<a id="1c3eda9b0fe18145907ac454aa3504e6"></a>

대부분의 응답이 10ms 이내에 처리되는 것을 확인할 수 있다&#46; 

<a id="1c3eda9b0fe1816dba02dd44e2760c65"></a>

캐싱 이후, <u>응답 처리 속도</u>가 <strong>약 40배 정도 개선</strong>되는 것을 확인할 수 있다&#46; 

</details>

</details>
