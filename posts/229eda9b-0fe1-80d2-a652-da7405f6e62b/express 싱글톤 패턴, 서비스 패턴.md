---
order: 50
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 229eda9b-0fe1-80d2-a652-da7405f6e62b
title: express 싱글톤 패턴, 서비스 패턴
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
    title: 탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )
  - id: 229eda9b-0fe1-80d2-a652-da7405f6e62b
    title: express 싱글톤 패턴, 서비스 패턴
excerpt: 제목 없음 목차 - Express 싱글톤 패턴, 서비스 패턴 - 1. 싱글톤 패턴 적용 - 2. 서비스 패턴 적용 [Singleton in TypeScript / Design Patterns]() Express 싱글톤 패턴, 서비스 패턴 --- 📖 Express에서 싱글톤 패턴과 서비스 패턴은 구조화된 백엔드 아키텍처를
cover: fb3b1ee7da4a15e0.webp
icon: 9bed2eae1e079b4b.avif
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
created: 2025-07-07T01:58:53.667Z
updated: 2025-07-09T15:26:06.036Z
legacy_path: Main/Nest.js-c3a886768c4d/탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )-d4fc3e106054/express 싱글톤 패턴, 서비스 패턴-da7405f6e62b/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/229eda9b0fe180d2a652da7405f6e62b
---
[제목 없음](#/post/229eda9b-0fe1-805d-833e-c59e9b0dd32c)

> 
> 
> <a id="229eda9b0fe180b5af20c3cb41da6cb3"></a>
> 
> <strong>목차</strong>
> 
> - [Express 싱글톤 패턴, 서비스 패턴](#229eda9b0fe180e28e54e36a9a3f5efe)
> - [1. 싱글톤 패턴 적용](#229eda9b0fe180819823f64810806c3f)
> - [2. 서비스 패턴 적용](#229eda9b0fe180b78745f0472e12a970)

[Singleton in TypeScript / Design Patterns]()

<a id="229eda9b0fe180e28e54e36a9a3f5efe"></a>

## Express 싱글톤 패턴, 서비스 패턴

---

> 📖 
> 
> <a id="229eda9b0fe180159006d2ee3620aa60"></a>
> 
> Express에서 <strong><code>싱글톤 패턴</code></strong>과 <strong><code>서비스 패턴</code></strong>은 <u>구</u><strong><u>조화된 백엔드 아키텍처를 구성</u></strong>할 때 자주 사용되는 디자인 패턴이다&#46;
> 
> <a id="229eda9b0fe1804999dad8fc01cd140d"></a>
> 
> 특히 NestJS 같은 프레임워크를 사용하지 않고도 유지보수성과 테스트 용이성을 확보하기 위해 활용된다&#46;

<a id="229eda9b0fe180819823f64810806c3f"></a>

### 1&#46; 싱글톤 패턴 적용

> ✏️ 
> 
> <a id="229eda9b0fe18047a519f5e008dc8c53"></a>
> 
> <code>싱글톤 패턴</code>은 <strong><u>애플리케이션 전체에서 단 하나의 인스턴스만 생성</u></strong><strong>되는 클래스/객체 패턴이다</strong>
> 
> <a id="229eda9b0fe180a282f1ec399a0bf4b5"></a>
> 
> 일반적으로 <strong><u>설정 객체, DB 커넥션, 로거, 캐시 등</u></strong>에 사용된다&#46;

<details>
<summary>ex 1) DB(<code>MongoDB</code>) 연결 객체 싱글톤 패턴 적용</summary>

> DB 커넥션을 한 번만 생성하고, 모든 요청에서 재사용함

<details>
<summary>&#91; 코드 &#93; db&#46;ts</summary>

<a id="229eda9b0fe1805ba8ccf77796a09b4c"></a>

```javascript
import { MongoClient } from "mongodb";

class Database {
  private static instance: MongoClient;

  private constructor() {} // 외부에서 new 방지

  static async getInstance() {
    if (!Database.instance) {
      Database.instance = new MongoClient("mongodb://localhost:27017");
      await Database.instance.connect();
    }
    return Database.instance;
  }
}

export default Database; 
```

</details>

<details>
<summary>&#91; 코드 &#93; app&#46;ts</summary>

<a id="229eda9b0fe1809793d2c1749ef29b2b"></a>

```javascript
import express from "express";
import Database from "./db";

const app = express();

app.get("/", async (req, res) => {
  const dbClient = await Database.getInstance(); // 항상 같은 인스턴스를 공유
  res.send("Hello with DB connection!");
});

app.listen(3000, () => console.log("Server is running"));
```

</details>

</details>

<details>
<summary>ex 2) 강의 코드</summary>

<details>
<summary><strong>&#91; 코드 &#93; </strong><code>app&#46;ts</code></summary>

<a id="229eda9b0fe180969854dc891a0e391c"></a>

```typescript
import express from "express";
import catRouter from "./cats/cats.route.js";

const port = 8000;

class Server {
	private static instance: Server;
  public app: express.Application;

  constructor() {
    this.app = express();
  }
  
  // 인스턴스 싱글톤으로 생성
  public static getInstance(): Sever {
	  if (!Server.instance) {
		  Server.instance = new Server();
	  }
	  return Server.instance;
  }

  private setRoute() {
    this.app.use(catRouter);
  }

  private setMiddleware() {
    //* logging middleware
    this.app.use((req, res, next) => {
      console.log(req.rawHeaders[1]);
      console.log("this is logging middleware");
      next();
    });

    //* json middleware
    this.app.use(express.json());

    this.setRoute();

    //* 404 middleware
    this.app.use((req, res, next) => {
      console.log("this is error middleware");
      res.send({ error: "404 not found" });
    });
  }

  public listen(port: number) {
    this.setMiddleware();
    this.app.listen(port, () => {
      console.log("Server is running on port", port);
    });
  }
}

function init() {
  const server = Server.getInstance(); // 🔄 항상 동일 인스턴스 반환
  server.listen(port);
}

init();

```

</details>

</details>

<a id="229eda9b0fe180b78745f0472e12a970"></a>

### 2&#46; 서비스 패턴 적용

> ✏️ 
> 
> <a id="229eda9b0fe1802da23afb410b87dbaa"></a>
> 
> <strong>비즈니스 로직을 라우터와 분리</strong>해서 모듈화하는 아키텍처이다&#46;
> 
> <a id="229eda9b0fe18078a6e7d2bc7ba79bd0"></a>
> 
> <code>라우터</code>는 <strong><u>요청&#45;응답만 담당</u></strong>하고, <code>서비스</code>는 <strong><u>데이터 처리나 도메인 로직을 담당</u></strong>한다&#46;

<details>
<summary>ex 1) 강의 코드</summary>

<details>
<summary>&#91; 코드 &#93; <code>cats&#46;route&#46;ts</code></summary>

<a id="229eda9b0fe180958948c48f5f3bd256"></a>

```typescript
import { Router } from 'express';
import { NextFunction } from 'express-serve-static-core';
import {
  createCat,
  deleteCat,
  readAllcat,
  readCat,
  updateCat,
  updatePartialCat,
} from './cats.service';

const router = Router();

router.get('/cats', readAllcat);
router.get('/cats/:id', readCat);
router.post('/cats', createCat);
router.put('/cats/:id', updateCat);
router.patch('/cats/:id', updatePartialCat);
router.delete('/cats/:id', deleteCat);

export default router;
```

</details>

<details>
<summary>&#91; 코드 &#93; <code>cats&#46;service&#46;ts</code></summary>

<a id="229eda9b0fe180eb9013d03e895f37d8"></a>

```typescript
import { Request, Response } from "express";
import { Cat, CatType } from "./cats.module.js";

export const createCat = (req: Request, res: Response) => {
  try {
    const data: CatType = req.body;
    Cat.push(data); // create
    res.status(201).send({
      success: true,
      data: { data },
    });
  } catch (error: any) {
    res.status(400).send({
      success: false,
      error: error.message,
    });
  }
};

export const readAllCats = (req: Request, res: Response) => {
  try {
    res.status(200).send({
      success: true,
      data: { Cat },
    });
  } catch (error: any) {
    res.status(400).send({
      success: false,
      error: error.message,
    });
  }
};

export const readCat = (req: Request, res: Response) => {
  try {
    const { id } = req.params;
    const cat: CatType | undefined = Cat.find((cat) => cat.id === id);

    if (!cat) {
      throw new Error("Cat not found");
    }

    res.status(200).send({
      success: true,
      data: { cat },
    });
  } catch (error: any) {
    res.status(400).send({
      success: false,
      error: error.message,
    });
  }
};

//* [PUT] 특정 고양이 데이터 수정
export const updateCat = (req: Request, res: Response) => {
  try {
    const { id } = req.params;
    const body: CatType = req.body;

    const index = Cat.findIndex((cat) => cat.id === id);
    if (index === -1) throw new Error("Cat not found");

    Cat[index] = body;
    const result = Cat[index];

    res.status(200).send({
      success: true,
      data: { result },
    });
  } catch (error: any) {
    res.status(400).send({
      success: false,
      error: error.message,
    });
  }
};

//* [PATCH] 특정 고양이 데이터 부분 수정
export const updatePartialCat = (req: Request, res: Response) => {
  try {
    const { id } = req.params;
    const body: Partial<CatType> = req.body;

    const index = Cat.findIndex((cat) => cat.id === id);
    if (index === -1) throw new Error("Cat not found");

    Cat[index] = { ...Cat[index], ...body };
    const result = Cat[index];

    res.status(200).send({
      success: true,
      data: {
        cat: { result },
      },
    });
  } catch (error: any) {
    res.status(400).send({
      success: false,
      error: error.message,
    });
  }
};

//* [DELETE] 특정 고양이 데이터 삭제
export const deleteCat = (req: Request, res: Response) => {
  try {
    const params = req.params;
    const newCat = Cat.filter((cat) => cat.id !== params.id);
    res.status(200).send({
      success: true,
      data: { newCat },
    });
  } catch (error: any) {
    res.status(400).send({
      success: false,
      error: error.message,
    });
  }
};

```

</details>

</details>
