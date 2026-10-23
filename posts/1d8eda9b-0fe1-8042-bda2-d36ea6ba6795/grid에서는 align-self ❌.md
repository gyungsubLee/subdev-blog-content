---
order: 58
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1d8eda9b-0fe1-8042-bda2-d36ea6ba6795
title: grid에서는 align-self ❌
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1d8eda9b-0fe1-8042-bda2-d36ea6ba6795
    title: grid에서는 align-self ❌
excerpt: "문제 css .con4 .listBox .cardBox h3 { font-size: 300px; font-weight: bold; line-height: 0.9; align-self: flex-end;} .con4 .listBox .cardBox .text { align-self: flex-end; line-height:"
cover: null
icon: null
notionProperties:
  Tags: 오류
  상태: 진행 중
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-17T16:17:24.932Z
updated: 2025-04-17T16:22:03.562Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/grid에서는 align-self ❌-d36ea6ba6795/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1d8eda9b0fe18042bda2d36ea6ba6795
---
<a id="1d8eda9b0fe18042acebdbe712efaee7"></a>

### 문제 

<a id="1d8eda9b0fe18064b9dddd0b4906d8e6"></a>

```css
.con4 .listBox .cardBox h3 { font-size: 300px; font-weight: bold; line-height: 0.9; align-self: flex-end;}
.con4 .listBox .cardBox .text { align-self: flex-end; line-height: 1.4; }
```

> &#46;cardBox가 <code>display&#58; grid;</code>인 상태에서 <br>&#46;text는 “그리드 아이템”인데, <code>align&#45;self</code>는 grid에서도 정상 작동

<a id="1d8eda9b0fe180eb95cfd1476dcc5d9a"></a>

## <strong>🔥 조금 더 기술적으로 말하면</strong>

<a id="1d8eda9b0fe1801b916afafc36d44cd3"></a>

grid 컨텍스트 안에서는&#58;

- &#42;각 grid item(자식 요소)&#42;&#42;은 <strong>자기 영역 안에서</strong> 정렬할 수 있어&#46;

- 이때 align&#45;self를 쓰는데,
    - grid에서는 start, center, end, stretch 키워드를 써야 해&#46;

    - 그런데 <strong>브라우저가 flex 문법인 flex&#45;end를 end로 자동 매핑해서 이해</strong>하는 경우가 있어&#46;

> 즉, &#46;text에 align&#45;self&#58; flex&#45;end를 줬지만

> 브라우저가 “아 얘 grid인데? flex&#45;end = end로 이해할게”

> ➔
> 
> <a id="1d8eda9b0fe180b78a4af1321c9cf66a"></a>
> 
> <strong>자동으로 end처럼 적용</strong>

<a id="1d8eda9b0fe18070b529d75da8908969"></a>

✅ 그래서 정상 작동한 거야&#46;

|  |  |
| --- | --- |
| <strong>상황</strong> | <strong>결과</strong> |
| 부모가 grid인데 align&#45;self&#58; flex&#45;end를 썼다 | 브라우저가 “end”로 매핑해서 처리함 (자동) |
| &#46;text는 자체적으로 크기도 충분하고 grid cell 안에 잘 들어가 있어서 문제없이 하단으로 내려감 | O |
| &#46;h3는 폰트 크기가 300px로 너무 커서 기본 flow에 눌려 있었던 것 | X |

<a id="1d8eda9b0fe18059b44dd9819710f875"></a>

### <strong>&#46;h3가 align&#45;self가 잘 안 먹었던 더 깊은 이유</strong>

|  |  |
| --- | --- |
| <strong>요소</strong> | <strong>왜 align&#45;self가 먹었는지</strong> |
| &#46;text | 브라우저가 flex&#45;end를 end로 매핑해서 정상 작동 |
| &#46;h3 | 폰트가 너무 커서 grid 내에서 셀을 꽉 채워버려 align&#45;self가 기대처럼 적용 안 됨 |

<a id="1d8eda9b0fe1801982caf2cbe3f8cadf"></a>

&#46;h3는 <strong>폰트 사이즈가 엄청 커(300px)</strong>&#46;

<a id="1d8eda9b0fe180a4bcb1dbdfb3d4bbe9"></a>

grid 배치 안에서 그 커다란 사이즈로 인해

- 셀 높이를 이미 꽉 채우거나

- grid auto&#45;flow 규칙에 의해 <strong>강제로 윗줄에</strong> 들어가 있었던 거야&#46;

<a id="1d8eda9b0fe180ccbbb4dbe4934d028a"></a>

그러다 보니

- align&#45;self를 줘도,

- 적용할 수 있는 “남는 공간”이 없었거나,

- 기대하는 위치로 내려가지 않았던 거야&#46;

- &#42;(line&#45;height&#58; 0&#46;9)&#42;&#42;까지 적용돼서 더 빡빡하게 말려 있었고&#46;

<a id="1d8eda9b0fe180e5bcfad94ee2f39868"></a>

### 해결

<details>
<summary>Grid 권장 CSS</summary>

<a id="1d8eda9b0fe18032982ff362aaff1092"></a>

```css
.con4 .listBox .cardBox {
  display: grid;
  grid-template-columns: 60% auto; /* 2컬럼: 왼쪽 60%, 오른쪽 auto */
  grid-template-rows: auto 1fr; /* 2줄: 첫 줄 auto(h2), 두 번째는 1fr로 채움 */
  gap: 20px; /* 컬럼, 로우 간 여백 */
  padding: 50px 80px;
  background-color: #d1dbfd;
  color: #000;
  border-radius: 10px;
  margin-bottom: 20px;
}

/* 1번 줄 : h2 (제목) */
.con4 .listBox .cardBox h2 {
  font-size: 40px;
  font-weight: normal;
  letter-spacing: -2px;
  padding-bottom: 20px;
  border-bottom: solid 1px #ddd;
  grid-column: 1 / 3; /* 1~2열 전체 차지 */
  grid-row: 1 / 2; /* 첫 번째 줄 */
  margin-bottom: 50px;
}

/* 2번 줄, 왼쪽 컬럼 : h3 (큰 숫자) */
.con4 .listBox .cardBox h3 {
  font-size: 300px;
  font-weight: bold;
  line-height: 0.9;
  align-self: end; /* grid에서는 flex-end 대신 end */
  grid-column: 1 / 2; /* 1번째 컬럼 */
  grid-row: 2 / 3; /* 두 번째 줄 */
}

/* 2번 줄, 오른쪽 컬럼 : text (본문) */
.con4 .listBox .cardBox .text {
  align-self: end;
  line-height: 1.4;
  grid-column: 2 / 3; /* 2번째 컬럼 */
  grid-row: 2 / 3; /* 두 번째 줄 */
}

/* .text 안의 제목(h4) */
.con4 .listBox .cardBox .text h4 {
  margin-bottom: 20px;
  line-height: 1.2;
}

/* .text 안의 본문(p) */
.con4 .listBox .cardBox .text p {
  opacity: 0.5;
}
```

</details>

<details>
<summary>tailwindcss</summary>

<a id="1d8eda9b0fe180c2b353cd201ebc1d6a"></a>

```css
<div class="grid grid-cols-[60%_auto] grid-rows-[auto_1fr] gap-5 p-10 bg-[#d1dbfd] text-black rounded-2xl mb-5">
  <h2 class="text-[40px] font-normal tracking-[-2px] pb-5 border-b border-gray-300 col-span-2 mb-12">CREATION</h2>
  <h3 class="text-[300px] font-bold leading-[0.9] self-end col-start-1 row-start-2">1</h3>
  <div class="self-end leading-[1.4] col-start-2 row-start-2">
    <h4 class="mb-5 leading-[1.2]">You have an idea?</h4>
    <p class="opacity-50">본문 텍스트</p>
  </div>
</div>
```

</details>
