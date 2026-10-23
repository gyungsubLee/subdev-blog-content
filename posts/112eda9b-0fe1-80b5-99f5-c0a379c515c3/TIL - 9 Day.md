---
order: 49
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 112eda9b-0fe1-80b5-99f5-c0a379c515c3
title: TIL - 9 Day
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 10aeda9b-0fe1-8045-a8c4-f10918253453
    title: TIL
  - id: 112eda9b-0fe1-80b5-99f5-c0a379c515c3
    title: TIL - 9 Day
excerpt: 💡 PDS 다이어리 참조 PlAN --- - [x] firebase Doc를 보며 Update, delete 로직 구현 및 테스트 - [ ] 기능:[ open API(naver) -프록시 서버 ] - 리펙토링 필요 - cors-anywhere.herokuapp.com 사용 시, 해당 홈페이지에 들어가 demo sever
cover: null
icon: null
notionProperties:
  날짜: 2024-10-02
  Category: TIL
  Keyword: • firebase - CRUD
schema_version: 1
parent_id: 10aeda9b-0fe1-8045-a8c4-f10918253453
created: 2024-10-01T23:54:41.184Z
updated: 2024-10-18T04:52:44.035Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/TIL-f10918253453/TIL - 9 Day-c0a379c515c3/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/112eda9b0fe180b599f5c0a379c515c3
---
> 💡 
> 
> <a id="112eda9b0fe1815ba329c6fe33697614"></a>
> 
> PDS 다이어리 참조

<a id="112eda9b0fe181769dcaefa3ce827f8d"></a>

### PlAN 

---

- [x] firebase Doc를 보며 Update, delete 로직 구현 및 테스트 

- [ ] <del> 기능&#58;&#91; open API(naver)  &#45;프록시 서버 &#93; &#45; 리펙토링 필요 </del>
    -  <strong><a href="http://cors-anywhere.herokuapp.com">cors&#45;anywhere&#46;herokuapp&#46;com</a></strong><strong> 사용 시, <br>해당 홈페이지에 들어가 demo sever에 들어가 access 권한을 요청해야 한다&#46;</strong>
        - → 자동화 or 다른 프록시 서버로 교체 

- [ ] <del>스프링 MVC &#45; 동시 요청&#95; 멀티 쓰레드 학습  </del>

<a id="112eda9b0fe181f98c5beac84cdf619b"></a>

### DO ( 오늘 공부한 내용)

---

<a id="112eda9b0fe181a1a735e6314ff9dc16"></a>

## <a href="https://firebase.google.com/docs/firestore/manage-data/add-data?hl=ko&#38;_gl=1*1qo7urn*_up*MQ..*_ga*MTg2ODkxNTU5My4xNzI3ODI2MTg3*_ga_CW55HF8NVT*MTcyNzgyNjE4Ni4xLjAuMTcyNzgyNjE4Ni4wLjAuMA..#web_8">firebase/Cloud Firestore</a>

<details>
<summary>DB ( Firestore ) 구조</summary>

- 계층적 구조 
    > <code>컬렉션</code> &#45;  <code>문서(식별자, 즉 id 로 쓰임)</code> &#45; <code>데이터</code> 

    ![](e90155f4c981b2ca.webp)

</details>

<details>
<summary>Cloud Firestore 초기화</summary>

<details>
<summary>firebaseConfig 확인 </summary>

> 내가 만든 프로젝트 → 프로젝트 개요 → 프로젝트 설정  &#45; SDK 설정 구성

![](d56cbad97cb21adf.webp)

![](1b37d1624494cbd4.webp)

</details>

<a id="112eda9b0fe18008befef5fe76007246"></a>

```javascript
import { initializeApp } from "firebase/app";
import { getFirestore } from "firebase/firestore";


const firebaseConfig = {
    // config 복사 
};

// 초기화
const app = initializeApp(firebaseConfig);
// db 연동
const db = getFirestore(app);
```

</details>

<details>
<summary>사용 가능한 데이터 유형</summary>

<a id="099c7ece76024a69a5e8d0d7011baa5c"></a>

<code>문자열</code>, <code>불리언</code>, <code>숫자</code>, <code>날짜</code>, <code>null</code>, <code>중첩 데이터(배열 or 객체)</code> 등

> 거의 모든 데이터 타입이 사용 가능한 것 같다&#46; 

- ex)
    <a id="267d7b7bdd5543efbdfbf2400235a790"></a>

    ```javascript
    import { doc, setDoc, Timestamp } from "firebase/firestore"; 

    const docData = {
        stringExample: "Hello world!",
        booleanExample: true,
        numberExample: 3.14159265,
        dateExample: Timestamp.fromDate(new Date("December 10, 1815")),
        arrayExample: [5, true, "hello"],
        nullExample: null,
        objectExample: {
            a: 5,
            b: {
                nested: "foo"
            }
        }
    };
    await setDoc(doc(db, "data", "one"), docData);
    ```

</details>

<a id="113eda9b0fe18086b46ec7c157dd5049"></a>

## CRUD

<details>
<summary>테스트 템플릿</summary>

<details>
<summary>Title</summary>

<details>
<summary>전체 코드 </summary>

<a id="f398e1e81d094cfcb22f48bcb267b6a9"></a>

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1, shrink-to-fit=no"
    />
    <title>firebase Test</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.4/jquery.min.js"></script>
    <script type="module">
      // Firebase SDK 라이브러리 가져오기
      import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-app.js";
      import { getFirestore } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";
      import {
        collection,
        addDoc,
        getDocs,
        updateDoc,
        deleteDoc,
      } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";

      const firebaseConfig = {
	        // config
      };

      // Firebase 인스턴스 초기화
      const app = initializeApp(firebaseConfig);
      const db = getFirestore(app);

      

      
    </script>
  </head>

  <body>
    <button id="create-doc">이벤트 트리거</button>
  </body>
</html>

```

</details>

---

<details>
<summary>firebase 연동을 위한 초기 설정</summary>

<a id="702564fa22684086866a6bbc034166e0"></a>

```java
<script type="module">
    // Firebase SDK 라이브러리 가져오기
    import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-app.js";
    import { getFirestore } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";
    import {
	    doc,
      collection,
      addDoc,
      getDocs,
      getDoc,
      updateDoc,
      deleteDoc,
    } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";

    const firebaseConfig = {
	     // config 설정 
	  };

    // Firebase 인스턴스 초기화
    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);
    
    
</script>
```

</details>

<details>
<summary>crud 함수 </summary>



</details>

<details>
<summary>이벤트 트리거 </summary>

<a id="2b80d69a5f14409392c1d73ac9ac4b11"></a>

```java
 // script (JS)
 $("#create-doc").click(() => readDocuments());
 
 
 // HTML
 <button id="create-doc">이벤트 트리거</button>
```

</details>

<details>
<summary>결과 확인</summary>



</details>

</details>

</details>

<details>
<summary>전체 코드</summary>

<a id="113eda9b0fe1806bb478d23f02d93ba6"></a>

```javascript
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1, shrink-to-fit=no"
    />
    <title>firebase Test</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.4/jquery.min.js"></script>
    <script type="module">
      // Firebase SDK 라이브러리 가져오기
      import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-app.js";
      import { getFirestore } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";
      import {
        doc,
        collection,
        addDoc,
        getDocs,
        getDoc,
        updateDoc,
        deleteDoc,
      } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";

      const firebaseConfig = {
        apiKey: "AIzaSyDivBgHhoAzbxgRBvCGlfGKy1rgVLK8IuY",
        authDomain: "sparta-12281.firebaseapp.com",
        projectId: "sparta-12281",
        storageBucket: "sparta-12281.appspot.com",
        messagingSenderId: "497101658964",
        appId: "1:497101658964:web:c57a76520033977b3bc6c1",
      };

      // Firebase 인스턴스 초기화
      const app = initializeApp(firebaseConfig);
      const db = getFirestore(app);

      // 문서 생성
      async function createDocument() {
        try {
          // 생성 확인을 위한 더미 데이터
          const data = {
            name: "Los Angeles",
            state: "CA",
            country: "USA",
          };

          // 문서 저장
          const docRef = await addDoc(collection(db, "cities"), data);

          // 저장된 문서 id 값 확인
          console.log("Document written with ID: ", docRef.id);
        } catch (e) {
          // 저장 오류 메세지
          console.error("Error adding document: ", e);
        }
      }

      // 전체 문서(컬랙션) 조회
      async function getDocuments() {
        const getDocuments = await getDocs(collection(db, "cities"));
        getDocuments.forEach((doc) => {
          console.log(`${doc.id} => ${doc.data()}`);
        });
      }

      // 특정 문서 조회
      async function getDocument() {
        // 문서명 ( 테스트 확인을 위한 예시 문서명, DB에서 가져옴)
        const id = "4RBKRXVNg8QJ95KZd4OH";

        // 특정 문서 참조
        const docRef = doc(db, "cities", id);
        // 특정 문서 조회
        const docSnap = await getDoc(docRef);

        if (docSnap.exists()) {
          console.log("문서 정보: ", docSnap.data());
        } else {
          console.log("해당하는 문서가 존재하지 않습니다.");
        }
      }

      // 문서 업데이트
      async function updateDocument() {
        const id = "4RBKRXVNg8QJ95KZd4OH";

        /**
          cities = {
             country: string,
             name: string,
             state: string,
          }
        */
        const updateData = {
          name: "업데이트 테스트2",
        };

        const docRef = doc(db, "cities", id);
        await updateDoc(docRef, updateData);
      }

      async function deleteDocument() {
        const id = "5yXAAHjajcPnprSa1Eit";

        const collectionName = "cities";
        const docRef = doc(db, collectionName, id);

        // 문서 참조 생성
        console.log(`문서 참조 생성 성공: ${docRef.path}`);

        // 문서 존재 여부 확인
        const docSnapshot = await getDoc(docRef);
        if (!docSnapshot.exists()) {
          console.error("문서가 존재하지 않습니다.");
          return; // 문서가 존재하지 않으면 함수 종료
        }

        // 문서 삭제
        await deleteDoc();
      }

      // 이벤트 트리거
      $("#create-doc").click(() => deleteDocument());
    </script>
  </head>

  <body>
    <button id="create-doc">이벤트 트리거</button>
  </body>
</html>

```

</details>

<details>
<summary>API 불러오기</summary>

<a id="113eda9b0fe18005bebbcd12ac5f43b2"></a>

```javascript
// npm
import { doc, collection, addDoc, getDocs, getDoc, updateDoc, deletDoc  } from "firebase/firestore";


// 모듈 <script type="module">.  ( 버전 수정 필요 )
import { doc, collection, addDoc, getDocs, getDoc, updateDoc } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";

```

</details>

<details>
<summary>🧐 <strong><u>참조값 생성</u></strong> 후, <strong><u>CRUD(생성, 조회, 업데이트, 삭제)</u></strong> 진행</summary>

<a id="113eda9b0fe180799d79e6cb058765c6"></a>

Firestore는 <strong><u>문서와 컬렉션의 구조가 </u></strong><strong><u>계층적</u></strong>으로 되어 있기 때문에 <strong>특정 문서를 </strong><strong><u>명확하게 지정</u></strong>하기위해 <strong><u>참조값 생성</u></strong> 후, CRUD를 진행한다&#46; 

<details>
<summary>장점</summary>

- <strong>명확한 위치 지정</strong>

- 확장성
    - 다른 컬렉션이나 하위 컬렉션을 참조하거나 특정 경로에서 데이터를 가져오는 작업이 명확해짐

- 지연로딩(Lazy Loading)
    - 참조는 데이터 자체를 즉시 가져오지 않고 위치만 가르킨다&#46;

    - 즉, 필요할 때 getDoc()으로 데이터 불러온다

</details>

</details>

<a id="8af8fd6536ef4056ae4e0d9f4ec7eff4"></a>

### <strong>C</strong>reate(문서 생성)&#58; <code>setDoc()</code>, <code>addDoc()</code>

<details>
<summary><code>setDoc()</code>&#58; 문서명(id 값) 직접 생성</summary>

<a id="113eda9b0fe18027abb2dc232bef592a"></a>

```javascript
setDoc(doc(db, 생성할 컬렉션명, 생성할 문서명), 생성할 데이터))
```

<details>
<summary>ex)</summary>

<a id="4cdde7b9ca474a26b2b1dc4dd87b93a7"></a>

```javascript
import { doc, setDoc } from "firebase/firestore"; 
// import { doc, getDocs } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";

const data = {
  name: "Los Angeles",
  state: "CA",
  country: "USA"
};

// id 값(문서명) 직접 지정
await setDoc(doc(db, "cities", "new-doc-id"), data);
```

</details>

</details>

<details>
<summary><code>addDoc()</code>&#58; 문서명(id 값) 자동 생성 </summary>

<details>
<summary>🧐 <code>id</code>&#58; 랜덤한 문자열 값을 생성함</summary>

![](bad7bfe2aef368e6.webp)

</details>

<a id="7ab99de5fa4a4841bcb4f22f187dc474"></a>

```javascript
// firestore DB 연동  =>  자세한 내용은 위의 'Cloud Firestore' 초기화 참조
const db = getFirestore(app);

const docRef = await addDoc(collection(db, 생성할 컬렉션 명), 생성할 객체 데이터);
```

- firebase DB(<strong>Cloud Firestore)</strong> &#45; 생성된 데이터 확인 
    ![](75e14000ff1e6a0f.webp)

<details>
<summary>ex1) <code>addDoc()</code>  ( Dos 발췌 )</summary>

<a id="03a5eb43d3a0411d995d3215b9db2eb4"></a>

```javascript
import { collection, addDoc } from "firebase/firestore"; 


const docRef = await addDoc(collection(db, "cities"), {
  name: "Tokyo",
  country: "Japan"
});
console.log("Document written with ID: ", docRef.id);
```

</details>

<details>
<summary>ex2) <code>addDoc()</code> (스파르타 &#45; 웹 종합반 강의 참조)</summary>

<details>
<summary>Post 생성 뷰</summary>

<details>
<summary>닫기 &#45; toggle()</summary>

<a id="aa70497927314479aeb7ba588edd44bc"></a>

```javascript
// 포스트 생성 창 토글
$("#savebtn").click(async function () {
  $("#postingbox").toggle();
});
```

</details>

![](c883277231b09dbf.webp)

<a id="a3389d89627241fa9d75ab16cd4f3803"></a>

```html
<div class="mypostingbox" id="postingbox">
  <div class="form-floating mb-3">
    <input
      type="email"
      class="form-control"
      id="image"
      placeholder="name@example.com"
    />
    <label for="floatingInput">앨범 이미지</label>
  </div>
  <div class="form-floating mb-3">
    <input
      type="email"
      class="form-control"
      id="title"
      placeholder="name@example.com"
    />
    <label for="floatingInput">앨범 제목</label>
  </div>
  <div class="form-floating">
    <input
      type="email"
      class="form-control"
      id="content"
      placeholder="name@example.com"
    />
    <label for="floatingTextarea">앨범 내용</label>
  </div>
  <div class="form-floating mb-3">
    <input
      type="email"
      class="form-control"
      id="date"
      placeholder="name@example.com"
    />
    <label for="floatingInput">앨범 날짜</label>
  </div>
  <div class="mybtn">
    <button id="postingbtn" type="button" class="btn btn-dark">
      기록하기
    </button>
    <button type="button" class="btn btn-outline-dark">닫기</button>
  </div>
</div>
```

</details>

<a id="112eda9b0fe18132b642eb7eb4dce896"></a>

```javascript
import { getDocs } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";


 $("#postingbtn").click(async function () {

		// 사용자로부터 받아온 데이터
    let image = $("#image").val();
    let title = $("#title").val();
    let content = $("#content").val();
    let date = $("#date").val();
		
		// 추가할 데이터 객체 
    let doc = {
      image: image,
      title: title,
      content: content,
      date: date,
    };
		
		// DB(fireStore) - 저장(Create)
    await addDoc(collection(db, "albums"), doc);

    alert("저장완료!");
    window.location.reload();
});

```

</details>

</details>

---

<details>
<summary>문서 생성 테스트</summary>

<details>
<summary>전체 코드 </summary>

<a id="113eda9b0fe180919d68e793d400a4b0"></a>

```java
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1, shrink-to-fit=no"
    />
    <title>firebase Test</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.4/jquery.min.js"></script>
    <script type="module">
      // Firebase SDK 라이브러리 가져오기
      import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-app.js";
      import { getFirestore } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";
      import {
        collection,
        addDoc,
      } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";

      const firebaseConfig = {
      
        // config 설정  ( DOS - 프로젝트 설정 확인 ) 	 
           
      };

      // Firebase 인스턴스 초기화
      const app = initializeApp(firebaseConfig);
      const db = getFirestore(app);

      // 문서 생성
      async function createDocument() {
        try {
          // 생성 확인을 위한 더미 데이터
          const data = {
            name: "Los Angeles",
            state: "CA",
            country: "USA",
          };

          // 문서 저장
          const docRef = await addDoc(collection(db, "cities"), data);

          // 저장된 문서 id 값 확인
          console.log("Document written with ID: ", docRef.id);
        } catch (e) {
          // 저장 오류 메세지
          console.error("Error adding document: ", e);
        }
      }
			
			// 문서 저장을 위한 이벤트 트리거
      $("#create-doc").click(() => createDocument());
      
    </script>
  </head>

  <body>
    <button id="create-doc">문서 생성 테스트</button>
  </body>
</html>

```

</details>

---

<details>
<summary>firebase 연동을 위한 초기 설정</summary>

<a id="113eda9b0fe180d08881db4d471e2e04"></a>

```java
<script type="module">
    // Firebase SDK 라이브러리 가져오기
    import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-app.js";
    import { getFirestore } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";
    import {
      collection,
      addDoc,
    } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";

    const firebaseConfig = {
	     // config 설정 
	  };

    // Firebase 인스턴스 초기화
    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);
    
    
</script>
```

</details>

<details>
<summary>문서 생성(저장)&#58; <code>createDocument()</code></summary>

<a id="113eda9b0fe18066adfada5764d1c8c8"></a>

```java
// 문서 생성
async function createDocument() {
  try {
    // 생성 확인을 위한 더미 데이터
    const data = {
      name: "Los Angeles",
      state: "CA",
      country: "USA",
    };

    // 문서 저장
    const docRef = await addDoc(collection(db, "cities"), data);

    // 저장된 문서 id 값 확인
    console.log("Document written with ID: ", docRef.id);
  } catch (e) {
    // 저장 오류 메세지
    console.error("Error adding document: ", e);
  }
}
```

</details>

<details>
<summary>문서 저장 이벤트 설정</summary>

<a id="113eda9b0fe1808095a7ff7cacfd84be"></a>

```java
 // script (JS)
 $("#create-doc").click(() => createDocument());
 
 
 // HTML
 <button id="create-doc">이벤트 트리거</button>
```

</details>

<details>
<summary>아래와 같이 정상적으로 저장되는 것을 확인</summary>

![](936d60f13890971a.webp)

![](dc176281efd08556.webp)

</details>

</details>

<a id="1cf6d1495501480c982831efab80a3ef"></a>

### <strong>R</strong>ead(문서 조회)&#58; <code>getDocs()</code>, <code>getDoc()</code> 

<details>
<summary>🧐 굳이 참조값을 생성(<code>colletion</code>, <code>doc</code>) 후  다시 조회(<code>getDoc()</code>)를 하는 이유는?</summary>

<a id="6f79e168f8fe4a3eaebae3ff08598ba7"></a>

Firestore는 <strong><u>문서와 컬렉션의 구조가 </u></strong><strong><u>계층적</u></strong>으로 되어 있기 때문에 <strong>특정 문서를 </strong><strong><u>명확하게 지정</u></strong>하기위해 <strong><u>참조값을 사용</u></strong>한다&#46;

<details>
<summary>1) 컬랙션 조회 </summary>

<details>
<summary>1&#46; 컬렉션 참조값 생성</summary>

- 참조값 생성&#58; <code>collection(db, 컬렉션 명)</code> 

- ex) 생성되는 참조값&#58; <code>“cities&#34;</code>
    <a id="60f03b5ae3414e0aa913518fbc327fd4"></a>

    ```javascript
    const collectionRef = collection(db, "cities");  // “cities" 
    ```

</details>

<details>
<summary>2&#46; 컬렉션 조회</summary>

- 컬렉션 조회&#58;  <code>getDocs(참조값)</code>

- ex)
    <a id="be51e4da363d477eb853322e3f0fde7d"></a>

    ```javascript
    const querySnapshot = await getDocs(collectionRef); 
    ```

</details>

</details>

<details>
<summary>2) 문서 조회</summary>

<details>
<summary>1&#46; 먼저 문서에 대한 참조를 생성</summary>

- 참조&#58; <code>컬렉션/문서명</code>

- ex) <code>cities/LA</code>
    <a id="add7f5edb82f4205898cdd12c22ece09"></a>

    ```javascript
    doc(db, "cities", "LA");
    ```

</details>

<details>
<summary>2&#46; 참조값을 통해 해당하는 문서의 데이터 가져옴  </summary>

<a id="df1f722f14c142338c782b8fab358822"></a>

```javascript
await getDoc(참조값)
```

<details>
<summary>ex) </summary>

<a id="035f74686c3c476880a86487459a2a09"></a>

```javascript
const docSnap = await getDoc(docRef); 
```

</details>

</details>

</details>

<details>
<summary>장점</summary>

- <strong>명확한 위치 지정</strong>

- 확장성
    - 다른 컬렉션이나 하위 컬렉션을 참조하거나 특정 경로에서 데이터를 가져오는 작업이 명확해짐

- 지연로딩(Lazy Loading)
    - 참조는 데이터 자체를 즉시 가져오지 않고 위치만 가르킨다&#46;

    - 즉, 필요할 때 getDoc()으로 데이터 불러온다

</details>

</details>

<details>
<summary><strong><u>전체 데이터(컬렉션)</u></strong> 조회&#58; <code>getDocs(컬렉션 참조값)</code></summary>

<a id="113eda9b0fe1807cb21cc4c4f7e561d7"></a>

```javascript
// 컬렉션(전체 문서) 참조값 생성
const colletionRef = collection(db, 컬렉션명

// 컬렉션(전체 문서) 조회
const colletionSnap getDocs(colletionRef)
```

<details>
<summary>ex) <code>getDocs()</code> (스파르타 &#45; 웹 종합반 강의 참조)</summary>

- 해당하는 컬렉션 전체 조회 
    <a id="312cc6e5ce0b40d58eb36eefa3cfec9d"></a>

    ```javascript
    let docs = await getDocs(collection(db, "albums"))
    ```

    <details>
    <summary>조회한 데이터로 포스트 뷰 생성</summary>

    ![](25f31d753c38e034.webp)

    <a id="1b8f632dee814996938f0277b4cfdc0f"></a>

    ```javascript
    import { getDocs } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";

    // config, 인스턴스 초기화

    let docs = await getDocs(collection(db, "albums"))

    docs.forEach((doc) => {
    	  let row = doc.data();
    	
    	  let image = row["image"];
    	  let title = row["title"];
    	  let content = row["content"];
    	  let date = row["date"];
    	
    	  let temp_html = `
    	      <div class="col">
    	          <div class="card h-100">
    	              <img src="${image}"
    	                  class="card-img-top" alt="...">
    	              <div class="card-body">
    	                  <h5 class="card-title">${title}</h5>
    	                  <p class="card-text">${content}</p>
    	              </div>
    	              <div class="card-footer">
    	                  <small class="text-muted">${date}</small>
    	              </div>
    	          </div>
    	      </div>`;
    	  });
    	  
    	  // 생성된 카드 아래의 html에 추가 
    	  $("#card").append(temp_html);
    });
    ```

    <a id="113eda9b0fe1807fbebdeb7dd11913e8"></a>

    ```html
    <body>
    	 .  .  .

    	<div class="mycards">
          <!-- 포스팅 내용들 -->
          <div id="card" class="row row-cols-1 row-cols-md-4 g-4"></div>
      </div>
    </body>
    ```

    </details>

</details>

</details>

<details>
<summary><strong><u>특정 </u></strong><strong><u>데이터(문서)</u></strong> 조회&#58; <code>getDos(문서 참조값)</code></summary>

<a id="113eda9b0fe180559c08ed8212b9850e"></a>

```java
// 참조값 생성
const docRef = doc(db, 컬랙션명, 문서명(id));

// 데이터 조회
const docSnap = await getDoc(docRef)
```

<details>
<summary>ex</summary>

<a id="113eda9b0fe18087b26fe71383ecce25"></a>

```javascript
const docRef = doc(db, "cities", "LA");  // 특정 문서 참조
const docSnap = await getDoc(docRef);
```

</details>

</details>

---

<details>
<summary>테스트</summary>

<details>
<summary>전체 문서(컬렉션) 조회</summary>

<details>
<summary>전체 코드 </summary>

<a id="113eda9b0fe180f5b4c4f80526d996a4"></a>

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1, shrink-to-fit=no"
    />
    <title>firebase Test</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.4/jquery.min.js"></script>
    <script type="module">
      // Firebase SDK 라이브러리 가져오기
      import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-app.js";
      import { getFirestore } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";
      import {
        doc,
        collection,
        addDoc,
        getDocs,
        updateDoc,
        deleteDoc,
      } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";

      const firebaseConfig = {
	        // config
      };

      // Firebase 인스턴스 초기화
      const app = initializeApp(firebaseConfig);
      const db = getFirestore(app);

      // 전체 문서(컬랙션) 조회
      async function getDocuments() {
        const getDocuments = await getDocs(collection(db, "cities"));
        getDocuments.forEach((doc) => {
          console.log(`${doc.id} => ${doc.data()}`);
        });
      }

      $("#create-doc").click(() => getDocuments());
    </script>
  </head>

  <body>
    <button id="create-doc">이벤트 트리거</button>
  </body>
</html>

```

</details>

---

<details>
<summary>firebase 연동을 위한 초기 설정</summary>

<a id="a21cdd8954dc4fed99b5d203d669fce9"></a>

```java
<script type="module">
    // Firebase SDK 라이브러리 가져오기
    import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-app.js";
    import { getFirestore } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";
    import {
      collection,
      getDocs,
    } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";

    const firebaseConfig = {
	     // config 설정 
	  };

    // Firebase 인스턴스 초기화
    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);
    
    
</script>
```

</details>

<details>
<summary>전체 문서(컬렉션) 조회&#58; <code>getDocuments()</code></summary>

<a id="113eda9b0fe1804d9945f2ece9d5eae2"></a>

```javascript
// 전체 문서(컬랙션) 조회
async function readDocuments() {
  const getDocuments = await getDocs(collection(db, "cities"));
  getDocuments.forEach((doc) => {
    console.log(`${doc.id} => ${doc.data()}`);
  });
}
```

</details>

<details>
<summary>전체 문서 조회 &#45; 이벤트 트리거 </summary>

<a id="c0c8af79ce6c44e0a60bdec05d5db506"></a>

```java
 // script (JS)
 $("#create-doc").click(() => readDocuments());
 
 
 // HTML
 <button id="create-doc">이벤트 트리거</button>
```

</details>

<details>
<summary>결과 확인</summary>

<a id="113eda9b0fe1802ab525fca7cb79525e"></a>

아래와 같이 정상적으로 가져옴

![](b78301ef9c59e70a.webp)

</details>

</details>

<details>
<summary>특정 문서 조회 </summary>

<details>
<summary>전체 코드 </summary>

<a id="0d43493f10874d858ff74c413288ee2c"></a>

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1, shrink-to-fit=no"
    />
    <title>firebase Test</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.4/jquery.min.js"></script>
    <script type="module">
      // Firebase SDK 라이브러리 가져오기
      import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-app.js";
      import { getFirestore } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";
      import {
	      doc,
        getDoc
      } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";

      const firebaseConfig = {
	        // config
      };

      // Firebase 인스턴스 초기화
      const app = initializeApp(firebaseConfig);
      const db = getFirestore(app);
			
			// 특정 문서 조회
			async function getDocument() {
			
			  // 문서명 ( 테스트 확인을 위한 예시 문서명, DB에서 가져옴)
			  const id = "4RBKRXVNg8QJ95KZd4OH";
			
			  // 특정 문서 참조
			  const docRef = doc(db, "cities", id);
			  
			  // 특정 문서 조회
			  const docSnap = await getDoc(docRef);
			
			  if (docSnap.exists()) {
			    console.log("문서 정보: ", docSnap.data());
			  } else {
			    console.log("해당하는 문서가 존재하지 않습니다.");
			  }
			}

      $("#create-doc").click(() => getDocument());
    </script>
  </head>

  <body>
    <button id="create-doc">이벤트 트리거</button>
  </body>
</html>

```

</details>

---

<details>
<summary>firebase 연동을 위한 초기 설정</summary>

<a id="4fdb4ba2bd464c30869e8eb084822532"></a>

```java
<script type="module">
    // Firebase SDK 라이브러리 가져오기
    import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-app.js";
    import { getFirestore } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";
    import {
	    doc,
      getDoc,
    } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";

    const firebaseConfig = {
	     // config 설정 
	  };

    // Firebase 인스턴스 초기화
    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);
    
    
</script>
```

</details>

<details>
<summary>특정 문서 조회&#58; <code>getDocument()</code></summary>

<a id="113eda9b0fe180d09074cf51c262fa37"></a>

```javascript
// 특정 문서 조회
async function getDocument() {

  // 문서명 ( 테스트 확인을 위한 예시 문서명, DB에서 가져옴)
  const id = "4RBKRXVNg8QJ95KZd4OH";

  // 특정 문서 참조
  const docRef = doc(db, "cities", id);
  
  // 특정 문서 조회
  const docSnap = await getDoc(docRef);

  if (docSnap.exists()) {
    console.log("문서 정보: ", docSnap.data());
  } else {
    console.log("해당하는 문서가 존재하지 않습니다.");
  }
}
```

</details>

<details>
<summary>이벤트 트리거 </summary>

<a id="113eda9b0fe1801999bae0213fd9c5e3"></a>

```java
 // script (JS)
 $("#create-doc").click(() => getDocument());
 
 
 // HTML
 <button id="create-doc">이벤트 트리거</button>
```

</details>

<details>
<summary>결과 확인</summary>

<a id="113eda9b0fe180f896d0d0852b5a2134"></a>

아래와 같이 정상적으로 가져와 콘솔에 출력됨

![](9c98ab03effcd4a4.webp)

</details>

</details>

</details>

<a id="758bdafb6fe841a48502958e726cc141"></a>

### <strong>U</strong>pdate(문서 업데이트)&#58; <code>updateDoc()</code>

<details>
<summary>문서(필드) 업데이트</summary>

> 동일하게 <strong><u>참조값 생성(</u></strong><strong><code>doc()</code></strong><strong>)</strong>해 가져와 <strong>업데이트(</strong><strong><code>updateDoc()</code></strong><strong>)</strong>를 한다&#46; 

<a id="113eda9b0fe1802888ebe311e852603e"></a>

```javascript
// 참조값 생성: '컬렉션명/문서명'
const docRef = doc(db, 컬렉션명, 문서명);

// 업데이트
// 부분 업데이트 가능 [ post or patch ])
await updateDoc(docRef, 업데이트 데이터)
```

<details>
<summary>ex)</summary>

<details>
<summary>컬렉션&#58; <code>cities</code>  </summary>

<a id="113eda9b0fe18021bab4ece7e8498df8"></a>

```javascript
cities = {
   country: string,
   name: string,
   state: string,
}  
```

</details>

<a id="113eda9b0fe18099a6addbedf0f29edb"></a>

```javascript
import { doc, updateDoc } from "firebase/firestore";

async function updateDocument() {
  const docRef = doc(db, "cities", "LA");
  await updateDoc(docRef, {
    state: "California"
  });
}
```

</details>

</details>

---

<details>
<summary>테스트 </summary>

<details>
<summary>전체 코드 </summary>

<a id="7c313ccf316b4a6aa10403bf63d965ef"></a>

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1, shrink-to-fit=no"
    />
    <title>firebase Test</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.4/jquery.min.js"></script>
    <script type="module">
      // Firebase SDK 라이브러리 가져오기
      import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-app.js";
      import { getFirestore } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";
      import {
	      doc,
        updateDoc
      } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";

      const firebaseConfig = {
	        // config
      };

      // Firebase 인스턴스 초기화
      const app = initializeApp(firebaseConfig);
      const db = getFirestore(app);

      // 문서 업데이트
      async function updateDocument() {
        const id = "4RBKRXVNg8QJ95KZd4OH";

        /**
          cities = {
             country: string,
             name: string,
             state: string,
          }  
        */
        const updateData = {
          name: "업데이트 테스트2",
        };

        const docRef = doc(db, "cities", id);
        await updateDoc(docRef, updateData);
      }
			
			// 이벤트 트리거
      $("#create-doc").click(() => updateDocument());
    </script>
  </head>

  <body>
    <button id="create-doc">이벤트 트리거</button>
  </body>
</html>

```

</details>

---

<details>
<summary>firebase 연동을 위한 초기 설정</summary>

<a id="2dfd9261e85f43a69c2ad7b3fa4daf6c"></a>

```java
<script type="module">
    // Firebase SDK 라이브러리 가져오기
    import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-app.js";
    import { getFirestore } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";
    import {
			doc,
      updateDoc,
    } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";

    const firebaseConfig = {
	     // config 설정 
	  };

    // Firebase 인스턴스 초기화
    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);
    
    
</script>
```

</details>

<details>
<summary>문서 업데이트</summary>

<a id="113eda9b0fe180249748d9aad371cfe9"></a>

```javascript
async function updateDocument() {
  const id = "4RBKRXVNg8QJ95KZd4OH";

  /**
    cities = {
       country: string,
       name: string,
       state: string,
    }  
  */
  const updateData = {
    // county: "업데이트 테스트",
    name: "업데이트 테스트2",
  };

  const docRef = doc(db, "cities", id);
  await updateDoc(docRef, updateData);
}
```

</details>

<details>
<summary>이벤트 트리거 </summary>

<a id="3fa983bffd3240f6aa21c4f1e07c2363"></a>

```java
 // script (JS)
 $("#create-doc").click(() => updateDocument());
 
 
 // HTML
 <button id="create-doc">이벤트 트리거</button>
```

</details>

<details>
<summary>결과 확인</summary>

![](388b5518ac4a7cf8.webp)

![](f9041356c9b6a984.webp)

</details>

</details>

<a id="bdfec475ac77485e89389919efe8afff"></a>

### <strong>D</strong>elete(문서 삭제)&#58; <code>deleteDoc()</code>

<details>
<summary>문서 삭제</summary>

> 여기도 동일하게 참조값을 생성(<code>doc()</code>)한 후 삭제(<code>deleteDoc(참조값)</code>)

<a id="113eda9b0fe180bc99a6e6954b14139c"></a>

```javascript
// 참조값 생성
const docRef = doc(db, 컬렉션명, 문서명(id))

// 문서 삭제: deleteDoc(참조값)
await deleteDec(doRef)
```

</details>

---

<details>
<summary>테스트 </summary>

<details>
<summary>🤬 &#91;Error&#93; 문서 삭제 안됨</summary>

<a id="113eda9b0fe180e38cb5d51af4bc7c1b"></a>

### 문제점 1

---

<a id="113eda9b0fe180a68903f0e2bfa81e88"></a>

<strong><u>컬렉션을 명을 잘못 입력</u></strong>하여 문서가 삭제되지 않았음

- <code>“cites”</code>  → <code>“cities”</code>
    <a id="113eda9b0fe180f0b540c6cc5fe7f14c"></a>

    ```javascript
    async function deleteDocument() {
    const id = "4RBKRXVNg8QJ95KZd4OH";

    const docRef = doc(db, "cites", id);
    await deleteDoc(docRef);
    console.log("문서 삭제 완료");
    }
    ```

- 잘못된 컬렉션명을 입력했는데도 아무런 에러가 발생하지 않았음
    <a id="113eda9b0fe1800b99a3c687cfe42bc7"></a>

    따라서 아래와 같이 try&#45;catch 구문으로 error 발생 시 해당 오류 메세지를 출력하도록 변경함

    <a id="113eda9b0fe180339a00d71ded710b1c"></a>

    ```javascript
    try {
        // 문서 참조 생성
        docRef = doc(db, collectionName, id);
        console.log(`문서 참조 생성 성공: ${docRef.path}`);
      } catch (error) {
        console.error("문서 참조 생성 중 오류 발생:", error);
        return; // 오류가 발생하면 함수 종료
      }

      try {
        // 문서 삭제
        await deleteDoc(docRef);
        console.log("문서 삭제 완료");
      } catch (error) {
        console.error("문서 삭제 중 오류 발생:", error);
      }
    ```

<a id="113eda9b0fe18030a09bf30d5c6cae0d"></a>

### 문제점 2

---

- 그러나 잘못된 컬렉션명(<code>cites</code>) 입력 시 오류 메세지가 나와야 하는데, 아래와 같이 정상적으로 삭제 되었다는 메세지가 생성됨
    ![](99976274992ffc61.webp)

- 원인1) 참조값 생성(doc)이 db를 통한 검증이 아닌 <strong><u>입력받은 인자를 url 형태로 포맷</u></strong> 처리만 함

- 원인2) 잘못된 참조값으로 <code>delecDoc()</code>가 실행 되어도 성공/실패 여부를 판단할 반환값이 존재하지 않음

<a id="113eda9b0fe180a58c02f488377959b2"></a>

### 해결

---

<a id="113eda9b0fe180e08588ecb65bf0d794"></a>

따라서 <strong><u>생성된 참조값으로 문서를 조회</u></strong>하여, <strong><u>해당 문서 존재 여부 확인</u></strong> 후 삭제를 진행함

<a id="113eda9b0fe18036bfccc62eef109426"></a>

```javascript
async function deleteDocument() {
  const id = "4RBKRXVNg8QJ95KZd4OH";

  const collectionName = "cities";
  
  // 참조 값 생성
  const docRef = doc(db, collectionName, id);

  // 문서 참조값 출력
  console.log(`문서 참조 생성 성공: ${docRef.path}`);

  // 문서 존재 여부 확인
  const docSnapshot = await getDoc(docRef);
  if (!docSnapshot.exists()) {
    console.error("문서가 존재하지 않습니다.");
    return; // 문서가 존재하지 않으면 함수 종료
  }

  // 문서 삭제
  await deleteDoc(docRef);
}
```

<a id="113eda9b0fe180edb809d9e3fc600e61"></a>

잘못된 컬렉션 값(<code>cites</code>) 입력 시 아래와 같이 오류 메시지를 출력하는 것을 확인 

![](cb64f63d8ae6d2d7.webp)

<a id="113eda9b0fe180a181b9d891c9ea8e29"></a>

또한 정삭적인 컬렉션 값(<code>cities</code>) 입력 시 해당하는 문서가 정상적으로 삭제되는 것을 확인함

![](84194fedee96776a.webp)

![](161dd251a563fff4.webp)

</details>

<details>
<summary>전체 코드 </summary>

<a id="a240889a352440f1a70a87dfa8d67c74"></a>

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1, shrink-to-fit=no"
    />
    <title>firebase Test</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.4/jquery.min.js"></script>
    <script type="module">
      // Firebase SDK 라이브러리 가져오기
      import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-app.js";
      import { getFirestore } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";
      import {
			  doc,
        deleteDoc,
      } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";

      const firebaseConfig = {
	        // config
      };

      // Firebase 인스턴스 초기화
      const app = initializeApp(firebaseConfig);
      const db = getFirestore(app);

      // 문서 삭제
			async function deleteDocument() {
				  const id = "4RBKRXVNg8QJ95KZd4OH";
				
				  const collectionName = "cities";
				  
				  // 참조 값 생성
				  const docRef = doc(db, collectionName, id);
				
				  // 문서 참조값 출력
				  console.log(`문서 참조 생성 성공: ${docRef.path}`);
				
				  // 문서 존재 여부 확인
				  const docSnapshot = await getDoc(docRef);
				  if (!docSnapshot.exists()) {
				    console.error("문서가 존재하지 않습니다.");
				    return; // 문서가 존재하지 않으면 함수 종료
				  }
				
				  // 삭제
				  await deleteDoc(docRef);
		  }
		  
		  // 이벤트 트리거
		  $("#create-doc").click(() => deleteDocument());
      
    </script>
  </head>

  <body>
    <button id="create-doc">이벤트 트리거</button>
  </body>
</html>

```

</details>

---

<details>
<summary>firebase 연동을 위한 초기 설정</summary>

<a id="1a9e3ceaedec44c5884793a5bbfcc6b5"></a>

```java
<script type="module">
    // Firebase SDK 라이브러리 가져오기
    import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-app.js";
    import { getFirestore } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";
    import {
      doc,
      deleteDoc
    } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";

    const firebaseConfig = {
	     // config 설정 
	  };

    // Firebase 인스턴스 초기화
    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);
    
    
</script>
```

</details>

<details>
<summary>문서 삭제</summary>

<a id="113eda9b0fe18018a812c11b2b47565f"></a>

```javascript
async function deleteDocument() {
  const id = "4RBKRXVNg8QJ95KZd4OH";

  const collectionName = "cities";
  
  // 참조 값 생성
  const docRef = doc(db, collectionName, id);

  // 문서 참조값 출력
  console.log(`문서 참조 생성 성공: ${docRef.path}`);

  // 문서 존재 여부 확인
  const docSnapshot = await getDoc(docRef);
  if (!docSnapshot.exists()) {
    console.error("문서가 존재하지 않습니다.");
    return; // 문서가 존재하지 않으면 함수 종료
  }

  // 문서 삭제
  await deleteDoc(docRef);
}
```

</details>

<details>
<summary>이벤트 트리거 </summary>

<a id="a969642678a54c458f4cebbd34d486a4"></a>

```java
 // script (JS)
 $("#create-doc").click(() => deleteDocument());
 
 
 // HTML
 <button id="create-doc">이벤트 트리거</button>
```

</details>

<details>
<summary>결과 확인</summary>



</details>

</details>

<a id="112eda9b0fe181618c50f97b8f9433a8"></a>

### SEE ( 피드백 )

---

- 머리가 과부화다&#46;&#46; 더는 안돌아감

- 그냥 css나 만지면서 놀음…
