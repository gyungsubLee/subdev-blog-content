---
order: 4
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 28feda9b-0fe1-80c7-97e7-fafc104c89f8
title: "[ 이론 ] Joi"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 260eda9b-0fe1-801b-836b-c2e229a88ff9
    title: 한 번에 끝내는 NestJS 패키지 - Part 1. 기초
  - id: 27deda9b-0fe1-8071-8d19-d2363d6d91d0
    title: 유효성 검사 및 변환 ( Class Validator, Class Transformer )
  - id: 28feda9b-0fe1-80c7-97e7-fafc104c89f8
    title: "[ 이론 ] Joi"
excerpt: "목차 - Joi - 사용 방법 - 커스텀 에러 메세지 - 커스텀 Validator Joi --- 📖 Joi는 스키마(Schema) 기반 검증 라이브러리로 타입 세이프(Type Safe)하게 객체를 검증해 데이터 무결성을 유지한다. ❗ Joi 특성 - 풍부한 에러 메세지 커스터마이제이션 가능 - Extension을 통해 "
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 27deda9b-0fe1-8071-8d19-d2363d6d91d0
created: 2025-10-17T09:46:47.066Z
updated: 2025-10-17T10:13:06.518Z
legacy_path: Main/Nest.js-c3a886768c4d/한 번에 끝내는 NestJS 패키지 - Part 1. 기초-c2e229a88ff9/유효성 검사 및 변환 ( Class Validator, Class Transfor-d2363d6d91d0/[ 이론 ] Joi-fafc104c89f8/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/28feda9b0fe180c797e7fafc104c89f8
---
> 
> 
> <a id="28feda9b0fe1811e83e4c889861cb0d9"></a>
> 
> <strong>목차</strong>
> 
> - [Joi](#28feda9b0fe1810488d7de5b557de703)
> - [ 사용 방법](#28feda9b0fe181e69179de025feaa5e0)
> - [ 커스텀 에러 메세지](#28feda9b0fe18170b0d3c0f6378d7679)
> - [ 커스텀 Validator](#28feda9b0fe180f2b8d5cae52e00e59b)

<a id="28feda9b0fe1810488d7de5b557de703"></a>

## Joi

---

> 📖 
> 
> <a id="28feda9b0fe18101a4b0d1a70f15afff"></a>
> 
> <code>Joi</code>는 <strong>스키마(Schema) 기반</strong> 검증 라이브러리로 <strong><u>타입 세이프(Type Safe)</u></strong><strong><u>하게 객체를 검증</u></strong>해 <strong><u>데이터 무결성</u></strong><strong><u>을 유지</u></strong>한다&#46; 

> ❗ 
> 
> <a id="28feda9b0fe1816d94bee0637eb58fb6"></a>
> 
> Joi 특성
> 
> - 풍부한 에러 메세지 커스터마이제이션 가능
> 
> - Extension을 통해 얼마든지 새로운 검증 로직 추가 가능
> 
> - 환경변수 검증 시에 많이 사용됨 ( NestJS )

<a id="28feda9b0fe181e69179de025feaa5e0"></a>

###  사용 방법

> ✏️ 
> 
> - <code>Joi&#46;object({&#46;&#46;&#46;})</code>&#58; Joi 객체 초기화
> 
> - <code>&#46;string()</code>, <code>&#46;number()</code>… &#58; 타입 체크 (해당하는 타입이 아닐 시 오류 발생)
> 
> - <code>&#46;required()</code>&#58; 필수 값 설정 (값이 없을 시 오류 발생)
> 
> - <code>&#46;optional()</code>&#58; 옵션 값 설정

<a id="28feda9b0fe1801590bec90e767bd40a"></a>

```typescript
const schema = Joi.object({
	name: Joi.string().required(),
	email: Joi.string().email().required(),
	age: Joi.number().optional(),
});
```

<a id="28feda9b0fe180abb66bdd0ebe0d4012"></a>

```typescript
const data = {
	name: 'John',
	email: 'john@example.com'
}

const { error, value } = schema.validate(data);

if (error) {
	// 검증 실패, error 객체에 해당 정보가 담김
} else {
	// 검증 성공
}
```

<a id="28feda9b0fe18170b0d3c0f6378d7679"></a>

###  커스텀 에러 메세지

> ✏️ 
> 
> <a id="28feda9b0fe18045a5eee7568025691e"></a>
> 
> <code>&#46;message()</code> 후 해당하는 메세지 옵션을 넣으면 커스텀 메세지 설정이 가능하다&#46; 

<a id="28feda9b0fe1804cae22c0966a15673c"></a>

```typescript
const schema = Joi.object({
	name: Joi.string().required().messages({
		'string.empty': 'Name cannot be empty',
	}),
	email: Joi.string().email().required().messages({
		'string.email': 'Invalid email address',
	}),
});
```

<a id="28feda9b0fe180f2b8d5cae52e00e59b"></a>

###  커스텀 Validator

> ✏️ 
> 
> <a id="28feda9b0fe180c4aa29e4d263e61c7e"></a>
> 
> <code>Joi&#46;extend(&#46;&#46;&#46;)</code>를 사용해 검증 메서드를 추가할 수 있다&#46; 
> 
> - <strong>어떤 타입의 검증을 추가할지</strong>
> 
> - <strong>오류 메세지</strong>
> 
> - <strong>검증 룰</strong>

> ❗ 
> 
> <a id="28feda9b0fe180deb7b4ea5feeadb076"></a>
> 
> <strong>실제 사용할 일은 없다&#46;</strong>

<a id="28feda9b0fe18083b320c1715d441540"></a>

```typescript
const customJoi = Joi.extend((joi) => ({
		type: 'string',
		base: joi.string(),
		message: {
			'string.isCapitalized':
			'"{{#label}}"은 대문자로 시작해야합니다.',
		},
		rules: {
			isCapitalized: {
				validate(value, helpers) {
					is (value[0] !== value[0].toUpperCase()) {
						return helpers.error('string.isCapitalized');
					}
					return value;
				}
			},
		},
}));
```

- <code>Joi&#46;extend</code>를 통해 커스텀 Validator를 생성 가능하다&#46; 
    - type, base, message, rule 정의 필요

<a id="28feda9b0fe1801f8b7fc748311ed41a"></a>

```typescript
const schema = customJoi.object({
	name: customJoi.string().isCapitalized().required(),
	email: customJoi.string().email().required(),
});
```

- 기존 Joi 와 동일하게 체이닝 메서드를 통해 확장한다&#46;
