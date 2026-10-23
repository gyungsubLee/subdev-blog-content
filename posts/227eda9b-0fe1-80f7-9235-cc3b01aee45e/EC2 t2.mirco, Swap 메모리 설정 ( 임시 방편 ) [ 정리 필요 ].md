---
order: 6
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 227eda9b-0fe1-80f7-9235-cc3b01aee45e
title: EC2 t2.mirco, Swap 메모리 설정 ( 임시 방편 ) [ 정리 필요 ]
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817b-9c95-d96fd53640c4
    title: CI/CD
  - id: 227eda9b-0fe1-80d6-bacc-e93ff1df19a3
    title: 비전공자도 이해할 수 있는 CI/CD 입문·실전
  - id: 227eda9b-0fe1-80f7-9235-cc3b01aee45e
    title: EC2 t2.mirco, Swap 메모리 설정 ( 임시 방편 ) [ 정리 필요 ]
excerpt: "[[AWS] EC2 메모리 부족 현상 - AWS 프리티어 t2.micro에서 Swap 메모리 설정하기]() EC2 t2.mirco는 1GB의 메모리 스펙을 가진다. 따라서 여러 프로젝트를 동시에 실행하면 메모리 부족으로 서버가 죽는 일이 빈번하게 발생된다. 이를 swap 메모리 설정을 통해 임시적으로 디스크(HDD/SSD"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80d6-bacc-e93ff1df19a3
created: 2025-07-05T03:56:10.334Z
updated: 2025-07-05T04:44:51.047Z
legacy_path: Main/CI-CD-d96fd53640c4/비전공자도 이해할 수 있는 CI-CD 입문·실전-e93ff1df19a3/EC2 t2.mirco, Swap 메모리 설정 ( 임시 방편 ) [ 정리 필요 ]-cc3b01aee45e/index.md
legacy_category: CI/CD
source_url: https://beautiful-college-c84.notion.site/227eda9b0fe180f79235cc3b01aee45e
---
[&#91;AWS&#93; EC2 메모리 부족 현상 &#45; AWS 프리티어 t2&#46;micro에서 Swap 메모리 설정하기]()

<a id="227eda9b0fe1815384fcc0a499d0a6be"></a>

EC2 <code>t2&#46;mirco</code>는 1GB의 메모리 스펙을 가진다&#46; 따라서 여러 프로젝트를 동시에 실행하면 메모리 부족으로 서버가 죽는 일이 빈번하게 발생된다&#46; 

<a id="227eda9b0fe1810590fdd8f9c77e6ab4"></a>

이를 swap 메모리 설정을 통해 임시적으로 디스크(<code>HDD/SSD</code>) 일부를 마치 RAM처럼 사용하여 해결한다&#46; 

- 물리 메모리가 부족할 때 응급처리용으로 유용하지만, 디스크를 사용하는 만큼 속도는 RAM 보다 현저히 느리다&#46; 

- 하지만 서버가 죽어 서비스가 멈추는 것 보단 낫다&#46;
