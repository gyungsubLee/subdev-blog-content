---
order: 3
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 208eda9b-0fe1-80ec-8e66-e63b34f943b1
title: Github Actions를 사용한 git repo 이미지 버전 관리 시스템 구성
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817b-9c95-d96fd53640c4
    title: CI/CD
  - id: 208eda9b-0fe1-80ec-8e66-e63b34f943b1
    title: Github Actions를 사용한 git repo 이미지 버전 관리 시스템 구성
excerpt: "java name: Build & Push Docker to ECR on: push: branches: [main] env: IMAGETAG: ${{ github.sha }} REGION: ${{ secrets.AWSREGION }} jobs: deploy: runs-on: ubuntu-latest steps: - nam"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 1c3eda9b-0fe1-817b-9c95-d96fd53640c4
created: 2025-06-04T07:08:11.749Z
updated: 2025-07-05T04:34:54.881Z
legacy_path: Main/CI-CD-d96fd53640c4/Github Actions를 사용한 git repo 이미지 버전 관리 시스템 구성-e63b34f943b1/index.md
legacy_category: CI/CD
source_url: https://beautiful-college-c84.notion.site/208eda9b0fe180ec8e66e63b34f943b1
---
<a id="208eda9b0fe180ff817bcc313a0ed130"></a>

```java
name: Build & Push Docker to ECR

on:
  push:
    branches: [main]

env:
  IMAGE_TAG: ${{ github.sha }}
  REGION: ${{ secrets.AWS_REGION }}

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout source
        uses: actions/checkout@v3

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v2
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ${{ secrets.AWS_REGION }}

      - name: Login to Amazon ECR
        id: login-ecr
        uses: aws-actions/amazon-ecr-login@v1

      - name: Build, tag, and push image to Amazon ECR
        env:
          ECR_REPO: ${{ secrets.ECR_REPOSITORY }}
        run: |
          docker build -t $ECR_REPO:$IMAGE_TAG .
          docker tag $ECR_REPO:$IMAGE_TAG $ECR_REPO:latest
          docker push $ECR_REPO:$IMAGE_TAG
          docker push $ECR_REPO:latest

      - name: Output ECR image
        run: echo "🚀 ECR 이미지 푸시 완료: ${{ secrets.ECR_REPOSITORY }}:$IMAGE_TAG"
```

<a id="208eda9b0fe180078362ffdb10fe55e8"></a>

### 시크릿 키

|  |  |
| --- | --- |
| AWS&#95;ACCESS&#95;KEY&#95;ID | AWS 액세스 키 |
| AWS&#95;SECRET&#95;ACCESS&#95;KEY | AWS 시크릿 키 |
| AWS&#95;REGION | ap&#45;northeast&#45;2 등 |
| ECR&#95;REPOSITORY | 123456789012&#46;dkr&#46;ecr&#46;ap&#45;northeast&#45;2&#46;amazonaws&#46;com/my&#45;app |

<a id="208eda9b0fe1808eb4aef78bdec38665"></a>

```bash
aws configure

aws ecr create-repository --repository-name testImage --region ap-northeast-2
```
