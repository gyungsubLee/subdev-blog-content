---
order: 1
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 164eda9b-0fe1-8045-8afa-f7f337b19a14
title: CS 특강 - 운영체제 ( 정리 중 )
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 152eda9b-0fe1-807b-9fea-d50a10c7203e
    title: 데이터베이스 특강 2 ( 정리 중 )
  - id: 164eda9b-0fe1-8045-8afa-f7f337b19a14
    title: CS 특강 - 운영체제 ( 정리 중 )
excerpt: "📌 CS 특강 - 운영체제 - 진행: 이태현 튜터님 - 기간: 24.12.18 - reference: 페이지 ✏️ 학습 목표 - 운영체제 기술면접에서 가장 많이 물어보는 프로세스, 쓰레드 , 동기화에 대해서 학습 - 동시성 제어를 이해하기 위한 기본적인 CS 지식 - 추가 학습 내용 - Linux - 명령어, 권한, 파"
cover: null
icon: 👨🏻‍💻
notionProperties: {}
schema_version: 1
parent_id: 152eda9b-0fe1-807b-9fea-d50a10c7203e
created: 2024-12-22T08:46:14.808Z
updated: 2026-02-24T22:54:37.589Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/데이터베이스 특강 2 ( 정리 중 )-d50a10c7203e/CS 특강 - 운영체제 ( 정리 중 )-f7f337b19a14/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/164eda9b0fe180458afaf7f337b19a14
---
> 📌 
> 
> <a id="c92f50e4268a43ecb4d00ae8bd4cd783"></a>
> 
> CS 특강 &#45; 운영체제
> 
> - 진행&#58; 이태현 튜터님
> 
> - 기간&#58; 24&#46;12&#46;18
> 
> - reference&#58; <a href="https://beautiful-college-c84.notion.site/09221dd796b94eb1903e00eb114ecf62">페이지</a> 

> ✏️ 
> 
> <a id="75c1ae149b4b49caaf6ef832f30ff046"></a>
> 
> <strong>학습 목표</strong>
> 
> - 운영체제 기술면접에서 가장 많이 물어보는 <strong><code>프로세스</code></strong>, <strong><code>쓰레드</code></strong><strong> , </strong><strong><code>동기화</code></strong>에  대해서  학습
>     - 동시성 제어를 이해하기 위한 기본적인 CS 지식
> 
> - 추가 학습 내용
>     - <code>Linux</code> &#45;  <code>명령어</code>, <code>권한</code>, <code>파일(링크, 마운트)</code>, <code>스토리지</code> 등 

<a id="3dd3478b92794baaadb8dd5c671e9c51"></a>

# 1&#46; 운영 체제

- <strong><code>OS(Operating System)</code></strong>
    - <strong><code>하드웨어와 프로그램들을 관리하고 운영</code></strong>하는 최상위 소프트웨어

    - <strong><code>사용자와 컴퓨터 간의 상호작용</code></strong>을 할 수 있도록 돕는 역할 수행

    ![](af64388d07bb8453.webp)

<a id="164eda9b0fe180efa5b5c1504d490128"></a>

## 1&#46; 역할

![](a58c7d6dc5f8bc13.webp)

<a id="164eda9b0fe180bc8b2af6c5f69c6497"></a>

### 1&#46; 자원 관리

> 운영체제는 컴퓨터 시스템 내의 <code>CPU</code>, <code>Memory</code>, <code>Stroage</code>, <code>Network</code> 등과 같은 하드웨어 및 <code>소프트웨어 자원</code>을 효율적으로 관리한다&#46; 
> 
> - 만약 운영체제가 존재하지 않는다면 <u>각 프로그램</u>이 얼마만큼 <code>CPU</code>를 사용할지, <code>메모리 공간</code>을 어느 정도 할당할지, 어떻게 어디에 데이터나 파일을 저잘지 결정할 수 없다&#46; 

- 프로세스 관리
    - CPU 시간을 여러 프로세스에 공평하게 분배하고, 스케줄링을 통해 실행 순서를 결정한다&#46; 

- 메모리 관리 
    - 프로그램 실행 시, 필요한 메모리 할당 및 해체, 가상 메모리 지원

- 디스크 관리 
    - 파일 시스템을 통해 데이터 저장, 검색, 삭제

- 네트워크 관리
    - 네트워크 연겨로가 데이터 전송을 관리

- 권한 관리
    - 프로그램에 접근할 수 있는 권한을 지정

<a id="164eda9b0fe1803d9245dba8a783222b"></a>

### 2&#46; 자원 보호

> 운영체제는 시스템 자원을 비인가된 접근이나 악성 코드로 부터 보호한다&#46;

- 프로세스 격리
    - 프로세스 간 메모리 영역 접근을 차단하여 충돌 방지

- 사용자 권한 관리
    - 파일 및 프로그램에 대한 접근 권한 설정

- 보안 정책 적용
    - 데이터 암호화, 인증 절차, 방화벽 설정 등으로 시스템 보호

<a id="164eda9b0fe180a498ecd1f384b798a4"></a>

### 3&#46;  하드웨어 인터페이스 제공

<a id="164eda9b0fe18078afd5f8f41bef4cce"></a>

### 4&#46; 사용자 인터페이스 제공

<a id="164eda9b0fe180898786e72f7588fdcd"></a>

## 2&#46; 구성

![](528d6ac197020a3d.webp)

<a id="164eda9b0fe18017914cf191d4262cf3"></a>

## 3&#46; 종류

<a id="164eda9b0fe18021a9c3deabccb13c7f"></a>

# 2&#46; 프로세스, 쓰레드

<a id="164eda9b0fe1805dbc98e3b377e8d824"></a>

## 1&#46; 프로세스 ( Process )

<a id="164eda9b0fe180c0ada5de0c4f7008e7"></a>

### 1&#46; 프로세스의 실행 흐름

<a id="164eda9b0fe18057941fe1579abcf180"></a>

### 2&#46;  프로세스의 구조

<a id="164eda9b0fe1800f80a6de8cb81cf1d0"></a>

### 3&#46; 프로세스의 계층 구조

<a id="164eda9b0fe1800fb67bd923a3392852"></a>

### 4&#46; 프로세스의 상태

<a id="164eda9b0fe180619a63d8149b321b58"></a>

### 5&#46; 문맥 교환 ( Context Switching )

<a id="164eda9b0fe180148e3cca431aacd7b6"></a>

### 6&#46; 프로세스 스케쥴링

<a id="164eda9b0fe1801896baf63e2fc32093"></a>

### 7&#46; 프로세스 간의 통신

<a id="164eda9b0fe18092a82de69d29c78182"></a>

## 2&#46; 쓰레드 ( Tread )

<a id="164eda9b0fe1803b8828fd9f63d049ce"></a>

### 2&#46;1 &#45; 쓰레드의 상태

<a id="164eda9b0fe180388571cc7cb0134a38"></a>

### 2&#46;2 &#45; 문맥 교환 ( Context Switching )

<a id="164eda9b0fe18064b821cc9b080a3e90"></a>

# 3&#46;  동기화

<a id="164eda9b0fe18099a53cd9a374022426"></a>

## 1&#46; 경합 조건 ( Race Condition )

<a id="164eda9b0fe180918cd0c2611cc653b4"></a>

### 1&#46; 뮤텍스 락 ( Mutex Lock &#45; Mutual Exclusion Lock )

<a id="164eda9b0fe180b18ae3f5bb65c0787b"></a>

### 2&#46; 세마포어 락(Semaphore Lock &#45; Semaphore Lock)

<a id="164eda9b0fe1809ca402ff25f2c916b8"></a>

## 2&#46; 교착 상태 ( Deadlock )

<a id="164eda9b0fe180009d12d5d954d9fcb5"></a>

### 1&#46; 교착 상태 예방

<a id="164eda9b0fe180e2856cd88eda41a747"></a>

### 2&#46; 교착 상태 회피

<a id="164eda9b0fe180f19e26fb15245281f0"></a>

### 3&#46; 교착 상태 회복
