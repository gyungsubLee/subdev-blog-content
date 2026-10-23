---
order: 22
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8175-a89e-d9cdd18ece7d
title: git add + commit , alias 설정, + push
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81f9-b76e-c9d937ee7825
    title: Git
  - id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
    title: "Note: Git CLI"
  - id: 1c3eda9b-0fe1-8175-a89e-d9cdd18ece7d
    title: git add + commit , alias 설정, + push
excerpt: 'git commit -am --- 이미 Git에 추적되고 있는 파일을 수정하거나 삭제하는 경우에 사용 가능 bash git commit -am "커밋 메시지" git add . && git commit -m --- 새 파일도 포함 bash git add . && git commit -m "커밋 메시지" - git add '
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
created: 2025-03-27T07:47:52.779Z
updated: 2025-03-27T07:47:52.779Z
legacy_path: Main/Git-c9d937ee7825/Note- Git CLI-fb5c624de379/git add + commit , alias 설정, + push-d9cdd18ece7d/index.md
legacy_category: Git
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18175a89ed9cdd18ece7d
---
<a id="1c3eda9b0fe181dcae4bd9ef8f608b1d"></a>

### <strong><code>git commit &#45;am </code></strong>

---

<a id="1c3eda9b0fe1819bbabed6023729748c"></a>

이미 Git에 추적되고 있는 파일을 <strong>수정하거나 삭제하는 경우에</strong> 사용 가능

<a id="1c3eda9b0fe18142a7a2c88fd500b4a0"></a>

```bash
git commit -am "커밋 메시지"
```

<a id="1c3eda9b0fe181a1a40ad138566b26a6"></a>

### <strong><code>git add &#46; &#38;&#38; git commit &#45;m</code></strong>

---

<a id="1c3eda9b0fe181f68992f623e58c96b4"></a>

새 파일도 포함

<a id="1c3eda9b0fe18122aaebcfd20e5a0ee0"></a>

```bash
git add . && git commit -m "커밋 메시지"
```

- <code>git add &#46;</code>&#58; 현재 디렉토리의 모든 변경 사항을 스테이징

- <code>&#38;&#38;</code>&#58; 두 명령어를 연속 실행

- <code>git commit &#45;m</code>&#58; 커밋 메시지를 포함하여 커밋

<a id="1c3eda9b0fe181798173e90f92ba055e"></a>

### <strong>별도의 Git Alias로 설정</strong>

---

<a id="1c3eda9b0fe1814f8be1f93df7fa138e"></a>

 alias로 설정

<a id="1c3eda9b0fe181729629d31d1766cd74"></a>

```bash
git config --global alias.ac '!git add . && git commit -m'
```

- 사용

<a id="1c3eda9b0fe1817eacc5c770c89a57de"></a>

```bash
git ac "커밋 메시지"
```

<a id="1c3eda9b0fe1817d9eeacca8a846705a"></a>

### push까지 한번에 처리

---

<a id="1c3eda9b0fe181b5baceeb32a99773a4"></a>

```bash
git add . && git commit -m "커밋 메시지" && git push
```
