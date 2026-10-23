---
order: 3
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 28aeda9b-0fe1-80ea-960c-c3af7af1edc7
title: ref.  env 파일 생성 및 멀티 서버 docker 빌드
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8138-94e1-d1a8abd3203c
    title: Docker
  - id: 28aeda9b-0fe1-80ea-960c-c3af7af1edc7
    title: ref.  env 파일 생성 및 멀티 서버 docker 빌드
excerpt: "reference: ‣ yaml name: CI/CD on: push: branches: - main pullrequest: branches: - main jobs: build: name: Build and Deploy runs-on: ubuntu-latest steps: - name: Checkout Code uses:"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 1c3eda9b-0fe1-8138-94e1-d1a8abd3203c
created: 2025-10-12T14:36:47.663Z
updated: 2025-10-12T14:39:08.614Z
legacy_path: Main/Docker-d1a8abd3203c/ref.  env 파일 생성 및 멀티 서버 docker 빌드-c3af7af1edc7/index.md
legacy_category: Docker
source_url: https://beautiful-college-c84.notion.site/28aeda9b0fe180ea960cc3af7af1edc7
---
<a id="28aeda9b0fe1805289f6ddfb09dc18f5"></a>

reference&#58; ‣

<a id="28aeda9b0fe180cd9c5aca1b6c3b4b6e"></a>

```yaml
name: CI/CD

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build:
    name: Build and Deploy
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Set up JDK 17
        uses: actions/setup-java@v3
        with:
          java-version: '17'
          distribution: 'temurin'
          cache: gradle

      - name: Grant execute permission for Gradle
        run: chmod +x ./gradlew

      - name: Build with Gradle
        run: ./gradlew bootJar

      - name: Docker Build and Push main server image
        env:
          DOCKER_USER: ${{ secrets.DOCKER_USERNAME }}
          DOCKER_PASS: ${{ secrets.DOCKER_PASSWORD }}
          DOCKER_HUB_REPOSITORY: ${{ secrets.DOCKER_HUB_REPOSITORY }}
        run: |
          echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
          docker build -t "$DOCKER_HUB_REPOSITORY":pillyohae -f main-server/Dockerfile ./main-server
          docker push "$DOCKER_HUB_REPOSITORY":pillyohae

      - name: Docker Build and Push payment server image
        env:
          DOCKER_USER: ${{ secrets.DOCKER_USERNAME }}
          DOCKER_PASS: ${{ secrets.DOCKER_PASSWORD }}
          DOCKER_HUB_REPOSITORY: ${{ secrets.DOCKER_HUB_REPOSITORY }}
        run: |
          echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
          docker build -t "$DOCKER_HUB_REPOSITORY":payment -f payment-server/Dockerfile ./payment-server
          docker push "$DOCKER_HUB_REPOSITORY":payment

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v1
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ap-northeast-2

      - name: Create .env file
        run: |
          cat <<EOF > .env
          DOCKER_HUB_REPOSITORY=${{ secrets.DOCKER_HUB_REPOSITORY }}
          DATABASE_USERNAME=${{ secrets.DATABASE_ID }}
          DATABASE_PASSWORD=${{ secrets.DATABASE_PASSWORD }}
          DATABASE_URL=${{ secrets.DATABASE_URL }}
          JPA_HIBERNATE_DDL=${{ secrets.JPA_HIBERNATE_DDL }}
          BUCKET_NAME=${{ secrets.BUCKET_NAME }}
          AWS_REGION=${{ secrets.AWS_REGION }}
          ACCESS_KEY=${{ secrets.AWS_ACCESS_KEY }}
          SECRET_KEY=${{ secrets.AWS_SECRET_ACCESS_KEY }}
          TOSS_SECRET_KEY=${{ secrets.TOSS_SECRET_KEY }}
          JWT_SECRET_KEY=${{ secrets.JWT_SECRET_KEY }}
          RABBITMQ_HOST=${{ secrets.RABBITMQ_HOST }}
          RABBITMQ_PORT=${{ secrets.RABBITMQ_PORT }}
          RABBITMQ_USERNAME=${{ secrets.RABBITMQ_USERNAME }}
          RABBITMQ_PASSWORD=${{ secrets.RABBITMQ_PASSWORD }}
          REDIS_HOST=${{ secrets.REDIS_HOST }}
          OPENAI_API_KEY=${{ secrets.OPENAI_API_KEY }}
          TZ=Asia/Seoul
          EOF
      - name: List files in repo root
        run: ls -R

      - name: Copy docker files to main server
        uses: appleboy/scp-action@master
        with:
          host: ${{ secrets.AWS_MAIN_SERVER_SSH_HOST }}
          username: ${{ secrets.AWS_SSH_USERNAME }}
          key: ${{ secrets.AWS_SSH_KEY }}
          port: 22
          source: "./main-server/docker-compose.yml,./main-server/.env
          target: "~/app/"
          strip_components: 1  # main-server/ 경로 제거

      - name: Copy docker files to payment server
        uses: appleboy/scp-action@master
        with:
          host: ${{ secrets.AWS_PAYMENT_SERVER_SSH_HOST }}
          username: ${{ secrets.AWS_SSH_USERNAME }}
          key: ${{ secrets.AWS_SSH_KEY }}
          port: 22
          source: "./payment-server/docker-compose.yml,./payment-server/.env
          target: "~/app/"
          strip_components: 1

      - name: SSH into server and deploy main server
        uses: appleboy/ssh-action@master
        env:
          DOCKER_USER: ${{ secrets.DOCKER_USERNAME }}
          DOCKER_PASS: ${{ secrets.DOCKER_PASSWORD }}
        with:
          host: ${{ secrets.AWS_MAIN_SERVER_SSH_HOST }}
          username: ${{ secrets.AWS_SSH_USERNAME }}
          key: ${{ secrets.AWS_SSH_KEY }}
          port: 22
          script: |
            echo "$DOCKER_PASS" | sudo docker login -u "$DOCKER_USER" --password-stdin
            cd ~/app
            sudo docker rm -f server || true
            sudo docker compose pull
            sudo docker compose up -d --remove-orphans
          

      - name: SSH into server and deploy payment server
        uses: appleboy/ssh-action@master
        env:
          DOCKER_USER: ${{ secrets.DOCKER_USERNAME }}
          DOCKER_PASS: ${{ secrets.DOCKER_PASSWORD }}
        with:
          host: ${{ secrets.AWS_PAYMENT_SERVER_SSH_HOST }}
          username: ${{ secrets.AWS_SSH_USERNAME }}
          key: ${{ secrets.AWS_SSH_KEY }}
          port: 22
          script: |
            echo "$DOCKER_PASS" | sudo docker login -u "$DOCKER_USER" --password-stdin
            cd ~/app
            sudo docker rm -f server || true
            sudo docker compose pull
            sudo docker compose up -d --remove-orphans
      

```
