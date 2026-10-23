---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 377eda9b-0fe1-8076-956a-edbe73e00191
title: Terraform Resource
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817b-9c95-d96fd53640c4
    title: CI/CD
  - id: 2c0eda9b-0fe1-8030-ab57-dc0df8148eeb
    title: Terraform 마스터클래스
  - id: 377eda9b-0fe1-8076-956a-edbe73e00191
    title: Terraform Resource
excerpt: 리소스 구성 [Configure a resource | Terraform | HashiCorp Developer]() 📖 Resource 는 가상 네트워크, 컴퓨팅 인스턴스, DNS 레코드와 같은 상위 구성 요소를 포함하여 Terraform으로 생성하고 관리하려는 모든 인프라 객체를 의미한다. - 상세 내용은 위 doc
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 2c0eda9b-0fe1-8030-ab57-dc0df8148eeb
created: 2026-06-06T06:11:26.519Z
updated: 2026-06-07T10:00:33.732Z
legacy_path: Main/CI-CD-d96fd53640c4/Terraform 마스터클래스-dc0df8148eeb/Terraform Resource-edbe73e00191/index.md
legacy_category: CI/CD
source_url: https://beautiful-college-c84.notion.site/377eda9b0fe18076956aedbe73e00191
---
<a id="377eda9b0fe180188ff2f6993f147929"></a>

## 리소스 구성

[Configure a resource &#124; Terraform &#124; HashiCorp Developer]()

> 📖 
> 
> <a id="377eda9b0fe180419cf7daba43354cfb"></a>
> 
> Resource 는 <code>가상 네트워크</code>, <code>컴퓨팅 인스턴스</code>, <code>DNS 레코드</code>와 같은 상위 구성 요소를 포함하여 <strong><u>Terraform으로 생성하고 관리</u></strong>하려는 <strong>모든 인프라 객체</strong>를 의미한다&#46; 
> 
> - 상세 내용은 위 docs 참고

> ☝🏻 
> 
> - <code>필수 조건 &#45; Provider 구성</code>
>     - 리소스 생성 시 <strong>필수적으로 Provider 선택 및 구성</strong>해야 한다&#46; 
>         - Provider는 프로비저닝 가능한 다양한 리소스 유형을 제공하는 Terraform 플러그인이다&#46; 
> 
>     - 대부분의 Provider는 원격 API에 액세스하기 위해 인증 설정, 버전 요구 사항, 기타 인수를 필요로 한다&#46; 

<a id="377eda9b0fe180279c2bf0a846337fbd"></a>

### 리소스 선언

> ✏️ 
> 
> <a id="377eda9b0fe180ef8476d504b8fcd042"></a>
> 
> <code>Terraform 리소스 선언(생성&#95;</code>
> 
> <a id="377eda9b0fe1801ca23af8762bc2e478"></a>
> 
> <strong>Terraform configuration에 </strong><strong><u>리소스 블록을 추가</u></strong><strong> 및  </strong><strong><u>필요한 인수 지정</u></strong>

<a id="377eda9b0fe180c2b6e4f7d1d87ccca8"></a>

```python
resource "aws_instance" "web" {  
		#...
}
```

- 위 설정을 적용한 후 <u>상태 파일에서의 해당 리소스 주소</u>는 <code>aws&#95;instance&#46;web</code>이다&#46;

<a id="377eda9b0fe180e9b74cda5e6468d710"></a>

### <strong>provider&#45;specific arguments (</strong>개별 provider 인자<strong>)</strong> 구성

> ✏️ 
> 
> <a id="377eda9b0fe180599263c50c1f55ad28"></a>
> 
> <code>resource</code> 블록의 공통 문법은 Terraform에서 정하지만, 그 안에 <strong><u>어떤 설정값을 필요한지는 provider에 따라 다르다&#46;</u></strong>
> 
> <a id="377eda9b0fe180ffbd7dff75d08aa596"></a>
> 
> 따라서 해당 provider가 제공하는 리소스 종류마다 다르기 때문에 <strong><u>관련 provider 문서를 확인 후  필요한 값을 설정</u></strong>해야한다&#46; 

<details>
<summary><strong>🧐 provider&#45;specific arguments</strong></summary>

> ✏️ 
> 
> <a id="377eda9b0fe180cc8d59e5399380dbcd"></a>
> 
> 특정 provider와 특정 resource type에서만 의미가 있는 설정값
> 
> - Terraform 문법은 같지만 내부 인수는 provider/resource마다 달라진다&#46; 

- ex) AWS EC2
    <a id="377eda9b0fe1801b8d0ec93d25b9ca75"></a>

    ```python
    resource "aws_instance" "app_server" {
      ami           = "ami-1234567890abcdef0"
      instance_type = "t2.micro"
    }
    ```

- ex) Docker 컨테이너 
    <a id="377eda9b0fe1801eb44cf153ab69ae6f"></a>

    ```python
    resource "docker_container" "nginx" {
      name  = "nginx-server"
      image = docker_image.nginx.image_id
      ports {
        internal = 80
        external = 8080
      }
    }
    ```

</details>

<a id="377eda9b0fe18005a417e7802f12b196"></a>

```python
# hcl 구조
resource "<RESOURCE_TYPE>" "<LOCAL_NAME>" {
  # 이 안의 대부분은 resource type마다 다름
}
```

<a id="377eda9b0fe1808eb5cad66516368b8f"></a>

```python
# 예제
resource "aws_instance" "app_server" {
  ami           = "ami-1234567890abcdef0"
  instance_type = "t2.micro"

  tags = {
    Name = "app-server"
  }
}
```

| 구분 | <strong>의미</strong> |
| --- | --- |
| <code>resource</code> | Terraform에게 “인프라 리소스를 만들겠다”는 선언 |
| <code>aws&#95;instance</code> | AWS provider가 제공하는 EC2 인스턴스 리소스 타입 |
| <code>app&#95;server</code> | Terraform 코드 안에서 부를 이름 |
| <code>ami</code>, <code>instance&#95;type</code>, <code>tags</code> | aws&#95;instance 리소스가 요구하거나 지원하는 설정값 |

- <code>ami</code> 와 <code>instance&#95;type</code> arguments는  aws provider 별로 다르다&#46;

<a id="377eda9b0fe180adbebed7e52a44f34d"></a>

### timeouts 작업 정의

> ✏️ 
> 
> <a id="377eda9b0fe18003ba52f1049e04a9a0"></a>
> 
> 일부 리소스 유형은 <strong><u>특정 작업이 완료되기 전에 시간 초과 오류가 발생하지 않</u></strong>도록 <strong><u>Terraform 대기 시간을 사용자가 지정</u></strong>할 수 있도록 <code>timeout arguments</code>를 지원한다&#46; 
> 
> - 단위 표시&#58; <code>시간&#58; h</code>, <code>분&#58; m</code>,  <code>초&#58; s</code>

<a id="377eda9b0fe180b0bec7d9cd27f8e356"></a>

```python
resource "aws_db_instance" "example" {
  # ...

  timeouts {
    create = "60m"
    delete = "2h"
  }
}
```

- <code>example</code> AWS 데이터베이스 인스턴스 생성 및 삭제 시의 <code>timeout</code> 설정

<a id="377eda9b0fe1804cb521c02836056ebd"></a>

### meta&#45;arguments 구성

[Meta&#45;arguments &#124; Terraform &#124; HashiCorp Developer]()

> ✏️ 
> 
> <a id="377eda9b0fe180859c2fc42ca0fd441d"></a>
> 
> Terraform에서는 <code>meta&#45;arguments</code>라 불리우는 <u>내장 인수를 제공</u>한다&#46;
> 
> - 자세한 내용은 <a href="https://developer.hashicorp.com/terraform/language/meta-arguments">Meta&#45;arguments</a> 참조

<a id="377eda9b0fe180158905d502415e42b2"></a>

### Custom conditions (사용자 정의 조건)

[resource block reference &#124; Terraform &#124; HashiCorp Developer]()

> ✏️ 
> 
> <a id="377eda9b0fe18009ac5dcd0848a2c27c"></a>
> 
> 사용자 정의 조건은 meta&#45;argument 블록 내 <code>precondition</code>, <code>postcondition</code>블록록으로 정의할 수 있다&#46;

| <strong>구분</strong> | <code>precondition</code> | <code>postcondition</code> |
| --- | --- | --- |
| 검사 시점 | 리소스 생성/변경 전 | 리소스 생성/변경 후 |
| 목적 | “이 작업을 시작해도 되는가?” | “작업 결과가 올바른가?” |
| 주로 검사하는 것 | 입력값, data source, 변수, 전제 조건 | 생성된 리소스의 실제 속성 |
| 실패 시 | 리소스 생성/변경을 시작하지 않음 | 결과 검증 실패로 이후 의존 리소스 진행 차단 |
| 예시 | AMI가 x86&#95;64인가? | EC2에 public DNS가 생겼는가? |

<details>
<summary>ex 1) </summary>

<a id="377eda9b0fe1800891b7d40611f0146d"></a>

```python
# 데이터 블록 - data 블록에서 ami-abc123 AMI의 ID를 가져온다. 
data "aws_ami" "example" {
  owners = ["amazon"]
  filter {
    name   = "image-id"
    values = ["ami-abc123"]
  }
}

# 리소스 블록 - precondition, postcondition 지정
resource "aws_instance" "example" {
  instance_type = "t3.micro"
  ami           = data.aws_ami.example.id

  lifecycle {
	  # 사전 조건 - 데이터 블록에서 가져온 AMI ID에는 아키텍처 속성으로 x86_64가 포함되어야 함
    precondition {
      condition     = data.aws_ami.example.architecture == "x86_64"
      error_message = "The selected AMI must be for the x86_64 architecture."
    }
		
		# 사후 조건 - EC2 인스턴스에 공용 DNS 호스트 이름이 할당되어야 함
    postcondition {
      condition     = self.public_dns != ""
      error_message = "EC2 instance must be in a VPC that has public DNS hostnames enabled."
    }
  }
}
```

- <code>precondition</code>, <code>postcondition</code> 으로 지정한 조건 중 하나라도 충족되지 않으면 명시한 <code>error&#95;message</code>를 반환한다&#46; 

- 예제 코드 동작
    1. AMI 조회

    1. <code>precondition</code>&#58; 그 AMI가 x86&#95;64 아키텍처인지 EC2 생성 전에 검사

    1. EC2 생성

    1. <code>postcondition</code>&#58; 만든 EC2에 public&#95;dns가 생겼는지 생성 후 검사

</details>

<details>
<summary>ex 2)</summary>

<a id="377eda9b0fe180b8a8d1ff1117f1e6f6"></a>

```python
data "aws_ebs_volume" "example" {
  filter {
    name = "volume-id"
    values = [aws_instance.example.root_block_device[0].volume_id]
  }
  lifecycle {
    # The EC2 instance will have an encrypted root volume.
    postcondition {
      condition     = self.encrypted
      error_message = "The server's root volume is not encrypted."
    }
  }
}
output "api_base_url" {
  value = "https://${aws_instance.example.private_dns}:8433/"
}
```

- 위 코드 동작
    1. aws&#95;instance&#46;example의 루트 볼륨 ID를 사용해서 EBS 볼륨 조회

    1. <code>postcondition</code>&#58; 조회된 EBS 볼륨의 encrypted 값이 <code>true</code>인지 검사

    1. <code>false</code>이면 <code>error&#95;message</code> 반환

</details>

<a id="378eda9b0fe1807984a7fe9d977ad943"></a>

### provider 구성별 별칭(alisas) 정의

> ✏️ 
> 
> <a id="378eda9b0fe180999937ced04e3b2c5d"></a>
> 
> Terraform은 <code>리소스 유형 이름</code>을 사용하여 사용할 provider를 결정한다&#46; 
> 
> - 관례적으로 리소스 유형 이름은 해당 공급자의 기본 로컬 이름으로 시작한다&#46; 
> 
> <a id="378eda9b0fe180418a15f97dda067ef5"></a>
> 
> configuration에 여러 provider의 구성을 선언하고 각 리소스가 서로 다른 구성을 사용 가능하다&#46;
> 
> - <strong><u>여러 provider 구성을 사용</u></strong>하는 경우, <a href="https://developer.hashicorp.com/terraform/language/block/resource#provider"><code>provider</code></a> meta&#45;argument를 사용해 <strong><u>provider 구성을 수동으로 선택</u></strong>할 수 있다&#46;

<details>
<summary><code>provider</code> meta&#45;argument</summary>

- 문법
    [resource block reference &#124; Terraform &#124; HashiCorp Developer]()

    <a id="378eda9b0fe180f4bea5f2ca9dc2f1ac"></a>

    ```python
    resource {
      provider = <provider>.<alias>
    }
    ```

- 예제
    [resource block reference &#124; Terraform &#124; HashiCorp Developer]()

    <a id="378eda9b0fe180239bacca60270fbb00"></a>

    ```python
    provider "google" {
      region = "us-central1"
    }

    provider "google" {
      alias  = "europe"
      region = "europe-west1"
    }

    resource "google_compute_instance" "example" {
      provider = google.europe
      # ...
    }
    ```

</details>

<a id="377eda9b0fe1804ab226ec6d0660c903"></a>

### 리소스 종속성 지정

<details>
<summary><code>depends&#95;on</code> meta&#45;argument</summary>



</details>

<a id="377eda9b0fe18093902dfc16e1822cfb"></a>

## 리소스 제거

<a id="377eda9b0fe18058b1c8e0a7c299689b"></a>

### 

<a id="377eda9b0fe180d7b63ec44eefff1a37"></a>

###
