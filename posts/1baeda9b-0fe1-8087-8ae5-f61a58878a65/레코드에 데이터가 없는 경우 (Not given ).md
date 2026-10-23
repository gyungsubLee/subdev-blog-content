---
order: 5
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1baeda9b-0fe1-8087-8ae5-f61a58878a65
title: 레코드에 데이터가 없는 경우 (Not given )
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 108eda9b-0fe1-8075-8c0d-d40a042cccae
    title: 엑셀보다 쉽고 빠른 SQL
  - id: 1baeda9b-0fe1-8087-8ae5-f61a58878a65
    title: 레코드에 데이터가 없는 경우 (Not given )
excerpt: 레코드에 데이터가 없는 경우 (Not given ) 1) 값이 없는 경우 필터링(제외) 1-1. 암시적 연산 처리 - if( <>, truthy, falsy) 🧐 rate 평균 값인 average_of_rating, average_of_rating2이 동일하지 않다. 평균 값을 구하기 위한 연산 처리 시, ‘Not gi
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 108eda9b-0fe1-8075-8c0d-d40a042cccae
created: 2025-03-18T18:02:44.965Z
updated: 2025-04-22T15:07:23.781Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/엑셀보다 쉽고 빠른 SQL-d40a042cccae/레코드에 데이터가 없는 경우 (Not given )-f61a58878a65/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/1baeda9b0fe180878ae5f61a58878a65
---
<a id="10feda9b0fe180e2addafa187fab8ff4"></a>

### 레코드에 데이터가 없는 경우 (<code>Not given</code> )

<a id="10feda9b0fe180c0bb16c0a2d96cee42"></a>

1) 값이 없는 경우 필터링(제외)

<details>
<summary>1&#45;1&#46;  암시적 연산 처리 &#45; <code>if( &#60;&#62;, truthy, falsy)</code></summary>

<details>
<summary>🧐 rate 평균 값인 <code>average&#95;of&#95;rating</code>, <code>average&#95;of&#95;rating2</code>이 동일하지 않다&#46; </summary>

![](1bb3003334c26fd4.webp)

<details>
<summary>평균 값을 구하기 위한 연산 처리 시, ‘Not give’은 <code>0</code>의 값으로 인식되어 처리된다&#46; </summary>

- Mysql 에서는 사용할 수 없는 값일 때, 해당 값을 연산에서 제외하다&#46; → 0으로 간주
    ![](b110e61f687ff47c.webp)

</details>

<details>
<summary>MySQL <code>null</code> 값을 제외하여 평균값을 구한다&#46; <br>따라서 <code>average&#95;of&#95;rating2</code> 의 평균 값 연산 처리 시 <code>null</code> 데이터는 제외하여 연산을 한다&#46; </summary>

- <strong>‘Not given’</strong> → <code>null</code> 
    <a id="110eda9b0fe180f5bc12f22ba4749b33"></a>

    ```sql
    if(rating<>'Not given', rating, null)
    ```

![](e0470779ab47b36f.webp)

</details>

</details>

- 🧐 <code>&#60;&#62;</code> = <code>≠</code>

<a id="110eda9b0fe1803a8512d3e8ccfd5c8a"></a>

<strong>SQL Query</strong>

<a id="10feda9b0fe180dc9d9bf21101791325"></a>

```sql
select restaurant_name,
       avg(rating) average_of_rating,
       avg(if(rating<>'Not given', rating, null)) average_of_rating2
from food_orders
group by 1
```

![](b7040d06e28299ba.webp)

</details>

<details>
<summary>1&#45;2&#46; 명확한 연산 처리 &#45;  <u><code>is not</code></u><code> null</code></summary>

<a id="10feda9b0fe180d49afbe118b455dfa6"></a>

```sql
select a.order_id,
       a.customer_id,
       a.restaurant_name,
       a.price,
       b.name,
       b.age,
       b.gender
from food_orders a left join customers b on a.customer_id=b.customer_id
where b.customer_id is not null 
```

- null 제거를 하지 않았을 때
    ![](fc7f7828f7f6ec17.webp)

- null 제거를 했을 때 (join 시에는 inner join 과 동일함) 
    ![](4e4362b88ca95d9f.webp)

</details>

<details>
<summary>1&#45;3&#46; <code>inner join</code> </summary>

> <strong>lef join</strong> &#43;<strong> is not </strong><strong><code>null</code></strong>  = inner join 

</details>

<a id="10feda9b0fe18045a224e2d4129c4ee4"></a>

2) 값이 없는 경우 ‘특정 값’으로 대체&#58; <code>coalesce</code>

<a id="10feda9b0fe180c89617e7f34ba0e945"></a>

```sql
coalesce(age, 대체값)  // age = null
```

<a id="10feda9b0fe1809fad96ca8139511fc2"></a>

```sql
select a.order_id,
       a.customer_id,
       a.restaurant_name,
       a.price,
       b.name,
       b.age,
       coalesce(b.age, 20) "null 제거",
       b.gender
from food_orders a left join customers b on a.customer_id=b.customer_id
where b.age is null
```

![](ba6415de2b889ef0.webp)
