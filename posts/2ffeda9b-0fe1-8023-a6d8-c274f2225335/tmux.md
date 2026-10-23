---
order: 5
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 2ffeda9b-0fe1-8023-a6d8-c274f2225335
title: tmux
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 305eda9b-0fe1-80cb-881b-e0f1ba2b631b
    title: Tool
  - id: 2ffeda9b-0fe1-8023-a6d8-c274f2225335
    title: tmux
excerpt: ✏️ tmux는 터미널 멀티플렉서로, 하나의 터미널에서 여러 세션/창/패널을 관리할 수 있게 해준다. - 세션(Session) → 윈도우(Window) → 패인(Pane) 계층 구조로 구성 - 모든 tmux 명령의 접두사(prefix)는 기본적으로 Ctrl+b이다. 세션 관리 | 명령 | 설명 | | --- | --- |
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 305eda9b-0fe1-80cb-881b-e0f1ba2b631b
created: 2026-02-06T15:47:44.371Z
updated: 2026-04-04T13:54:43.064Z
legacy_path: Main/Tool-e0f1ba2b631b/tmux-c274f2225335/index.md
legacy_category: Tool
source_url: https://beautiful-college-c84.notion.site/2ffeda9b0fe18023a6d8c274f2225335
---
> ✏️ 
> 
> <a id="2ffeda9b0fe180a19179fcb9db475dbc"></a>
> 
> tmux는 터미널 멀티플렉서로, 하나의 터미널에서 여러 세션/창/패널을 관리할 수 있게 해준다&#46;
> 
> - <strong><code>세션(Session)</code></strong><strong> → </strong><strong><code>윈도우(Window)</code></strong><strong> → </strong><strong><code>패인(Pane)</code></strong> 계층 구조로 구성
> 
> - 모든 tmux 명령의 접두사(prefix)는 기본적으로 <code>Ctrl&#43;b</code>이다&#46;

<a id="2ffeda9b0fe1808e988ce9e9fd21e702"></a>

### 세션 관리

| 명령 | 설명 |
| --- | --- |
| <code>tmux new &#45;s 이름</code> | 새 세션 생성 |
| <code>tmux ls</code> | 세션 목록 보기 |
| <code>tmux attach &#45;t 이름</code> | 세션에 다시 접속 |
| <code>Ctrl&#43;b</code> → <code>d</code> | 현재 세션에서 분리(detach) |
| <code>tmux kill&#45;session &#45;t 이름</code> | 세션 종료 |

<a id="2ffeda9b0fe18099af68fc71669b314a"></a>

### 윈도우 (탭처럼 사용)

| 키 | 설명 |
| --- | --- |
| <code>Ctrl&#43;b</code> → <code>c</code> | 새 윈도우 생성 |
| <code>Ctrl&#43;b</code> → <code>n</code> / <code>p</code> | 다음/이전 윈도우 이동 |
| <code>Ctrl&#43;b</code> → <code>0&#126;9</code> | 번호로 윈도우 이동 |
| <code>Ctrl&#43;b</code> → <code>,</code> | 윈도우 이름 변경 |
| <code>Ctrl&#43;b</code> → <code>&#38;</code> | 현재 윈도우 닫기 |

<a id="2ffeda9b0fe1803b8afafa439337bea7"></a>

### 화면 분할

| 키 | 설명 |
| --- | --- |
| <code>Ctrl&#43;b</code> → <code>%</code> | 좌우 분할 |
| <code>Ctrl&#43;b</code> → <code>&#34;</code> | 상하 분할 |
| <code>Ctrl&#43;b</code> → <code>방향키</code> | 패인 간 이동 |
| <code>Ctrl&#43;b</code> → <code>x</code> | 현재 패인 닫기 |
| <code>Ctrl&#43;b</code> → <code>z</code> | 패인 최대화/복원 (zoom) |
| <code>Ctrl&#43;b</code> → <code>Ctrl&#43;방향키</code> | 패인 크기 조절 |

<a id="2ffeda9b0fe1803eadb9fb93238a91c2"></a>

```bash
# 1. 세션 만들고 작업
tmux new -s dev

# 2. 화면 분할해서 코드 편집 + 서버 실행 동시에
Ctrl+b → %          # 좌우 분할
# 왼쪽: vim main.py
# 오른쪽: python main.py

# 3. 퇴근 전 detach (세션은 살아있음)
Ctrl+b → d

# 4. 다음날 다시 접속
tmux attach -t dev
```
