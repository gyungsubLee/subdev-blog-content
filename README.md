# 콘텐츠 저장소

이 저장소는 글 원본과 첨부를 보관한다. 앱은 고정한 콘텐츠 커밋을 `content/` submodule로 읽는다.
2026-10-23에 아래 파일 배치와 SHA-256 예시를 정식 이관 파일과 대조했다.

## 원본 배치

```text
README.md
AGENTS.md
CONTENT_SCHEMA.md
categories.json
posts/
├── 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9/
│   ├── 리액트.md
│   ├── 35cde7f29524d65a.webp
│   └── 32693c38df449e4a.webp
├── 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd/
│   ├── React + GSAP.md
│   ├── ee7da0b7cbb72014.webp
│   └── ddc677e05c9e7c74.webp
└── 1dceda9b-0fe1-80d4-80ac-ee6d24a0638c/
    ├── z-index 적용한됨.md
    ├── 19ed92dd13daa7ad.webp
    └── 2e517ee72bc3809a.webp
```

이 목록은 확인한 글 세 개의 실제 배치다. 각 폴더의 형제 첨부 두 개를 모두 표시했다.
글 폴더는 고정 UUID를 사용한다. 같은 폴더에 Markdown 하나와 형제 첨부를 둔다.
분류와 부모가 바뀌어도 폴더를 이동하지 않는다. 제목을 바꾸면 같은 폴더에서 Markdown 파일명만 바꾼다.
파일명 정규화와 필드 계약은 [CONTENT_SCHEMA.md](CONTENT_SCHEMA.md)에 있다.
기존 `#/post/<글 ID>` 주소와 블록 fragment를 유지한다.

## 작성 절차

1. 기존 글은 정식 Markdown과 필요한 형제 첨부를 함께 읽는다. `id`와 입력 파일의 SHA-256을 확인한다.
2. 새 글은 정식 UUID를 한 번 만든다. 반복 저장과 내보내기에서도 같은 ID를 사용한다.
3. 제목과 메타데이터는 본문과 구분해 수정한다. 본문을 수정하지 않았다면 첫 H1과 본문 바이트를 보존한다.
4. 첨부는 Markdown 옆에 두고 `./파일명`으로 참조한다. 새 글 링크는 `#/post/<글 ID>`를 사용한다.
5. 기존 ID를 갱신하면 기준 revision을 확인한다. 누락 첨부와 충돌이 있으면 저장을 중단한다.
6. 앱 체크아웃에서 `node scripts/content.mjs --check`로 원본을 검사한다. `node scripts/prepare-site.mjs`로 공개 출력을 만든다.
7. 변경 diff에서 본문·메타데이터·첨부를 검토한다. 콘텐츠 커밋을 먼저 원격에 보관한 뒤 앱 gitlink를 갱신한다.

웹 편집은 브라우저 초안과 파일 내보내기를 사용한다. 웹에서 Git 저장소로 직접 발행하지 않는다.
정식 문서 전체를 읽은 편집과 공개 화면에서 시작한 수정본은 서로 다른 계약을 사용한다.
기존 ID에는 전체 편집본도 기준 revision이 필요하다. 새 ID의 첫 저장에는 기준 revision을 요구하지 않는다.
공통 파서와 파일명 규칙은 앱의 `src/shared/document.mjs`에 있다. 원본 읽기·검증·저장은 `scripts/content.mjs`에 있다.
이관 함수는 `scripts/migrate-content.mjs`의 `migrateLegacyContent`다. 편집기는 `src/features/post-editor/useDraftEditor.ts`에서 문서 모드와 기준 revision을 보관한다.
저장 반환값에 `cleanupWarnings`가 있으면 CLI는 경고를 표시한다. 이 경고 때문에 저장을 재시도하지 않는다.
이 경고는 저장 뒤 정리가 남았다는 뜻이며, 메타데이터와 공개 DTO에 넣지 않는다.

## 로컬 가져오기

다음 명령은 앱 체크아웃에서 실행한다. `/path/to/content`는 사용할 콘텐츠 체크아웃으로 바꾼다.
`--dry-run`은 문서·revision·첨부·참조를 검사하며 원본을 쓰지 않는다.

```sh
npm run import:md -- "./export/article.md" --content-root /path/to/content --dry-run
```

검사 결과와 diff를 검토한 뒤 같은 명령에서 `--dry-run`을 빼고 저장한다.
기준 revision이 없는 기존 ID의 전체 편집본에는 `--expected-revision`을 넣는다.
다음 해시는 문서 예시의 `z-index 적용한됨` 원문 revision이다. 실제 작업에서는 편집을 시작한 원문의 해시를 사용한다.

```sh
npm run import:md -- "./export/z-index 적용한됨.md" --content-root /path/to/content --expected-revision fa5e55da565197ce394c41240594bcacce545bbbdf6de484fa494214dd7cddd7 --dry-run
```

수정본의 `base_revision`은 CLI가 읽는다. 옵션과 파일의 기준 값이 다르면 저장을 중단한다.
콘텐츠 root는 `--content-root`, `CONTENT_ROOT`, 앱의 `content/` 순서로 선택한다.
입력 Markdown은 하나만 지정한다. `./파일명` 첨부는 입력 옆에서 읽으며, 같은 글의 기존 첨부도 재사용한다.
누락 첨부와 다른 바이트의 파일명 충돌은 저장 전에 거부한다. 성공 결과는 ID·상대 파일명·revision을 담은 JSON이다.

## 공개 경계

공개 Git 저장소에서는 frontmatter도 읽을 수 있다. 화면에서 숨긴 필드는 비공개 데이터가 아니다.
개인 메모와 로컬 LLM wiki는 앱과 콘텐츠 저장소 밖에 둔다.
게시 데이터는 허용 필드만 선택한다. 원시 YAML·AI 필드·확장 메타데이터를 공개 화면과 다운로드에 포함하지 않는다.
공개 다운로드는 본문만 제공한다. 편집기 내보내기는 전체 문서 또는 수정본이며 용도가 다르다.

## 로컬 LLM wiki

색인과 wiki는 후속 계약이다. 이번 범위에는 색인 생성기·wiki 순회·AI 호출·벡터 검색이 없다.
원본을 읽는 에이전트는 [AGENTS.md](AGENTS.md)를 따른다.
`catalog.jsonl`, `source_ids`, `source_revisions`, `source_assets` 형식은 [CONTENT_SCHEMA.md](CONTENT_SCHEMA.md)에 정의한다.
후속 생성기가 교체할 파일은 앱 밖의 `catalog.jsonl`뿐이다.
개인의 `index.md`, `wiki/`, `log.md`, `AGENTS.md`는 자동으로 덮어쓰지 않는다.
