---
order: 20
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 149eda9b-0fe1-8010-9b0f-dc35331888ed
title: "[sparta] 스프링 심화"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 149eda9b-0fe1-8010-9b0f-dc35331888ed
    title: "[sparta] 스프링 심화"
excerpt: "[sparta] 스프링 기초 강의 정리본 - 기간: 24.11.25 ~ 24.11.30 - ‣ reference 페이지 - MVC ( 1 주차 ) 페이지 ( 2 주차 ) 페이지 ( 3 주차 ) 1. 스프링 MVC 심화 HttpMessageConverter1 ArgumentResolver HttpMessageConverte"
cover: null
icon: afdb3850b2976bfa.webp
notionProperties: {}
schema_version: 1
parent_id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
created: 2024-11-25T11:57:34.917Z
updated: 2026-04-04T15:03:46.475Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/[sparta] 스프링 심화-dc35331888ed/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/149eda9b0fe180109b0fdc35331888ed
---
> 
> 
> <a id="ebf5d7afc5cb40b7bafa67fb88247f86"></a>
> 
> &#91;sparta&#93; 스프링 기초 강의 정리본
> 
> - 기간&#58; 24&#46;11&#46;25 &#126; 24&#46;11&#46;30 
> 
> - ‣
> 
> <details>
> <summary>reference</summary>
> 
> <a id="14aeda9b0fe180529799f6a7e647107c"></a>
> 
> <a href="https://beautiful-college-c84.notion.site/53a92a994a3e458aa0536c4caedb3e5e">페이지</a> &#45; MVC ( 1 주차 )
> 
> <a id="14aeda9b0fe18016914ad5e2f1670b27"></a>
> 
> <a href="https://beautiful-college-c84.notion.site/7547053cebc144dabb29c8c96210f588">페이지</a> ( 2 주차 )
> 
> <a id="14aeda9b0fe18032bde3ec5a52e1b85d"></a>
> 
> <a href="https://beautiful-college-c84.notion.site/03e30571f1654107bb4364861ed01c1a">페이지</a> ( 3 주차 )
> 
> </details>

<a id="149eda9b0fe180cf96a3e2268a6f642e"></a>

## 1&#46; 스프링 MVC 심화

[HttpMessageConverter1](#/post/14aeda9b-0fe1-8017-8b78-c89e26996c36)

[ArgumentResolver](#/post/14aeda9b-0fe1-80e3-a99d-fd99562a02c1)

[HttpMessageConverter2](#/post/14aeda9b-0fe1-8088-ba32-fb2fccce0154)

[TypeConverter](#/post/14aeda9b-0fe1-8021-899c-d48ea2ac55b6)

[Converter](#/post/14aeda9b-0fe1-80c3-b702-ca041ee56bd6)

[ConversionService](#/post/14aeda9b-0fe1-8020-b8c6-fc63a8380906)

[Converter 적용](#/post/14aeda9b-0fe1-80e4-88e9-ca388329da07)

[Formatter](#/post/14aeda9b-0fe1-8097-9078-f49d48d7c016)

[Spring Fomatter](#/post/14aeda9b-0fe1-800e-ada2-d3dc0861421e)

[마무리 정리](#/post/14aeda9b-0fe1-80dd-9f72-d22ff89a3591)

<a id="14aeda9b0fe180c882ded808799904e4"></a>

## 2&#46; JPA 심화

[1 : N 연관관계](#/post/14aeda9b-0fe1-813c-aaf7-fae71dd8e135)

[1 : 1 연관관계](#/post/14aeda9b-0fe1-81f5-a0c8-ec04735670f0)

[N : M 연관관계](#/post/14beda9b-0fe1-8099-be2d-f2d2912207ed)

[상속관계 매핑](#/post/14beda9b-0fe1-8031-9ee9-df3340f7d561)

[Proxy](#/post/14beda9b-0fe1-8015-a7a4-d811bc0b0c89)

[지연로딩, 즉시로딩](#/post/14beda9b-0fe1-80f8-a25d-d311950f323c)

[영속성 전이](#/post/14beda9b-0fe1-80dc-a9d0-f9845e66309c)

[JPA, Transaction](#/post/14beda9b-0fe1-80ec-b12a-dc2df0b2a35f)

<a id="14beda9b0fe1808c8424c8f5f85e48e0"></a>

##  3&#46; 스프링 활용

[Bean 생명주기 1](#/post/14beda9b-0fe1-8058-b823-cb44bad87a55)

[Bean 생명주기 2](#/post/14beda9b-0fe1-817e-92c2-d89a23c217b8)

[API 예외처리](#/post/14beda9b-0fe1-8181-aa65-dafdf8074941)

[JPQL](#/post/14beda9b-0fe1-8133-8296-ee5acd84c334)

[JPQL 기초 1](#/post/14beda9b-0fe1-8126-9995-c43baebc9711)

[JPQL 기초 2](#/post/14beda9b-0fe1-81fa-a88c-d788fb44ab0b)

[JPQL 기초 3](#/post/14beda9b-0fe1-81ff-91e0-e266f1205986)

[fetch join 1](#/post/14beda9b-0fe1-81d7-bdb7-f0820e0f7e8d)

[fetch join 2](#/post/14beda9b-0fe1-81c7-9ef2-daf7960bb96f)

[Spring Data JPA와 JPQL](#/post/14ceda9b-0fe1-807b-83d1-ed14d983ebc4)
