---
order: 13
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-814b-bfca-e31831859d05
title: "[ 오류 ] VPC 기본 설정 X"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8138-94e1-d1a8abd3203c
    title: Docker
  - id: 1c3eda9b-0fe1-8115-b158-c17d844ab16c
    title: 비전공자도 이해할 수 있는 Docker 입문/실전
  - id: 1c3eda9b-0fe1-814b-bfca-e31831859d05
    title: "[ 오류 ] VPC 기본 설정 X"
excerpt: "[ 오류 ] VPC 기본 설정 존재하지 않음 --- EC2 생성 중 VPC를 설정하는데 있어서, 기본 VPC 설정이 존재하지 않음 오류 기본 VPC 생성이 필요함 해결 - 기본 VPC 생성 --- - VPC - 콘솔창 열기 - 기본 VPC 조회 shell aws ec2 describe-vpcs - “Vpcs”: []: V"
cover: null
icon: null
notionProperties:
  Tags: 🤬 오류
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8115-b158-c17d844ab16c
created: 2025-03-27T07:47:52.769Z
updated: 2025-03-27T07:47:52.769Z
legacy_path: Main/Docker-d1a8abd3203c/비전공자도 이해할 수 있는 Docker 입문-실전-c17d844ab16c/[ 오류 ] VPC 기본 설정 X-e31831859d05/index.md
legacy_category: Docker
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1814bbfcae31831859d05
---
<a id="1c3eda9b0fe181f39c42cc2092d50b14"></a>

## &#91; 오류 &#93; VPC 기본 설정  존재하지 않음

---

<a id="1c3eda9b0fe181efbfc3dfcb94e49d51"></a>

EC2 생성 중 VPC를 설정하는데 있어서, 기본 VPC 설정이 존재하지 않음

<a id="1c3eda9b0fe1811db847f5e0939149cf"></a>

### 오류

![](b8d5466b805fc28e.webp)

<a id="1c3eda9b0fe181c7856bfbc83c141c34"></a>

기본 VPC 생성이 필요함

<a id="1c3eda9b0fe181359d08d07128b8a9f1"></a>

### 해결 &#45; 기본 VPC 생성

---

- VPC
    ![](17438cc678207904.webp)

- 콘솔창 열기
    ![](3608860b2fdde5e5.webp)

- 기본 VPC 조회
    <a id="1c3eda9b0fe181329ce3cc32ea4af45f"></a>

    ```shell
    aws ec2 describe-vpcs
    ```

    - <code>“Vpcs”&#58; &#91;&#93;</code>&#58;  VPC가 존재하지 않음
        ![](5a9428f25fd45183.webp)

- 기본 VPC가 존재하지 않을 경우, 다시 생성
    <a id="1c3eda9b0fe1812da9a6e29e8132b12e"></a>

    ```shell
    aws ec2 create-default-vpc
    ```

    ![](88e1de41561ace3b.webp)

- 기본 VPC가 정상적으로 생성되었는지 확인
    <a id="1c3eda9b0fe181448a08f92307fdc6d2"></a>

    ```shell
    aws ec2 describe-vpcs --query 'Vpcs[*].{ID:VpcId, IsDefault:IsDefault}'
    ```

    ![](569b0d03fe0611cd.webp)

<a id="1c3eda9b0fe181cd9a2ef0c34e4c1ac2"></a>

### 추가 &#45; VPC 이름 변경

---

![](b36794453212e3b7.webp)

<a id="1c3eda9b0fe181d5bf61f4435b557035"></a>

cli 로 생성한 vpc 이름이 <code>&#45;</code> 로 설정됨

<a id="1c3eda9b0fe18132a2d3d333b8fa313d"></a>

따라서 해당 부분을 수정을 진행함

- <strong>기본 VPC ID 확인</strong>
    <a id="1c3eda9b0fe18139bf21f98ad5261bb0"></a>

    ```shell
    aws ec2 describe-vpcs --query 'Vpcs[?IsDefault==`true`].VpcId' --output text
    ```

    ![](5b79462d7142e709.webp)

-  <strong>태그 업데이트 (이름 변경)</strong>
    <a id="1c3eda9b0fe181f2b939f35fe900711a"></a>

    ```shell
    aws ec2 create-tags --resources [VPC ID] --tags Key=Name,Value="My-Default-VPC"
    ```

    ![](272fc5abf4e284ea.webp)

    <a id="1c3eda9b0fe18122adaac294fb9177a6"></a>

    정상적으로 이름이 수정된 것을 확인할 수 있음
