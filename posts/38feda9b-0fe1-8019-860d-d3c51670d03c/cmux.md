---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 38feda9b-0fe1-8019-860d-d3c51670d03c
title: cmux
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 305eda9b-0fe1-80cb-881b-e0f1ba2b631b
    title: Tool
  - id: 38feda9b-0fe1-8019-860d-d3c51670d03c
    title: cmux
excerpt: ✏️ cmux는 터미널에서 cmux 앱/워크스페이스/탭/패널/브라우저/에이전트 세션을 제어하는 CLI이다. 쉽게 말하면 tmux처럼 터미널 세션을 나누고 제어할 수 있는데, 거기에 워크스페이스, 브라우저 패널, AI agent 세션, diff viewer, sidebar, notification 같은 GUI 기능까지 붙은
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 305eda9b-0fe1-80cb-881b-e0f1ba2b631b
created: 2026-06-30T08:30:29.742Z
updated: 2026-06-30T08:58:00.076Z
legacy_path: Main/Tool-e0f1ba2b631b/cmux-d3c51670d03c/index.md
legacy_category: Tool
source_url: https://beautiful-college-c84.notion.site/38feda9b0fe18019860dd3c51670d03c
---
> ✏️ 
> 
> <a id="38feda9b0fe18056889ced570b7064c9"></a>
> 
> <code>cmux</code>는 터미널에서 <strong>cmux 앱/워크스페이스/탭/패널/브라우저/에이전트 세션을 제어하는 CLI</strong>이다&#46;
> 
> <a id="38feda9b0fe18050ad4ce7e8d0c8e9f4"></a>
> 
> 쉽게 말하면 <code>tmux</code>처럼 터미널 세션을 나누고 제어할 수 있는데, 거기에 <strong>워크스페이스, 브라우저 패널, AI agent 세션, diff viewer, sidebar, notification</strong> 같은 GUI 기능까지 붙은 도구로 보면 된다&#46;

<a id="38feda9b0fe18017aff9db98c6d82d8e"></a>

## <strong>1&#46; 기본 개념</strong>

<a id="38feda9b0fe180cb8e48d553ccca704c"></a>

<code>cmux</code>의 구조는 대략 아래와 같다&#46; 

<a id="38feda9b0fe1803fa896fb10cfe580c5"></a>

```python
Window
 └─ Workspace
     └─ Pane / Panel
         └─ Surface
             ├─ terminal
             ├─ browser
             └─ agent-session
```

| <strong>개념</strong> | <strong>의미</strong> |
| --- | --- |
| Window | cmux 앱의 창 |
| Workspace | 프로젝트 단위 작업 공간 |
| Pane / Panel | 화면 분할 영역 |
| Surface | 실제 실행되는 터미널, 브라우저, 에이전트 세션 |
| Tab | Surface를 탭처럼 관리하는 단위 |
| Agent Session | Codex, Claude, opencode 같은 AI agent 세션 |

<a id="38feda9b0fe1801e980acc0f1d9f378f"></a>

```bash
cmux welcome
```

- 위 명령어 사용 시 조작 단축키에 대한 설명이 나온다&#46; 

- 해당 단축키로 더 쉽고 빠르게 조작 가능하다&#46;

<a id="38feda9b0fe180e3a04cfe7be0acef44"></a>

## 2&#46;  명령어

<details>
<summary><strong>디렉터리를 새 워크스페이스로 열기</strong></summary>

<a id="38feda9b0fe1801aa16bdeaa7f47e53e"></a>

```bash
# cmux {경로}
cmux /path/to/project

# 현재 경로로 열기
cmux .
```

</details>

<details>
<summary><strong>현재 상태 확인 명령어</strong></summary>

<a id="38feda9b0fe18041bf2bc6d10615deaf"></a>

```bash
# 현재 워크스페이스 확인
cmux current-workspace
```

<a id="38feda9b0fe180e883a6fa754d2b18ff"></a>

```bash
# 현재 윈도우 확인
cmux current-window
```

<a id="38feda9b0fe1809b9a21e32b6e19d33f"></a>

```bash
# 현재 pane 목록 보기
cmux list-panes
```

<a id="38feda9b0fe1802cb043c528c70169fb"></a>

```bash
# workspace 목록 보기
cmux list-workspaces
```

<a id="38feda9b0fe1807b8acdf2f1e741aebb"></a>

```bash
# 전체 구조 트리 보기
cmux tree
```

<a id="38feda9b0fe1804fac12d90ab22ce328"></a>

```bash
# 전체 윈도우/워크스페이스까지 확인
cmux tree --all
```

</details>

<details>
<summary><strong>워크스페이스 관리</strong></summary>

<a id="38feda9b0fe18069998bcef61cb4d23c"></a>

```bash
# 새 워크스페이스 생성
cmux new-workspace --name "backend" --cwd /path/to/backend

# 명령어까지 같이 실행
cmux new-workspace \
  --name "backend-server" \
  --cwd /path/to/backend \
  --command "pnpm dev"
```

<a id="38feda9b0fe180f292acfcc6cbbc1332"></a>

```bash
# 워크스페이스 이름 변경
cmux rename-workspace "new-name"

cmux rename-workspace --workspace workspace:2 "api-server"
```

<a id="38feda9b0fe18016893cff924c2d99a8"></a>

```bash
# 워크스페이스 선택
cmux select-workspace --workspace workspace:1
```

<a id="38feda9b0fe18074b153e2cbdf06e347"></a>

```bash
# 워크스페이스 닫기
cmux close-workspace --workspace workspace:1
```

</details>

<details>
<summary><strong>화면 분할</strong></summary>

<a id="38feda9b0fe180fd84eacc3876146ccd"></a>

```bash
# 오른쪽으로 새 pane 생성
cmux new-split right

# 아래쪽으로 새 pane 생성
cmux new-split down
```

<a id="38feda9b0fe1807ca3a3d05fda9dffee"></a>

```bash
# 왼쪽으로 새 pane 생성
cmux new-split left

# 위쪽으로 새 pane 생성
cmux new-split up
```

</details>
