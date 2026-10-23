---
order: 19
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: fffeda9b-0fe1-819c-9589-f86fe1898e02
title: Lv1. 랜덤 닉네임 생성기
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 10aeda9b-0fe1-80df-a9e7-c0a68dc3edaa
    title: Spring 사전캠프 퀘스트 모음집
  - id: fffeda9b-0fe1-819c-9589-f86fe1898e02
    title: Lv1. 랜덤 닉네임 생성기
excerpt: 과제를 끝내고 나면 할 수 있어요! - java/kotlin 에서 변수를 이해하고 선언할 수 있어요. - java/kotlin 의 배열을 이해하고 사용할 수 있어요. - java/kotlin 의 함수를 이해하고 사용할 수 있어요. - java/kotlin 의 random 라이브러리를 활용할 수 있어요. - 완결된 java
cover: null
icon: 📔
notionProperties: {}
schema_version: 1
parent_id: 10aeda9b-0fe1-80df-a9e7-c0a68dc3edaa
created: 2024-09-23T10:56:26.501Z
updated: 2024-09-23T10:56:26.501Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/Spring 사전캠프 퀘스트 모음집-c0a68dc3edaa/Lv1. 랜덤 닉네임 생성기-f86fe1898e02/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/fffeda9b0fe1819c9589f86fe1898e02
---
<details>
<summary>과제를 끝내고 나면 할 수 있어요&#33;</summary>

- java/kotlin 에서 변수를 이해하고 선언할 수 있어요&#46;

- java/kotlin  의 배열을 이해하고 사용할 수 있어요&#46;

- java/kotlin  의 함수를 이해하고 사용할 수 있어요&#46;

- java/kotlin  의 random 라이브러리를 활용할 수 있어요&#46; 

- 완결된 java/kotlin  프로그램을 만들 수 있어요&#46;

</details>

> ⚡ <strong>Notification&#58; 과제 시작 전 확인할 내용&#33;</strong>

- [ ] 개발환경 구축 완료

- [ ] 자바 파일 생성 후 실행 가능

- [ ] 기본 데이터 유형 중 리스트(lists)를 이해

<details>
<summary>과제 수행을 위해 참고하면 좋을 만한 자료</summary>

[02장 자바 시작하기]()

</details>

> 🍀 <strong>본격적으로 시작해 볼까요?</strong>

- <strong>랜덤한 닉네임을 생성하는 자바 코드를 작성해보세요&#46; </strong>

![](bdba4efe91326aa5.webp)

1. <strong>사용자는 최소 27가지 이상의 닉네임 중 하나를 랜덤으로 출력 할 수 있습니다&#46;</strong><br>(아래의 키워드를 사용해주세요&#33;)
    - 기철초풍, 멋있는, 재미있는

    - 도전적인, 노란색의, 바보같은

    - 돌고래, 개발자, 오랑우탄 

<a id="fffeda9b0fe18130996ec107062dccba"></a>

&#42;10분 동안 고민하고 해결되지 않을때 보기&#42;

<details>
<summary>힌트 1단계</summary>

<a id="fffeda9b0fe181c8b021f751905fd83e"></a>

java 의 <code>Random</code> 라이브러리를 활용해보세요

<a id="fffeda9b0fe18119acabde24821c76f6"></a>

```java
import java.util.Random;
```

</details>

<details>
<summary>힌트 2단계</summary>

<a id="fffeda9b0fe181e0bfcfd2b4709efbc0"></a>

```java

import java.util.Random;

public class RandomNicknameCreator {

    private String[] firstList = {"기철초풍", "멋있는", "재미있는"};
    private String[] secondList = {"도전적인", "노란색의", "바보같은"};
    private String[] thirdList = {"돌고래", "개발자", "오랑우탄"};

    public String createRandomNickname() {
        // 여기에 랜덤으로 닉네임을 만드는 코드를 적어주세요

        return "랜덤으로 생성된 닉네임";
    }

    public static void main(String[] args) {
        RandomNicknameCreator randomNicknameCreator = new RandomNicknameCreator();
        String myNickname = randomNicknameCreator.createRandomNickname();
        System.out.println(myNickname);
    }
}
```

</details>

> 🔥 <strong>완료하셨다면?</strong>

- 과제를 수행하며 고민하고 검색했던 내용을 모아 TIL을 작성해주세요&#46;

- 최종코드와 함께 업로드한 TIL을 제출해주세요&#46;

- <strong>원활하게 작동되는 정답코드를 퀘스트로 제출해주세요 👉 </strong><strong><a href="https://forms.gle/pomadzyiNKAyw4CB8">https&#58;//forms&#46;gle/pomadzyiNKAyw4C</a></strong>
