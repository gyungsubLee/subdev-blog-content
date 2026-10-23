---
order: 30
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8152-8952-eaf9d0cc7ebf
title: Ubuntu에서 Docker, Docker Compose 설치하기
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8138-94e1-d1a8abd3203c
    title: Docker
  - id: 1c3eda9b-0fe1-8115-b158-c17d844ab16c
    title: 비전공자도 이해할 수 있는 Docker 입문/실전
  - id: 1c3eda9b-0fe1-8152-8952-eaf9d0cc7ebf
    title: Ubuntu에서 Docker, Docker Compose 설치하기
excerpt: EC2 콘솔 접속 --- - 해당하는 인스턴스 클릭 - 연결 클릭 - 해당 EC2의 콘솔 창으로 접속 Ubuntu에서 Docker, Docker Compose 설치하기 bash sudo apt-get update && \ sudo apt-get install -y apt-transport-https ca-certifica
cover: null
icon: null
notionProperties:
  Tags: AWS EC2 + Dokcer
  중요도: Yes
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8115-b158-c17d844ab16c
created: 2025-03-27T07:47:52.765Z
updated: 2025-03-27T07:47:52.765Z
legacy_path: Main/Docker-d1a8abd3203c/비전공자도 이해할 수 있는 Docker 입문-실전-c17d844ab16c/Ubuntu에서 Docker, Docker Compose 설치하기-eaf9d0cc7ebf/index.md
legacy_category: Docker
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181528952eaf9d0cc7ebf
---
<details>
<summary>EC2 콘솔 접속</summary>

---

- 해당하는 인스턴스 클릭
    ![](1d4d6ff3fb722084.webp)

- 연결 클릭
    ![](eb83c69c6cfba2c1.webp)

    ![](12218d4932fafd2b.webp)

- 해당 EC2의 콘솔 창으로 접속 
    ![](f4708eb9509c87a6.webp)

</details>

<a id="1c3eda9b0fe181bca9bce3eed649a610"></a>

### Ubuntu에서 Docker, Docker Compose 설치하기

<a id="1c3eda9b0fe1811ebc9ac51ac75aa9ac"></a>

```bash
  sudo apt-get update && \
	sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common && \
	curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && \
	sudo apt-key fingerprint 0EBFCD88 && \
	sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" && \
	sudo apt-get update && \
	sudo apt-get install -y docker-ce && \
	sudo usermod -aG docker ubuntu && \
	newgrp docker && \
	sudo curl -L "https://github.com/docker/compose/releases/download/2.27.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && \
	sudo chmod +x /usr/local/bin/docker-compose && \
	sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

<a id="1c3eda9b0fe1815e9b5de606945feb9a"></a>

### 설치 확인

<a id="1c3eda9b0fe1815fb66de27cb411d554"></a>

```bash
# Docker 버전 확인
docker -v

# Docker Compose 버전 확인
docker compose version
```
