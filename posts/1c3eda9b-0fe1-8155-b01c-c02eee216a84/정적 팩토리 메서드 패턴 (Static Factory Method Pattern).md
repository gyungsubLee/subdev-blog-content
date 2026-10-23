---
order: 14
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8155-b01c-c02eee216a84
title: 정적 팩토리 메서드 패턴 (Static Factory Method Pattern)
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
    title: 대규모 시스템 설계
  - id: 1c3eda9b-0fe1-8151-a9bf-f4bde443f283
    title: 대규모 시스템 설계 - 게시판
  - id: 1c3eda9b-0fe1-8155-b01c-c02eee216a84
    title: 정적 팩토리 메서드 패턴 (Static Factory Method Pattern)
excerpt: 정적 팩토리 메서드 패턴 (Static Factory Method Pattern) --- ✏️ new 키워드를 사용하지 않고, 객체 생성을 캡슐화 하는 패턴 - 클래스 내부에서 static 메서드를 제공하여 인스턴스 를 바로 반환 → 생성자 역할을 하는 정적(static) 메서드를 통해 객체 생성 장점 - 이름을 통해 가
cover: null
icon: null
notionProperties:
  Tags: 🧐 질문
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8151-a9bf-f4bde443f283
created: 2025-03-27T07:52:18.662Z
updated: 2025-03-27T07:52:18.662Z
legacy_path: Main/대규모 시스템 설계-d6a1706fbaf8/대규모 시스템 설계 - 게시판-f4bde443f283/정적 팩토리 메서드 패턴 (Static Factory Method Pattern)-c02eee216a84/index.md
legacy_category: 대규모 시스템 설계
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18155b01cc02eee216a84
---
<a id="1c3eda9b0fe1815fb771e66653b1298e"></a>

## 정적 팩토리 메서드 패턴 <strong>(Static Factory Method Pattern)</strong>

---

> ✏️ 
> 
> <a id="1c3eda9b0fe181208139ddaf335acb99"></a>
> 
> <code>new</code> 키워드를 <strong><u>사용하지 않</u></strong>고, <strong><u>객체 생성을 캡슐</u></strong><strong><u>화 </u></strong>하는 패턴
> 
> - 클래스 내부에서 <strong><u>static 메서드를 제공</u></strong>하여 <strong><u>인스턴스 를 바로 반환</u></strong>
> 
> <a id="1c3eda9b0fe181adac92cbdbbbf503e3"></a>
> 
>          → 생성자 역할을 하는 정적(static) 메서드를 통해 객체 생성

<details>
<summary><strong>장점</strong></summary>

- <strong>이름을 통해 가독성을 높일 수 있음</strong>
    - ArticleResponse&#46;from(article) → 의미가 명확

    - 반면, new ArticleResponse(article)은 의미가 직관적이지 않을 수 있음

- <strong>객체 생성을 제어 가능</strong>
    - 필요에 따라 <strong>캐싱, 싱글턴 패턴 적용, 서브타입 반환</strong> 등이 가능

- <strong>생성자를 은닉하여 불필요한 new 호출을 막을 수 있음</strong>
    - private 생성자와 함께 사용하면 불변 객체 패턴에도 활용 가능

</details>

<a id="1c3eda9b0fe18194bce1e49063ada865"></a>

### 예시1) 객체 내부에서 필드 할당

<details>
<summary>&#91; 전체 코드 &#93; ArticleResponse</summary>

<a id="1c3eda9b0fe181cc8840f09867485f43"></a>

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

<a id="1c3eda9b0fe1814fb2f5d0bc9446bb15"></a>

```java
@Getter
@ToString
@NoArgsConstructor(access = AccessLevel.PRIVATE)
public class ArticleResponse {

      . . .

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

<a id="1c3eda9b0fe181208f9beee36d18f664"></a>

### 예시2) 빌더 패턴(<code>&#64;Builder</code>)

- Lombok의 &#64;Builder와 함께 사용

<a id="1c3eda9b0fe181bc961bca777a0cfbfa"></a>

```java
@Getter
@Builder
public class ArticleResponse {
    private Long articleId;
    private String title;
    private String content;
    private Long boardId;
    private Long writerId;
    private LocalDateTime createdAt;
    private LocalDateTime modifiedAt;

    public static ArticleResponse from(Article article) {
        return ArticleResponse.builder()
                .articleId(article.getArticleId())
                .title(article.getTitle())
                .content(article.getContent())
                .boardId(article.getBoardId())
                .writerId(article.getWriterId())
                .createdAt(article.getCreatedAt())
                .modifiedAt(article.getModifiedAt())
                .build();
    }
}
```

- new 없이도 ArticleResponse를 쉽게 생성 가능

- 위와 동일하게 <strong><u>불변 객체(Immutable Object)</u></strong>로 설계 가능

---

<details>
<summary>빌더 패턴 사용의 장•단점</summary>

- 장점
    <details>
    <summary><strong>필드 선택적 생성 가능</strong></summary>

    - <code>title</code>과 <code>content</code>만 설정
        <a id="1c3eda9b0fe1811885c5c2b74df8348a"></a>

        ```java
        ArticleResponse response = ArticleResponse.builder()
            .title("Sample Title")
            .content("Sample Content")
            .build();
        ```

    </details>

    - <strong>가독성이 좋음</strong> (체이닝 방식으로 값 설정)

- <strong>단점</strong>
    - <strong>중간(빌더) 객체 생성 비용이 증가</strong> (빌더 객체 생성 → 최종 객체 생성)

    - <strong>필드가 많지 않으면 오버스펙</strong>

</details>

> ☝🏻 
> 
> <a id="1c3eda9b0fe181b9b662f4d669232427"></a>
> 
> 빌더 패턴은 <strong>객체 생성 시 </strong>생성 객체의 <strong><u>필드가 많</u></strong>아 <strong><u>인자로 넘기는 값이 많은 경우</u></strong> 사용이 적절하다&#46; 
> 
> - 이전 정리 내용) <a href="#/post/1c3eda9b-0fe1-8196-ad8d-e7a04eac7b77">페이지</a> 
> 
> <a id="1c3eda9b0fe18106a463da3f0cdcef29"></a>
> 
> 위 예시의 경우는 인자로 <strong><u>엔티티 객체 자체를 넘</u></strong>기기 때문에 빌더 사용이 오히려 <strong><u>불필요한 비용을 발생</u></strong>시킨다&#46;
> 
> - 빌더 객체 생성 → 최종 객체 생성
