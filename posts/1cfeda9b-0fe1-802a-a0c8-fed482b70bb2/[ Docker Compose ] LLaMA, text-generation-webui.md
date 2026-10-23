---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1cfeda9b-0fe1-802a-a0c8-fed482b70bb2
title: "[ Docker Compose ] LLaMA, text-generation-webui"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1cfeda9b-0fe1-808c-bfc1-c22724f5b32d
    title: Python
  - id: 1cfeda9b-0fe1-802a-a0c8-fed482b70bb2
    title: "[ Docker Compose ] LLaMA, text-generation-webui"
excerpt: 1. LLaMa 모델 및 라이센스 확인 ‣ Llama CLI 설치 bash pip install llama-stack 이미 설치되어 있는 경우 업데이트 pip install llama-stack -U 모델 목록 찾기 bash llama model list llama model list --show-all llama mod
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 1cfeda9b-0fe1-808c-bfc1-c22724f5b32d
created: 2025-04-08T15:41:18.332Z
updated: 2025-04-08T15:53:16.010Z
legacy_path: Main/Python-c22724f5b32d/[ Docker Compose ] LLaMA, text-generation-web-fed482b70bb2/index.md
legacy_category: Python
source_url: https://beautiful-college-c84.notion.site/1cfeda9b0fe1802aa0c8fed482b70bb2
---
<a id="1cfeda9b0fe18067a9e2c32938ad2501"></a>

### 1&#46; LLaMa 모델 및 라이센스 확인

> ‣

<a id="1cfeda9b0fe180f4bed0c84fe414972a"></a>

<strong>Llama CLI 설치</strong>

<a id="1cfeda9b0fe180a3a7a7eb1d3c446323"></a>

```bash
pip install llama-stack

# 이미 설치되어 있는 경우 업데이트
pip install llama-stack -U
```

<a id="1cfeda9b0fe180abaf9ce699fa42866d"></a>

<strong>모델 목록 찾기</strong>

<a id="1cfeda9b0fe180ab8609e9e43d980ddb"></a>

```bash
llama model list

llama model list --show-all

llama model download --source meta --model-id  MODEL_ID
```

<a id="1cfeda9b0fe18056b91fd989d5764dcd"></a>

<strong>사용자 정의 URL을 지정</strong>

<a id="1cfeda9b0fe180928621ff347239d279"></a>

```bash
https://llama3-2-lightweight.llamameta.net/*?Policy=eyJTdGF0ZW1lbnQiOlt7InVuaXF1ZV9oYXNoIjoidGlxb3Exa2FhMjMzeGp3dTBoaXhpcmhoIiwiUmVzb3VyY2UiOiJodHRwczpcL1wvbGxhbWEzLTItbGlnaHR3ZWlnaHQubGxhbWFtZXRhLm5ldFwvKiIsIkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTc0NDI5NjEwN319fV19&Signature=PQWhITWsq8au7e0LzdiOi4LT3bsqJY6epP82%7ENvE-fQUqB9nlzYOQkIMMtVVregkLmCXnf8yovYkoICd93wMv5xsD6UrZLpZJlyHz37znvq0tV8hddlWa6PNs0AQ%7ECMc3iMyDPDRfSKq4QjUPxv5dgZdfJ%7Eu5wNcgyt8%7ErnWQrm3IgYpvLIok99uQV1aqisc9lbAaGnq0cnyGuZukfR9tqGoRYz0YueAoKQofG7x9%7EaHtvZsavzdrVqwFQgNqLpH%7EV0ERSF4%7E258f-Bem2ftlprbdlb92mpCfL-AVymUTNZkocrhPFsJpT8%7ESBTS02fU4XZhOXV-6TUCs39iEejpOg__&Key-Pair-Id=K15QRJLYKIFSLZ&Download-Request-ID=1790022548224888
```

<a id="1cfeda9b0fe1803c8ca7e09d160fc6a1"></a>

### 2&#46; text&#45;generation&#45;webui

> ‣

<a id="1cfeda9b0fe180c1b8d5e2e2bf3d4889"></a>

LLaMA의 GPU 환경으로 제공

<a id="1cfeda9b0fe1809d8972ccd461713a5b"></a>

### 3&#46; Docker Compose

<a id="1cfeda9b0fe18094860edfac6d7e1456"></a>

<strong>LLaMA &#43; Text Generation Web UI (popular setup)</strong>

<a id="1cfeda9b0fe180c38cf6f68f922723eb"></a>

```bash
version: '3.8'

services:
  llama:
    image: ghcr.io/oobabooga/text-generation-webui:latest
    ports:
      - "7860:7860"
    volumes:
      - ./models:/app/models
    environment:
      - MODEL=llama
```

<a id="1cfeda9b0fe180099f41c16b51b642fc"></a>

모델 파일은 huggingface 또는 meta에서 받은 LLaMA 파일을 &#46;/models 폴더에 위치

<a id="1cfeda9b0fe180468e06ed5fdd6130f9"></a>

```bash
docker-compose up
```
