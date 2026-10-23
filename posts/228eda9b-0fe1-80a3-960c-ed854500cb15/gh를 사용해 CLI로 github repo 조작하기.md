---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 228eda9b-0fe1-80a3-960c-ed854500cb15
title: gh를 사용해 CLI로 github repo 조작하기
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81f9-b76e-c9d937ee7825
    title: Git
  - id: 228eda9b-0fe1-80a3-960c-ed854500cb15
    title: gh를 사용해 CLI로 github repo 조작하기
excerpt: "GitHub CLI는 gist, 릴리스 및 GitHub Actions를 포함하여 더 많은 명령어와 기능을 갖춘 매우 강력한 도구이다. 따라서 더 자세한 내용은 gh help 명령어나 공식문서 참조를 추천한다. 1. gh 설치 [GitHub - cli/cli: GitHub’s official command line tool"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 1c3eda9b-0fe1-81f9-b76e-c9d937ee7825
created: 2025-07-06T05:23:13.477Z
updated: 2026-02-20T03:21:36.735Z
legacy_path: Main/Git-c9d937ee7825/gh를 사용해 CLI로 github repo 조작하기-ed854500cb15/index.md
legacy_category: Git
source_url: https://beautiful-college-c84.notion.site/228eda9b0fe180a3960ced854500cb15
---
> 
> 
> <a id="228eda9b0fe18056ac06f8c2285fb8f4"></a>
> 
> GitHub CLI는 gist, 릴리스 및 GitHub Actions를<br>포함하여 더 많은 명령어와 기능을 갖춘 매우 강력한 도구이다&#46;
> 
> <a id="228eda9b0fe180d6ae05f536921f359a"></a>
> 
> 따라서 더 자세한 내용은 <code>gh help</code> 명령어나 <a href="https://cli.github.com/manual/">공식문서</a> 참조를 추천한다&#46;

<details>
<summary>1&#46; gh 설치</summary>

[GitHub &#45; cli/cli&#58; GitHub’s official command line tool]()

<a id="228eda9b0fe1801a82d0ce6761994480"></a>

```bash
brew install gh
```

- gh를 통해 github에 대한 repo 생성 및 설정들을 local PC에서 CLI를 통해 조작할 수 있다&#46;

</details>

<details>
<summary>2&#46; gh 로그인</summary>

<a id="228eda9b0fe180e2bc10e8c22a3f3eab"></a>

```bash
gh auth login
```

- 설치가 완료되면 GitHub 계정으로 인증해야한다&#46;<br>위 명령을 실행하고 대화형 프롬프트에 따른다&#46;

- 그러면 웹 브라우저가 열리고 CLI를 승인하라는 메시지가 표시되며 자격 증명이 안전하게 저장된다&#46; ( 인증 성공 )

</details>

<details>
<summary>3&#46; 일반적인 명령어 포맷</summary>

<a id="228eda9b0fe1800a8454fa422398a37c"></a>

```bash
 gh <command> <subcommand>
```

- gh의 기본 명령어 구조는 위와 같다&#46;

</details>

<a id="228eda9b0fe1808f837ddec706f434e0"></a>

### 4&#46;  리포지토리 (<code>repo</code>)

<details>
<summary>4&#46;1 리포지토리 복제</summary>

<a id="228eda9b0fe18077a385ef8de6752ca5"></a>

```bash
 gh repo clone owner/repository
```

- <code> git clone</code>과 똑같이 작동하지만 전체 URL이 필요하지 않으므로 더 편리하다&#46; 

</details>

<details>
<summary>4&#46;2 repository 생성</summary>

<a id="228eda9b0fe180eab6ade9e00c0d947d"></a>

```bash
gh repo create {프로젝트명} --public --add-readme
	# --public
	# --private
	# --template
```

- GitHub에 새 리포지토리 생성

- <code> &#45;&#45;public</code>, <code>&#45;&#45;private</code> , <code>&#45;&#45;template</code>과 같은 플래그로 구성 가능

</details>

<details>
<summary>4&#46;3 repository 보기</summary>

<a id="228eda9b0fe1802799f6c04a0a120561"></a>

```bash
gh repo view
```

- 복제된 리포지토리의 디렉터리 내에서 실행하면 리포지토리의 설명과 README 파일이 표시된다&#46;

</details>

<a id="228eda9b0fe1806b8efcc143b25bf036"></a>

### 5&#46; 풀 리퀘스트 (<code>pr</code>)

<details>
<summary>5&#46;1 풀 리퀘스트 목록</summary>

<a id="228eda9b0fe180f899a0e33aca7ce579"></a>

```bash
 gh pr list
```

- 현재 리포지토리에 대해 열려 있는 풀 리퀘스트 목록을 표시한다&#46;

</details>

<details>
<summary>5&#46;2 풀 리퀘스트 생성</summary>

<a id="228eda9b0fe180d8ad43cbbc5595ff7d"></a>

```bash
 gh pr create
```

- 변경 사항을 새 브랜치로 푸시한 후 위 명령어를 통해 풀 리퀘스트를 생성할 수 있다&#46;

- 그러면 PR의 제목, 본문 및 기본 브랜치를 설정하는 대화형 프로세스가 시작된다&#46;

</details>

<details>
<summary>5&#46;3 풀 리퀘스트 체크아웃</summary>

<a id="228eda9b0fe1807ab418e7d026eb55a3"></a>

```bash
 gh pr checkout <pr-number>
```

- 로컬에서 풀 리퀘스트를 검토하기 위해 위과 같이 브랜치처럼 체크아웃할 수 가능하다&#46;

-  이는 기여자의 변경 사항을 테스트하는 데 매우 유용하다&#46;

</details>

<details>
<summary>5&#46;4  풀 리퀘스트 병합</summary>

<a id="228eda9b0fe1802cb77cde759bdeb31a"></a>

```bash
gh pr merge <pr-number>
```

- 위와 같이 CLI로 직접 PR을 병합할 수 있다&#46; 

</details>

<a id="228eda9b0fe180768b98f35b26e6597a"></a>

### 6&#46; 이슈 (<code>issue</code>)

<details>
<summary>6&#46;1 이슈 목록</summary>

<a id="228eda9b0fe180279d76caa417b3cd87"></a>

```bash
 gh issue list
```

- 리포지토리에 대해 열려 있는 이슈 목록 표시

</details>

<details>
<summary>6&#46;2 이슈 생성</summary>

<a id="228eda9b0fe18083a65bd39b11114774"></a>

```bash
 gh issue create /
 --title /
 "My New Issue" /
 --body /
 "Here are the details."
```

- CLI를 통해 새 이슈 생성

</details>
