---
order: 44
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 22aeda9b-0fe1-8009-88cf-faa9489d2d9c
title: ESLint, Prettier [ 정리 필요 ]
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
    title: 탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )
  - id: 22aeda9b-0fe1-8009-88cf-faa9489d2d9c
    title: ESLint, Prettier [ 정리 필요 ]
excerpt: "목차 - 1. Server Action [Rules Reference - ESLint - Pluggable JavaScript Linter]() 1. Server Action --- 📖 VS ✏️ ESLint 플러그인을 설치한 후에도 정상 동작하지 않는다면 아래와 같이 .vscode/settings.json 생성 후, "
cover: fb3b1ee7da4a15e0.webp
icon: 9bed2eae1e079b4b.avif
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
created: 2025-07-08T08:44:53.027Z
updated: 2025-07-10T04:15:23.754Z
legacy_path: Main/Nest.js-c3a886768c4d/탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )-d4fc3e106054/ESLint, Prettier [ 정리 필요 ]-faa9489d2d9c/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/22aeda9b0fe1800988cffaa9489d2d9c
---
> 
> 
> <a id="22aeda9b0fe181b68807e1af3f3fe861"></a>
> 
> <strong>목차</strong>
> 
> - [1. Server Action](#22aeda9b0fe18144b7e8e859d5bae8ef)

[Rules Reference &#45; ESLint &#45; Pluggable JavaScript Linter]()

<a id="22aeda9b0fe18144b7e8e859d5bae8ef"></a>

## 1&#46; Server Action

---

> 📖 
> 
> <a id="22aeda9b0fe180ffbb06f3bb9d87b523"></a>
> 
> VS

> ✏️ 
> 
> <a id="22aeda9b0fe18076b87dc248bcae936e"></a>
> 
> ESLint 플러그인을 설치한 후에도 정상 동작하지 않는다면 <br>아래와 같이 <code>&#46;vscode/settings&#46;json</code> 생성 후, 설정 정의가 필요하다&#46;

![](f0a210a5abe6e4eb.webp)

![](be226c4903b6e377.webp)

<details>
<summary>설정 정보</summary>

<a id="22aeda9b0fe180ecab32d561c7f91eee"></a>

```javascript
{
	"git.ignoreLimitWarning": true,
	"eslint.codeAction.showDocumentation": {
		"enable": true
	},
	"eslint.alwaysShowStatus": true,
	"editor.formatOnSave": true,
	"editor.defaultFormatter": "esbenp.prettier-vscode",
	"editor.codeActionsOnSave": {
		"source.fixAll": true
	},
	
...
```

</details>

<a id="22aeda9b0fe180fe911eedf87c59966c"></a>

실무에서 ESLint 사용이 필수이다&#46;

<a id="22aeda9b0fe18084add0fd7451c23200"></a>

어떤 코드 컨벤션을 따라야 될지 정의를 하는 것이기 때문에 

> ✏️ 
> 
> <a id="22aeda9b0fe18071b8ecf6db3f4bb9bc"></a>
> 
> 기업마다 코드 컨벤션이 있다&#46; 그에 맞게 prettier 설정을 해
