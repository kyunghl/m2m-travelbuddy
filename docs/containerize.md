# TravelBuddy 컨테이너화하기

이 실습에서는 TravelBuddy 애플리케이션을 컨테이너화 하는 방법을 학습니다. 기존에 운영중인 Java와 maven을 이용하는 TravelBuddy 애플리케이션이 제공되므로, 우리는 처음부터 애플리케이션을 빌드하는 대신 컨테이너화 하는 것에만 집중하여 학습을 진행합니다.

## 준비하기

먼저 다음과 같이 `~/environment`에 [TravelBuddy.zip](https://workshops.devax.academy/monoliths-to-microservices/module1/files/TravelBuddy.zip) 파일을 받아서 압축해제합니다.

```bash
# 폴더 이동
cd ~/environment

# 다운로드 및 압축해제
wget https://workshops.devax.academy/monoliths-to-microservices/module1/files/TravelBuddy.zip
unzip TravelBuddy.zip
```
