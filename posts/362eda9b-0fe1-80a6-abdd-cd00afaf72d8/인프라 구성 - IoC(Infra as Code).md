---
order: 11
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 362eda9b-0fe1-80a6-abdd-cd00afaf72d8
title: 인프라 구성 - IoC(Infra as Code)
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
    title: 대규모 시스템 설계
  - id: 356eda9b-0fe1-8010-9561-c7098d310a4f
    title: "The RED: 대용량 서비스를 위한 아키텍처 with Redis (by 강대명)"
  - id: 362eda9b-0fe1-80a6-abdd-cd00afaf72d8
    title: 인프라 구성 - IoC(Infra as Code)
excerpt: 인프라 구성 - IoC(Infra as Code) --- 📖 Ansible, Teraform을 사용한 인프라 구성 - 실습에 사용할 프로젝트 [the_red_infra/terraform/ec2/ap-northeast-2 at main · charsyam/the_red_infra]() terraform bash 경로 이동
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 356eda9b-0fe1-8010-9561-c7098d310a4f
created: 2026-05-16T04:40:46.996Z
updated: 2026-05-16T05:01:00.617Z
legacy_path: Main/대규모 시스템 설계-d6a1706fbaf8/The RED- 대용량 서비스를 위한 아키텍처 with Redis (by 강대명)-c7098d310a4f/인프라 구성 - IoC(Infra as Code)-cd00afaf72d8/index.md
legacy_category: 대규모 시스템 설계
source_url: https://beautiful-college-c84.notion.site/362eda9b0fe180a6abddcd00afaf72d8
---
<a id="362eda9b0fe18051a3ffc6ea516f4127"></a>

## 인프라 구성 &#45; IoC(Infra as Code)

---

> 📖 

<a id="362eda9b0fe18040976ed3e0dc0bffb2"></a>

## Ansible, Teraform을 사용한 인프라 구성

- 실습에 사용할 프로젝트
    [the&#95;red&#95;infra/terraform/ec2/ap&#45;northeast&#45;2 at main · charsyam/the&#95;red&#95;infra]()

<a id="362eda9b0fe180e38ba5d400ac394f72"></a>

### terraform

<a id="362eda9b0fe180d6af90e019028b6e4b"></a>

```bash
# 경로 이동
cd terraform/ec2/ap-northeast-2

terraform init

terraform plan -out "output"

terrafrm apply "output"
```
