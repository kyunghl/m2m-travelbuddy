# Application Modernization

Agenda

- Sample Application 소개
- Monolith - TravelBuddy 마이그레이션
  - 이론: Monolith란?
  - 실습 환경 구성
  - 실습 1: TravelBuddy 애플리케이션 컨테이너화
  - 실습 2: Database 구성
  - 실습 3: TravelBuddy 애플리케이션을 EKS에 배포
- Microservice - HotelSpecial 애플리케이션
  - 이론: Microservice란?
  - 실습 B: Strangler Fig Pattern - FlightSpecial 애플리케이션을 분리

## Sample Application 소개

이번 실습을 진행하면서 우리는 [TravelBuddy.zip](https://workshops.devax.academy/monoliths-to-microservices/module1/files/TravelBuddy.zip)라는 가상의 웹 애플리케이션을 활용하여 마이크로서비스 아키텍처로 전환하는 예제로 사용할 것입니다.

![travelbuddy.png](./docs/assets/travelbuddy.png)

이 실습을 통해 다음의 Topic을 다룰 것입니다.

- AWS 환경에서 개발 및 배포 등의 작업을 수행하기 위해서 Cloud9을 사용
- TravelBuddy 애플리케이션을 컨테이너화하고 컨테이너 이미지를 ECR에 푸시
- EKS 클러스터를 생성하고 monolith인 TravelBuddy를 배포
- Monolith 개념을 이해하고 TravelBuddy 애플리케이션을 분석하여 개선 방향을 검토
- Microservice 개념을 이해하고 HotelSpecial 애플리케이션을 통해 실전 학습
- FlightSpecial 애플리케이션을 직접 개발하면서 학습 내용을 복습

## TravelBuddy 마이그레이션

이 실습에서는 애플리케이션 현대화의 첫 번째 단계로서 기존 on-premise에서 운영하던 가상의 웹 애플리케이션을 AWS 클라우드 환경으로 옮겨서 배포합니다. 이를 통해 우리는 점진적으로 애플리케이션 현대화를 수행해 나갈 클라우드 환경을 확보할 수 있습니다.

### 실습 환경 구성

- 먼저 [Cloud9 환경 구성하기](./docs/cloud9.md)를 합니다.
- 다음으로 [EKS Cluster를 생성](./docs/eks-cluster.md)합니다.

### 실습 1: TravelBuddy 애플리케이션 컨테이너화

- [TravelBuddy 컨테이너화](./docs/containerize.md) 내용에 따라서 컨테이너 이미지를 생성합니다.

### 실습 2: Database 구성

- 클라우드 환경에 [데이터베이스를 구성](./docs/database.md)합니다.

### 실습 3: TravelBuddy 애플리케이션을 EKS에 배포

- 컨테이너화 한 TravelBuddy 애플리케이션을 [EKS에 배포](./docs/deploy.md)합니다.

## Monolith란?

[Monolith](./docs/monolith.md)의 개념을 간단히 살펴보고 몇 가지 개선 방법을 알아봅니다.

## Microservice란?

[Microservice](./docs/%08microservices.md)의 개념을 간단히 살펴보고, 어떤 경우에 마이크로서비스가 필요한지 토론해봅니다.

## FlightSpecial Microservice 애플리케이션

- Layered architecture를 반영한 [Package 구조](./docs/package.md)를 살펴봅니다.
- Docker compose를 활용하여 sandbox 환경을 구성하는 방법을 알아봅니다.

### 실습 4: Strangler Fig Pattern - HotelSpecial 애플리케이션을 분리

- FlightSpecial 프로젝트를 참고하여 직접 HotelSpecial 애플리케이션을 제작합니다.
- 이 과정을 통해서 앞에서 학습한 세부 기술들을 익히고 내재화합니다.
