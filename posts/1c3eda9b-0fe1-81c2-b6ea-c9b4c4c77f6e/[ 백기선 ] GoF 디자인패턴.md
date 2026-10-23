---
order: 2
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81c2-b6ea-c9b4c4c77f6e
title: "[ 백기선 ] GoF 디자인패턴"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8188-9ddf-e42c6289f47d
    title: 디자인패턴
  - id: 1c3eda9b-0fe1-81c2-b6ea-c9b4c4c77f6e
    title: "[ 백기선 ] GoF 디자인패턴"
excerpt: ✏️ ‣ 1. 싱글톤 패턴 2. 팩토리 메서드 패턴 3. 추상 팩토리 패턴 4. 빌더 패턴 5. 프로토타입 패턴 6. 어댑터 패턴 7. 브릿지 패턴 8. 컴포짓 패턴 9. 데코레이터 패턴 10. 퍼사드 패턴 11. 플라이웨이트 패턴 12. 프록시 패턴 13. 책임 연쇄 패턴 14. 커맨드 패턴 15. 인터프리터 패턴 16
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 1c3eda9b-0fe1-8188-9ddf-e42c6289f47d
created: 2025-03-27T07:47:12.298Z
updated: 2026-01-23T14:26:37.999Z
legacy_path: Main/디자인패턴-e42c6289f47d/[ 백기선 ] GoF 디자인패턴-c9b4c4c77f6e/index.md
legacy_category: 디자인패턴
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181c2b6eac9b4c4c77f6e
---
> ✏️ 
> 
> <a id="1c3eda9b0fe181a1a274dc7437f24d69"></a>
> 
> ‣

[1. 싱글톤 패턴](#/post/1c3eda9b-0fe1-815d-9f98-c943ffb02293)

[2. 팩토리 메서드 패턴](#/post/1c3eda9b-0fe1-8151-b738-c4484e341ba3)

[3. 추상 팩토리 패턴](#/post/1c3eda9b-0fe1-8197-bcad-cef9e1fc22fa)

[4. 빌더 패턴](#/post/1c3eda9b-0fe1-8133-b416-d228fed10301)

[5. 프로토타입 패턴](#/post/1c3eda9b-0fe1-8187-a1e2-d189efaac209)

[6. 어댑터 패턴](#/post/1c3eda9b-0fe1-81ec-b8a3-df145d2a62d3)

[7. 브릿지 패턴](#/post/1c3eda9b-0fe1-81c6-a517-df47762c9879)

[8. 컴포짓 패턴](#/post/1c3eda9b-0fe1-811c-ba3e-da5c00e44d86)

[9. 데코레이터 패턴](#/post/1c3eda9b-0fe1-8111-b43a-d4d6e133b9be)

[10. 퍼사드 패턴](#/post/1c3eda9b-0fe1-81a2-90eb-f595d42ea695)

[11. 플라이웨이트 패턴](#/post/1c3eda9b-0fe1-81e7-a376-f38fa535a545)

[12. 프록시 패턴](#/post/1c3eda9b-0fe1-8113-8acd-edf688f2426d)

[13. 책임 연쇄 패턴](#/post/1c3eda9b-0fe1-81c3-a969-f75a75b9b3a3)

[14. 커맨드 패턴](#/post/1c3eda9b-0fe1-81ba-a0be-e3c5a004ccd5)

[15. 인터프리터 패턴](#/post/1c3eda9b-0fe1-8119-a1fb-dbc69090f188)

[16. 이터레이터 패턴](#/post/1c3eda9b-0fe1-816d-978d-ebb48559f569)

[17. 중재자 패턴](#/post/1c3eda9b-0fe1-81c3-a2ed-f3349b1279a8)

[18. 메멘토 패턴](#/post/1c3eda9b-0fe1-8101-b098-dbc77ad329c0)

[19. 옵저버 패턴](#/post/1c3eda9b-0fe1-81d3-aee4-fc8f6ca57c65)

[20. 상태 패턴](#/post/1c3eda9b-0fe1-81d9-9fb5-f2de9702f586)

[21. 전략 패턴](#/post/1c3eda9b-0fe1-81ca-9f82-d83bfe68e477)

[22. 템플릿 메서드 패턴](#/post/1c3eda9b-0fe1-81ef-b87b-daddd7fd3dfc)

[23. 비지터 패턴](#/post/1c3eda9b-0fe1-8100-a749-efcbef4bc551)

[빈 컨테이너 구현](#/post/1c4eda9b-0fe1-8016-a2af-ec0b89bfb95f)

[UriComponentsBuilder 직접 구현](#/post/1c4eda9b-0fe1-807a-8983-e8c44fb07f19)

[@Builder 직접 구현](#/post/1c4eda9b-0fe1-8036-b18c-de70dccb39f0)

[디자인 패턴과 OOP 특징의 관계](#/post/1c3eda9b-0fe1-8108-909d-ea3578308e36)

[팩토리 매소드 패턴 vs 추상 팩토리 패턴](#/post/1c3eda9b-0fe1-8194-838b-f9236b0b8a9b)

[바이트 코드 확인](#/post/1c3eda9b-0fe1-81c1-83e9-ff9f63beb97c)

[enum](#/post/1c3eda9b-0fe1-8160-ae51-dee6bd3ec082)
