---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-804e-9041-e8fa06046f59
title: Trello 프로젝트 - 피드백 정리
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 165eda9b-0fe1-8012-bd01-cd9331c2dbdb
    title: 10.  Trello 프로젝트
  - id: 1c3eda9b-0fe1-804e-9041-e8fa06046f59
    title: Trello 프로젝트 - 피드백 정리
excerpt: 1. Config 패키진에 filter와 interceptor는 common 패키지가 더 적합해 보입니다. 1. TokenDeserializer에 baseUrl은 이미 중복으로 사용되고 있는 것만 보더라도 설정파일로 빼거나 상수처리하는게 좋겠습니다. 또한 if 안에서 return을 하는게 아니라 if 안에서 예외를 발생시
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 165eda9b-0fe1-8012-bd01-cd9331c2dbdb
created: 2025-03-27T03:37:28.315Z
updated: 2026-04-04T15:50:06.177Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/10.  Trello 프로젝트-cd9331c2dbdb/Trello 프로젝트 - 피드백 정리-e8fa06046f59/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1804e9041e8fa06046f59
---
1. Config 패키진에 filter와 interceptor는 common 패키지가 더 적합해 보입니다&#46;

1. TokenDeserializer에 <strong><u>baseUrl은 이미 중복으로 사용</u></strong>되고 있는 것만 보더라도 <strong><u>설정파일로 빼거나 상수처리</u></strong>하는게 좋겠습니다&#46; 또한 if 안에서 return을 하는게 아니라 <u>i</u><strong><u>f 안에서 예외를 발생시키고 if에 해당하지 않으면 최종 return</u></strong>하는게 더 좋은 코드겠습니다&#46;
    <a id="16eeda9b0fe18019bbacd9b71f2ebfc5"></a>

    ```java
    if (!url.startsWith(baseUrl)) {
    	throw new IllegalArgumentException("Invalid Slack webhook URL");
    }
    return url.substring(baseUrl.length()); // 포맷 변경
    ```

1. GlobalExceptionHandler에 getMapResponseEntity는 static 메소드가 아닌 일반 메소드여야겠죠&#46;

1. SessionUtils의 경우 filter나 interceptor에서 session을 가장 많이 다루고 있는데 활용되지 않고 있어요&#46; 위와 같은 코드 활용 불일치가 일어나면 불필요하거나 중복되는 코드가 소스코드 전반에 분포하게되어 유지보수하기 힘들어져요&#46; reloadSession &#45;&#62; reload, clearSession &#45;&#62; clear라고 작명해도 session을 리로드하고 초기화한다고 알 수 있겠어요&#46; checkAuthorization의 경우 user와 결합도가 생기는데 userService가 util를 활용하는 코드가 더 좋은 방법이겠습니다&#46;

1. 패키지 구조가 각 도메인마다 상이한 부분이 있는 듯합니다&#46; <br>어떤 패키지는 entity 패키지에 entity를 넣고 그렇지 않은 곳도 보입니다&#46; 규칙성이 필요해보입니다&#46;

1. User 도메인에서 Token entity를 관리하고 있는데 token의 종류는 무수한데 어떤 토큰 정보를 관리하는 entity인지 전혀 유추할 수 없습니다&#46; Access 용도인지, Slack 용도인지 어떤한 정보를 관리하는 객체인지구분할 필요가 있습니다&#46;
    - Token → SlackToken

1. Enum 상수를 지정하실 때 대소문자의 차이만으로 value를 추가하는건 무의미해보입니다&#46; 위와 같은 경우 항상 value를 직접 비교하여 찾아줘야하고 항상 대소문자를 변경해줘야합니다&#46; 무엇보다 상수는 대문자로 작성하는 것이 기본 규칙이 되겠습니다&#46;

1. <strong><u>파라미터 validation을 꼭&#33; 필수로 구현</u></strong>해주시기 바랍니다&#46;

1. WorkspaceUserRepository에 getWorkspaceOwnerdp 경우 where 조건에 id를 가장 먼저 조회하는 것이 가장 빠르게 조회할 수 있습니다&#46; <strong><u>Where 조건에 순서도 중요</u></strong>합니다&#46; indTokensByWorkspaceIdOrElseThrow은 동사 &#43; 명사로 작명해주시기 바랍니다&#46;
    <a id="1b3eda9b0fe1802abdc4e95dda68a0bf"></a>

    → <code>f</code> 생략됨

1. Notification에 경우 workspace에 종속되어 생성되는 데이터인데 해당 workspace에 공지를 읽었는지 누가 언제 읽었는지 isRead하는게 어떻게 가능할까요? 예상이 가지 않네요&#46;
    <a id="1b3eda9b0fe180e89313e98a9de22900"></a>

    → <br>NotificationServiceFacade에 경우<strong><u> evenMapperUtil을 통해 eventResult를 생성</u></strong>하는데 <strong><u>util 클래스에게 객체의 생성을 맡기는 것</u></strong>은 해당 클래스의<strong> </strong><strong><u>역할에 맞지 않는 설계 방법</u></strong>입니다&#46; <strong><u>util 클래스는 말그대로 구현의 편의를 위한 클래스</u></strong>이지 <strong><u>객체의 생명주기와 행동을 담당하는 클래스가 아닙니다</u></strong>&#46; 오히려 <strong><u>util 클래스의 난발은 객체지향 프로그래밍을 해체는 방식</u></strong>입니다&#46;<br>또한 애써 만들어 놓은 eventReuslt는 현재 notification과 그 역할을 차이가 전혀 없습니다&#46; 두 객체는 동일한 객체라고 볼 수도 있습니다&#46;<br>또한 <strong>알림 발송에 성공/실패했을 경우 </strong><strong><u>notification에 그 여부를 동기화</u></strong><strong> 해주어야지 </strong><strong><u>해당 공지가 발송되었는지 실패하였는지 추적할 수 있</u></strong>겠습니다&#46;

1. &#64;SessionAttribute 에는 SessionNames에 상수를 선언해두었기 때문에 사용하시면 좋겠네요&#46;

1. BoardResponseDto workspace&#95;id 는 카멜케이스로 해주세요&#46;

1. &#64;RestControllerAdvice 프로그램에 하나만 선언하여 사용하시기 바랍니다&#46; 종복 선언할 시 여러번 aop로 호출되고 중복 예외처리될 수 있습니다&#46;

1. 인가/권한 처리의 경우 filter와 interceptor에서 처리하는게 더 적합하겠습니다&#46;

1. File과 괄련된 경우 현재 패키지 계층 구조상으론 file 패키지로 옮기는게 적합하겠습니다&#46;

1. FileUtils 에 input, output stream에 자원 해제는 finally에 작성해 주시기 바라며 system&#46;out&#46;print는 사용하시면 안됩니다&#46;

1. cardService&#46;readAllCard()의 경우는 전체 카드를 조회 후 file과 cardUser를 여러번 호출해서 응답결과를 만들어주는 것이 아니라 sql을 작성하여 한번에 조회하는 코드를 만들어주시기 바랍니다&#46; 이때 entity로 sql 결과를 파싱하는게 아니라 dto로 바로 반환하면 더 좋겠죠&#46; 또한 card 전체를 조회하는 것은 데이터양에 따라 너무 많은 양의 데이터를 조회하는 것으로 적합하지 않을 것 같습니다&#46;

1. cardService&#46;updateCard의 경우에도 하나씩 데이터를 조회하는 것이 아니라 card와 cardUser를 조회해 와서 context에 등록하고 사용하거나 card에 관계를 통해서 구현해보시기 바랍니다&#46;

1. <strong><u>각 도메인 rest api url을 계층을 strict하게 정</u></strong>하셨는데<u> 상위 id가 필요치 않는 경우가 발</u>생하는게 보이셨을겁니다&#46; <strong><u>rest url을 설계할 때 너무 긴 혹은 너무 깊은 계층을 모두 표현하면 필요치 않은 값을 클라이언트에게 요구하게 되는 것이고 그만큼 클라이언트는 해당 값을 소유하고 유지해야하는 어려움을 겪게됩니다&#46; </u></strong>이 경험이 꼭 다음 프로젝트에 개선되었으면 좋겠네요&#46;

1. CommentService&#46;validateUserPermission은 작성되어 있지 않네요&#46; CommentService&#46;validateUserPermission&#46;getCurrentUser에 1L이 상수로 작성되어있는 이유는 무엇일까요? setter에 사용은 지양해주세요&#46;

1. ListsService에 아래와 같은 중복코드가 발생하고 있어요&#46; 메소드로 분리하여 작성해보세요&#46; 또한 유저 정보가 있는지 없는지는 인증/인가 단계에서 이미 확인이 된 거겠죠?
    <a id="16eeda9b0fe180978f82cb91187be6f2"></a>

    ```java
    User user = userRepository.findByEmail(email)
    .orElseThrow(() -> new RuntimeException("사용자를 찾을 수 없습니다"));

    Lists list = listsRepository.findById(listId)
    .orElseThrow(() -> new RuntimeException("리스트를 찾을 수 없습니다"));
    ```

<a id="16eeda9b0fe180479dcaf9722f00382f"></a>

<br>22&#46; SearchCardRepositoryCustomImpl&#46;getQueryDSLCardsByIdOrTitleOrderByCreatedAtDesc에 경우는 <strong><u>queryMethod 규칙에 맞출필요가 없</u></strong>기 때문에 <strong><u>너무 긴 메소드 네이밍을 고수할 필요가 없</u></strong>습니다&#46; 또한 q<u>ueryDsl임을 네이밍에 포함시킬 필요도 없</u>습니다&#46;<strong> </strong><strong>f</strong><strong><u>indCard(…)나 findCardByIdAndTilte(…) 정도만으로도 충분</u></strong>하겠습니다&#46;
