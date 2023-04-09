# TravelBuddy 애플리케이션을 EKS에 배포

## Bastion 호스트에 접속해서 TravelBuddy 애플리케이션 실행해보기

```bash
# CF로 배포한 환경의 RDS 주소
export RDS_ENDPOINT=<RDS_ENDPOINT>

# env.yaml 파일의 내용을 확인하여 환경변수를 주입하여 컨테이너 실행
docker run --rm \
  -e JDBC_CONNECTION_STRING="jdbc:mysql://${RDS_ENDPOINT}:3306/travelbuddy?useSSL=false" \
  -e JDBC_UID=root \
  -e JDBC_PWD=labpassword \
  -dp 8080:8080 travelbuddy
```
