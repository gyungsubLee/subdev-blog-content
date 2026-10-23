---
order: 10
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-813f-842e-d3c86d43d555
title: RedisTemplate, Jedis, Lettuce 비교
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81b8-a968-f6b1b2a79b94
    title: Redis
  - id: 1c3eda9b-0fe1-81c7-ae23-cfbc9fd6e83a
    title: 비전공자도 이해할 수 있는 Redis - 캐싱 [ 리펙토링 필요 ]
  - id: 1c3eda9b-0fe1-813f-842e-d3c86d43d555
    title: RedisTemplate, Jedis, Lettuce 비교
excerpt: Redis Docs 를 보던 중, 이전 Redis 사용 시, Redis Template을 사용 했는데, Docs에 Jedis, Lettuce가 나와 있어 해당 내용을 비교하여 정리 진행한다. - ‣ - ‣ - ‣ - 학습 시, Spring Boot 3.4.3을 사용 비교 | 비교 항목 | RedisTemplate (Spr
cover: null
icon: null
notionProperties:
  Tags: 추가
  Point: Redisson, 사용 예시 - 추가 정리 필요
  상태: 진행 중
schema_version: 1
parent_id: 1c3eda9b-0fe1-81c7-ae23-cfbc9fd6e83a
created: 2025-03-27T07:47:52.770Z
updated: 2025-03-27T07:47:52.770Z
legacy_path: Main/Redis-f6b1b2a79b94/비전공자도 이해할 수 있는 Redis - 캐싱 [ 리펙토링 필요 ]-cfbc9fd6e83a/RedisTemplate, Jedis, Lettuce 비교-d3c86d43d555/index.md
legacy_category: Redis
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1813f842ed3c86d43d555
---
<a id="1c3eda9b0fe181a8b810fdc282c8dcef"></a>

Redis Docs 를 보던 중, 이전 Redis 사용 시, Redis Template을 사용 했는데, 

<a id="1c3eda9b0fe181fd9b53dc3f7777ed71"></a>

Docs에 Jedis, Lettuce가 나와 있어 해당 내용을 비교하여 정리 진행한다&#46; 

- ‣

- ‣

- ‣
    - 학습 시, Spring Boot 3&#46;4&#46;3을 사용

<a id="1c3eda9b0fe181559fc4e0022029e22e"></a>

### 비교 

| <strong>비교 항목</strong> | <strong>RedisTemplate</strong> (Spring 제공) | <strong>Lettuce</strong> (비동기) | <strong>Jedis</strong> (싱글스레드) |
| --- | --- | --- | --- |
| <strong>기본 제공 여부</strong> | ✅ Spring Boot에서 기본 제공 | ✅ Spring Boot 2&#46;x 이상 기본 | ❌ 별도 설정 필요 |
| <strong>스레드 안전성</strong> | ✅ (클라이언트에 따라 다름) | ✅ 멀티스레드 (Thread&#45;safe) | ❌ 싱글스레드 (Thread&#45;safe 아님) |
| <strong>비동기 지원</strong> | ❌ 불가능 | ✅ 가능 (Reactive 지원) | ❌ 불가능 |
| <strong>성능 (멀티스레드 환경)</strong> | ⭕ 보통 | ✅ 높음 (커넥션 풀 지원) | ❌ 낮음 |
| <strong>설정 난이도</strong> | ⭕ 보통 (직렬화 설정 필요) | ⭕ 보통 (비동기 처리 주의) | ✅ 쉬움 |
| <strong>트랜잭션 지원</strong> | ✅ 지원 | ✅ 지원 | ✅ 지원 |
| <strong>추천 사용 사례</strong> | 일반적인 Spring Boot 환경 | 대규모 트래픽, WebFlux 사용 | 간단한 싱글스레드 Redis 사용 |

<a id="1c3eda9b0fe181738a57f864b6061c4e"></a>

### <strong>RedisTemplate (Spring 제공)</strong>

> ✏️ 
> 
> - Spring에서 제공하는 <strong>고수준 API</strong>
> 
> - Redis의 다양한 데이터 타입 (String, List, Set, Hash, ZSet 등) 지원
> 
> - 내부적으로 Lettuce 또는 Jedis를 사용할 수 있음
> 
> - <strong>직접 Redis 클라이언트를 선택하지 않아도 됨</strong>

<details>
<summary><strong>✅ 장점</strong></summary>

- ✔ Spring Boot에 최적화된 방식

- ✔ 여러 데이터 타입을 쉽게 다룰 수 있음 (opsForValue(), opsForList(), opsForSet() 등)

- ✔ 트랜잭션 및 파이프라이닝 지원


</details>

<details>
<summary><strong>✅ 단점</strong></summary>

- ❌ 기본적인 직렬화 방식 (JdkSerializationRedisSerializer)이 비효율적이므로, <strong>직렬화 방식을 변경해야 함</strong> (StringRedisSerializer 추천)

- ❌ 저수준 설정이 어려울 수 있음 (클라이언트를 직접 관리하지 않음)

<a id="1c3eda9b0fe18183b8a9d90ca0db70e8"></a>

 

</details>

<details>
<summary><strong>✅ 사용 예시</strong></summary>

<a id="1c3eda9b0fe181f29e5bd39581314781"></a>

```java
@Configuration
public class RedisConfig {
    @Bean
    public RedisTemplate<String, Object> redisTemplate(RedisConnectionFactory connectionFactory) {
        RedisTemplate<String, Object> template = new RedisTemplate<>();
        template.setConnectionFactory(connectionFactory);
        
        // 직렬화 설정
        template.setKeySerializer(new StringRedisSerializer());
        template.setValueSerializer(new Jackson2JsonRedisSerializer<>(Object.class));
        return template;
    }
}

@Service
public class RedisService {
    private final RedisTemplate<String, Object> redisTemplate;

    public RedisService(RedisTemplate<String, Object> redisTemplate) {
        this.redisTemplate = redisTemplate;
    }

    public void saveValue(String key, String value) {
        redisTemplate.opsForValue().set(key, value);
    }

    public String getValue(String key) {
        return (String) redisTemplate.opsForValue().get(key);
    }
}
```

</details>

<a id="1c3eda9b0fe181319f08d03af380d185"></a>

### <strong>Lettuce (Spring Boot 기본 클라이언트, 비동기 지원)</strong>

<details>
<summary><strong>✅ 개요</strong></summary>

- Spring Boot 2&#46;x 이후 <strong>기본 Redis 클라이언트</strong>

- <strong>비동기 및 넌블로킹</strong> 방식 지원

- 멀티스레드 환경에서 안전 (Thread&#45;safe)

</details>

<details>
<summary><strong>✅ 장점</strong></summary>

- ✔ <strong>멀티스레드 지원</strong> (Thread&#45;safe)

- ✔ <strong>비동기 지원</strong> (Async, Reactive) → WebFlux와 함께 사용 가능

- ✔ 커넥션 풀을 기본적으로 제공하여 성능이 뛰어남

</details>

<details>
<summary><strong>✅ 단점</strong></summary>

- ❌ Jedis보다 상대적으로 설정이 복잡할 수 있음

- ❌ 비동기 방식이므로, 동기식 코드에서는 조심해서 사용해야 함

</details>

<a id="1c3eda9b0fe181b483dafae49d967dc2"></a>

### Jedis ( 사용 ❌ )

> ✏️ 
> 
> <a id="1c3eda9b0fe1816fbfb4c50f1d63ffb4"></a>
> 
> Redis 공식 클라이언트 (redis&#46;clients&#46;jedis)
> 
> <a id="1c3eda9b0fe181c7abbaf4deac3cf0ff"></a>
> 
> <strong>싱글 스레드</strong> 기반이므로, 멀티스레드 환경에서 Thread&#45;safe 하지 않음
> 
> <a id="1c3eda9b0fe18122871cd9a599e47a92"></a>
> 
> Spring Boot 2&#46;x 이후부터는 기본 클라이언트에서 제외됨 (대신 Lettuce 사용)

<details>
<summary><strong>✅ 장점</strong></summary>

- ✔ 단순하고 빠름

- ✔ Redis의 기본 명령어를 쉽게 사용할 수 있음

- ✔ Spring을 사용하지 않는 경우, 직접 Jedis를 사용할 수 있음

</details>

<details>
<summary><strong>✅ 단점</strong></summary>

- ❌ 싱글 스레드 기반이라 <strong>멀티스레드 환경에서는 문제가 발생할 수 있음</strong>

- ❌ Spring Boot에서 공식적으로 <strong>기본 지원되지 않음</strong> (JedisConnectionFactory를 명시적으로 등록해야 함)

</details>

<details>
<summary><strong>✅ 사용 예시</strong></summary>

<a id="1c3eda9b0fe1817d8dafd1b13f162e9d"></a>

```java
@Configuration
public class RedisConfig {
    @Bean
    public JedisConnectionFactory jedisConnectionFactory() {
        return new JedisConnectionFactory();
    }

    @Bean
    public RedisTemplate<String, Object> redisTemplate(JedisConnectionFactory jedisConnectionFactory) {
        RedisTemplate<String, Object> template = new RedisTemplate<>();
        template.setConnectionFactory(jedisConnectionFactory);
        template.setKeySerializer(new StringRedisSerializer());
        return template;
    }
}
```

</details>

<a id="1c3eda9b0fe181cfade9ec4d07f3b3b1"></a>

### Reddison 추가 필요 

<a id="1c3eda9b0fe1814b92a7e4b7fe55a004"></a>

### 질문 정리 전

<a id="1c3eda9b0fe181c2828afc445863c438"></a>

기본 Redis 클라이언트

<a id="1c3eda9b0fe181529b2ec15732290297"></a>

여기서 클라이언트라는 단어는 백엔드&#46; 클라이언트를 가르키는 것이 아닌 것 같은데,

<a id="1c3eda9b0fe181d4875cd849d1a4eaa9"></a>

해당 라이브러이에서  지원되어 서버에서 사용하는 API 라고 이해를 하면되나?

<a id="1c3eda9b0fe1816d8674e0c57fc54e29"></a>

네, 맞습니다&#33; 여기서 &#42;&#42;“클라이언트”&#42;&#42;라는 단어는 <strong>백엔드 애플리케이션에서 Redis 서버와 상호작용을 하는 라이브러리</strong>를 의미합니다&#46; 즉, Redis 클라이언트는 Redis 서버에 명령을 보내고 응답을 받는 역할을 하는 <strong>서버에서 사용하는 API</strong>나 라이브러리를 가리킵니다&#46;

<a id="1c3eda9b0fe1812eb673fd55a17b2d01"></a>

따라서, <strong>클라이언트</strong>라는 용어는 <strong>Redis 서버와 연결하여 데이터를 처리하는 인터페이스</strong>를 뜻하며, 이를 통해 애플리케이션(백엔드)에서 Redis와 통신을 할 수 있게 됩니다&#46;

<a id="1c3eda9b0fe18153ad95fd25ccb77c9c"></a>

이와 같은 클라이언트 라이브러리들은 각기 다른 방식으로 Redis 서버와 연결하고 데이터를 읽고 쓰는 작업을 처리하게 됩니다&#46; RedisTemplate, Jedis, Lettuce와 같은 라이브러리는 모두 <strong>백엔드에서 Redis 서버와의 상호작용을 처리하는 클라이언트 라이브러리</strong>입니다&#46;
