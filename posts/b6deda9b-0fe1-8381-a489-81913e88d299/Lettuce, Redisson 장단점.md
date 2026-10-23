---
order: 3
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: b6deda9b-0fe1-8381-a489-81913e88d299
title: Lettuce, Redisson 장단점
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 165eda9b-0fe1-8072-b168-fab7f9ef1bfa
    title: "[ Inflearn ] 동시성 제어"
  - id: b6deda9b-0fe1-8381-a489-81913e88d299
    title: Lettuce, Redisson 장단점
excerpt: Lettuce - 장점 - 구현 간단 - Spring Data Redis 사용 시, lettuce가 기본 라이브러리이다. 따라서 별도의 라이브러리를 사용하지 않아도 됨 - 단점 - spin lock 방식이기 때문에, 동시에 많은 스레드가 lock 획득 대기 상태라면 redis에 부하가 갈 수 있다. Redisson - 장
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 165eda9b-0fe1-8072-b168-fab7f9ef1bfa
created: 2026-04-10T05:12:37.849Z
updated: 2026-04-10T05:12:37.849Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/[ Inflearn ] 동시성 제어-fab7f9ef1bfa/Lettuce, Redisson 장단점-81913e88d299/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/b6deda9b0fe18381a48981913e88d299
---
<a id="7ebeda9b0fe1823f9e7781bc846897d2"></a>

### Lettuce 

- 장점
    - 구현 간단

    - Spring Data Redis 사용 시, lettuce가 기본 라이브러리이다&#46;<br>따라서 별도의 라이브러리를 사용하지 않아도 됨

- 단점
    - spin lock 방식이기 때문에, 동시에 많은 스레드가 lock 획득 대기 상태라면 redis에 부하가 갈 수 있다&#46;

<a id="da7eda9b0fe1824e8d560105983eb121"></a>

### Redisson 

- 장점
    - <u>락 획득 재시도</u>를 <strong><u>기본</u></strong>으로 제공한다&#46;

    - pub&#45;sub 방식으로 구현 되어있기 때문에, lettuce 와 비교했을 때 redis에 부하가 덜 간다&#46;

- 단점
    - 별도의 redisson 라이브러리 설치 필요

    - lock을 라이브러리 차원에서 제공해주기 때문에 사용법을 공부 해야한다&#46;

<a id="cddeda9b0fe18281a63901c3821905fb"></a>

### 실무

- 재시도가 필요하지 않는 lock = lettuce

- 재시도가 필요한 lock = redisson
