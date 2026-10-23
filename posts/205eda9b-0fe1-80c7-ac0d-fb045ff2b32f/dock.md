---
order: 6
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 205eda9b-0fe1-80c7-ac0d-fb045ff2b32f
title: dock
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817b-9c95-d96fd53640c4
    title: CI/CD
  - id: 205eda9b-0fe1-80c7-ac0d-fb045ff2b32f
    title: dock
excerpt: docker-nginx yaml ┌──────────────┐ ┌─────────────────────────────┐ │ PR 생성/수정 │ ─────▶│ CLA 체크 및 동의 유도(F5 CLA) │ └──────────────┘ └─────────────────────────────┘ │ ▼ ┌─────────────
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 1c3eda9b-0fe1-817b-9c95-d96fd53640c4
created: 2025-06-01T05:10:58.934Z
updated: 2025-06-01T05:22:38.369Z
legacy_path: Main/CI-CD-d96fd53640c4/dock-fb045ff2b32f/index.md
legacy_category: CI/CD
source_url: https://beautiful-college-c84.notion.site/205eda9b0fe180c7ac0dfb045ff2b32f
---
[docker-nginx](https://github.com/nginx/docker-nginx)

<a id="205eda9b0fe180099166f66d94afc0a8"></a>

```yaml
┌──────────────┐       ┌─────────────────────────────┐
│  PR 생성/수정  │ ─────▶│  CLA 체크 및 동의 유도(F5 CLA)  │
└──────────────┘       └─────────────────────────────┘
         │
         ▼
┌──────────────────────┐
│ 매트릭스 기반 테스트      │
│ generate-jobs + test │
└──────────────────────┘
         │
         ▼
┌────────────────────────────────┐
│ DockerHub → AWS ECR Public 동기화│
│ 수동 or 매일 자동 트리거됨           │
└────────────────────────────────┘
```

<details>
<summary>&#91; 코드 &#93; ci&#46;yml</summary>

<a id="205eda9b0fe1808a9528e1efdf96f343"></a>

```yaml
name: GitHub CI

on:
  pull_request:
  push:
  schedule:
    - cron: 0 10 * * Mon

defaults:
  run:
    shell: 'bash -Eeuo pipefail -x {0}'

jobs:

  generate-jobs:
    name: Generate Jobs
    runs-on: ubuntu-latest
    outputs:
      strategy: ${{ steps.generate-jobs.outputs.strategy }}
    steps:
      - uses: actions/checkout@v3
      - uses: docker-library/bashbrew@v0.1.12
      - id: generate-jobs
        name: Generate Jobs
        run: |
          strategy="$(GITHUB_REPOSITORY=nginx "$BASHBREW_SCRIPTS/github-actions/generate.sh")"
          strategy="$(GITHUB_REPOSITORY=nginx "$BASHBREW_SCRIPTS/github-actions/munge-i386.sh" -c <<<"$strategy")"
          echo "strategy=$strategy" >> "$GITHUB_OUTPUT"
          jq . <<<"$strategy" # sanity check / debugging aid

  test:
    needs: generate-jobs
    strategy: ${{ fromJson(needs.generate-jobs.outputs.strategy) }}
    name: ${{ matrix.name }}
    runs-on: ${{ matrix.os }}
    steps:
      - uses: actions/checkout@v3
      - name: Prepare Environment
        run: ${{ matrix.runs.prepare }}
      - name: Pull Dependencies
        run: ${{ matrix.runs.pull }}
      - name: Build ${{ matrix.name }}
        run: ${{ matrix.runs.build }}
      - name: History ${{ matrix.name }}
        run: ${{ matrix.runs.history }}
      - name: Test ${{ matrix.name }}
        run: ${{ matrix.runs.test }}
      - name: '"docker images"'
        run: ${{ matrix.runs.images }}
```

</details>

<details>
<summary>&#91; 코드 &#93; <strong>f5&#95;cla</strong>&#46;yml</summary>

<a id="205eda9b0fe18089ba76f898dfccfd38"></a>

```yaml
# 전체 동작 흐름 요약
1. 사용자가 PR을 생성하거나, 댓글을 작성
2. 워크플로우 트리거
3. CLA 어시스턴트 실행 조건 확인
4. CLA 서명 여부 확인
   └─ ❌ 미서명 시: 안내 댓글 작성
   └─ ✅ 서명 시: 확인 메시지 + PR에 ✅ 상태 표시
5. 서명된 사용자는 별도 저장소(f5-cla-data)에 기록
```

<a id="205eda9b0fe18057a02bc63fbda9d200"></a>

```yaml
---
name: F5 CLA
on:
  issue_comment:
    types: [created]
  pull_request_target:
    types: [opened, closed, synchronize]
permissions: read-all
jobs:
  f5-cla:
    name: F5 CLA
    runs-on: ubuntu-24.04
    permissions:
      actions: write
      pull-requests: write
      statuses: write
    steps:
      - name: Run F5 Contributor License Agreement (CLA) assistant
        if: (github.event.comment.body == 'recheck' || github.event.comment.body == 'I have hereby read the F5 CLA and agree to its terms') || github.event_name == 'pull_request_target'
        uses: contributor-assistant/github-action@ca4a40a7d1004f18d9960b404b97e5f30a505a08 # v2.6.1
        with:
          # Path to the CLA document.
          path-to-document: https://github.com/f5/f5-cla/blob/main/docs/f5_cla.md
          # Custom CLA messages.
          custom-notsigned-prcomment: '🎉 Thank you for your contribution! It appears you have not yet signed the [F5 Contributor License Agreement (CLA)](https://github.com/f5/f5-cla/blob/main/docs/f5_cla.md), which is required for your changes to be incorporated into an F5 Open Source Software (OSS) project. Please kindly read the [F5 CLA](https://github.com/f5/f5-cla/blob/main/docs/f5_cla.md) and reply on a new comment with the following text to agree:'
          custom-pr-sign-comment: 'I have hereby read the F5 CLA and agree to its terms'
          custom-allsigned-prcomment: '✅ All required contributors have signed the F5 CLA for this PR. Thank you!'
          # Remote repository storing CLA signatures.
          remote-organization-name: f5
          remote-repository-name: f5-cla-data
          # Branch where CLA signatures are stored.
          branch: main
          path-to-signatures: signatures/signatures.json
          # Comma separated list of usernames for maintainers or any other individuals who should not be prompted for a CLA.
          # NOTE: You will want to edit the usernames to suit your project needs.
          allowlist: bot*
          # Do not lock PRs after a merge.
          lock-pullrequest-aftermerge: false
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          PERSONAL_ACCESS_TOKEN: ${{ secrets.F5_CLA_TOKEN }}
```

</details>

<details>
<summary>&#91; 코드 &#93; sync&#46;yml</summary>

<a id="205eda9b0fe180b797f4f540c3f91e1f"></a>

```yaml
name: Sync DockerHub with AWS ECR

on:
  workflow_dispatch:
  schedule:
    - cron: 23 20 * * *

defaults:
  run:
    shell: 'bash -Eeuo pipefail -x {0}'

jobs:
  sync-awsecr:
    name: Sync Docker Hub to AWS ECR Public
    runs-on: ubuntu-24.04
    permissions:
      id-token: write
      contents: read
    steps:
      - uses: actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4.2.2

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@e3dd6a429d7300a6a4c196c26e071d42e0343502 # v4.0.2
        with:
          role-to-assume: ${{ secrets.AWS_ROLE_PUBLIC_ECR }}
          aws-region: us-east-1

      - name: Login to Amazon ECR Public
        id: login-ecr-public
        uses: aws-actions/amazon-ecr-login@062b18b96a7aff071d4dc91bc00c4c1a7945b076 # v2.0.1
        with:
          registry-type: public

      - name: Login to Docker Hub
        uses: docker/login-action@9780b0c442fbb1117ed29e0efdff1e18412f7567 # v3.3.0
        with:
          username: ${{ secrets.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}

      - name: Build, tag, and push docker image to Amazon ECR Public
        run: |
          ./sync-awsecr.sh > sync-real.sh
          chmod +x sync-real.sh
          ./sync-real.sh
```

</details>
