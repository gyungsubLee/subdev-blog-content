---
order: 10
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 367eda9b-0fe1-8014-b834-f04a86647e59
title: Replication (데이터 복제)
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
    title: 대규모 시스템 설계
  - id: 356eda9b-0fe1-8010-9561-c7098d310a4f
    title: "The RED: 대용량 서비스를 위한 아키텍처 with Redis (by 강대명)"
  - id: 367eda9b-0fe1-8014-b834-f04a86647e59
    title: Replication (데이터 복제)
excerpt: Replication (데이터 복제) --- 📖 Replication은 데이터의 복제를 의미한다. - Replication이 안되면, 장애 시 데이터의 유실이 많이 발생하게 된다. - Replication을 하더라도 100% 데이터가 보장되지 않을 수 있다. 어플케이션 서버, API 서버 같은 경우 보통 stateles
cover: null
icon: null
notionProperties:
  Point: 실습 파트 정리 필요
  상태: 완료
schema_version: 1
parent_id: 356eda9b-0fe1-8010-9561-c7098d310a4f
created: 2026-05-21T13:08:56.179Z
updated: 2026-05-25T22:35:50.193Z
legacy_path: Main/대규모 시스템 설계-d6a1706fbaf8/The RED- 대용량 서비스를 위한 아키텍처 with Redis (by 강대명)-c7098d310a4f/Replication (데이터 복제)-f04a86647e59/index.md
legacy_category: 대규모 시스템 설계
source_url: https://beautiful-college-c84.notion.site/367eda9b0fe18014b834f04a86647e59
---
<a id="367eda9b0fe1807bbd64dfb639b22ba6"></a>

## Replication (데이터 복제)

---

> 📖 
> 
> <a id="368eda9b0fe18047a978dd6e46475e69"></a>
> 
> Replication은 데이터의 복제를 의미한다&#46; 
> 
> - Replication이 안되면, 장애 시 데이터의 유실이 많이 발생하게 된다&#46; 
> 
> - Replication을 하더라도 100% 데이터가 보장되지 않을 수 있다&#46; 
> 
> <a id="368eda9b0fe18027995cd8189445ebef"></a>
> 
> 어플케이션 서버, API 서버 같은 경우 보통 stateless 이기 때문에 데이터의 백업이 필요없다&#46; 
> 
> - 데이터가 없더라도 그 시점에 연산을 해서 db에 있는 데이터를 가져와 처리한다&#46;
> 
> <a id="368eda9b0fe1807b952bdc6c41740a31"></a>
> 
> 그러나 실제 데이터 자체를 보관하고 있는 DBMS 같은 경우, 장애가 발생되면 모든 데이터가 사라지기 때문에 데이터에 대한 백업이 항상 필요하다&#46; 
> 
> <a id="368eda9b0fe1802c9025efbef9c136c1"></a>
> 
> 그 백업을 이용해 실시간으로 계속 서비스가 운영되어야 HA(High Availability)를 보장 수 있다&#46; 
> 
> <a id="368eda9b0fe18014a94cd8d331602491"></a>
> 
> ⇒ Primary 의 데이터를 Secondary 에서 복사해서 데이터의 Sync를 맞추는 작업
> 
> - primary 와 secondary가 같은 데이터를 가지고 있어야 한다 &#46;

<a id="368eda9b0fe18008b008f23eb442b8e0"></a>

## Replication

<a id="368eda9b0fe18000b861d0256593ba18"></a>

#### Replication(데이터 복제) 시 명령어를 보내는 것과 데이터를 보내는 것은 다르다&#46; 

- case 1 &#45; 데이터
    ![](45c58f92a082bb3b.webp)

    - 데이터의 경우, 이상없음

- case 2 &#45; 명령어 1
    ![](da600c5f55e567be.webp)

    - 명령어는 중간에 형식이 바뀔 수 있다&#46; 

- case 3 &#45; 명령어 2
    ![](0c7d4eb299a2db7c.webp)

    - 특히 시간의 경우, 위와 같이 날짜가 변경되어 기록되는 오류가 발생될 수 있다&#46; 

<a id="368eda9b0fe18033ad48caca422dafcd"></a>

### 장애 시 Failover (Active, StandBy 패턴)

> ✏️ 
> 
> <a id="368eda9b0fe180f8849bfacade66a621"></a>
> 
> <strong>Active, StandBy 패턴</strong>
> 
> - <code>Active</code>
>     - Primary는 읽기/쓰기(Read/Write)를 모두 담당한다&#46; 
> 
> - <code>StandBy</code>
>     - Secondary로 Primary의 데이터를 Replication 받다가, Primary의 장애 시에 Primary로 승격되어서 읽기/쓰기를 담당하게 된다&#46; 
> 
> ![](0e188bc1098f431c.gif)
> 
> - primary에서 장애가 발생되면 secondary가 primary로 승격되어 READ/WRITE(<code>READ</code> → <code>READ/WRITE</code>)를 작업을 수행한다&#46; 

<a id="367eda9b0fe180cc8c3bf2198c5d5180"></a>

#### &#91;주의&#93; failover 전 작업 (데이터 무결성 문제)

![](1be7eb75fae333a7.webp)

<a id="368eda9b0fe1807c824dc52eae89b721"></a>

<strong>Active, StandBy 패턴</strong>은 primary(Active)에서 secondary(StandBy)로  데이터를 복제(Replication) 한다&#46; 

<a id="369eda9b0fe180da954bc487efbd19a7"></a>

즉, <code>primary 데이터 쓰기</code> → <code>secondary 데이터 복제</code> 라는 동작 순서를 가진다&#46; 

<a id="369eda9b0fe1800b98c3e879e5abe23f"></a>

여기서 primary에 장애가 발생되는 경우 failover가 동작하여 secondary를 primary를 승격시키는데, 

<a id="369eda9b0fe1804c8d61ef5564e5c1c0"></a>

그전 secondary에서 <strong>장애 전까지 발생된 데이터를 정상 복제 처리해야 </strong> 데이터의 무결성이 깨지지 않고 동작할 수 있게 된다&#46;

- ex)
    - ON&#45;PREMIS&#58; MySQL &#45; MHA, MMM

    - AWS RDS에서는 자동으로 지원된다&#46;

    <a id="369eda9b0fe18018a0e2e8c91f210d8e"></a>

    이후 DNS, VIP 등의 방식으로 failover를 수행한다&#46; 

<a id="369eda9b0fe1808f944ce81102a30a8a"></a>

####  &#91;주의&#93; Secondary 개수

> ✏️ 
> 
> <a id="369eda9b0fe180f0826be1e46da42b72"></a>
> 
> 장비 장애 상황에서 복구 과정은 <strong><u><code>1) 리부팅</code></u></strong><strong><u> 을 통해 해결</u></strong>할 수 있는 상황 과 <strong><u>해당 장비가 망가져 </u></strong><strong><u><code>2) 새로운 장비</code></u></strong><strong><u> 들어와야 하는 상황</u></strong>이 있을 수 있다&#46;
> 
> ![](94eafb03b6a1dda1.webp)
> 
> <a id="369eda9b0fe1809fa992c6e9e1231356"></a>
> 
> 이때, 만약 <code>2) 새로운 장비</code> 상황의 경우, <strong>장애 복구된 뒤 </strong><strong><u>데이터 갭</u></strong><strong>이 발생</strong>된다&#46; 따라서 위와 같이 <strong><u>sync를 맞추는 작업</u></strong>, 즉 <strong>초기 데이터 복제</strong>가 필요하다&#46; 
> 
> <a id="369eda9b0fe180a68216eda150cb9168"></a>
> 
> 이를 <strong><u>효율적으로 동작</u></strong>시키기 위해서는 <strong>몇개의 secondary가 있어야 하는가?</strong>에 대해서  고려해야 한다&#46; 

<a id="369eda9b0fe180959604ffc1a405a0fc"></a>

#### &#91;오류&#93; Secondary&#58; <code>1대</code>

- 사례 &#45; mysql
    ![](498c4f912251a720.webp)

    <a id="369eda9b0fe180ee9e07d302be41eb8b"></a>

    새로운 장비를 들여와 초기 데이터를 복제하는 과정은 많은 부하가 발생되는 작업이다&#46; 

    <a id="369eda9b0fe180aa87b5f0b0a5e93296"></a>

    따라서 오히려 새로 복구된 primary 서버에서 다시 장애가 발생될 수 있다&#46; 

    - 초기 데이터가 많으면 많을 수록 primary 서버 부하(load)가 높아질 수 밖에 없다&#46; 

    - 디스크 I/O, 네트워크 I/O, CPU 등 많은 비용이 든다&#46; 

- 사례 &#45; redis
    ![](67169526793009c2.webp)

    <a id="369eda9b0fe18060b773c4cadcdbff94"></a>

    레디스는 좀더 심각한 부하가 발생된다&#46; 

    <a id="369eda9b0fe180ef988bfe72067b0e2c"></a>

    장애 발생 시 모든 데이터를 복제해야 하기 때문에 primary가 fork 작업을 진행하는데 이로 인해  redis의 메모리나 CPU 작용이 늘어나 문제를 일으킬 수 있다&#46;

    - 이러한 문제 개선을 위해 <code>P&#45;SYNC</code> 방식이 있지만, 아직 마스터가 바뀌면 동작하지 않는다&#46; 

    > 🤔 
    > 
    > <a id="369eda9b0fe1808abaf0fb0b7aa852d5"></a>
    > 
    > <code>Redis P&#45;SYNC(Partial Resynchronization, 부분 동기화)</code>
    > 
    > <a id="369eda9b0fe180878e29da2ba7d6e85c"></a>
    > 
    > 마스터(Master)와 복제본(Replica) 노드 간의 네트워크 연결이 일시적으로 끊겼을 때, 전체 데이터를 처음부터 다시 전송(Full Sync)하지 않고 <strong>끊긴 시점 이후의 변경 데이터만 찾아내어 부분적으로 동기화</strong><strong>하는 기술</strong>이다&#46;
    > 
    > <a id="369eda9b0fe1807daec2d57324dfde63"></a>
    > 
    > Redis <code>2&#46;8</code> 버전에서 처음 도입되었으며, 네트워크가 불안정한 환경에서 동기화 효율을 극대화하고 마스터 노드의 부하를 획기적으로 줄여준다&#46;

<a id="369eda9b0fe1800fbf49c8731868b365"></a>

#### &#91;권장&#93; Secondary&#58; <code>2대</code>

> 
> 
> <a id="369eda9b0fe180008a08f912ed92b054"></a>
> 
> 기본적으로 2대의 Secondary를 권장하지만 <strong><u>비용이 더 발생</u></strong>된다&#46; 
> 
> - 실무 온프레미스 환경에서는 대부분 2대의 secondary로 운영한다&#46;
>     - DB 같은 state를 관리하는 경우, 2대 사용을 권장
> 
> - AWS Aurora 같은 경우 내부적으로 자동으로 처리해준다&#46; <br>따라서 기본적으로 제공하는 멀티 AZ만 사용해도 큰 문제없다&#46;

- 더 장애를 유연하게 대처 가능
    ![](64d6d9f0e08dc93d.webp)

- 새로운 Secondary가 추가된 경우, <strong><u>다른 Secondary에서 데이터 복제</u></strong>를 하기 때문에 <strong>primary 서버에 부하를 주지 않고 더 안전하게 데이터 복사 처리</strong>할 수 있음
    ![](4085e3977325e144.webp)

    - secondary로 부터 초기 데이터 복구 작업이 완료된 후, primary로 부터 replication을 받는다&#46;

> ⚠️ 
> 
> <a id="369eda9b0fe180f8b0b2e6c49a016070"></a>
> 
> Redis는 secondary가 primary(Master)를 통해서만 확장되기 때문에 <strong><u>secondary를 통한 데이터 복사 위임</u></strong><strong>이 </strong><strong>불가능</strong>하다&#46;
> 
> ![](393a2bbe571d60d3.webp)

<a id="369eda9b0fe180efb031ea9dff838a2a"></a>

## 읽기 분배

> ✏️ 
> 
> <a id="369eda9b0fe18053b511c8030d74b30c"></a>
> 
> StandBy는 평소 백업용이고 서비스에서는 사용되지 않는다&#46; 
> 
> - StandBy 도 Active  와 같은 규모(성능)의 장비이다&#46;
>     - 장애 발생 시 Active 보다 성능이 떨어진다면 서비스 정상 운영이 어려울 수 있다&#46; 
> 
> - 따라서 실제 운영 비용이 최소 2배(primay 1, secondary 1) 이다&#46; 
>     - db 장비가 제일 비싼 장비를 사용하기 때문에 비용이 많이 든다&#46; 
> 
> - 그러나 Standby db 장비는 대부분 노는 것 같기 때문에 서비스의 성능을 올리기 위해서 primary에는 write, secondary에는 read를 처리하는 패턴을 많이 사용한다&#46; 

<a id="369eda9b0fe18084bd97e207bb5805f6"></a>

### 읽기 분배 &#45; Query Off

![](9d98a4b803b7c244.webp)

- write 를 primary에서 처리하고 secondary로 replication을 진행한다 &#46; 그리고 read 요청을 secondary에서 처리해 primary의 부하를 줄여 서비스의 성능을 향상시킨다&#46; 

- 일반적으로 Read 요청이 훨씬 많기 때문에 read 용 secondary 노드를 늘려서 서비스의 성능을 쉽게 향상시킬 수 있다&#46;

<a id="369eda9b0fe180879ad5c147350be2f9"></a>

### 읽기 분배 단점 &#45; Replication Lag

> ✏️ 
> 
> ![](2cdeeee002474fca.webp)
> 
> - Replication Lag 발생
>     - Primary 와 Secondary 의 데이터가 다르므로, 이미 쓰여진 데이터를 읽기 못할 수 있다&#46; 
>         - ex1) 내가 쓴 SNS의 글이 보이지 않는다&#46; → Not Bad
> 
>         - ex2) 내가 송금한 금액이 보이지 않는다&#46; → 🤬 <strong>Critical</strong>
> 
>     - 즉, 서비스에서 허용할 수 있는 경우와 허용할 수 없ㅅ는 경우가 존재한다&#46; 
> 
> - Replication Lag가 발생한 상황에서 데이터를 Cache하게 되면 문제가 오래 지속될 수 있다&#46; 
>     - write 시점에 cache를 먼저 해, 부하를 줄일 수 있는 방법 존재
>         <a id="369eda9b0fe180d3a300cdc8e36f2d6b"></a>
> 
>         이때, 캐시가 사라졌을 때 Replication Lag이 지속적으로 발생하면서 데이터의 깨짐 현상에 발생하거나 데이터가 누락되어 보일 수 있다&#46; 
> 
>     - 평소에는 미미하지만, 서비스 특성에 따라 굉장히 많은 차이를 보일 수 있다&#46; 
> 
>     - 따라서 <strong>모니터링 할 때 Replication Lag을 많이 지속적으로 체크</strong> 해야한다&#46; 
> 
>     - 빠른 디스크를 쓰는 것 보다 메모리를 증설하는게 조금 더 Replication Lag을 줄이는 좋은 방법이긴 하지만, 케이스마다 원인 및 해결책이 다르기 때문에 이를 고려해서 처리해야 한다&#46; 
> 
> - Query Off 에 의해 Replication Lag 발생이 심하다면 Secondary가 아닌 Primary에서 READ를 처리하도록 수정해야 한다&#46;

> 🤔 
> 
> <a id="369eda9b0fe18008aa1bd934e991ce40"></a>
> 
> <code>eventual consistency</code>
> 
> - 시간이 지나면 같아지지만 특정 시점에는 서로 다른 데이터를 가지는 특성을 지니는 데이터들을 의미한다&#46;

<a id="369eda9b0fe18018817dd766d4681113"></a>

<strong><u>계좌 정보와 같이 중요한 데이터</u></strong>들 즉, primary &#45; secondary 사이의 달라지면 안되는 데이터 무결성이 중요한 경우, 이러한 Query Off 구조를 사용하기 어렵다&#46; 

<a id="369eda9b0fe180cbb0cdcd0e2e92a287"></a>

→ <strong><u>무조건 Primary에서 read/write가 진행</u></strong>되어야 한다&#46;

<a id="369eda9b0fe1804582c9ca2321cb110c"></a>

대부분의 웹서비스의 경우 secondary에서 읽어도 큰 문제가 없기 때문에 <strong><u>Query Off를 사용</u></strong>하는 경우, <strong>사용 가능한 서비스인지 아닌지를  먼저 구분</strong>하는 것이 중요하다&#46; 

- 이커머스 &#45; 결제, 예약 … 등 1자리를 가지고 타겟팅하는 경우 사용하기 어려움

- SNS 댓글
    - 당장 다른 사람들에게 보이지 않아도 괜찮음

    - 시간이 지나면 결국 정상 처리됨

<a id="369eda9b0fe1803290bdf48b4c8aa7b6"></a>

## 실습

> AWS Aurora를 통해 replication이 되고 있는 서버에 장애가 발생했을 때 DNS 이용해 failover를 통해 고가용성을 확보한다&#46;

[the&#95;red/chapter&#95;2/replication at main · charsyam/the&#95;red]()

- write 인스턴스의 도메인 adress
    > ‣

    <a id="369eda9b0fe1802ba220c623c5ab62f3"></a>

    ```bash
    [log]
    path=sync.log

    [database]
    url=mysql+pymysql://the_red:the_red@database-1.cluster-cti5mc0i9dvk.ap-northeast-2.rds.amazonaws.com:3306/the_red
    ```
