---
order: 4
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 227eda9b-0fe1-80fd-8121-daa9b43f7e2b
title: 매번 Github 계정과 비밀번호를 치는 과정 없애기
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817b-9c95-d96fd53640c4
    title: CI/CD
  - id: 227eda9b-0fe1-80d6-bacc-e93ff1df19a3
    title: 비전공자도 이해할 수 있는 CI/CD 입문·실전
  - id: 227eda9b-0fe1-80fd-8121-daa9b43f7e2b
    title: 매번 Github 계정과 비밀번호를 치는 과정 없애기
excerpt: "reference [Git, Pull/Push할 때 id password 묻지 않게 하기]() 💬 배포를 할 때마다 Github 계정과 비밀번호를 일일이 치는 과정이 포함되어 있으면 배포를 자동화할 수가 없다. 따라서 최초 한 번만 작성하고 그 이후에는 Github 계정과 비밀번호를 입력하지 않아도 되게 해야한다. - "
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80d6-bacc-e93ff1df19a3
created: 2025-07-05T03:56:09.638Z
updated: 2025-07-05T04:46:02.764Z
legacy_path: Main/CI-CD-d96fd53640c4/비전공자도 이해할 수 있는 CI-CD 입문·실전-e93ff1df19a3/매번 Github 계정과 비밀번호를 치는 과정 없애기-daa9b43f7e2b/index.md
legacy_category: CI/CD
source_url: https://beautiful-college-c84.notion.site/227eda9b0fe180fd8121daa9b43f7e2b
---
<details>
<summary>reference</summary>

[Git, Pull/Push할 때 id password 묻지 않게 하기]()

</details>

> 💬 
> 
> <a id="227eda9b0fe181689755cec1e990d072"></a>
> 
> 배포를 할 때마다 <strong>Github 계정과 비밀번호를 일일이 치는 과정이 포함</strong>되어 있으면 <strong><u>배포를 자동화할 수가 없</u></strong>다&#46;
> 
> <a id="227eda9b0fe1814fb53fefaffb849ea2"></a>
> 
> 따라서 <strong><u>최초 한 번만 작성</u></strong>하고 그 이후에는<strong> </strong><strong><u>Github 계정과 비밀번호를 입력하지 않</u></strong>아도 되게 해야한다&#46;
> 
> - cofig 설정을 통해 최초 한번만 작성, 이후 해당 내용을 가져다 사용 

<a id="222eda9b0fe180b7838ef77a27521047"></a>

```bash
# config - credential helper 설정
git config --global credential.helper store

# 프로젝트 pull
git pull origin main
	# Github 계정 및 비밀번호 입력

# 프로젝트 pull 2 - 더이상 인증 정보를 확인하지 않는다.
$ git pull origin main
```

> ⚠️ 
> 
> <a id="222eda9b0fe180138400f7f1e1e94ad4"></a>
> 
> 해당 방식은 <code>&#126;/&#46;git&#45;credentials</code>에 로그인 정보를 저장하여 자동으로 인증하는 방식이다&#46; 
> 
> <a id="222eda9b0fe180b3a15febebf7e49d9f"></a>
> 
> 따라서 <strong>EC2에 접근 가능한 모든 사용자가 해당 </strong><strong><u>Github 인증 정보를 확인</u></strong>할 수 있기 때문에 <strong><u>보안적 취약점</u></strong>이 존재한다&#46;
