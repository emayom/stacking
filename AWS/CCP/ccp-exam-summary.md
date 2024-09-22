# AWS Certified Cloud Practitioner(CLF-C02) 
### Domain 1: Cloud Concepts 🌕🌕🌗🌑🌑

#### 클라우드 컴퓨팅 유형  
- **IaaS**: Amazon EC2, Amazon S3, Amazon VPC
- **PaaS**: AWS Elastic Beanstalk, AWS Lambda, Amazon RDS
- **SaaS**: Amazon WorkSpaces, Amazon Chime, AWS CodePipeline

#### AWS Well-Architected Framework의 원칙
1. 운영 우수성(Operational Excellence)
1. 보안(Security)
1. 신뢰성(Reliability)
1. 성능 효율성(Performance Efficiency)
1. 비용 최적화(Cost Optimization)
1. 지속 가능성(Sustainability)

#### AWS Cloud Adoption Framework(AWS CAF)의 6가지 관점
1. 비즈니스(Bussiness)
1. 인력(People)
1. 거버넌스(Governance)
1. 플랫폼(Platform)
1. 보안(Security)
1. 운영(Operations)

#### AWS CAF Transformation Phases
1. 비전 수립 단계(Envision) `비즈니스 기회 식별 · 우선 순위 지정`
1. 정렬 단계(Align)
1. 실행 단계(Launch)
1. 확장 단계(Scale)

#### 클라우드 마이그레이션 전략(7Rs)
1. Retire
1. Retain 
1. Rehost `lift and shift`
1. Relocate
1. Repurchase `drop and shop`
1. Replatform `lift and reshape`
1. Refactor/Re-architect

#### 클라우드 마이그레이션 서비스 
1. AWS Migration Hub
1. AWS Migration Evaluator `리소스 분석 및 계획 수립에 도움`
1. AWS Application Migration Service(MGN)
1. AWS Database Migration Service(DMS)
1. AWS Server Migration(SMS)
1. AWS Snow Family `물리적 장치`
    - AWS Snowcone `최대 8TB`
    - AWS Snowball Edge `최대 수 페타바이트 규모`, `반복적인 전송 워크플로우` 
        - Snowball Edge **Storage** Optimized  
        - Snowball Edge **Compute** Optimized  

    - AWS Snowmobile `최대 엑사바이트 규모`, `데이터 센터 수준` 

1. AWS DataSync
1. AWS CloudEndure Migration

### Domain 2: Security and Compliance 🌕🌕🌕🌑🌑

#### AWS 공동 책임 모델(Shared Responsibility Model)
- **AWS의 책임**: 클라우드 "**자체**"의 보안(Security "of" the Cloud)
- **고객의 책임**: 클라우드 "**내부**"의 보안(Security "in" the Cloud)
- **공유 책임**: 패치 관리, 구성 관리, 인식 및 교육 관리 

#### DDoS 공격 방지 서비스  
1. AWS Shield
1. AWS WAF
1. AWS CloudFront 및 AWS Route 53

#### AWS 네트워크 보안 서비스 
- AWS Shield `DDoS 공격 보호`
    - Standard `기본(무료)`
        - Layer 3 · 4
    - Advanced `고급 모니터링 및 보호`  
        - Layer 7
        - 24/7 DRT(DDoS Response Team)
        - 피해 완화 크레딧

    - 대상 리소스: Amazon CloudFront, Amazon Route 53, AWS Global Accelerator, Amazon EC2, Elastic Load Balancing(ELB)

- AWS WAF(Web Application Firewall) `Layer 7(HTTP(S))`, `웹 취약점 보호`
    - Web ACL(Access Control List)
        - SQL injection, Cross-Site Scripting(XSS) 보호 
        - Size constraint, Geographic match
        - Rate-based rules → IP 자동 차단, DDoS 공격 완화

    - 대상 리소스: Amazon CloudFront, Application Load Balancer(ALB), Amazon API Gateway

- AWS Network Firewall `Layer3-7`, `VPC 전반 보호`
- AWS Firewall Manager `방화벽 규칙 중앙 구성 · 관리`

#### AWS 암호화 서비스
- AWS KMS(Key Management Service) `암호화 키 생성, 저장, 관리`
    - KMS Key의 종류 
        - 고객 관리 키(Customer Managed Key)
        - AWS 관리 키(AWS Managed Key)
        - AWS 소유 키(AWS Owned Key)

- AWS CloudHSM `하드웨어 보안 모듈(HSM) 제공`

#### AWS 데이터 보안 및 개인정보 보호 서비스
- AWS Macie `S3 버킷 내의 민감 데이터 보호`
- AWS Secrets Manager `비밀 정보 안전하게 저장`
- AWS Certificate Manager(ACM) `SSL/TLS 인증서 관리`

#### AWS 액세스 관리 및 감사 서비스
- AWS IAM(Identity and Access Management) `권한 · 접근 제어`
    - AWS Security Token Service(AWS STS)
        - AWS 리소스에 대한 액세스를 제어할 수 있는 임시 보안 자격 증명 생성(단기적)

    - MFA(Multi-Factor Authentication)
        - Virtual MFA device `디바이스에 설치된 앱 사용` 
        - U2F(Universal 2nd Factor) security key  `USB 포트 연결 물리장치`
        - Other hardware MFA device `여섯 자리 숫자 코드 제공 물리장치` 
        - ~~SMS text message-based MFA~~ `지원 종료`

    - IAM JSON 정책 요소
        - Version
        - Id 
        - Statement `필수`
        - Sid
        - Effect `필수`
        - Principal / NotPrincipal
        - Action / NotAction `필수`
        - Resource / NotResource
        - Condition
        - Variables and tags
        - Supported data types

- AWS CloudTrail `보안 및 감사`
- AWS Artifact `보안 및 규정 준수 보고서`
- Amazon GuardDuty `AWS 계정 보호`, `지능형 위협 탐지`
- Amazon Inspector `자동화된 보안 평가(네트워크 노출 · 취약성)`
- AWS Trusted Advisor `비용 최적화, 보안 및 성능 개선`
    - 검사 범주 
        - 비용 최적화(Cost Optimization)
        - 성능(Performance)
        - 보안(Security)
        - 내결함성(Fault Tolerance)
        - 서비스 한도(Server Limits)
        - 운영 우수성(Operational Excellenc

- AWS Config `구성 변경 추적 및 기록`
- Amazon CloudWatch `리소스 성능 모니터링`, `알림`  
    - 청구 메트릭 데이터는 미국 동부(노스버지니아) 지역 `us-east-1`에 저장 

- Amazon CloudWatch Log `서버 로그 중앙 집중화`
- AWS CloudTrail `계정별 활동 및 감사`, `API 호출 기록`
    - 기본적으로 CloudTrail이 S3 버킷으로 전송하는 로그 파일은 Amazon S3 관리 키(SSE-S3)를 사용한 서버 측 암호화를 사용하여 암호화

- AWS Health Dashboard
    - Account health `특정 AWS 계정과 관련된 이벤트 및 상태`
    - Service health `전체 서비스 상태`, `전반적인 운영 상태`

### Domain 3: Cloud Technology and Services 🌕🌕🌕🌘🌑

#### 글로벌 범위의 AWS 서비스 
- AWS Identity and Access Management(AWS IAM)
- Amazon CloudFront
- Amazon Route 53
- AWS WAF

#### AWS 글로벌 인프라 
- Region `최소 3개 이상의 AZ`
    - 선택 시 고려사항  
        - 데이터 거버넌스 및 법적 요구 사항 준수
        - 고객과의 근접성
        - 기능 가용성
        - 요금

- Availability Zone(AZ) `최소 1개 이상의 데이터 센터`
- Edge Location `CDN` `캐싱`
- Regional Edge Cache
- Wavelength `5G 엣지 컴퓨팅`
- Local Zone `저지연`
- AWS Outposts `하이브리드 클라우드 환경`

#### Amazon EC2 인스턴스 유형
- 범용 인스턴스
- 컴퓨팅 최적화 인스턴스 
- 메모리 최적화 인스턴스
- 엑셀러레이티드 인스턴스 
- 스토리지 최적화 인스턴스

#### AWS 컨테이너 서비스
- Amazon Elastic Container Registry(Amazon ECR) `Docker 이미지 저장 · 관리 · 배포`
- Amazon Elastic Container Service(Amazon ECS) `Docker 컨테이너 애플리케이션 실행 · 중지 · 관리`
- Amazon Elastic Kubernetes Service(Amazon EKS) `Kubernetes`

#### AWS 서버리스 컴퓨팅 서비스 
- AWS Fargate `컨테이너용 서버리스 컴퓨팅 엔진`
- AWS Lambda

#### AWS Auto Scaling 
- 스케일링 전략 
    - 수동 스케일링(Manual Scaling)
    - 동적 스케일링(Dynamic Scaling)
        - 단순 스케일링(Simple Scaling)
        - 단계적 스케일링(Step Scaling)
        - 대상 추적 스케일링(Target Tracking Scaling)
        
    - 예측 스케일링(Predictive Scaling)
        - CloudWatch 기록 데이터 기반 필요량 예측

- Auto Scaling 그룹(ASG)
    - 최소 인스턴스 크기(Minimum size)
    - 희망 인스턴스 용량(Desired capacity)  
        - 희망 Amazon EC2 인스턴스 수를 지정 ✗ → 최소 크기로 설정
    - 최대 인스턴스 크기(Maximum size)

#### Elastic Load Balancing(ELB)
 - 로드 밸런서 유형
    - Application Load Balancer `Layer 7`
    - Network Load Balancer 
        - **낮은 지연시간으로 초당 수백만 개의 요청 처리 가능** 
        - `Layer 4`에서 작동하며 초고성능으로 TCP, UDP 및 TLS 트래픽의 로드 밸런싱에 적합 

    - Gateway Load Balancer `Layer 3`
    - ~~Classic Load Balancer~~ `Layer4 & 7`

#### AWS 데이터베이스 서비스 
- Amazon RDS
    - 배포 옵션
        - Read Replicas  `비동기식 복제`
        - Multi-AZ `동기식 복제`
        - Multi-Region(Read Replicas)

- Amazon Aurora `클라우드 기반 RDS`
- Amazon DynamoDB `NoSQL`, `서버리스`, `저장 중 암호화(Data at Rest)`
    - Global Tables
        - 여러 AWS 리전에서 저지연 접근이 가능한 데이터 복제본(Active-Active Replication) 제공 
    - DynamoDB Accelerator(DAX)
        - Amazon DynamoDB용 고가용성 인 메모리 캐시 서비스

- Amazon DocumentDB `MongoDB 워크로드 지원`
- Amazon MemoryDB `Redis 호환 인메모리 DB`
- Amazon ElastiCache `비영속적 캐시`, `Redis 및 Memcached 지원`
- Amazon Neptune `그래프 DB`, `NoSQL`
- Amazon QLDB(Quantum Ledger Database) `완전 관리형 원장 DB`, `변경 불가능`
- Amazon Managed Blockchain `탈중앙화(decentralized)`, `분산형 원장 시스템`

#### AWS 네트워크 서비스
- Amazon Virtual Private Cloud(Amazon VPC) `논리적으로 격리`
    - 구성 
        - 서브넷 `가용 영역 수준 리소스`
        - 라우팅 테이블 
        - 인터넷 게이트웨이 
        - NAT 게이트웨이 `AWS에서 관리`
        - NAT 인스턴스 `고객에서 관리`
        - 보안그룹 `인스턴스 · ENI 수준`, `ALLOW`, `상태 저장 방식(Stateful)`
        - NACL `서브넷 수준`, `ALLOW · DENY`, `상태 비저장 방식(Stateless)`  
        - Elastic IP(EIP) `고정된 공용 IPv4`
        - VPC Peering: `타 VPC와 비공개 연결`
        - VPC Endpoint `AWS 네트워크`, `타 AWS와 연결`

- AWS Transit Gateway `Hub & Spoke`, `여러 VPC 간의 연결`  

#### AWS 엣지 네트워킹 서비스
- Amazon CloudFront `CDN`
- Amazon Route 53 `DNS`
    - Route Policy
        - 단순 라우팅(Simple routing) `단일 리소스 IP`
        - 장애 조치 라우팅(Failover routing) `액티브-패시브 DR`
        - 지역 근접 라우팅(Geoproximity routing) `리소스 위치 기반`
        - 지역 기반 라우팅(Geolocation routing) `사용자 위치 기반`
        - 지연 시간 기반 라우팅(Latency routing)
        - IP 기반 라우팅(IP-based routing)
        - 가중치(Weighted) 기반 라운드 로빈 `트래픽 분산`

    - [참고] 재해 복구(DR) 시나리오 
        - **active/passive(standby)**
            - 백업과 복구(Backup & Restore) `PRO/RTO: Hour`
            - 파일럿 라이트(Pilot Light) `PRO/RTO: 10s of Minutes`
            - 웜 스탠바이(Warm Standby) `PRO/RTO: Minutes`
        - **active/active**
            - 멀티 사이트 액티브-액티브(Multi-site active-active) `PRO/RTO: Real-time`

- AWS Global Accelerator `사용자 트래픽 최적화`
    - AWS 엣지 로케이션을 통해 연결하려는 리전까지 빠른 접근 가능 
        - TCP, UDP 트래픽 라우팅에 최적화
        - 멀티 리전 애플리케이션의 트래픽을 라우팅하는데 사용 

#### AWS 하이브리드 연결
- AWS Direct Connect(DX) `비공개 전용 연결`, `인터넷 우회`
- AWS Site-to-Site VPN  `암호화된 네트워크 경로`, `빠른 설정`, `대역폭 제한`
- AWS Client VPN

#### AWS 스토리지 서비스
- Instance Store `임시 블록 수준 스토리지`, `장애 · 종료 시 데이터 손실`
- Amazon Elastic Block Store(Amazon EBS) `고성능 블록 수준 스토리지`, `가용 영역 수준 리소스`
- Amazon Elastic File System(Amazon EFS) `파일 스토리지`, `수백 개의 EC2 인스턴스에서 동시에 액세스`
    - EFS 스토리지 클래스
        - Standard 
        - Infrequent Access (IA)

- Amazon FSx
    - FSx for Lustre `고성능 컴퓨팅(HPC)용 스토리지`
    - FSx for Windows File Server 
    - FSx for NetApp ONTAP

- Amazon Simple Storage Service(Amazon S3) `객체 스토리지 서비스`, `리전 단위`  
    - S3 스토리지 클래스
        - S3 Standard
        - S3 Intelligent-Tiering `액세스 패턴 모니터링`
        - S3 Standard-Infrequent Access(S3 Standard-IA)
        - S3 One Zone-Infrequent Access(S3 One Zone-IA) `단일 AZ(낮은 가용성)`  
        - S3 Glacier `콜드 데이터(Cold Data)`, `암호화(AES-256)`
        - S3 Glacier Deep Archive `장기 보관 및 디지털 보존`

- AWS Storage Gateway `하이브리드 클라우드 스토리지`
    - Storage Gateway 유형 
        - File Gateway
        - Volumn Gateway
        - Tape Gateway

#### AWS AI/ML 서비스
- Amazon Rekognition `사람, 텍스트, 객체 인식 · 분석`
- Amazon Transcribe `음성을 텍스트로 변환`
- Amazon Polly `텍스트를 음성으로 변환(TTS)`
- Amazon Translate `언어 번역`
- Amazon SageMaker `ML 모델을 신속하게 빌드, 훈련, 배포`
- Amazon Lex `대화형 인터페이스(챗봇, 음성 비서 등) 구축`
- Amazon Textract `텍스트 및 데이터 자동 추출`
- Amazon Forcast `예측`
- Amazon Kendra `엔터프라이즈 검색 서비스`
- Amazon Personalize `개인화 추천 시스템 구축`
- Amazon Comprehend `자연어 처리(NLP)`, `텍스트에서 인사이트를 추출, 관계성 분석`

#### AWS 분석 서비스 
- Amazon Athena `표준 SQL 이용 S3 데이터 분석`
- Amazon Elastic MapReduce(Amazon EMR) `빅테이터 분석`, `Hadoop 클러스터`
- Amazon Redshift `OLAP`, `데이터 웨어하우징`, `빅테이터 분석`
- Amazon Kinesis `실시간 데이터 분석 처리 시스템`, `데이터 스트림`
- AWS Glue `ETL(Extract, Transform, Load)`
- Amazon Quicksight `데이터 시각화`, `대시보드`

### Domain 4: Billing, Pricing, and Support 🌕🌘🌑🌑🌑

#### Amazon EC2 결제 및 구매 옵션
- On-Demand Instances `최소 1분 요금`
- Savings Plans `기간 & 사용량 약정`, `최대 72% 할인`
- Reserved Instances `기간 약정`  
- Spot Instances `중단을 견딜 수 있는 워크로드`, `최대 90% 할인`
- Dedicated Instances
- Dedicated Host `소켓 · 코어 · 소프트웨어 라이선스 당 청구`
- Capacity Reservations

#### AWS 비용 동인(drivers of cost with AWS)
- 컴퓨팅 (Compute)
- 스토리지 (Storage) 
- 아웃바운드 데이터 전송(Outbound data transfer)
    - 인바운드 데이터 전송, 동일 리전 내 AWS 서비스 간 데이터 전송에는 요금 부과 ✗

#### AWS 비용 관리 서비스 
- AWS Organizations `계정 중앙 집중식 관리`
    - 예약된 EC2 인스턴스 공유 
    - 사용량 통합 결제 (대량 구매 요금 할인, 예약 인스턴스 할인 및 Savings Plans)    
    - AWS Single Sign-On(SSO) 중앙 사용자 포털 

- AWS Billing Conductor `AWS Marketplace 채널 파트너 및 조직 맞춤형 청구 서비스`
- AWS Cost allocation tags `비용 할당 태그`
    - AWS 생성 태그, 사용자 정의 태그 
    - 각 리소스에 대해 각 태그 키는 고유해야 하며, 각 태그 키는 하나의 값만 가질 수 있음
    - AWS 생성 태그, 사용자 정의 태그 모두 개별적 활성화해야 Cost Explorer 또는 비용 할당 보고서에 표시할 수 있음 

- AWS Budgets `임계값 알림`, `사용자 지정 예산`
    - 사용자 지정 예산(advanced)
        - Cost Budget
        - Usage Budget
        - Saving Plans Budget
        - Reservation Budget

- AWS Cost and Usage Report(AWS CUR) `종합적(comprehensive)`, `상세한 비용 및 사용량 보고서`
- AWS Cost Explorer `비용 및 사용량 시각화`
- AWS Pricing Calculator `비용 추정 도구`
- AWS Compute Optimizer `리소스 사용 최적화`

#### AWS Support Plans
- Basic `일부 AWS Trusted Advisor 검사`, `AWS Personal Health Dashboard`
- Developer `업무 시간 동안 기술 지원 액세스`
- Business `모든 AWS Trusted Advisor 검사`, `24/7 기술 지원 액세스`
- Enterprise On-Ramp
- Enterprise `TAM`, `자습형 실습 및 온라인 교육`

#### AWS Partners
- AWS Marketplace `디지털 카탈로그`
    - 소프트웨어 제공 옵션 
        - Amazon Machine Image(AMI) 
        - SaaS 솔루션

- AWS Partner Network(APN) `글로벌 파트너 프로그램`
    - APN Consulting Partners `컨설팅 및 관리 서비스(클라우드 전략, 마이그레이션)`
    - APN Technology Partners `AWS와 통합된 기술(하드웨어, 소프트웨어) 솔루션`