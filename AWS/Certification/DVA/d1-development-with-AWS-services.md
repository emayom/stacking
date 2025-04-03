---
last_modified_at: '2025-04-03T06:45:43.462Z'
date: '2025-03-29T17:29:41.646Z'
---
# AWS Certified Developer - Associate (DVA-C02) 
## Domain 1:  

#### TOC
- [1.1 AWS에서 호스팅되는 애플리케이션의 코드를 개발합니다.](#11-aws에서-호스팅되는-애플리케이션의-코드를-개발합니다)
    - [AWS CLI](#aws-command-line-interfaceaws-cli)
    - [AWS CloudShell](#aws-cloudshell)
    - [Amazon EC2](#amazon-elastic-compute-cloudamazon-ec2)
    - [Amazon VPC](#amazon-virtual-private-cloudvpc)
    - [Amazon Route 53](#amazon-route-53)
    - [ELB](#elastic-load-balancerelb)
    - [Amazon API Gateway](#amazon-api-gateway)
    
- [1.2 AWS Lambda용 코드를 개발합니다.](#12-aws-lambda용-코드를-개발합니다)
    - [AWS Lambda](#aws-lambda)
    - [Integration with AWS Lambda](#integration-with-aws-lambda)
    - [Lambda in VPC](#lambda-in-vpc)
    - [Deploying AWS Lambda functions with CloudFormation](#deploying-aws-lambda-functions-with-cloudformation)

- [1.3 애플리케이션 개발 시 데이터 스토어를 사용합니다.](#13-애플리케이션-개발-시-데이터-스토어를-사용합니다)
    - AWS 기반 스토리지 
        - [Amazon EC2 Instance Store](#amazon-ec2-instance-store)
        - [Amazon EBS](#amazon-elastic-block-storeamazon-ebs)
        - [Amazon EFS](#amazon-elastic-file-systemamazon-efs)
        - [Amazon FSx](#amazon-fsx)
        - [Amazon S3](#amazon-simple-storage-serviceamazon-s3)

    - AWS 기반 데이터베이스
        - [Amazon RDS](#amazon-relational-database-serviceamazon-rds)
        - [Amazon Aurora](#amazon-aurora)
        - [Amazon DynamoDB](#amazon-dynamodb)
        - [Amazon MemoryDB](#amazon-memorydb)
        - [Amazon ElastiCache](#amazon-elasticache)
        - [기타 AWS 데이터베이스](#기타-aws-데이터베이스)

### 1.1 AWS에서 호스팅되는 애플리케이션의 코드를 개발합니다.
---
<details>
<summary>  
    <b>Knowledge of:</b>
</summary>

- 아키텍처 패턴 
    - 이벤트 기반(Event-Driven)
    - 마이크로서비스(Microservices)
    - 모놀리식(Monolithic)
    - 코레오그래피(Choreography)
    - 오케스트레이션(Orchestration)
    - 팬아웃(Fan-out)

- 멱등성(Idempotency)
    > [!NOTE]  
    > [안정적인 API를 위한 HTTP 메서드의 멱등성 이해하기](../../../Architecture/idempotency-in-HTTP-methods.md)

    - 동일한 연산을 여러 번 적용하더라도 결과가 달라지지 않는 성질

- Stateful과 Stateless의 차이점
    > [!NOTE]  
    > [Stateful vs Stateless](../../../Architecture/stateful-vs-stateless.md) 

    - Stateful(상태 유지)
        - 이전 요청의 상태를 저장하고, 이후 요청에서 그 상태를 사용 = 지속적인 상태 유지  
    - Stateless(상태 없음)
        - 각 요청이 독립적으로 처리되며, 이전 요청의 영향을 받지 않음  

- 긴밀하게 결합된 컴포넌트와 느슨하게 결합된 컴포넌트의 차이점
    - 긴밀하게 결합된(tightly coupled) 컴포넌트
        - 구성 요소들이 강하게 연결되어 있어 변경이 어렵고, 확장성이 낮음 
    - 느슨하게 결합된(loosely coupled) 컴포넌트
        - 구성 요소들이 최소한의 의존성만 가지며 독립적으로 동작하여 확장성 및 유지보수성이 뛰어남

- 내결함성 설계 패턴(Fault-Tolerant Design Patterns)
    - 시스템이 장애를 견디고 정상적으로 운영될 수 있도록 하는 설계 방법
    - 재시도 전략(Retry Strategy)
        - 지수 백오프(Exponential Backoff)
            - 네트워크 상에서 일시적인 오류가 발생했을 때, 재시도 간격을 점진적으로 늘려가며 재시도를 수행  
                → 서버에 과도한 요청을 하지 않도록, 지수적으로 대기시간을 늘린다. 

        - 지터(Jitter)
            - 지수 백오프에 랜덤 요소를 추가해서 동시 재시도 요청을 분산

        - 배달 못한 편지 대기열(Dead Letter Queue, DLQ)
            - 특정 메시지를 여러 번 처리하지 못하면 DLQ로 이동하여 분석 및 처리
                → 장애 발생 시 원인을 추적 가능

- 동기식 패턴과 비동기식 패턴의 차이점
    - 동기식(Synchronous) 패턴
        - 작업을 순차적으로 처리하며, 하나의 작업이 완료될 때까지 다음 작업을 시작하지 않음 = 요청과 응답 순서 보장
    - 비동기식(Asynchronous) 패턴 
        > 단일 스레드 환경에서는 비동기 실행이 병렬적이지 않을 수도 있다.

        - 각 작업이 독립적으로 실행되며, 특정 작업이 끝나기를 기다리는 동안 다른 작업을 병렬적으로 수행  

- 주요 네트워크 포트
    | 포트 번호 | 프로토콜 |
    |----------|-------|
    | 21       | FTP(File Transfer Protocol) |
    | 22       | SSH(Secure Shell)           |
    | 22       | SFTP(Secure File Transfer Protocol) |
    | 80       | HTTP(HyperText Transfer Protocol)   |
    | 442      | HTTPS(Secure HyperText Transfer Protocol) |
    | 3389     | RDP(Remote Desktop Protocol) |
    
</details>

---
- AWS에 액세스하는 방법
    - AWS Management Console
    - AWS Command Line Interface(AWS CLI)
    - AWS Software Development Kit(SDK)
        - 기본 리전을 구성하지 않을 경우 `us-east-1`으로 설정됨 (default)

### AWS Command Line Interface(AWS CLI)
- 명령줄 쉘에서 AWS 서비스와 상호 작용할 수 있는 오픈 소스 도구 (Windows, Mac OS, Linux)
    - Public API를 호출하는 중개자 역할
    - AWS Management Console과 동일한 기능을 CLI에서 수행
    - AWS CLI를 사용하여 AWS 서비스에 접근하려면 액세스 키와 비밀 액세스 키(Secret Access Key)가 필요
- 기존 AWS CLI v1의 경우 Python 설치 필요 
    - AWS CLI v2의 경우 별도 설치 ❌

#### AWS CLI 환경에서 MFA 인증 
- 임시 세션 토큰 발급 (STS `GetSessionToken` API 호출)
    ```sh
    aws sts get-session-token 
        --duration-seconds 900  # 생성 후 15분 뒤에 만료
        --serial-number "YourMFADeviceSerialNumber" 
        --token-code 123456
    ```
#### AWS CLI Credential Provider Chain
> CLI는 다음과 같은 우선순위로 credential 을 찾는다.

1. Command line options  
    - `--region`, `--output`, `--profile`
1. Environment variables
    - `AWS_ACCESS_KEY`, `AWS_SECRET_ACCESS_KEY`, `AWS_SESSION_TOKEN`
1. CLI credentials file
1. CLI configuration file
1. Container credentials - for ECS tasks
1. Instance profile credentials - for EC2 Instance Profiles


#### AWS CLI 기본 명령어 ❗️
- S3 관련 명령어
    ```sh
    # 모든 S3 버킷 나열 
    aws s3 ls   
    
    # 버킷에 있는 모든 객체와 접두사를 나열
    aws s3 ls s3://${BucketName} 

    # S3 버킷 생성 
    aws s3 mb s3://${BucketName} 

    # S3 버킷 삭제 
    aws s3 rb s3://${BucketName} 
    aws s3 rb s3://${BucketName} --force        # ✅ 비어있지 않은 버킷 제거

    # 객체 삭제 
    aws s3 rm s3://${BucketName} 
    aws s3 rm s3://${BucketName} --recursive    # ✅ 재귀적으로 모든 객체를 삭제

    # 객체 이동 
    aws s3 mv filename.txt s3:${BucketName}

    # 객체 복사
    aws s3 cp filename.txt s3://${BucketName}
    ```

- Lambda 관련 명령어
    ```sh
    # 현재 사용자의 모든 함수 목록 조회
    aws lambda list-functions   
    
    # 동기식 간접 호출
    aws lambda invoke --function-name ${FuncName}
        --cli-binary-format raw-in-base64-out   # AWS CLI 버전 2를 사용할 때 필요
        --payload '{ "key": "value" }' response.json 
    
    # 비동기식 간접 호출
    aws lambda invoke 
        --function-name ${FuncName}
        --invocation-type Event             # ✅ InvocationType 파라미터를 `Event`로 설정 
        --cli-binary-format raw-in-base64-out 
        --payload '{ "key": "value" }' response.json
    
    # Lambda 함수 배포
    aws lambda update-function-code 
        --function-name ${FuncName}
        --zip-file fileb://my-function.zip   # filb:// 압축된 파일을 바이너리로 처리하도록 지시
    ```

- EC2 관련 명령어
    ```sh
    # 인스턴스 목록 조회
    aws ec2 describe-instances  

    # 새로운 인스턴스 시작 
    aws ec2 run-instances 
        --image-id ${ImageId}
        --count ${InstanceCount}
        --instance-type ${InstanceType}
        --key-name ${KeyName}

    # 중지된 인스턴스 시작
    aws ec2 start-instances --instance-ids ${InstanceId}  

    # 인스턴스 중지
    aws ec2 stop-instances --instance-ids ${InstanceId}   

    # 인스턴스 종료 (삭제)
    aws ec2 terminate-instances --instance-ids ${InstanceId}   

    # 인스턴스에 태그 추가
    aws ec2 create-tags 
        --resources ${InstanceId} 
        --tags Key=${KeyName},Value=${Value} 
    ```

- CloudFormation 관련 명령어
    ```sh
    # 스택 생성 
    aws cloudformation create-stack 
        --stack-name ${StackName} 
        --template-body file://sampletemplate.json 
        --parameters ParameterKey=KeyPairName,ParameterValue=TestKey ParameterKey=SubnetIDs,ParameterValue=SubnetID1\\,SubnetID2
    
    # 스택 조회 
    aws cloudformation describe-stacks 
        --stack-name ${StackName} 

    # 스택 삭제
    aws cloudformation delete-stack 
        --stack-name ${StackName} 
    ```

### AWS CloudShell
> ![NOTE]   
> [약 23개의 리전](https://docs.aws.amazon.com/ko_kr/cloudshell/latest/userguide/supported-aws-regions.html)에서 AWS CloudShell이 제공된다. 

- AWS CloudShell은 AWS Management Console을 통해 접근할 수 있는 **브라우저 기반 셸**
    - AWS 리소스를 관리하는 데 필요한 모든 도구가 이미 설치되어 있음 
        - 별도의 AWS CLI나 AWS SDK 설치 없이 즉시 사용 가능 
    - 추가 비용 없이 **리전당 최대 1GB의 영구적인 홈 디렉토리(`$HOME`)를 제공** (세션 간에 유지)

### Amazon Elastic Compute Cloud(Amazon EC2)
#### EC2 Instance 유형
> [!NOTE]  
> e.x) m5.2xlarge → `<instance class><generation>.<size>`  

- 범용(General Purpose)
- 컴퓨팅 최적화(Compute Optimized)
- 메모리 최적화(memory Optimized)
- 가속 컴퓨팅(Accelerated Computing)
- 스토리지 최적화(Storage Optimized)
- HPC 최적화(HPC Optimized)

#### EC2 Instance Metadata(IMDS)
- EC2 인스턴스 자체에 대한 정보 
    - 특정 URL(http://169.254.169.254/latest/meta-data)을 통해 Metadata, Userdata를 확인할 수 있음 
        - Metadata
            - `hostname`, `instance-id`, `public-hostname`, `identity-credentials` 등 
            -  IAM 역할 이름을 검색할 수 있지만 <u>IAM 정책 자체는 검색할 수 없음</u>
        - Userdata: EC2 인스턴스 실행 스크립트
- Metadata 버전별 호출 방식 
    - IMDSv1 (token optional)
        1. URL(IPv4/IPv6)에 직접 접근 
            ```sh
            curl http://169.254.169.254/latest/meta-data/
            ```

    - IMDSv2 (token required)
        1. `PUT` 명령어로 Session Token을 GET
            ```sh
            TOKEN=`curl -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600"`
            ```
        1. Session Token을 사용하여 IMDSv2 호출 
            ```sh
            curl -H "X-aws-ec2-metadata-token: $TOKEN" http://169.254.169.254/
            ```

#### EC2 Instance 구매 옵션
- On-Demand
    - **사용한 컴퓨팅 시간**에 대해서만 비용을 지불
        - 중단할 수 없는 불규칙한 단기 워크로드가 있는 애플리케이션에 매우 적합
        - 애플리케이션 개발 및 테스트, 예측할 수 없는 사용 패턴 애플리케이션에 적합
        - 1년 이상 지속되는 워크로드에는 권장하지 않음(비용 절감 측면)
        - 인스턴스 최소 요금
            - Linux 기반 → **최소 1분 요금 청구**, 초단위 과금(30초 이용 → 60초 요금 부과)
            - Windows 기반 → 시간 단위 과금 

- Savings Plans
    - 1년 또는 3년 기간 동안 <u>일정한 컴퓨팅 사용량을 약정</u>
        - **컴퓨팅 사용량이 일정한 워크로드에 매우 적합**
    - 온디맨드 요금에 비해 최대 72%까지 비용 절감
    - 약정 초과 사용량 → 일반 온디맨드 요금 부과

- Reserved Instances
    - 표준 예약 및 컨버터블 예약 인스턴스는 **1년 또는 3년** <u>기간 약정</u> 
        - 정기 예약 인스턴스는 1년 약정으로 구입 가능
        - 3년 약정 옵션 → 더 큰 비용 절감
    - 약정 종료 시, 중단 없이 Amazon EC2 인스턴스 계속 사용 (온디맨드 요금 부과)
        - 인스턴스 종료, 인스턴스 속성과 일치하는 새 예약 인스턴스 구입 시 중단

- Spot Instances
    - 시작 및 종료 시간이 자유롭거나 **중단을 견딜 수 있는 워크로드**에 적합
    - <u>미사용 Amazon EC2 컴퓨팅 용량 사용</u>  
        → 온디맨드 인스턴스 가격 대비 최대 90%까지 할인된 가격으로 제공
    - Savings Plans와 달리, 계약이나 일정한 컴퓨팅 사용량에 대한 약정 필요 ✗

- Dedicated Instances
    - **사용자 전용**의 Amazon EC2 인스턴스 용량을 갖춘 물리적 서버
    - 모든 Amazon EC2 옵션 중에서 전용 호스트가 가장 비용이 많이 듬
    - 단일 고객 전용 하드웨어에서 Virtual Private Cloud(VPC)를 통해 실행

- Dedicated Host
    - 소켓 or 코어 or VM 소프트웨어 라이선스 당 청구
    - 기존 서버 바운드 소프트웨어 라이선스 사용 가능

- Capacity Reservations
    - 특정 인스턴스 유형과 리전에 대해 EC2 인스턴스의 용량을 예약

#### EC2 Instance 연결 방법  
- SSH 연결 
    ```sh
    # Public DNS
    ssh -i /path/key-pair-name.pem instance-user-name@instance-public-dns-name

    # IPv6
    ssh -i /path/key-pair-name.pem instance-user-name@instance-IPv6-address
    ```
    - SSH 키 페어(Key Pairs)로 인증 
        - SSH 연결을 위한 포트 22 인바운드 룰 필요 
    - Mac OS, Linux, Windows >= 10에서 사용 가능 
        - Windows < 10 경우 PuTTY 사용 

- EC2 Instance Connect
    - 임시 SSH 키 생성하여 연결, IAM을 통한 인증 (키 파일 관리 필요 ❌)
    - Amazon Linux 2 및 Ubuntu 16.04 버전 이상의 인스턴스만 지원 
    - Mac OS, Linux, Windows 모두 사용 가능 

- System Manager Session Manager 
    - AWS API 기반으로 EC2와 통신, IAM을 통한 인증 
    - SSM Agent 설치 필요 

- EC2 직렬 콘솔(EC2 Serial Console)
    - EC2 시리얼 포트로 연결, IAM을 통한 인증 + Root PWD
    - 특정 인스턴스 타입 및 리전에서만 사용 가능 (e.g. t2 시리즈 사용 불가능)

### Amazon Virtual Private Cloud(VPC)
- AWS 리소스에 경계를 설정하는 데 사용할 수 있는 가상 네트워크 서비스  
    → 사용자가 AWS 리소스를 <u>논리적으로 격리된</u> 가상 네트워크 환경에서 운영할 수 있도록
- 특정 리전과 연결, 특정 리전 내에서 작동하는 가상 네트워크 = **리전 리소스**
    - 리전마다 1개의 기본 VPC 존재 
- 구성 요소
    - **서브넷(Subnet)**   
        - VPC 내의 네트워크 분할 (AZ 수준에서 정의)  
        - 공용 서브넷(Public Subnet) → 인터넷(www) 접근 가능
        - 사설 서브넷(Private Subnet) → 인터넷 접근 제한 

    - **라우팅 테이블(Routing Table)**  
        - 네트워크 트래픽을 전달할 위치를 결정하는 데 사용되는 라우팅이라는 규칙 집합

    - **인터넷 게이트웨이(Internet Gateway, IGW)**  
        - VPC 인스턴스와 인터넷 간의 연결을 지원 
            - 공용 서브넷에 있는 EC2 인스턴스 → IGW로 라우팅 → 공개적 연결 

    - **NAT 게이트웨이 및 NAT 인스턴스**  
        - 사설 서브넷 내의 인스턴스가 프라이빗 상태를 유지하면서 인터넷이나 다른 AWS 서비스에 연결할 수 있도록 지원 
            - NAT 게이트웨이 또는 NAT 인스턴스를 공용 서브넷에 배포 → 사설 서브넷에서 라우팅 → IGW로 라우팅 → 공개적 연결 
        - NAT(Network Address Translation) 게이트웨이 → AWS에서 관리    
        - NAT 인스턴스 → 사용자가 관리
            
    - **보안 그룹(Security Group)** 
        - ENI(Elastic Network Interfaces) / EC2 인스턴스에 대한 **인바운드, 아웃바운드 트래픽을 제어하는 가상 방화벽 역할**
            - 프로토콜, 포트, IP 주소 범위를 기준으로 규칙 설정 
            - <u>기본적으로 모든 인바운드 트래픽을 **거부**, 모든 아웃바운드 트래픽을 **허용**</u>
            - ALLOW 규칙만 존재 → 특정 IP 차단 불가 
        - 보안 그룹을 여러 인스턴스에서 사용하거나 여러 보안 그룹을 한 인스턴스에서 사용 가능 
        - 보안 그룹은 서로 참조 가능 = 보안 그룹 참조(Security Group Referencing)
        - 기본적으로 동일한 VPC 내에서만 유효 
            - 새로운 VPC를 생성할 경우, 새로운 보안 그룹 생성 필요 
            - AWS RAM을 이용하면 보안 그룹 공유 가능
                - 동일 리전 내 다른 VPC 간 보안 그룹 공유 
                - Organizations 내의 계정 간 보안 그룹 공유 (Resource Sharing)
                    - 조직 외부의 다른 계정 간 공유 ❌ 

    - **네트워크 ACL(Network Access Control List, NACL)** 
        - **서브넷 수준**에서 인바운드 및 아웃바운드 트래픽을 제어하는 가상 방화벽
            - IP 주소를 기준으로 규칙 설정 
            - VPC를 생성하면 자동으로 하나의 기본 NACL이 생성  
                → <u>기본적으로 모든 인바운드 및 아웃바운드 트래픽을 **허용**</u>
            - ALLOW(허용) 및 DENY(거부) 규칙이 모두 존재 

    - **VPC Flow Logs**
        - 네트워크 인터페이스로 들어오고 나가는 모든 IP 트래픽에 대한 정보를 캡처 가능
            - VPC Flow Logs
            - Subnet Flow Logs
            - Elastic Network Interface Flow Logs

    - **VPC Peering**  
        - AWS의 네트워크를 사용해 다른 VPC와 프라이빗으로 연결 → 마치 동일한 네트워크에 있는 것처럼 동작
        - 각 VPC CIDR Range(허용하는 IP 범위)는 서로 겹치지 않아야 함
        - VPC Peering 연결은 전이적(transitive)이지 않음

    - **VPC Endpoint**
        - **인터넷을 거치지 않고**, VPC 내부에서 프라이빗 네트워크를 통해 AWS 서비스를 이용 가능 
        - 게이트웨이 엔드포인트(Gateway Endpoint) → Amazon S3 & DynamoDB (라우팅 기반, 무료)
        - 인터페이스 엔드포인트(Interface Endpoint) → 제외한 모든 AWS 서비스 (ENI 기반, 유료)

    - **Site-to-Site VPN**
        - 온프레미스 데이터센터와 VPC 간 **암호화된 네트워크 경로(IPsec 터널)** 생성
            - **Public 인터넷**을 통해 연결 → 대역폭 제한, 보안 문제 발생 가능
            - 약 5분 정도의 빠른 설정 

    - **Direct Connect(DX)**
        - 온프레미스 데이터센터와 VPC 간 물리적으로 연결 
            - **비공개 전용 회선**을 통해 연결 → 느린 설정, 높은 비용 
            - 짧은 지연 시간, 최대한 높은 수준의 보안, 고속 및 대역폭 확장 

### Amazon Route 53
> [!NOTE]  
> DNS(Domain Name System) 용어 
> ![Image](https://github.com/user-attachments/assets/2ded27db-04b8-46ec-a3c2-326c35c05e8a)
> 
> - Domain Registrar: Amazon Route 53, GoDaddy 등
> - DNS Records: `A`, `AAAA`, `CNAME`, `NS` 
> - Zone File: contains DNS records
> - Name Server: resolves DNS queries(Authoritative or Non-Authoritative)
> - Top Level Domain(TLD)
> - Second Level Doman(SLD)

- 관리형 DNS(Domain Name System) 웹 서비스  
- 사용자 요청을 AWS에서 실행되는 인프라에 연결
- 단일 위치에서 DNS 레코드 관리 기능  
    - 다른 도메인 등록 대행자(3rd Party Registrar)가 관리하는 기존 도메인 이름의 DNS 레코드 전송 가능  
- 100% SLA 가용성을 제공하는 유일한 AWS 서비스 

#### 호스팅 영역(Hosted Zone)
- 특정 도메인의 DNS 설정을 저장하는 레코드의 컨테이너 역할
    - 비용: $0.50 / month 
- Public Hosted Zone
    - 인터넷에서 접근할 수 있는 도메인의 DNS 레코드를 관리
- Private Hosted Zone
    - 특정 VPC 내에서만 사용할 수 있는 도메인의 DNS 레코드를 관리

#### TTL(Time-To-Live)
- DNS 레코드가 캐시될 수 있는 시간을 정의하는 값
    - 초(seconds) 단위 설정
    - 캐시된 레코드는 다시 DNS 서버에 요청하지 않음 → 네트워크 트래픽 절감

#### Health Checks
- 리소스의 정상 작동 여부를 모니터링 → DNS 장애 조치 자동화 가능
- Health Check 유형 
    - **Endpoint Health Check**
        - 특정 IP 주소나 도메인에 요청을 보내 응답 여부 확인
            - **인터넷에서 접근 가능한 리소스 = Public IP / Public URL**
            - ALB나 엔드포인트에 접근이 가능해야 함 
        - HTTP, HTTPS, TCP 프로토콜 지원
        - 텍스트 기반 응답 확인 → 처음 5,120byte 내에서 설정한 문자열 일치 확인

    - **Calculated Health Check**
        - 여러 개의 개별 Health Checks 결과를 종합하여 하나의 Health Check 생성 
            - 최대 256개 결합 가능 
            - OR, AND, NOT 조건 조합 가능 

    - **CloudWatch Alarm Health Check**
        - CloudWatch Alarm을 활용하여 리소스 상태 모니터링
            - VPC 내부 리소스(Private IP) 모니터링 가능 (Private 엔드포인트 ❌)
            - CloudWatch Matrix 기반 Health Check
  
- 고급 구성 
    - **Failure Threshold** * `필수`
        - Health Check 요청 간격 
        - 3 (default)
    - Request Interval 
        - 장애로 간주되기 전까지 몇 번의 장애가 발생해야 하는지 
        - Standard (30s) 
        - Fast (10s) → 더 높은 비용
    - String Matching
    - Latency Graphs
    - Invert Health Check Status 
    - Disable Health Check
    - Health Checker Regions
        - Customize
        - Use recommended

#### 레코드 종류(Records Types)
> [!NOTE]  
> **CNAME vs Alias**  
> Alias 레코드는 AWS Route 53에서만 제공하는 기능으로, CNAME과 비슷하게 동작하지만 특정 <u>AWS 리소스</u>가리킬 수 있다. (EC2 제외)

| 유형 | 설명 |
|----------------|---------|
| **A** | 도메인을 **IPv4 주소**로 매핑 |
| **AAAA** | 도메인을 **IPv6 주소**로 매핑 |
| **CNAME(Canonical Name)** | 도메인을 다른 도메인으로 매핑 (redirect) |
| **NS(Name Server)** | 도메인을 관리하는 네임서버의 주소를 지정 |

#### 라우팅 정책(Route Policy)
> [!NOTE]  
> Route 53이 어떻게 DNS Query에 응답할지 정의하는 정책

- **단순 라우팅(Simple Routing)** 
    - 기본 라우팅 방식으로, <u>하나의 레코드에 단일 값 지정</u> 
        - DNS에 의해 다중 값을 받은 경우 클라이언트에서 무작위로 선정, 단일 응답 반환
        - Alias 레코드 사용 시, 단 하나의 AWS 리소스만 지정 가능   
            → 하나의 Alias 레코드가 여러 AWS 리소스를 가리키는 것은 불가능
        - **<u>Health Check 미지원</u>**

- **가중치 기반 라우팅(Weighted Routing)** 
    - 여러 엔드포인트에 대해 가중치(%)를 설정하여 트래픽 분산 
        - 가중치를 부여할 DNS 레코드는 반드시 동일한 레코드 이름과 ID을 가져야 함
        - 가중치는 최소 0, 최대 255로 설정 가능 
            - 레코드의 가중치가 0일 경우, 트래픽이 전달되지 않음
    - Health Check 지원

- **지연 시간 기반 라우팅(Latency-based Routing)** 
    - 사용자가 가장 짧은 지연 시간을 갖는 리전에 연결되도록 라우팅 
    - Health Check 지원

- **지리적 라우팅(Geolocation Routing)** 
    - 사용자의 물리적 위치(국가 또는 대륙)에 기반하여 라우팅 
        - 지정된 일치하는 위치가 없을 경우를 위해 Default 레코드 생성 필요 
    - Health Check 미지원

- **지리적 근접 라우팅(Geoproximity Routing)** 
    - 사용자와 리소스의 지리적 위치를 기반으로 라우팅 
        - Route 53 Traffic Flow
            - Geoproximity map을 통해 시각적인 라우팅 정책 관리 (GUI 기반)
            - 편향 값(Bias) 설정 
                ```
                Biased distance = actual distance * [1 - (bias/100)]
                ```
                - 1 to 99 : 지리적 리전의 크기 확장 = 더 많은 트래픽
                - -1 to -99 : 지리적 리전의 크기 축소 = 더 적은 트래픽 
    - Health Check 미지원

- **다중값 응답 라우팅(Multivalue Answer Routing)** 
    - Health Check 결과 정상인 리소스 중 무작위로 선택된 최대 8개의 정상 레코드로 응답
    - 클라이언트 사이드 로드 밸런싱 (ELB 대체 불가능)

- **장애 조치 라우팅(Failover Routing)** 
    - Active-Passive 장애 조치를 구성하려는 경우  
    - 기본 리소스 장애 시 대체 리소스로 라우팅 (기본 레코드의 상태를 기반으로 동작)  
        → Health Check 기반의 장애 조치 
    - Health Check 지원
        - **Health Check 없이 기본 레코드 저장 불가** (mandatory)

- **IP 기반 라우팅(IP-based Routing)**
    - 클라이언트의 IP 주소를 기반으로 라우팅 
    - CIDR 제공 필요 

### Elastic Load Balancer(ELB)
- AWS 관리형 로드밸런서 
    - 클라이언트에 대한 단일 접점 역할
    - 어떠한 경우에도 로드 밸런서가 작동할 것을 보장
    - AWS측에서 업그레이드, 유지 관리 및 고가용성을 책임
- 기본적으로 **단일 리전 내에서만 동작**하며, 리전의 여러 AZ의 다운스트림(downstream) 인스턴스로 부하 분산
    - 인스턴스의 상태를 설정된 주기(interval)마다 Health Check
    - 다운스트림 인스턴스 장애 처리(Failover)  
        - 비정상 인스턴스를 감지 → 트래픽 차단 (직접 복구 ❌)
- 애플리케이션에 사용 가능한 **Static DNS Name**을 제공 (Static IP ❌)
    - 단, NLB는 Static DNS Name과 Static IP를 모두 제공
- SNI(Server Name Indication) 지원 (ALB, NLB)
    - 서버 인증서를 퍼블릭 IP 주소가 아닌 도메인 이름으로 판단 → 하나의 LB에서 여러 개의 SSL/TLS 인증서 사용 가능
    - 최대 25개의 인증서 설정 가능 
- Connection Draining 지원 (GWLB 제외)
    - 인스턴스가 로드 밸런서에서 제거되기 전에, 연결된 클라이언트 세션이 정상적으로 종료될 수 있도록 도와주는 기능
        - 인스턴스가 종료되거나, 비정상 상태로 전환되기 전에 현재 연결된 요청들이 안전하게 처리될 수 있도록
    - CLB(Connection Draining), ALB, NLB(Deregistration Delay)

#### 구성 요소
- Listener
    - 구성된 프로토콜, 포트로 클라이언트로부터 받은 요청 수신
    - Listener Rules을 기반으로 어떤 타겟 그룹으로 라우팅하는 방법 결정
        - 각 규칙은 우선 순위, 하나 이상의 작업, 하나 이상의 조건으로 구성
- Target Group
    - 리스너가 전달한 요청을 처리하기 위한 부하 분산 대상들의 모임 
- Security Groups
    - 로드 밸런서에 대한 인바운드 및 아웃바운드 트래픽을 제어
- Health Check

#### 로드 밸런서 유형
> [!NOTE]  
> Target Group은 로드밸런서가 트래픽을 분배할 대상 서버(target)들의 집합을 나타낸다. 

- ~~Classic Load Balancer(CLB)~~ `Layer4 & 7`
- **Application Load Balancer(ALB)** 
    - `Layer 7`에서 작동
        - HTTP, HTTPS, gRPC(HTTP/2 기반), WebSocket 프로토콜 지원 
    - 경로 기반 라우팅(Path-based Routing) = 요청된 URL 경로에 따라
    - 호스트 기반 라우팅 (Host-based Routing) = 요청된 호스트 헤더에 따라
    - 쿼리스트링 및 헤더 기반 라우팅
    - Target Groups 
        - EC2 instances 
        - ECS tasks
        - Lambda Functions 
        - (Private) IP Addresses 
    - 사용 사례: 마이크로 서비스 & 컨테이너 기반 애플리케이션에 적합
        
- **Network Load Balancer(NLB)** 
    - `Layer 4`에서 작동
        - TCP, TLS(secure TCP), UDP 프로토콜 지원 
        - **초당 수백만 개의 요청 처리 가능** = 최고 성능과 최저 지연 시간(Latency)
    - **AZ 당 하나의 고정(static) IP를 가지고, 각 가용 영역에서 Elastic IP 주소 연결 가능**
        - ALB는 DNS 기반이므로 IP 고정 불가능
    - TCP, HTTP, HTTPS 프로토콜 Health Check 지원 
    - Target Groups 
        - EC2 instances 
        - (Private) IP Addresses 
        - ALB

- **Gateway Load Balancer(GWLB)** 
    - `Layer 3`에서 작동
        - IP 패킷 수준에서 동작
    - IP 패킷 자체에서 GENEVE 프로토콜 
    - 네트워크 트래픽을 처리하고 필터링
    - 트래픽을 방화벽으로 라우팅 
    - GENEVE 6081 포트 
    - Target Groups 
        - EC2 instances 
        - (Private) IP Addresses 
    - 사용 사례: 보안, 침입 감지, 방화벽 

#### Sticky Sessions
- 클라이언트가 로드밸런서에게 두번의 요청을 할 때 동일한 인스턴스가 응답하도록 하는 것 
    - 클라이언트가 로드밸런서로 요청을 보낼 때 쿠키(stickiness, expiration date 포함)와 함께 전송 (NLB 제외)
- CLB, ALB, NLB에서 활성화 가능

- Cookie Names
    - **애플리케이션 기반 쿠키(Application-based Cookies)**
        - 사용자 정의 쿠키(Custom Cookie)
            - 애플리케이션에 의해 생성
            - 사용자 정의 속성 포함 가능
            - Cookie Name: 각 타겟 그룹마다 개별적으로 지정해야 함
            - 예약된 이름 사용 불가 (AWSALB, AWSALBAPP, AWSALBTG) 
        - Application Cookie
            - 로드밸런서에 의해 생성 
            - Cookie Name: AWSALBAPP

    - **지속 시간 기반 쿠키(Duration-based Cookies)**
        - 로드밸런서에 의해 생성 
        - Cookie Name: AWSALB (for ALB), AWSELB (for CLB)

#### 교차 영역 로드 밸런싱(Cross Zone Load Balancing)
- <u>모든 AZ에 등록된 모든 EC2 인스턴스 개수가 불균형하더라도</u> 부하를 고르게 분산

    | 유형 | 기본 설정 | AZ 간 데이터 전송 비용 |
    |-----|---------|-------------------|
    | **CLB**  | 비활성화       | 없음 |
    | **ALB**  | 활성화        | 없음  |
    | **NLB**  | 비활성화 (유료) | 부과  |
    | **GWLB** | 비활성화 (유료) | 부과  |

#### Auto Scaling Groups(ASG) ❗️
- Scale-Out 이벤트 중에는 ASG에 구성한 최대 용량 초과 ❌
- 각 스케일링 활동 후 쿨다운 기간 존재 
    - 기본값은 300s(5m)
    - EC2 인스턴스를 시작하거나 종료하지 않음 → 메트릭이 안정화될 시간
- **Scaling Policies**
    - 동적 스케일링(Dynamic Scaling)
        - Target Tracking Scaling
            - 평균 CPU 사용률, 평균 네트워크 IN/OUT (byte), 타겟당 ALB 요청 수에 따라 설정 가능 
        - Simple Scaling
            - CloudWatch Alarm이 발당될 때마다 스케일링 
        - Step Scaling
            - CloudWatch Alarm을 기준으로 여러 단계를 갖도록 
    - 예측 스케일링(Predictive Scaling) 
        - 머신 러닝 기반 
    - 예약 스케일링(Scheduled Scaling)
        - 예약할 희망 용량(capacity), 주기, 타임존, 시작/끝 시간 설정 가능 

### Amazon API Gateway
- 규모에 상관없이 API 생성, 유지 관리, 모니터링 및 보호를 할 수 있게 해주는 완전 관리형 서비스 
    - Endpoints와 REST API를 통합적으로 관리 가능 
    - API 버저닝 및 다양한 환경(`dev`, `test`, `prod` 등)에 대응 가능
    - Open API  연동 → SDK 및 API 규격 생성 지원 
    - 기본적으로 요청 쓰로틀링(throttling) 기능 제공 
        - 기본 제한 
            - 초당 요청(RPS): 10,000 TPS (Soft Limit)
            - 버스트 제한: 5,000
        - 스테이지 별 / 메서드별 / API Key를 사용하는 클라이언트별로 개별적인 요청 제한 가능

#### API 유형
- **HTTP API**
    - API Proxy 기능 정도만 필요한 경우
        - OIDC 및 OAuth 2.0 지원, 기본 CORS 지원 
        - 데이터 매핑 제공 ❌
        - 리소스 정책 지원 ❌
        - <u>짧은 지연 시간, 비용 효율적</u>

- **REST API**
    - API 관리 기능, request/response에 대한 제어가 필요한 경우 
        - RESTful 아키텍처 기반으로 동작
        - 대부분의 기능 지원(Native OpenID Connect / OAuth 2.0 / JWT 제외) 
         - <u>높은 비용</u>


- REST API (Private) → VPC 내에서만 액세스할 수 있도록 
- **WebSocket API** → 양방향 통신이 필요한 실시간 애플리케이션용

#### Endpoint Types
- **Edge-optimized API endpoints** (default) 
    - 클라이언트가 지리적으로 분산된 경우(글로벌 클라이언트)
    - 모든 CloudFront Edge 위치에서 요청을 라우팅 → 지연 시간 개선 

- **Regional API endpoints**
    - 동일 리전 내에 위치한 클라이언트 

- **Private API endpoints**
    - VPC 내에서만 액세스 가능 
    - 인터페이스 VPC 엔드포인트(ENI) 사용 
    - 리소스 정책 정의 가능 

#### Deployment Stages
- Stage Variables
    - Lambda Aliases
        `${stageVariables.lambdaAlias}`

#### API Gateway 보안 
- User Authentication through
    - IAM 역할 
        - Signature v4
    - Cognito User Pool
        - 모바일 애플리케이션, 웹 애플리케이션 등 외부 사용자 
    - Custom Authorizer
        - 3rd party tokens

- Custom Domain Name HTTPS

#### Integration Types
- **Mock**
    - 백엔드로 요청을 보내지않고, 응답 반환 

- **HTTP / AWS** (Lambda function & AWS Services)
    - mapping template을 사용하여 데이터 매핑 구성 가능 

- **AWS_PROXY** (Lambda Proxy)
    - mapping template, 헤더, 쿼리스트링 파라미터 등 ❌

- **HTTP_PROXY**
    - mapping template ❌
    - HTTP 요청이 백엔드로 전달됨 
    - 필요 시 HTTP 헤더 추가 가능 

#### Cache API responses
- **캐시 TTL**: 최소 0s, 최대 3600s(1h), 기본 300s
- **캐시 용량(Cache Capacity)**: 0.5GB to 237GB
- 매서드별 캐시 설정 오버라이드 가능 
- 캐시 암호화 가능 
- 전체 캐시 무효화(flush) 가능 
    - UI / 클라이언트에서 API 게이트웨이로 보내는 쿼리에 `header: Cache-Control: max-age=0` 헤더 추가 (IAM authorization 필요)

### 1.2 AWS Lambda용 코드를 개발합니다.
---
<details>
<summary>  
    <b>Knowledge of:</b>
</summary>

- 이벤트 소스 매핑 (Event Source Mapping)
    - AWS Lambda에서 특정 이벤트 소스를 폴링하여 자동으로 Lambda 함수를 트리거하는 기능

- 스테이트리스 애플리케이션
    - 이전 요청의 상태를 저장하지 않는 방식의 애플리케이션 
        - REST API
        - AWS Lambda
        - 웹 서버 (Nginx, Apache)

- 단위 테스트(Unit Test)
    - 코드의 작고 격리된 애플리케이션 코드 블록(일반적으로 함수 또는 메서드)의 정확성을 확인하는 프로세스

- 이벤트 기반 아키텍처 
    - 시스템 구성 요소들이 이벤트를 통해 비동기적으로 상호 작용하는 패턴

- 확장성(Scalability)
    - 시스템이 데이터, 사용자, 거래량 등이 증가해도 성능이나 보안을 저하시키지 않고 효율적으로 처리할 수 있는 능력

- Lambda 코드에서 VPC의 프라이빗 리소스에 액세스
</details>

---

- AWS 환경에서의 서버리스(Serverless in AWS)
    - AWS Lambda
    - DynamoDB
    - AWS Cognito
    - AWS API Gateway
    - Amazon S3
    - AWS SNS & SQS
    - AWS Kinesis Data Firehose
    - Aurora Serverless
    - Step Functions
    - Fargate

### AWS Lambda
- 인프라를 프로비저닝하거나 관리하지 않고도 코드를 실행할 수 있는 서버리스 컴퓨팅 서비스
    - 이벤트에 대한 응답으로 코드를 실행 = **온디맨드 실행** 
    - 함수당 최대 10GB(10,240MB)까지 RAM 프로비저닝 가능
- 다른 AWS 서비스와 쉽게 통합, CloudWatch를 통한 로그 모니터링 가능 
- 함수 버저닝 및 별칭(Alias) 기능 지원
    - **`$LATEST`(가장 최근에 배포된 함수)를 제외한 각 버전은 불변(immutable)**
    - `$LATEST`가 기존 버전과 동일할 경우, 새로운 버전으로 생성 불가 
    - 특정 Lambda 함수 버전를 참조하는 별칭(Alias)을 생성 가능 
        - <u>Alias는 다른 Alias를 참조할 수 없음</u>
    - Weighted Alias는 
- 다양한 언어 지원 
    - 공식 지원 언어 
        - Java, Go, PowerShell, Node.js, C#, Python 및 Ruby
    - 커스텀 런타임(Custom Runtime)
        - 공식 지원하지 않는 언어나 라이브러리를 포함한 커스텀 실행 환경이 필요할 경우  
            1. Lambda Runtime API을 사용하여 직접 커스텀 런타임 환경을 구축
            1. Lambda Container Image를 사용하여 Docker 컨테이너 이미지를 기반으로 커스텀 런타임 환경을 구축

#### 요금(Pricing)
- 호출 횟수와 컴퓨팅 시간에 따라 비용 결정, Free Tier 제공 
    - 호출(Requests)
        - 월 100만건 요청 무료, 추가 요청 100만 건당 $0.2x ($0.0000002 / request)
    - 지속 시간(Duration)
        - 월 40만 GB-초 컴퓨팅 시간 무료, 추가 GB-초당 청구 (리전별 비용 상이) 

#### 할당량 (리전별 적용) ❗️
- **메모리 할당**: 128MB ~ 10,240MB (1MB 단위)
    - 구성된 메모리에 비례하여 vCPU가 함수에 할당 (네트워크 품질 및 성능도 향상)
- **제한 시간**: 기본 3s, 최대 900s(15m) 
    - 15분 이상의 실행 시간이 필요할 경우 다른 서비스(e.g. Fargate, ECS, EC2) 사용
- **환경 변수**: 최대 4KB
- **리소스 기반 정책**: 20KB
- **임시 스토리지(/tmp)**: 512MB ~ 10,240MB (1MB 단위)
- **동시 실행(concurrency executions)**: 최대 1,000건
- **배포 패키지 크기** 
    - ZIP 파일(.zip): 최대 50MB (압축되지 않으면 250MB)
    - 컨테이너 이미지: 최대 10GB

#### Lambda 함수를 AWS 외부에 노출하는 방법 (HTTP Endpoints)
1. **API Gateway**
    - 쓰로틀링, 요청 유효성 검사, 사용자 지정 권한 부여, 리소스 정책 등 다양한 기능 제공 
    - 다양한 인증 방식 및 고급 보안 기능 제공 
    - 추가 비용 발생 
1. **Function URL** (2022.04 ~ 공식 지원)
    ```sh
    # 고유한 URL 엔드포인트
    https://<url-id>.lambda-url.<region>.on.aws
    ```

    - HTTPS 엔드포인트에서 Lambda 함수 호출을 지원 (IPv4 및 IPv6)
        - Enable function URL / Create function URL 필요
        - API Gateway의 Lambda proxy integration처럼 동작  
        - 리소스 기반 정책 & CORS 구성 지원 
        - AWS IAM 인증 방식만을 제공
        - Lambda 호출 비용 이외의 추가 비용 발생 ❌
        - Private 액세스 지원 ❌
        - 일부 리전에서는 Function URL 지원 ❌

#### Lambda 함수에 전달되는 입력 데이터 (Argument)
```js
exports.handler = async (event, context) => {
    // ...
};
```

- 이벤트(Event) 객체 
    - Lambda 함수에 전달되는 input 데이터
    - 함수가 처리할 이벤트 데이터가 포함된 JSON 객체
    - `event`는 런타임에 따라서 다른 객체로 변환 (e.g. python → dict type)
    - 예시 
        - API Gateway를 통해 호출된 HTTP 요청 정보
        - S3 버킷에 업로드 된 객체의 정보 
        - DynamoDB Streams 이벤트 

- 컨텍스트(Context) 객체
    - Lambda 함수의 메타데이터(metadata)
        - 공통 속성 (Node.js 기준)
            > 일부 속성은 특정 언어나 런타임 환경에 의존하여 다르게 제공될 수 있다.

            - `functionName` → Lambda 함수의 이름
            - `functionVersion` → 함수의 버전
            - `invokedFunctionArn` → 호출된 Lambda 함수의 ARN
            - `memoryLimitInMB` → 함수에 할당된 메모리의 양 
            - `awsRequestId` → 호출 요청 식별자
            - `logGroupName` → 함수에 대한 로그 그룹
            - `logStreamName` → 함수 인스턴스에 대한 로그 스트림

#### Lambda Destination
- 비동기식 호출(Asynchronous Invocation)
    - **실패하거나 성공했을 때, 이벤트를 다른 서비스(destination)로 전달** 
        - 특정 서비스로 실행 결과(`OnFailure`, `OnSuccess` 이벤트)를 전달하여 추가적인 처리를 수행할 수 있도록
        - DLQ와 유사한 동작 → DLQ 대신 destination의 사용을 권장 

- 스트림 호출(Stream Invocation) = 이벤트 소스 매핑(Event Source Mapping)
    - **실패한 이벤트만** 다른 서비스(destination)로 전달

- Destination type 
    - Amazon SQS
    - Amazon SNS
    - Amazon EventBridge
    - AWS Lambda

#### Lambda Layers
- 핵심 함수 로직을 종속 항목과 분리  
    - **배포 패키지 크기 최소화 및 배포 시간 단축**
    - 자주 변경되는 함수 코드와 자주 변경되지 않는 외부 종속성을 분리 → 독립적으로 관리 
    - 여러 함수가 공유하는 코드 및 데이터를 중앙에서 관리 → 참조를 통해 재사용 
- 함수당 최대 5개의 Layer 추가 가능 
    - 함수의 소스 코드 + Layers 크기 <= 250MB
    - <u>Layer 버전은 게시된 후 수정하거나 삭제할 수 없음</u> = Immutable   
        → 업데이트하려면 새로운 버전을 만들어야 함 
- 버전 관리 지원
- 유형 
    - **AWS layers** → AWS에서 공식적으로 제공하는 Layer 
        - 예시 
            - `AWS SDK for JavaScript`
            - `AWS X-Ray SDK for Node.js` 
    - **Custom layers** → 사용자가 직접 Layer를 생성
        - Custom Runtimes이 필요한 경우 (e.g. Rust, C++ 등 공식 지원되지 않는 언어 실행)
        - 종속성(dependencies)을 재사용 가능한 형태로 externalize
    - **Specify an ARN** → 이미 생성되거나 공유된 Layer의 ARN을 직접 입력하여 사용
   
### Integration with AWS Lambda 
#### AWS Lambda 호출 방식(AWS Lambda Invocation Types)
- **동기식(Synchronous)** = Push Model
    - 클라이언트가 Lambda 함수의 실행을 끝날 때까지 대기, 응답을 반환 = API 응답이 필요한 경우
        - <u>클라이언트 사이드에서 에러 핸들링</u>
            - 재시도(retry), 지수 백오프(exponential backoff) 등
    - 주요 서비스
        - Elastic Load Balancing (ALB)
        - Amazon API Gateway
        - Amazon Cognito
        - Amazon CloudFront (Lambda@Edge)
        - AWS CLI
        - AWS SDK
        - AWS Step Functions

- **비동기식(Asynchronous)** = Event Model
    - Lambda 함수는 호출 후 즉시 반환, 백그라운드에서 처리 = 응답을 기다리지 않음 
        - <u>자동 재시도(최대 2회) 및 에러 핸들링 수행</u>
            - 실행되는 Lambda 함수는 **멱등적**이어야한다. 
    - 주요 서비스 
        - Amazon S3 
        - Amazon SNS 
        - Amazon SES
        - Amazon CloudWatch Logs 
        - Amazon CloudWatch Events 
        - AWS CloudFormation
        - AWS CodeCommit
        - AWS Config

- **이벤트 소스 매핑(Event Source Mapping)** = Poll-Based
    - <u>Lambda가</u> 지속적으로 폴링(polling)하여 새로운 데이터를 감지 → Lambda 함수로 전달 
    - 자동 재시도 & Dead Letter Queue(DLQ) 가능
        - Lambda DLQ의 경우 비동기식 호출에만 작동 
    - Stream (Kinesis, DynamoDB Streams)
        - 샤드(shard) 레벨에서 아이템을 순차적으로 처리 
            - 읽기 시작 위치 지정 가능 
            - 에러 핸들링
                - 배치(batch)에 오류 발생 시 처리 중단 (to ensure in-order processing)
    - Queue (SQS & SQS FIFO)
        - Short Polling (default)
        - Long Polling
            - 대기열이 비어있을 경우, 일정 시간 대기 후 반환 (1s~20s)  
                → 불필요한 CPU 연산 및 API 호출 방지 

    - 주요 서비스 
        - Amazon DocumentDB
        - Amazon DynamoDB
        - Amazon Kinesis
        - Amazon MQ
        - Amazon Managed Streaming for Apache Kafka (Amazon MSK)
        - Amazon SQS

#### ALB + Lambda
- 동기식 호출 
- HTTP(S) 요청을 Lambda로 전달
    - Lambda 함수를 Target Group으로 등록 필요 
    - ALB ↔︎ Lambda 함수 간 HTTP ↔︎ JSON 변환(translate)
    - Multi-Header 지원
        - 다중 헤더 값은 배열으로 변환 

#### Amazon API Gateway + Lambda
- 동기식 호출 
- HTTP(S) 요청을 Lambda로 전달
    - API Gateway의 인증/보안 기능 활용 가능
    - 통합 방식 
        - 프록시 통합(Proxy Integration) → API Gateway가 요청을 **원본 그대로** Lambda에 그대로 전달
        - 비 프록시 통합(Non-Proxy Integration) → API Gateway에서 요청을 **가공(매핑) 후 전달** (매핑 템플릿 필요)

#### Amazon Kinesis + Lambda
- 이벤트 소스 매핑
- 실시간 데이터 스트림에서 이벤트 발생 감지(polling) → Lambda 함수 호출  
    - 실시간 로그 분석 및 데이터 처리
    - 이벤트 기반 데이터 파이프라인 구축
    - 실시간 데이터 변환 및 저장 (e.g. Kinesis → Lambda → S3, DynamoDB, Redshift)

#### Amazon DynamoDB + Lambda
- 이벤트 소스 매핑
- DynamoDB Streams 이벤트 발생 감지(polling) → Lambda 함수 실행
    - 데이터 처리 및 동기화 (e.g. DynamoDB → Lambda → S3, Elasticsearch)
    - 비즈니스 로직 자동 실행 (e.g. 신규 고객 추가 시 자동 환영 이메일 전송)

#### Amazon SQS + Lambda
- 이벤트 소스 매핑
- SQS 대기열에서 메시지 도착 감지(polling) → Lambda 함수 실행

#### Amazon S3 + Lambda
- 비동기식 호출 
- S3 버킷에서 이벤트 발생 시 (S3 Event Notification) → Lambda 함수로 전송
    - 이미지 자동 리사이징
    - 비디오 썸네일 생성 
    - Metadata Sync
        - S3에 객체가 업로드될 때, 객체의 메타데이터를 DynamoDB 테이블이나 RDS DB의 테이블로 동기화 
        
#### Amazon EventBridge + Lambda
- 비동기식 호출 

#### Amazon CloudWatch Logs + Lambda
- 비동기식 호출 
- 로그 이벤트 발생 시 → Lambda 함수 실행

#### Amazon SNS + Lambda
- 비동기식 호출 
- SNS Topic에서 메시지 게시 → 메시지 payload와 함께 Lambda 함수 호출 

#### Amazon Cognito + Lambda
- 사용자 인증 및 권한 부여 과정 중 **사전에 정의한 특정 시점** → Lambda 함수 실행
    - Lambda 트리거
        - 인증 → Pre / Post Authentication
        - 가입 → Pre Sign-up, Post Confirmation, Migrate User
        - 메시지 → Custom Message

#### CloudFront + Lambda
- CloudFront 이벤트
    - Viewer Request → 사용자의 요청이 수신되었을 때 실행
    - Viewer Response → 사용자에게 응답을 반환하기 전에 실행
    - Origin Request → CloudFront가 Origin(e.g. S3, EC2)으로 요청을 전달하는 경우에만 실행
    - Origin Response → CloudFront가 Origin(e.g. S3, EC2)로부터 응답을 수신한 후 실행 (응답 캐싱)

- **CloudFront Functions**
    - CloudFront의 **네이티브 기능**
    - 218개 이상의 엣지 로케이션에서 실행
    - 단순 Request/Response 조작에 최적화
        - 캐시 키 조작 및 정규화
        - HTTP 헤더 조작
        - URL 다시 쓰기 및 리디렉션
        - 액세스 권한 부여(인가)
    - 단기 실행 경량 함수, 비용이 저렴하고, 매우 빠르게(µs 단위) 대량 트래픽에 적합
        - Lambda@Edge 요금의 약 1/6의 비용

- **Lambda@Edge**  
    ![Image](https://github.com/user-attachments/assets/4384730d-8178-41a1-81e0-bcc0e0c61fbc)

    - **AWS Lambda의 확장된 기능**
        - Lambda를 통해 CloudFront의 엣지 로케이션에서 코드를 실행할 수 있도록 지원
    - CloudFront 리전별 엣지 캐시 및 일부 AWS 리전에서 실행
    - `us-east-1`에서만 작성 가능 
        - AWS 리전(`us-east-1`)에 작성하면 CloudFront에서 모든 로케이션에 복제 
    - 복잡한 로직 처리 가능 (AWS 서비스와 연동 가능)
        - JWT 인증, 이미지 변환 등의 기능 수행 가능
    - 상대적으로 느림, 실행 시간이 상대적으로 길고 비용이 더 비쌈

- **CloudFront Functions vs Lambda@Edge** ❗️
    |      | CloudFront Functions | Lambda@Edge |
    |------|-----------------|--------------|
    | **프로그래밍 언어** | JavaScript | Node.js, Python |
    | **실행 속도** | 초당 수백만 개의 요청 (마이크로초(µs) 단위) | 초당 수천개의 요청 (밀리초(ms)) |
    | **이벤트 소스 (Trigger)** | Viewer Request / Response | Viewer Request / Response <br> Origin Request / Response |
    | **최대 실행 시간** | < 1ms | Up to 5s (viewer request / response) <br> Up to 30s (origin request / response) |
    | **최대 메모리** | 2MB | 128MB (viewer request / response) <br> 10,240MB (origin request / response) |
    | **총 패키지 크기 (라이브러리 포함)**| 10 KB | 50MB |
    | **Network / File system access** | No | Yes |
    | **Access to the request body** | No | Yes |
    | **요금** | Free Tier 지원 <br> 요청당 과금 | Free Tier 미지원 <br> 요청 & 실행 시간(duration)당 과금 |

### Lambda in VPC 
> [!NOTE]  
> 모든 Lambda 함수는 Lambda 서비스가 소유하고 관리하는 VPC 내에서 실행된다. 이러한 VPC는 Lambda에 의해 자동으로 유지 관리되며 고객에게는 표시되지 않는다.  

- Lambda 네트워크 모드
    - VPC mode
    - no-VPC mode (default)

#### no-VPC mode
- AWS가 관리하는 VPC(AWS-owned VPC)에서 실행되는 기본 상태 
    - AWS Public 서비스(e.g. S3, SNS, SQS, Kinesis 등)에 접근 가능 
        - AWS 내부 네트워크를 통해 접근 
        - IAM 권한 필요
    - **인터넷 액세스 가능**
        - 외부 API와 연동 가능 
        - 3rd party 데이터베이스 접근 가능 
    - **자체 VPC 내 Private Subnet의 리소스(e.g. RDS, ElasticCache, Internal ELB)에 접근 불가 ❌**
        
#### VPC mode
- 사용자의 VPC(Customer VPC) 내 Public 또는 Private Subnet에서 실행되는 상태 
- **인터넷 액세스 불가 ❌**
    - Private Subnet은 기본적으로 인터넷에 연결되지 않음
    - 외부 API 요청 불가능 = 외부 서비스와 통신 불가
    - 단, CloudWatch Logs는 내부 AWS 네트워크를 통해 작동하므로 어떤 상황에서든 작동
- **자체 VPC 내 Private Subnet의 리소스에 접근 가능** 

#### VPC mode + NAT Gateway / Instance
> [!NOTE]  
> NAT Gateway는 Private Subnet에서 온 트래픽을 인터넷으로 전달하는 역할을 담당 
- 사용자의 VPC(Customer VPC) 내 Private Subnet에서 실행되는 상태 
- **인터넷 액세스 가능**
    - Private Subnet → NAT Gateway → Internet Gateway(IGW) → 외부 인터넷 연결
- **자체 VPC 내 Private Subnet의 리소스에 접근 가능** 

#### VPC mode + VPC Endpoints
- 사용자의 VPC(Customer VPC) 내 Public 또는 Private Subnet에서 실행되는 상태 
- **인터넷 액세스 불가하지만, 인터넷 없이 AWS 서비스와 연결 가능** 
    - AWS PrivateLink 또는 Gateway Endpoint를 통해 접근
        - Gateway Endpoint → S3, DynamoDB
        - Interface Endpoint (AWS PrivateLink) → SSM, SNS, SQS, Kinesis 등
- **자체 VPC 내 Private Subnet의 리소스에 접근 가능** 

#### Lambda 네트워크 모드 비교 
| | 실행 위치 (Subnet) | 인터넷 액세스 | AWS Public 서비스 접근 | Private Subnet 리소스 접근 |
|-|------------------|-----------|---------------------|--------------------------|
| **no-VPC mode**      | AWS-owned VPC | 가능      | 가능 | 불가 |
| **VPC mode**         | Public 또는 Private Subnet | 불가 | 가능  | 가능 |
| **VPC mode + NAT**   | Private Subnet | 가능 | 가능 | 가능 |
| **VPC mode + VPC Endpoints** | Public 또는 Private Subnet | 불가 | 가능 | 가능 |

#### VPC Access 설정 과정 
1. 사용할 VPC, Subnet 생성, Security Group 정의 
1. Lambda 함수에서 VPC 설정 추가
    - 내부적으로 **Elastic Network Interface(ENI)** 를 생성하여 VPC의 서브넷에 연결
        - ENI를 관리하기 위해 `AWSLambdaVPCAccessExecutionRole` 필요 
1. 네트워크 설정 (인터넷 액세스 필요 시)
    - NAT Gateway 생성
        - Public Subnet에 NAT Gateway 배포
        - Elastic IP 할당
    - Route Table 수정
        - Private Subnet → NAT Gateway로 라우팅 

### Deploying AWS Lambda functions with CloudFormation
- AWS Lambda 배포 방법 
    - AWS Management Console 
    - AWS CLI 
    - AWS CloudFormation
    - AWS SAM 
    - AWS CDK(Cloud Development Kit) 

#### CloudFormation을 사용한 Lambda 함수 배포
> `AWS::Lambda::Function`

- Lambda 함수와 관련된 모든 AWS 리소스를 코드(YAML/JSON)로 선언적으로 정의하여 배포 
    - 수동 설정 없이 코드 기반으로 배포
    - deployment package(`.zip` 파일)와 execution role 필요 
- Lambda 함수 배포 방식 
    - **인라인 배포** → 빠르고 간단한 배포
        - Lambda 함수를 CloudFormation 템플릿 내부에 직접 코드로 포함하는 방식
            - `Code.ZipFile` 속성을 사용하여 함수 정의 → 내부적으로 deployment package 생성 
            - 최대 4MB 초과 불가 
            - **외부 라이브러리(종속성)를 포함시킬 수 없음**

    - **S3 참조 배포**
        - Lambda 코드를 S3 버킷에 업로드 → CloudFormation 템플릿에서 해당 S3 파일을 참조하는 방식
            - `S3Bucket`, `S3Key`, `S3ObjectVersion` 속성 사용 
        - **Multi-Account 배포 가능**
            - CloudFormation StackSets을 활용하여 여러 AWS 계정에 배포 가능
            - Cross-Account IAM Role & S3 버킷 정책 설정 필요
  
### 1.3 애플리케이션 개발 시 데이터 스토어를 사용합니다.
---
<details>
<summary>  
    <b>Knowledge of:</b>
</summary>

- 관계형 데이터베이스 및 비관계형 데이터베이스
    - 관계형 데이터베이스(RDB)
        - 열과 행이 있는 테이블에 데이터를 저장
        - 데이터 무결성과 일관성을 유지하면서 **정형 데이터**에 대한 복잡한 쿼리를 처리 가능
            - Amazon Relational Database Service(RDS)

    - 비관계형 데이터베이스(NoSQL)
        - 키-값, 문서 또는 그래프 
        - 이미지, 비디오, 문서 및 기타 **반정형 및 비정형 데이터**를 저장하는 데 사용
            - Amazon DynamoDB
            - Amazon DocumentDB (MongoDB 호환)
            - Amazon MemoryDB
            - Amazon Neptune

- 클라우드 스토리지 옵션
    - 객체 스토리지(Object Storage) → Amazon S3
    - 블록 스토리지(Block Storage) → Amazon EBS, EC2 Instance Store
    - 파일 스토리지(File Storage) → Amazon EFS, Amazon FSx
    - 백업 및 아카이브 스토리지 → AWS Backup, S3 Glacier

- 클라우드 스토리지 유형 비교  
    - 파일 스토리지
        > Network Attached Storage(NAS) 서버에서 지원되는 경우가 많음 

        - 각 파일을 단일 데이터 단위로 취급 (변경 시, 전체 파일 재업로드)
        - 여러 호스트 컴퓨터에서 쉽게 공유 및 관리해야 하는 파일에 대한 중앙 집중식 액세스가 필요한 경우에 적합
            - 웹 애플리케이션과 통합
            - 분석 워크플로와 통합 
            - 미디어 및 엔터테인먼트
            - 홈 디렉터리

    - 블록 스토리지
        > Direct Attached Storage(DAS) 또는 Storage Area Network(SAN)와 유사

        - 파일을 고유한 주소를 가진 고정된 크기의 데이터 청크로 분할하여 저장 
        - 지연 시간이 짧은 작업에 최적화
            - 트랜잭션 워크로드 
            - 컨테이너 저장 
            - 가상 머신(VM) 
    
    - 객체 스토리지
        - 파일과 마찬가지로 객체는 저장될 때 구분된 단일 데이터 단위로 처리
        - 일반적으로 대규모 또는 비정형 데이터 집합을 저장하는 데 유용
            - 데이터 아카이빙
            - 백업 및 복구
            - 리치 미디어 

- 데이터베이스 일관성 모델(Database Consistency Model)
    - 최종 일관성(Eventual Consistency)
        - 일시적으로 비일관성 상태 허용 
    - 강력한 일관성(Strong Consistency)
        - 모든 노드에서 데이터를 읽고 쓸 때 동일한 값을 즉시 반환
    - 즉시 일관성(Immediate Consistency)
        - 시스템에 변경이 일어났을 때, 즉시 모든 복제본에 반영
        - 주로 단일 노드 시스템에서 사용
    - 약한 일관성(Weak Consistency)
        - 데이터의 동기화가 즉시 이루어지지 않지만, 시스템이 계속 동작하면서 결국 일관성을 맞춤 

- 쿼리 작업과 스캔 작업의 차이점    
    > DynamoDB에서는 데이터를 조회하는 방법으로 쿼리(Query)와 스캔(Scan)을 제공한다. 

    - 쿼리 작업 
        - 인덱스를 기반으로 특정 조건에 맞는 항목만 가져온다.  
    - 스캔 작업
        - 1\) 전체 테이블이나 보조 인덱스를 스캔 후 2\) 값을 필터링하여 결과를 가져온다.  
            → Full Table Scan과 유사
        - 병렬 스캔(Parallel Scan)

- Amazon DynamoDB 키 및 인덱싱
    - 키(Keys)
        - 파티션 키(Partition Key) 
        - 파티션 키(Partition Key) 및 정렬 키(Sort Key)  
    - 인덱스(Indexes)
        - 글로벌 보조 인덱스(GSI)
        - 로컬 보조 인덱스(LSI)

- 캐싱 전략
    - 동시 쓰기(Write-through) → `Write Penalty`
    - 동시 읽기(Read-through)
    - 지연 로드(Lazy Loading / Cache-Aside / Lazy Population) → `Reads Penalty`
    - TTL(Time to Live)

- 임시 데이터 스토리지 패턴과 영구 데이터 스토리지 패턴 비교
    - 임시 스토리지(Ephemeral Storage) = 휘발성 스토리지
        - EC2 Instance Store, AWS Lambda Ephemeral Storage (`/tmp`), Amazon ElastiCache 

    - 영구 스토리지(Persistent Storage)
        - Amazon S3, Amazon EBS, Amazon RDS, Amazon DynamoDB 
</details>

---

### Amazon EC2 Instance Store
- EC2 인스턴스를 호스팅하는 것과 동일한 물리적 서버에 존재하는 **임시 블록 스토리지**
    - 물리적으로 연결된 저장소로 I/O 속도가 매우 빠름 
    - 인스턴스 사용 비용에 포함 → 비용 효율적 솔루션

- 주의 사항
    - 데이터의 수명 주기가 EC2 인스턴스 수명 주기와 연동 →  인스턴스 종료(Terminate) 시 데이터 소멸
    - 특정 인스턴스에 직접 연결됨 → **인스턴스 간 파일 공유에 사용 불가**

- 사용 사례 
    - 데이터를 Hadoop 클러스터 등 다른 EC2 인스턴스로 복제하는 애플리케이션을 호스팅하는 경우
    - 버퍼, 캐시, 스크래치 데이터 및 기타 임시 콘텐츠 저장소 

### Amazon Elastic Block Store(Amazon EBS)
- <u>Amazon EC2 인스턴스에 연결할 수 있는</u> 고성능 블록 수준 스토리지
- 특징
    - EC2 인스턴스에서 EBS 볼륨을 분리 가능 (이후 다른 인스턴스에 연결 가능)
    - EC2 인스턴스를 중지/종료하더라도 연결된 EBS 볼륨의 데이터는 보존 (별도의 생명 주기) 
    - EBS Snapshot 기반 **증분 백업** 지원 

- 주의 사항
    - 루트 볼륨의 경우, 기본적으로 인스턴스 **종료** 시 삭제(Delete on Termination) 옵션 활성화 
    - 특정 단일 가용 영역에 EBS 볼륨 생성
        - **동일한 가용 영역의 인스턴스에만 연결 가능 = AZ 수준 리소스**
    - 기본적으로 EC2 인스턴스와 EBS 볼륨은 1:n 관계 (io1, io2 제외)
        - **EBS Multi Attach** → 동일한 EBS 볼륨을 동일한 AZ의 여러 인스턴스에 연결
            - <u>io1/io2 제품군에서만 사용 가능</u> 
            - 각 인스턴스는 full read & write 권한을 가짐
            - 하나의 볼륨을 <u>**한 번에 최대 16개의 EC2 인스턴스에 부착 가능**</u>
            - 클러스터를 인식할 수 있는(cluster-aware) 파일 시스템을 사용해야 한다. 
    - 볼륨 유형별 저장할 수 있는 최대 용량 제한 있음

- 사용 사례 

#### EBS Snapshot
- 마지막 스냅샷 이후 변경된 볼륨의 블록만 저장 = 증분 백업 
- Amazon S3을 사용하여 여러 가용 영역(AZ) 또는 리전에 백업이 중복 저장 (AWS에서 처리)
- 주요 기능 
    - EBS Snapshot Archive → 장기 백업 
    - Recycle Bin for EBS Snapshots → 영구 삭제 전 임시 보관 (복구 목적)
    - Fast Snapshot Restore (FSR) → 빠른 복구가 필요한 경우

#### EBS 볼륨 유형 ❗️
> [!NOTE]  
> 크기, 처리량(Throughput), 초당 입출력 작업 수(IOPS, I/O Ops Per Sec)에 따라 구분 

- **SSD 볼륨** 
    - 범용(General Purpose) SSD → gp2, gp3
    - 프로비저닝 된 IOPS SSD → io1, io2 Block Express

- **HDD 볼륨** → <u>EC2 인스턴스를 생성할 때 boot volume으로 사용 불가능 ❌</u>  
    - 처리량 최적화 HDD → st1
    - 콜드 HDD → sc1
    - 마그네틱 → standard

### Amazon Elastic File System(Amazon EFS)
- 관리형 네트워크 파일 시스템(Managed NFS)
- 특징
    - 볼륨 자동 확장/축소 → 미리 스토리지를 프로비저닝할 필요 ❌
    - 페타바이트(PB) 단위 데이터 저장 가능
    - **여러 AZ, 여러 인스턴스에서 동시에 액세스 가능**
        - 데이터를 여러 가용 영역(AZ)에 걸쳐 자동으로 복제, 중복 저장  
            → 하나의 가용영역이 파괴되더라도 다른 AZ에서 서비스 제공 가능(높은 가용성, 데이터 내구성)
    - NFSv4.1 프로토콜을 사용 
    - 보안 그룹 설정을 통해 EFS 액세스 제어 가능 

- 주의 사항
    - 리전 레벨 리소스 
    - Linux 기반 EC2 AMI와만 호환(Windows ❌)

#### 파일 시스템 유형 & 스토리지 클래스 
- **Regional** (권장)
    > AWS 리전내에서 지리적으로 분리된 여러 가용 영역에 데이터를 중복 저장

    - EFS Standard → 자주 액세스하는 데이터, 높은 성능 
    - EFS Standard-Infrequent Access(Standard-IA) → 자주 액세스하지 않는 데이터, 비용 절감 효과
    - EFS Archive

- **One Zone** 
    > 단일 가용 영역 내에 데이터를 저장
    - EFS One Zone
    - EFS One Zone-Infrequent Access(EFS One Zone-IA)

#### 성능 모드(Performance Mode)
> [!NOTE]  
> EFS 파일 시스템 생성 시 설정

| 모드 | 특징 | 사용 사례 |
|--------|------|--------|
| **General Purpose** (default) | 최소 Latency 제공 | 일반적인 파일 스토리지, 웹 애플리케이션 |
| **Max I/O** | 병렬 처리 최적화 (일반 성능 모드보다 Latency가 증가할 수 있음) | 빅데이터, 대규모 데이터 처리 |

#### 처리량 모드(Throughput Mode)
> [!NOTE]  
> 운영 중 변경 가능 

| 모드 | 특징 | 사용 사례 |
|----------|-----|---------|
| **Elastic Throughput** (권장) | 자동으로 애플리케이션의 요구 사항에 맞게 처리량을 조절 | 변동성이 큰 워크로드 |
| **Provisioned Throughput** | 사용자가 예약한 일정한 처리량 제공 | 예측 가능한 워크로드 |
| **Bursting Throughput** | 스토리지의 저장 용량에 비례하여 처리량을 확장 | 특정 시간대에 부하가 집중되는 워크로드 |

### Amazon FSx
- AWS에서 완전 관리형으로 제공하는 파일 스토리지 서비스
- 특징 
    - 서드 파티 파일 시스템과 네이티브 호환성을 제공
- 유형 
    - Amazon FSx for NetApp ONTAP → 하이브리드 클라우드 환경
    - Amazon FSx for OpenZFS
    - Amazon FSx for Windows File Server → Windows 기반 파일 공유
    - Amazon FSx for Lustre → 빅데이터 분석 & AI/ML

- 사용 사례 
    - 기존 온프레미스 NAS를 클라우드로 이전
    - 고성능 데이터 처리 및 AI/ML 분석
    - 하이브리드 클라우드 환경 구축

### Amazon Simple Storage Service(Amazon S3)
`리전 레벨`, `백업 · 스토리지`

- 컴퓨팅과 연동되지 않는 독립형 객체 스토리지 서비스
- 특징 
    - 데이터를 버킷(Bucket)이라는 컨테이너에 객체(Object)로 저장
        - 계층 구조 없이 객체를 저장 (flat namespace)
        - 객체(Object)는 Amazon S3 관리 키(SSE-S3)로 서버 측 암호화를 사용하여 자동으로 암호화
    - 파일 업로드 시, 권한 설정 → 파일에 대한 표시 여부 및 액세스를 제어 가능
    - Amazon S3 버전 관리 기능 제공 
    - Amazon S3 데이터 SQL 기반 분석 → Amazon Athena
    - 무제한에 가까운 확장성 

- 주의 사항
    - 버킷의 이름은 DNS를 준수해야 하며, <u>**전역적으로** 고유</u>해야 함
    - 업로드 가능한 객체의 최대 파일 크기는 5TB(5000GB)
        - 5GB보다 큰 파일을 업로드하고 싶다면, **multi-part 업로드**를 사용해야 함  
            → **파일이 100MB를 초과하는 즉시 멀티파트 업로드를 권장**

#### S3 버킷(Bucket)
- 객체는 키(full path)를 가진 파일 
- 객체는 버킷 이름, 키, 버전 ID를 포함한다.
- 모든 유형의 파일(이미지, 동영상, 텍스트 파일 등)을 업로드 가능

- 버킷 네이밍 규칙 
    - 버킷 이름은 최소 3자, 최대 63자여야 합니다.
    - 버킷 이름은 소문자, 숫자, 점(.) 및 하이픈(-)으로만 구성할 수 있습니다.
    - 버킷 이름은 문자 또는 숫자로 시작하고 끝나야 합니다.
    - 버킷은 IP 주소 형식이 아니어야 합니다.
    - 버킷 이름을 동일한 파티션 내의 다른 AWS 계정에서 사용하지 않아야 합니다. 해당 버킷이 
    삭제되어야 그 이름을 사용할 수 있습니다.

#### S3 버전 관리 
→ 객체 변경 사항 추적 가능 
- 버전 관리 활성화, 기존 파일의 버전 = null
- delete marker

#### S3 버킷 정책
> 모든 항목은 비공개가 기본값

- 버킷에 대해 허용 또는 거부되는 작업이 무엇인지 정의하는 JSON 형식의 규칙 
- S3 버킷 정책은 S3 버킷에만 연결할 수 있음 (특정 폴더, 객체 ❌)

- 리소스 기반 정책(Resource-Based)
    - Bucket Policies → 특정 사용자, 계정에 버킷 권한 
    - Object ACL(Access Control List)
    - Bucket ACL(Access Control List)

#### S3 암호화(Encryption)
- Server-Side Encryption `Default`
    - SSE-S3 (AES-256)
    - SSE-KMS (AWS KMS-managed keys)
    - SSE-C (고객 제공 키)
- Client-Side Encryption

#### S3 Replication
> 최저 지연 시간과 비용
- 버전 관리 기능 활성화 필요 
- Replication rule, IAM role 생성 
- 복제 활성화 시점, 기존 소스 버킷 객체 복제 → optional
- 영구 삭제의 경우 동기화 x 
- Delete markder replication만 동기화 
- 유형
    - Cross-Region Replication(CRR) → 리전 간 복제 
    - Same-Region Replication(SRR) → 동일 리전 복제 

- **Amazon S3 Transfer Acceleration**  
    클라이언트와 S3 버킷 간의 장거리 파일 전송을 파일을 빠르고 쉽고 안전하게 전송할 수 있는 버킷 수준 기능

#### S3 Storage Classes
> [!NOTE]  
> 모든 클래스의 내구성은 동일, 가용성은 스토리지 클래스에 따라 상이하다.

- **S3 Standard**
    - 자주 액세스하는 데이터를 위해 높은 내구성, 가용성 및 성능을 갖춘 스토리지 제공
    - 짧은 지연 시간 및 많은 처리량 성능
    - AZ >= 3에 데이터를 저장

- **S3 Intelligent-Tiering**    
    - 데이터 액세스 패턴을 알 수 없거나 액세스 패턴이 변경되는 데이터 보관
        - **객체의 액세스 패턴을 모니터링**  
            → 30일 연속 객체에 액세스하지 않으면 자동으로 계층 이동
    - 월별 객체 모니터링 비용과 자동 이동 비용 발생 
    - AZ >= 3에 데이터를 저장

- **S3 Standard-Infrequent Access(S3 Standard-IA)**
    - 자주 액세스하지 않지만 필요할 때 빠르게 액세스해야 하는 데이터 보관
        → 백업, 재해 복구 파일 또는 장기 보관이 필요한 모든 객체에 적합 
    - AZ >= 3에 데이터를 저장

- **S3 One Zone-Infrequent Access(S3 One Zone-IA)**  
    - 낮은 액세스 빈도를 가지고 있지만 필요할 때 빠르게 액세스해야 하는 데이터 보관
    - **단일 AZ**에 데이터 저장   
        - 가용성 및 복원력이 필요 없는 경우(e.g. 쉽게 재생성이 가능한 경우) 
        - S3 Standard-IA보다 비용이 20% 저렴

- **S3 Glacier**
    > `콜드 데이터(Cold Data)`, `암호화(AES-256)`

    - 데이터 보관을 위한 안전하고 내구성이 있으며 저렴한 스토리지 제공 
    - 객체를 몇 분에서 몇 시간 이내에 검색
    - 256비트 고급 암호화 표준(AES-256)으로 서버측 자동 암호화 
    - 잠금 정책 
        - 한 번 쓰기/여러 번 읽기(WORM)
    - Glacier Instant Retrieval
    - Glacier Flexible Retrieval (기존 Glacier)
    - Glacier Deep Archive
        - 검색시간 요구 사항이 없는 경우
        - 데이터의 장기 보관 및 디지털 보존
        - 객체를 **12시간 또는 48시간** 내에 데이터 검색

#### S3 Lifecycle Rules

### Amazon Relational Database Service(Amazon RDS)
- 데이터베이스 관리 작업 자동화 
    - 프로비저닝, 구성, 패치 적용, 백업, 이중화, 장애 조치, 재해 복구과 같은 데이터베이스 관리 작업을 자동화
        - **Storage Auto Scaling** 지원
        - 자동 백업 기능 및 특정 시점 복구(Point-in-Time Recovery) 제공
    - On-Premise 환경에서 Amazon RDS로 _Lift and Shift(Rehost)_ 마이그레이션 가능(AWS DMS)  
- 고객이 데이터, 스키마 소유 및 네트워크 제어
- 주요 데이터베이스 엔진 지원  
    <small>
    - 상용
        - Oracle
        - Microsoft SQL Server
    - 오픈 소스 
        - MySQL
        - PostgreSQL
        - MariaDB
    - 클라우드 네이티브 
        - Amazon Aurora
    </small>

#### Amazon RDS 배포 옵션
- Single-AZ
- Multi-AZ 
    - 동기식 복제(Sync Replication)  
    - 가용 영역(AZ) 수준 장애 보호 = 리전 장애로부터 보호 ❌
        - 주로 재해 복구, Failover 시 사용 (Standby ↔︎ Master)
    - **Single-AZ에서 Multi-AZ로 전환 시 다운타임이 발생하지 않음**
- Read Replicas  
    - 비동기식 복제(Async Replication) → 최종 일관성(Eventual Consistency)
    - 읽기 작업이 많은 워크로드 부하 분산에 적합
    - 각 복제본마다 **별도의 엔드포인트(DNS 이름)** 생성
    - 동일 AZ, Cross AZ 혹은 Cross Region에 최대 5개까의 인스턴스 생성 가능  
        → <u>Cross Region은 네트워크 복제 비용 발생</u>

#### Amazon RDS Proxy
- 모든 애플리케이션을 데이터베이스 인스턴스가 아닌 RDS Proxy에 연결 
    - 데이터베이스에 직접적인 연결 최소화 (리소스 스트레스 감소 및 장애 조치 시간 최소화)
- MySQL, PostgreSQL, MariaDB 지원
- **데이터베이스에 대한 IAM 인증 시행**
- 공개적으로 액세스할 수 없음 = Private subnet
    - VPC에서만 엑세스 가능

### Amazon Aurora
- AWS 독점기술 (오픈소스 ❌)
- PostgreSQL과 MySQL과 호환 
- 클라우드 최적화(cloud optimized) → RDS에서 PostgreSQL보다 3x, MySQL보다 5x 뛰어난 성능 
- 공유 스토리지 볼륨을 10GB에서 128TB까지 자동 확장(Auto Expanding) 
- 최대 15개의 읽기 전용 복제본 보유 가능 (MySQL의 경우 최대 5개)
- 즉각적인 Failover → 고가용성(HA)
- 3개의 AZ에 걸쳐 6개의 사본을 저장 = **다중 AZ와 유사**
    - 쓰기에는 4개, 읽기에는 3개의 사본이 필요 
- 자가 복구 P2P 복제 

#### Aurora DB Cluster 
- Writer Endpoint
- Reader Endpoint
    - 연결 로드 밸런싱 

### Amazon DynamoDB
- 완전관리형 NoSQL 서버리스 데이터베이스
    - 조인이나 집계 함수의 사용이 어려움
- 높은 동시성과 연결성
- 데이터를 분산 방식으로 저장하므로 수평적 확장성을 가짐.
- 여러 AZ에 걸쳐 복제 가능 

- 구성 요소
    - 테이블(Tables)
        - 기본 키(Primary Key)
            > [!IMPORTANT]  
            > 특정 키 값이 한 파티션에 몰리지 않도록 높은 카디널리티(High Cardinality) 파티션 키를 사용하는 것이 중요하다.  

            - 파티션 키(Partition Key) → HASH
            - 파티션 키(Partition Key) 및 정렬 키(Sort Key) → HASH + RANGE
        
        - 인덱스(Indexes)
            - 글로벌 보조 인덱스(GSI, Global Secondary Index)
                - **쓰기가 GSI에서 쓰로틀(throttled)되면, 메인 테이블도 쓰로틀됨**
            - 로컬 보조 인덱스(LSI, Local Secondary Index)
                - 테이블 생성 시점에 생성 (이후 생성 불가)
                - 테이블 당 최대 5개 LSI까지 허용 

    - 항목(Items) = rows
       - 고유하게 식별할 수 있는 속성들의 집합  
        - 테이블에 저장할 수 있는 항목 수에 제한이 없음  
            → **각 항목 데이터의 최대 크기는 400KB**
    - 속성(Attributes)
        - 각 항목은 하나 이상의 속성으로 구성

- 읽기/쓰기 용량 모드(R/W Capacity Modes)
    > [!NOTE]  
    > 24시간 마다 모드 변경 가능 

    - 프로비저닝 모드(Provisioned Mode) `default`
        - 초당 R/W 지정 
        - Read Capacity
            - Read Capacity Units(RCU)
                - 강력 일관성 읽기 모드(Strongly Consistent Read)
                    - 최대 4KB의 항목에 대해 초당 **1개의 읽기**  
                    - API 호출 시 `ConsistentRead` 파라미터 true 설정 필요 
                - 최종 일관성 읽기 모드(Eventually Consistent Read) `default`  
                    - 최대 4KB의 항목에 대해 초당 **2개의 읽기**  

            - Write Capacity Units(WCU)
                - 최대 1KB의 항목에 대해 초당 1개의 쓰기  
                    > ![WARNING]  
                    > 초당 6개의 항목, 개당 4.5KB 크기 → 30WCUs 
            - Transcational

        - 버스트 용량(Burst Capacity)을 다 소진 → `ProvisionedThroughputExceededExpection` 오류 발생 

    - 온디멘드 모드(On-Demand Mode)
        - RCU / WCU를 지정할 필요가 없음 
        - Read Request Units(RRU)
        - Write Request Units(WRU)

#### Table 클래스 
- Standard
- Standard-IA


### Amazon MemoryDB
- Redis 호환 인메모리 DB
- 초당 1억 6천만건의 요청을 처리하는 초고속 성능 
- 스케일을 10GB ~ 100TB 이상까지 원활하게 조정
- Multi AZ 트랜잭션 로그 → 빠른 복구와 내구성 

- 사용 사례 
    - 웹 및 모바일 애플리케이션
    - 온라인 게임
    - 미디어 스트리밍 

### Amazon ElastiCache
- AWS의 완전 관리형 분산 인메모리(In-memory) 캐싱 서비스
- 읽기 집중적인 작업 부하에서 데이터베이스의 부하를 줄이는데 도움 
- KVS(Key-Value Store)형 데이터베이스 엔진 지원
    - Amazon ElastiCache for Memcached
    - Amazon ElastiCache for Redis
- 클러스터 모드가 비활성화된 ElastiCache Redis 클러스터에 추가할 수 있는 읽기 전용 복제본의 최대 수는 5개 
- 사례
    - DB 캐시 (최신 데이터를 위한 캐시 무효화(cache invalidation) 전략이 필요 )
    - 유저 세션 스토어 ↔︎ Sticky Session
    

#### Amazon ElastiCache for Memcached
> `sharding`

- 여러 노드를 설정하여 데이터를 파티셔닝 (sharding)
- HA, Replication 없음 
- 문제가 발생하면 전체 캐시 소실 가능 
    - 서버리스 버전에서 백업 및 복원 기능 제공
- 멀티 스레드 아키텍쳐  

#### Amazon ElastiCache for Redis
> `Replication`

- Auto Failover, Multi AZ (추가 비용 발생)
- 읽기 복제본(read replicas)를 생성하여 읽기 작업을 확장하고, HA 제공 
- AOF(Append-Only File) 지속성을 사용하여 데이터 내구성 제공  
    → 모든 쓰기 명령을 기록
- 백업 및 복원 기능 제공 
- Set과 Sorted Set 지원 

### 기타 AWS 데이터베이스
- Amazon DocumentDB `문서`, `MongoDB 워크로드 지원`
- Amazon Neptune `그래프 DB`, `NoSQL`
- Amazon QLDB(Quantum Ledger Database) `완전 관리형 원장 DB`, `변경 불가능`
- Amazon Managed Blockchain `탈중앙화(decentralized)`, `분산형 원장 시스템`
- Amazon Keyspaces `와이드 컬럼 DB`, `산업용 대규모 애플리케이션(장비 유지 관리, 플릿 관리, 라우팅 최적화용)`
