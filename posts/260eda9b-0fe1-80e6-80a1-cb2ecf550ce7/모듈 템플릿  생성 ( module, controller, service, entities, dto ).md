---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 260eda9b-0fe1-80e6-80a1-cb2ecf550ce7
title: 모듈 템플릿  생성 ( module, controller, service, entities, dto )
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 260eda9b-0fe1-801b-836b-c2e229a88ff9
    title: 한 번에 끝내는 NestJS 패키지 - Part 1. 기초
  - id: 266eda9b-0fe1-807e-9171-cbbbc7a95935
    title: Nest CLI
  - id: 260eda9b-0fe1-80e6-80a1-cb2ecf550ce7
    title: 모듈 템플릿  생성 ( module, controller, service, entities, dto )
excerpt: 목차 - 모듈 모듈 --- ❗ Class를 DI(Dependency Injection) 하기 위해서는 각 모듈 계층해서 해당하는 클래스를 provider로 등록해야 한다. bash 모듈 템플릿 생성 - module, controller, service, entities, dto nest g resource 1. 도메인 명
cover: fb3b1ee7da4a15e0.webp
icon: 9bed2eae1e079b4b.avif
notionProperties: {}
schema_version: 1
parent_id: 266eda9b-0fe1-807e-9171-cbbbc7a95935
created: 2025-08-31T08:05:42.318Z
updated: 2025-10-31T12:20:21.402Z
legacy_path: Main/Nest.js-c3a886768c4d/한 번에 끝내는 NestJS 패키지 - Part 1. 기초-c2e229a88ff9/Nest CLI-cbbbc7a95935/모듈 템플릿  생성 ( module, controller, service, ent-cb2ecf550ce7/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/260eda9b0fe180e680a1cb2ecf550ce7
---
> 
> 
> <a id="260eda9b0fe18142ab93c7b1f4992917"></a>
> 
> <strong>목차</strong>
> 
> - [모듈](#260eda9b0fe181d1b39ac2d77571d600)

<a id="260eda9b0fe181d1b39ac2d77571d600"></a>

## 모듈

---

> ❗ 
> 
> <a id="266eda9b0fe18029afb7f7a9f696b0fb"></a>
> 
> Class를  DI(Dependency Injection) 하기 위해서는 각 모듈 계층해서 해당하는 클래스를 provider로 등록해야 한다&#46; 

<a id="260eda9b0fe1805a80cfdece110ad7e5"></a>

```bash
# 모듈 템플릿 생성 - module, controller, service, entities, dto
nest g resource
	# 1. 도메인 명칭 
	# 2. 컨텍스트 유형 ( REST API, GraphQL, Microservice, WebSocket )
	# 3. CRUD 엔드포인트 자동 생성
```

> ✏️ 
> 
> <a id="260eda9b0fe1803b9d63fe22e54dab55"></a>
> 
> 외부 모듈의 provider(빈)를 DI 해서 사용하고 싶다면?
> 
> 1. 해당 provider가 속한 모듈에서 export 처리 ( module 1 )
> 
> 1. 사용하려는 모듈(module 2) 계층해서  해당 모듈 ( module 1)을 import 

- 위 과정을 거치지 않으면 정상적으로 DI가 되지 않는다&#46;
