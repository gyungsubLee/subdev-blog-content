---
order: 20
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-818a-b55d-efa1defa142b
title: "PK 수동 생성: snowflake 알고리즘"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
    title: 대규모 시스템 설계
  - id: 1c3eda9b-0fe1-8151-a9bf-f4bde443f283
    title: 대규모 시스템 설계 - 게시판
  - id: 1c3eda9b-0fe1-818a-b55d-efa1defa142b
    title: "PK 수동 생성: snowflake 알고리즘"
excerpt: "Primary Key 수동 생성 - Snowflake 알고리즘 --- ✏️ 오름차순 유니크 숫자를 생성하기 위한 알고리즘은 이미 많이 공개되어 있다. - Snowflake, TSID 등 해당 자료에서는 Snowflake를 사용하여 실습을 진행한다. --- - [ ] ‘🧐 왜 오름차순 유니크 숫자로 pk를 설정하는가’에 "
cover: null
icon: null
notionProperties:
  소분류: 알고리즘
  중요도: No
  상태: 의문점 정리 필요
schema_version: 1
parent_id: 1c3eda9b-0fe1-8151-a9bf-f4bde443f283
created: 2025-03-27T07:52:18.661Z
updated: 2025-03-27T07:52:18.661Z
legacy_path: Main/대규모 시스템 설계-d6a1706fbaf8/대규모 시스템 설계 - 게시판-f4bde443f283/PK 수동 생성- snowflake 알고리즘-efa1defa142b/index.md
legacy_category: 대규모 시스템 설계
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1818ab55defa1defa142b
---
<a id="1c3eda9b0fe18162a055fe9d9065e230"></a>

### Primary Key 수동 생성 &#45; <strong><code>Snowflake</code></strong><strong> 알고리즘 </strong>

---

> ✏️ 
> 
> <a id="1c3eda9b0fe181bcbe4ec3d992682682"></a>
> 
> <code>오름차순 유니크 숫자</code>를 생성하기 위한 알고리즘은 이미 많이 공개되어 있다&#46; 
> 
> - Snowflake, TSID 등
> 
> <a id="1c3eda9b0fe1814ebf42fd9123e333a8"></a>
> 
> 해당 자료에서는 <strong><u>Snowflake를 사용</u></strong>하여 실습을 진행한다&#46; 
> 
> ---
> 
> - [ ] ‘🧐 왜 <code>오름차순 유니크 숫자</code>로 pk를 설정하는가’에 대한 내용은 이후 챕터에서 다룬다고 하니, 해당 내용 학습 후 정리 진행
>     - <strong><u>분산 시스템</u></strong>과 <strong><u>인덱스 구조</u></strong>에 대한 이해가 필요
> 
> - [ ] <code>오름차순 유니크 숫자</code> 에 대한 다른 알고리즘도 비교하여 정리 진행

<a id="1c3eda9b0fe18118b621f10f294019f0"></a>

오름차순 유니크 숫자를 앱에서 직접 생성

- <code>AUTO&#95;INCREMENT</code> or <code>UUID</code> 사용 ❌ 

<details>
<summary><strong><code>Snowflake</code></strong> 채택</summary>

> 분산 시스템에서 <strong><u>고유한 64비트 ID를 생성</u></strong>하는 알고리즘

<a id="1c3eda9b0fe18144a2baecc6bcfd72c1"></a>

```sql
# 구조: 총 64 비트
[1비트] [41비트: 타임스탬프][10비트: 노드][12비트: 시퀀스 번호]
```

- X (전 Twitter)에서 개발

- 분산 환경에서도 중복 없이 순차적 ID 생성하기 위한 규칙
    - 타임스탬프 &#58; 순차성

    -  노드ID &#43; 시퀀스 번호 &#58; 고유성

- 유니크, 시간 기반 순차성  →  분산 환경에서의 높은 성능

</details>

<a id="1c3eda9b0fe18195981dc4ae9dd0137f"></a>

### <strong>코드</strong>

> ✏️ 
> 
> <a id="1c3eda9b0fe181fab2b2eda2bd0596ca"></a>
> 
> common 모듈 내부에 snowflake 로직을 추가하고, <code>settings&#46;gradle</code>에  추가된 내용을 등록한다&#46; 

[Feat: snowflake 알고리즘 및 모듈 설정 추가](https://github.com/gyungsubLee/large-board/commit/fde937883ce2824f84ffd4b4f1473683f67be44b)

<details>
<summary>&#91; 코드 &#93; Snowflake</summary>

<a id="1c3eda9b0fe181399664e3db0bb5c374"></a>

```java
package kuke.board.common.snowflake;
 
 import java.util.random.RandomGenerator;
 
 public class Snowflake {
 	private static final int UNUSED_BITS = 1;
 	private static final int EPOCH_BITS = 41;
 	private static final int NODE_ID_BITS = 10;
 	private static final int SEQUENCE_BITS = 12;
 
 	private static final long maxNodeId = (1L << NODE_ID_BITS) - 1;
 	private static final long maxSequence = (1L << SEQUENCE_BITS) - 1;
 
 	private final long nodeId = RandomGenerator.getDefault().nextLong(maxNodeId + 1);
 	// UTC = 2024-01-01T00:00:00Z
 	private final long startTimeMillis = 1704067200000L;
 
 	private long lastTimeMillis = startTimeMillis;
 	private long sequence = 0L;
 
 	public synchronized long nextId() {
 		long currentTimeMillis = System.currentTimeMillis();
 
 		if (currentTimeMillis < lastTimeMillis) {
 			throw new IllegalStateException("Invalid Time");
 		}
 
 		if (currentTimeMillis == lastTimeMillis) {
 			sequence = (sequence + 1) & maxSequence;
 			if (sequence == 0) {
 				currentTimeMillis = waitNextMillis(currentTimeMillis);
 			}
 		} else {
 			sequence = 0;
 		}
 
 		lastTimeMillis = currentTimeMillis;
 
 		return ((currentTimeMillis - startTimeMillis) << (NODE_ID_BITS + SEQUENCE_BITS))
 			| (nodeId << SEQUENCE_BITS)
 			| sequence;
 	}
 
 	private long waitNextMillis(long currentTimestamp) {
 		while (currentTimestamp <= lastTimeMillis) {
 			currentTimestamp = System.currentTimeMillis();
 		}
 		return currentTimestamp;
 	}
 }
```

</details>

<details>
<summary>&#91; 코드 &#93; SnowflakeTest</summary>

<a id="1c3eda9b0fe181d3bddede2ca25d231d"></a>

```java
package kuke.board.common.snowflake;
 
 import static org.assertj.core.api.Assertions.*;
 
 import java.util.ArrayList;
 import java.util.List;
 import java.util.concurrent.CountDownLatch;
 import java.util.concurrent.ExecutionException;
 import java.util.concurrent.ExecutorService;
 import java.util.concurrent.Executors;
 import java.util.concurrent.Future;
 
 import org.junit.jupiter.api.Test;
 
 class SnowflakeTest {
 	Snowflake snowflake = new Snowflake();
 
 	@Test
 	void nextIdTest() throws ExecutionException, InterruptedException {
 		// given
 		ExecutorService executorService = Executors.newFixedThreadPool(10);
 		List<Future<List<Long>>> futures = new ArrayList<>();
 		int repeatCount = 1000;
 		int idCount = 1000;
 
 		// when
 		for (int i = 0; i < repeatCount; i++) {
 			futures.add(executorService.submit(() -> generateIdList(snowflake, idCount)));
 		}
 
 		// then
 		List<Long> result = new ArrayList<>();
 		for (Future<List<Long>> future : futures) {
 			List<Long> idList = future.get();
 			for (int i = 1; i < idList.size(); i++) {
 				assertThat(idList.get(i)).isGreaterThan(idList.get(i - 1));
 			}
 			result.addAll(idList);
 		}
 		assertThat(result.stream().distinct().count()).isEqualTo(repeatCount * idCount);
 
 		executorService.shutdown();
 	}
 
 	List<Long> generateIdList(Snowflake snowflake, int count) {
 		List<Long> idList = new ArrayList<>();
 		while (count-- > 0) {
 			idList.add(snowflake.nextId());
 		}
 		return idList;
 	}
 
 	@Test
 	void nextIdPerformanceTest() throws InterruptedException {
 		// given
 		ExecutorService executorService = Executors.newFixedThreadPool(10);
 		int repeatCount = 1000;
 		int idCount = 1000;
 		CountDownLatch latch = new CountDownLatch(repeatCount);
 
 		// when
 		long start = System.nanoTime();
 		for (int i = 0; i < repeatCount; i++) {
 			executorService.submit(() -> {
 				generateIdList(snowflake, idCount);
 				latch.countDown();
 			});
 		}
 
 		latch.await();
 
 		long end = System.nanoTime();
 		System.out.println("times = %s ms".formatted((end - start) / 1_000_000));
 
 		executorService.shutdown();
 	}
 }
```

</details>

<details>
<summary>모듈 설정 추가&#58; <strong><code>‎settings&#46;gradle</code></strong></summary>

<a id="1c3eda9b0fe181bd960bc4f078aa6647"></a>

```groovy
rootProject.name = 'large-board'
 
include 'common'
include 'common:snowflake'
include 'service'
include 'service:article'
```

</details>
