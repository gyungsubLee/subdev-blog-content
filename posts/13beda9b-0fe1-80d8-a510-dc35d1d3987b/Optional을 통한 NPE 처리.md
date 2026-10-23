---
order: 1
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 13beda9b-0fe1-80d8-a510-dc35d1d3987b
title: Optional을 통한 NPE 처리
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 12eeda9b-0fe1-80f4-a546-d62ca61b62ff
    title: 4. 일정 관리 앱 v1
  - id: 138eda9b-0fe1-8017-91ab-e3adeaa05665
    title: 피드백 정리
  - id: 13beda9b-0fe1-80d8-a510-dc35d1d3987b
    title: Optional을 통한 NPE 처리
excerpt: reference - ‣ - ChatGPT 서론 --- Optional을 통한 NPE 처리를 고려를 하긴 했으나, 아직 정확하게 학습하지 못해 강의 코드를 참조하여 아래와 같이 if문을 통한 null 값 비교를 통해 NullPointException을 처리했다. java // NPE 방지 if (findSchedule =
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 138eda9b-0fe1-8017-91ab-e3adeaa05665
created: 2024-11-11T08:47:23.336Z
updated: 2024-11-11T11:17:01.414Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/4. 일정 관리 앱 v1-d62ca61b62ff/피드백 정리-e3adeaa05665/Optional을 통한 NPE 처리-dc35d1d3987b/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/13beda9b0fe180d8a510dc35d1d3987b
---
<details>
<summary>reference</summary>

- ‣

- ChatGPT

</details>

<a id="13beda9b0fe180528777c2853b162b80"></a>

### 서론 

---

<a id="13beda9b0fe1803a9895ee804aa9f9f1"></a>

Optional을 통한 NPE 처리를  고려를 하긴 했으나, 아직 정확하게 학습하지 못해 강의 코드를 참조하여 아래와 같이 <code>if문을 통한 null 값 비교</code>를 통해 <code>NullPointException</code>을 처리했다&#46; 

<a id="138eda9b0fe180edb06bd87b3c57a115"></a>

```java
// NPE 방지
if (findSchedule == null) {
		throw new ResponseStatusException(HttpStatus.NOT_FOUND, id + "에 해당하는 Schedule 이 존재하지 않습니다.");
}
```

<a id="13beda9b0fe180949454d9b81c271872"></a>

튜터님께서 추가 학습 내용으로 피드백을 해주셔서 겸사겸사 정리해보려고 한다&#46;

<a id="13beda9b0fe1808289ffcc76c7711549"></a>

### Opional 이란?

---

<a id="13beda9b0fe180c38ee7dfa8e4617121"></a>

Optional은 Java 8에 도입된 클래스로, Java&#46;util 패키지에 속해 있다&#46; 

<a id="13beda9b0fe180a2a7c0ca212a600acf"></a>

<code>null</code> 값으로 인한 오류를 줄이고 코드의 가독성을 높이기 위해 사용된다&#46;

<a id="13beda9b0fe180e89e93d396675028fb"></a>

Optional은 <u>값을 포함</u>하거나<u> 비어 있을 수 있는 </u><u>컨테이너 객체</u><u>이</u>다&#46;

-  <code>&#46;get()</code>를 통해 Optianal 객체 내부의 실제 값을 조회함

- Optional을 사용하게 되면 <code>nullable</code> 한 값에 대해 발생되는 <u>예외(NPM)를 피</u><u>할 수 있</u>다&#46;
    - NullPointerException 방지

    - null&#45;safe 하게 코드 작성 가능

- <strong><u>명시적인 null 체크</u></strong>를 하기 때문에 <code>nullable</code>한 상태를 <u>더 명확하게 표현</u>하며 <u>예외 상황(NPM)을 더 쉽게 처리</u>할 수 있고 <u>코드 가독성 높</u>이며 이로인해 <u>유지보수를 용이</u>하게 해준다&#46; 

- <u>제네릭</u>을 사용하여 만들어져 있어, <u>어떤 타입의 객체</u>라도 값이 없을 수 있는 경우 <u>Optional 사용 가능</u>

<a id="13beda9b0fe1805d9383dc7872bd5298"></a>

### 왜  Optional을 사용하는가? 

---

<a id="13beda9b0fe18022be68d24848204f3f"></a>

 <u>Java8전</u>에는 Optional이라는 클래스가 없었으므로, <u>메서드의 리턴 타입</u>으로 <code>‘결과 없음’</code>을  <code>null</code>을 사용하여 표현하였다&#46;

<a id="13beda9b0fe180ce8171e128bf3ed2ff"></a>

그러나 객체 값이 null인 경우에, <strong><u>null 체크 없</u></strong>이 해당 객체의 메서드를 호출하거나, 부주의하게 사용하는 경우 <strong> ‘NPE(NullPointerException)’이 발생</strong><strong>하면서</strong><strong> 프로그램이 죽어버리는 상황</strong><strong>이 발생되었다&#46;</strong>

<a id="13beda9b0fe180feb2e5c031b9665cd5"></a>

이를 방지하기 위해 자바8 버전부터 Optional이 도입되었다&#46; <strong><br></strong>

<a id="13beda9b0fe18083a38fe88c6232bd7e"></a>

### <strong>  Optional이 제공하는 메서드와 사용방법</strong>

---

<details>
<summary><code>Optional&#46;of(T value)</code></summary>

- null이 아닌<strong><u> 값을 감싸는 </u></strong><strong><u>Optional 객체 생성</u></strong>

- 만약 value가 null이면 NullPointerException이 발생

- ex)
    <a id="13beda9b0fe1806c95b0e1355c5d396a"></a>

    ```java
    Optional<String> optional = Optional.of("Hello");
    ```

</details>

<details>
<summary><code>Optional&#46;empty()</code></summary>

- 비어 있는 Optional 객체를 생성

<details>
<summary>ex)</summary>

<a id="13beda9b0fe1804081a0ebb255f86e19"></a>

```java
Optional<String> empty = Optional.empty();
```

</details>

</details>

<details>
<summary><strong><code>&#46;isPresent()</code></strong></summary>

- Optional의 값이 존재하면 <code>true</code>, 해당 값이 없으면 <code>false</code>를 리턴<br>

</details>

<details>
<summary><strong><code>&#46;isEmpty()</code></strong></summary>

-  Optional의 값이 비어있으면 <code>true</code>, 해당 값이 존재하면 <code>false</code>를 리턴
    - <strong><code>&#46;isPresent()</code></strong><strong> 반대</strong><br>

</details>

<details>
<summary><strong><code>&#46;get()</code></strong></summary>

- Optional이 감싸고 있는 <u>실제 값을</u> 얻기 위해서 사용

- 만일 Optional의 값이 비어있는 경우,<strong> </strong><strong><code>NoSuchElementException</code></strong>이 발생

> ⚠️ 
> 
> <a id="6bf6aabc95574c5c903f31c4cd0444a3"></a>
> 
> <strong><u>Null Safe</u></strong>한 상황이 아니라면, <code>isPresent(</code>) 또는<code> isEmpty()</code>로 값의 존재 여부를 체크 후,  <code>get()</code>를 사용해야 한다&#46;
> 
> <details>
> <summary>ex)</summary>
> 
> <a id="13beda9b0fe18035b2f8d144c016a2cb"></a>
> 
> ```java
> Optional<String> optionalString = Optional.of("Hello");
> 
> if (optionalString.isPresent()) {    // 값이 존재하는지 확인
>     System.out.println("Optional contains a value: " + optionalString.get());
> } else {
>     System.out.println("Optional is empty");
> }
> ```
> 
> </details>

</details>

<details>
<summary><strong><code>&#46;ifPresent(람다 함수)</code></strong><strong>, </strong><strong><code>&#46;ifPresentOrElse(람다 함수)</code></strong><strong>, </strong><strong><code>람다 함수</code></strong></summary>

- <code>ifPresent()</code>&#58; 값이 있는 경우 

- <code>ifPresentOrElse()</code>; <strong>값이 있는 경우와 없는 경우를 동시에 처리</strong>
    - Optional 클래스는 값이 없는 경우(empty), 대체 값이나 예외를 발생시킬 수 있는 <code>orElse()</code>, <code>orElseGet()</code>, <code>orElseThrow()</code> 메서드를 제공한다&#46;

<details>
<summary>ex)</summary>

<a id="13beda9b0fe18011aadaf99b2e544da1"></a>

아래와 같이 코드 작성 시,  if 문을 사용하는 것보다 간략하게 코드를 작성 가능하다&#46;

<a id="13beda9b0fe1800794c8da6d00b7cd12"></a>

```java

Optional<String> optionalString = Optional.of("Hello");

optionalString.ifPresent(val -> System.out.println("Optional contains a value: " + val), () -> System.out.println("Optional is empty"));
```

</details>

</details>

<details>
<summary><strong><code>&#46;orElse()</code></strong><strong>, </strong><strong><code>&#46;orElseGet()</code></strong><strong>, </strong><strong><code>&#46;orElseThrow()</code></strong></summary>

- <strong><code>&#46;orElse()</code></strong><strong>&#58;  </strong><strong><u>대체값 지정</u></strong>
    <a id="13beda9b0fe1802db83cf5a4302a4cd5"></a>

    ```java
    Optional<String> optionalString = Optional.of("Hello");

    // // 대체값 지정
    String value = optionalString.orElse("Default Value"); 
    ```

- <strong><code>&#46;orElseGet()</code></strong><strong>&#58; 대체 값 </strong><strong><u>람다합수 형태</u></strong><strong>로 지정</strong>
    <a id="13beda9b0fe1807e92afdfdfb90db758"></a>

    ```java
    Optional<String> optionalString = Optional.of("Hello");

    // 대체값을 람다함수로 지정
    String result = optionalString.orElseGet(() -> "Value from Supplier");
    ```

- <strong><code>&#46;orElseThrow()</code></strong><strong>&#58; </strong>값이 없을 때 예외 던짐
    - 람다 함수형태로 작성

    <a id="13beda9b0fe180be9ef3eaee26d77141"></a>

    ```java
    Optional<String> optionalString = Optional.of("Hello");

    // 값이 없는 경우, 예외 던짐
    String str = emptyOptional.orElseThrow(() -> new RuntimeException("Optional is empty"));
    ```

</details>

<details>
<summary><strong><code>&#46;or()</code></strong></summary>

- Java9부터 추가됨

- 값이 없는 경우, &#46;or() 내부 람다함수를 실행하며, 내부 람다 함수도 null 값일 수 있기 때문에<br><strong><code>&#46;orElse()</code></strong><strong>, </strong><strong><code>&#46;orElseGet()</code></strong><strong>, </strong><strong><code>&#46;orElseThrow()</code></strong><strong> 과 같이 사용함</strong>

<details>
<summary>ex) </summary>

<a id="13beda9b0fe18066863bf536d108c45d"></a>

```java
Optional<String> firstOptional = Optional.empty();  // 빈 객체
Optional<String> secondOptional = Optional.of("Hello, world!");

// 두 Optional 객체 중 하나라도 값이 존재하는 경우 값을 반환
		// 모두 값이 없는 경우 "Default Value" 반환
String result = firstOptional.or(() -> secondOptional).orElse("Default Value");

System.out.println("Result: " + result);
```

</details>

</details>

<details>
<summary><strong><code>&#46;filter(조건)</code></strong></summary>

- filter 조건에 맞는 요소만 실행됨
    <a id="13beda9b0fe180c18465e6525b9277ad"></a>

    ```java
    Optional<String> optionalString = Optional.of("Hello World");

    // filter, 문자열의 길이가 5 이상인 요소만 해당됨
    optionalString
    		.filter(s -> s.length() >= 5)
    		.ifPresent(s -> System.out.println("Filtered Value: " + s));
    ```

</details>

<details>
<summary><strong><code>&#46;map()</code></strong></summary>

- Optional 객체로 변환 후, for문 처럼 처리 가능

<a id="13beda9b0fe1800f81ccd46a10975e12"></a>

```java
Optional<String> optionalString = Optional.of("Hello World");

// map을 사용하여 문자열을 대문자로 변환
Optional<String> upperCaseOptional = optionalString.map(String::toUpperCase);
upperCaseOptional.ifPresent(s -> System.out.println("Uppercase Value: " + s))
```

</details>

<details>
<summary><strong><code>&#46;flatMap()</code></strong></summary>

<details>
<summary>🧐 <code>map()</code>과 <code>flatMap()</code>의 차이</summary>

- <code>map()</code>
    -  반환된 값을 Optional 안에 감싸기 때문에, 결과가 <u>중첩된 Optional </u>(<code>Optional&#60;Optional&#60;T&#62;&#62;</code>) 형태가 될 수 있다&#46;

- <code>flatMap()</code>
    - 반환된 <u>Optional을 평탄화</u>하여 <code>Optional&#60;T&#62;</code> 형태로 반환한다&#46;

    - 즉, 중첩된 Optional을 제거할 수 있다&#46; 

</details>

- 중첩된 Optional을 평탄화(flatten)하여 처리할 수 있도록 하는 메서드이다&#46;
    -  값이 존재하면 함수(mapper)를 적용하고, 그 결과로 Optional을 반환한다&#46;

- ex) 
    - map() 사용 시, 3중 Optional 객체로 생성됨
        - Optional ( User &#45;  Address )
            - Optional ( Optional ( Optional ( String )))

    - 이를 <code>flatMap()</code> 을 통해 평탄화(Optional 중복 제거)할 수 있다&#46; 

    <a id="13beda9b0fe1808bb41dc2b6d48666cd"></a>

    ```java
    public class User {
        private Optional<Address> address;

        public Optional<Address> getAddress() {
            return address;
        }
    }

    public class Address {
        private Optional<String> street;

        public Optional<String> getStreet() {
            return street;
        }
    }

    public class Main {
        public static void main(String[] args) {
            User user = new User();
            Optional<User> userOptional = Optional.of(user);

            // flatMap을 사용하여 중첩된 Optional을 평탄화 
            Optional<String> street = userOptional
                                        .flatMap(User::getAddress)
                                        .flatMap(Address::getStreet);

            street.ifPresent(System.out::println);
        }
    }
    ```

</details>

<a id="13beda9b0fe180299db7e51455cba90d"></a>

### 주의점

<details>
<summary>1&#46;<u> </u><strong><u>Optional 변수</u></strong><strong>에 </strong><strong><u>null 할당 ❌ </u></strong></summary>

<a id="13beda9b0fe180ed9b80ff50bac8e2d9"></a>

null을 사용하지 않기 위한 클래스인데 Optional을 null로 초기화하면 Optional의 사용 의도와 맞지 않는다&#46;

- 빈 값으로 Optional 생성 → <code>Optional&#46;empty()</code>

</details>

<details>
<summary>2&#46; <strong>Optional </strong><strong><u>필드 타입</u></strong><strong> 사용 ❌ </strong></summary>

<a id="13beda9b0fe180a38458f6c76d825e56"></a>

Optional은 <strong><u>메서드의 리턴 타입으로 사용</u></strong>하기 위한 용도로 설계되었다&#46; <br>따라서<strong><u> Optional을 클래스 필드로 선언하는 것은 잘못된 사용 방식</u></strong><strong>이다&#46;</strong>

<a id="13beda9b0fe1800d9e09ff8f92800420"></a>

→ <strong>필드 타입은 객체를 그대로 사용</strong>

</details>

<details>
<summary>3&#46;<u> </u><strong><u>메서드의 인자</u></strong><strong>로 Optional 사용 ❌ </strong></summary>

<a id="13beda9b0fe1802b8829f6cb3040cebf"></a>

위 내용과 동일, 메서드의 리턴 타입을 위한 용도이므로, <strong><u>메서드의 인자</u></strong><strong>도 역시 </strong><strong><u>객체를 그대로 사용</u></strong>

</details>

<details>
<summary>4&#46; <u>빈 컬렉션</u>이나 <u>빈 배열</u>을 나타낼 때, Optional 사용 ❌ </summary>

- 빈 컬렉션을 리턴하고자 하는 경우, Optional을 사용할 것이 아니라 <u>빈 컬렉션을 리턴</u>한다&#46;
    - <code>ArrayList</code>나 <code>HashMap</code> 등은 <u>최초 객체를 생성</u>하면 <strong>비어있는 컬렉션이 생성</strong>됨<br>이를 사용해 빈 객체 리턴

</details>

<details>
<summary>5&#46;<u> </u><strong><u>원시 타입을 값으로 가지는 Optional이 필요할 때</u></strong><strong>는 </strong><strong><u>원시 타입 용도로 만</u></strong><strong>들어진 </strong><strong><code>클래스</code></strong><strong>를 사용</strong></summary>

- 원시 타입(primitive type)을 Optional로 사용해야 할 때
    - <u> </u><u>Wrapper 클래스</u>로 된 Optional 클래스가 아닌
        -  <u>Optional, Optional, Optional 형태를 사용</u>하게 되면, boxing, unboxing이 일어나면서 성능이 저하된다&#46;

    - <u>원시 타입 용도로 만</u>들어진 <code>OptionalInt</code>, <code>OptionalLong</code>, <code>OptionalDouble</code> 형태의 클래스를 사용하는 것이 <strong><u>성능 측면에서 유리</u></strong>하다&#46;

</details>

<a id="13beda9b0fe180b4b237f30853b116d7"></a>

### Spring <strong>Data JPA 사용 예시 </strong>

- Java Spring 백엔드 개발을 하는 경우, DB 연동을 위해 ORM Framework인 JPA를 사용한다

- 이때 SpringData JPA에서 제공하는<strong> </strong><strong><u>JPA Repository의 메서드</u></strong><strong>에서 </strong><strong><u>return 타입이 Optional을 리턴</u></strong><strong>한다&#46;</strong>

---

<details>
<summary>ex 1) </summary>

<a id="13beda9b0fe180a2aa66f3f3eef43312"></a>

```java
public interface CrudRepository<T, ID> extends Repository<T, ID> {
    Optional<T> findById(ID id);
}
```

</details>

<details>
<summary>ex 2) </summary>

<a id="6bdf6cfe53d046099b4cc3a009635ae0"></a>

```java
@Service
@RequiredArgsConstructor
public class UserService {

    private final UserRepository userRepository;

    public void getUserById(Long userId) {
        Optional<User> userOptional = userRepository.findById(userId);
		    if (userOptional.isPresent()) {
		        User user = userOptional.get();
            System.out.println("User found: " + user.getName());
        } else {
            System.out.println("User not found with ID: " + userId);
        }
    }
}
```

</details>

<details>
<summary>ex 3) </summary>

<a id="8aa9ef200d5f4f5e9bde5379498e3a06"></a>

```java
@Entity
@Data
public class User {

    @Id
    @GeneratedValue(strategy = jakarta.persistence.GenerationType.IDENTITY)
    private Long id;
    private String username;
    private String email;
}
```

<a id="13beda9b0fe18089bdabe9a62875bf16"></a>

```java
@Repository
public interface UserRepository extends JpaRepository<User, Long> {

    Optional<User> findByUsername(String title);

    @Query("SELECT u FROM User u WHERE u.email = :email")
    Optional<User> findByEmail(@Param("email") String email);
}
```

</details>
