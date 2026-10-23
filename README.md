# 콘텐츠 저장소

이 저장소는 글 원본과 첨부를 보관한다. 앱은 고정한 콘텐츠 커밋을 `content/` submodule로 읽는다.
2026-10-23에 아래 파일 배치와 SHA-256 예시를 정식 이관 파일과 대조했다.
현재 앱의 변경 범위는 submodule 연결과 기존 글 조회다. 새 편집·가져오기·게시 기능은 포함하지 않는다.

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

## 원본 조회와 검증

정식 Markdown의 frontmatter와 본문을 구분해 읽는다. 이미지가 근거라면 같은 폴더의 실제 파일도 확인한다.
원본 Markdown·첨부·ID·확장 메타데이터를 임의로 바꾸지 않는다.
현재 앱은 원본을 읽고 관계·첨부를 검증한 뒤 공개 출력을 생성한다.

앱 체크아웃에서 다음 명령을 실행한다.

```sh
npm run check:content
npm run build
```

기본 콘텐츠 root는 앱의 `content/`다. 앱 밖 staging은 로컬 검증에만 `CONTENT_ROOT`로 지정할 수 있다.
공통 파서와 파일명 규칙은 앱의 `src/shared/document.mjs`에 있다. 원본 읽기·검증은 `scripts/content.mjs`에 있다.
이관 함수는 `scripts/migrate-content.mjs`의 `migrateLegacyContent`다.
콘텐츠 커밋을 원격에 보관한 뒤 앱 gitlink를 갱신한다. 빌드는 기록한 커밋을 사용하며 원격 최신 브랜치를 추적하지 않는다.

## 작성·게시 기능의 현재 경계

기존 브라우저의 블록 글쓰기와 초안 저장은 별도 기능이다. 콘텐츠 submodule에 직접 게시하지 않는다.
이번에 추가한 본문 전용 Markdown 입력, 전체 문서·수정본 내보내기와 동반 첨부·백업 변경은 롤백한다.
`npm run import:md`는 기존 JSON 경로용 도구다. submodule 전환 뒤에는 쓰기를 중단한다.
`--content-root`, `--expected-revision`, `--dry-run`을 사용하는 정식 Markdown 게시 절차는 현재 지원하지 않는다.
새 작성·게시 계약은 별도 요청에서 다시 검토한다. 공통 파서의 전송 타입이 현재 편집기 지원을 뜻하지 않는다.

## 공개 경계

공개 Git 저장소에서는 frontmatter도 읽을 수 있다. 화면에서 숨긴 필드는 비공개 데이터가 아니다.
개인 메모와 로컬 LLM wiki는 앱과 콘텐츠 저장소 밖에 둔다.
게시 데이터는 허용 필드만 선택한다. 원시 YAML·AI 필드·확장 메타데이터를 공개 화면과 다운로드에 포함하지 않는다.
공개 다운로드는 게시 본문만 제공한다. 기존 편집기의 내보내기는 정식 원본 전체의 백업이나 게시 파일로 취급하지 않는다.

## 로컬 LLM wiki

색인과 wiki는 후속 계약이다. 이번 범위에는 색인 생성기·wiki 순회·AI 호출·벡터 검색이 없다.
원본을 읽는 에이전트는 [AGENTS.md](AGENTS.md)를 따른다.
`catalog.jsonl`, `source_ids`, `source_revisions`, `source_assets` 형식은 [CONTENT_SCHEMA.md](CONTENT_SCHEMA.md)에 정의한다.
후속 생성기가 교체할 파일은 앱 밖의 `catalog.jsonl`뿐이다.
개인의 `index.md`, `wiki/`, `log.md`, `AGENTS.md`는 자동으로 덮어쓰지 않는다.
