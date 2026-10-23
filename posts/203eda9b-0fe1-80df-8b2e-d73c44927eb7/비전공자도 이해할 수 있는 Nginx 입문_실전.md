---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 203eda9b-0fe1-80df-8b2e-d73c44927eb7
title: 비전공자도 이해할 수 있는 Nginx 입문/실전
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 206eda9b-0fe1-8063-9f3b-f5406da4ca5b
    title: Nginx
  - id: 203eda9b-0fe1-80df-8b2e-d73c44927eb7
    title: 비전공자도 이해할 수 있는 Nginx 입문/실전
excerpt: "/icons/push-pingreen.svg [인프런] 비전공자도 이해할 수 있는 Nginx 입문/실전 - 기간: 25.05.30(금) ~ 25.06.03(화) - 강의: ‣ - reference: 페이지 - 이후 학습 자료: Nginx 쿡북 💬 해당 강의에서는 Nginx에서 많이 사용하는 대표적인 기능 위조로 선별해 "
cover: null
icon: 776f277b25a19f1a.webp
notionProperties: {}
schema_version: 1
parent_id: 206eda9b-0fe1-8063-9f3b-f5406da4ca5b
created: 2025-05-30T14:01:37.426Z
updated: 2025-06-12T11:13:50.261Z
legacy_path: Main/Nginx-f5406da4ca5b/비전공자도 이해할 수 있는 Nginx 입문-실전-d73c44927eb7/index.md
legacy_category: Nginx
source_url: https://beautiful-college-c84.notion.site/203eda9b0fe180df8b2ed73c44927eb7
---
> /icons/push-pin_green.svg 
> 
> <a id="203eda9b0fe181dcb8bcdb5604fd57c6"></a>
> 
> &#91;인프런&#93; <strong>비전공자도 이해할 수 있는 Nginx 입문/실전</strong>
> 
> - 기간&#58; 25&#46;05&#46;30(금) &#126; 25&#46;06&#46;03(화)
> 
> - 강의&#58; ‣
> 
> - reference&#58; <a href="https://beautiful-college-c84.notion.site/16011062ff0780aa87a3e879cb3ef482">페이지</a> 
> 
> - 이후 학습 자료&#58; <a href="https://product.kyobobook.co.kr/detail/S000213834501">Nginx 쿡북</a>

> 💬 
> 
> <a id="203eda9b0fe1805c9378c3ff5f381424"></a>
> 
> 해당 강의에서는 Nginx에서 많이 사용하는 대표적인 기능 위조로 선별해 학습한다&#46; 
> 
> <a id="203eda9b0fe180f39d9bc678126b9d9a"></a>
> 
> Nginx를 학습 시 중요한 점은 Nginx 설정 파일을 내가 구성하고 싶은 대로 응용할 수 있어야 한다는 점이다&#46; 그러려면 자주 쓰이는 Nginx 문법과 기본적인 파일 구조를 익혀야 한다&#46; 
> 
> - 원리와 기본 문법을 모르면 내가 원하는 방식으로 커스텀할 수 없다&#46; 
> 
> - 개발은 단순히 블로그 글을 보고 따라치는 정도가 아닌 실제 프로젝트에 응용 가능하도록 학습하는 것이 중요하다&#46; 

<details>
<summary><strong>주요 cmd</strong></summary>

<a id="206eda9b0fe180fca04ff9bff6094f00"></a>

```bash
# nginx 정상 동작 확인
sudo systemctl status nginx

# 문법 checking
sudo nginx -t

# nginx 재로딩
sudo nginx -s reload

# access.log 확인
tail -f /var/log/nginx/access.log

# error.log
tail -f /var/log/nginx/error.log

# 정적 파일 수정
sudo vi /usr/share/nginx/html/{파일}

# 라우팅 경로 수정
sudo /etc/nginx/conf.d/default.conf
```

</details>

<a id="203eda9b0fe181b4b5c2ee989a3c4bf3"></a>

## Chapter

[1. 왜 Nginx를 사용하는가](#/post/203eda9b-0fe1-8114-9941-c39cc7292b3a)

[1.2  Apache 쓰면 안 되나요? 왜 굳이 Nginx를 써야 되는거죠?](#/post/203eda9b-0fe1-808d-81bc-d5f1958255f0)

[2. Nginx 설치 및 실행](#/post/203eda9b-0fe1-805b-a109-cead69837fad)

[3.1 Nginx의 웹서버 기능](#/post/203eda9b-0fe1-80ea-bda6-f0c99f4d53f8)

[3.2 Nginx 디버깅](#/post/205eda9b-0fe1-801a-a693-eb3a206de32f)

[3.3 Nginx를 사용한 웹사이트 베포](#/post/206eda9b-0fe1-805d-9767-c1628721338a)

[4. Rout53, 도메인](#/post/203eda9b-0fe1-80b4-a452-d78186e11df2)

[5. 1개 서버, 멀티 도메인 베포](#/post/203eda9b-0fe1-80b7-9f6d-eaa383bb9c05)

[6. Nginx를 활용한 HTTPS 적용](#/post/203eda9b-0fe1-80d3-9f39-db33f51d0acc)

[7. 리버스 프록시(Reverse Proxy)를 활용한 백엔드 서버 베포](#/post/203eda9b-0fe1-80f2-90b8-f70da77d8386)

[8. Nginx를 로드벨런서(Load Balancer)로 사용하기](#/post/203eda9b-0fe1-8099-a5bb-cf3e1a451ec7)

<a id="203eda9b0fe18013994ad013cca8d8b0"></a>

### 추가 

[Docker Compose + Nginx 최적화 통합 가이드](#/post/203eda9b-0fe1-806e-bbb1-e81d0f55fa50)

[DevOps 템플릿 프로젝트](#/post/203eda9b-0fe1-80d5-a8f0-eaf556d5e7f5)

[docker compose로 Nginx 실행](#/post/203eda9b-0fe1-8099-9b1f-c7f557aec443)
