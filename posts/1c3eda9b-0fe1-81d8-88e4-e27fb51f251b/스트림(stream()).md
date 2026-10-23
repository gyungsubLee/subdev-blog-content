---
order: 51
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81d8-88e4-e27fb51f251b
title: 스트림(stream())
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81e5-a912-c23dfb0cbee3
    title: 알고리즘
  - id: 1c3eda9b-0fe1-81dc-9260-fa89456b4fa7
    title: "[인프런] 알고리즘-자바(초급)"
  - id: 1c3eda9b-0fe1-81d8-88e4-e27fb51f251b
    title: 스트림(stream())
excerpt: "스트림 자바 8 이전 배열 or Collections 인스턴스를 다루는 방법은 for문 or forEach문을 돌면서 요소를 하나씩 꺼내서 처리하는 방법이다. 코드가 간단하면 상관없지만 복잡해질 수록 위 방법은 번거롭고 생산성이 낮다. 해당 방법을 보안하기위해 자바 8에서 추가된 것이 stream 이다. 람다를 활용하여 "
cover: null
icon: null
notionProperties:
  💻 알고리즘-자바(초급): "[페이지](https://beautiful-college-c84.notion.site/1c3eda9b0fe181348a6ddc47e7781265)"
  "진행 ": 정리중
schema_version: 1
parent_id: 1c3eda9b-0fe1-81dc-9260-fa89456b4fa7
created: 2025-03-27T07:47:30.916Z
updated: 2025-03-27T07:47:30.916Z
legacy_path: Main/알고리즘-c23dfb0cbee3/[인프런] 알고리즘-자바(초급)-fa89456b4fa7/스트림(stream())-e27fb51f251b/index.md
legacy_category: 알고리즘
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181d888e4e27fb51f251b
---
<a id="1c3eda9b0fe181f0a153cc489ea8fcef"></a>

# 스트림

<a id="1c3eda9b0fe181ebbde6f3e514e8520e"></a>

<strong>자바 8 이전</strong> <code>배열</code> or<code> Collections 인스턴스</code>를 다루는 방법은 <strong>for문</strong> or <strong>forEach문</strong>을 돌면서 <u>요소를 하나씩 꺼내서 처리</u>하는 방법이다&#46; 

<a id="1c3eda9b0fe181faa544c163e54061ac"></a>

코드가 간단하면 상관없지만 복잡해질 수록 위 방법은 번거롭고 생산성이 낮다&#46; 

<a id="1c3eda9b0fe181c8a0b9fdcb497a4e2c"></a>

 해당 방법을 보안하기위해 <strong>자바 8</strong>에서 추가된 것이 <code>stream</code> 이다&#46; 

<a id="1c3eda9b0fe181c68e49f7785ab27cc2"></a>

 람다를 활용하여 <code>배열</code>과 <code>컬렉션 인스턴스(ArrayList 등</code>)에 여러 개의 함수를 조합하여 원하는 결과를 <strong>필터링</strong>하고 <strong>가공된 결과</strong>를 얻을 수 있다&#46; 

<a id="1c3eda9b0fe181b1b1d3f1c7660f06c8"></a>

또한<strong> </strong><strong>병렬처리(multi&#45;threading)</strong>이 가능하여, 하나의 작업을 병렬 처리(여러개의 쓰레드 사용)하여 많은 요소들을 빠르게 처리할 수 있다&#46; 

<a id="1c3eda9b0fe181bfb65af9fb37f305b6"></a>

## 사용법

> 1&#46; <code>생성</code>&#58; 스트림 인스턴스 생성<br>2&#46;<code>가공</code>&#58; 필터링(filtering), 맵핑(mapping) 등 <br>3&#46;<code>결과</code>&#58;  terminal operations

<a id="1c3eda9b0fe181f9809ce9c9f64c48cf"></a>

## 생성하기 

<a id="1c3eda9b0fe18133bb1fe859e36bacc5"></a>

배열, 컬렉션, 그외 다양한 방법을 사용하여 스트림 만듬

<a id="1c3eda9b0fe181258a2ed967e91ad49c"></a>

### 배열 스트림(Array&#46;stream)

<details>
<summary>ex)</summary>

<a id="1c3eda9b0fe1814299b7f2d2aa9ca88a"></a>

```java
String[] arr = new String("A", "B", "C");

Stream<String> stream = Arrays.stream(arr);

// stream(배열, 시작 인덱스, 끝 인덱스[미포함])
Stream<String> stream2 = Arrays.stream(arr, 1, 3) // ["B", "C"]  
```

</details>

<details>
<summary>배열의 타입이 <code>기본 타입(int, char &#46;&#46;)</code>인 경우 <code>wrapper 클래스(Integer, Charector &#46;&#46;)</code>로 변경해야 한다&#46; </summary>

<details>
<summary>Error (기본 타입&#58; <code>int</code>)</summary>

<a id="1c3eda9b0fe181f6bb78d95887105514"></a>

```java
public static void main(String args[]) {
  int[] arr= {0, 1, 2, 3, 4};
  Stream<int> intStream = Arrays.stream(arr;
}
```

</details>

<details>
<summary>해결 (Wrapper 클래스&#58; <code>Integer</code> ) </summary>

<a id="1c3eda9b0fe181c0accdce71952e0fc7"></a>

```java
public static void main(String args[]) {
  Integer[] arr= {0, 1, 2, 3, 4};
  Stream<Integer> intStream = Arrays.stream(arr;
}
```

</details>

</details>

<details>
<summary>Java의 버전이 1&#46;8 이상인 경우<code> java&#46;util&#46;stream</code> 패키지를 통해 기본 타입의 배열을 스트림으로 변환 가능하다&#46; </summary>

- IntStream&#58; int 타입의 스트림

- DoubleStream&#58; double 타입의 스트림

- LongStream&#58; ㅣong 타입의 스트림

</details>

<a id="1c3eda9b0fe181328bc0e63cc714d34e"></a>

### 컬렉션 스트림

<a id="1c3eda9b0fe181579891c57834a0a30e"></a>

컬렉션 타입(Collectiom, List, Set)은 인터페이스에 추가된 디폴트 메소드 <code>stream</code> 을 사용하여 스트림 생성

<a id="1c3eda9b0fe18175a960ec69e5f4c09a"></a>

```java
public interface Collection<E> extends Iterable<E> {
  default Stream<E> stream() {
    return StreamSupport.stream(spliterator(), false);
  } 
  // ...
}
```

<details>
<summary>생성</summary>

<a id="1c3eda9b0fe1816eb348d836f1a63bf3"></a>

```java
List<String> list = Arrays.asList("a", "b", "c");
Stream<String> stream = list.stream();
Stream<String> parallelStream = list.parallelStream(); // 병렬 처리 스트림
```

</details>

<a id="1c3eda9b0fe181819348c6a753084871"></a>

### Reference)

---

<a id="1c3eda9b0fe1812c9562c0eefb8f7876"></a>

<a href="https://futurecreator.github.io/2018/08/26/java-8-streams/">https&#58;//futurecreator&#46;github&#46;io/2018/08/26/java&#45;8&#45;streams/</a>
