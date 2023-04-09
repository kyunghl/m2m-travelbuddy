# TravelBuddy 마이그레이션

이 실습에서는 애플리케이션 현대화의 첫 번째 단계로서 기존 on-premise에서 운영하던 가상의 웹 애플리케이션을 AWS 클라우드 환경으로 옮겨서 배포합니다. 이를 통해 우리는 점진적으로 애플리케이션 현대화를 수행해 나갈 클라우드 환경을 확보할 수 있습니다.

## Topics Covered

- AWS 환경에서 개발 및 배포 등의 작업을 수행하기 위해서 Cloud9을 사용
- TravelBuddy 애플리케이션을 컨테이너화하고 컨테이너 이미지를 ECR에 푸시
- EKS 클러스터를 생성하고 TravelBuddy를 배포하여 실행
- Monolith 개념을 이해하고 TravelBuddy 애플리케이션을 분석하여 개선 방향을 검토

## 실습 환경 구성

- 먼저 [Cloud9 환경 구성하기](./docs/cloud9.md)를 합니다.
- 다음으로 [EKS Cluster를 생성](./docs/eks-cluster.md)합니다.

## Sample Application

이번 실습을 진행하면서 우리는 [TravelBuddy.zip](https://workshops.devax.academy/monoliths-to-microservices/module1/files/TravelBuddy.zip)라는 가상의 웹 애플리케이션을 활용하여 마이크로서비스 아키텍처로 전환하는 예제로 사용할 것입니다.

- 먼저 [TravelBuddy 애플리케이션을 컨테이너화](./docs/containerize.md)합니다.
- [데이터베이스를 구성](./docs/database.md)합니다.
- TravelBuddy 애플리케이션을 EKS에 배포합니다.

## TravelBuddy 애플리케이션 컨테이너화

- [TravelBuddy 애플리케이션을 컨테이너화](./docs/containerize.md) 내용에 따라서 컨테이너 이미지를 생성합니다.
