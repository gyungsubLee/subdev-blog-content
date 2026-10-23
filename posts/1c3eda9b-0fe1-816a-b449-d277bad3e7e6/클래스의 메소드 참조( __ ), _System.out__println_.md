---
order: 2
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-816a-b449-d277bad3e7e6
title: '클래스의 메소드 참조( :: ), "System.out::println"'
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-814c-8dc5-d29a6b4043e6
    title: Java [ 문법, 자료구조 …] (중단)
  - id: 1c3eda9b-0fe1-816a-b449-d277bad3e7e6
    title: '클래스의 메소드 참조( :: ), "System.out::println"'
excerpt: 클래스 메소드 참조 예제) [ for문 축약 ] java import java.util.ArrayList; import java.util.List; public class MethodRef { public static void main(String[] args) { List names = new ArrayList(); n
cover: null
icon: 🤔
notionProperties:
  URL: "[https://myhappyman.tistory.com/65](https://myhappyman.tistory.com/65)"
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-814c-8dc5-d29a6b4043e6
created: 2025-03-27T07:53:11.122Z
updated: 2025-03-27T07:53:11.122Z
legacy_path: Main/Spring ( Java )-cd1f71740107/Java [ 문법, 자료구조 …] (중단)-d29a6b4043e6/클래스의 메소드 참조( -- ), -System.out--println--d277bad3e7e6/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1816ab449d277bad3e7e6
---
<a id="1c3eda9b0fe181e38cf0cebd8f742ac2"></a>

# 클래스 메소드 참조 

<a id="1c3eda9b0fe181fa9892efd5f327f3ce"></a>

### 예제) &#91; for문 축약 &#93;

<a id="1c3eda9b0fe18123bb3de44bae719b2c"></a>

```java
import java.util.ArrayList;
import java.util.List;

public class MethodRef {
    public static void main(String[] args) {
        List<String> names = new ArrayList<String>();
        names.add("Matilda");
        names.add("Leon");
        names.add("Naples");
        names.add("Harry Potter");
        names.add("Iron Man");
				
					.   .   .

    }
}
```

<a id="1c3eda9b0fe18102a61de2337a283def"></a>

### <strong>단순 반복문(for 문)  출력</strong>

<a id="1c3eda9b0fe181f29213f2bceaff335f"></a>

```java
for(int i=0; i<names.size(); i++) {
    System.out.println(names.get(i));
}
```

<a id="1c3eda9b0fe181f49d3df9b2092306ab"></a>

### <strong>forEach</strong>문

<a id="1c3eda9b0fe181778f3bf2ad95042154"></a>

```java
names.forEach(d->
	System.out.println(d)
);
```

<a id="1c3eda9b0fe1818b99daf2e01551f7cf"></a>

### <strong>메소드 참조(&#58;&#58;)</strong>

<a id="1c3eda9b0fe1812cabddc7c56d8b62ea"></a>

```java
names.forEach(System.out::println);
```

<a id="1c3eda9b0fe181e1b0c3d37fb8efd0c4"></a>

### 예제2 )  &#91; 클래스 &#45; 메서드  &#93; 

<a id="1c3eda9b0fe181d3ac4ed33b4fd70c0d"></a>

```java
import java.util.ArrayList;
import java.util.List;

public class RamdaT {
	
	private void someFunction(String str) {
		System.out.println(str);
	}

	public static void main(String[] args) {
		List<String> list = new ArrayList<String>();
		list.add("Apple");
		list.add("Banana");
		list.add("Cherry");
		
		list.forEach(System.out::println);
		
		System.out.println(); * 3
		
		list.forEach((new RamdaT())::someFunction);
	}
}



================ 출력값 ===================
Apple
Banana
Cherry

Apple
Banana
Cherry
```
