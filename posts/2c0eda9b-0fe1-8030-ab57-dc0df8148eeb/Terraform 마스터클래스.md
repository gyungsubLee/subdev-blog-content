---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 2c0eda9b-0fe1-8030-ab57-dc0df8148eeb
title: Terraform 마스터클래스
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817b-9c95-d96fd53640c4
    title: CI/CD
  - id: 2c0eda9b-0fe1-8030-ab57-dc0df8148eeb
    title: Terraform 마스터클래스
excerpt: "[FastCampus] Terraform Masterclass : 대규모 인프라를 위한 GitOps 기반 실전 Terraform 활용법 - 기간: 26.06.04(수) ~ 25.06.() - 강의: Terraform Masterclass :대규모 인프라를 위한 GitOps 기반 실전 Terraform 활용법 Referen"
cover: baf64395bf897a27.webp
icon: d482ea1907fc0cd4.webp
notionProperties: {}
schema_version: 1
parent_id: 1c3eda9b-0fe1-817b-9c95-d96fd53640c4
created: 2025-12-05T04:39:49.359Z
updated: 2026-06-22T08:25:06.822Z
legacy_path: Main/CI-CD-d96fd53640c4/Terraform 마스터클래스-dc0df8148eeb/index.md
legacy_category: CI/CD
source_url: https://beautiful-college-c84.notion.site/2c0eda9b0fe18030ab57dc0df8148eeb
---
> 
> 
> <a id="2c0eda9b0fe180f08b1ff0c8f0525926"></a>
> 
> <strong>&#91;FastCampus&#93; Terraform Masterclass &#58; 대규모 인프라를 위한 GitOps 기반 실전 Terraform 활용법</strong>
> 
> - 기간&#58;<strong> 26&#46;06&#46;04(수) &#126; 25&#46;06&#46;()</strong>
> 
> - 강의&#58; <strong><a href="https://fastcampus.co.kr/dev_online_terraform">Terraform Masterclass &#58;대규모 인프라를 위한 GitOps 기반 실전 Terraform 활용법</a></strong>
> 
> <details>
> <summary>Referenec&#58; </summary>
> 
> - ‣
> 
> - ‣
> 
> - ‣
> 
> - ‣
> 
> </details>

> 
> 
> <a id="2c0eda9b0fe18020a649cf9d8c35f698"></a>
> 
> <strong>목차</strong>
> 
> - [ 1. Terraform 시작](#2c0eda9b0fe18079b7e4fd0c7b168c97)
> - [Terraform(HCL) 기본 문법](#377eda9b0fe1808aa05ac9f3f578a8d9)
> - [ 2. AWS 인프라 구성](#2c0eda9b0fe18087b8f5dd79df8f7ff2)
> - [ 3. Github 관리](#2c0eda9b0fe1809bbb8ac3ab74b6df96)
> - [ 4.  Jenkins 구축](#2c0eda9b0fe180789843fc7847beed0d)
> - [ 5. AWS ECS 구성](#2c0eda9b0fe180e3bdadec5c11c31aa6)
> - [ 6. AWS EC2 구성](#2c0eda9b0fe1803ea505dde1f9e69fa8)
> - [ 7. AWS EKS 구성](#2c0eda9b0fe18051b146d66615d16407)
> - [ 8. Terraform, Observability](#2c0eda9b0fe180a0af33f7f277682156)

<details>
<summary>Template</summary>

> 

> ✏️ 

> 📖 

> 
> 
> <a id="2c0eda9b0fe1819f8fbcd15cf4b22910"></a>
> 
> <strong>목차</strong>
> 
> - [ 1. Terraform 시작](#2c0eda9b0fe18079b7e4fd0c7b168c97)
> - [Terraform(HCL) 기본 문법](#377eda9b0fe1808aa05ac9f3f578a8d9)
> - [ 2. AWS 인프라 구성](#2c0eda9b0fe18087b8f5dd79df8f7ff2)
> - [ 3. Github 관리](#2c0eda9b0fe1809bbb8ac3ab74b6df96)
> - [ 4.  Jenkins 구축](#2c0eda9b0fe180789843fc7847beed0d)
> - [ 5. AWS ECS 구성](#2c0eda9b0fe180e3bdadec5c11c31aa6)
> - [ 6. AWS EC2 구성](#2c0eda9b0fe1803ea505dde1f9e69fa8)
> - [ 7. AWS EKS 구성](#2c0eda9b0fe18051b146d66615d16407)
> - [ 8. Terraform, Observability](#2c0eda9b0fe180a0af33f7f277682156)

[제목 없음](#/post/2c0eda9b-0fe1-8119-8685-db726a3dc337)

[제목 없음](#/post/2c0eda9b-0fe1-81a1-b1f0-e25a8019b629)

</details>

<a id="2c0eda9b0fe18079b7e4fd0c7b168c97"></a>

###  1&#46; Terraform 시작

[DevOps, IaC](#/post/2c0eda9b-0fe1-8070-9776-c91961711f86)

[Terraform, TACOS](#/post/2c0eda9b-0fe1-800c-abe0-f9cd2d191ac5)

[Terraform CLI](#/post/2c1eda9b-0fe1-800d-9154-f3cc9daed482)

<a id="377eda9b0fe1808aa05ac9f3f578a8d9"></a>

#### Terraform(HCL) 기본 문법

[HCL 기초 문법](#/post/2c1eda9b-0fe1-80d8-bccb-c9957dd5c35a)

[Terraform Resource](#/post/377eda9b-0fe1-8076-956a-edbe73e00191)

[HCL Data Sources](#/post/374eda9b-0fe1-806f-960c-e8c78235f23c)

[변수](#/post/374eda9b-0fe1-80a9-80b7-f7bba799abef)

[상태 관리](#/post/374eda9b-0fe1-8038-9108-fb0767408fbd)

[반복문](#/post/374eda9b-0fe1-8095-b380-e8b6b0bfb3d6)

[조건문](#/post/374eda9b-0fe1-8035-8145-db166cfafc36)

[module 구성](#/post/374eda9b-0fe1-8096-8856-dcc38b06be89)

<a id="2c0eda9b0fe18087b8f5dd79df8f7ff2"></a>

###  2&#46; AWS 인프라 구성

[튜토리얼](#/post/2c1eda9b-0fe1-80d4-bb4b-d7f2b804390d)

<a id="2c0eda9b0fe1809bbb8ac3ab74b6df96"></a>

###  3&#46; Github 관리

[Terraform Registry]()

<a id="2c0eda9b0fe180789843fc7847beed0d"></a>

###  4&#46;  Jenkins 구축

<a id="2c0eda9b0fe180e3bdadec5c11c31aa6"></a>

###  5&#46; AWS <code>ECS</code> 구성

<a id="2c0eda9b0fe1803ea505dde1f9e69fa8"></a>

###  6&#46; AWS <code>EC2</code> 구성

<a id="2c0eda9b0fe18051b146d66615d16407"></a>

###  7&#46; AWS <code>EKS</code> 구성

<a id="2c0eda9b0fe180a0af33f7f277682156"></a>

###  8&#46; <strong>Terraform, Observability</strong>
