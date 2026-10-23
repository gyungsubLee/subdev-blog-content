---
order: 29
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-812c-af14-f511d3315b5c
title: Mockito를 사용한 테스트코드
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
    title: 대규모 시스템 설계
  - id: 1c3eda9b-0fe1-8151-a9bf-f4bde443f283
    title: 대규모 시스템 설계 - 게시판
  - id: 1c3eda9b-0fe1-812c-af14-f511d3315b5c
    title: Mockito를 사용한 테스트코드
excerpt: 1. Mockito - Mock 객체, given().willReturn() ✏️ Mock 객체는 테스트 시, 사용되는 가짜 객체이다. 실제 필드를 가지지 않으며, 실제 객체와 동일한 동작을 하도록 I/O 값을 지정해서 사용한다. - I/O 를 given().willReturn()을 통해 설정한다. 예제 java Comm
cover: null
icon: null
notionProperties:
  Tags: 추가
  중요도: Yes
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8151-a9bf-f4bde443f283
created: 2025-03-27T07:52:18.505Z
updated: 2025-03-27T07:52:18.505Z
legacy_path: Main/대규모 시스템 설계-d6a1706fbaf8/대규모 시스템 설계 - 게시판-f4bde443f283/Mockito를 사용한 테스트코드-f511d3315b5c/index.md
legacy_category: 대규모 시스템 설계
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1812caf14f511d3315b5c
---
<a id="1c3eda9b0fe1816f8fb2e3389b1dac42"></a>

### 1&#46; Mockito &#45; <code>Mock 객체</code>, <code>given()&#46;willReturn()</code>

> ✏️ 
> 
> <a id="1c3eda9b0fe181298307df36339a7f4d"></a>
> 
> Mock 객체는 테스트 시, 사용되는 가짜 객체이다&#46; 
> 
> <a id="1c3eda9b0fe1814eb966c3f3baf8c31d"></a>
> 
> 실제 필드를 가지지 않으며, 실제 객체와 동일한 동작을 하도록 I/O 값을 지정해서 사용한다&#46; 
> 
> - I/O 를 <code>given()&#46;willReturn()</code>을 통해 설정한다&#46; 

<details>
<summary>예제</summary>

<a id="1c3eda9b0fe181798a16ed7a162f8e70"></a>

```java
Comment comment = mock(Comment.class);  // Mock 객체 생성

given(comment.getArticleId()).willReturn(1L);  // articleId getter 설정,  settter를 통해 1L로 설정하고 getter로 조회하는 것과 동일한 동작을 함
given(comment.getCommentId()).willReturn(2L);  

System.out.println(comment.getArticleId()); // 1L 출력
System.out.println(comment.get(CommentId)); // 2L 출력
```

- mock 객체는 <strong><u>실제 필드를 가지지 않</u></strong>는다&#46; 
    - mock 객체 생성&#58; <code>mock(Comment&#46;class)</code>

- 따라서 <code>given()&#46;willReturn()</code>을 통해 <strong><u>특정 메서드에 대한 return을 설정</u></strong>할 수 있다&#46; <br>실제 필드는 존재하지 않지만 <strong><u>실제 필드가 있는 것처럼 동작에 대한 값 지정 가능</u></strong>
    - comment&#46;getArticleId 반환 값 지정&#58; <code>given(comment&#46;getArticleId())&#46;willReturn(1L);</code>

</details>

<details>
<summary>Mock 객체는 <strong>직접 필드에 값을 할당할 수 없</strong>다&#46; </summary>

<a id="1c3eda9b0fe181cf8c7bc54c3ba86a1e"></a>

```java
Comment comment = mock(Comment.class);
comment.setArticleId(1L);  // 아무런 효과 없음!
System.out.println(comment.getArticleId()); // null 출력됨

given(comment.getArticleId()).willReturn(1L);
System.out.println(comment.getArticleId()); // 1L 출력됨
```

<a id="1c3eda9b0fe181658337d9308818e9d2"></a>

위에서 설명했듯이 mock 객체는 필드가 존재하지 않는 가짜 객체이다&#46; 

<a id="1c3eda9b0fe1818fb351e9d2f4686d23"></a>

따라서 setter를 통해 객체의 필드 값을 설정해도 값이 존재하지 않기 때문에 <code>null</code>  값으로 반환된다 &#46;

- <code>given(comment&#46;getArticleId())&#46;willReturn(1L)</code>과 같이 <code>given()&#46;willReturn()</code> 을 통해 직접 return 값을 지정한다&#46; 

> ✏️ 
> 
> <a id="1c3eda9b0fe181aaa13dfca4292e3278"></a>
> 
> Mock 객체에서 필드 값 조회 시, <code>given()&#46;wiiReturn()</code>을 통해서만 필드 조회의 동작(<code>mock&#46;getField()</code>)에 대한 <strong><u>반환값을 지정</u></strong>하므로써 <strong><u>실제 객체와 동일하게 동작</u></strong>되도록 한다&#46;

</details>

<a id="1c3eda9b0fe1811db5a3ddeb8d4eb9da"></a>

### 2&#46; Mockito &#45; <code>verify()</code>

> ✏️ 
> 
> <a id="1c3eda9b0fe1819aaa9fffba2ad1c725"></a>
> 
> <strong><code>verity()</code></strong>는 특정 메서드가 실행 되었는지를 확인한다&#46; 
> 
> - <strong><u>비교 대상 없</u></strong>이, 단순하게 <strong><u>특정 메서드가 호출</u></strong> 되었는지만 확인한다&#46;

<details>
<summary>예제) <strong><code>verty()</code></strong></summary>

<a id="1c3eda9b0fe181cba304e16a4fb9d94a"></a>

```java
@Test
void verifyTest() {
    Comment comment = mock(Comment.class);

    // when
    comment.delete();  // delete() 메서드 호출

    // then
    verify(comment).delete();  // delete()가 실행되었는지 검증
}
```

- <code>verify(comment)&#46;delete();</code>
    - ‘<strong><code>comment&#46;delete()</code></strong>가 <strong><u>한 번 이상 호출</u></strong>되었는가?’ 를 확인한다&#46; 

    - 만약 comment&#46;delete() 가 <strong><u>호출되지 않</u></strong>았다면 <strong><u>테스트가 실패</u></strong>한다&#46; 

</details>

<details>
<summary>예제2) 호출 횟수 검증</summary>

<a id="1c3eda9b0fe181c39e1ec294d7136124"></a>

```java
verify(comment, times(1)).delete(); // delete()가 1번 호출되었는지 확인
verify(comment, times(2)).delete(); // delete()가 2번 호출되었는지 확인 (실패 가능)
verify(comment, never()).delete();  // delete()가 한 번도 호출되지 않았는지 확인
verify(comment, atLeastOnce()).delete(); // 최소 1번 호출되었는지 확인
verify(comment, atMost(3)).delete(); // 최대 3번 호출되었는지 확인
```

</details>

<a id="1c3eda9b0fe181b682bbd043b5cd9ec6"></a>

## 3&#46; <strong>기본적인 Mocking 패턴</strong>

<details>
<summary>🧐 <code>&#64;InjectMocks</code> 동작</summary>

<details>
<summary>동작</summary>

1. 객체 생성
    - <code>&#64;InjectMocks</code>로 명시한 클래스의 인스턴스를 생성한다&#46; 
        - Mock 객체가 아닌 실제 인스턴스를 생성한다&#46;

1. 의존성 탐색
    - 생성된 객체의 필드, 생성자, 세터 메서드를 리플렉션을 통해 분석한다&#46; 

1. 주입된 대상 식별
    - 테스트 클래스 내의 <code>&#64;Mock</code>, <code>&#64;Spy</code> 등으로 생성된 모의 객체를 식별한다&#46; 

1. 의존성 주입
    <a id="1c3eda9b0fe1819c9a60d875b83195bd"></a>

    아래의 순서로 의존성 주입을 시도한다&#46; 

    1. 생성자 주입

    1. Setter 주입

    1. 필드 주입

1. 타입 매칭
    - 주입 시 먼저 타입을 기준으로 매칭한다&#46; 

    - 동일한 타입의 Mock 객체가 여러개 있는 경우, 필드 이름과 모의 객체 이름을 비교하여 매칭한다&#46; 

</details>

<details>
<summary>예시 </summary>

<a id="1c3eda9b0fe1813580a8fee1a1c719c1"></a>

```java
@Service
@RequiredArgsConstructor
public class CommentService {
    private final CommentRepository commentRepository;

    // 생성자
    // public CommentService(CommentRepository commentRepository) {
    //     this.commentRepository = commentRepository;
    // }

    // 메서드들...
}

@ExtendWith(MockitoExtension.class)
class CommentServiceTest {
    @Mock
    private CommentRepository commentRepository;

    @InjectMocks
    private CommentService commentService;

    // 테스트 메서드들...
}
```

<a id="1c3eda9b0fe18122a7f1cee6e8e92d4d"></a>

위 예시의 경우 아래와 같이 동작한다&#46; 

1. CommentService 인스턴스 생성

1. CommentService의 생성자를 분석하여 CommentRepository 타입의 의존성이 필요함을 확인한다&#46;

1. 테스트 클래스에서 &#64;Mock으로 생성된 commentRepository 객체를 찾는다&#46;

1. CommentService의 생성자를 호출하면서 mock commentRepository를 주입한다&#46;

1. 

</details>

> ✏️ 
> 
> <a id="1c3eda9b0fe181889943d204eee6d94a"></a>
> 
> <strong>정리 </strong>
> 
> <a id="1c3eda9b0fe181d5b586fa2bc7a338fd"></a>
> 
> <strong><code>&#64;InjectMocks</code></strong>는 <u>테스트 환경</u>에서 <strong><u>의존성 주입을 자동화</u></strong>하여, 스프링의 IoC 컨테이너와 유사한 역할을 수행한다&#46; 
> 
> <a id="1c3eda9b0fe181abaf58e6d9a784b589"></a>
> 
> 그러나 <u>테스트에 특화</u>되어 있어, 실제 애플리케이션의 IoC 컨테이너만큼 복잡하거나 강력하지는 않다&#46;

</details>

<a id="1c3eda9b0fe181f1a20dde9a6970ef3b"></a>

### 1&#46; <strong><code>&#64;Mock</code></strong>을 사용한 의존성 객체 Mocking &#45; <code>&#64;Mock</code>, <code>&#64;InjectMcoks</code> 

<a id="1c3eda9b0fe181169fbfdad0a37cd5d8"></a>

<strong>예제</strong>

<a id="1c3eda9b0fe18156ae06e2b91b6124fa"></a>

```java
@ExtendWith(MockitoExtension.class) // JUnit5와 함께 사용
class CommentServiceTest {

    @Mock  // CommentRepository를 Mock 객체로 생성
    private CommentRepository commentRepository;

    @InjectMocks  // CommentService에 Mock 객체 자동 주입
    private CommentService commentService;

    @Test
    void deleteShouldMarkDeletedIfHasChildren() {
        // given
        Long commentId = 1L;
        Comment comment = mock(Comment.class);
        given(commentRepository.findByIdOrElseThrow(commentId)).willReturn(comment);
        given(commentRepository.countBy(any(), any(), any())).willReturn(2L);

        // when
        commentService.delete(commentId);

        // then
        verify(comment).delete(); // delete() 메서드가 실행되었는지 확인
    }
}
```

- <strong><code>&#64;Mock</code></strong>&#58;  commentRepository를 <strong><u>Mock 객체</u></strong>로 생성

- <strong><code>&#64;InjectMocks</code></strong>&#58; commentService 에 &#64;Mock으로 선언한 객체가 자동으로 주입됨
    - 위 예시에서는 Mock 객체로 생성된 commentRepositroy가 자동으로 주입됨

> ☝🏻 
> 
> <a id="1c3eda9b0fe1813eba41f5504a755cd6"></a>
> 
> <strong><code>&#64;Mock</code></strong><strong> 은 직접  인스턴스(</strong><code>new CommentRepository()</code>)<strong>를 생성하는 것이 아닌 </strong><u>Mock 객체를 생성</u><strong>한 한다&#46; </strong>
> 
> - 동작을 추가로 지정해줘야 한다&#46; ( <strong>Stubbing</strong> )
>     <a id="1c3eda9b0fe181878a26d585b5064ec9"></a>
> 
>     → <code>given()&#46;willReturn()</code> …

<a id="1c3eda9b0fe181d5a582de23ed8fcef1"></a>

### 2&#46; <strong> 메서드 동작 정의 (Stubbing)</strong>

<details>
<summary>1&#46; <strong><code>given</code></strong><strong><code>()&#46;</code></strong><strong><code>willReturn</code></strong><strong><code>()</code></strong>을 사용한 <strong><u>특정 메서드 호출 시 반환 값 설정</u></strong></summary>

<a id="1c3eda9b0fe181deb76eda70ca1aeecb"></a>

```java
given(commentRepository.findByIdOrElseThrow(1L)).willReturn(mock(Comment.class));
```

- <strong>해당 메서드가 실행될 때 Mock 객체를 반환하도록 설정</strong>
    - <code>mock(Comment&#46;class)</code> 반환

</details>

<details>
<summary><strong>2&#46; </strong><strong><code>given()&#46;</code></strong><strong><code>willThrow()</code></strong><strong> 사용 (예외 발생 테스트)</strong></summary>

<a id="1c3eda9b0fe181ac9759fb383043c4fe"></a>

```java
given(commentRepository.findByIdOrElseThrow(99L))
        .willThrow(new RuntimeException("댓글을 찾을 수 없습니다."));
```

- findByIdOrElseThrow(99L) 호출 시 <strong>RuntimeException 발생</strong>하도록 설정

</details>

<details>
<summary><strong>3&#46; </strong><strong><code>doReturn</code></strong><strong><code>()&#46;</code></strong><strong><code>when</code></strong><strong><code>()</code></strong><strong>&#45; </strong> <strong>Void 메서드나 spy 객체에서 사용</strong></summary>

<a id="1c3eda9b0fe18127a31de3264806c6d1"></a>

```java
// given().willReturn() 사용
given(mockObject.someMethod()).willReturn("Hello");

// doReturn() 사용
doReturn("Hello").when(mockObject).someMethod();
```

- given()&#46;willReturn() → <strong>일반적인 메서드 Stubbing</strong>

- doReturn()&#46;when() → <strong>Void 메서드나 spy 객체에서 사용할 때 필요</strong>

</details>

<a id="1c3eda9b0fe18157aea6f8cebca8bcc2"></a>

### <strong>3&#46; 특정 메서드 호출 검증 (</strong><strong><code>verify()</code></strong><strong>)</strong>

<a id="1c3eda9b0fe181228453e6fcff890f48"></a>

```java
verify(commentRepository).deleteById(1L); // 특정 메서드가 실행되었는지 검증
verify(commentRepository, times(1)).deleteById(1L); // 1번 호출되었는지 검증
verify(commentRepository, never()).deleteById(2L); // 한 번도 호출되지 않았는지 검증
verify(commentRepository, atLeastOnce()).deleteById(1L); // 최소 1번 호출되었는지 검증
verify(commentRepository, atMost(3)).deleteById(1L); // 최대 3번 호출되었는지 검증
```

- 특정 메서드가 실행되었는지 검증할 때 사용

- 호출 횟수(<code>times()</code>, <code>never()</code>, <code>atLeastOnce()</code> 등) 지정 가능

<a id="1c3eda9b0fe181be9809fa606973dcc9"></a>

### 4&#46; <strong>ArgumentCaptor을 사용한 전달된 인자 검증</strong>

<a id="1c3eda9b0fe181f4a0afe5a0f70f7e59"></a>

Mock 객체가 특정 메서드를 호출할 때, <strong>전달된 인자가 올바른지 검증한다&#46;</strong>

<a id="1c3eda9b0fe181b69b57c00c94618478"></a>

```java
@ExtendWith(MockitoExtension.class)
class CommentServiceTest {

    @Mock
    private CommentRepository commentRepository;

    @InjectMocks
    private CommentService commentService;

    @Test
    void testArgumentCaptor() {
        // given
        ArgumentCaptor<Long> captor = ArgumentCaptor.forClass(Long.class);

        // when
        commentService.delete(1L);

        // then
        verify(commentRepository).deleteById(captor.capture());
        assertThat(captor.getValue()).isEqualTo(1L); // 전달된 인자 검증
    }
}
```

- ArgumentCaptor는 <strong>실제 메서드가 호출될 때 전달된 값을 검증</strong>할 수 있다&#46;

- <code>captor&#46;capture()</code>를 사용하여 전달된 인자를 잡아 <code>assertThat()</code>으로 비교하여 값을 검증한다&#46; 

<a id="1c3eda9b0fe181a9873ce8e7ca8cd244"></a>

### 5&#46; <strong>spy()를 사용한 부분 Mocking</strong>

<a id="1c3eda9b0fe18196b8bac243a2faae9d"></a>

<strong><code>Mock 객체</code></strong>는 기본적으로 메서드를 실행하지 않지만, <br><strong><code>Spy 객체</code></strong>는 <strong><u>실제 객체의 메서드를 실행</u></strong><strong>하면서 </strong><strong><u>일부만 Mocking 가능</u></strong>하다

<a id="1c3eda9b0fe181c2a255c0baabd78c54"></a>

<strong>Mocking 가능</strong>

<a id="1c3eda9b0fe181c2b195ee0c5ae14d33"></a>

```java
List<String> list = spy(new ArrayList<>());
list.add("Hello");

verify(list).add("Hello"); // add() 메서드가 실행되었는지 검증
assertThat(list.size()).isEqualTo(1); // 실제 리스트 크기 검증
```

- <strong><code>spy()</code></strong><strong>는 실제 객체를 감싸서 일부만 Mocking 가능</strong>

<a id="1c3eda9b0fe181a0b0e1e0436636aa12"></a>

<strong><code>spy()</code></strong><strong> 사용 시, </strong><strong><code>doReturn()</code></strong><strong>을 이용한 Stubbing 필요</strong>

<a id="1c3eda9b0fe181e19182fcc109c51444"></a>

```java
List<String> list = spy(new ArrayList<>());
doReturn(100).when(list).size(); // 리스트 크기를 100으로 Mocking

assertThat(list.size()).isEqualTo(100);
```

<a id="1c3eda9b0fe1816db6c1da9d419b34a5"></a>

### 6&#46; <strong>doNothing()을 사용한 Void 메서드 처리</strong>

<a id="1c3eda9b0fe181659455ffe1cf6855c8"></a>

```java
doNothing().when(commentRepository).deleteById(1L);
commentService.delete(1L);
verify(commentRepository, times(1)).deleteById(1L);
```

- <strong>Void 메서드는 </strong><strong><u><code>given()&#46;willReturn()</code></u></strong><strong><u>을 사용할 수 없</u></strong><strong>기 때문에 </strong><strong><code>doNothing()</code></strong><strong> 사용</strong>

<a id="1c3eda9b0fe1812c8c1ede2084eb584a"></a>

### 7&#46; <strong>timeout()을 이용한 비동기 검증</strong>

<a id="1c3eda9b0fe18114879efb8cd22fce91"></a>

Mockito는 <strong>비동기 호출을 검증</strong>하는 기능도 제공한다&#46;

<a id="1c3eda9b0fe1811682fae863c989cc26"></a>

```java
verify(commentRepository, timeout(1000)).deleteById(1L); // 1초 내 실행 확인
```

- <code>timeout(1000)</code> → <strong><u>1초 이내에 deleteById(1L)이 호출</u></strong>되었는지 검증

<a id="1c3eda9b0fe181399b5aeffd63603399"></a>

### <strong>Mockito에서 자주 사용하는 패턴 총정리</strong>

| <strong>패턴</strong> | <strong>설명</strong> | <strong>예제</strong> |
| --- | --- | --- |
| <code>&#64;Mock</code> | Mock 객체 생성 | <code>&#64;Mock private CommentRepository repository;</code> |
| <code>&#64;InjectMocks</code> | Mock을 주입할 객체 자동 생성 | <code>&#64;InjectMocks private CommentService service;</code> |
| <code>given()&#46;willReturn()</code> | 특정 메서드 호출 시 원하는 값 반환 | <code>given(repository&#46;findById(1L))&#46;willReturn(comment);</code> |
| <code>given()&#46;willThrow()</code> | 특정 메서드 호출 시 예외 발생 | <code>given(repository&#46;findById(99L))&#46;willThrow(new RuntimeException());</code> |
| <code>verify()</code> | 특정 메서드가 실행되었는지 검증 | <code>verify(repository)&#46;deleteById(1L);</code> |
| <code>times(n)</code> | 메서드 실행 횟수 검증 | <code>verify(repository, times(1))&#46;deleteById(1L);</code> |
| <code>ArgumentCaptor</code> | 전달된 인자 검증 | <code>assertThat(captor&#46;getValue())&#46;isEqualTo(1L);</code> |
| <code>spy()</code> | 실제 객체를 감싸 일부만 Mocking | <code>List&#60;String&#62; list = spy(new ArrayList&#60;&#62;());</code> |
| <code>doNothing()</code> | Void 메서드 Stubbing | <code>doNothing()&#46;when(repository)&#46;deleteById(1L);</code> |
| <code>timeout()</code> | 비동기 검증 | <code>verify(repository, timeout(1000))&#46;deleteById(1L);</code> |
