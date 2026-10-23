---
order: 53
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8119-bf05-d4ecb20225c8
title: vite를 사용한 react 프로젝트 생성
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1c3eda9b-0fe1-81e6-a83a-de71fca84d73
    title: 실무 중심! FE 입문자를 위한 React
  - id: 1c3eda9b-0fe1-8119-bf05-d4ecb20225c8
    title: vite를 사용한 react 프로젝트 생성
excerpt: "vite로 react 프로젝트 생성 --- Vite로 프로젝트 생성 bash npm create vite@latest - 프로젝트 설정 입력 bash Need to install the following packages: create-vite@latest Ok to proceed? (y) y ✔ Project name: "
cover: null
icon: null
notionProperties:
  Tags: 추가
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-81e6-a83a-de71fca84d73
created: 2025-03-27T07:47:43.043Z
updated: 2025-03-27T07:47:43.043Z
legacy_path: Main/리액트-c6a3a1072bb9/실무 중심! FE 입문자를 위한 React-de71fca84d73/vite를 사용한 react 프로젝트 생성-d4ecb20225c8/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18119bf05d4ecb20225c8
---
<a id="1c3eda9b0fe18102ad9ff993aad44209"></a>

## vite로 react 프로젝트 생성

---

<a id="1c3eda9b0fe181a386ced735bb1e6232"></a>

### Vite로 프로젝트 생성

<a id="1c3eda9b0fe181e192dcd5732e506fd0"></a>

```bash
npm create vite@latest
```

- 프로젝트 설정 입력
    <a id="1c3eda9b0fe181b99b41fc08f34e61dc"></a>

    ```bash
    Need to install the following packages:
      create-vite@latest
    Ok to proceed? (y) y
    ✔ Project name: … my-vite-react-app
    ✔ Select a framework: › React
    ✔ Select a variant: › JavaScript
    ```

- 프로젝트 이동 및 의존성 설치
    <a id="1c3eda9b0fe18109820ae01836052bff"></a>

    ```bash
    cd my-vite-react-app
    npm install
    ```

- 개발 서버 실행
    <a id="1c3eda9b0fe1814c9648d739acfbcb37"></a>

    ```bash
    npm run dev

    # http://localhost:5173
    ```

- 프로젝트 구조
    <a id="1c3eda9b0fe181b88e6fdd6ae8e3aeea"></a>

    ```bash
    my-vite-react-app
    ├── index.html         # 메인 HTML 파일
    ├── src/               # React 소스 코드
    │   ├── App.jsx        # 메인 App 컴포넌트
    │   ├── main.jsx       # 진입점 파일
    │   └── assets/        # 정적 자산
    ├── package.json       # 프로젝트 의존성 및 스크립트
    ├── vite.config.js     # Vite 구성 파일
    └── node_modules/      # 설치된 의존성
    ```

<a id="1c3eda9b0fe181e597c4fa431abb6117"></a>

### <code>React</code> &#43; <code>TypeScript</code> 프로젝트 생성

<a id="1c3eda9b0fe1815e957dec60b5fdec70"></a>

```bash
npm create vite@latest my-vite-react-app -- --template react-ts
```

- 베포 파일 빌드
    <a id="1c3eda9b0fe18124ac1bec22ef90c68d"></a>

    ```bash
    npm run build
    ```

- 빌드된 결과 로칼에서 확인
    <a id="1c3eda9b0fe181b8a0a9d096a8d8bd1e"></a>

    ```bash
    npm run preview
    ```
