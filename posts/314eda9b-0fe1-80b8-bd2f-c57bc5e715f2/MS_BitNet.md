---
order: 2
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 314eda9b-0fe1-80b8-bd2f-c57bc5e715f2
title: MS/BitNet
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 309eda9b-0fe1-800e-bce7-e83bc84702c5
    title: Model
  - id: 314eda9b-0fe1-80b8-bd2f-c57bc5e715f2
    title: MS/BitNet
excerpt: "[arxiv.org]() [microsoft/bitnet-b1.58-2B-4T · Hugging Face]() - 모델 다운로드 python hf download microsoft/bitnet-b1.58-2B-4T-gguf --local-dir models/bitnet python BitNet App git clone h"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 309eda9b-0fe1-800e-bce7-e83bc84702c5
created: 2026-02-27T22:49:08.030Z
updated: 2026-02-27T22:49:11.889Z
legacy_path: Main/Model-e83bc84702c5/MS-BitNet-c57bc5e715f2/index.md
legacy_category: Model
source_url: https://beautiful-college-c84.notion.site/314eda9b0fe180b8bd2fc57bc5e715f2
---
[arxiv&#46;org]()

[microsoft/bitnet&#45;b1&#46;58&#45;2B&#45;4T · Hugging Face]()

- 모델 다운로드

<a id="314eda9b0fe181d38068dfa64467e6a6"></a>

```python
hf download microsoft/bitnet-b1.58-2B-4T-gguf --local-dir models/bitnet
```

<a id="314eda9b0fe181f58125cab68dff0403"></a>

```python
# BitNet App
git clone https://github.com/microsoft/BitNet
cd BitNet
pip install -r requirements.txt

# 모델 다운로드 (Hugging Face) - microsoft/bitnet-b1.58-2B-4T
hf download microsoft/bitnet-b1.58-2B-4T-gguf --local-dir models/bitnet
```

<a id="314eda9b0fe18155a259d8f34fbb9692"></a>

```python
# 1. Python으로 커널 헤더 파일 생성
python utils/generate_lookup_table.py

# 또는 setup_env.py가 이 작업을 할 수도 있음
python setup_env.py

# 2. 생성된 파일 확인
ls include/bitnet-lut-kernels.h
```

<a id="314eda9b0fe181ebbe2be3d3a7e7a2b1"></a>

```python
# 1. 먼저 CMake로 빌드 설정
cmake -B build -S .

# 2. 컴파일
cmake --build build --config Release

# 또는 make 사용
cd build
make -j$(nproc)
cd ..
```

<a id="314eda9b0fe181f2b78ad66d77e53acf"></a>

```python
# bitnet.cpp로 실행
./build/bin/main -m models/bitnet-b1.58-2B-4T
```

<a id="314eda9b0fe18183b3c6de87558ab331"></a>

```python
python setup_env.py \ --model models/bitnet \ --quant i2_e
```
