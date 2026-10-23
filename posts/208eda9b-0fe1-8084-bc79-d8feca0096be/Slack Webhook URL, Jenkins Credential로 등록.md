---
order: 3
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 208eda9b-0fe1-8084-bc79-d8feca0096be
title: Slack Webhook URL, Jenkins Credential로 등록
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817b-9c95-d96fd53640c4
    title: CI/CD
  - id: 203eda9b-0fe1-80d5-8c37-c693a491e2cd
    title: 애플리케이션 배포 자동화와 CI/CD -Jenkins
  - id: 208eda9b-0fe1-8084-bc79-d8feca0096be
    title: Slack Webhook URL, Jenkins Credential로 등록
excerpt: Slack Webhook URL, Jenkins Credential로 등록 --- 1. Slack App 설정 → Incoming Webhooks 활성화 - Slack App 설정 → Incoming Webhooks 활성화 - Webhook URL 생성 - ex) https://hooks.slack.com/services
cover: null
icon: null
notionProperties:
  Tags: 추가
  상태: 완료
schema_version: 1
parent_id: 203eda9b-0fe1-80d5-8c37-c693a491e2cd
created: 2025-06-04T12:18:05.302Z
updated: 2025-06-05T08:30:51.612Z
legacy_path: Main/CI-CD-d96fd53640c4/애플리케이션 배포 자동화와 CI-CD -Jenkins-c693a491e2cd/Slack Webhook URL, Jenkins Credential로 등록-d8feca0096be/index.md
legacy_category: CI/CD
source_url: https://beautiful-college-c84.notion.site/208eda9b0fe18084bc79d8feca0096be
---
<a id="208eda9b0fe180629dc1d716f4ab2259"></a>

### Slack Webhook URL, <code>Jenkins Credential</code>로 등록

---

1. Slack App 설정 → <strong>Incoming Webhooks</strong> 활성화
    - Slack App 설정 → <strong>Incoming Webhooks</strong> 활성화

    - Webhook URL 생성

    - ex) <code>https&#58;//hooks&#46;slack&#46;com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX</code>

1. Jenkins Credentials 등록 
    - Jenkins → Manage Jenkins → Credentials 
        ![](c70948806e67af7b.webp)

        ![](e5348012cb7e10da.webp)

    - Domains, (global) &#45; Add Credentials
        ![](a2c262483b852d8e.webp)

        ![](2adfd32e9cb4ec64.webp)

    - Credential 입력
        ![](344322c050d579af.webp)

1. 사용
    <a id="208eda9b0fe1809db274e0ee6c618bec"></a>

    ```groovy
     . . . 
     
    	post {
            success {
                script {
                    def logContent = readFile('deploy-check.log')
                    if (logContent.contains("APPLICATION FAILED TO START")) {
                        error("🚨 Spring Boot 애플리케이션이 포트 충돌 등으로 인해 시작 실패했습니다.")
                    }
                }
                withCredentials([string(credentialsId: 'SLACK_WEBHOOK_URL', variable: 'SLACK_URL')]) {
                    sh """
                    curl -X POST -H 'Content-type: application/json' \\
                    --data '{"text":"✅ *배포 성공* : ${JOB_NAME} #${BUILD_NUMBER}"}' \\
                    \$SLACK_URL
                    """
                }
            }
            failure {
                withCredentials([string(credentialsId: 'SLACK_WEBHOOK_URL', variable: 'SLACK_URL')]) {
                    sh """
                    curl -X POST -H 'Content-type: application/json' \\
                    --data '{"text":"❌ *배포 실패* : ${JOB_NAME} #${BUILD_NUMBER}"}' \\
                    \$SLACK_URL
                    """
                }
            }
        }
    }
    ```

    - <code>withCredentials(&#91;string(credentialsId&#58; &#39;SLACK&#95;WEBHOOK&#95;URL&#39;, variable&#58; &#39;SLACK&#95;URL&#39;)&#93;)</code>
        - 등록한 Slack Webhook을 credentialsId로 가져와 변수로 등록해 사용한다&#46;
