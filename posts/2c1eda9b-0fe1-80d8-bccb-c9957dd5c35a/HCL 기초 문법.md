---
order: 7
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 2c1eda9b-0fe1-80d8-bccb-c9957dd5c35a
title: HCL 기초 문법
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817b-9c95-d96fd53640c4
    title: CI/CD
  - id: 2c0eda9b-0fe1-8030-ab57-dc0df8148eeb
    title: Terraform 마스터클래스
  - id: 2c1eda9b-0fe1-80d8-bccb-c9957dd5c35a
    title: HCL 기초 문법
excerpt: "[Syntax Overview - Configuration Language | Terraform | HashiCorp Developer]() Syntax 📖 Syntax 유형 - Configuration Syntax - 기본 - JSON Configuration Syntax - JSON 방식 JSON 구문이 사람이 읽고"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 2c0eda9b-0fe1-8030-ab57-dc0df8148eeb
created: 2025-12-06T03:28:21.497Z
updated: 2026-06-06T11:17:19.056Z
legacy_path: Main/CI-CD-d96fd53640c4/Terraform 마스터클래스-dc0df8148eeb/HCL 기초 문법-c9957dd5c35a/index.md
legacy_category: CI/CD
source_url: https://beautiful-college-c84.notion.site/2c1eda9b0fe180d8bccbc9957dd5c35a
---
[Syntax Overview &#45; Configuration Language &#124; Terraform &#124; HashiCorp Developer]()

<a id="377eda9b0fe180bdbd6aed4c28ad3a0e"></a>

## <strong>Syntax</strong>

> 📖 
> 
> <a id="376eda9b0fe180d4bfd7e7817b3429fb"></a>
> 
> <strong>Syntax 유형 </strong>
> 
> - <code>Configuration Syntax</code>  &#45; 기본
> 
> - <u><code>JSON</code></u><code> Configuration Syntax</code> &#45; JSON 방식
> 
> <a id="376eda9b0fe18077947ed9bd64f995dc"></a>
> 
> JSON 구문이 사람이 읽고 편집하기에는 더 어렵지만 프로그램적으로 생성하고 구문 분석하기는 더 쉽다&#46; 
> 
> - <code>&#46;tf</code> → Configuration
> 
> - <code>&#46;tf&#46;json</code> → JSON Configuration

<a id="376eda9b0fe18037a30fdf1f0ee50402"></a>

### Configuration Syntax

[Syntax &#45; Configuration Language &#124; Terraform &#124; HashiCorp Developer]()

> ✏️ 
> 
> <a id="376eda9b0fe18046bd56d1a839a39aaa"></a>
> 
> Terraform은 <strong><u>HCL 구문</u></strong>으로 정의되며 해당 구문은 HashiCorp의 다른 제품에서 사용되는된다&#46;
> 
> <a id="376eda9b0fe18093ad6dfd471f674391"></a>
> 
> Terraform을 사용하기 위해서 모든 HCL의 세부사항을 알 필요는 없으며 해당 섹션에서도 중요한 문법들만 다룬다&#46; 
> 
> - HCL 구문 자세한 내용 확인&#58; ‣

<details>
<summary>인자 (Arguments)</summary>

> 인자 (Arguments)는 특정 이름에 값을 할당한다&#46; 

<a id="376eda9b0fe1807a8190cba1af31a7bc"></a>

```python
image_id = "abc123"
```

- 등호 앞의 식별자는 <u>인자 이름</u> 이고, 등호 뒤의 표현식은 <u>인자의 값</u> 이다&#46; (변수 선언)

</details>

<details>
<summary>블록 (Blocks)</summary>

> 블록은 다른 콘텐츠를 담는 컨테이너이다&#46; 

<a id="376eda9b0fe180198d6ef7e37980eaa4"></a>

```python
resource "aws_instance" "example" {
  ami = "abc123"

  network_interface {
    # ...
  }
}
```

- 블록에는 유형(<code>type</code>)이 존재하며<br>생성하려는 리소스에 대한 단위를 블록으로 정의해 생성한다&#46; 
    > Most of Terraform&#39;s features (including <u>resources, input variables, output values, data sources</u>, etc&#46;) are implemented as top&#45;level blocks&#46;

    - 리소스 블록

    - 데이터 블록

    - 아웃풋 블록 

</details>

<details>
<summary>식별자</summary>

- 인자 이름, 블록 유형 이름, 리소스, 입력 변수 등과 같은 대부분의 구성 요소들의 이름은 모두 식별자이다&#46; 

- 식별자에는 <code>문자</code>, <code>숫자</code>, <code>underscores(&#95;)</code>, <code>hyphens(&#45;)</code> 등이 올 수 있다&#46; 

- 식별자의 <strong>첫번째 문자는 </strong><strong><u>숫자가 아니</u></strong>어야 한다&#46; (리터럴 숫자와의 모호성 방지)

</details>

<details>
<summary>주석</summary>

> <code>&#35;</code> 이 기본 주석 스타일아며, 이를 권장한다&#46; 
> 
> <a id="376eda9b0fe180259ba4f9448937ed3a"></a>
> 
> ```bash
> # 주석 1
> # 주석 2
> # 주석 3
> ```

- <code>&#35;</code>&#58; 한줄 주석

- <code>//</code>&#58; 한줄 주석

- <code>/&#42;</code>&#58; 여러줄 주석

</details>

<details>
<summary>문자 인코딩 및 줄바꿈</summary>

- Terraform <strong><u>설정 파일은 항상 </u></strong><strong><u><code>UTF&#45;8</code></u></strong><strong><u>로 인코딩</u></strong>되어야 한다&#46; 

- UTF&#45;8의 구분 기호는 모두 ASCII 문자이지만,  <u>식별자, 주석 및 문자열 값에 비ASCII 문자 허용</u>

-  관용적인 스타일로 <code>Unix</code> 규칙을 사용한다&#46; 따라서 CRLF 줄 바꿈을 LF로 자동 변환될 수 있다&#46;

</details>

<a id="376eda9b0fe18040aa80d70c93e1dbcc"></a>

### JSON Configuration Syntax

[JSON Configuration Syntax &#45; Configuration Language &#124; Terraform &#124; HashiCorp Developer]()

- 해당 강의에서는 다루지 않음

<a id="2c1eda9b0fe180a79e84d425eb80ff8a"></a>

## 스타일 가이드

[Style Guide &#45; Configuration Language &#124; Terraform &#124; HashiCorp Developer]()

> 📖 
> 
> <a id="376eda9b0fe1809fabc9c83bdd631fc0"></a>
> 
> Terraform에서 코드 작성, 디렉터리 구조화, 구성 테스트 시 다양한 옵션 제공한다&#46;
> 
> <a id="377eda9b0fe180308933fb4354419567"></a>
> 
> 일반적으로 권장되는 몇 가지 패턴이 존재하며 해당 섹션에서는 조직의 스타일 가이드를 개발할 때 <u>고려해야 할 사항</u>과 <u>모범 사례</u>를 다른다&#46; 

<a id="377eda9b0fe1801393dbdc5d32da8e30"></a>

### 코드 스타일 

> Terraform 코드를 일관된 스타일로 작성하며 가독성과 유지보수성이 향상된다&#46; 

- 코드 커밋 전  &#45; <code>terraform fmt</code>, <code>terraform validate</code> 실헹

- 린터(ex&#46; <a href="https://github.com/terraform-linters/tflint">TFLint</a>) &#45; 코딩 모법 사례를 준수하도록 설정

-  주석 코멘트 &#45;  모두 <code>&#35;</code>을 권장

- 리소스 이름 &#45;  <code>명사</code>로 표현하며 <code>리소스 유형</code>은 포함 ❌

- 참조하는 리소스 → 종속 리소스 정의

- 모든 변수, 출력 &#45;  <u>유형</u>과 <u>설명</u> 포함

- 변수와 로컬 value에 대한 남용 금지

- 기본 provider 구성 항상 포함

- <code>count</code>, <code>for&#95;each</code>는 가급적 적제 사용

<a id="377eda9b0fe18085b240e716558a97ea"></a>

### 코드 포멧팅

- 2칸 들여쓰기

<details>
<summary>인수(arguments) 등호 정렬</summary>

<a id="377eda9b0fe18079adaefc23224507df"></a>

```python
ami           = "abc123"
instance_type = "t2.micro"
```

- 위와 같이 등호(<code>=</code>) 기준으로 인수(변수) 정렬

</details>

<details>
<summary>인수, 블록 → 인수 위, 블록 하위</summary>

<a id="377eda9b0fe180e7af5bf89f8d5343d6"></a>

```python
resource "aws_instance" "example" {
  ami           = "abc123"
  instance_type = "t2.micro"

  network_interface {
    # ...
  }
}
```

- 인수(변수) 맨 위, 블록 그 하위로 구성한다&#46; 

</details>

<details>
<summary>메타 인수, 메타 인수 블록</summary>

<a id="377eda9b0fe180a5a394c0432ca7fd5e"></a>

```python
resource "aws_instance" "example" {
  # meta-argument first
  count = 2

  ami           = "abc123"
  instance_type = "t2.micro"

  network_interface {
    # ...
  }

  # meta-argument block last
  lifecycle {
    create_before_destroy = true
  }
}
```

- 메타 인수 (<code>count</code>&#46;&#46;&#46;)  &#45; 맨위

- 메타 인수 블록(<code>lifecycle</code> …) 맨 아래

</details>

<details>
<summary><code>terraform fmt</code></summary>

<a id="377eda9b0fe18067a400e0117bbdfd74"></a>

```python
terraform fmt
```

- 해당 권장사항으로 terraform 포멧을 변경해준다&#46; (formatting)

- 버전 관리(커밋 전) 사용 권장

</details>

<a id="2c1eda9b0fe180cdaae6f83b955a7408"></a>

### 코드 유효성 검사 (validation)

<a id="2c1eda9b0fe180d38330e2ef929a07a9"></a>

```python
terraform validate
```

- configuration 구문이 올바르며, 내부적으로 일관성이 있는 지 확인한다&#46;

- 값의 유효성 여부는 판단하지 않지만, 올바른 타입인지 검사한다&#46; 

- 자주 실행해도 안전하다&#46; 

- 커밋 전 훅으로 정의하거나 CI/CD 파이프라인으로 포함아여 자동 검증되도록 할 수 있다&#46; 

<a id="377eda9b0fe180099c35e0dda0d85b6d"></a>

### 파일명

- <code>backend&#46;tf</code>
    - 백엔드 인프라 구성 정보를 정의한 파일

    - 백엔드 구성을 Terraform 및 공급자 버전 관리 구성과 분리

- <code>main&#46;tf</code>
    - 모든 리소스 및 데이터 소스 블록이 포함된 파일

- <code>output&#46;tf</code>
    - 모든 출력 블록에 대해 정의한 파일 (알파벳 순 정렬)

- <code>provider&#46;tf</code>
    - 모든 <code>provider</code> 블록, 설정 내용이 포함된 파일

- <code>terraform&#46;tf</code>
    - <code>required version</code>, <code>required providers</code>를 정의한 단일 terraform 블록을 포함한 파일

- <code>variables&#46;tf</code>
    - 모든 <strong><u>변수 블록</u></strong>을 포함한 파일 (알파벳 순 정렬)

- <code>locals&#46;tf</code>
    - 모든 <strong><u>로컬 값</u></strong>를 포함한 파일

    - 자세한 내용은 <a href="https://developer.hashicorp.com/terraform/language/style#local-values">local value</a> 참조 

- <code>override&#46;tf</code>
    - 구성에 대한 재정의(override)가 포함된 파일

    - 재정의(override) 파일은 코드의 가독성을 떨어뜨리므로, 가급적 사용 자제
        - 사용 시 원래 리소스 정의를 주석으로 명시

        - 자세한 내용은 <a href="https://developer.hashicorp.com/terraform/language/files/override">override files</a> 참조

> 🤔 
> 
> - 코드베이스가 커짐에 따라 위 파일로는 유지보수 및 탐색이 어려워 질 수 있다&#46; <br>이를 해결하기 위해 리소스, 데이터 소스 등을 논리적인 그룹별로 나눠 별도의 파일로 구성하는 것이 좋다&#46; 
> 
> - 예를 들어, 웹 애플리케이션에 네트워킹, 스토리지 및 컴퓨터 리소스를 분리하려는 경우 아래와 같은 파일을 생성할 수 있다&#46; 

- <code>network&#46;tf</code>
    - VPC, 서브넷, 로드 밸런서 및 기타 모든 네트워킹 리소스가 포함된 파일

- <code>storage&#46;tf</code>
    - 객체 저장소 및 관련 권한 구성이 포함된 파일

- <code>compute&#46;tf</code>
    - 컴퓨팅 인스턴스가 포함된 파일

<a id="377eda9b0fe1809b93faf6ab453cc677"></a>

### 린팅 및 정적 코드 분석

- Terraform에는 내장 린터가 없지만, 외부 린팅 도구를 사용하여 코드 표준을 준수할 수 있다&#46;
    - TFLint 많이 사용
        [GitHub &#45; terraform&#45;linters/tflint&#58; A Pluggable Terraform Linter]()

- 린터는 정적 코드 분석을 통해 코드를 일련의 규칙과 비교한다&#46; 

- 대부분의 린터는 기본 규칙 set을 제공하며, 사용자가 직접 규칙 작성도 가능하다&#46;

<a id="377eda9b0fe180d79288df811a35871b"></a>

### 리소스 이름 지정

<a id="377eda9b0fe18024a40dd7f2daadc79a"></a>

```python
# ❌ 잘못된 사용
resource aws_instance webAPI-aws-instance {...}

# ✅ 올바른 사용
resource "aws_instance" "web_api" {...}
```

- configuration 내 모든 리소스는 <strong><u>고유한 이름</u></strong>을 가져야 한다&#46; 

- 일관성 및 가독성을 위해 <code>명사</code>를 사용하고 <strong><u>단어는 밑줄로 구분</u></strong>한다&#46; 

- 리소스 주소에 이미 리소스 유형이 포함된다&#46; 따라서 <strong>식별자에는 리소스 유형을  포함하지 않</strong>는다&#46; 

- 리소스 유형과 이름은 <code>큰타옴표(””)</code>로 묶어 표현한다&#46;

<a id="377eda9b0fe180099a1acbcaad4241a9"></a>

### 리소스 순서

> 🤔 
> 
> <a id="377eda9b0fe180cc8877c777b9922066"></a>
> 
> 구성 코드 내 리소스들의 순서는 실제 테라폼 인프라 구성 시에 영향을 주지 않는다&#46;<br>따라서 가독성 있게 순서를 배치하는 것이 중요하다&#46; 
> 
> - 리소스 간의 종속성을 기반으로 생성 순서를 결정한다&#46; 

> /icons/iterate_gray.svg 
> 
> <a id="377eda9b0fe1805a942ad2cb1b0a51f0"></a>
> 
> 리소스 매개변수 순서
> 
> <a id="377eda9b0fe180bf992eff9ffddb0fb9"></a>
> 
> 리소스 매개변수에 대해 일관된 순서를 따르는 것이 좋다&#46; 
> 
> 1. <code>count</code>, <code>for&#95;each</code>  메타 인수
> 
> 1. 리소스별 비블록 매개변수
> 
> 1. 리소스별 블록 매개변수
> 
> 1. <code>lifecycle</code>블록
> 
> 1. <code>depends&#95;on</code> 매개변수

- 데이터 소스를 참조하는 리소스 와 함꼐 정의하는 것이 좋다&#46; <br>이때, 참조하는 리소스보다 먼저(위에) 정의한다&#46; 
    <details>
    <summary>예시) <code>aws&#95;ami</code> 와 <code>aws&#95;availability&#95;zone</code>을 의존하는 <code>aws&#95;instance</code> </summary>

    <a id="377eda9b0fe180b58b82e9ce5eeaf0bb"></a>

    ```python
    data "aws_ami" "web" {
      ##...
    }

    data "aws_availability_zones" "available" {
      ##...
    }

    resource "aws_instance" "web" {
      ami               = data.aws_ami.web.id
      availability_zone = data.aws_availability_zones.available.names[0]
      ##...
    }
    ```

    </details>

<a id="377eda9b0fe180d29b0bda5023bfe56b"></a>

### 변수 (Variables)

> 🤔 
> 
> <a id="377eda9b0fe180ecb35be5298af84fcc"></a>
> 
> 리소스 설정에 변수를 사용할 지 여부는 <strong><u>해당 매개변수가 베포 간에 변경될 가능성이 있</u></strong>는지 고려해야 한다&#46;
> 
> <a id="377eda9b0fe180168e3df5d38a654876"></a>
> 
> 변수를 사용하면 모듈 유연성이 향상되지만, <strong>과도하게 사용 시 코드 가독성이 떨</strong>어질 수 있다&#46;

> /icons/iterate_gray.svg 
> 
> <a id="377eda9b0fe180d9960ffbffa3468582"></a>
> 
> 변수 매개변수 순서
> 
> <a id="377eda9b0fe180b9bc25f1e7aa38b7ca"></a>
> 
> 변수의 매개변수에 대해서는 일관된 순서를 따르는 것이 좋다&#46; 
> 
> 1. <code>type</code>&#58; 유형
> 
> 1. <code>description</code>&#58; 설명
> 
> 1. <code>default</code>&#58; 기본값  (선택사항)
> 
> 1. <code>sensitive</code>&#58; 민감도 (선택사항)
> 
> 1. <code>validation</code>&#58; <a href="https://developer.hashicorp.com/terraform/language/block/variable#validation">유효성 검사 블록 </a>

- 변수 설명
    - 변수에 대해 <code>type</code>, <code>description</code> 작성

    - 변수가 optional 인 경우, 적절한 <code>default</code> 정의

- 민감한 값 &#45; 마스킹 처리
    - <code>password</code> 와 <code>private key</code> 와 같은 <strong><u>민감한 값</u></strong>인 경우, <code>sensitive=ture</code> 설정을 통해서 마스킹된 값으로 출력되도록 설정 가능하다&#46; 

    - store에는 원본 value로 저장되며 plan, apply 출력 시에 마스킹된 값으로 출력한다&#46; 

    - 자세한 내용은 <a href="https://developer.hashicorp.com/terraform/language/style#secrets-management">secrets management</a> 참조 

- 추가 유효성 검사 정의
    - 변수 값에 대한 추가 유효성검사 규칙을 정의하려는 경우 사용
        - 변수 값에 고유한 제한 요구사항이 있는 경우만 권장

    - ex)
        <a id="377eda9b0fe180619a42d4f302a2a2aa"></a>

        ```python
        variable "web_instance_count" {
          type        = number
          description = "Number of web instances to deploy. This application requires at least two instances."

          validation {
            condition     = var.web_instance_count > 1
            error_message = "This application requires at least two web instances."
          }
        }
        ```

        - Terraform 구성에 웹 인스턴스가 2개 필요한 경우 이를 강제하는 validation 블록 추가

<a id="377eda9b0fe1809580a2f790f22514c1"></a>

### Outputs

> ✏️ 
> 
> <a id="377eda9b0fe1805e8812ec180b30f23b"></a>
> 
> output value릍 활용해 명령줄에서 인프라에 대한 데이터 export 및 다른 Terraform 구성에서 참조 가능하도록 할 수 있다&#46; 
> 
> - 변수와 마찬가지로 각 출력에 대해 type, description 명시
> 
> - 다른 컨벤션과 동일하게 <code>고유한 식별자</code>, <code>명사</code>, <code>understore(&#95;)</code> 으로 출력명을 작성한다&#46;

> /icons/iterate_gray.svg 
> 
> <a id="377eda9b0fe18051a280f15c62ef0c46"></a>
> 
> 출력 매개변수 순서
> 
> 1. <code>type</code>&#58; 유형
> 
> 1. <code>description</code>&#58; 설명
> 
> 1. <code>value</code>&#58; 값
> 
> 1. <code>sensitive</code>&#58; 민감도 (선택사항)

<a id="377eda9b0fe18002bd88cd3a68d71c9d"></a>

```python
variable "db_disk_size" {
 type        = number
 description = "Disk size for the API database"
 default     = 100
}

variable "db_password" {
 type        = string
 description = "Database password"
 sensitive   = true
}

output "web_public_ip" {
 type        = string
 description = "Public IP of the web instance"
 value       = aws_instance.web.public_ip
}
```

<a id="377eda9b0fe180d19d0dfadadeb92683"></a>

### Local Value

> ✏️ 
> 
> <a id="377eda9b0fe180d79ebef9a3bdea8988"></a>
> 
> 로컬 변수를 사용해 <strong><code>표현식</code></strong>이나<strong> </strong><strong><code>값</code></strong>을 재사용
> 
> - 로컬 변수를 과도하게 사용하면 코드 이해가 어려워질 수 있으므로 신중하게 사용

> 💬 
> 
> <a id="377eda9b0fe180fdbdace208745700f1"></a>
> 
> local value 정의 
> 
> - 여러 파일에서 사용 → <code>locals&#46;tf</code>
> 
> - 특정 파일에서만 사용 → <code>해당 파일 맨위</code> 

<a id="377eda9b0fe1804bbb89de270d75fd3f"></a>

```python
locals {
  name_suffix = "${var.region}-${var.environment}"
}

resource "aws_instance" "web" {
  ami           = data.aws_ami.ubuntu.id
  instance_type = "t3.micro"

  tags = {
    Name = "web-${local.name_suffix}"
  }
}
```

- local value를 사용하여 지역 및 환경에 대한 접미사를 생성해 이를 여러 리소스에 재사용 가능

<a id="377eda9b0fe18066ae46e1832d8e23aa"></a>

### Provider 별칭 지정(aliasing)

> ✏️ 
> 
> <a id="377eda9b0fe180a3bdd6df553f6587b2"></a>
> 
> 같은 Terraform provider를 사용하는 여러 개의 provider 블록이 있을 경우 사용한다&#46;
> 
> - <code>리소스에 대한 provider 메타 인수</code> 와 <code>모듈에 대한 provider 메타 인수</code>는 사용할 provider를 명시한다&#46;

- ex) 단일 구성 내 여러 리전의 리소스들을 프로비저닝 하는 경우
    > 
    > 
    > <a id="377eda9b0fe180c498f5df74232ab8dd"></a>
    > 
    > <strong>provider 정의 규칙</strong>
    > 
    > - <code>alias</code> 매개변수를 정의하지 않은 provider block은 모두 기본 provider cofiguration이다&#46; 
    >     - 아래 <code>provider&#46;tf</code>의 <code>alias</code> 가 없는 구성 정보
    > 
    > - 항상 기본 provider configuration을 포함하고 모든 provider를 동일한 파일에 정의한다&#46; 
    > 
    > - provider instance가 여러 개 있어야 하는 경우, <strong>alias가 없는 default provider block을 먼저 정의</strong>해야 한다&#46;
    > 
    > - 기본 provider가 아닌 경우(non&#45;default provider), provider 블록의 첫번째 매개변수로 <code>alias</code> 를 정의해야 한다&#46; 

    - <code>provider&#46;tf</code>
        <a id="377eda9b0fe180debcedd8f823f3e07a"></a>

        ```python
        # 기본 provider configuration
        provider "aws" {
          region = "us-east-1"
        }

        provider "aws" {
          alias  = "west"
          region = "us-west-2"
        }
        ```

    - <code>main&#46;tf</code>
        <a id="377eda9b0fe180f88db5f639f0a63891"></a>

        ```python
        resource "aws_instance" "example" {
          provider = aws.west
          # ...
        }

        module "aws_vpc" {
          source = "./aws_vpc"
          providers = {
            aws = aws.west
          }
        }
        ```

<a id="377eda9b0fe1804ebd39e323ddfbd672"></a>

### Dynamic resource count

> ✏️ 
> 
> <a id="377eda9b0fe1800e89b5ed6ecac2b027"></a>
> 
> <code>for&#95;each</code> 와 <code>count</code> meta&#45;arguments는 실행(run&#45;time) 조건에 따라 하나의 리소스 블록부터 여러 리소스 블록까지 생성할 수 있다&#46; 
> 
> <a id="377eda9b0fe180a7845dcecc456cdaa2"></a>
> 
> 또한 중복 리소스 블록을 줄이고 유연한 코드 를 만들 수 있다&#46; 
> 
> - 자원이 거의 동일한 경우 → <a href="https://developer.hashicorp.com/terraform/language/meta-arguments#count"><code>count</code></a>
> 
> - 인수 중 정수가 아닌 고유한 값이 필요한 경우 → <a href="https://developer.hashicorp.com/terraform/language/meta-arguments#for_each"><code>for&#95;each</code></a>

> ❗ 
> 
> <a id="377eda9b0fe18082ab00c6938a8ccb10"></a>
> 
> 메타인수는 코드를 간소화하지만 복잡성을 증가시키므로 적절하게 사용해야 한다&#46;

<details>
<summary>ex 1) for&#95;each</summary>

<a id="377eda9b0fe180ed9657f935b2d3a979"></a>

```python
variable "web_instances" {
  type        = list(string)
  description = "A list of instances for the web application"
  default = [
    "ui",
    "api",
    "db",
    "metrics"
  ]
}
resource "aws_instance" "web" {
  for_each = toset(var.web_instances)
  ami           = data.aws_ami.webapp.id
  instance_type = "t3.micro"
  tags = {
    Name = "web_${each.key}"
  }
}
output "web_private_ips" {
  description = "Private IPs of the web instances"
  value = {
    for k, v in aws_instance.web : k => v.private_ip
  }
}
output "web_ui_public_ip" {
  description = "Public IP of the web UI instance"
  value       = aws_instance.web["ui"].public_ip
}
```

- <code>for&#95;each</code>를 사용해 정의된 문자열 <code>(”ui”, “api”, “ab”, “metrics”) </code>각각에 대해 aws&#95;instance 생성

- <code>each&#46;key</code>를 사용하여 각 인스턴스에 고유한 이름 지정

<details>
<summary><code>web&#95;private&#95;ips</code>출력은 for 표현식을 사용하여 인스턴스 이름과 해당 개인 IP 주소의 맵 생성</summary>

<a id="377eda9b0fe180dfa060e49976660b0e"></a>

```python
output "web_private_ips" {
  description = "Private IPs of the web instances"
  value = {
    for k, v in aws_instance.web : k => v.private_ip
  }
}
```

</details>

<details>
<summary><code>web&#95;ui&#95;public&#95;ip</code> 출력은 &#34;ui&#34; 키를 가진 인스턴스 직접 지정</summary>

<a id="377eda9b0fe1803a8c89ee0ebd1da88d"></a>

```python
output "web_ui_public_ip" {
  description = "Public IP of the web UI instance"
  value       = aws_instance.web["ui"].public_ip
}
```

</details>

- for&#95;each 메타 인수에 대한 더 많은 예제는 <a href="https://developer.hashicorp.com/terraform/language/meta-arguments#for_each">for&#95;each</a> 참조

</details>

<details>
<summary>ex 2)  count</summary>

> <code>count</code> 메타 인수를 사용해 <strong><u>1&#126;N 인스턴스 블록 생성</u></strong>이 가능하다&#46; 

<a id="377eda9b0fe18002b32fc73edf8d3a32"></a>

```python
variable "enable_metrics" {
  description = "True if the metrics server should be deployed"
  type        = bool
  default     = true
}

resource "aws_instance" "web" {
  count = var.enable_metrics ? 1 : 0

  ami           = data.aws_ami.webapp.id
  instance_type = "t3.micro"
  ##...
}
```

- <code>count &#45; 조건식</code>을 통해서 <strong><u>조건부 리소스 생성 </u></strong>가능

</details>

<a id="377eda9b0fe18084a49acee8546272e1"></a>

### <code>,gitignore</code> 관리 목록

[Terraform.gitignore](https://github.com/github/gitignore/blob/main/Terraform.gitignore)

<a id="377eda9b0fe1805fb72fcf61f86c94af"></a>

####  commit 금지 목록 ( <code>&#46;gitignore</code> 관리)

- <code>terraform&#46;tfstate</code>, <code>terraform&#46;tfstate&#46;&#42;</code>
    - 백업 상태 파일을 포함한 상태 파일

    - 상태 파일에는 비밀 정보 및 기타 민감한 정보가 포함될 수 있다&#46; 

    -  버전 관리 시스템은 Terraform 인스턴스 하나만 동시에 수정할 수 있도록 상태 파일을 잠그는 기능을 지원하지 않는다&#46;

- <code>&#46;terraform&#46;tfstate&#46;lock&#46;info</code>
    - Terraform이 <code>terraform apply</code>명령어를 실행할 때 자동으로 생성하고 삭제하는 파일로 <br><a href="https://developer.hashicorp.com/terraform/language/state/locking">state lock</a> 정보가 포함되어 있다&#46; 

- <code>&#46;terraform</code> 폴더
    - Terraform 프로바이더와 하위 모듈을 다운로드하는 디렉터리

- Saved plan files
    - <code>terraform plan</code>의 <code>&#45;out</code> 플래그 사용 시 생성되는 plan 파일

- <code>&#46;tfvars</code>
    - 민감 정보가 포함되는 파일

<a id="377eda9b0fe180a2b7d4fec9e09a9722"></a>

####  commit 가능한 목록

- 모든 Terraform 코드 파일들

- <code>&#46;terraform&#46;lock&#46;hcl</code>
    - <a href="https://developer.hashicorp.com/terraform/language/files/dependency-lock">dependency lock file</a>

- <code>&#46;gitignore</code>

- <code>README&#46;md</code>

<a id="377eda9b0fe180338499e0d5ed1eddcc"></a>

### Workflow 스타일

> ✏️ 
> 
> <a id="377eda9b0fe1809091f5da6903c7dc08"></a>
> 
> 예측 가능하고 안전한 Terraform 워크플로를 가능하게 하는 표준을 검토한다&#46; 
> 
> - 로컬 모듈 저장 위치&#58; <code>&#46;/modules/&#60;module&#95;name&#62;</code>

- Terraform, 프로바이더 및 모듈 <strong>버전 고정</strong>

- HCP Terraform 레지스트리를 사용할 때는 모듈 저장소 이름을 <code>terraform&#45;&#60;PROVIDER&#62;&#45;&#60;NAME&#62;</code>으로 나눠 지정

- <code>tfe&#95;outputs</code> &#45; <code>데이터 소스</code> or <code>공급자별 데이터 소스</code>를 사용해 <strong><u>두 상태 파일 간에 상태 공유</u></strong>

- <a href="https://developer.hashicorp.com/terraform/tutorials/cloud/dynamic-credentials"><code>dynamic provider credentials</code></a> 또는 HashiCorp Valuit 과 같은 <code>secrets manager</code>를 사용해 credentials 값 보호

- 모듈에 대한 테스트 작성

- HCP Terraform <a href="https://developer.hashicorp.com/terraform/cloud-docs/workspaces/policy-enforcement">정책 시행</a>을 통해 인프라 운영에 대한 guardrails 설정

<a id="377eda9b0fe1809f8c97f06cfc0c8122"></a>

### 버전 고정

> ✏️ 
> 
> <a id="377eda9b0fe1805eaba2e8b8c45f178d"></a>
> 
> provider 및 module 업그레이드로 인해 인프라에 의도치 않는 변경사항이 발생하는 것을 방지하려면 버전을 고정해 사용해야 한다&#46;
> 
> <a id="377eda9b0fe1802bb3e2edc36f046a6b"></a>
> 
> 이를 <code>required&#95;providers 블록</code>을 통해 provider 버전을 지정할 수 있다&#46; 
> 
> <a id="377eda9b0fe18055ab23fe5ae4c92faf"></a>
> 
> 안정성을 확보하기 위해 <strong><u>모듈을 </u></strong><strong><u><code>특정 주 버전 및 부 버전</code></u></strong><strong><u>으로 고정</u></strong>하는 것을 권장한다&#46; 
> 
> - 모듈이 주 버전 업데이트 외에는 호환성을 깨뜨리는 변경 사항을 도입하지 않는다고 확신하는 경우, 더 완화된 제한 가능
> 
> <details>
> <summary> 테라폼 블록에서 <code>required&#95;version</code> 속성을 사용하여 <strong><u>테라폼 바이너리의 최소 요구 버전을 설정</u></strong>하는 것이 좋다&#46; 이를 통해 모든 오퍼레이터가 구성에 필요한 모든 기능을 포함하는 테라폼 버전을 사용하는 것을 강제할 수 있다&#46; </summary>
> 
> <a id="377eda9b0fe180339741faa73556f4ef"></a>
> 
> ```python
> terraform {
>   ...
> 
>   required_version = ">= 1.7"
> }
> ```
> 
> </details>

> 📎 
> 
> <a id="377eda9b0fe1808ba6e8cedbec596892"></a>
> 
> <strong>추가 자료 </strong>
> 
> - <a href="https://developer.hashicorp.com/terraform/language/providers/requirements#requiring-providers">required provider</a>
> 
> - <a href="https://developer.hashicorp.com/terraform/language/providers/requirements#version-constraints">version constraints</a>

<a id="377eda9b0fe180c593a4e0fc7144a5a7"></a>

```python
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "5.34.0"
    }
  }

  required_version = ">= 1.7"
}
```

- <code>hashicorp/aws</code> provider 버전을 <code>5&#46;34&#46;0</code> 고정

- Terraform <code>1&#46;7</code>이상만 사용 가능

<a id="377eda9b0fe1801399c9d10eb971cfc5"></a>

```python
module "vault_starter" {
  source  = "hashicorp/vault-starter/aws"
  version = "1.0.0"
  ##...
}
```

- 레지스트리에서 가져온 모듈의 경우, 모듈 블록에서 버전 매개변수를 사용해 버전 고정

- 로컬 모듈의 경우, Terraform은 버전 매개변수 무시한다&#46;

<a id="377eda9b0fe180e3b476e65cfa3207ec"></a>

### 저장소 구조

> ✏️ 
> 
> <a id="377eda9b0fe18080ba42cada9d95c8a5"></a>
> 
> 논리적으로 관련된 리소스를 그룹화하여 저장소에 인프라 구성을 정리하는 것을 권장한다&#46; 
> 
> - 리소스를 그룹으로 분리하면 특정 작업에서 발생하는 장애로 인해 영향을 받을 수 있는 리소스의 수를 제한할 수 있다&#46;
> 
> - 예를 들어, 컴퓨팅, 네트워킹 및 데이터베이스 리소스가 필요한 웹 애플리케이션의 경우 단일 저장소를 사용할 수 있다&#46; 

- 단일 구조 
    <details>
    <summary>예시 1)  모든 모듈과 인프라 구성을 단일 모놀리식 저장소(모노레포)로 그룹화</summary>

    > 🤔 
    > 
    > <a id="377eda9b0fe1809f9e25dd01fb6ceaf7"></a>
    > 
    > <strong>단일 모놀리식 장소(모노레포) 그룹화 (단일 소스)</strong>
    > 
    > - 장점
    >     - 든 인프라 변경 사항을 단일 소스에서 추적 가능
    > 
    > - 단점
    >     - CI/CD 자동화 복잡성 증가
    > 
    >     - 코드 변경이 발생하면 전체 저장소에 대한 배포가 트리거되므로 <br>수정된 디렉터리만 대상으로 워크플로를 실행하는 것이 불가능함
    > 
    >     - 저장소에 접근 권한이 있는 사용자는 저장소 내의 모든 파일을 수정할 수 있으므로 세부적인 접근 제어가 어려워짐

    <a id="377eda9b0fe1803589d2cad7c9d08965"></a>

    ```python
    .
    ├── modules
    │   ├── function
    │   │   ├── main.tf      # contains aws_iam_role, aws_lambda_function
    │   │   ├── outputs.tf
    │   │   └── variables.tf
    │   ├── queue
    │   │   ├── main.tf      # contains aws_sqs_queue
    │   │   ├── outputs.tf
    │   │   └── variables.tf
    │   └── vpc
    │       ├── main.tf      # contains aws_vpc, aws_subnet
    │       ├── outputs.tf
    │       └── variables.tf
    ├── main.tf
    ├── outputs.tf
    └── variables.tf
    ```

    - 모노레포는 인프라 스택의 각 구성 요소에 대한 로컬 모듈 모음을 정의하고 이를 루트 모듈에 배포 가능하다&#46;

    </details>

- 다양한 환경
    <details>
    <summary>예시 2) 환경 별로 워크스페이스 분리</summary>

    > 🤔 
    > 
    > - 모든 환경에서 저장소의 <code>main</code>브랜치를 기준 소스로 사용
    > 
    > - 코드베이스 규모가 큰 경우, 상태 파일 크기를 줄이고 변경으로 인한 예상치 못한 결과를 최소화하기 위해 리소스를 여러 워크스페이스로 분산하는 것이 좋다&#46;
    > 
    > - HCP Terraform 및 Terraform Enterprise 사용자의 경우,각 환경 별로 별도의 워크스페이스 사용

    <a id="377eda9b0fe1805e92e5edbd5d453d23"></a>

    ```python
    ├── compute
    │   ├── main.tf
    │   ├── outputs.tf
    │   └── variables.tf
    ├── database
    │   ├── main.tf
    │   ├── outputs.tf
    │   └── variables.tf
    └── networking
        ├── main.tf
        ├── outputs.tf
        └── variables.tf
    ```

    - 환경별로 세 개의 워크스페이스를 생성

    </details>

    <details>
    <summary><a href="https://developer.hashicorp.com/well-architected-framework/operational-excellence/operational-excellence-workspaces-projects">Terraform 워크스페이스 및 프로젝트 모범 사례</a></summary>

    [Best Practices &#45; Workspaces &#45; HCP Terraform &#124; Terraform &#124; HashiCorp Developer]()

    </details>

    <details>
    <summary>예시 3) 모듈을 사용한 캡슐화</summary>

    <a id="377eda9b0fe1804695d2c9543c651cdd"></a>

    ```python
    ├── modules
    │   ├── compute
    │   │   └── main.tf
    │   ├── database
    │   │   └── main.tf
    │   └── network
    │       └── main.tf
    ├── dev
    │   ├── backend.tf
    │   ├── main.tf
    │   └── variables.tf
    ├── prod
    │   ├── backend.tf
    │   ├── main.tf
    │   └── variables.tf
    └── staging
        ├── backend.tf
        ├── main.tf
        └── variables.tf
    ```

    - 모듈을 사용하여 구성을 캡슐화하고 각 환경별로 디렉터리를 만들어 각 환경마다 별도의 상태 파일을 저장

    - 각 디렉터리의 구성은 해당 환경에 특화된 매개변수를 사용하여 로컬 모듈을 호출
        <a id="377eda9b0fe18099a318d53f45a1e10c"></a>

        → 각 환경에 대해 별도의 변수 및 백엔드 구성 관리

    </details>

<a id="377eda9b0fe18097b487d23e525aaa69"></a>

### <strong>통합 및 단위 테스트</strong>

[Tests &#45; Configuration Language &#124; Terraform &#124; HashiCorp Developer]()

[Write Terraform Tests &#124; Terraform &#124; HashiCorp Developer]()

<a id="377eda9b0fe18013b542c0b7efffedc3"></a>

Terraform 테스트는 모듈의 유효성을 검사하고 호환성을 깨뜨리는 변경 사항을 감지할 수 있도록 해준다&#46;

- 풀 리퀘스트 병합 전 검사 또는 자동화된 CI/CD 파이프라인의 필수 단계로 자동 트리거 가능
