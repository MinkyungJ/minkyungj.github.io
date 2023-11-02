---
title: Building a self-service security environment
tags: [AWS, Network Infra, Secure Environment]
date: 2023-09-19 22:00 +0900
categories: [AWS, AWS Infra]
toc: true
---

> CS 스터디이 참여할 때도 그렇고 DevOps Engineer가 되기 위해 학습을 하면서 보안의 중요성에 대해서 점점 더 심각하게 받아들이고 있다. 진지하게 학습하기전에 개발자는 마냥 창의적으로 꼼꼼하게 개발에 착수하는 줄만 알았지만, 기업의 요구사항이나 프로젝트를 진행하며 보안이 차지하는 비율과 중요성에 대해 점점 더 심각하게 생각하게 된다. <br>
이번에는 AWS Skill Builder을 통해 학습하며 **보안 전략 구현에 대한 솔루션**을 학습해보려한다.

---

모든 기업이 보안에 예민하겠지만, 은행과 같이 규제가 엄격한 부문에 속한 기업들은 보안 상태를 최신으로 유지하며 그를 준수하고 지속적으로 변화에 대비할 수 있도록 노력할 것입니다.<br>
은행을 예로 들자면, ATM과 오프라인 창구에서 돈을 관리하던 과거와 다르게 인터넷 뱅킹 및 디지털 참여의 전환이 크게 일어나는 만큼 보안의 요구치가 크게 상승했습니다.<br>
이런 경우에, **보안과 규정 준수**가 금융 서비스 고객의 최우선 과제이기 때문에 빠르게 혁신하고 보안을 유지하는 것이 필수적입니다.

이러한 해결책 중, AWS Skill Builder에서 제공하는 솔루션 중 하나인 **머신러닝 솔루션**에 대해 먼저 학습해보려고 합니다.

---

## 머신러닝 솔루션 (ML Solution)

아래의 아키텍처는 고객을 위해 개발한 ML Solution으로 운영, 보안 성능과 감독 기관의 규제 및 규정 요구사항을 충족하도록 설계되었습니다.
![ML_Solution](https://github.com/MinkyungJ/MinkyungJ.github.io/blob/main/_posts/ML_Solution.png?raw=true)*ML_Solution*

이 ML Solution은 Security Guardrail과 AWS CloudFormation Template을 사용하여 구축 및 자동화되고 **Service Catalog**를 통해 추상화됩니다.
> Service Catalog?
> - Service Catalog를 사용하면, 사용자가 승인된 IT 서비스를 신속하게 배포하여 리소스 프로비저닝 중에 관리, 준수 및 보안 모범 사례를 적용할 수 있습니다.

또한, Amazon SageMaker, S3, RDS를 활용하여 고급 ML 모델 개발을 가능하게 합니다. 이 모델은 보안이 가장 중요하므로 S3의 데이터는 RDS의 열에 대한 클라이언트 측 암호화 및 열 수준 암호화를 사용하여 암호화되며 사용자는 지속적인 규정 준수를 위해 **AWS Config 규칙**을 통해 보안 제어를 편성합니다.
> AWS Config?
> - 리소스의 구성 및 관계에 대한 지속적인 진단 및 평가를 수행합니다.
> - 계정의 리소스를 검색하거나 타사의 리소스 구성 데이터를 AWS Config에 게시하고 기록, 변경 사항을 캡쳐항 운영 문제를 신속하게 해결합니다.
> - 규정 준수 요구 사항을 코드화하고 수정 작업을 진행하여 조직 전체의 리소스 구성 평가를 자동화합니다.

---

### 1. 컴퓨팅 및 네트워크 격리 솔루션 (Compute and network isolation)

최고 수준의 보안을 달성하면서 새로운 ML 모델을 신속하게 탐색할 수 있도록 분리된 VPC를 사용하여 인프라를 격리하고 보안 그룹별로 액세스 제어가 가능합니다.

#### ❗️ 이 솔루션의 핵심 - Amazon SageMaker (Compute and network isolation)
Amazion SageMaker : ML 모델을 신속하게 구축, 훈련 및 배포할 수 있는 기능을 제공하는 **완전 관리형 서비스**
- 이때의 완전 관리형 서비스는 장점이자 단점이 될 수 있습니다.
- Amazion SageMaker은 다음과 같은 기능을 제공하는 관리형 Juypter 노트북입니다.
  1. 데이터 준비 및 처리
  2. 모델 학습을 위한 코드 작성
  3. SageMaker 호스팅에 모델 배포
  4. 모델 테스트 또는 검증

#### 💡 Amazon SageMaker?

학습을 하다가, Amazon SageMaker가 궁금해서 더 자세하게 알아보았다.
**Amazon SageMaker**는 완전 관리형 기계 학습 서비스로, SageMaker를 사용하면 데이터 과학자와 개발자는 기계 학습 모델을 빠르고 쉽게 구축 및 교육한 다음 이를 프로덕션에 바로 사용할 수 있는 호스팅 환경에 직접 배포할 수 있다고합니다. **한마디로, 개발한 머신러닝 모델들을 쉽고 빠르게 build하고 train해서 프로덕션 단계가지 배포해주는 머신러닝 서비스이다.** <br>
뿐만 아니라, 같은 애플리케이션 환경에서 build, train, deploy해주는 **SageMaker Studio**와 **SageMaker Studio Lab**과 같은 서비스 또한 제공된다. 
> SageMaker에 대해 간단하게 소개해봤지만, 자세한 것은 <https://aws.amazon.com/ko/sagemaker/> 에서 확인해보자.

##### 💡 Amazon SageMaker의 작동 방식

![SageMaker](https://github.com/MinkyungJ/MinkyungJ.github.io/blob/main/_posts/SageMaker.png?raw=true)*SageMaker*

크게는 <span style="color:yellowgreen">'Generate Example Data'</span> -> <span style="color:indigo">'Train Model'</span> -> <span style="color:orange">'Deploy the Model'</span> 단계로 작동한다.

1. <span style="color:yellowgreen">Generate Example Data</span> : 전처리될 데이터 준비
2. <span style="color:indigo">Train Model</span> : 모델 훈련과 평가 모두 포함되어 있으며, 빠르고 즉시 사용 가능한 솔루션을 위해 SageMaker가 제공하는 알고리즘 사용 가능
3. <span style="color:orange">Deploy the Model</span> : 일반적으로 모델을 애플리케이션과 통합하고 배포하기 전에 모델을 다시 엔지니어링함

> 자세한 내용은 <https://docs.aws.amazon.com/sagemaker/latest/dg/how-it-works-mlconcepts.html> 에서 확인해보자.

ML 솔루션에서 노트북은 AWS Service와의 비공개 통신을 가능하게하는 VPC Endpoint 이외의 연결 없이 **격리된 VPC**에서 실행됩니다. VPC EndPoint Policy과 함께 사용하면 노트북을 사용하여 해당 서비스에 대한 액세스 제어가 가능합니다. <br>
또한, SageMaker 노트북은 조건키를 사용하여 AWS Organizations이 소유한 리소스와만 통신할 수 있도록 사용되며, AWS Organizations은 엄격한 규정 준수를 위한 거버넌스를 제공하며, 리소스 기반 정책의 조건 키를 사용하여 계정에서 IAM 보안 주체에 대한 액세스를 쉽게 제한할 수 있습니다.

#### 💡 AWS:PrincipalOrgID 조건 키

> 조건이란?
정책이 권한을 부여하거나 거부하는 특별한 상황을 지정하는 데 사용할 수 있는 선택적 IAM 정책 요소로, 조건 키와 연산자 및 조건 값이 포함됩니다.
조건은 두 가지 유형이 존재합니다.
- 서비스별 조건 : AWS 서비스의 특정 작업에만 적용
  - 조건 키 ec2:InstanceType은 특정 EC2 작업 지원
- 전역 조건 : 모든 AWS 서비스 전반에 걸쳐 모든 작업 지원

**AWS:PrincipalOrgID 조건 키**
이 조건 키를 사용하여 리소스 기반 정책의 Principal 요소에 필터를 적용할 수 있고, StringLike 와 같은 문자열 연산자를 사용하여 AWS 조직 ID를 지정할 수 있습니다.
- aws:PrincipalOrgID
- Description : 리소스에 액세스하는 주체가 조직의 계정에 속하는지 확인합니다.
- Operator(s) : 모든 문자열
- Value : 모든 AWS Organizations ID

---

### 2. 데이터 보호

AWS Key Management Service (SSE-KMS) 암호화 에 저장된 **AWS KMS 키**와 함께 서버 측 암호화를 사용하여 저장 데이터를 보호합니다.
> SSE-KMS는 KMS를 활용하고 KMS 키와 함께 봉투 암호화 전략을 사용합니다. 
> - 봉투 암호화는 데이터 키로 데이터를 암호화한 다음 다른 키인 KMS 키를 사용하여 해당 데이터 키를 암호화하는 방식입니다. 
> - KMS 키는 KMS에서 생성되며 KMS를 암호화되지 않은 상태로 두지 않습니다.

이 방식을 사용하면, KMS 키에 대한 액세스와 모든 액세스 로깅 및 Amazon CloudTrail 에 대한 키 액세스 시도에 대한 세부적인 제어가 가능합니다. <br>
또한, KMS 키의 수명이 AWS Config에 의해 추적되고 정기적으로 교체되며, AWS 리소스 구성을 지속적으로 모니터링하고 기록하여 배포된 AWS 리소스의 구성을 평가, 감사 및 평가할 수 있습니다. <br>
이를 통해, 원하는 구성에 대해 기록된 구성을 **자동**으로 평가할 수 있습니다.

---

### 3. 지속적인 규정 준수

지속적인 규정 준수 접근 방식을 채택하여 구성 변경이 규정 준수 상태를 위반하려고 시도하는 경우 아키텍처의 규정 준수 상태를 지속적으로 평가하고 자동으로 교정합니다.
> 이를 위해 AWS Config 및 구성 규칙을 사용하여 리소스가 정의된 정책을 준수하도록 구성되었는지 확인
> - AWS Lambda는 AWS Config에 포함된 규칙을 확장하는 사용자 지정 규칙 세트를 구현하는 데 사용됨

---

### 4. 데이터 유출 방지

모든 계정에서 VPC 흐름 로그가 활성화되어 각 VPC의 네트워크 인터페이스로 들어오고 나가는 IP 트래픽에 대한 정보를 기록하고, 데이터 유출 시도를 나타낼 수 있는 비정상적이고 예상치 못한 아웃바운드 연결 요청을 감시할 수 있습니다. 
> **Amazon GuardDuty**는 VPC 흐름 로그, AWS CloudTrail 이벤트 로그 및 DNS 로그를 분석하여 AWS 환경 내에서 예상치 못한 잠재적으로 악의적인 활동을 식별합니다.
> - EX> GuardDuty 는 알려진 명령 및 제어 서버와 통신하는 손상된 EC2 인스턴스를 감지할 수 있습니다.

---