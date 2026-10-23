---
order: 13
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-810b-9448-dd6448d4de7c
title: 게시글 CRUD API
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
    title: 대규모 시스템 설계
  - id: 1c3eda9b-0fe1-8151-a9bf-f4bde443f283
    title: 대규모 시스템 설계 - 게시판
  - id: 1c3eda9b-0fe1-810b-9448-dd6448d4de7c
    title: 게시글 CRUD API
excerpt: "게시글 CRUD API --- 코드 Feat: article CRUD API [ 코드 ] ArticleController java package sub.board.article.controller; import lombok.RequiredArgsConstructor; import org.springframework.web"
cover: null
icon: null
notionProperties:
  소분류: CRUD
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8151-a9bf-f4bde443f283
created: 2025-03-27T07:52:18.662Z
updated: 2025-03-27T07:52:18.662Z
legacy_path: Main/대규모 시스템 설계-d6a1706fbaf8/대규모 시스템 설계 - 게시판-f4bde443f283/게시글 CRUD API-dd6448d4de7c/index.md
legacy_category: 대규모 시스템 설계
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1810b9448dd6448d4de7c
---
<a id="1c3eda9b0fe1814ebbbfc1c8939f890d"></a>

## 게시글 CRUD API 

---

<a id="1c3eda9b0fe1813588b1c0493d56a37f"></a>

### 코드

[Feat: article CRUD API](https://github.com/gyungsubLee/large-board/pull/11/commits/d92a8e1498821f6e18b392133fadc50e5f9f3f1f)

<details>
<summary>&#91; 코드 &#93; ArticleController</summary>

<a id="1c3eda9b0fe1813dbea3d24e7f14d308"></a>

```java
package sub.board.article.controller;

import lombok.RequiredArgsConstructor;
import org.springframework.web.bind.annotation.*;
import sub.board.article.service.ArticleService;
import sub.board.article.service.request.ArticleCreateRequest;
import sub.board.article.service.request.ArticleUpdateRequest;
import sub.board.article.service.response.ArticleResponse;

@RestController
@RequiredArgsConstructor
@RequestMapping("/api/v1/articles")
public class ArticleController {
    private final ArticleService articleService;

    @PostMapping
    public ArticleResponse create(@RequestBody ArticleCreateRequest request) {
        return articleService.create(request);
    }

    @GetMapping("/{articleId}")
    public ArticleResponse read(@PathVariable Long articleId) {
        return articleService.read(articleId);
    }

    @PatchMapping("/{articleId}")
    public ArticleResponse update(@PathVariable Long articleId, @RequestBody ArticleUpdateRequest request) {
        return articleService.update(articleId, request);
    }

    @DeleteMapping("/{articleId}")
    public void delete(@PathVariable Long articleId) {
        articleService.delete(articleId);
    }
}
```

</details>

<details>
<summary>&#91; 코드 &#93; ArticleService</summary>

<a id="1c3eda9b0fe181fd877edb2d4b072db8"></a>

```java
package sub.board.article.service;

import lombok.RequiredArgsConstructor;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;
import sub.board.article.entity.Article;
import sub.board.article.repository.ArticleRepository;
import sub.board.article.service.request.ArticleCreateRequest;
import sub.board.article.service.request.ArticleUpdateRequest;
import sub.board.article.service.response.ArticleResponse;
import sub.board.common.snowflake.Snowflake;

@Service
@RequiredArgsConstructor
public class ArticleService {
    private final Snowflake snowflake = new Snowflake();
    private final ArticleRepository articleRepository;

    @Transactional
    public ArticleResponse create(ArticleCreateRequest request) {
        Article buildArticle = Article.builder()
                .articleId(snowflake.nextId())
                .title(request.getTitle())
                .content(request.getContent())
                .boardId(request.getBoardId())
                .writerId(request.getWriterId())
                .build();

        Article article = articleRepository.save(buildArticle);

        return ArticleResponse.from(article);
    }

    @Transactional
    public ArticleResponse update(Long articleId, ArticleUpdateRequest request) {
        Article findArticle = articleRepository.findByIdOrElseThrow(articleId);
        findArticle.update(request.getTitle(), request.getContent());
        return ArticleResponse.from(findArticle);
    }

    @Transactional(readOnly = true)
    public ArticleResponse read(Long articleId) {
        return ArticleResponse.from(articleRepository.findByIdOrElseThrow(articleId));
    }

    @Transactional
    public void delete(Long articleId) {
        articleRepository.deleteById(articleId);
    }
}
```

</details>

<details>
<summary>&#91; 코드 &#93; ArticleRepository</summary>

<a id="1c3eda9b0fe1811bb37acfef26728356"></a>

```java

package sub.board.article.repository;

import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.http.HttpStatus;
import org.springframework.stereotype.Repository;
import org.springframework.web.server.ResponseStatusException;
import sub.board.article.entity.Article;

@Repository
public interface ArticleRepository extends JpaRepository<Article, Long> {
    default Article findByIdOrElseThrow(Long id) {
        return findById(id).orElseThrow(() ->
                // TODO: Exception 헨들링
                new ResponseStatusException(HttpStatus.NOT_FOUND, "Article not found with id: " + id));
    }
}
```

</details>

<details>
<summary>&#91; 코드 &#93; Article</summary>

<a id="1c3eda9b0fe18132a2ddf602731fd53d"></a>

```java
package sub.board.article.entity;

import jakarta.persistence.Entity;
import jakarta.persistence.Id;
import jakarta.persistence.Table;
import lombok.*;

import java.time.LocalDateTime;

@Table(name = "article")
@Entity
@Getter
@ToString
@NoArgsConstructor(access = AccessLevel.PROTECTED)
public class Article {

    @Id
    private Long articleId;
    private String title;
    private String content;
    private Long boardId; // Shard Key
    private Long writerId;
    private LocalDateTime createdAt;
    private LocalDateTime modifiedAt;

    @Builder
    public Article(Long articleId, String title, String content, Long boardId, Long writerId) {
        this.articleId = articleId;
        this.title = title;
        this.content = content;
        this.boardId = boardId;
        this.writerId = writerId;
        this.createdAt = LocalDateTime.now();
        this.modifiedAt = this.createdAt;
    }

    public void update(String title, String content) {
        this.title = title;
        this.content = content;
        modifiedAt = LocalDateTime.now();
    }
}
```

</details>

<details>
<summary>&#91; 코드 &#93; ArticleCreateRequest</summary>

<a id="1c3eda9b0fe181159d7feea1e3315200"></a>

```java
package sub.board.article.service.request;

import lombok.Getter;
import lombok.ToString;

@Getter
@ToString
public class ArticleCreateRequest {
    private String title;
    private String content;
    private Long boardId;
    private Long writerId;
}
```

</details>

<details>
<summary>&#91; 코드 &#93; ArticleUpdateRequest</summary>

<a id="1c3eda9b0fe1818292cfd104ccd9da73"></a>

```java
package sub.board.article.service.request;

import lombok.Getter;
import lombok.ToString;

@Getter
@ToString
public class ArticleUpdateRequest {
	  private String title;
	  private String content;
}
```

</details>

<details>
<summary>&#91; 코드 &#93; ArticleResponse</summary>

<a id="1c3eda9b0fe181e2be40ee393f373b1f"></a>

```java
package sub.board.article.service.response;

import lombok.*;
import sub.board.article.entity.Article;

import java.time.LocalDateTime;

@Getter
@ToString
@NoArgsConstructor(access = AccessLevel.PRIVATE)
public class ArticleResponse {
    private Long articleId;
    private String title;
    private String content;
    private Long boardId;
    private Long writerId;
    private LocalDateTime createdAt;
    private LocalDateTime modifiedAt;
		
		// 정적 팩토리 메서드 패턴
    public static ArticleResponse from(Article article) {
        ArticleResponse response = new ArticleResponse();
        response.articleId = article.getArticleId();
        response.title = article.getTitle();
        response.content = article.getContent();
        response.boardId = article.getBoardId();
        response.writerId = article.getWriterId();
        response.createdAt = article.getCreatedAt();
        response.modifiedAt = article.getModifiedAt();
        return response;
   }
}
```

</details>
