---
order: 13
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-817c-91be-eddc56e018ec
title: SHA-256을 활용한 Password 해싱
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-812e-b8ac-c13c536efd00
    title: Spring Boot를 활용한 채팅 서비스 만들어보기
  - id: 1c3eda9b-0fe1-817c-91be-eddc56e018ec
    title: SHA-256을 활용한 Password 해싱
excerpt: "SHA-256을 활용한 Password 해싱 --- 📖 🧐 SHA-256 [ 코드 ] AuthService java @Slf4j @Service @RequiredArgsConstructor public class AuthService { private final UserRepository userRepository; "
cover: null
icon: null
notionProperties:
  상태: 진행 중
schema_version: 1
parent_id: 1c3eda9b-0fe1-812e-b8ac-c13c536efd00
created: 2025-03-27T07:53:11.124Z
updated: 2025-03-27T07:53:11.124Z
legacy_path: Main/Spring ( Java )-cd1f71740107/Spring Boot를 활용한 채팅 서비스 만들어보기-c13c536efd00/SHA-256을 활용한 Password 해싱-eddc56e018ec/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1817c91beeddc56e018ec
---
<a id="1c3eda9b0fe181ee8a10f5f7bb0d610e"></a>

## SHA&#45;256을 활용한 Password 해싱

---

> 📖 

<details>
<summary>🧐 SHA&#45;256</summary>



</details>

<details>
<summary>&#91; 코드 &#93; AuthService</summary>

<a id="1c3eda9b0fe181ffa9cfc125713ee452"></a>

```java
@Slf4j
@Service
@RequiredArgsConstructor
public class AuthService {

    private final UserRepository userRepository;
    private final Hasher hasher;

    @Transactional(transactionManager = "createUserTranscationManager")
    public CreateUserResponse createUser(CreateUserRequest request) {

        Optional<User> findUser = userRepository.findByName(request.name());

        // TODO: 예외처리 - 생성하려는 유저의 가입 내역 존재
        if (findUser.isPresent()) {

        }

        try {
            User newUser = this.newUser(request.name());
            UserCredentials userCredentials = newUserCredentials(newUser, request.password());
            newUser.setCredentials(userCredentials);

            User saveUser = userRepository.save(newUser);

            if (saveUser == null) {
                // TODO: 예외처리 - 유저 DB 저장 오류

            }
        } catch (Exception e) {
            // TODO: 예외처리 - 유저 DB 저장 로직 중 오류 발생

        }

        return new CreateUserResponse(request.name());
    }

    private User newUser(String name) {
        return User.builder()
                .name(name)
                .created_at(new Timestamp(System.currentTimeMillis()))
                .build();
    }

    private UserCredentials newUserCredentials(User user, String password) {
        return UserCredentials.builder()
                .user(user)
                .hashed_password(hasher.getHashingValue(password))
                .build();
    }
}
```

</details>

<details>
<summary>&#91; 코드 &#93; Hasher</summary>

<a id="1c3eda9b0fe181aab86cf16bcfabca4d"></a>

```java
@Service
public class Hasher {

    public String getHashingValue(String password) {
        try {
            MessageDigest digest = MessageDigest.getInstance("SHA-256");
            byte[] hash = digest.digest(password.getBytes(StandardCharsets.UTF_8));

            return Base64.getEncoder().encodeToString(hash);
        } catch (NoSuchAlgorithmException e) {
            // TODO: handle exception
            throw new RuntimeException("Hash Failed", e);
        }
    }
}
```

- MessageDigest

- MessageDigest&#46;getInstance(&#34;SHA&#45;256&#34;)
    - 해시 알고리즘 <code>SHA&#45;256</code> 가져오기 

- MessageDigest&#46;digest(password&#46;getBytes(StandardCharsets&#46;UTF&#95;8))
    - UTF&#95;8로 인코딩

- Base64&#46;getEncoder()&#46;encodeToString(hash);
    - Base64 인코딩 

</details>
