---
order: 6
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81eb-92a1-d34a37006ee7
title: SSH 키
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81f9-b76e-c9d937ee7825
    title: Git
  - id: 1c3eda9b-0fe1-81a7-a498-c683f7d0c859
    title: 제대로 파는 git & github (얄코)
  - id: 1c3eda9b-0fe1-81eb-92a1-d34a37006ee7
    title: SSH 키
excerpt: SSH 키란? - SSH 키는 “Secure Shell” 키의 약자로, 네트워크 상에서 데이터를 암호화하여 안전하게 통신하기 위해 사용된다. - 주로 서버와 클라이언트 간의 인증을 위해 사용되며, 암호 대신 사용할 수 있다. - SSH 키를 사용하면, 비밀번호를 입력할 필요 없이 안전하게 서버에 로그인하거나 GitHub와
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-81a7-a498-c683f7d0c859
created: 2025-03-27T07:47:52.774Z
updated: 2025-03-27T07:47:52.774Z
legacy_path: Main/Git-c9d937ee7825/제대로 파는 git & github (얄코)-c683f7d0c859/SSH 키-d34a37006ee7/index.md
legacy_category: Git
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181eb92a1d34a37006ee7
---
<a id="1c3eda9b0fe181a4a0f3ea469bb42e7a"></a>

### SSH 키란?

- SSH 키는 “Secure Shell” 키의 약자로, 네트워크 상에서 데이터를 암호화하여 안전하게 통신하기 위해 사용된다&#46; 

- 주로 서버와 클라이언트 간의 인증을 위해 사용되며, 암호 대신 사용할 수 있다&#46;

- SSH 키를 사용하면, 비밀번호를 입력할 필요 없이 안전하게 서버에 로그인하거나 GitHub와 같은 서비스에 접근할 수 있다&#46;

<a id="1c3eda9b0fe18124a0c5c381953de3af"></a>

### SSH 키 구성

- <strong><code>공개 키 (Public Key)</code></strong>&#58; 이 키는 <strong><u>서버나 서비스에 업로드</u></strong>하여 <strong>사용자가 인증</strong>될 수 있도록 한다&#46;

- <strong><code>개인 키 (Private Key)</code></strong>&#58; 이 키는 <strong><u>사용자의 컴퓨터에 안전하게 저장</u></strong>되어 있어야 하며, <strong><u>절대 다른 사람과 공유해서는 안 된다&#46;</u></strong>

<a id="1c3eda9b0fe1818596f4f7635ce15a89"></a>

### SSH 키, 생성과 사용

<details>
<summary><strong>1&#46; SSH 키 생성</strong></summary>

<a id="1c3eda9b0fe1810fb8b9c3f00f3ccd5d"></a>

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

- <code>&#45;t ed25519</code>&#58; 키 유형 지정

- <code> “your&#95;email&#64;example&#46;com”</code>&#58; 키 식별 주석 

- 생성 과정에서 키를 저장할 위치와 비밀번호를 설정할 수 있다&#46; 기본 경로를 사용하고 비밀번호는 설정하지 않아도 된다&#46;

</details>

<details>
<summary><strong>2&#46; SSH 키 확인</strong></summary>

<a id="1c3eda9b0fe18112ac25e8090ae6f76f"></a>

```bash
ls -al ~/.ssh
```

</details>

<details>
<summary><strong>3&#46; 공개 키 GitHub에 추가</strong></summary>

- 생성된 공개 키 파일(<code>&#126;/&#46;ssh/id&#95;ed25519&#46;pub</code>)의 내용을 복사
    <a id="1c3eda9b0fe1810e8679e65ff7df7c17"></a>

    ```bash
    cat ~/.ssh/id_ed25519.pub
    ```

- GitHub 웹사이트에 로그인 및 이동
    >  Settings &#45;&#62; SSH and GPG keys

- New SSH key를 클릭하고, 공개 키를 입력한 후 저장


</details>
