---
order: 2
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8137-8ef9-f4f389e5bfb9
title: Mac homebrew mysql 설치 후 ERROR, The server quit without updating PID file
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
    title: DBMS
  - id: 1c3eda9b-0fe1-81ef-9506-cdc300921ef3
    title: MySQL
  - id: 1c3eda9b-0fe1-8137-8ef9-f4f389e5bfb9
    title: Mac homebrew mysql 설치 후 ERROR, The server quit without updating PID file
excerpt: "🧐 PORT vs PID PID ( Process ID ) - 운영 체제 내에서 고유하게 프로세스를 식별하기 위한 ID 값 - 프로세스 관리 용도로 사용, 특정 프로그램(프로세스)의 시작, 종료, 상태 조회 등, 생존 주기를 괸리하기 위해 필요하다. - ex) java 프로그램 2개 → 각 다른 PID를 가짐 PORT "
cover: ff1f0fbd226abd35.png
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-81ef-9506-cdc300921ef3
created: 2025-03-27T07:47:52.778Z
updated: 2025-03-27T07:47:52.778Z
legacy_path: Main/DBMS-e8c2debc9fa0/MySQL-cdc300921ef3/Mac homebrew mysql 설치 후 ERROR, The server qui-f4f389e5bfb9/index.md
legacy_category: DBMS
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181378ef9f4f389e5bfb9
---
<details>
<summary>🧐 <code>PORT</code>  vs<code> PID</code></summary>

<details>
<summary>PID ( Process ID )</summary>

- 운영 체제 내에서 고유하게 프로세스를 식별하기 위한 ID 값

- 프로세스 관리 용도로 사용, 특정 프로그램(프로세스)의 <strong><u>시작, 종료, 상태 조회</u></strong> 등, 생존 주기를 괸리하기 위해 필요하다&#46; 
    - ex) java 프로그램 2개 → 각 다른 PID를 가짐

</details>

<details>
<summary>PORT</summary>

- 네트워크 상에서 특정 서비스와 통신을 식별하기 위한 번호

- 네트워크 연결을 위한 ‘출입구’ 역활을 한다&#46;
    - ex) HTTP&#58; <code>80</code>,  MySQL&#58; <code>3306</code>

- 같은 서버에서 여러 프로세스가 같은 포트를 사용하면 충돌이 발생함
    - 각 서비스 별로 고유하게 할당함
        - ex) MySQL 3306 포트 사용 중, 다른 서비스는 3306 포트 사용 ❌

</details>

- 정리 
    - PID는 운영 체제(OS)에서 실행 중인 프로세스 자체를 식별하는데 쓰이며,

    - PORT는 네트워크 통신에서 어떤 서비스와 연결할지를 식별한다&#46; 

| 구분 | PID (Process ID) | PORT (포트 번호) |
| --- | --- | --- |
| <strong>역할</strong> | 운영 체제에서 실행 중인 프로세스 자체를 식별 | 네트워크 통신에서 어떤 서비스와 연결할지를 식별 |
| <strong>범위</strong> | 운영 체제에서 관리하는 로컬 식별자 | 네트워크에서 서버와 클라이언트 간 통신에 사용 |
| <strong>유효성</strong> | 특정 OS 내에서만 고유 | 같은 서버 내에서도 IP와 함께 조합해 여러 서비스 식별 가능 |
| <strong>할당 대상</strong> | 실행 중인 모든 프로세스 | 네트워크 소켓에 연결된 네트워크 서비스(HTTP, MySQL 등) |
| <strong>일반 사용 위치</strong> | 프로세스 종료 및 자원 관리 | 클라이언트가 특정 서비스에 접속할 때 사용 (예&#58; HTTP 80, MySQL 3306) |

</details>

<details>
<summary>🧐 PID </summary>

<a id="1c3eda9b0fe1817ea800f39adbc061cd"></a>

PiD는 <strong><u>Process ID</u></strong> 의 약자로, <u>운영 체제(OS)가 각 실행 중인 프로스세에 부여하는 고유한 숫자 식별자</u>이다&#46; 

<a id="1c3eda9b0fe181e5b24dd0ad74bfedb0"></a>

프로세스는 운영 체제에서 실행되는 프로그램의 단위이며, PID를 통해 운영체제와  사용자가 특정 프로세스를 구별하도록 한다&#46;

- PID의 주요 특징 과 역활
    <details>
    <summary>고유성</summary>

    - PID는 특정 순간에 실행 중인 프로세스마다 고유하게 할당한다&#46;

    - 이를 통해 운영 체제는 동시에 여러 프로세스를 실행하면서도 각각을 구별할 수 있다&#46;

    </details>

    <details>
    <summary>프로세스 관리</summary>

    - 사용자는 PID를 사용하여 특정 프로세스를 종료하거나, 리소스 사용량을 확인하거나, 우선 순위를 조정할 수 있다&#46; 

    - ex)  Unix 계열의 운영 체제, <code>kill </code>명령어를 사용 → PID를 지정하여 특정 프로세스 종료 가능

    </details>

    <details>
    <summary>PID 파일</summary>

    - 데몬이나 서버 프로세스(MySQL, Apache&#46;&#46;)는 시작할 때 자신만의  PID를 파일에 저장한다<br>이를 PID 파일이라고 한다&#46; 
        - 데몬이나, 서버 프로세스가 자신의 PID를 파일에 저장하는 것은 해당 프로세스가 실행 중인지 여부를 확인하고, 다른 인스턴스가 동일한 PID로 프로세스를 시작하지 않도록 하기 위함이다&#46; 

    </details>

    <details>
    <summary>PID 재사용</summary>

    - 프로세스가 종료되면 해당 PID는 다시 사용 가능 상태가 된다&#46;

    - 따라서 이후 새로운 프로세스가 실행되면 해당 PID에 새로운 프로세스를 할당할 수 있다&#46; 

    </details>

<details>
<summary>명령어</summary>

<details>
<summary>PID 확인 </summary>

<a id="1c3eda9b0fe18160a227d1b6d1d0e686"></a>

```sql
ps -ef | grep {프로그램명}
```

- <code>ps</code>&#58; 현재 실행 중인 프로세스의 상태 출력

- <code>&#45;e</code>&#58; 모든 프로세스 표시, 시스템의 모든 사용자가 실행 중인 프로세스를 포함함

- <code>&#45;f</code>&#58;  프로세스의 전체 정보를 출력, 
    - 즉, PID, 부모 PID, 사용자, CPU 및 메모리 사용량, 실행 시간, 명령어 등을 포함

- <code>&#124;</code>&#58;  파이프 기호, 앞의 명령어의 출력을 뒤의 명령어에 입력으로 전달

- <code>grep  {프로그램명}</code>
    - 해당하는 프로그램의 이름(문자열)이 포함된 라인을 검색함

    - ex) grep java
        - 자바 프로세스가 실행 중인지 여부를 확인함

<details>
<summary>예시) h2 확인 </summary>

<a id="1c3eda9b0fe18166bf04fbf249da60dc"></a>

```sql
ps -ef | grep h2
```

<a id="1c3eda9b0fe181138355e87fdfe4c156"></a>

```plaintext
  501   953     1   0  1:58PM ??         0:00.01 /bin/sh /opt/homebrew/Cellar/h2/2.3.232/libexec/bin/h2.sh -tcp -web -pg
  501   976   953   0  1:58PM ??         0:03.11 /usr/bin/java -cp /opt/homebrew/Cellar/h2/2.3.232/libexec/bin/h2-2.3.232.jar:: org.h2.tools.Console -tcp -web -pg
  501  4844  3529   0  3:41PM ttys002    0:00.01 grep --color=auto --exclude-dir=.bzr --exclude-dir=CVS --exclude-dir=.git --exclude-dir=.hg --exclude-dir=.svn --exclude-dir=.idea --exclude-dir=.tox --exclude-dir=.venv --exclude-dir=venv h2
```

</details>

</details>

<details>
<summary>p</summary>



</details>

</details>

</details>

<a id="1c3eda9b0fe181c39226ddb5c27276db"></a>

### 오류

---

<a id="1c3eda9b0fe18117b24ced5507ab2806"></a>

```sql
ERROR! The server quit without updating PID 
file (/opt/homebrew/var/mysql/igyeongseobs-MacBook-Pro.local.pid)
```

Error Message

<a id="1c3eda9b0fe1818c9c86ed21e30d503e"></a>

위 오류 메세지에서 수정된 PID가 없기 때문에 mysql이 중단 되었다고 알린다&#46; 

<a id="1c3eda9b0fe181599c23cdadae0c406b"></a>

이것 저것 다하다가 결국 그냥 모든 mysql 파일 삭제 후 재설치함

- 관리자 권한으로 삭제해야 삭제됨

<a id="1c3eda9b0fe181968fc3ea7ab3937f6e"></a>

```bash
sudo rm -rf /opt/homebrew/var/mysql
```

<a id="1c3eda9b0fe18149b88bee4481093e85"></a>

사용자 확인

-  현재 해당 디렉토리의 소유자와 그룹을 확인

<a id="1c3eda9b0fe181b7a4b3f24fd6955825"></a>

```bash
ls -ld /opt/homebrew/var/mysql
```

- 해당 디렉토리의 소유자와 그룹 변경
    - 유저 이름 →  mysql

<a id="1c3eda9b0fe181bc9711fd65e6b464fa"></a>

```bash
sudo chown -R mysql:mysql /usr/local/var/mysql
```

- 권한 주기
    - 컴퓨터 디스크 crud를 위한 권한 설정

<a id="1c3eda9b0fe1812c98afe4fc01989c43"></a>

```bash
sudo chmod -R 777 /usr/local/var/mysql
```

<a id="1c3eda9b0fe18119a4acd0a11bbc238a"></a>

사용자 변경 

<a id="1c3eda9b0fe18147b52fdc97a6378438"></a>

이전 버전(&#64;8&#46;4) 을 설치하니 해결됨… 

<a id="1c3eda9b0fe18188ba82e69dc41bee03"></a>

5시간 걸렸네 썩을&#46;&#46;
