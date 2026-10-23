---
order: 5
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 208eda9b-0fe1-8052-9f2f-d5c5361c6da9
title: EC2 개인 키 Jenkins Credential로 등록
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817b-9c95-d96fd53640c4
    title: CI/CD
  - id: 203eda9b-0fe1-80d5-8c37-c693a491e2cd
    title: 애플리케이션 배포 자동화와 CI/CD -Jenkins
  - id: 208eda9b-0fe1-8052-9f2f-d5c5361c6da9
    title: EC2 개인 키 Jenkins Credential로 등록
excerpt: "EC2 개인 키 Jenkins Credential로 등록 --- ‣ - Jenkins → Manage Jenkins → Credentials - Domains, (global) - Add Credentials - credentials 값 입력 - kind: SSH Username with private key - scop"
cover: null
icon: null
notionProperties:
  Tags: 추가
  상태: 완료
schema_version: 1
parent_id: 203eda9b-0fe1-80d5-8c37-c693a491e2cd
created: 2025-06-04T12:18:26.120Z
updated: 2025-06-04T12:32:40.058Z
legacy_path: Main/CI-CD-d96fd53640c4/애플리케이션 배포 자동화와 CI-CD -Jenkins-c693a491e2cd/EC2 개인 키 Jenkins Credential로 등록-d5c5361c6da9/index.md
legacy_category: CI/CD
source_url: https://beautiful-college-c84.notion.site/208eda9b0fe180529f2fd5c5361c6da9
---
<a id="208eda9b0fe18052a645e0fa8221107e"></a>

### EC2 개인 키 <code>Jenkins Credential</code>로 등록

---

<a id="207eda9b0fe1803a874ad7cff3e49831"></a>

‣

- Jenkins → Manage Jenkins → Credentials 
    ![](c70948806e67af7b.webp)

    ![](e5348012cb7e10da.webp)

- Domains, (global) &#45; Add Credentials
    ![](a2c262483b852d8e.webp)

    ![](2adfd32e9cb4ec64.webp)

- credentials 값 입력
    ![](8e2f5004e267bc51.webp)

    - kind&#58; SSH Username with private key

    - scope&#58; Global

    - ID&#58; 실제 사용 시, 식별하는 키

    - Description&#58; credentials 에 대한 설명 ( 선택 )

    - Username&#58; OS에서 사용하는 유저명 사용

    - Private Key&#58; SSH 개인키의 value 값 입력
        <a id="208eda9b0fe180baa48bedf263e6b831"></a>

        ```bash
        cat jenkins_prac.pem | pbcopy
        ```

        - 그냥 복사 시, 공백 때문에 문제가 생길 수 있음

    - Passphrase&#58; credentials에 비밀번호 ( 선택 )
        - CI/CD 구축에 사용 시, 일반적으로 설정 안함
