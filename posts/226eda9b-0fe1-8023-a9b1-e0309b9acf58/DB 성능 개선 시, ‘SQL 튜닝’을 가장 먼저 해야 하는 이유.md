---
order: 11
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 226eda9b-0fe1-8023-a9b1-e0309b9acf58
title: DB 성능 개선 시, ‘SQL 튜닝’을 가장 먼저 해야 하는 이유
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
    title: DBMS
  - id: 226eda9b-0fe1-80be-80bb-ca65a5c45f49
    title: 비전공자도 이해할 수 있는 MySQL 성능 최적화 입문/실전 (SQL 튜닝편)
  - id: 226eda9b-0fe1-8023-a9b1-e0309b9acf58
    title: DB 성능 개선 시, ‘SQL 튜닝’을 가장 먼저 해야 하는 이유
excerpt: "목차 - 1. DB 성능을 개선하는 방법 - 🧐 많은 개선 방법 중 왜 ‘SQL 튜닝’을 먼저 고려해야 하는가? 1. DB 성능을 개선하는 방법 --- 📖 DB에 부하가 걸렸을 때 성능을 개선하는 방법은 다양하다 - SQL 튜닝 - 캐싱 서버 활용 ( Redis 등 ) - 레플리케이션 ( Master/Slave 구조 "
cover: fb3b1ee7da4a15e0.webp
icon: 9bed2eae1e079b4b.avif
notionProperties: {}
schema_version: 1
parent_id: 226eda9b-0fe1-80be-80bb-ca65a5c45f49
created: 2025-07-04T14:16:02.912Z
updated: 2025-07-04T14:42:07.763Z
legacy_path: Main/DBMS-e8c2debc9fa0/비전공자도 이해할 수 있는 MySQL 성능 최적화 입문-실전 (SQL 튜닝편)-ca65a5c45f49/DB 성능 개선 시, ‘SQL 튜닝’을 가장 먼저 해야 하는 이유-e0309b9acf58/index.md
legacy_category: DBMS
source_url: https://beautiful-college-c84.notion.site/226eda9b0fe18023a9b1e0309b9acf58
---
> 
> 
> <a id="226eda9b0fe181c7aa6bd4c08c7186ea"></a>
> 
> <strong>목차</strong>
> 
> - [1.  DB 성능을 개선하는 방법](#226eda9b0fe1818ca03ae761db5ad8da)
> - [🧐 많은 개선 방법 중 왜 ‘SQL 튜닝’을 먼저 고려해야 하는가?](#226eda9b0fe180d29f4de82190328ea3)

<a id="226eda9b0fe1818ca03ae761db5ad8da"></a>

## 1&#46;  DB 성능을 개선하는 방법

---

> 📖 
> 
> <a id="226eda9b0fe181bebe48f9a9c80d287b"></a>
> 
> DB에 부하가 걸렸을 때 성능을 개선하는 방법은 다양하다
> 
> - <strong>SQL 튜닝</strong>
> 
> - 캐싱 서버 활용 ( Redis 등 )
> 
> - 레플리케이션 ( Master/Slave 구조 )
> 
> - 샤딩
> 
> - 스케일업 ( CPU, Memory, SSD 등 하드웨어 업그레이드 )

<a id="226eda9b0fe180d29f4de82190328ea3"></a>

### 🧐 많은 개선 방법 중 왜 ‘SQL 튜닝’을 먼저 고려해야 하는가?

- SQL 튜닝을 제외한<strong><u> 나머지 방법은 추가적인 시스템을 구축</u></strong>해야 한다&#46;<br>따라서 <u>금전적, 시간적 비용이 추가적으로 발생</u>한다&#46; <br>또한 조금 더 복잡해진 시스템 구조로 인해 <strong><u>관리 비용이 늘</u></strong>어난다&#46; <br>그에 비해 SQL 튜닝은 기존의 시스템의 변경없이 성능 개선을 할 수 있다&#46;

- 근본적인 문제를 해결하는 방법이 SQL 튜닝일 가능성이높다&#46; <br><strong>SQL 자체가 비효율적으로 작성 됐다면 아무리 시스템적으로 성능을 개선한다고 하더라도 한계가 있다&#46;</strong><br>하지만 SQL 튜닝을 통해 기본적으로 성능을 향상 시킨다면, 시스템적인 성능 개선이 필요 없거나 훨씬 간단한 방법으로 큰 성능 개선 효과를 얻을 수 있다&#46;

<a id="226eda9b0fe180388deaea6205cdb9a3"></a>

간단히 정리하자면 <strong><u>DB 성능 개선 방법 중 </u></strong><strong><u>가장 가성비가 좋은 방법</u></strong><strong>이 </strong><strong><code>SQL 튜닝</code></strong>이기 때문에 가정 먼저 고려하는 것이 효율적이다&#46;
