# 콘텐츠 문서 계약

정식 원본은 YAML frontmatter와 Markdown 본문으로 구성한다. 공개 출력과 편집 전송 파일은 정식 원본과 구분한다.
2026-10-23에 정식 이관 파일의 경로·전체 메타데이터·원문과 첨부 해시를 문서 예시와 대조했다.

## 파일과 식별자

콘텐츠 root에는 `categories.json`과 `posts/`를 둔다.
글은 `posts/<글 UUID>/<실제 제목>.md`에 보관한다. 같은 폴더에 본문 Markdown을 정확히 하나 둔다.
글 ID는 소문자·하이픈 UUID다. 기존 v4와 v8 UUID를 모두 허용한다.
부모와 카테고리를 바꿔도 UUID 폴더를 유지한다. 같은 제목도 ID가 다르면 별도 글이다.

파일명은 제목을 NFC로 정규화한 뒤 경로 금지 문자와 제어 문자를 `_`로 바꾼다.
끝의 점과 공백은 제거한다. Windows 예약 이름 앞에는 `_`를 붙인다.
확장자를 포함한 UTF-8 길이가 200바이트를 넘으면 코드 포인트 경계에서 줄인다.
빈 파일명은 `제목 없음.md`를 쓴다. 메타데이터의 원래 `title`은 바꾸지 않는다.
제목 변경은 같은 폴더에서 새 파일 저장을 확인한 뒤 이전 Markdown을 제거한다.

첨부 경로는 글 폴더 기준이다. `./파일명`은 형제 첨부를 가리킨다.
경로 이탈과 심볼릭 링크의 폴더 탈출을 거부한다. 누락 첨부와 다른 바이트의 파일명 충돌도 저장 전에 중단한다.
기존 공개 파일의 바이트를 사용한다. archive를 다시 변환하거나 원격 파일을 다시 내려받지 않는다.
이모지와 Notion `/icons/...` 아이콘은 기존 표현을 보존한다.
글 링크는 `#/post/<글 ID>`와 기존 블록 fragment를 사용한다.
게시 첨부는 `/content/assets/<글 ID>/<파일명>`으로 생성한다. 첨부 URL을 글 링크로 해석하지 않는다.

## 정식 YAML 스키마

다음은 형식을 설명하는 예시다. AI 필드는 기본값이며 실제 분석이나 검토 완료를 뜻하지 않는다.
전체 본문과 원래 확장 필드는 생략했다. 실제 저장에서는 생략한 값을 삭제하면 안 된다.

```yaml
schema_version: 1
id: "1dceda9b-0fe1-80d4-80ac-ee6d24a0638c"
title: "z-index 적용한됨"
parent_id: "1d4eda9b-0fe1-80a2-95f7-e975482b1dcd"
order: 5
kind: "article"
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
source_url: "https://beautiful-college-c84.notion.site/1dceda9b0fe180d480acee6d24a0638c"
review_status: "unreviewed"
created: "2025-04-21T02:48:47.208Z"
updated: "2025-04-21T06:22:27.987Z"
cover: null
icon: null
legacy_path: "Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/z-index 적용한됨-ee6d24a0638c/index.md"
legacy_category: "리액트"
notionProperties:
  Tags: "오류"
  상태: "완료"
```

실제 문서는 YAML 앞뒤를 `---`로 감싼다. 닫는 구분선 뒤에 원래 Markdown 본문을 둔다.
`category_id` 생략은 상속이다. 위 글의 실제 이관 `order`는 `5`다.

| 필드 | 타입·기본값 | 계약 |
|---|---|---|
| `schema_version` | 필수 정수 `1` | 다른 주 버전은 오류 |
| `id` | 필수 UUID 문자열 | 폴더 ID와 일치 |
| `title` | 필수 문자열 | 원래 제목 보존 |
| `parent_id` | 필수 UUID 또는 `null` | 루트는 `null`, 없는 부모·순환 금지 |
| `category_id` | 선택 문자열 | 유효한 카테고리 ID, 생략하면 조상 상속 |
| `order` | 0 이상 정수, 기본 `0` | 형제 동순위는 ID순 |
| `kind` | 기본 `article` | `article`, `troubleshooting`, `concept`, `reference`, `synthesis` |
| `summary` | 문자열, 기본 `""` | 주제·범위를 1-3문장으로 설명 |
| `tags` | 문자열 배열, 기본 `[]` | 본문에서 확인한 개념 |
| `aliases` | 문자열 배열, 기본 `[]` | 검색용 다른 표현 |
| `related_ids` | UUID 배열, 기본 `[]` | 의미 연결, 부모 관계와 구분 |
| `source_ids` | UUID 배열, 기본 `[]` | 작성 근거 문서 |
| `source_url` | 선택 HTTP·HTTPS URL | 원문의 공개 주소 |
| `review_status` | 기본 `unreviewed` | `unreviewed`, `reviewed`, `needs_review` |
| `created`, `updated` | 필수 ISO 날짜·시간 문자열 | 원래 날짜 보존, 실제 변경 때만 수정 |
| `cover`, `icon` | 선택 문자열 또는 `null` | 로컬 파일·공개 URL·기존 아이콘 표현 |
| `legacy_path` | 선택 문자열 | 이전 Markdown 경로의 별칭 |
| `legacy_category` | 선택 문자열 | 원래 분류, 공개 호환 값 선택에 사용 |

`notionProperties`, `breadcrumbs`, 원래 `excerpt`는 확장 필드로 보존한다.
`notionProperties`의 내부 키·공백·대소문자·빈 문자열을 바꾸지 않는다.
내부 `id`는 글 ID와 별개다. 관계처럼 보이는 문자열도 근거 없이 `parent_id`로 승격하지 않는다.
이미 대응한 원문 필드는 정식 필드로 옮긴다. 소비하지 않은 원문 필드는 원래 이름과 의미값을 유지한다.
원래 `excerpt` 보존과 공개 `excerpt` 생성은 별개다. 공개 미리보기는 frontmatter를 제거한 본문에서만 만든다.

알 수 없는 필드는 JSON 호환 의미값을 보존한다.
허용 값은 유한 숫자·문자열·불리언·null·배열·일반 객체다. 중첩 위치에서도 `__proto__`, `constructor`, `prototype` 키를 거부한다.
YAML 1.2 매핑을 사용한다. 중복 키·비문자열 키·사용자 태그·YAML 별칭을 거부한다.
주석과 YAML 줄바꿈 모양은 보존 대상이 아니다. 메타데이터 의미값과 원문 본문은 보존 대상이다.

첫 구분선 사이가 YAML 매핑이 아니면 일반 Markdown 구분선으로 보존한다.
메타데이터 키가 있는 잘못된 헤더는 오류로 중단한다. 오류 헤더를 본문에 노출하지 않는다.
알 수 없는 필드만 있는 유효한 YAML 헤더도 본문에서 분리한다.
정식 본문의 첫 H1은 추가하거나 제거하지 않는다. 기존 형식의 제목 처리는 호환 어댑터에 한정한다.
빈 요약과 빈 본문을 혼동하지 않는다. 속성을 가진 빈 본문 기록도 유효한 원문이다.

## 카테고리와 글 계층

`categories.json`은 다음 형식의 배열이다.

```json
[
  {"id":"group:frontend","name":"프론트엔드","parent_id":null,"order":0,"sources":[]},
  {"id":"source:리액트","name":"리액트","parent_id":"group:frontend","order":0,"sources":["리액트"]}
]
```

카테고리 ID는 이름을 바꿔도 유지한다. `sources`는 기존 분류 문자열과 브라우저 설정을 연결하는 호환 값이다.
글의 `parent_id`와 카테고리의 `parent_id`는 별도 계층이다. 각 계층의 중복 ID·없는 부모·순환을 검사한다.
카테고리 `sources` 중복도 오류다. 잘못된 명시 분류를 미분류로 숨기지 않는다.

글은 가장 가까운 조상의 명시 `category_id`를 상속한다. 직접 지정한 값은 부모 이동 뒤에도 유지한다.
상속할 값이 없으면 생성 데이터에서 `group:unclassified`로 표시한다. 기본 호환 값은 `미분류`다.
기존 `Main`은 `source:Main`을 직접 지정한다. 이 분류는 미분류 아래에 두고 `sources: ["Main"]`을 유지한다.
현재 corpus는 시작 글 39개와 Main에 직접 분류를 두고 나머지 글이 상속한다.
이관 `order`는 부모별 기존 배열 순서를 0부터 기록한다. 수정일 동률을 다시 정렬하지 않는다.

공개 `Post.category`는 현재 분류의 `sources`에 있는 `legacy_category`를 사용한다.
그 값이 없거나 유효하지 않으면 카테고리 ID를 호환 값으로 쓴다. `sources[0]`으로 원래 분류를 추측하지 않는다.
공개 카테고리의 `sources`에는 해당 ID도 포함한다. 화면 표시명은 `categoryId`로 정식 카테고리를 찾는다.
이름 변경과 상위 분류 묶기는 `categories.json`만 바꾼다.
카테고리 ID를 제거하는 병합은 해당 ID를 직접 지정한 글도 수정한다. 상속 자식과 폴더는 이동하지 않는다.
브라우저 v1·v2 개인 설정은 정식 원본을 덮어쓰지 않는다. 손상된 저장 값도 덮어쓰지 않는다.

## 전체 문서·수정본·기존 형식

파서는 `full`, `patch`, `legacy`를 구분한다. 각 모드의 `markdown`에는 frontmatter를 넣지 않는다.
전체 문서는 `{ metadata, markdown }`으로 다룬다. 수정본에는 필수 원본 필드나 AI 기본값을 채우지 않는다.
`document_mode`와 `base_revision`은 전송 전용이다. 정식 원본 메타데이터에는 저장하지 않는다.

- `full`: 스키마 1의 전체 문서다. 전체 편집본은 `document_mode: full`과 `base_revision`을 전송할 수 있다.
- `patch`: 정식 원본 전체를 읽지 않은 공개 편집이다. 제목·본문·명시적으로 바꾼 분류만 합친다.
- `legacy`: frontmatter 없는 Markdown 또는 스키마 없는 기존 내보내기다. 정식 저장 때 스키마 1로 정규화한다.

스키마 1의 `id`와 `source_id`가 다르면 오류다.
기존 내보내기는 유효한 `source_id`를 우선한다. 그 경우 `id`는 초안 별칭이다.
유효한 `source_id`가 없으면 유효한 `id`를 쓴다. 둘 다 없으면 정식 UUID를 한 번 만든다.
기존 `draft-UUID`는 브라우저 초안 키로 유지한다. 정식 문서 ID와 합치지 않는다.

`revision`은 게시 URL 변환 전 정식 Markdown 파일 바이트의 SHA-256이다.
해시는 소문자 16진수 64자다. 숨긴 메타데이터가 바뀌어도 revision은 바뀐다.
전체 원본을 처음 가져온 초안은 입력 파일 SHA-256을 기준 revision으로 보관한다.
이미 `base_revision`이 있는 전체 편집본은 그 값을 유지한다. 편집본 파일의 새 해시로 대체하지 않는다.

기존 ID는 전체 편집본도 기준 revision이 필요하다. 새 ID의 첫 저장에는 기준 revision을 요구하지 않는다.
기준 값 없는 전체 문서와 기존 형식은 diff 검토 뒤 `--expected-revision <SHA-256>`을 명시해야 기존 ID에 적용할 수 있다.
파일과 옵션의 기준 값이 다르면 중단한다. 수정일과 강제 옵션으로 검사를 우회하지 않는다.

다음 수정본은 검증한 원문 revision을 사용한다. 실제 수정본에는 이 헤더 뒤에 새 본문을 넣는다.

```yaml
schema_version: 1
document_mode: "patch"
id: "1dceda9b-0fe1-80d4-80ac-ee6d24a0638c"
base_revision: "fa5e55da565197ce394c41240594bcacce545bbbdf6de484fa494214dd7cddd7"
title: "z-index 적용한됨"
```

수정본에는 `schema_version`, `document_mode`, `id`, `base_revision`이 필요하다.
`title`은 제목을 바꾼 경우만 넣는다. 제목 생략은 기존 제목 유지다.
`category_id`는 분류를 바꾼 경우만 넣는다. 분류 생략은 기존 분류 유지다.
수정본 본문은 새 본문이며 원본의 부모·출처·확장 필드를 재구성하지 않는다.
로컬 가져오기는 ID로 원본을 찾고 현재 SHA-256과 기준 값을 비교한다.
원본이 없거나 기준 값이 다르면 쓰기 전에 중단한다.
일치하면 제목·본문·변경 분류만 합친다. 본문 변경은 `needs_review`와 새 수정일을 기록한다.
첨부 검증과 임시 저장에 성공한 뒤 원본을 교체한다. 게시 실패 시 기존 원본을 복구하며, 복구 실패 시 복구 파일을 보존한다.
`scripts/content.mjs`의 `writeContentDocument`는 저장 후 정리가 실패하면 반환값에 선택 필드 `cleanupWarnings`를 넣는다.
이 경고는 저장 완료 뒤 정리가 남았다는 뜻이다. 호출 CLI는 경고를 표시하며 저장을 재시도하지 않는다.
경고는 작업 반환값에만 둔다. 정식 메타데이터와 공개 DTO에는 넣지 않는다.
`scripts/import-markdown.mjs`는 결과 JSON을 표준 출력에 쓰고 경고를 표준 오류에 쓴다. 저장 호출은 한 번만 한다.

## 공개 데이터와 편집기

`scripts/prepare-site.mjs`는 원본을 검증한 뒤 공개 `posts/`, `index.json`, `categories.json`과 참조 첨부만 생성한다.

원본 `ContentDocument`는 전체 메타데이터와 본문을 가진다.
공개 `Post`는 다음 필드만 허용한다.

```json
["id","title","parentId","category","categoryId","createdAt","updatedAt","markdown","path","url","excerpt","cover","icon","order","revision","bodyLoaded"]
```

`draft`는 브라우저 초안 필드이며 정식 게시 출력에 넣지 않는다.
`summary`, `tags`, `aliases`, `related_ids`, `source_ids`, `review_status`, `legacy_path`, `legacy_category`와 확장 필드는 공개 출력에서 제외한다.
원시 frontmatter는 게시 본문·목록·미리보기·편집기 DOM·공개 다운로드에 포함하지 않는다.
제목과 본문에 사람이 쓴 같은 단어까지 지우지 않는다.
공개 미리보기는 본문에서만 만든다. 색인 본문 미리보기는 1,400자를 유지한다.
원본 Markdown·백업·블록 JSON·로컬 wiki는 공개 출력에 복사하지 않는다.
공개 Git의 frontmatter는 누구나 읽을 수 있다. 비공개 메모는 별도 로컬 경로에 둔다.

편집기는 보존 메타데이터를 별도 상태로 유지한다. 본문 입력에는 frontmatter를 넣지 않는다.
기존 글과 가져온 Markdown은 본문 전용 입력을 쓴다. 제목만 바꾸거나 내보내기만 하면 본문 바이트를 그대로 사용한다.
새 블록 글과 기존 블록 초안은 기존 BlockNote 흐름을 유지한다. 가져온 Markdown을 자동으로 블록으로 바꾸지 않는다.
전체 내보내기와 JSON 백업은 보존 메타데이터를 유지한다. 공개 화면의 Markdown 다운로드는 본문만 제공한다.
공개 데이터만 읽은 편집기는 숨긴 필드를 추측하지 않고 수정본을 내보낸다.

Markdown과 형제 첨부는 함께 선택할 수 있다. 브라우저는 선택하지 않은 로컬 파일을 읽지 않는다.
선택한 첨부의 이름과 바이트는 초안·JSON 백업에 보관한다. 미리보기 임시 URL은 원문과 백업에 저장하지 않는다.
이미지는 하나당 5MiB다. Markdown과 형제 첨부를 가져올 때는 선택한 파일의 `File.size` 합계를 10MiB 이하로 제한한다.
파일을 읽거나 초안을 바꾸기 전에 이 합계를 검사한다.

JSON 백업을 가져올 때는 현재 본문의 UTF-8 바이트와 디코딩한 첨부 바이트를 한 번씩 합산한다.
이 합계도 10MiB 이하다. JSON의 본문 사본과 base64 확장 바이트는 이 합계에 중복 계산하지 않는다.
본문과 첨부 합계가 10MiB 이하라면 JSON 파일 자체가 10MiB를 넘어도 가져올 수 있다.

JSON 백업 파일에는 별도의 160MiB 상한을 적용한다. `maxBackupContainerBytes`는 문서 예산 10MiB의 16배다.
가져오기는 파일을 읽고 파싱하기 전에 이 상한을 검사한다. 내보내기도 JSON의 UTF-8 바이트를 다운로드 전에 검사한다.
상한을 넘으면 가져오기와 내보내기를 중단한다. 가져오기가 실패하면 기존 초안을 바꾸지 않는다.
저장 용량이 부족하면 화면 입력을 유지하고 백업 내보내기를 제공한다. 누락 첨부 목록을 보여주고 본문을 지우지 않는다.
Markdown 단독 내보내기는 상대경로를 유지한다. 원래 형제 첨부 폴더에 저장해야 한다.
공개 URL만 있는 파일을 완전한 첨부 백업이라고 표시하지 않는다.
로컬 CLI는 `./파일명`을 입력 Markdown 옆에서 읽는다. 공개 `/content/assets/<ID>/...`도 해당 글의 로컬 첨부로 해석한다.

## 로컬 LLM wiki 계약

이 절은 후속 도구의 계약이다. 색인 생성기·변경 감지기·wiki 순회·AI 호출은 구현하지 않는다.
개인 wiki는 앱과 콘텐츠 저장소 밖에 둔다. 출력 경로가 앱·콘텐츠·`public`·`dist` 안으로 해석되면 거부한다.

```text
second-brain-local/
├── AGENTS.md
├── catalog.jsonl
├── index.md
├── wiki/<wiki UUID>/<개념 제목>.md
└── log.md
```

후속 생성기가 교체할 파일은 자신이 만든 `catalog.jsonl`뿐이다.
`index.md`, `wiki/`, `log.md`, 개인 `AGENTS.md`는 덮어쓰지 않는다.
절대 checkout root는 실행 환경에서 정한다. 공개 Git에는 절대경로를 고정하지 않는다.

`catalog.jsonl`은 UTF-8 JSON Lines 형식이다. 한 줄에 글 하나를 기록한다.
각 레코드는 `id`, `path`, `metadata`, `revision`을 포함한다.
`path`는 콘텐츠 root 기준 상대경로이며 `posts/`로 시작한다. 앱의 `content/` 접두어를 넣지 않는다.
로컬 도구는 확인한 절대 root와 상대 `path`를 조합해 원문을 연다. 해석 결과가 root 밖이면 거부한다.
`metadata`는 안전한 확장 필드를 포함한 전체 정식 메타데이터다. 공개 DTO나 요약 필드 일부로 대체하지 않는다.
`revision`은 해당 정식 Markdown 전체 바이트의 SHA-256이다.
첨부는 `path`의 부모 폴더에서 찾는다. 아래 `assets`는 확인한 전체 형제 첨부의 파일명을 보여주는 예시 확장 필드다.

아래 세 레코드는 2026-10-23 정식 이관 파일과 대조했다.
`metadata`는 `src/shared/document.mjs`의 `parseMarkdownDocument`가 읽은 전체 메타데이터다.
`revision`은 해당 파일 전체 바이트의 SHA-256이다. `order`는 순서대로 `26`, `0`, `5`다.
`assets`는 각 폴더의 형제 첨부 전체이며, 파일 존재와 바이트 해시를 확인했다.

```jsonl
{"id":"1c3eda9b-0fe1-819c-beab-c6a3a1072bb9","path":"posts/1c3eda9b-0fe1-819c-beab-c6a3a1072bb9/리액트.md","metadata":{"order":26,"kind":"article","summary":"","tags":[],"aliases":[],"related_ids":[],"source_ids":[],"review_status":"unreviewed","id":"1c3eda9b-0fe1-819c-beab-c6a3a1072bb9","title":"리액트","breadcrumbs":[{"id":"1c3eda9b-0fe1-8053-a02d-d27418c5a3fb","title":"Main"},{"id":"1c3eda9b-0fe1-819c-beab-c6a3a1072bb9","title":"리액트"}],"excerpt":"실무 중심! FE 입문자를 위한 React 리액트 스터디 ( 코알누 ) React + GSAP","cover":"35cde7f29524d65a.webp","icon":"32693c38df449e4a.webp","notionProperties":{},"schema_version":1,"parent_id":"1c3eda9b-0fe1-8053-a02d-d27418c5a3fb","created":"2025-03-27T07:47:12.301Z","updated":"2026-10-04T01:57:57.231Z","legacy_path":"Main/리액트-c6a3a1072bb9/index.md","legacy_category":"리액트","source_url":"https://beautiful-college-c84.notion.site/1c3eda9b0fe1819cbeabc6a3a1072bb9","category_id":"source:리액트"},"revision":"053f67d981238936cd71a40e1610d80eec071b515e0c37029ecfea6441bc0d69","assets":["32693c38df449e4a.webp","35cde7f29524d65a.webp"]}
{"id":"1d4eda9b-0fe1-80a2-95f7-e975482b1dcd","path":"posts/1d4eda9b-0fe1-80a2-95f7-e975482b1dcd/React + GSAP.md","metadata":{"order":0,"kind":"article","summary":"","tags":[],"aliases":[],"related_ids":[],"source_ids":[],"review_status":"unreviewed","id":"1d4eda9b-0fe1-80a2-95f7-e975482b1dcd","title":"React + GSAP","breadcrumbs":[{"id":"1c3eda9b-0fe1-8053-a02d-d27418c5a3fb","title":"Main"},{"id":"1c3eda9b-0fe1-819c-beab-c6a3a1072bb9","title":"리액트"},{"id":"1d4eda9b-0fe1-80a2-95f7-e975482b1dcd","title":"React + GSAP"}],"excerpt":"/icons/tagblue.svg [유데미] 실전 GSAP의 scrollTrigger를 활용한 웹사이트제작 - 기간 - HTML, CSS, JS: 25.04.13(일) ~ 25.04.23(수) - React, tailwind CSS: reference - ‣ - ‣ - ‣ - ‣ - ‣ - 페이지 - 페이지 - ‣ - ‣","cover":"ee7da0b7cbb72014.webp","icon":"ddc677e05c9e7c74.webp","notionProperties":{},"schema_version":1,"parent_id":"1c3eda9b-0fe1-819c-beab-c6a3a1072bb9","created":"2025-04-13T04:29:44.927Z","updated":"2025-04-23T05:44:05.070Z","legacy_path":"Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/index.md","legacy_category":"리액트","source_url":"https://beautiful-college-c84.notion.site/1d4eda9b0fe180a295f7e975482b1dcd"},"revision":"97e8c92b7ad46af4f21cc3f17075fc4a8855cd9ce24ffc21e0b533ccff3a5eb7","assets":["ddc677e05c9e7c74.webp","ee7da0b7cbb72014.webp"]}
{"id":"1dceda9b-0fe1-80d4-80ac-ee6d24a0638c","path":"posts/1dceda9b-0fe1-80d4-80ac-ee6d24a0638c/z-index 적용한됨.md","metadata":{"order":5,"kind":"article","summary":"","tags":[],"aliases":[],"related_ids":[],"source_ids":[],"review_status":"unreviewed","id":"1dceda9b-0fe1-80d4-80ac-ee6d24a0638c","title":"z-index 적용한됨","breadcrumbs":[{"id":"1c3eda9b-0fe1-8053-a02d-d27418c5a3fb","title":"Main"},{"id":"1c3eda9b-0fe1-819c-beab-c6a3a1072bb9","title":"리액트"},{"id":"1d4eda9b-0fe1-80a2-95f7-e975482b1dcd","title":"React + GSAP"},{"id":"1dceda9b-0fe1-80d4-80ac-ee6d24a0638c","title":"z-index 적용한됨"}],"excerpt":"문제 ❗ z-index를 사용하여 특정 DOM 뒤로 css css / footer / footer { position: relative; overflow: hidden; } footer .inner { height: 100vh; padding: 75px 75px 25px; box-sizing: border-box; dis","cover":null,"icon":null,"notionProperties":{"Tags":"오류","상태":"완료"},"schema_version":1,"parent_id":"1d4eda9b-0fe1-80a2-95f7-e975482b1dcd","created":"2025-04-21T02:48:47.208Z","updated":"2025-04-21T06:22:27.987Z","legacy_path":"Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/z-index 적용한됨-ee6d24a0638c/index.md","legacy_category":"리액트","source_url":"https://beautiful-college-c84.notion.site/1dceda9b0fe180d480acee6d24a0638c"},"revision":"fa5e55da565197ce394c41240594bcacce545bbbdf6de484fa494214dd7cddd7","assets":["19ed92dd13daa7ad.webp","2e517ee72bc3809a.webp"]}
```

첫 레코드의 `path`로 `리액트.md`를 연다. 같은 폴더의 `35cde7f29524d65a.webp`가 대표 첨부다.
나머지 두 레코드도 같은 방식으로 Markdown과 형제 첨부를 찾는다.
세 레코드의 `assets`에는 표지와 아이콘도 포함한다. 각 글은 형제 첨부 두 개를 가진다.

### wiki 근거와 변경 감지

다음 YAML은 앱 밖 wiki의 근거 기록 예시다. 정식 콘텐츠 원본으로 저장하는 예시가 아니다.
원문과 대표 첨부의 해시는 실제 파일 바이트에서 계산했다. 이미지 내용의 기술 검토나 wiki 작성은 실행하지 않았다.

```yaml
kind: "synthesis"
summary: ""
review_status: "unreviewed"
source_ids:
  - "1c3eda9b-0fe1-819c-beab-c6a3a1072bb9"
  - "1d4eda9b-0fe1-80a2-95f7-e975482b1dcd"
  - "1dceda9b-0fe1-80d4-80ac-ee6d24a0638c"
source_revisions:
  "1c3eda9b-0fe1-819c-beab-c6a3a1072bb9": "053f67d981238936cd71a40e1610d80eec071b515e0c37029ecfea6441bc0d69"
  "1d4eda9b-0fe1-80a2-95f7-e975482b1dcd": "97e8c92b7ad46af4f21cc3f17075fc4a8855cd9ce24ffc21e0b533ccff3a5eb7"
  "1dceda9b-0fe1-80d4-80ac-ee6d24a0638c": "fa5e55da565197ce394c41240594bcacce545bbbdf6de484fa494214dd7cddd7"
source_assets:
  "1c3eda9b-0fe1-819c-beab-c6a3a1072bb9":
    "35cde7f29524d65a.webp": "846d585c921e533cc95fe58b5347ae4598903c2da34ccf7a0ea9ca702803ba11"
  "1d4eda9b-0fe1-80a2-95f7-e975482b1dcd":
    "ee7da0b7cbb72014.webp": "e69f982b25e749c950155fd78068bdf10622f70c7a544002797bb0972b93dc6b"
  "1dceda9b-0fe1-80d4-80ac-ee6d24a0638c":
    "19ed92dd13daa7ad.webp": "891ed53ece57dce81b95c4b18336073618eee844c8b3ddafa7ffda15b4e93504"
    "2e517ee72bc3809a.webp": "d4a18893d727610c076b6f3402ef659a0badbb887d11885a61a2daaad0e3a71e"
```

`source_ids`는 실제 작성에 사용한 근거 문서 ID다.
`source_revisions`는 글 ID→SHA-256 매핑이며 근거 문서별 사용 당시 revision을 기록한다.
`source_assets`는 글 ID→형제 파일명→SHA-256 매핑이다. 첨부 바이트를 근거로 사용한 경우에 기록한다.
모든 해시는 소문자 16진수 64자다. 첨부만 바뀌면 Markdown revision이 같을 수 있으므로 두 해시를 구분한다.

후속 도구는 기록한 원문 revision이 달라지면 해당 wiki를 재검토 대상으로 보고한다.
근거 첨부의 해시 변경·누락도 따로 보고한다. 이를 원문 자동 교정이나 wiki 자동 덮어쓰기로 연결하지 않는다.
재검토 전에는 기존 근거 해시를 새 해시로 자동 교체하지 않는다.
에이전트는 바뀐 원문과 필요한 이미지를 읽고 이전 값·변경 값·근거·검토 상태를 diff로 남긴다.
메타데이터 보강과 본문 수정은 구분해 검토한다. 기술 주장은 근거 없이 사실로 확정하지 않는다.
사람이 검토한 뒤 `reviewed`를 기록한다. 근거 변경으로 재검토가 필요하면 `needs_review`를 사용한다.

빈 `summary`는 원문 부재가 아니다. 요약 없는 글은 빈 값과 `unreviewed`를 유지한다.
기존 빈 본문도 속성에 API 정보와 질문을 담을 수 있다. 에이전트는 원문 메타데이터를 함께 읽는다.
후속 도구는 원본을 읽을 뿐 자동으로 수정하지 않는다. 공개 빌드에는 색인과 개인 wiki를 포함하지 않는다.
