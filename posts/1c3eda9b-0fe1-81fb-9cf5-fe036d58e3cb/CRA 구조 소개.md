---
order: 54
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81fb-9cf5-fe036d58e3cb
title: CRA 구조 소개
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1c3eda9b-0fe1-81e6-a83a-de71fca84d73
    title: 실무 중심! FE 입문자를 위한 React
  - id: 1c3eda9b-0fe1-81fb-9cf5-fe036d58e3cb
    title: CRA 구조 소개
excerpt: "package.json --- 현재 프로젝트에 대한 정보들을 담고 있는 하나의 파일 프로젝트의 이름, 버전, private 유무, dependency 등 이 명시 되어 있다. - name: 프로젝트 명 - version: 프로젝트 버전 - private: 프로젝트의 공개 유무 dependencies: 프로젝트의 의존성 명"
cover: null
icon: null
notionProperties:
  상태: 재정리 필요
schema_version: 1
parent_id: 1c3eda9b-0fe1-81e6-a83a-de71fca84d73
created: 2025-03-27T07:47:43.043Z
updated: 2025-03-27T07:47:43.043Z
legacy_path: Main/리액트-c6a3a1072bb9/실무 중심! FE 입문자를 위한 React-de71fca84d73/CRA 구조 소개-fe036d58e3cb/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181fb9cf5fe036d58e3cb
---
<a id="1c3eda9b0fe181fdb0f3e86772912ba3"></a>

## package&#46;json

---

<a id="1c3eda9b0fe181659498e058c59712ca"></a>

현재 프로젝트에 대한 정보들을 담고 있는 하나의 파일

<a id="1c3eda9b0fe18168b5a6dca4308c5d54"></a>

프로젝트의 이름, 버전, private 유무, dependency 등 이 명시 되어 있다&#46; 

- <code>name</code>&#58; 프로젝트 명

- <code>version</code>&#58; 프로젝트 버전

- <code>private</code>&#58; 프로젝트의 공개 유무

<a id="1c3eda9b0fe18180b29be28147b9f647"></a>

### <code>dependencies</code>&#58; 프로젝트의 의존성 명시 

- 프로젝트에서 

- <code>ReactDOM</code>, <code>React Script</code> … 등 다양한 모듈들의 설치 정보가 담겨있음

<a id="1c3eda9b0fe1812da307ceed18c31282"></a>

### <code>script</code> &#45; 프로젝트에서 실행할 cli 명시

<details>
<summary>🧐 React Script</summary>

- CRA로 만들어진 앱은 Script에 의해 빌드되고 실행된다&#46;

- React Script에는 굉장히 다양한 설정들이 포함되어 있다
    - Webpack, Babel … 등

    - CRA의 프로젝트들은 이런 설정 값들이 모두 Script 내부에 감춰져 있다&#46;

    - 따라서 이런 복잡한 설정을 신경 쓸 필요 없이 서비스의 개발에만 집중할 수 있다&#46;

</details>

> ✏️ 
> 
> <a id="1c3eda9b0fe1810db455ca8f6feffe35"></a>
> 
> <code>react run &#91;정의한 script명&#93;</code> 
> 
> - ex) <code>react run start</code> …

- <code>start</code>
    - 서비스를 실행하는 명령어, 서비스에 대한 개발 서버를 띄워, <code>localhost&#58;3000</code> 포트에 접속하면 개발 서비스를 브라우저에서 확인할 수 있다&#46;

- <code>build</code>
    >  개발한 코드 →  압축

    - 리액트로 개발한 코드들을 자바스크립트 코드로 번들링 해준다&#46;
        - 컴포넌트 단위로 쪼개져 있던 파일들을 2,3 개의 번들로 합쳐준다&#46;

        - 번들링된 js 파일을 확인해 보면 <strong><u>한 줄</u></strong>로 쭉, 미니파이된 형태로 복잡하게 나열되있다&#46;

- <code>test</code>
    - 테스트 코드 실행

- <code>eject</code> 
    > ☝🏻 
    > 
    > <a id="1c3eda9b0fe181b68200c36da18eeae7"></a>
    > 
    > 프로젝트를 처음 생성 했을 때만 가능하며, 한번 실행 후 되돌릴 수 없다&#46;
    > 
    > - 초기에 설정 후, 다시 돌릴 필요가 있는 경우 git으로 변경 전 버전으로 돌림
    >     > ⚠️ 프로젝트를 <u>초기 생성 상태로 롤백</u> 하는 것임
    > 
    >     <a id="1c3eda9b0fe181f4884cf13f045a1c49"></a>
    > 
    >     ```bash
    >     git reset --hard
    >     ```

    - React Script에 있는 설정들을 다 밖으로 꺼낸다&#46; ( 다시 되돌릴 수 없음 )
        - <code>eject</code> 명령어는 한번 사용되면 사라짐

    - config 파일에 대한 수정이 필요한 경우 ( env, path, webpack config 수정 등 ) <br>해당 명령어를 사용하여 React Script 내부에 있는 config 파일을 꺼내와 수정한다 

<a id="1c3eda9b0fe1815ab59ee7c972577dc0"></a>

##
