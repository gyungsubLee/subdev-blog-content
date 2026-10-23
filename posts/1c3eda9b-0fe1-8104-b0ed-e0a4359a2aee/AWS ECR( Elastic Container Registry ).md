---
order: 15
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8104-b0ed-e0a4359a2aee
title: AWS ECR( Elastic Container Registry )
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8138-94e1-d1a8abd3203c
    title: Docker
  - id: 1c3eda9b-0fe1-8115-b158-c17d844ab16c
    title: 비전공자도 이해할 수 있는 Docker 입문/실전
  - id: 1c3eda9b-0fe1-8104-b0ed-e0a4359a2aee
    title: AWS ECR( Elastic Container Registry )
excerpt: AWS ECR --- 📖 필요한 앱의 이미지를 다운로드 받을 때 Dockerhub를 사용한다. - Dockerhub는 이미지를 저장 및 다운할 수 있는 저장소이다. 이런 Dockerhub와 동일한 역할을 하는 서비스가AWS ECR이다. - 이미지를 저장 및 다운 가능한 저장소 역할을 한다. 🤔 왜 Dockerhub 대
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8115-b158-c17d844ab16c
created: 2025-03-27T07:47:52.769Z
updated: 2025-03-27T07:47:52.769Z
legacy_path: Main/Docker-d1a8abd3203c/비전공자도 이해할 수 있는 Docker 입문-실전-c17d844ab16c/AWS ECR( Elastic Container Registry )-e0a4359a2aee/index.md
legacy_category: Docker
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18104b0ede0a4359a2aee
---
<a id="1c3eda9b0fe181c1ad23ddbdb672b315"></a>

## AWS ECR

---

> 📖 
> 
> <a id="1c3eda9b0fe181549fb3e70fe2227f43"></a>
> 
> 필요한 앱의 이미지를 다운로드 받을 때 <code>Dockerhub</code>를 사용한다&#46;
> 
> - Dockerhub는 이미지를 저장 및 다운할 수 있는 저장소이다&#46; 
> 
> <a id="1c3eda9b0fe1818fbd64c5832c47a40d"></a>
> 
> <br>이런 <strong><u><code>Dockerhub</code></u></strong><strong><u>와 동일한 역할</u></strong>을 하는 서비스가<code>AWS ECR</code>이다&#46; 
> 
> - <strong><u>이미지를 저장 및 다운</u></strong><em><strong>  </strong></em>가능한 <strong><u>저장소</u></strong><strong><u> 역할</u></strong>을 한다&#46; 

> 🤔 
> 
> <a id="1c3eda9b0fe1816985dbfd83360b58cb"></a>
> 
> 왜 Dockerhub 대신 AWS ECR을 사용하는가?
> 
> <a id="1c3eda9b0fe181ddacd5dc93af4d1977"></a>
> 
> AWS 클라우드 환경에서 인프라 구축 시, <u><code>AWS ECR</code></u><u>을 사용</u>하면 다른 <strong><u>AWS Resource와의 연동이 편</u></strong>하고, <strong><u>AWS 내에서 한 번에 관리</u></strong>할 수 있다&#46;
> 
> - Dockerhub을 사용해도 크게 문제는 없다&#46;

![](5de3d127325b402a.webp)

<a id="1c3eda9b0fe181918ecadfdeca674d3c"></a>

Docker를 사용하지 않을 적에는 많은 사람들이 Github를 사용하여 프로젝틀 코드를 Push  후 EC2에 접속하여 pull 받아 실행시키는  방식을 많이 사용했다&#46; 

<a id="1c3eda9b0fe18179a2fcd106ae4c30f9"></a>

이 방식은 <strong><u>프로젝트 코드 전체를 EC2로 이동</u></strong>시켜야 하며,  프로젝트 <strong><u>코드를 실행시킬 런타임 환경(Node, JDK 등)도 설치</u></strong>되어 있어야만 실행이 가능하다&#46;

![](3326c0069add8f7c.webp)

<a id="1c3eda9b0fe181688549e9733781aaf8"></a>

Docker의 가장 큰 장점은 <strong><u>이식성</u></strong>이다&#46; 

- Docker만 깔려있다면 어디서든 내가 원하는 프로젝트를 실행시킬 수 있다&#46; 

<a id="1c3eda9b0fe1815ba330d522b188d688"></a>

Gitbub를 활용해 프로젝트 코드 전체를 EC2로 옮겨 Docker 기반으로 실행해도 되지만,

<a id="1c3eda9b0fe181899959c842ffc28045"></a>

프로젝트의 <strong><u>필요한 코드만 Docker image로 빌드</u></strong>하고<strong><u> EC2에서 해당 이미지만 다운</u></strong> 받아서 실행하는 것이 훨<u>씬 더 심플</u>하다&#46;

<a id="1c3eda9b0fe181e38229d4dcc48a6d0a"></a>

정리하자면 <strong><u>AWS ECR을 배우는 이유</u></strong><strong>는 </strong><strong>훨씬 간단하게 프로젝트를 배포하고 실행</strong><strong>하기 위해서이다&#46; </strong>
