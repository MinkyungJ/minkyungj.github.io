---
title: AWS Global Backbone for Data Center Migration and Global Expansion
tags: [AWS, Network Infra, Architecture, AWS Direct Connect]
date: 2023-09-12 15:00 +0900
categories: [AWS, AWS Infra]
toc: true
---

AWS Global Backbone에 대해 학습하기 전에 Backbone의 의미를 알아봅시다.

## ❗️ "Backbone" 이란?
Backbone은 네트워크에서 네트워크의 핵심을 가리키며, 일반적으로 여러 지리적 위치와 장치 간 데이터를 신속하고 안정적으로 전달하는 주요 네트워크 인프라의 일부를 의미합니다.

> "Backbone" 의 사용
> - 더 작은 지역 네트워크나 지점 간 연결에 사용됩니다.
> - 전체 네트워크의 핵심이므로, 고성능과 신뢰성이 요구됩니다.

---

### 💡 AWS Global Backbone (AWS Global Infra Network)
AWS는 클라우드 컴퓨팅 서비스를 제공하기 위해 전 세계적으로 분산된 데이터 센터와 네트워크 인프라를 구축하고 운영합니다.
이때, **AWS Global Backbone**은 데이터 센터를 연결하고 AWS의 다양한 클라우드 서비스와 리소스를 고객에게 제공하는 핵심 네트워크입니다.

이를 요약하자면, **AWS의 글로벌 네트워크 인프라를 활용하여 클라우드 기반 애플리케이션 및 서비스를 빌드하고 운영하는 것**을 의미한다고 할 수 있습니다.

> AWS Global Backbone의 기능
> - **빠른 데이터 전송 속도, 안정성, 내결함성**을 제공하여 고객이 AWS의 클라우드 서비스를 안정적으로 이용할 수 있도록 지원함
> - AWS Service의 **글로벌 확장** 가능
> -  **다양한 지역**에서 엔터프라이즈 수준의 애플리케이션과 데이터를 호스팅 가능

---

## 💡 기업, 국가가 애플리케이션을 활용하고있는 방식 

- **기업**
  - 여러 기업들이 Application을 실행하는 Data Center, Server Room, 등은 일반적으로 핵심 시스템이 여러 개의 소규모 Data Center에서 호스팅되는 소수의 중앙 대규모 Data Center가 혼합됨
  - 기업 자체 관리형 국제 광역 네트워크(WAN)를 구축
    - 이를 통신 제공업체의 서비스로 계약하여 여러 사이트 간의 연결을 활성화하는 접근 방식 사용
- **국가**
  - 같은 국가의 Local Data Center에서 실행되는 Application과 Remote Data Center에서 실행되는 Application에 접근

---

## ❗️ AWS Global Backbone 활용
AWS Global Backbone Architecture을 활용하면 AWS와 On-prmise Hosting Application 모두에 액세스 가능하며 다양한 국가 및 대륙에 있는 고객 사이트 간의 연결을 제공한다.

### 💡 AWS Global Backbone 활용 예시
1. **고객 사이트를 상호 연결하는 Global Wan**<br>
한국의 한 기업이 자사의 핵심 시스템을 호스팅하는 중앙 Data Center을 보유하고있고, 이 회사는 인도에서 호스팅하는데 필요한 Application을 실행하기 위해 뭄바이에 공간을 임대했습니다. 고객은 Global Wan을 통해 뭄바이 Data Center에서 실행되는 여러 Application과 한국에서 실행되는 Application의 핵심 시스템에 접근합니다.
![Global_Wan](https://github.com/MinkyungJ/MinkyungJ.github.io/blob/main/_posts/Global_Wan.png?raw=true)*고객 사이트를 상호연결하는 Global Wan을 갖춘 초기 Architecture*

2. **AWS Global Network을 통한 Application Access**<br>
고객은 뭄바이의 Data Center에서 AWS Mumbai Region으로 Application을 마이그레이션합니다. 인도에 있는 고객은 Application은 물론 한국 Data Center에서 실행되는 핵심 시스템에도 접근해야합니다.
📝 **AWS Mumbai Region으로 연결할 때, 사용하는 설정 방식**
  - AWS Direct Connect(DX) 사용
    - 고객은 AWS 인프라를 통해 전송되도록 허용하는 AWS Transit Gateway(TGW)를 사용하여 Direct Connect Gateway(DXGW)에 연결합니다.
    - AWS Transit Gateway 을 통해 고객은 동일한 지역에 있는 여러 VPC 또는 VPN에 대한 단일 연결을 관리할 수 있습니다.
  - AWS Site-to-Site VPN 사용
📝 **WAN 비용 최적화를 위한 피어링 기능 사용**
WAN 비용을 최적화하기 위해 고객은 AWS Transit Gateway Region 간 피어링 기능을 활용하여 AWS Mumbai Region의 AWS Transit Gateway를 AWS Korea Region의 AWS Transit Gateway에 연결합니다.
- Region간 Transit Gateway 피어링을 사용하는 트래픽은 다음과 같은 특징을 가지고 있습니다.
  - 항상 **암호화**된다. 
  - AWS Global Network에 유지된다.
  - 퍼블릭 인터넷을 통과하지 않는다.
- Transit Gateway 피어링을 사용하면 대륙간 통신이 가능합니다.
![Application_Access](https://github.com/MinkyungJ/MinkyungJ.github.io/blob/main/_posts/Application_Access.png?raw=true)*AWS Global Network를 통해 고객 사이트에서 AWS Region 및 온프레미스 Application 접근*

3. **Global Expansion with AWS Global Network**<br>
고객이 해외로 확장함에 따라서 새로운 해외 사무소에서 **AWS Global Network**를 통해 다른 고객 사이트 또는 AWS Region까지 접근할 수 있게됩니다.
- 대역폭 요구 사항에 따라 고객은 AWS DX를 사용하여 가장 가까운 AWS Region으로 이동하고 TGW Region 간 피어링을 활용할 수 있습니다.
- VPN 기반 연결이 대역폭 및 사용자 경험 요구 사항을 충족하는 사이트의 경우, 고객은 AWS Global Accelerator를 사용하여 가속화된 사이트 간 VPN을 활용할 수 있습니다.

> 이와 같은 Architecture를 사용한다면, 수천 개의 사이트를 상호 연결하고 AWS Global Network를 사용하여 온프레미스 또는 AWS에서 실행되는 Application에 액세스할 수 있습니다.

![Global_Expansion](https://github.com/MinkyungJ/MinkyungJ.github.io/blob/main/_posts/Global_Expansion.png?raw=true)*AWS Global Network를 통해 고객 사이트에서 AWS Region 및 온프레미스 Application 접근*

#### 💡 Architecture 채택 시, 고려할 점
1. TGW 연결, VPN / DX 연결 : 고정된 시간 당 비용 발생
2. TGW, AWS OUT 및 리전을 통과하는 트래픽에 따라 달라지는 사용량 기반 구성 요소 존재
3. 실제로 제공하는 업체에서는 고정된 모델 가격으로 네트워크를 제공하는 경우가 많음

> 따라서 동일한 Region에서 사이트 수가 많은 고객의 경우, 해당 지역 Wan 설정을 고려하는 것이 좋고, 위의 활용 예시와 같이 국제 연결이 필요할 때에는 AWS Global Network를 사용하는 것이 좋습니다.

---

## 📔 블로깅을 마치며
Data Center에서 실행하는 애플리케이션을 AWS로 마이그레이션하고 AWS Global Network를 사용하여 Wan Architecture 설계와 비용적인 측면 모두 최적화 할 수 있다는 것을 배웠습니다. 또한, TGW 지역 간의 Peering 기능을 통해 비용 최적화 및 글로벌 확장의 촉진 및 온프레미스 / AWS 워크로드 모두 접근할 수 있는 Architecture를 설계할 수 있다는 것을 배웠습니다. 다음에는 AWS의 보안 환경 구축에 대해 공부해볼 생각이다.

---

## ❗️ Reference
> AWS Blog About Global Expansion & Data Center Migration
<https://aws.amazon.com/ko/blogs/architecture/leveraging-aws-global-backbone-for-data-center-migration-and-global-expansion/>