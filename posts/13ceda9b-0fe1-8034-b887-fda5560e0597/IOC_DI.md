---
order: 33
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 13ceda9b-0fe1-8034-b887-fda5560e0597
title: IOC/DI
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 13ceda9b-0fe1-8067-9531-e4fdae3568a2
    title: "[sparta] 스프링 숙련"
  - id: 13ceda9b-0fe1-8034-b887-fda5560e0597
    title: IOC/DI
excerpt: "IOC ( 제어의 역전, Inversion Of Control ) 📖 객체 생성, 관리 권한을 Spring 컨테이너가 담당하는 것을 말한다. - new 키워드를 통해 직접 객체를 생성하는 것이 아닌, 객체를 빈으로 등록 후 컨테이너에서 생성, 주입, 소멸을 관리한다. - IoC 개념 - 객체의 생성 및 생명주기 관리를 "
cover: null
icon: null
notionProperties:
  Point: |-
    • IOC
    • DI
  상태: 완료
schema_version: 1
parent_id: 13ceda9b-0fe1-8067-9531-e4fdae3568a2
created: 2024-11-12T02:30:24.251Z
updated: 2024-11-12T07:50:21.203Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/[sparta] 스프링 숙련-e4fdae3568a2/IOC-DI-fda5560e0597/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/13ceda9b0fe18034b887fda5560e0597
---
<a id="13ceda9b0fe18028b14fdba99f93dd1b"></a>

## IOC ( 제어의 역전, Inversion Of Control ) 

> 📖 
> 
> <a id="1874591f919046a7b8d9ef27c7d725b6"></a>
> 
> 객체 생성, 관리 권한을 Spring 컨테이너가 담당하는 것을 말한다&#46;
> 
> - <code>new</code> 키워드를 통해 직접 객체를 생성하는 것이 아닌, 객체를 <u>빈으로 등록 </u>후 <u>컨테이너에서 생성, 주입, 소멸을 관리</u>한다&#46; 

- <strong>IoC 개념</strong>
    - 객체의 생성 및 생명주기 관리를 컨테이너가 담당하기 때문에, <br>객체 간의 결합도를 낮추고 유연성을 높여 유지보수에 용이함
        - 클래스 내부에서 직접 객체를 생성하는 것이 아닌 외부에서 생성돼서 주입 받음

<a id="13ceda9b0fe1807496edc5cb8972b874"></a>

## DI ( 의존성 주입, Dependency Injection )

> 📖 
> 
> <a id="9f2ad5fab54b4786bd4efee111d84e1e"></a>
> 
> Spring에서 객체 간의 의존성을 자동으로 주입하는 것을 말한다&#46; <br>한 객체가 다른 객체 사용 시, 해당 객체를 직접 생성하지 않고<u> </u><u>외부(Spring)에서 생성되어 주입 받</u>기 때문에 <u>클래스간의 결합도를 낮</u>추고 <u>변경 및 확장 용이</u>하게 설계할 수 있다&#46;

- 인터페이스를 통해 다형성 활용

- 생성자 주입을 통한 의존성 주입 
    - 생성자 1개 시, &#64;Autowired 생략 가능

    - Lombok 사용 시, 생성자도 필요없음

- ex)
    <details>
    <summary>🤬 직접 인스턴스 생성 및 관리</summary>

    <details>
    <summary>&#91; 코드 &#93; &#60; interface &#62;  MyService</summary>

    <a id="13ceda9b0fe180b5b394f185f0200e4f"></a>

    ```java
    // Service 인터페이스
    public interface MyService {
        void doSomething();
    }
    ```

    </details>

    <details>
    <summary>&#91; 코드 &#93; &#60; interface &#62;  MyRepository</summary>

    <a id="66443ad14d064dcbbb5927ffc8cdad7b"></a>

    ```java
    // Repository 인터페이스
    public interface MyRepository {
        void queryDatabase();
    }
    ```

    </details>

    <details>
    <summary>&#91; 코드 &#93; MyServiceImpl</summary>

    <a id="327db572a7f746dfa7d271c102e6efec"></a>

    ```java
    // Service 구현체
    public class MyServiceImpl implements MyService {
    	    private MyRepository myRepository;
    	
    	    // 의존성 주입
    	    public MyServiceImpl(MyRepository myRepository) {
    	        this.myRepository = myRepository;
    	    }
    	
    	    @Override
    	    public void doSomething() {
    	        System.out.println("서비스 작업 실행");
    	        myRepository.queryDatabase();
    	    }
    }
    ```

    </details>

    <details>
    <summary>&#91; 코드 &#93; MyRepositoryImpl</summary>

    <a id="4c30c96ebe45423389f04975c375b84b"></a>

    ```java
    // Repository 구현체
    public class MyRepositoryImpl implements MyRepository {
        @Override
        public void queryDatabase() {
            System.out.println("데이터베이스 쿼리 실행");
        }
    }
    ```

    </details>

    - &#91; 코드 &#93; MyApp
        - MyApp 내부에서<strong><u> new 키워드를 사용</u></strong>하여 <strong><u>직접 인스턴스를 생성</u></strong>하기 때문에, <u>객체간에 강한 결합이 형성</u>된다&#46; 

        - 새로운 Service나 Repository가 생긴다면 클라이언트측 코드(MyApp)에 영향을 줄 수 있다&#46; 

        <a id="b6eaf13fb07c4d30aae8dcfabf2fa29f"></a>

        ```java
        public class MyApp {
            public static void main(String[] args) {
                MyRepository repo = new MyRepositoryImpl();
                MyService myService = new MyServiceImpl(repo);
                myService.doSomething();
            }
        }
        ```

    </details>

    <details>
    <summary>😁  <strong>Spring Container통한 관리 ( IOC, DI )</strong></summary>

    - 생성자 주입을 통한 의존성 주입 
        - 생성자 1개 시, &#64;Autowired 생략 가능

        - Lombok 사용 시, 생성자도 필요없음

    ---

    <details>
    <summary>&#91; 코드 &#93; &#60; interface &#62;  MyService</summary>

    <a id="c5ec5d7c1a5d4635983e35910738bd11"></a>

    ```java
    // Service 인터페이스
    public interface MyService {
        void doSomething();
    }
    ```

    </details>

    <details>
    <summary>&#91; 코드 &#93; &#60; interface &#62;  MyRepository</summary>

    <a id="451d9687e81f43bcba9506aba6a01a42"></a>

    ```java
    // Repository 인터페이스
    public interface MyRepository {
        void queryDatabase();
    }
    ```

    </details>

    <details>
    <summary>&#91; 코드 &#93; MyRepositoryImpl</summary>

    <a id="2373d8b6cc0a4d9592cdb565f631d86e"></a>

    ```java
    // Repository 구현체
    public class MyRepositoryImpl implements MyRepository {
        @Override
        public void queryDatabase() {
            System.out.println("데이터베이스 쿼리 실행");
        }
    }
    ```

    </details>

    -  코드 &#93; MyServiceImpl &#45; DI 적용 ( 생성자 주입 )
        <a id="38103b447b45454d81875d5636733ea8"></a>

        ```java
        // Service 구현체
        public class MyServiceImpl implements MyService {
        	    private MyRepository myRepository;
        	
        	    // 생성자 주입(DI 적용)
        	    @Autowired
        	    public MyIocService(MyRepository myRepository) {
        	        this.myRepository = myRepository;
        	    }
        	
        	    @Override
        	    public void doSomething() {
        	        System.out.println("서비스 작업 실행");
        	        myRepository.queryDatabase();
        	    }
        }
        ```

    - &#91; 코드 &#93; MyIocApp &#45; 컴포넌트 스캔을 통해  Spring Container 관리 (IoC 적용)
        - MyApp 내부에서<strong><u> new 키워드를 사용</u></strong>하여 <strong><u>직접 인스턴스를 생성</u></strong>하기 때문에, <u>객체간에 강한 결합이 형성</u>된다&#46; 

        - 새로운 Service나 Repository가 생긴다면 클라이언트측 코드(MyApp)에 영향을 줄 수 있다&#46; 

        <a id="b8c80afd88cc47a7a020bdf4dad7af0f"></a>

        ```java
        // Spring Container 관리(IoC 적용)
        @ComponentScan(basePackages = "com.example")
        public class MyIocApp {

            public static void main(String[] args) {
                ApplicationContext context = new AnnotationConfigApplicationContext(MyIocApp.class);

                // Service 빈을 가져와서 실행
                MyService service = context.getBean(MyService.class);
                service.doSomething();
            }
        }

        ```

    </details>
