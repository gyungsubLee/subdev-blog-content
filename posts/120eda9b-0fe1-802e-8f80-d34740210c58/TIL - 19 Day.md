---
order: 55
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 120eda9b-0fe1-802e-8f80-d34740210c58
title: TIL - 19 Day
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 10aeda9b-0fe1-8045-a8c4-f10918253453
    title: TIL
  - id: 120eda9b-0fe1-802e-8f80-d34740210c58
    title: TIL - 19 Day
excerpt: 💡 PDS 다이어리 참조 PlAN ( 오늘 학습할 내용들 ) --- - [x] 계산기 구현 - 1차 - [x] github 저장소 만들기 - [x] readme 작성 - [ ] 자바 - 4주차 정리 ( 정리 중 ) DO ( 오늘 공부한 내용) --- 과제) 계산기 구현 - 스프링 MVC 학습할 때, 정리했던 ‘어댑터 패
cover: null
icon: null
notionProperties:
  날짜: 2024-10-15
  Category: TIL
  Keyword: • 과제) 계산기 구현
schema_version: 1
parent_id: 10aeda9b-0fe1-8045-a8c4-f10918253453
created: 2024-10-15T00:18:02.167Z
updated: 2024-10-18T04:51:16.606Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/TIL-f10918253453/TIL - 19 Day-d34740210c58/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/120eda9b0fe1802e8f80d34740210c58
---
> 💡 
> 
> <a id="120eda9b0fe1813ea448e9216f51abb3"></a>
> 
> PDS 다이어리 참조

<a id="120eda9b0fe18102948df4859e618a93"></a>

### PlAN ( 오늘 학습할 내용들 )

---

- [x] 계산기 구현 &#45; 1차

- [x] github 저장소 만들기

- [x] readme 작성

- [ ] 자바 &#45; 4주차 정리 ( 정리 중 ) 

<a id="120eda9b0fe181d8911ff07cbbb25588"></a>

### DO ( 오늘 공부한 내용)

---

<details>
<summary>과제) 계산기 구현</summary>

- 스프링 MVC 학습할 때, 정리했던  ‘어댑터 패턴’ 복습 겸, 적용해봄
    > <a href="https://beautiful-college-c84.notion.site/2b9bb7eb0ff045c2b3413eeb77b2e010">페이지</a> 

- SRP, OCP, DIP 준수를 위해, interface를 만들어 구현 처리함
    > <a href="https://beautiful-college-c84.notion.site/11beda9b0fe180d19947c51365c8c1a9">페이지</a> 

    - 근데 의존성이 Main 클래스 밖에 없는데, 굳이 적용해야 하나 싶음<br>그래도 복습 겸 적용함

    - [ ] calculator 클래스 &#45; 생성자 주입으로 수정 → DIP 준수

---

<details>
<summary>3주차 과제 </summary>

[Java_문법_종합반_이경섭.zip](a0b0a2063966c98c.zip)

<details>
<summary>Step 1, 2 &#45; if문, switch 문</summary>

<details>
<summary>Calculator</summary>

<a id="50d37f7e34254388a42791cc633a0fa0"></a>

```java
package calculator.Step1_2;

public class Calculator {

    // if 문
    public double calculate1(String operator, int firstNumber, int secondNumber) {
        double answer = 0;

        if (operator.equals("+")) {
            answer = firstNumber + secondNumber;
        } else if (operator.equals("-")) {
            answer = firstNumber - secondNumber;
        } else if (operator.equals("*")) {
            answer = firstNumber * secondNumber;
        } else if (operator.equals("/")) {
            answer = firstNumber / secondNumber;
        } else if (operator.equals("%")) {    // else 문 가능, 더 명시적으로 표현하기 위해 else if 사용
            answer = firstNumber % secondNumber;
        }
        
        return answer;
    }

    // switch 문
    public double calculate2(String operation, double a, double b) {
        switch (operation) {
            case "+": return a + b;
            case "-": return a - b;
            case "*": return a * b;
            case "/": return a / b;
            case "%": return a % b;
            default: throw new UnsupportedOperationException("Unknown operation");
        }
    }

}

```

</details>

<details>
<summary>Main</summary>

<a id="7da1234522ce408698b19db8b5a18c96"></a>

```java
package calculator.Step1_2;

public class Main {
    public static void main(String[] args) {
        Calculator calculator  = new Calculator();
        System.out.println(calculator.calculate1("%", 10, 20));
        System.out.println(calculator.calculate2("%", 10, 20));
    }
}
```

</details>

</details>

<details>
<summary>Step 3 &#45; 클래스 분리</summary>

- operation
    <details>
    <summary>AddOperation</summary>

    <a id="1e2c480059b24fb9a95e66b9f498dee4"></a>

    ```java
    package calculator.Step3.operation;

    public class AddOperation{
        public double calculate(double a, double b) {
            return a + b;
        }
    }
    ```

    </details>

    <details>
    <summary>SubstractOperation</summary>

    <a id="4f2a58a5fb614d119349d701a8a6e78b"></a>

    ```java
    package calculator.Step3.operation;

    public class SubstractOperation {
        public double calculate(double a, double b) {
            return a - b;
        }
    }
    ```

    </details>

    <details>
    <summary>MultiplyOperation</summary>

    <a id="33c36d5a77e24b0d958fb34bfa645a24"></a>

    ```java
    package calculator.Step3.operation;

    public class MultiplyOperation{
        public double calculate(double a, double b) {
            return a * b;
        }
    }
    ```

    </details>

    <details>
    <summary>DivideOperation</summary>

    <a id="812e8c0ea27e446493b02a4dd72e351c"></a>

    ```java
    package calculator.Step3.operation;

    public class DivideOperation{
        public double calculate(double a, double b) {
            return a / b;
        }
    }
    ```

    </details>

<details>
<summary>Calculator</summary>

<a id="120eda9b0fe1806ea637f3f1859cba7a"></a>

```java
package calculator.Step3;

import calculator.Step3.operation.AddOperation;
import calculator.Step3.operation.DivideOperation;
import calculator.Step3.operation.MultiplyOperation;
import calculator.Step3.operation.SubstractOperation;


// @RequiredArgsConstructor
public class Calculator {

    private final AddOperation addOperation;
    private final SubstractOperation substractOperation;
    private final MultiplyOperation multiplyOperation;
    private final DivideOperation divideOperation;

    public Calculator(AddOperation addOperation, SubstractOperation substractOperation, MultiplyOperation multiplyOperation, DivideOperation divideOperation) {
        this.addOperation = addOperation;
        this.substractOperation = substractOperation;
        this.multiplyOperation = multiplyOperation;
        this.divideOperation = divideOperation;
    }

    public double calculate(String operator, int num1, int num2) {
        double answer = 0;

        if(operator.equals("+")){
            answer = addOperation.calculate(num1, num2);
        }else if(operator.equals("-")){
            answer = substractOperation.calculate(num1, num2);
        }else if(operator.equals("*")){
            answer = multiplyOperation.calculate(num1, num2);
        }else if(operator.equals("/")) {
            answer = divideOperation.calculate(num1, num2);
        }
        return answer;
    }
}

```

</details>

<details>
<summary>Main</summary>

<a id="edb74ab5f301456d86a0f3fee6644196"></a>

```java
package calculator.Step3;

import calculator.Step3.operation.AddOperation;
import calculator.Step3.operation.DivideOperation;
import calculator.Step3.operation.MultiplyOperation;
import calculator.Step3.operation.SubstractOperation;

public class Main {
    public static void main(String[] args) {
        Calculator calculator  = new Calculator(new AddOperation(), new SubstractOperation(),
                new MultiplyOperation(), new DivideOperation());
        System.out.println(calculator.calculate("+", 10, 20));
        System.out.println(calculator.calculate("*", 10, 20));

    }
}
```

</details>

</details>

<details>
<summary>Step 4 &#45; 추상 클래스</summary>

- operation
    <details>
    <summary>&#60; 추상(abstract) 클래스 &#62; AbstractOperation</summary>

    <a id="120eda9b0fe180a08f0bd898635c9cc3"></a>

    ```java
    package calculator.Step4.operation;

    public abstract class AbstractOperation {
        public abstract double calculate(double a, double b);
    }
    ```

    </details>

    <details>
    <summary>AddOperation</summary>

    <a id="cc2b429f37944125867564ccbe1c94c5"></a>

    ```java
    package calculator.Step4.operation;

    public class AddOperation extends AbstractOperation {

        @Override
        public double calculate(double a, double b) {
            return a + b;
        }
    }

    ```

    </details>

    <details>
    <summary>SubstractOperation</summary>

    <a id="b6e8b7722d7f42159638cee7eca06d2a"></a>

    ```java
    package calculator.Step4.operation;

    public class SubstractOperation extends AbstractOperation {
        @Override
        public double calculate(double a, double b) {
            return a - b;
        }
    }

    ```

    </details>

    <details>
    <summary>MultiplyOperation</summary>

    <a id="3cfcdc64538a47d298e0d8061fa5dbad"></a>

    ```java
    package calculator.Step4.operation;

    public class MultiplyOperation extends AbstractOperation {

        @Override
        public double calculate(double a, double b) {
            return a * b;
        }
    }

    ```

    </details>

    <details>
    <summary>DivideOperation</summary>

    <a id="9a143c8294da4bba9e012c6a02c6efc1"></a>

    ```java
    package calculator.Step4.operation;

    public class DivideOperation extends AbstractOperation {
        @Override
        public double calculate(double a, double b) {
            return a / b;
        }
    }

    ```

    </details>

<details>
<summary>Calculator</summary>

<a id="9ce30f13399346f896145ed10f0900bd"></a>

```java
package calculator.Step4;

import calculator.Step4.operation.AbstractOperation;


public class Calculator {

    private AbstractOperation operation;

    public Calculator(AbstractOperation operation) {
        this.operation = operation;
    }


    // Setter를 통해 operation 클래스 수정
    public void setOperation(AbstractOperation operation) {
        this.operation = operation;
    }

    public double calculate(int a, int b) {
        double answer = 0;
        answer = operation.calculate(a, b);
        return answer;
    }

}
```

</details>

<details>
<summary>Main</summary>

<a id="71f9d3cd03b140dcb8a33a964d4a211a"></a>

```java
package calculator.Step4;

import calculator.Step4.operation.AddOperation;
import calculator.Step4.operation.DivideOperation;
import calculator.Step4.operation.MultiplyOperation;
import calculator.Step4.operation.SubstractOperation;

public class Main {
    public static void main(String[] args) {
        Calculator calculator  = new Calculator(new AddOperation());
        System.out.println(calculator.calculate(10, 20));
        calculator.setOperation(new MultiplyOperation());
        System.out.println(calculator.calculate(10, 20));
    }
}
```

</details>

</details>

<details>
<summary>추가) Step 5 &#45; 인터페이스, 어댑터 패턴</summary>

- operation
    <details>
    <summary>&#60;interface&#62; Operation</summary>

    <a id="120eda9b0fe180119819dffbdd5d3395"></a>

    ```java
    package calculator.Step5.operation;

    public interface Operation {
        double calculate(double a, double b);
    }

    ```

    </details>

    <details>
    <summary>AddOperation</summary>

    <a id="722e6c1f95414859ac3b0a3726801dc2"></a>

    ```java
    package calculator.Step5.operation;

    public class AddOperation implements Operation {

        @Override
        public double calculate(double a, double b) {
            return a + b;
        }
    }
    ```

    </details>

    <details>
    <summary>SubstractOperation</summary>

    <a id="c9531ee2464a438a83c7999bd3259399"></a>

    ```java
    package calculator.Step5.operation;

    public class SubstractOperation implements Operation {
        @Override
        public double calculate(double a, double b) {
            return a - b;
        }
    }
    ```

    </details>

    <details>
    <summary>MultiplyOperation</summary>

    <a id="322f07ee67b8480aa7fd2ca8ab368a02"></a>

    ```java
    package calculator.Step5.operation;

    public class MultiplyOperation implements Operation {

        @Override
        public double calculate(double a, double b) {
            return a * b;
        }
    }
    ```

    </details>

    <details>
    <summary>DivideOperation</summary>

    <a id="f35dd6ac0da14556907f940aefb4cf8b"></a>

    ```java
    package calculator.Step5.operation;

    public class DivideOperation implements Operation {
        @Override
        public double calculate(double a, double b) {
            return a / b;
        }
    }
    ```

    </details>

<details>
<summary>Calculator &#45; 어댑터 패턴 적용</summary>

<a id="9f39a4c1a68c4d949d62b98885150a01"></a>

```java
public class Calculator {
    private final Map<String, Operation> operationMappingAapter = new HashMap<>();

    public Calculator() {
        initOperationMappingMap();
    }

    private void initOperationMappingMap(){
        operationMappingAapter.put("+", new AddOperation());
        operationMappingAapter.put("-", new SubstractOperation());
        operationMappingAapter.put("*", new MultiplyOperation());
        operationMappingAapter.put("/", new DivideOperation());
    }

    public double calculate(String operator, double a, double b){
        Operation mappingOperation = operationMappingAapter.get(operator);
        if (mappingOperation == null) {
            throw new UnsupportedOperationException("Unknown operation: " + operator);
        }
        return mappingOperation.calculate(a, b);
    }
}
```

</details>

<details>
<summary>Main</summary>

<a id="5f2db9307c554a74be56fab4929e52d7"></a>

```java
package calculator.Step5;

public class Main {
    public static void main(String[] args) {
        Calculator calculator  = new Calculator();

        System.out.println("Addition: " + calculator.calculate("+", 10, 20)); // 30
        System.out.println("Subtraction: " + calculator.calculate("-", 20, 10)); // 10
        System.out.println("Multiplication: " + calculator.calculate("*", 10, 20)); // 200
        System.out.println("Division: " + calculator.calculate("/", 20, 10)); // 2
    }
}
```

</details>

</details>

</details>

<details>
<summary>github </summary>

[Calculator_with_java](https://github.com/gyungsubLee/Calculator_with_java)

</details>

</details>

- 자바 종합반   &#45; 4주차 정리 중
    > <a href="https://beautiful-college-c84.notion.site/213de689e18f49d7bfbbb2d46e7663d8">페이지</a> &#45; 4주차

<details>
<summary>이전에 적어둔 의문점 해결 </summary>

- 머리가 안돌아가서 이전에 작성한 TIL 보던 중, 이전에 표시하고 정리 안한 내용 정리함

<details>
<summary>🧐 실제 반환 받는 JSON 데이터에서 알아서 스프링이 DTO 포맷에 맞춰 데이터를 필터링 해준다&#46; 내부 동작 방식이 어떻게 되는가?</summary>

<a id="c570721cb0be4375a8778669fdf28d61"></a>

크게 아래 3가지 요소에 의해 이루어 진다&#46;

- HTTPMessageConverter

- ObjectMapper(Jackson)

- Reflection

<details>
<summary>1&#46;  요청 수신, 데이터 처리</summary>

<a id="3ac55d30d4ac4729ad11044a61e0ee20"></a>

클라이언트로부터 JSON 데이터 수신

- &#64;RequestBody&#58; JSON → userDTO 변환
    - ‘HTTP 요청 메세지(POST) &#45; Body’ 에 있는 json 데이터 가져와 DTO로 변환

<a id="ff7d872091904d278d0fe00aeab2e98a"></a>

```java
@PostMapping("/user")
public ResponseEntity<String> createUser(@RequestBody UserDTO userDTO) {
    // userDTO 내부에 클라이언트의 JSON 데이터가 바인딩됨
    return ResponseEntity.ok("User created");
}
```

</details>

<details>
<summary>2&#46; HttpMessageConverter </summary>

- Spring은 요청 본문(Body)의 데이터를 처리할 때, HttpMessageConverter를 사용한다&#46;
    <a id="b75a169aeecb439d9e41635129af94e3"></a>

    즉, &#64;RequestBody를 통한 <strong><u>JSON 데이터의 DTO 변환</u></strong>은 <strong><u>HttpMessageConverter를 사용</u></strong>하여 이뤄진다&#46;

    - 정확히는 <code>MappingJackson2HttpMessageConverter</code>에서 <strong><u>Jackson 라이브러리</u></strong>의 <code>ObjectMapper</code> 사용

- JSON → 콘텐츠 타입&#58; <code>application/json</code>
    - ⇒  <code>MappingJackson2HttpMessageConverter</code>

- 해당 메세지 컨버터는 Jackson 라이브러리의 ObjectMapper를 사용해 JSON 데이터를 Java 객체(DTO)로 변환한다&#46;  

</details>

<details>
<summary>3&#46; <strong>Jackson의 ObjectMapper와 Reflection</strong></summary>

- Reflection
    - Java 런타임에서 클래스나 메서드, 필드에 대해 동적으로 접근하는 기술

- <code>ObjectMapper</code>가 <code>reflection</code><strong>을 사용하여 </strong><strong><u>JSON 문자열을 파싱할 때,</u></strong> <strong><u>DTO 클래스의 필드 이름</u></strong>과 <strong><u>JSON 키 값</u></strong>을 <strong><u>비교</u></strong>하여 <strong><u>자동으로 매핑</u></strong>한다&#46;
    > ⚠️ 
    > 
    > <a id="110ec7417c9749f4af80667b45688261"></a>
    > 
    > <strong><u>DTO 필드명</u></strong>과 <strong><u>JSON 키 값</u></strong>이 <strong><u>동일</u></strong>해야 함

    <details>
    <summary>ex)</summary>

    <details>
    <summary>json</summary>

    <a id="694d657021fc4dbdbf39801161d752fc"></a>

    ```json
    {
      "name": "John",
      "age": 30
    }
    ```

    </details>

    <details>
    <summary>DTO</summary>

    <a id="e0786446dd0b4409ba86b67a16932a2c"></a>

    ```java
    @Getter @Setter
    public class UserDTO {
        private String name;
        private int age;
    }
    ```

    </details>

    </details>

</details>

<details>
<summary>4&#46; DTO,  필터링 </summary>

- DTO 클래스에 정의된 필드만 매핑
    - 선언되지 않은 필드는 무시

    <details>
    <summary>ex)</summary>

    > json 데이터에 정의된 ‘extraField’ 데이터는 DTO에 해당하는 필드가 존재하지 않기 때문에 무시된다&#46; 

    <details>
    <summary>json</summary>

    <a id="c9c160b00ca54b5a92f4b0c8b338cc61"></a>

    ```json
    {
      "name": "John",
      "age": 30,
      "extraField": "This won't be mapped" // DTO에 정의되지 않은 필드 -> 무시
    }
    ```

    </details>

    <details>
    <summary>DTO</summary>

    <a id="1a643bcba352443fbdfcbc03532f9d40"></a>

    ```java
    @Getter @Setter
    public class UserDTO {
        private String name;
        private int age;
    }
    ```

    </details>

    </details>

</details>

</details>

<details>
<summary>추가 의문점 &#45; 리플랙션</summary>

- 런타임 환경이면, JVM에 stack 영역이거나, Heap 영역일 텐데, 어떻게 동작되는지 궁금함

</details>

</details>

<a id="120eda9b0fe181b788abd43dadd683d1"></a>

### SEE ( 피드백 )

---

- &#91; 과제&#45; 계산기 &#93; 핵심 로직은 다 구현함
    - [ ] 입력값 받는 코드 및 추가 연산 반복 처리 추가 필요 

    - [ ] enum, 제네릭 적용

- 정리를 꼼꼼히 하고 싶어서 이것 저것 찾아보면서 더하고 있는데 너무 진도가 안나간다…
    - 우선은 고, 내일까지 해보고 안되면 그냥 필요한 부분만 간략하게 정리 

<a id="120eda9b0fe1803a8903ea6400bde714"></a>

과제를 구현하느라 시간을 너무 많이 썻다&#46;&#46; 깔끔하게 수정하는데 좀 걸림

<a id="120eda9b0fe18003a2dbebefee67e348"></a>

진짜 간단한 코드인데…
