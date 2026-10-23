---
order: 3
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 309eda9b-0fe1-8037-8eb0-e7aa1d2bac9c
title: glm-4.7 flash 실행
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 309eda9b-0fe1-800e-bce7-e83bc84702c5
    title: Model
  - id: 309eda9b-0fe1-8037-8eb0-e7aa1d2bac9c
    title: glm-4.7 flash 실행
excerpt: 1. Hugging Face 에서 모델 확인 --- - 모델 파일 다운로드 - ‣ 가장 유명한 최적화 팀인 Unsloth에서 만든 버전 버그 수정이 반영된 최신 버전이라 매우 안정적 bash ollama 다운 ollama run hf.co/unsloth/GLM-4.7-Flash-GGUF:Q4KM 2. 데이터셋 다운 ---
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 309eda9b-0fe1-800e-bce7-e83bc84702c5
created: 2026-02-16T14:15:00.509Z
updated: 2026-02-18T06:03:36.985Z
legacy_path: Main/Model-e83bc84702c5/glm-4.7 flash 실행-e7aa1d2bac9c/index.md
legacy_category: Model
source_url: https://beautiful-college-c84.notion.site/309eda9b0fe180378eb0e7aa1d2bac9c
---
<a id="309eda9b0fe180e4bfd6f4ccb230cb52"></a>

### 1&#46;  Hugging Face 에서 모델 확인

---

- <strong>모델 파일 다운로드</strong>
    - ‣
        > 가장 유명한 최적화 팀인 Unsloth에서 만든 버전<br>버그 수정이 반영된 최신 버전이라 매우 안정적

        <a id="309eda9b0fe18085b187c7f17d8fa30f"></a>

        ```bash
        # ollama 다운
        ollama run hf.co/unsloth/GLM-4.7-Flash-GGUF:Q4_K_M
        ```

<a id="309eda9b0fe18070a0d8dd225f744335"></a>

### 2&#46; 데이터셋 다운

---

[AI&#45;Hub]()

[AI&#45;Hub]()

<a id="309eda9b0fe180659a06f9acde1a1a8e"></a>

### M1 Pro 최적화 설정 팁

---

<a id="309eda9b0fe180c4b17cf1a713d19919"></a>

M1 Pro의 통합 메모리 성능을 극대화하려면 다음 설정 확인

- <strong>동시 실행 확인</strong>
    - <code>ollama ps</code> 명령어로 다른 모델이 메모리를 점유하고 있지 않은지 확인

- <strong>추론 속도 향상</strong>
    - 만약 속도가 느리다면, <code>Q4&#95;K&#95;M</code> 대신 더 가벼운 <code>Q3&#95;K&#95;L</code>이나 <code>Q2&#95;K</code> 양자화 파일을 사용하면 속도가 훨씬 빨라진다&#46;

    - 하지만 9B 모델은 M1 Pro에서 Q4 버전도 충분히 빠르다&#46;

<a id="309eda9b0fe180df9a1bfdcb22253147"></a>

<strong>지금 바로 </strong><strong><code>ollama run glm4&#58;9b</code></strong><strong>를 먼저 실행해 보시고, AI에게 &#34;너의 버전이 뭐야?&#34; 혹은 &#34;2025년 이후의 최신 기술에 대해 알아?&#34;라고 물어보세요&#46; 4&#46;7 버전이라면 최신 정보와 향상된 추론 능력을 보여줄 것입니다&#46;</strong>
