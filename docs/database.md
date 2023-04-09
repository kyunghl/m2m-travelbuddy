# Database Setup

## RDS MySQL 인스턴스 생성

AWS 콘솔에서 RDS Service로 이동한 후 Create database를 클릭합니다.

Create database 화면에서 `Standard create`, Engine으로는 `MySQL`, Engine Version은 `MySQL 8.0.32`를 선택합니다.
![db1.png](./assets/db1.png)

Template에서는 이번 실습에서는 상용 구축을 하는 것은 아니므로 `Dev/Test`를 선택합니다.
![db3.png](./assets/db3.png)

가용성 설정은 `Multi-AZ DB instance`를 선택합니다.
![db5.png](./assets/db5.png)

설정 값으로는 DB 이름으로 `travelbuddy`를 입력하고, 마스터 유저이름을 `root`, 패스워드를 `labpassword`라고 입력합니다.
![db6.png](./assets/db6.png)

인스턴스 설정은 Burstable class로 `db.t3.small`을 선택합니다.
![db7.png](./assets/db7.png)

저장소는 기본 설정을 유지하고,
![db8.png](./assets/db8.png)

(중요) 접근성 설정에서는 이전 단계에서 생성한 **EKS 클러스터와 동일한 VPC를 선택**합니다. 나머지 설정은 유지하고 Create를 클릭합니다. 기본 설정으로 public 접속을 차단한 것을 기억합니다.
![db9.png](./assets/db9.png)

## Bastion host 프로비저닝

RDS에 public access가 불가하기 때문에, RDS 설정을 위한 bastion host가 필요합니다.

아래 그림과 같이 bastion 호스트의 이름을 입력합니다. (eg. bastion)
![bastion2.png](./assets/bastion2.png)

OS는 `Amazon Linux 2`를 선택합니다.
![bastion3.png](./assets/bastion3.png)

인스턴스 타입은 이번 실습에서는 `t2.medium`을 선택합니다.
![bastion4.png](./assets/bastion4.png)

실습에서는 `Create new key pair`를 클릭하여 새로운 키를 생성한후 이를 사용합니다. 로컬에 다운로드된 private key 파일은 잘 보관합니다.
![bastion1.png](./assets/bastion1.png)
![bastion5.png](./assets/bastion5.png)

네트워크 설정은 이전 단계에서 생성한 EKS 클러스터와 동일한 VPC를 선택하고, 서브넷으로는 public 서브넷 중 하나를 선택합니다.
![bastion6.png](./assets/bastion6.png)

스토리지는 컨테이너 빌드 등에 활용하기 위해서 30GB로 설정합니다.
![bastion7.png](./assets/bastion7.png)

요약 내용을 확인한 후 `Launch instance` 버튼을 클릭하여 인스턴스를 시작합니다.
![bastion8.png](./assets/bastion8.png)

## MySQL에 접속하고 설정하기

### Cloud9에서 bastion 호스트에 접속

Cloud9에서 `File > Upload Local Files...`를 선택하여 이전 단계에서 다운로드한 key 파일을 업로드합니다.
![upload.png](./assets/upload.png)

다음과 같이 업로드한 key 파일의 권한을 변경합니다.

```bash
chmod 400 m2m-bastion.pem
```

EC2 > Instances로 이동하여, bastion 호스트를 선택한 후 Connect 버튼을 클릭하여 SSH client 접속 명령어를 복사합니다.
![ssh.png](./assets/ssh.png)

Cloud9 터미널 창에서 아래 예시와 같이 복사한 명령어를 입력하여 bastion 호스트에 접속합니다.

```bash
ssh -i "m2m-bastion.pem" ec2-user@ec2-43-207-144-210.ap-northeast-1.compute.amazonaws.com
```

접속되지 않는 다면 SecurityGroup에 Cloud9의 공인 IP로 SSH 연결을 허용해야 합니다.

다음 명령어로 cloud9의 public IP를 조회합니다.

```bash
curl ifconfig.me
```

EC2 > instances로 이동하여 bastion 호스트를 선택한 후 Security 탭에서 security group을 선택한 후 `Edit inbound rules` 버튼을 클릭하고 아래 위에서 조회한 IP에 대해 SSH 접속을 허용하는 규칙을 추가합니다.

![ssh-allow.png](./assets/ssh-allow.png)

이제 다시 ssh 접속해보면 성공하는 것을 확인할 수 있습니다.

![ssh-success.png](./assets/ssh-success.png)

### MySQL 클라이언트 설치하기

```bash
sudo yum -y install mysql
```

### RDS 접속

```bash
mysql -u root --password=labpassword -h <rds_host>
```

접속에 성공하면 다음 명령어로 travelbuddy 데이터베이스를 생성합니다.

```sql
-- Database 생성
CREATE DATABASE travelbuddy;

-- 확인
SHOW DATABASES;
```

Database를 생성한 후 [prepare/dbinit.sql](../prepare/dbinit.sql) 내용을 실행하여 database를 초기화합니다. SQL을 성공적으로 실행한 후 다음과 같이 확인합니다.

```sql
-- Hotel Special 테이블 확인
SELECT * FROM hotelspecial;

-- Flight Special 테이블 확인
SELECT * FROM flightspecial;
```

![tables.png](./assets/tables.png)
