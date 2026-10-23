---
order: 22
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-819f-9cb3-ee371e8823ac
title: 게시글 CRUD API 테스트
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
    title: 대규모 시스템 설계
  - id: 1c3eda9b-0fe1-8151-a9bf-f4bde443f283
    title: 대규모 시스템 설계 - 게시판
  - id: 1c3eda9b-0fe1-819f-9cb3-ee371e8823ac
    title: 게시글 CRUD API 테스트
excerpt: 게시글 CRUD API 테스트 --- [[ Test ] 게시글 CRUD API](https://github.com/gyungsubLee/large-board/issues/10) [ 코드 ] ArticleApiTest java package sub.board.article.api; import lombok.AllArgsCo
cover: null
icon: null
notionProperties:
  소분류: 테스트코드
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8151-a9bf-f4bde443f283
created: 2025-03-27T07:52:18.661Z
updated: 2025-03-27T07:52:18.661Z
legacy_path: Main/대규모 시스템 설계-d6a1706fbaf8/대규모 시스템 설계 - 게시판-f4bde443f283/게시글 CRUD API 테스트-ee371e8823ac/index.md
legacy_category: 대규모 시스템 설계
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1819f9cb3ee371e8823ac
---
<a id="1c3eda9b0fe1810e8396e506f280a207"></a>

## 게시글 CRUD API 테스트

---

[[ Test ] 게시글 CRUD API](https://github.com/gyungsubLee/large-board/issues/10)

<details>
<summary>&#91; 코드 &#93; ArticleApiTest</summary>

<a id="1c3eda9b0fe181d6aad5c1c91f437168"></a>

```java
package sub.board.article.api;


import lombok.AllArgsConstructor;
import lombok.Getter;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.annotation.Rollback;
import org.springframework.web.client.RestClient;
import sub.board.article.service.response.ArticleResponse;

import static org.assertj.core.api.Assertions.assertThat;
import static org.junit.jupiter.api.Assertions.assertNotNull;
import static org.junit.jupiter.api.Assertions.assertThrows;

public class ArticleApiTest {
    RestClient restClient = RestClient.create("http://localhost:9000");

    // 생성 test 에서 출력된 id 값 사용
    Long articleId;

    // Article id 동적 생성
    @DisplayName("Article 생성")
    @BeforeEach
    void setUp() {
        //
        ArticleCreateRequest request = new ArticleCreateRequest("hi", "Ctest", 1L, 1L);

        // 테스트용 게시글을 먼저 생성하고 ID를 저장
        ArticleResponse response = create(request);
        assertNotNull(response, "생성된 게시글이 null이면 안 됩니다.");

        this.articleId = response.getArticleId();  // 동적으로 생성된 ID 저장
        System.out.println("생성된 articleId = " + this.articleId);
    }

    ArticleResponse create(ArticleCreateRequest request) {
        return restClient.post()
                .uri("/api/v1/articles")
                .body(request)
                .retrieve()
                .body(ArticleResponse.class);
    }

    @DisplayName("Article 조회")
    @Test
    void readTest() {
        // When
        ArticleResponse response = read(articleId);

        // Then
        assertNotNull(response, "response 객체가 null 이면 안됩니다.");
        assertThat(response.getArticleId()).isEqualTo(articleId);

        System.out.println("read = " + response);
    }

    ArticleResponse read(Long articleId) {
        return restClient.get()
                .uri("/api/v1/articles/{articleId}", articleId)
                .retrieve()
                .body(ArticleResponse.class);
    }

    @DisplayName("Article 수정")
    @Test
    void updateTest() {
        // Given
        ArticleUpdateRequest request = new ArticleUpdateRequest("h12", "Ctest2");

        // When
        ArticleResponse response = update(articleId, request);

        // Then
        assertNotNull(response, "response 객체는 null 이면 안됩니다.");
        assertThat(response.getTitle()).isEqualTo(request.getTitle());
        assertThat(response.getContent()).isEqualTo(request.getContent());

        System.out.println("response = " + response);
    }

    ArticleResponse update(Long articleId, ArticleUpdateRequest requset) {
        return restClient.patch()
                .uri("/api/v1/articles/{articleId}", articleId)
                .body(requset)
                .retrieve()
                .body(ArticleResponse.class);
    }

    @DisplayName("Article 삭제")
    @Test
    void deleteTest() {
        // When
        restClient.delete()
                .uri("/api/v1/articles/{articleId}", articleId)
                .retrieve();

        // Then
        Exception exception = assertThrows(Exception.class, () -> read(articleId));
        System.out.println("삭제 후 조회 시도 예외: " + exception.getMessage());
    }


    @Getter
    @AllArgsConstructor
    static class ArticleCreateRequest {
        private String title;
        private String content;
        private Long boardId;
        private Long writerId;
    }

    @Getter
    @AllArgsConstructor
    static class ArticleUpdateRequest {
        private String title;
        private String content;
    }
}
```

</details>

---

<details>
<summary>0&#46; 요청, 응답 DTO 정의</summary>

<a id="1c3eda9b0fe1812897b5e2a020df32ae"></a>

```java
@Getter
@AllArgsConstructor
static class ArticleCreateRequest {
    private String title;
    private String content;
    private Long boardId;
    private Long writerId;
}

@Getter
@AllArgsConstructor
static class ArticleUpdateRequest {
    private String title;
    private String content;
}
```

</details>

<details>
<summary>1&#46; <code>&#64;BeforeEach</code>를 통해 각 테스트 메서드 실행 전, Article 객체 생성</summary>

> 해당 로직, Article 생성 테스트 와 동일함

<a id="1c3eda9b0fe181f8ac88f546c0a0b60d"></a>

```java
@DisplayName("Article 생성")
@BeforeEach
void setUp() {
    //
    ArticleCreateRequest request = new ArticleCreateRequest("hi", "Ctest", 1L, 1L);

    // 테스트용 게시글을 먼저 생성하고 ID를 저장
    ArticleResponse response = create(request);
    assertNotNull(response, "생성된 게시글이 null이면 안 됩니다.");

    this.articleId = response.getArticleId();  // 동적으로 생성된 ID 저장
    System.out.println("생성된 articleId = " + this.articleId);
}

ArticleResponse create(ArticleCreateRequest request) {
    return restClient.post()
            .uri("/api/v1/articles")
            .body(request)
            .retrieve()
            .body(ArticleResponse.class);
}
```

</details>

<details>
<summary>2&#46; 조회 API 테스트 </summary>

<a id="1c3eda9b0fe181e6b242d179090378bb"></a>

```java
@DisplayName("Article 조회")
@Test
void readTest() {
    // When
    ArticleResponse response = read(articleId);

    // Then
    assertNotNull(response, "response 객체가 null 이면 안됩니다.");
    assertThat(response.getArticleId()).isEqualTo(articleId);

    System.out.println("read = " + response);
}

ArticleResponse read(Long articleId) {
    return restClient.get()
            .uri("/api/v1/articles/{articleId}", articleId)
            .retrieve()
            .body(ArticleResponse.class);
}
```

</details>

<details>
<summary>3&#46; 조회 API 테스트 </summary>

<a id="1c3eda9b0fe1814392f4e001f5966ae6"></a>

```java
@DisplayName("Article 수정")
@Test
void updateTest() {
    // Given
    ArticleUpdateRequest request = new ArticleUpdateRequest("h12", "Ctest2");

    // When
    ArticleResponse response = update(articleId, request);

    // Then
    assertNotNull(response, "response 객체는 null 이면 안됩니다.");
    assertThat(response.getTitle()).isEqualTo(request.getTitle());
    assertThat(response.getContent()).isEqualTo(request.getContent());

    System.out.println("response = " + response);
}

ArticleResponse update(Long articleId, ArticleUpdateRequest requset) {
    return restClient.patch()
            .uri("/api/v1/articles/{articleId}", articleId)
            .body(requset)
            .retrieve()
            .body(ArticleResponse.class);
}
```

</details>

<details>
<summary>4&#46; 삭제 API 테스트 </summary>

<a id="1c3eda9b0fe1817cbb46ed88e9a1ca74"></a>

```java
@DisplayName("Article 삭제")
@Test
void deleteTest() {
    // When
    restClient.delete()
            .uri("/api/v1/articles/{articleId}", articleId)
            .retrieve();

    // Then
    Exception exception = assertThrows(Exception.class, () -> read(articleId));
    System.out.println("삭제 후 조회 시도 예외: " + exception.getMessage());
}
```

</details>

> ☝🏻 
> 
> <a id="1c3eda9b0fe181499126fd0190eb54fc"></a>
> 
> 위 로직의 경우 단순 CRUD API를 호출하는 <code>end&#45;to&#45;end </code>테스트이다&#46; 
> 
> <a id="1c3eda9b0fe181edb3f2c1940a275b9c"></a>
> 
> 그러나 단순  CRUD의 경우, 테스트할 가치가 낮고, end &#45; to &#45; end 또한 비용만 높은 테스트 가치가 낮은 방법이다&#46; 
> 
> - 통합 테스트인 경우는 필요함
> 
> <a id="1c3eda9b0fe1816e93f1ee5651275fbf"></a>
> 
> <br>따라서 위 테스트 코드는 작성 가치가 낮은 코드이다&#46; 
> 
> <a id="1c3eda9b0fe181c2bc3df459626a4546"></a>
> 
> 그러나 연습을 위한 코드 작성이기 때문에, 작성 및 정리를 한다&#46;
