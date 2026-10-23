---
order: 29
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8160-ae51-dee6bd3ec082
title: enum
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8188-9ddf-e42c6289f47d
    title: 디자인패턴
  - id: 1c3eda9b-0fe1-81c2-b6ea-c9b4c4c77f6e
    title: "[ 백기선 ] GoF 디자인패턴"
  - id: 1c3eda9b-0fe1-8160-ae51-dee6bd3ec082
    title: enum
excerpt: "‣ 질문 (정리 전 ) 왜 enum은 역직렬화해도 새로운 인스턴스를 만들지 않고 기존 enum 상수를 돌려주는가? 일반적으로 Serializable 객체를 직렬화하면, 자바는 다음을 저장합니다: 1. 클래스 이름 2. 직렬화된 필드 값들 3. (생략 가능) 버전 UID 역직렬화 시에는 자바가: • .class 파일을 로딩"
cover: null
icon: null
notionProperties:
  Tags: 추가
  상태: 진행 중
schema_version: 1
parent_id: 1c3eda9b-0fe1-81c2-b6ea-c9b4c4c77f6e
created: 2025-03-27T07:47:13.029Z
updated: 2025-03-27T07:47:13.029Z
legacy_path: Main/디자인패턴-e42c6289f47d/[ 백기선 ] GoF 디자인패턴-c9b4c4c77f6e/enum-dee6bd3ec082/index.md
legacy_category: 디자인패턴
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18160ae51dee6bd3ec082
---
<a id="1c3eda9b0fe181b3ad13e2f6787f39f6"></a>

‣

<a id="1c3eda9b0fe181779520d7b7f0ed5252"></a>

### 질문 (정리 전 )

> <strong>왜 enum은 역직렬화해도 새로운 인스턴스를 만들지 않고 기존 enum 상수를 돌려주는가?</strong>

<a id="1c3eda9b0fe1816aadd7c43b1c9580ec"></a>

일반적으로 Serializable 객체를 직렬화하면, 자바는 다음을 저장합니다&#58;

<a id="1c3eda9b0fe18137af7bf7c41fc0a60c"></a>

1&#46;	클래스 이름

<a id="1c3eda9b0fe181d5bd49cee37263350a"></a>

2&#46;	직렬화된 필드 값들

<a id="1c3eda9b0fe1812baf8ac2ac12e77bd4"></a>

3&#46;	(생략 가능) 버전 UID

<a id="1c3eda9b0fe1817a8b49c5241adf9d0c"></a>

역직렬화 시에는 자바가&#58;

<a id="1c3eda9b0fe18193af2bca954118b221"></a>

•	&#46;class 파일을 로딩하고

<a id="1c3eda9b0fe1818dbd9ac29b9a14cce7"></a>

•	기본 생성자 없이도 내부 필드를 복원하여

<a id="1c3eda9b0fe1811b87a0cfe0ac656b81"></a>

•	<strong>새로운 인스턴스</strong>를 메모리에 만들어냅니다

> 그래서 일반 클래스는 readResolve()를 오버라이드하지 않으면 싱글톤이 깨지는 겁니다&#46;

---

<details>
<summary><strong>✅ enum은 예외적인 존재다</strong></summary>

<a id="1c3eda9b0fe181f7ab27e73ac6952b90"></a>

자바의 enum은 그냥 특별한 클래스가 아니에요&#46;

<a id="1c3eda9b0fe181afa20de0436aae3c43"></a>

<strong>자바 언어 명세 &#43; JVM 자체에서 enum을 특별 취급합니다&#46;</strong>

<a id="1c3eda9b0fe18118a8b5fef383b1d666"></a>

<strong>🔹 자바 enum은 내부적으로 다음과 같이 처리됩니다&#58;</strong>

<a id="1c3eda9b0fe1811ea8cee0e69ca7e1d7"></a>

```java
public enum Settings {
    INSTANCE;
}
```

<a id="1c3eda9b0fe181d29ce2eb431dac2acb"></a>

➡ 컴파일되면 아래처럼 변환됩니다&#58;

<a id="1c3eda9b0fe181debab1c87bde65fd74"></a>

```java
public final class Settings extends Enum<Settings> {
    public static final Settings INSTANCE = new Settings("INSTANCE", 0);

    private Settings(String name, int ordinal) {
        super(name, ordinal);
    }

    public static Settings[] values();
    public static Settings valueOf(String name);
}
```

<a id="1c3eda9b0fe18192a540e17369eb9c80"></a>

즉&#58;

<a id="1c3eda9b0fe181eb8e93d7ecffb0e28b"></a>

•	INSTANCE는 static final 필드

<a id="1c3eda9b0fe18149afabf3f1587bf199"></a>

•	생성자는 무조건 <strong>private</strong>

<a id="1c3eda9b0fe18130860cd0a65005899b"></a>

•	생성 시 name, ordinal 값이 들어갑니다

</details>

<details>
<summary>✅ <strong>Enum 클래스는 </strong><strong><code>readResolve()</code></strong><strong>를 오버라이드한다</strong></summary>

<a id="1c3eda9b0fe181c4a27ded42b68da22d"></a>

자바의 모든 enum은 <strong>java&#46;lang&#46;Enum</strong> 클래스를 자동으로 상속합니다&#46;

<a id="1c3eda9b0fe181cea5f1d4fb22ab7959"></a>

그리고 이 Enum 클래스는 JVM에 의해 특별히 취급되고,

<a id="1c3eda9b0fe181dbb1dce805a6a61cbd"></a>

직렬화/역직렬화 시 다음처럼 작동합니다&#58;

<a id="1c3eda9b0fe18131924ced4abe71fdc0"></a>

<strong>🔒 Enum 클래스 내부적으로 이렇게 동작합니다&#58;</strong>

<a id="1c3eda9b0fe181ad9a82dd5fcc4e8fce"></a>

```java
protected final Object readResolve() throws ObjectStreamException {
    return Enum.valueOf(getDeclaringClass(), name);
}
```

<a id="1c3eda9b0fe181b995ddde3da89e20b8"></a>

즉, 역직렬화할 때&#58;

<a id="1c3eda9b0fe18174b09fd3501a1e99c7"></a>

1&#46;	enum 상수의 이름 (INSTANCE)을 읽음

<a id="1c3eda9b0fe181db897ce8a73a9b2430"></a>

2&#46;	그 이름으로 valueOf()를 호출

<a id="1c3eda9b0fe181a28c83e299722a77b0"></a>

3&#46;	클래스 로딩 시 만들어진 <strong>기존 enum 상수를 반환</strong>&#33;

<a id="1c3eda9b0fe1816c9b6ee53e6312ed5b"></a>

👉 새로운 객체를 만들지 않고, 이미 있는 enum 인스턴스를 돌려줍니다&#46;

</details>

<details>
<summary><strong>✅ JVM 레벨에서 enum을 어떻게 다루나?</strong></summary>

<a id="1c3eda9b0fe18127b8d7ffd7a9bf1290"></a>

•	JVM은 <strong>enum 클래스당 상수 1개만 생성됨을 보장</strong>합니다&#46;

<a id="1c3eda9b0fe181959dd0c43ef3bebb89"></a>

•	INSTANCE, RED, GREEN 같은 enum 상수는 클래스 로딩 시 생성되어 <strong>메모리 상에 고정됨</strong>&#46;

<a id="1c3eda9b0fe181f59f67e0fad9d35ad2"></a>

•	valueOf()를 호출하면 이름으로 기존 인스턴스를 찾아줍니다&#46;

<a id="1c3eda9b0fe18175a524ea3f3f6dbd30"></a>

•	<strong>이건 JVM 명세에 명시된 동작이기 때문에 바꿀 수 없습니다&#46;</strong>

</details>

<a id="1c3eda9b0fe18126952df7bc1a99623c"></a>

```java
1. 클래스 로딩 시:
   Settings.INSTANCE ← 메모리에 1번만 생성

2. 직렬화:
   - 클래스명: "Settings"
   - 상수명: "INSTANCE"

3. 역직렬화:
   - JVM: Settings.class.valueOf("INSTANCE")
   - 반환: 기존 Settings.INSTANCE 인스턴스
```

|  |  |
| --- | --- |
| <strong>일반 클래스</strong> | <strong>enum</strong> |
| 직렬화 시 데이터 저장 | 클래스 &#43; 필드 값 |
| 역직렬화 시 인스턴스 생성 | 새 객체 생성 |
| 동일 인스턴스 보장하려면? | readResolve() 필요 |
| enum은? | Enum&#46;readResolve() 내부 구현으로 자동 처리됨 |
| JVM이 특별히 다뤄줌 | ✅ |

<a id="1c3eda9b0fe181b6aeaeea2e9212750e"></a>

```java
enum Settings {
    INSTANCE
}

public class EnumTest {
    public static void main(String[] args) throws Exception {
        Settings s1 = Settings.INSTANCE;

        // 직렬화
        ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("settings.obj"));
        oos.writeObject(s1);

        // 역직렬화
        ObjectInputStream ois = new ObjectInputStream(new FileInputStream("settings.obj"));
        Settings s2 = (Settings) ois.readObject();

        System.out.println(s1 == s2); // ✅ true
    }
}
```

<details>
<summary><strong>✅ 역직렬화 시 객체 생성 방식</strong></summary>

> ❓ 역직렬화할 때 객체는 <strong>어떻게 만들어질까?, </strong>생성자를 호출하는가?

<a id="1c3eda9b0fe18101be61ead84baddb6d"></a>

자바에서 객체를 역직렬화할 때는 일반적인 new 키워드를 쓰지 않습니다&#46;

<a id="1c3eda9b0fe18128be25eadac30fba10"></a>

즉, <strong>생성자(Constructor)는 호출되지 않습니다&#46;</strong>

<a id="1c3eda9b0fe181948309ef835470f0cc"></a>

<strong>🔧 대신 이렇게 처리합니다&#58;</strong>

<a id="1c3eda9b0fe181ea899ada8792b649bd"></a>

1&#46;	자바는 내부적으로 <strong>ObjectInputStream&#46;readObject()</strong> 를 호출

<a id="1c3eda9b0fe18130a0d4f84d69e4dc6e"></a>

2&#46;	JVM이 <strong>클래스를 메모리에 로딩</strong>

<a id="1c3eda9b0fe181c8a862f3af0ecc9f70"></a>

3&#46;	java&#46;io&#46;ObjectStreamClass 를 사용해서 클래스의 직렬화 정보 추출

<a id="1c3eda9b0fe181129eecf042e3224394"></a>

4&#46;	JVM은 <strong>생성자 호출 없이 메모리에 빈 객체를 “강제로” 생성</strong>

<a id="1c3eda9b0fe1812ab61ee32756696ec3"></a>

•	예&#58; Unsafe&#46;allocateInstance()

<a id="1c3eda9b0fe181a9bc8ff486747a7db0"></a>

5&#46;	직렬화된 <strong>필드 값을 메모리에 직접 채워 넣음</strong>

<details>
<summary>예시) Eager initialization ( 이른 초기화 )&#92;</summary>

<details>
<summary>🤬 문제&#58; 역직렬화 시, 싱글톤 패턴이 깨짐</summary>

<a id="1c3eda9b0fe18142b5f7f2554a1709be"></a>

```java
public class Settings implements Serializable {
    private static final Settings INSTANCE = new Settings();

    private Settings() {} // 외부에서 new 못 하도록

    public static Settings getInstance() {
        return INSTANCE;
    }
}
```

<a id="1c3eda9b0fe18100ae5ff78bdc23aff6"></a>

```java
Settings s1 = Settings.getInstance();

ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("settings.obj"));
oos.writeObject(s1);

ObjectInputStream ois = new ObjectInputStream(new FileInputStream("settings.obj"));
Settings s2 = (Settings) ois.readObject();

System.out.println(s1 == s2); // ❌ false (싱글톤 깨짐)
```

-  이유
    - JVM은 생성자 호출 없이<strong>새 인스턴스를 메모리에 직접 생성</strong>

    - 기존의 INSTANCE와는 전혀 다른 객체가 생성됨

</details>

<details>
<summary><strong>✅ 해결책&#58; </strong><strong><code>readResolve()</code></strong><strong> 메서드</strong></summary>

<a id="1c3eda9b0fe18180bf19f1cea1fed5bf"></a>

자바의 Serializable에서 <strong>이 문제를 방지하기 위한 전용 메서드</strong>가 있다&#46;

<a id="1c3eda9b0fe18124abe1c0419862bb49"></a>

```java
private Object readResolve() throws ObjectStreamException {
    return INSTANCE;
}
```

<a id="1c3eda9b0fe181e4ac78cf626f64faa3"></a>

동작 방식

<a id="1c3eda9b0fe181d7ba31f1e887bbf643"></a>

•	readObject() 내부적으로 역직렬화가 완료된 후

<a id="1c3eda9b0fe18111baa9d72723271b23"></a>

•	JVM은 readResolve() 메서드가 있으면 <strong>그 리턴값으로 최종 객체를 대체</strong>합니다

<a id="1c3eda9b0fe18101aefec9b13f38d13e"></a>

•	즉, 새로 만든 인스턴스를 버리고, <strong>내가 명시적으로 반환한 인스턴스를 사용</strong>

<a id="1c3eda9b0fe181e0a228e4ea3da6aacb"></a>

결과 

<a id="1c3eda9b0fe1818fbd7ec123087c26fa"></a>

```java
Settings s1 = Settings.getInstance();
Settings s2 = deserialize();

System.out.println(s1 == s2); // ✅ true
```

</details>

<a id="1c3eda9b0fe181ec8f98f6ffaccf5842"></a>

```java
1. 직렬화: Settings.INSTANCE → 바이트 스트림 저장

2. 역직렬화:
   a. JVM이 클래스 로딩
   b. 생성자 없이 인스턴스 생성 (새 객체)
   c. 필드 복원
   d. readResolve() 호출 → 기존 INSTANCE 반환
   e. 새로 만든 객체는 폐기
```

<a id="1c3eda9b0fe18192b956c11a1520edca"></a>

<strong>만약 readResolve()가 없다면?</strong>

<a id="1c3eda9b0fe181ec8833f48b20eadfaa"></a>

•	새 인스턴스가 그대로 반환되므로 == 비교에서 실패

<a id="1c3eda9b0fe1819a8d13edf437eb3225"></a>

•	<strong>싱글톤 패턴이 깨지고, 프로그램의 일관성이 무너질 수 있음</strong>

|  |  |
| --- | --- |
| <strong>항목</strong> | <strong>내용</strong> |
| 역직렬화 시 생성 방식 | 생성자 호출 없이 메모리 직접 할당 (Unsafe) |
| 싱글톤 문제 | INSTANCE와 다른 새 객체가 생김 |
| 해결 방법 | readResolve()를 오버라이드해서 기존 인스턴스를 반환 |
| enum이 안전한 이유 | Enum이 내부적으로 readResolve()를 구현하고, 이름으로 기존 상수를 반환하기 때문 |

</details>

</details>
