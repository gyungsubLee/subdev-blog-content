---
order: 18
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8181-a5f4-d5f05301848e
title: 좌표(x, y) 정렬
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81e5-a912-c23dfb0cbee3
    title: 알고리즘
  - id: 1c3eda9b-0fe1-81dc-9260-fa89456b4fa7
    title: "[인프런] 알고리즘-자바(초급)"
  - id: 1c3eda9b-0fe1-8181-a5f4-d5f05301848e
    title: 좌표(x, y) 정렬
excerpt: 좌표(x, y) 정렬 오름차순 정렬 java class Point implements Comparable{ int x, y; Point(int x, int y){ this.x=x; this.y=y; } @Override public int compareTo(Point o){ if(this.x==o.x) return thi
cover: null
icon: 📃
notionProperties:
  💻 알고리즘-자바(초급): "[페이지](https://beautiful-college-c84.notion.site/1c3eda9b0fe181538de9e76d4c008e2b)"
  "진행 ": 개념
  난이도: 중요
schema_version: 1
parent_id: 1c3eda9b-0fe1-81dc-9260-fa89456b4fa7
created: 2025-03-27T07:47:30.924Z
updated: 2025-03-27T07:47:30.924Z
legacy_path: Main/알고리즘-c23dfb0cbee3/[인프런] 알고리즘-자바(초급)-fa89456b4fa7/좌표(x, y) 정렬-d5f05301848e/index.md
legacy_category: 알고리즘
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18181a5f4d5f05301848e
---
<a id="1c3eda9b0fe1813bbb2ddd818abce857"></a>

# 좌표(x, y) 정렬

<a id="1c3eda9b0fe1814fb60ec0ae181f6442"></a>

## 오름차순 정렬

<a id="1c3eda9b0fe18166bdf3ee70906aa9b1"></a>

```java
class Point implements Comparable<Point>{
    int x, y;
    Point(int x, int y){
        this.x=x;
        this.y=y;
    }

    @Override
    public int compareTo(Point o){
        if(this.x==o.x) return this.y - o.y;
        else return this.x - o.x;
    }
}

Collections.sort([정렬하려는 ArrayList])
```

<a id="1c3eda9b0fe181c8b065d44a47d473ee"></a>

## 내림차순 정렬

<a id="1c3eda9b0fe1810586b0fcc0a847164d"></a>

```java
class Point implements Comparable<Point>{
    int x, y;
    Point(int x, int y){
        this.x=x;
        this.y=y;
    }

    @Override
    public int compareTo(Point o){
        if(this.x==o.x) return o.y-this.y;
        else return o.x-this.x;
    }
}

Collections.sort([정렬하려는 ArrayList])
```
