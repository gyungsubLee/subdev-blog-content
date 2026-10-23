---
order: 5
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8140-8c00-cc68f544eeea
title: "[Error] url 접속 시 발생되는 설정하지 않은 출력값 발생"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-8199-9d02-eeae5b4b5588
    title: 스프링 MVC 1편 -백엔드 웹 개발 핵심 기술
  - id: 1c3eda9b-0fe1-8140-8c00-cc68f544eeea
    title: "[Error] url 접속 시 발생되는 설정하지 않은 출력값 발생"
excerpt: 문제 --- 강의 코드를 따라하면서 학습하던 도중 이전에 발생되지 않았던 출력값 오류가 발생했다. 가정 --- 가정) 출력되는 내용은 위와 같은데 해당 내용이 아래의 Http ServletRequest - printHeaders() 와 유사하여 ‘해당 메서드가 어디서 잘못 실행되고 있나?’ 생각하여 다른 코드들을 뒤져보았
cover: ff1f0fbd226abd35.png
icon: null
notionProperties:
  Notes: 방향성에 대한 깨달음
  태그: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8199-9d02-eeae5b4b5588
created: 2025-03-27T07:50:55.492Z
updated: 2025-03-27T07:50:55.492Z
legacy_path: Main/Spring ( Java )-cd1f71740107/스프링 MVC 1편 -백엔드 웹 개발 핵심 기술-eeae5b4b5588/[Error] url 접속 시 발생되는 설정하지 않은 출력값 발생-cc68f544eeea/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181408c00cc68f544eeea
---
<a id="1c3eda9b0fe18123a7d1e7903cb50783"></a>

### 문제 

---

<a id="1c3eda9b0fe181289d04fdb35d79fd58"></a>

강의 코드를 따라하면서 학습하던 도중 이전에 발생되지 않았던 출력값 오류가 발생했다&#46; <br>

![](a9abbe0fff678aed.webp)

<a id="1c3eda9b0fe181c39e7ed74b94e21bd7"></a>

### 가정

---

<a id="1c3eda9b0fe181dfba8bc784e6c54829"></a>

<strong>가정)</strong> 출력되는 내용은 위와 같은데 해당 내용이 아래의 <code>Http ServletRequest </code>&#45; <code>printHeaders()</code> 와 유사하여  ‘해당 메서드가 어디서 잘못 실행되고 있나?’ 생각하여 다른 코드들을 뒤져보았다&#46; <br>

![](9a92071881d7787f.webp)

<a id="1c3eda9b0fe1810eb413c413f192a7f8"></a>

그러다가 <strong>서블릿을 통해 </strong><strong>매핑시킨 url에 접속 </strong>시에 <strong><u>그에 해당하는 메서드가 실행</u></strong>되는 것을 깨달았다&#46;

<a id="1c3eda9b0fe181978f9dd6bba1b859ea"></a>

강의를 들으면서도 몇번 들었던 내용인데도 전혀 생각을 하지 못했다&#46; 

![](629be536b415a402.webp)

<a id="1c3eda9b0fe181b2ae68c772c8420c96"></a>

따라서 <code>/</code>, <code>/hello</code>, <code>/request&#45;eader</code>, <code>/request&#45;param</code> 등 매핑한 모든 url에 접속하여 오류라 인지한 출력값이 기본적으로 출력되는 내용이라는 것을 확인할 수 있었다&#46; 

<a id="1c3eda9b0fe181eba3eec26aedd268f8"></a>

### 결론

---

<a id="1c3eda9b0fe181c5854bcb74690545a3"></a>

문제라고 인식한 내용을 가정을 통해 논리적으로 찾아갈 수 있는 경험이었다&#46; <br>결과적으론 큰 의미가 없는 작업이었지만, 문제를 해결과는 과정에 있어<strong> 논리적으로 접근하여 결론을 도출</strong>하는 중요하고 소중한 경험이었다&#46; 

> 문제 인식  → 가정 → 테스트 → 결과 도출

<a id="1c3eda9b0fe181f380a0ffa34ca97685"></a>

<br>또한 학습과 체화의 거리감을 인지할 수 있어 앞으로의 학습 방향에 대해 좀 더 심도있게 생각할 수 있게하는 굉장히 중요한 계기가 되었다&#46; 

> 학습과 기록 후 해당 내용을 머리에서 인지하고 생각할 수 있도록 체화시켜야 한다&#46;<br>→ 어떻게 체화 할 것인가?
