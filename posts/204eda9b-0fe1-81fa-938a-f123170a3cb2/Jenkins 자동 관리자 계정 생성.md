---
order: 4
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 204eda9b-0fe1-81fa-938a-f123170a3cb2
title: Jenkins 자동 관리자 계정 생성
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817b-9c95-d96fd53640c4
    title: CI/CD
  - id: 203eda9b-0fe1-80d5-8c37-c693a491e2cd
    title: 애플리케이션 배포 자동화와 CI/CD -Jenkins
  - id: 204eda9b-0fe1-81fa-938a-f123170a3cb2
    title: Jenkins 자동 관리자 계정 생성
excerpt: "🔧 Jenkins 자동 관리자 계정 생성: Production-Ready CI/CD 자동화 구현 📋 Executive Summary Jenkins는 DevOps 파이프라인의 핵심 컴포넌트로, 초기 설정 시 Setup Wizard를 통한 수동 관리자 계정 생성을 요구합니다. 하지만 Infrastructure as Cod"
cover: null
icon: null
notionProperties:
  Tags: 트러블슈팅
  상태: 다시보기
schema_version: 1
parent_id: 203eda9b-0fe1-80d5-8c37-c693a491e2cd
created: 2025-05-31T10:36:46.770Z
updated: 2025-06-05T08:25:47.684Z
legacy_path: Main/CI-CD-d96fd53640c4/애플리케이션 배포 자동화와 CI-CD -Jenkins-c693a491e2cd/Jenkins 자동 관리자 계정 생성-f123170a3cb2/index.md
legacy_category: CI/CD
source_url: https://beautiful-college-c84.notion.site/204eda9b0fe181fa938af123170a3cb2
---
<a id="204eda9b0fe18157a1becda38e4cf88d"></a>

# 🔧 Jenkins 자동 관리자 계정 생성&#58; Production&#45;Ready CI/CD 자동화 구현

<a id="204eda9b0fe181ada91af1e84a023b48"></a>

## 📋 Executive Summary

<a id="204eda9b0fe1814a8929ceeda1c44663"></a>

Jenkins는 DevOps 파이프라인의 핵심 컴포넌트로, 초기 설정 시 Setup Wizard를 통한 수동 관리자 계정 생성을 요구합니다&#46; 하지만 Infrastructure as Code(IaC) 환경에서는 <strong>완전 자동화된 배포</strong>가 필수적입니다&#46;

<a id="204eda9b0fe18133859ff940458ee9b6"></a>

본 가이드는 <strong>Groovy 스크립트 기반 초기화 메커니즘</strong>을 활용하여 Jenkins 관리자 계정을 자동 생성하고, Setup Wizard를 우회하는 Enterprise급 솔루션을 제시합니다&#46;

---

<a id="204eda9b0fe18174bc84d1307e34b9bb"></a>

## 🎯 Problem Statement

<a id="204eda9b0fe181298ac3fed22107a8a0"></a>

### 현재 상황 분석

- Jenkins 기본 이미지&#58; <code>jenkins/jenkins&#58;lts</code>는 초기 실행 시 Setup Wizard 강제 실행

- 환경변수 <code>JENKINS&#95;ADMIN&#95;ID</code>, <code>JENKINS&#95;ADMIN&#95;PASSWORD</code> 설정만으로는 자동 계정 생성 불가

- Container Orchestration 환경(Kubernetes, Docker Swarm)에서 수동 개입 불가능

<a id="204eda9b0fe1814ea7c2e85b336c5f58"></a>

### Business Impact

- <strong>배포 지연</strong>&#58; 수동 설정으로 인한 CI/CD 파이프라인 구축 병목

- <strong>일관성 부족</strong>&#58; 환경별 설정 차이로 인한 운영 리스크

- <strong>확장성 제한</strong>&#58; Auto&#45;scaling 환경에서 Jenkins 인스턴스 동적 생성 제약

---

<a id="204eda9b0fe181b48e58ee953bb58ceb"></a>

## 🏗️ Architecture Overview

<a id="204eda9b0fe181e0a952d18a07a9df47"></a>

```plaintext
jenkins-automation/
├── .env                           # Environment configuration
├── docker-compose.yml            # Container orchestration
├── security/
│   └── basic-auth.groovy         # Authentication bootstrap
└── scripts/
    └── init.groovy.d/
        └── 01-admin-setup.groovy  # Initialization script

```

<a id="204eda9b0fe181a984dbe5acab2377b0"></a>

### 🔄 Execution Flow

1. <strong>Container Startup</strong>&#58; Docker Compose 기반 Jenkins 인스턴스 시작

1. <strong>Environment Injection</strong>&#58; <code>&#46;env</code> 파일의 credential 정보 환경변수로 주입

1. <strong>Groovy Execution</strong>&#58; <code>init&#46;groovy&#46;d</code> 디렉토리 내 스크립트 자동 실행

1. <strong>Security Configuration</strong>&#58; HudsonPrivateSecurityRealm &#43; Authorization Strategy 적용

1. <strong>Wizard Bypass</strong>&#58; Setup Wizard 건너뛰고 즉시 서비스 가용

---

<a id="204eda9b0fe181828386d8c01de5e63b"></a>

## 💾 Implementation

<a id="204eda9b0fe18158a3cac89091e646b4"></a>

### 📄 Environment Configuration (<code>&#46;env</code>)

<a id="204eda9b0fe1810aaf4bcdc00d67a9d9"></a>

```shell
# Jenkins Admin Credentials
JENKINS_ADMIN_ID=admin
JENKINS_ADMIN_PASSWORD=P@ssw0rd!2024

# Security Settings
JENKINS_SLAVE_AGENT_PORT=50000
JAVA_OPTS=-Djenkins.install.runSetupWizard=false

```

<a id="204eda9b0fe1811db4cde06ea1a113a3"></a>

### 🐳 Container Orchestration (<code>docker&#45;compose&#46;yml</code>)

<a id="204eda9b0fe1812babc2fc0a7ce8c655"></a>

```yaml
version: '3.8'

services:
  jenkins-controller:
    image: jenkins/jenkins:2.426.1-lts
    container_name: jenkins-prod
    restart: unless-stopped

    environment:
      - TZ=Asia/Seoul
      - JENKINS_ADMIN_ID=${JENKINS_ADMIN_ID}
      - JENKINS_ADMIN_PASSWORD=${JENKINS_ADMIN_PASSWORD}
      - JAVA_OPTS=${JAVA_OPTS}

    ports:
      - "8080:8080"
      - "50000:50000"

    volumes:
      - jenkins_data:/var/jenkins_home
      - ./scripts/init.groovy.d:/var/jenkins_home/init.groovy.d:ro
      - /var/run/docker.sock:/var/run/docker.sock

    networks:
      - jenkins-network

    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8080/login"]
      interval: 30s
      timeout: 10s
      retries: 3
      start_period: 60s

volumes:
  jenkins_data:
    driver: local

networks:
  jenkins-network:
    driver: bridge
    ipam:
      config:
        - subnet: 172.20.0.0/16

```

<a id="204eda9b0fe181a2b573f75529a8cd2b"></a>

### 🔒 Security Bootstrap (<code>scripts/init&#46;groovy&#46;d/01&#45;admin&#45;setup&#46;groovy</code>)

<a id="204eda9b0fe181678208f949657fb758"></a>

```groovy
#!groovy

import jenkins.model.*
import hudson.security.*
import jenkins.security.s2m.AdminWhitelistRule

def instance = Jenkins.get()

// Environment variable validation
def adminId = System.getenv("JENKINS_ADMIN_ID")
def adminPassword = System.getenv("JENKINS_ADMIN_PASSWORD")

if (!adminId?.trim() || !adminPassword?.trim()) {
    println "❌ JENKINS_ADMIN_ID 또는 JENKINS_ADMIN_PASSWORD 환경변수가 설정되지 않았습니다."
    throw new IllegalArgumentException("Required environment variables missing")
}

println "🔧 Jenkins 보안 설정 초기화 중..."

// Security realm configuration
def hudsonRealm = new HudsonPrivateSecurityRealm(false)
hudsonRealm.createAccount(adminId, adminPassword)
instance.setSecurityRealm(hudsonRealm)

// Authorization strategy
def strategy = new FullControlOnceLoggedInAuthorizationStrategy()
strategy.setAllowAnonymousRead(false)
instance.setAuthorizationStrategy(strategy)

// Agent security (Prevent CSRF attacks)
instance.getInjector().getInstance(AdminWhitelistRule.class).setMasterKillSwitch(false)

// Save configuration
instance.save()

println "✅ 관리자 계정 '${adminId}' 생성 완료"
println "🔐 보안 설정 적용 완료"

```

---

<a id="204eda9b0fe181b5b908ed711849caba"></a>

## 🚀 Deployment &#38; Verification

<a id="204eda9b0fe1810fafe5fda3b95ccf08"></a>

### Launch Commands

<a id="204eda9b0fe181d7b0f7c3cfce9c5386"></a>

```shell
# Environment validation
grep -E "JENKINS_ADMIN_ID|JENKINS_ADMIN_PASSWORD" .env

# Container orchestration
docker-compose up -d

# Service status verification
docker-compose ps
docker-compose logs jenkins-controller --tail=50

```

<a id="204eda9b0fe18135aa90c48632486d9d"></a>

### Health Check

<a id="204eda9b0fe18102938fc8a87186adc6"></a>

```shell
# Jenkins availability check
curl -I http://localhost:8080/login

# Admin login verification
curl -u admin:P@ssw0rd!2024 http://localhost:8080/api/json

```

---

<a id="204eda9b0fe18151ac45ee27adc8a54c"></a>

## 🔐 Security Hardening

<a id="204eda9b0fe18107ad99f1b58f4ae9be"></a>

### Advanced Authentication Configuration

<a id="204eda9b0fe1818bb891d59317a4850a"></a>

```groovy
// LDAP Integration Example
import hudson.security.LDAPSecurityRealm

def ldapRealm = new LDAPSecurityRealm(
    "ldap://company.ldap.server:389",
    "dc=company,dc=com",
    "uid={0},ou=people,dc=company,dc=com",
    "cn=jenkins,ou=services,dc=company,dc=com",
    "jenkins_service_password"
)
instance.setSecurityRealm(ldapRealm)

```

<a id="204eda9b0fe181a29e48e00d4b6d6505"></a>

### Role&#45;Based Access Control

<a id="204eda9b0fe181bbb22ad5279f0fa4da"></a>

```shell
# Install Role Strategy Plugin
docker exec jenkins-prod java -jar /opt/jenkins-cli.jar \
  -s http://localhost:8080/ \
  -auth admin:P@ssw0rd!2024 \
  install-plugin role-strategy

```

---

<a id="204eda9b0fe181b7b84edf057d084afb"></a>

## 📊 Production Considerations

<a id="204eda9b0fe1818da021d8eb89beaacf"></a>

### Performance Optimization

|  |  |  |
| --- | --- | --- |
| Configuration | Recommended Value | Purpose |
| <code>JAVA&#95;OPTS</code> | <code>&#45;Xmx2g &#45;Xms1g</code> | JVM 메모리 최적화 |
| <code>executors</code> | <code>2 &#42; CPU&#95;CORES</code> | 병렬 작업 처리량 |
| <code>quietPeriod</code> | <code>5</code> | Build trigger 지연 최소화 |

<a id="204eda9b0fe18188a8abebdbc23d72a7"></a>

### Monitoring &#38; Alerting

<a id="204eda9b0fe1817fba22d94a22077678"></a>

```yaml
# Prometheus monitoring
- job_name: 'jenkins'
  static_configs:
    - targets: ['jenkins-controller:8080']
  metrics_path: '/prometheus'

```

<a id="204eda9b0fe1811e9ed2d2f04f2dc479"></a>

### Backup Strategy

<a id="204eda9b0fe1819e82adeac813c3515e"></a>

```shell
# Automated backup script
#!/bin/bash
BACKUP_DIR="/backup/jenkins"
DATE=$(date +%Y%m%d_%H%M%S)

docker exec jenkins-prod tar czf - /var/jenkins_home | \
  gzip > ${BACKUP_DIR}/jenkins_backup_${DATE}.tar.gz

```

---

<a id="204eda9b0fe1812a9ad1e98d8d309fbc"></a>

## 🔄 CI/CD Pipeline Integration

<a id="204eda9b0fe18140b778d29e89cae01f"></a>

### GitOps Workflow

<a id="204eda9b0fe1819c8617c8e57e1ceec0"></a>

```yaml
# .github/workflows/jenkins-deploy.yml
name: Deploy Jenkins
on:
  push:
    paths: ['infrastructure/jenkins/**']

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Deploy Jenkins
        run: |
          docker-compose -f infrastructure/jenkins/docker-compose.yml up -d
          ./scripts/wait-for-jenkins.sh

```

<a id="204eda9b0fe1813496d9febd782b5489"></a>

### Infrastructure as Code

<a id="204eda9b0fe181af88d5ea37a00cc860"></a>

```hcl
# Terraform example
resource "aws_ecs_service" "jenkins" {
  name            = "jenkins-controller"
  cluster         = aws_ecs_cluster.main.id
  task_definition = aws_ecs_task_definition.jenkins.arn
  desired_count   = 1

  deployment_configuration {
    maximum_percent         = 100
    minimum_healthy_percent = 0
  }
}

```

---

<a id="204eda9b0fe18107a42acf276998b9e8"></a>

## 🎯 Summary &#38; Next Steps

<a id="204eda9b0fe18170bfa7fc87ba39c468"></a>

### ✅ Achieved Outcomes

- <strong>Zero&#45;Touch Deployment</strong>&#58; Setup Wizard 완전 자동화

- <strong>Security Baseline</strong>&#58; Enterprise급 보안 설정 자동 적용

- <strong>Scalability</strong>&#58; Container Orchestration 환경 완전 호환

- <strong>Maintainability</strong>&#58; Infrastructure as Code 기반 관리

<a id="204eda9b0fe181838be0ef091e073dd7"></a>

### 🚀 Extended Roadmap

1. <strong>Multi&#45;Master Setup</strong>&#58; High Availability 구성

1. <strong>Plugin Management</strong>&#58; Automated plugin installation &#38; updates

1. <strong>Secret Management</strong>&#58; HashiCorp Vault 통합

1. <strong>Observability</strong>&#58; ELK Stack 기반 로그 분석

<a id="204eda9b0fe18162af21e1196f8aaf62"></a>

### 📚 References

- <a href="https://github.com/jenkinsci/docker/blob/master/README.md">Jenkins Docker Official Documentation</a>

- <a href="https://www.jenkins.io/doc/book/managing/groovy-hook-scripts/">Groovy Hook Scripts</a>

- <a href="https://www.jenkins.io/doc/book/security/">Jenkins Security Best Practices</a>

---

<a id="204eda9b0fe1813ca678e3df87a8c588"></a>

<strong>💡 Pro Tip</strong>&#58; Production 환경에서는 <code>&#46;env</code> 파일 대신 <strong>AWS Secrets Manager</strong> 또는 <strong>Kubernetes Secrets</strong>를 활용하여 credential 관리를 권장합니다&#46;
