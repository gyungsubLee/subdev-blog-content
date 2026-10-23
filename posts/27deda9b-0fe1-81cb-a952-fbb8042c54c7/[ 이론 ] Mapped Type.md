---
order: 1
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 27deda9b-0fe1-81cb-a952-fbb8042c54c7
title: "[ 이론 ] Mapped Type"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 260eda9b-0fe1-801b-836b-c2e229a88ff9
    title: 한 번에 끝내는 NestJS 패키지 - Part 1. 기초
  - id: 27deda9b-0fe1-80a6-a020-ffa3bb1ef371
    title: Mapped Types
  - id: 27deda9b-0fe1-81cb-a952-fbb8042c54c7
    title: "[ 이론 ] Mapped Type"
excerpt: "목차 - Mapped Type - 종류 - 1. Partial - 2. Pick - 3. Omit - 4. Intersection - 5. Composition Mapped Type --- 📖 NestJS의 Mapped Type은 기존 DTO(Class)에서 특정 속성만 변경하거나 선택적으로 만들어 새로운 타입을 쉽게 "
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 27deda9b-0fe1-80a6-a020-ffa3bb1ef371
created: 2025-09-29T11:09:23.264Z
updated: 2025-10-03T22:52:11.201Z
legacy_path: Main/Nest.js-c3a886768c4d/한 번에 끝내는 NestJS 패키지 - Part 1. 기초-c2e229a88ff9/Mapped Types-ffa3bb1ef371/[ 이론 ] Mapped Type-fbb8042c54c7/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/27deda9b0fe181cba952fbb8042c54c7
---
> 
> 
> <a id="27deda9b0fe18176a4d0dee6dbf77881"></a>
> 
> <strong>목차</strong>
> 
> - [Mapped Type](#27deda9b0fe1816bbe31e269a61a5ccf)
> - [ 종류](#27deda9b0fe181ab8d65d089aeff0d70)
> - [1. Partial](#27deda9b0fe1818f921bf53bbb58ac36)
> - [2. Pick](#27deda9b0fe180fcb6b1ee66e4a54529)
> - [3. Omit](#27deda9b0fe180688e8cdbff3ae375ff)
> - [4. Intersection](#27deda9b0fe18079a4f4c4137aef235f)
> - [5. Composition](#27deda9b0fe180a687a8ce1355c4e683)

<a id="27deda9b0fe1816bbe31e269a61a5ccf"></a>

## Mapped Type

---

> 📖 
> 
> <a id="27deda9b0fe18133a881de866feed02d"></a>
> 
> NestJS의 <code>Mapped Type</code>은 기존 <strong><u>DTO(Class)</u></strong>에서 <strong><u>특정 속성만 변경</u></strong>하거나 <strong><u>선택적으로 만</u></strong>들어 새로운 타입을 쉽게 생성해주는 유틸리티 기능이다&#46;
> 
> <a id="27deda9b0fe1809eaa57dda805de86ab"></a>
> 
> 이를 활용하면 CRUD 기능 구현 시 <strong><u>불필요한 반복 코드를 줄</u></strong>이고, <strong><u>효율적으로 타입을 변형</u></strong>할 수 있다&#46;

> ❗ 
> 
> <a id="27deda9b0fe181ee8724dae2c966730e"></a>
> 
> 필수는 아니다&#46; 서로의 의존성이 많이 생기는 경우, 나중에 복잡도가 증가할 수 있다&#46;
> 
> <a id="27deda9b0fe18066a349fe374ea9acaf"></a>
> 
> 따라서 Create, Update 같이 종속적인 경우 사용하는 것이 좋다&#46; 

<a id="27deda9b0fe181ab8d65d089aeff0d70"></a>

###  종류

> ✏️ 
> 
> - <code>Partial</code>&#58; 
>     - 모든 속성을 옵셔널(optional)로 변경
> 
>     - 주로 Update DTO를 만들 때 많이 사용
> 
> - <code>Pick</code>&#58;
>     - 지정한 속성만 골라 새로운 타입 생성 ( Omit 반대 )
> 
> - <code>Omit</code>&#58;
>     -  특정 속성만 제거하여 새로운 타입 생성
> 
> - <code>Intersection</code>&#58;
>     -  여러 DTO를 합쳐 하나의 타입으로 생성
> 
>     - 복수 엔티티의 정보를 함께 사용할 경우 적합
> 
> - <code>Composition</code>&#58;
>     - Mapped Types를 다양하게 조합해서 중첩 적용 가능

<a id="27deda9b0fe1818f921bf53bbb58ac36"></a>

### 1&#46; <code>Partial</code>

![](157bfbcbcc2fd618.webp)

- PartialType() 메서드 인자로 <code>CreateUserDto</code> 클래스를 넘겨 상속하면 <br><code>CreateUserDto</code> 내 모든 프로퍼티가 Optional로 <code>UpdateUserDto</code> 클래스 내에 생성된다&#46;

<a id="27deda9b0fe180fcb6b1ee66e4a54529"></a>

### 2&#46; <code>Pick</code>

![](2fdf2f0a05838fec.webp)

- <code>PickType()</code> 메서드 내 해당 클래스의 <strong><u>프로퍼티를 골라 상속</u></strong> 처리

<a id="27deda9b0fe180688e8cdbff3ae375ff"></a>

### 3&#46; <code>Omit</code>

![](091c5c45f774925a.webp)

- <code>OmitType()</code> 메서드 인자로 해당 클래스의 <strong><u>제외하려는 프로퍼티를 넘겨 상속</u></strong>처리

<a id="27deda9b0fe18079a4f4c4137aef235f"></a>

### 4&#46; <code>Intersection</code>

![](be261908aaed97c8.webp)

- <code>IntersectionType()</code>  메서드 인자로 해당되는 클래스들을 넘겨 상속 처리

<a id="27deda9b0fe180a687a8ce1355c4e683"></a>

### 5&#46; <code>Composition</code>

![](81ea0d03f42e5033.webp)

- 위와 같이 중첩해서 적용 가능하다&#46; ( 구성 )
