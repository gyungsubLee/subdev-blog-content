---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-811d-bb3e-dec7600b321f
title: Docker Compose, 실습
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8138-94e1-d1a8abd3203c
    title: Docker
  - id: 1c3eda9b-0fe1-81b0-b5b3-cdd0065097a4
    title: "[ sparta ] Docker + CI/CD (중단)"
  - id: 1c3eda9b-0fe1-811d-bb3e-dec7600b321f
    title: Docker Compose, 실습
excerpt: "Docker Compose --- 📖 Docker Compose를 사용하면 여러 컨테이너를 한번에 관리(실행, 종료 …) 가능하다. Docker Compose 사용 이유 yaml 파일을 통한 간단한 설정 및 실행, 종료 여러 컨테이너를 한 파일(yaml)에서 관리 가능 - 각 컨테이너의 이미지, 포트, 환경 변수 등을 "
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-81b0-b5b3-cdd0065097a4
created: 2025-03-27T07:47:43.041Z
updated: 2025-10-12T14:42:40.346Z
legacy_path: Main/Docker-d1a8abd3203c/[ sparta ] Docker + CI-CD (중단)-cdd0065097a4/Docker Compose, 실습-dec7600b321f/index.md
legacy_category: Docker
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1811dbb3edec7600b321f
---
<a id="1c3eda9b0fe1812c92b0f7b99236826c"></a>

## Docker Compose

---

> 📖 
> 
> <a id="1c3eda9b0fe18182aca7e7459cca7e43"></a>
> 
> Docker Compose를 사용하면 <u>여러 컨테이너</u>를 한번에 <strong><u>관리(</u></strong><strong><u><code>실행</code></u></strong><strong><u>, </u></strong><strong><u><code>종료</code></u></strong><strong><u> …)</u></strong> 가능하다&#46;

<details>
<summary>Docker Compose 사용 이유</summary>

<details>
<summary><code>yaml</code> 파일을 통한 간단한 설정 및 실행, 종료</summary>

<details>
<summary>여러 컨테이너를 한 파일(<code>yaml</code>)에서 관리 가능</summary>

- 각 컨테이너의 <strong><u>이미지, 포트, 환경 변수 등을 설정</u></strong> 가능

<details>
<summary>ex) <code>compose&#46;yml</code></summary>

<a id="1c3eda9b0fe181f2912dce3b187b8834"></a>

```yaml
services:
  my-server:
    build: .
    ports:
      - 8080:8080
    depends_on:
      my-db:
        condition: service_healthy
      my-cache-server:
        condition: service_healthy  
  my-db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: pwd1234
      MYSQL_DATABASE: mydb
    volumes:
      - ./mysql_data:/var/lib/mysql
    ports:
      - 3306:3306
    healthcheck:
      test: [ "CMD", "mysqladmin", "ping" ]
      interval: 5s
      retries: 10
  my-cache-server:
    image: redis
    ports:
      - 6379:6379
    healthcheck:
      test: [ "CMD", "redis-cli", "ping" ]
      interval: 5s
      retries: 10
```

</details>

</details>

<details>
<summary><code>docker compose up</code>을 통해 compose 파일을 실행하여 여러 컨테이너 한번에 실행 및 종료 가능 </summary>

<details>
<summary>CLI에서 입력하는 것보다 훨씬 간단하게 실행 가능</summary>

<a id="1c3eda9b0fe18149ae4bf46e7f825f46"></a>

```bash
docker run -d -p 3306:3306 -e MYSQL_ROOT_PASSWART=... -v ...
```

</details>

- 앱을 만드는 <strong><u>여러 컨테이너들</u></strong>을 <u>한꺼번에 관리</u>하고 <u>쉽게 확장</u> 가능

</details>

</details>

<details>
<summary>의존성 관리</summary>

- 컨테이너들 사이 의존관계가 있을 시, Docker Compose(<code>depend on</code>)통해 이를 관리할 수 있다&#46; 

<details>
<summary>ex) </summary>

<a id="1c3eda9b0fe181c98da2c1d868073081"></a>

```plaintext
services:
  my-server:
    build: .
    ports:
      - 8080:8080
    depends_on:
      my-db:
        condition: service_healthy
  my-db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: pwd1234
      MYSQL_DATABASE: mydb
    volumes:
      - ./mysql_data:/var/lib/mysql
    ports:
      - 3306:3306
    healthcheck:
      test: [ "CMD", "mysqladmin", "ping" ]
      interval: 5s
      retries: 10
```

</details>

</details>

<details>
<summary>모니터링, 로깅</summary>

- 컨테이너들 모니터링  가능
    <a id="1c3eda9b0fe181669311d138fbc0409f"></a>

    →  로그를 모아서 관리<br>      문제 발생 시, 빠르게 원인을 찾아 수정 가능

</details>

<details>
<summary>유연성</summary>

- Docker Compose는 <strong><u>개발 환경, 테스트 환경, 실제 운영 환경</u></strong>에서도 <strong>같은 설정 파일</strong>을 써 <strong><u>일관성을 유지</u></strong>할 수 있다&#46; 

</details>

<details>
<summary>보안 강화</summary>

- 컨테이너들의 네트워크를 분리 
    <a id="1c3eda9b0fe181f9ade5ee801bada049"></a>

    ⇒  외부로부터 접근 제한

</details>

<details>
<summary>유지보수 용이</summary>

- 설정 파일 하나로 컨테이너들을 관리하기 때문에, 무언가 바꿀 일이 있으면 파일만 수정하면 된다&#46; 
    - Docker Compose 자동으로 변경사항을 적용한다&#46;

</details>

</details>

<details>
<summary>사용 환경</summary>

<details>
<summary>1&#46; 개발 환경</summary>

- 앱 개발 시, 테스트를 위한 환경 구성이 필요하다

- 이를 docker compose를 통해 쉽게 만들고 관리할 수 있다&#46;
    <details>
    <summary>ex) <code>compose&#46;yml</code> 에 필요  서비스들(데이터베이스, 큐, 캐시, 웹 API 등)을 정의하고 한번에 실행 및 종료 가능하다&#46; </summary>

    <a id="1c3eda9b0fe181d28a2bf3c48342db40"></a>

    ```bash
    # 정의한 compose 파일 실행
    docker compose up -d [--build]

    # 확인
    docker compsoe ps

    # 종료
    docker compose down 
    ```

    </details>

</details>

<details>
<summary>2&#46; 자동화된 테스트 환경</summary>

- 테스트는 앱의 신뢰성을 확보하기 위한 중요한 검증 과정이다&#46; 

- 이를 docker compose를 통해 자동화된 테스트 환경을 구성하여 개발 생산성을 증진시킬 수 있다&#46; 

<details>
<summary>ex)</summary>

<a id="1c3eda9b0fe181ef97daef45f6c8c719"></a>

```bash
docker compose up -d
./run_tests
docker compose down
```

</details>

</details>

<details>
<summary>3&#46; 단일 호스트 베포 </summary>

<a id="1c3eda9b0fe181c292b6cbbbe68f9c7b"></a>

개발, 테스트 뿐 아니라, 실제 앱 운영을 위한 프로덕션 환경에서도 사용 가능하다&#46;

- ex)  <a href="#/post/1c3eda9b-0fe1-810d-bffd-db686e061b22">페이지</a> 

</details>

</details>

<details>
<summary>Docker compsoe 실행 순서</summary>

1. 각 앱의 <code>Dockerfile</code> 작성
    - 개발한 앱의 소스코드를 실행하기 위한 dockerfile 작성

    - 서버 ( Spring Boot, Nginx … )

1. <code>docker&#45;compose&#46;yml</code> 파일 작성
    - 앱 실행을 위한 부가적인 서비스( MySQL, Redis …) 등을 정의하여 한번에 서버와 같이 실행

1. compose 파일 실행
    <a id="1c3eda9b0fe181cea5f6ccfb055d40d4"></a>

    ```bash
    docker compose up -d 
    ```

</details>
