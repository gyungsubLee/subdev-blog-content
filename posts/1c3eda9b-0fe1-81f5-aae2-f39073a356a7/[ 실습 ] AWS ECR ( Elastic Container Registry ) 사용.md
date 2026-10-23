---
order: 9
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81f5-aae2-f39073a356a7
title: "[ 실습 ] AWS ECR ( Elastic Container Registry ) 사용"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8138-94e1-d1a8abd3203c
    title: Docker
  - id: 1c3eda9b-0fe1-8115-b158-c17d844ab16c
    title: 비전공자도 이해할 수 있는 Docker 입문/실전
  - id: 1c3eda9b-0fe1-81f5-aae2-f39073a356a7
    title: "[ 실습 ] AWS ECR ( Elastic Container Registry ) 사용"
excerpt: EC2 콘솔 접속 --- - 해당하는 인스턴스 클릭 - 연결 클릭 - 해당 EC2의 콘솔 창으로 접속 [ 실습 ] AWS ECR ( Elastic Container Registry ) 사용 --- 1. AWS CLI 설치 - 맥 (Mac OS) bash aws cli 설치 brew install awscli 설치 확인 a
cover: null
icon: null
notionProperties:
  중요도: Yes
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8115-b158-c17d844ab16c
created: 2025-03-27T07:47:52.768Z
updated: 2025-05-14T03:23:58.909Z
legacy_path: Main/Docker-d1a8abd3203c/비전공자도 이해할 수 있는 Docker 입문-실전-c17d844ab16c/[ 실습 ] AWS ECR ( Elastic Container Registry )-f39073a356a7/index.md
legacy_category: Docker
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181f5aae2f39073a356a7
---
<details>
<summary>EC2 콘솔 접속</summary>

---

- 해당하는 인스턴스 클릭
    ![](1d4d6ff3fb722084.webp)

- 연결 클릭
    ![](eb83c69c6cfba2c1.webp)

    ![](12218d4932fafd2b.webp)

- 해당 EC2의 콘솔 창으로 접속 
    ![](f4708eb9509c87a6.webp)

</details>

<a id="1c3eda9b0fe1819291c9f05cbbb5d066"></a>

## &#91; 실습 &#93; AWS ECR ( Elastic Container Registry ) 사용

---

<a id="1c3eda9b0fe181739ae3fc6025e8870a"></a>

### 1&#46; AWS CLI 설치

- <strong>맥 (Mac OS)</strong>
    <a id="1c3eda9b0fe18199834fdc1a64fbe364"></a>

    ```bash
    # aws cli 설치
    brew install awscli

    # 설치 확인
    aws --version
    ```

- <strong>우분투(Ubuntu)</strong>
    <a id="1c3eda9b0fe1814d840bf67dc6b3cde1"></a>

    ```bash
    sudo apt install unzip

    curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

    unzip awscliv2.zip

    sudo ./aws/install

    aws --version # 잘 출력된다면 정상 설치된 상태
    ```

<details>
<summary><strong>윈도우(Windows)</strong></summary>

- 이 링크(<a href="https://awscli.amazonaws.com/AWSCLIV2.msi">https&#58;//awscli&#46;amazonaws&#46;com/AWSCLIV2&#46;msi</a>)를 다운받아 설치하기

- 설치 확인
    <a id="1c3eda9b0fe181d890f0f669e8427727"></a>

    ```bash
    aws --version # 잘 출력된다면 정상 설치된 상태
    ```

</details>

<a id="1c3eda9b0fe18174a31af861754cc7f1"></a>

### 2&#46; IAM 생성

<details>
<summary>1&#46; 사용자 생성</summary>

- 액세스 관리 &#45; 사용자 &#45; 사용자 생성
    ![](c19bc992b68e7dd1.webp)

- <code>1단계</code>&#58; 사용자 세부정보 지정
    ![](aac92bb479771537.webp)

- <code>2단계</code>&#58; 권한 설정
    ![](1655d5cec12ee0da.webp)

- <code>3단계</code>&#58; 검토 및 생성
    ![](31e567d84127c2fc.webp)

</details>

<details>
<summary>2&#46; Access Key 생성</summary>

- 생성한 사용자에 접속 &#45; 보안 자격 증명 &#45; 액세스 키 만들기 
    ![](a11c3c1aec27ca1e.webp)

- <code>1단계</code>&#58; 액세스 키 모법 사례 및 대안 &#45; AWS 외부에서 실행되는 애플리케이션  클릭
    ![](fc53ff665ba76f21.webp)

- <code>2단계</code>&#58; 설명 태그
    ![](d0ee5176fdd751b5.webp)

- <code>3단계</code>&#58; 엑세스 키 검색
    ![](2ab94dbdb803702a.webp)

    - 처음 생성 시에만 <code>저장</code> 및 <code>키 확인</code>이 가능하다&#46; ( 이후 확인 불가) 
        - 문제 발생 시, 다시 엑세스 키 생성

</details>

<details>
<summary>3&#46; AWS CLI로 액세스 키 등록하기</summary>

> ☝🏻 
> 
> <a id="1c3eda9b0fe181eb86d5dbf87fe67ba5"></a>
> 
> local 과 EC2 모두 등록해줘야 한다&#46;

<a id="1c3eda9b0fe1816d9f6fe4b1ad8f1ce9"></a>

```bash
# AWS 설정 정보 수정
aws configure

# 아래 내용 순차적으로 입력 
AWS Access Key ID [None]: <IAM 생성 시 발급한 Key id> #
AWS Secret Access Key [None]: <IAM 생성 시 발급한 Secret Access Key>
Default region name [None]: ap-northeast-2
Default output format [None]:

# 등록한 정보 확인
cat ~/.aws/credentials

# 출력 내용
	# aws_access_key_id =  AKIA4U7EZBW4H4Y2UIGJ
	# aws_secret_access_key = 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
```

- <code>aws configure</code>
    ![](4981662c2e961829.webp)

    <a id="1c3eda9b0fe181099465c851a72a405e"></a>

    위와 같이 입력 화면이 나옴 → 값만 차례대로 입력하면 됨

- <code>AWS Access Key ID </code>
    ![](7c02c0f59a5b1dd3.webp)

- <code>AWS Secret Access Key</code>
    - Access Key 생성 시, 저장한 Secret Key

    <a id="1c3eda9b0fe1813e9144c5af5220cd5d"></a>

    ```bash
    # key 저장 
    /Users/igyeongseob/Develop/keys/key.html 
    ```

- <code>Default region name</code>
    - 선택한 리전 id 값 입력
        ![](7855864f0cda3d1a.webp)

</details>

<a id="1c3eda9b0fe181dfb648e5326dae7a1c"></a>

### 3&#46;  AWS ECR(Elastic Container Registry) 설정

<details>
<summary>1&#46; Elastic Container Registry  접속</summary>

![](5169b5b1ca0579e6.webp)

</details>

<details>
<summary>2&#46; 리포지토리 생성</summary>

![](e36edbca55a28401.webp)

> ☝🏻 
> 
> <a id="1c3eda9b0fe1818da439e31f7836db12"></a>
> 
> 강의가 예전 버전이라 내용이 조금 달라졌다&#46; 
> 
> - 강의에서는 <code>public</code> / <code>private</code>으로 구분되지만
> 
> - 현재는 <code>private</code>이 기본으로 존재한다&#46;  

![](1c785280557cfa02.webp)

- 레포지토리 이름 설정

- 태그 변경 가능 설정

- 암호화 알고리즘 설정

- 생성 
    ![](f643a1546b1f8ca3.webp)

</details>

<details>
<summary>3&#46; ECR로 로컬 image 푸시하기 </summary>

- 생성한 ECR 접속
    ![](38d058381b4513bc.webp)

- 프로젝트 이미지 생성 후, ECR에 push
    <details>
    <summary>푸시 명령 보기</summary>

    ![](29778271bceae0f0.webp)

    ![](37ce44a318a5eb1b.webp)

    - 인증 토큰을 검색 및 레지스트리에 대해 Docker 클라이언트를 인증, 이후 AWS CLI 사용
        <a id="1c3eda9b0fe1811b9805d35000d220aa"></a>

        ```bash
        aws ecr get-login-password --region ap-northeast-2 | docker login --username AWS --password-stdin 869673799096.dkr.ecr.ap-northeast-2.amazonaws.com
        ```

    - 도커 이미지 빌드
        <a id="1c3eda9b0fe181c98479dc8886d02b32"></a>

        ```bash
        docker build -t docker-test .
        ```

    - 빌드가 완료 후, 이미지에 태그를 지정
        <a id="1c3eda9b0fe181c09420f948c719dd3a"></a>

        ```bash
        docker tag docker-test:latest 869673799096.dkr.ecr.ap-northeast-2.amazonaws.com/docker-test:latest
        ```

    - 이미지 새로 생성한 ECR에 푸시
        <a id="1c3eda9b0fe18102892ddd2ace90e0eb"></a>

        ```bash
        docker push 869673799096.dkr.ecr.ap-northeast-2.amazonaws.com/docker-test:latest
        ```

    </details>

    1. AWS 인증
        - aws configure 설정했기 때문에, 정상적으로 인증 가능

        <a id="1c3eda9b0fe18133968bc698c93fc158"></a>

        ```bash
        aws ecr get-login-password --region ap-northeast-2 | docker login --username AWS --password-stdin 869673799096.dkr.ecr.ap-northeast-2.amazonaws.com

        # 성공
        # Login Succeeded
        ```

        ![](edb3e93cbfbf1ffb.webp)

    1. 이미지 생성
        <details>
        <summary>Dockerfile 작성</summary>

        <a id="1c3eda9b0fe1814a9004cdb7954186ca"></a>

        ```bash
        FROM openjdk:17-jdk

        ENTRYPOINT ["/bin/bash", "-c", "sleep  5000"]
        ```

        </details>

        <a id="1c3eda9b0fe181b98e0cd257daaa0ec6"></a>

        ```bash
        docker build -t docker-test .
        ```

        - 이미지명은 &#91;AWS &#45; 푸시 명령 보기 &#93; 참고

    1. 태그 지정
        <a id="1c3eda9b0fe1818180b9dbf97a227baa"></a>

        ```bash
        docker tag docker-test:latest 869673799096.dkr.ecr.ap-northeast-2.amazonaws.com/docker-test:latest
        ```

    1. AWS 리포지토리에  푸시 
        <a id="1c3eda9b0fe181d19f14c3332d7704c0"></a>

        ```bash
        docker push 869673799096.dkr.ecr.ap-northeast-2.amazonaws.com/docker-test:latest
        ```

- Push한 Image 확인
    ![](7fba6206ec9cba8d.webp)

</details>

<details>
<summary>4&#46; ECR에 push 한 이미지 받아오기&#58; <code>pull</code></summary>

- 생성된 aws 이미지 제거
    ![](b1e7d23861d4ee27.webp)

    <a id="1c3eda9b0fe181f7a0bee3c3824affbe"></a>

    ```bash
    docker image ls

    docker image rm -f [aws-이미지 ID]ㅣㅣㅣ
    ```

- ECR 이미지 <code>pull</code> 
    ![](c421c11959aa2cfa.webp)

    ![](a5683839a6c54bfa.webp)

    <a id="1c3eda9b0fe18181a607ed8a5250400e"></a>

    ```bash
    # ECR 이미지 다운 
    docker pull [이미지 url]

    # 다운 확인
    docker image ls
    ```

    ![](5a9eb3e46b9f49b5.webp)

</details>
