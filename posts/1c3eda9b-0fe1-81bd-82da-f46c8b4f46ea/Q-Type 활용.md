---
order: 14
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81bd-82da-f46c8b4f46ea
title: Q-Type 활용
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
    title: "[ Inflearn ] Querydsl"
  - id: 1c3eda9b-0fe1-81bd-82da-f46c8b4f46ea
    title: Q-Type 활용
excerpt: 기본 Q-Type 활용 --- 📖 QueryDSL에서는 모듈 자체에서 Entity를 변환한 Q클래스를 사용하여 쿼리를 생성한다. Q클래스 인스턴스를 사용하는 2가지 방법 java QMember qMember = new QMember("m"); //별칭 직접 지정 QMember qMember = QMember.member
cover: null
icon: null
notionProperties:
  Point: Q 클래스 사용 방법
  ZOVW: Yes
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
created: 2025-03-27T07:53:11.118Z
updated: 2025-03-27T07:53:11.118Z
legacy_path: Main/Spring ( Java )-cd1f71740107/[ Inflearn ] Querydsl-f8e742a95d76/Q-Type 활용-f46c8b4f46ea/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181bd82daf46c8b4f46ea
---
<a id="1c3eda9b0fe181579901c66b6a69327f"></a>

## <strong>기본 </strong>Q&#45;Type <strong>활용</strong>

---

> 📖 
> 
> <a id="1c3eda9b0fe181828f29cc2a1f86eb68"></a>
> 
> QueryDSL에서는 모듈 자체에서 Entity를 변환한 Q클래스를 사용하여 쿼리를 생성한다&#46; 

<details>
<summary><strong>Q클래스 인스턴스를 사용하는 2가지 방법</strong></summary>

<a id="1c3eda9b0fe181289b2af31496469b29"></a>

```java
QMember qMember = new QMember("m"); //별칭 직접 지정 
QMember qMember = QMember.member; //기본 인스턴스 사용
```

</details>

<details>
<summary><strong>기본 인스턴스를 static import와 함께 사용</strong></summary>

<a id="1c3eda9b0fe181369ef5c7d429c78d4f"></a>

```java
import static study.querydsl.entity.QMember.*;

@Test
public void startQuerydsl3() {

		QMember member = QMember.member; 

		//member1 조회
		Member findMember = queryFactory
		             .select(member)
		             .from(member)
		             .where(member.username.eq("member1"))
		             .fetchOne();
		             
    assertThat(findMember.getUsername()).isEqualTo("member1");
}

```

</details>

> ☝🏻 
> 
> <a id="1c3eda9b0fe181d58e99e0803224324c"></a>
> 
> 참고)  같은 테이블을 조인해야 하는 경우가 아니면 <u>기본 인스턴스(Q클래스) 사용을 권장</u>
> 
> - ex) <code>QMember qMember = QMember&#46;member;</code>
