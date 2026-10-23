---
order: 16
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1dbeda9b-0fe1-8024-ad2e-e49032bfda79
title: rem ( root em )
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1dbeda9b-0fe1-8024-ad2e-e49032bfda79
    title: rem ( root em )
excerpt: rem --- 📖 rem은 “root em” 의 줄임말이다. - root = HTML 최상위 요소 (<html>) - em = “어떤 요소의 폰트 크기”를 기준으로 상대적으로 크기를 정하는 단위 따라서 rem은 html 태그에 설정된 font-size를 기준으로 크기를 정하는 것을 말한다. rem의 기본 작동 방식 기본
cover: null
icon: null
notionProperties:
  Tags: 단위
  중요도: Yes
  상태: 완료
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-20T01:01:34.995Z
updated: 2025-04-20T01:16:00.365Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/rem ( root em )-e49032bfda79/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1dbeda9b0fe18024ad2ee49032bfda79
---
<a id="1dbeda9b0fe18084a977c46ee4bccb0e"></a>

## <strong><br>rem</strong>

---

> 📖 
> 
> <a id="1dbeda9b0fe1800ba8e5e344b9ee8383"></a>
> 
> <strong><code>rem</code></strong>은 <strong><u>“root em” 의 줄임말</u></strong>이다&#46;
> 
> - <code>root</code> = HTML 최상위 요소 (<code>&#60;html&#62;</code>)
> 
> - <code>em</code> = “<strong><u>어떤 요소의 폰트 크기”를 기준</u></strong>으로 <strong>상대적으로 크기를 정</strong>하는 단위
> 
> <a id="1dbeda9b0fe180909b19eeaaae53d82b"></a>
> 
> 따라서 <code>rem</code>은 <strong><u>html 태그에 설정된 font&#45;size를 기준</u></strong><u>으로 크기를 정</u>하는 것을 말한다&#46; 

<details>
<summary><strong> rem의 기본 작동 방식</strong></summary>

> <strong>기본 브라우저 설정&#58;  16px</strong>

| <strong>rem 값</strong> | <strong>실제 px 값 (기본 16px 기준)</strong> |
| --- | --- |
| <code>1rem</code> | 16px |
| <code>0&#46;5rem</code> | 8px |
| <code>2rem</code> | 32px |
| <code>3rem</code> | 48px |

- <code>1rem</code> = <code>&#60;html&#62;</code> font&#45;size의 100%

</details>

<details>
<summary>ex) <code>2rem</code></summary>

1. 아무 설정이 없는 경우
    <a id="1dbeda9b0fe180e4bb95e7a0ff1306ca"></a>

    ```html
    <html>
    <body>
      <h1 style="font-size: 2rem;">Hello</h1>
    </body>
    </html>
    ```

    - <code>2rem</code> = <code>2</code> × <code>16px</code> = <code>32px</code>

1. <strong>root 폰트 사이즈를 바꾼 경우</strong>
    <a id="1dbeda9b0fe1805c9567c90be327dc25"></a>

    ```css
    html {
      font-size: 10px;
    }
    ```

    <a id="1dbeda9b0fe18070ab84c9853748ee37"></a>

    ```html
    <h1 style="font-size: 2rem;">Hello</h1>
    ```

    - <code>h1&#58; 2rem</code> → <code>20px</code>
        - <code>2rem</code> = <code>2</code> × <code>10px</code> = <code>20px</code>

</details>

<details>
<summary>왜 rem을 쓰는가?</summary>

- <strong>반응형 레이아웃</strong> 짤 때 <strong><u>일관성 유지</u></strong>하기 좋다&#46;

- 사이트 <u>전체 폰트 크기를 </u><strong><u>한 번에 조정</u></strong>할 수 있다&#46;
    - html DOM의 폰트 크기만 조정하면 된다&#46;

- <strong>접근성(accessibility)</strong> 높이는 데도 좋다&#46;
    - 사용자가 <strong><u>브라우저 폰트 크기를 키워도, rem은 따라 키워져서 잘 보이게 된</u></strong>다&#46;<br><br><br><br><br>

</details>

<details>
<summary><strong><code>em</code></strong><strong> vs </strong><strong><code>rem</code></strong><strong> 차이</strong></summary>

> ☝🏻 
> 
> <a id="1dbeda9b0fe1801c9100ef9f92110f25"></a>
> 
> <strong><u>실무</u></strong><strong>에서는 거의 </strong><strong><code>rem</code></strong><strong>을 쓴다&#46;</strong>
> 
> - <code>em</code>은 예상치 못한 상속 문제 때문에 복잡해질 수 있음

| <strong>구분</strong> | <strong>설명</strong> |
| --- | --- |
| <code>em</code> | <strong>자기 부모 요소</strong>의 폰트 크기를 기준으로 크기 계산 |
| <code>rem</code> | <strong>html(root)</strong> 폰트 크기를 기준으로 크기 계산 |

</details>
