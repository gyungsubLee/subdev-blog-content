---
order: 23
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8121-87bb-e4ab36949003
title: 스레드풀 (Executors.newFixedThreadPool()) vs IntStream.parallel()
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
    title: 대규모 시스템 설계
  - id: 1c3eda9b-0fe1-8151-a9bf-f4bde443f283
    title: 대규모 시스템 설계 - 게시판
  - id: 1c3eda9b-0fe1-8121-87bb-e4ab36949003
    title: 스레드풀 (Executors.newFixedThreadPool()) vs IntStream.parallel()
excerpt: 두 가지 병렬 처리 방식 비교 1. 스레드풀 (Executors.newFixedThreadPool())을 이용한 방식 2. IntStream.parallel()을 이용한 방식 🔹 1. Executors.newFixedThreadPool() 방식 java ExecutorService executorService = Exe
cover: null
icon: null
notionProperties:
  Tags: 🧐 질문
  상태: 진행 중
schema_version: 1
parent_id: 1c3eda9b-0fe1-8151-a9bf-f4bde443f283
created: 2025-03-27T07:52:18.660Z
updated: 2025-03-27T07:52:18.660Z
legacy_path: Main/대규모 시스템 설계-d6a1706fbaf8/대규모 시스템 설계 - 게시판-f4bde443f283/스레드풀 (Executors.newFixedThreadPool()) vs IntS-e4ab36949003/index.md
legacy_category: 대규모 시스템 설계
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1812187bbe4ab36949003
---
<a id="1c3eda9b0fe181499025e9f5efcab4af"></a>

<strong>두 가지 병렬 처리 방식 비교</strong>

<a id="1c3eda9b0fe18185b636cac23989c326"></a>

1&#46;	<strong>스레드풀 (Executors&#46;newFixedThreadPool())을 이용한 방식</strong>

<a id="1c3eda9b0fe1812fad70f8ec7fa6d846"></a>

2&#46;	<strong>IntStream&#46;parallel()을 이용한 방식</strong>

<a id="1c3eda9b0fe1814e8db3c32cdd693e87"></a>

### <strong>🔹 1&#46; Executors&#46;newFixedThreadPool() 방식</strong>

<a id="1c3eda9b0fe18149bcefec6c73a03922"></a>

```java
ExecutorService executorService = Executors.newFixedThreadPool(10);
for (int i = 0; i < EXCUTE_COUNT; i++) {
    executorService.submit(() -> {
        insert();
        latch.countDown();
    });
}
latch.await();
executorService.shutdown();
```

<a id="1c3eda9b0fe1816ea744f73ee3c08b75"></a>

<strong>특징</strong>

<a id="1c3eda9b0fe1810bab9bca15ed0298f7"></a>

•	Executors&#46;newFixedThreadPool(10)을 사용해 <strong>고정된 개수(10개)의 스레드</strong>를 생성

<a id="1c3eda9b0fe18110b559e858d41a435a"></a>

•	executorService&#46;submit()을 통해 작업을 스레드풀에 제출

<a id="1c3eda9b0fe18132b9ccf2521456a39b"></a>

•	latch&#46;await()를 사용해 모든 작업이 끝날 때까지 대기

<a id="1c3eda9b0fe181b1856ad8be540bd2db"></a>

•	<strong>명시적으로 스레드 개수를 지정</strong>할 수 있음

<a id="1c3eda9b0fe181d795fed7980bee7740"></a>

<strong>✔ 장점</strong>

<a id="1c3eda9b0fe18187995be35fecbe9342"></a>

✅ 스레드 개수를 조절 가능 → <strong>CPU 코어 수와 작업량에 맞게 최적화 가능</strong>

<a id="1c3eda9b0fe181c3af19c1024dbb2e66"></a>

✅ CountDownLatch를 이용해 동기화 및 종료 시점을 명확하게 관리 가능

<a id="1c3eda9b0fe18102b864d7fcb7897608"></a>

<strong>✔ 단점</strong>

<a id="1c3eda9b0fe1813d946dd012e1563de9"></a>

❌ <strong>스레드풀 관리 필요</strong> (명시적으로 shutdown() 해줘야 함)

<a id="1c3eda9b0fe18143beb2f09afe6a7392"></a>

❌ 스레드 개수가 고정되어 있어, 작업량이 많을 경우 <strong>일부 스레드는 대기 상태</strong>가 됨

<a id="1c3eda9b0fe18198ad6ee3207dbce778"></a>

### <strong>🔹 2&#46; IntStream&#46;parallel() 방식</strong>

<a id="1c3eda9b0fe181428cd8f4f61437a0b2"></a>

```java
IntStream.range(0, EXCUTE_COUNT)
        .parallel()
        .forEach(i -> insert());
```

<a id="1c3eda9b0fe1817d9f3acb641796a65f"></a>

<strong>✔ 특징</strong>

<a id="1c3eda9b0fe1816a9c1fc1f0840040c3"></a>

•	&#46;parallel()을 호출하면 <strong>ForkJoinPool&#46;commonPool</strong>을 사용하여 자동으로 병렬 처리

<a id="1c3eda9b0fe181b2b8a5d82ffd3d569c"></a>

•	개발자가 <strong>직접 스레드 개수를 조정할 필요 없음</strong> (자동으로 처리)

<a id="1c3eda9b0fe181ec9d21f42fe1d2727e"></a>

<strong>✔ 장점</strong>

<a id="1c3eda9b0fe18170aa10e196e88e0976"></a>

✅ 코드가 간결하고 <strong>스레드풀을 직접 관리할 필요 없음</strong>

<a id="1c3eda9b0fe18196887ac2521b8566d1"></a>

✅ CPU 코어 수에 맞춰 자동으로 병렬 처리 최적화

<a id="1c3eda9b0fe181349be8e6c0d197e2f5"></a>

<strong>✔ 단점</strong>

<a id="1c3eda9b0fe18127b058e799f807d9a6"></a>

❌ <strong>스레드 개수 조절이 어려움</strong> (기본적으로 ForkJoinPool&#46;commonPool 사용)

<a id="1c3eda9b0fe1815fb6c7e76a260f39fc"></a>

❌ <strong>비싼 리소스를 다루는 경우 비효율적</strong> (트랜잭션, DB 연산 등)

<a id="1c3eda9b0fe1817cbafbed85f0d0366f"></a>

❌ 스레드 동기화 제어가 어려움 (CountDownLatch 같은 수동 제어 불가능)

<a id="1c3eda9b0fe181698926f932a700206f"></a>

### <strong>실무에서는 어떤 방식을 써야 할까?</strong>

|  |  |  |
| --- | --- | --- |
| <strong>기준</strong> | Executors&#46;newFixedThreadPool() | IntStream&#46;parallel() |
| <strong>제어 가능성</strong> | ✅ 직접 스레드 개수 조절 가능 | ❌ 자동 최적화 (수동 조절 어려움) |
| <strong>코드 간결성</strong> | ❌ 상대적으로 복잡 | ✅ 매우 간결 |
| <strong>DB 트랜잭션 처리</strong> | ✅ 명확한 제어 가능 | ❌ 트랜잭션 관리 어려움 |
| <strong>CPU 연산 (예&#58; 숫자 계산)</strong> | ❌ 오버헤드 발생 가능 | ✅ 적합 |
| <strong>비동기 작업 (예&#58; 네트워크, 파일 IO)</strong> | ✅ 적합 | ❌ 적합하지 않음 |

<a id="1c3eda9b0fe181c5800ed69b429911fe"></a>

<strong>🚀 결론</strong>

<a id="1c3eda9b0fe1815597c1c98b0cd638ea"></a>

•	<strong>DB 트랜잭션을 사용하는 경우 → Executors&#46;newFixedThreadPool()이 더 적합</strong>

<a id="1c3eda9b0fe18168ade2f0bc29ad186c"></a>

•	<strong>CPU 연산 중심의 병렬 처리 → IntStream&#46;parallel()이 더 적합</strong>

<a id="1c3eda9b0fe18166bd76f101906599bd"></a>

•	<strong>단순한 데이터 처리</strong>는 parallelStream()이 간편하지만, <strong>복잡한 동기화가 필요한 경우</strong> 직접 스레드를 관리하는 방식이 필요

> ☝🏻 
> 
> <a id="1c3eda9b0fe18137b109ed832cb1e82d"></a>
> 
> <strong>DB에 대량 데이터를 삽입하는 현재 코드에서는 Executors&#46;newFixedThreadPool() 방식이 더 적합&#33;</strong>
