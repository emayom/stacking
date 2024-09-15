# AWS Certified Cloud Practitioner(CLF-C02) 
### Domain 2: Security and Compliance 🌕🌕🌕🌑🌑
#### 2.1 AWS 공동 책임 모델(Shared Responsibility Model) 정의 ❗️
![image](https://github.com/user-attachments/assets/f2c624ab-8452-4061-a3f4-3240ee1a2c81)

- **AWS 책임**   
    클라우드 "**자체**"의 보안(Security "of" the Cloud)
    
    - AWS 클라우드에서 제공하는 모든 서비스가 실행되는 인프라를 보호할 책임  
        - 소프트웨어 → 컴퓨팅, 스토리지, 데이터베이스, 네트워킹
        - 하드웨어 / AWS 글로벌 인프라 → <u>리전, 가용 영역, 엣지 로케이션</u>
- **고객 책임**   
    클라우드 "**내부**"의 보안(Security "in" the Cloud)

    - 클라우드 내에서 생성하고 배치하는 모든 것의 보안을 책임짐 
        - 고객 데이터
        - 플랫폼, 애플리케이션 관리, 자격 증명 및 액세스 관리(IAM)
        - 운영 체제(보안 패치 및 업데이트), 네트워크 및 방화벽 구성 
        - 클라이언트 측 데이터 암호화 및 데이터 무결성 인증, 서버 측 암호화(파일 시스템 및 또는 데이터), 네트워크 트래픽 보호(암호화, 무결성, 자격 증명)

- **공동 제어(Shared Control)**
    - **패치 관리(Patch Management)**
        - AWS → 인프라 내의 패치 작업과 결함 수정 / RDS
        - 고객 → 게스트 운영 체제와 애플리케이션 패치 작업 / EC2
    - **구성 관리(Configuration Management)**
        - AWS → 자체 인프라 디바이스의 구성 유지 관리
        - 고객 → 자체 게스트 운영 체제, 데이터베이스, 애플리케이션 구성 유지 관리 
    - **인식 및 교육(Awareness & Trainning)**
        - AWS → 직원이 서비스를 올바르게 사용하고, 보안 가이드라인을 준수하도록 교육
        - 고객 → 직원이 클라우드를 올바르게 사용하도록 교육


- **클라우드 서비스 별 책임**
    ![image](https://github.com/user-attachments/assets/19b5c8ff-6c91-4e65-bf58-0398cbe0070d)
    
    - Amazon Elastic Compute Cloud (Amazon EC2) → `IaaS`  
        - AWS의 책임
            - 위와 동일
        - 고객의 책임
            - 위와 동일 

    - Amazon RDS → `Managed Service`  
        - AWS의 책임  
            기본 EC2 인스턴스 관리, SSH 액세스 비활성화, DB, OS 패치 자동화 
            - 플랫폼, 애플리케이션 관리
            - 운영 체제, 네트워크 및 방화벽 구성 
            - 소프트웨어
            - 하드웨어 / AWS 글로벌 인프라

        - 고객의 책임  
            <u>고객이 필요한 모든 보안 구성 및 관리 작업</u>
            - 고객 데이터
            - 네트워크 트래픽 보호
            - 클라이언트 측 데이터 암호화
            - 방화벽 구성 
            
    - AWS Lambda
        - AWS의 책임
            - 기본 인프라 및 서비스
            - 운영 체제 및 애플리케이션 플랫폼 관리 

        - 고객의 책임
            - 함수 내의 코드 보안
            - 자격 증명 및 액세스 관리(IAM)

    - Amazon S3, AWS KMS, Amazon DynamoDB → `Manged Service`  
        - AWS의 책임
            - 서버 측 암호화
            - 네트워크 트래픽 보호
            - 플랫폼, 애플리케이션 관리 
            - 운영 체제, 네트워크 및 방화벽 구성 
            - 소프트웨어
            - 하드웨어 / AWS 글로벌 인프라 

        - 고객의 책임
            - 고객 데이터
            - 클라이언트 측 데이터 암호화 

#### 2.2 AWS 클라우드 보안, 거버넌스 및 규정 준수(Compliance) 개념 이해
- **AWS Shield** ❗️   
    > `DDos 공격으로부터 보호`  

    - AWS Shield Standard
        - 모든 AWS 고객에게 제공, 추가 비용 없음
        - SYN/UDP/ACK Floods, Reflection attacks, Layer3/4 공격 방지 
        - ELB<sup>Elastic Load Balancing</sup>, Amazon CloudFront, Route 53 리소스 유형에 자동으로 적용 

    - AWS Shield Advanced → 고급 모니터링 및 보호
        - 조직당 월 $3,000 추가 비용 발생
        - 24시간 연중 항상 AWS DDoS 대응 팀(DRT)의 지원을 받을 수 있음 
        - DDoS 공격으로 인해 발생할 수 있는 비용 급증에 대해 어느 정도 보호
        - AWS EC2, ELB<sup>Elastic Load Balancing</sup>, Amazon CloudFront, AWS Global Accelerator, Route 53 리소스 유형에 정교한 공격 방지

- **AWS WAF(Web Application Firewall)**  
    보호된 웹 애플리케이션 리소스에 전달되는 <u>HTTP(S) 요청을 모니터링할 수 있는</u> 웹 애플리케이션 방화벽  
    → 웹의 비정상 트래픽을 탐지하고 차단하기 위한 방화벽(**단순 방화벽**: TCP/IP 레벨에 포함된 정보 기반)

    - Layer7(L7)의 웹 취약점 공격으로부터 보호 
    - Application Load Balancer(ALB), Amazon API Gateway REST API, Amazon CloudFront 등의 리소스 유형 보호 
    - **Web ACL(Access Control List)** 를 사용하여 보호 
        - SQL injection, Cross-Site Scripting(XSS)와 같은 일반적인 공격으로부터 보호 
        - Size constraint, geographic match(특정 국가 허용/차단) 설정
        - Rate-based rules → 요청이 너무 빠른 속도로 수신될 때 수신 요청 수를 계산하고 요청 속도를 제한

- **AWS Network Firewall**  
    VPC(Virtual Private Cloud)를 위한 관리형 방화벽 서비스  
    외부로 통하는 액세스 포인트와 사용자의 퍼블릭 서브넷 사이에 위치하여 상태 저장 및 상태 비저장 규칙 그룹을 통해 트래픽을 필터링/감시하는 서비스  
    → <u>VPC(Virtual Private Cloud)를 전반적으로 보호하는 방법</u>

    - Layer3-7 까지 보호 가능
    - 모든 방향에서의 트래픽 검사 가능 
        - VPC to VPC 트래픽
        - 인터넷으로 아웃바운드 트래픽
        - 인터넷에서 인바운드 트래픽
        - Direct Connect & Site-to-Site VPN 양방향
    - AWS Firewall Manager와 함께 작동
    - DDoS와 같은 볼륨 공격을 완화하도록 설계된 것은 아님 

- **AWS Firewall Manager**  
    > `방화벽 규칙 중앙 구성 · 관리`

    - AWS Organizations의 여러 계정과 애플리케이션 전반의 <u>방화벽 규칙을 중앙에서 구성하고 관리</u>
    - 언제든지 모든 계정에 걸쳐 규정이 일관되게 관리됨을 보장 

- **Penetration Testing** 
    - 허용 서비스(AWS 승인 불필요) `종류 출제 범위 ✗`
    <small>
        - Amazon EC2 인스턴스, WAF, NAT Gateways, Elastic Load Balaners
        - Amazon RDS
        - Amazon CloudFront
        - Amazon Aurora
        - Amazon API Gateways
        - AWS Lambda, Lambda Edge functions
        - Amazon Lightsail 리소스
        - Amazon Elastic Beanstalk 환경 등 
    </small>

    - 금지 활동 → AWS의 인프라를 공격하는 것으로 간주 
        - Amazon Route 53 Hosted Zones를 통한 DNS zone walking
        - Route 53를 통하여 DNS 하이재킹
        - Route 53를 통하여 DNS 파밍
        - DoS, DDoS, 모의 DoS, 모의 DDoS
        - 포트 플러딩, 프로토콜 플러딩, 요청 플러딩

- **AWS KMS, CloudHSM 기반 데이터 암호화**  
    - 암호화 방식
        - Data **at Rest**(저장 시 암호화)  
            → 데이터가 물리적으로 데이터 저장소나 디바이스에 저장됨 

            - 서버 측 암호화
            - 클라이언트 측 암호화 
        - Data **in Transit**(전송 중 암호화) → 네트워크 상에 전송되며 

    - 암호화 서비스  
        - **AWS KMS(Key Management Service)**  
            <u>데이터 암호화 시 사용되는 암호화 키를 쉽게 생성 및 제어할 수 있게 해주는 관리형 서비스</u>   
            → 암호화 키: 데이터 잠금(암호화) 및 잠금 해제(암호 해독)에 사용되는 임의의 숫자 문자열

            - KMS Key의 종류 
                - 고객 관리 키(Customer Managed Key) → 사용자가 직접 생성하고 관리하며, 접근 권한 설정 가능 
                - AWS 관리 키(AWS Managed Key) → AWS가 자동으로 생성하고 관리하며, 고객은 직접 제어 불가능 
                - AWS 소유 키(AWS Owned Key) → AWS가 소유하고 관리하며, 고객은 접근 불가능 
            
        - **AWS CloudHSM**
            > `암호화`, `하드웨어 보안 모듈(HSM) 제공`

            하드웨어 보안 모듈(HSM)을 제공하여 암호화 키를 생성하고 관리할 수 있게 해주는 서비스  

            - 높은 보안 수준과 규제 준수를 요구하는 환경에 적합
            - **AWS에서 암호화에 이용되는 하드웨어만 제공, 고객이 HSM의 모든 운영 및 보안을 직접 관리**
            - FIFS 140-2 레벨 3 검증 HSM(Hardware Security Module)을 사용하여 암호화 키 관리 → Tamper-resistant

- **AWS Certificate Manager(ACM)**  
    **SSL/TLS 인증서**를 쉽게 프로비전, 관리, 배포할 수 있는 관리형 서비스 

    - TLS 인증서 자동 갱신(관리형 갱신)
    - HTTPS를 통해 전송 중 암호화 지원
    - AWS의 여러 서비스와 통합되어 인증서를 쉽게 배포하고 관리 가능

- **AWS Artifact** → 실제 서비스 ✗ ❗️    
    > `보안 및 규정 준수 보고서` 

    AWS **보안 및 규정 준수 보고서** 및 일부 온라인 계약에 대한 **온디맨드 액세스**를 제공하는 서비스

    - Artifact Reports   
        - 외부 감사 기관이 작성한 **규정 준수 보고서** 제공 
        - 다운로드 가능, 보안이나 규제 표준 준수 정보에 액세스할 수 있도록 지원

    - Artifact Agreements  
        <u>개별 계정 및 AWS Organizations 내 모든 계정에 대한 AWS와의 계약 검토, 수락 및 관리</u> 

        - BAA(Business Associate Addendum): 
        - GDPR(General Data Protection Regulation): 일반 데이터 보호 규정
        - **HIPAA**(Health Insurance Portability and Accountability): 미국 건강 보험 양도 및 책임에 관한 법

    - 모든 규정 준수 정보를 한 곳에서 확인하고 싶다면 → **AWS 규정 준수 센터** 

- **Amazon GuardDuty** ❗️  
    > `지능형 위협 탐지 기능`

    AWS 인프라 및 리소스에 대한 **지능형 위협 탐지 기능** 제공 서비스

    - 위협 분석 대상 
        - VPC Flow Logs → 네트워크 트래픽 패턴을 분석
        - CloudTrail Logs → API 호출 및 사용자 활동 모니터링
        - DNS Logs(AWS DNS) → DNS 쿼리와 관련된 활동 추적
        - Optional  
            - S3 Logs S3 
            - EBS Volumnes
            - Lambda Network Activity  
            - RDS & Aurora Login Activity 
            - EKS Audit Logs & Runtime Monitoring

- **Amazon Inspector** ❗️  
    > `보안 평가 자동화`, `의도하지 않은 네트워크 액세스`, `소프트웨어 취약성 탐지`
    
    - AWS 워크로드의 **소프트웨어 취약성**과 **의도하지 않은 네트워크 노출 여부**을 탐지하는 자동화된 취약성 관리 서비스 
    - 실행 중인 Amazon EC2 인스턴스, Amazon ECR 컨테이너 이미지, AWS Lambda 함수 자동 검색 및 스캔 → 결과 보고서 
    - Amazon Inspector 위험 점수 기반 문제 해결의 우선순위 → 평균 문제 해결 시간(MTTR) 단축

- **Amazon CloudWatch** ❗️  
    > `리소스 성능 모니터링`, `이벤트 및 경고`  

    AWS 리소스에 대한 지표를 수집하고 추적하는 모니터링 서비스

    - 리소스 사용률 및 성능 모니터링
    - 단일 대시보드에서 지표에 액세스
    - AWS Lambda와 Amazon CloudWatch 결합 → 트리거 기반 서버리스 로그 솔루션 구축 

- **Amazon CloudWatch Logs**
    > `로그 중앙 집중화`

    - Amazon EC2 인스턴스, AWS CloudTrail, Route 53 및 온프레미스 서버와 같은 기타 소스에서 로그 파일을 모니터링, 저장 및 액세스 가능 
    - 애플리케이션 및 AWS 서비스의 로그 중앙 집중화 

- **AWS CloudTrail** ❗️  
    > `계정별 활동 및 감사`

    - 애플리케이션 및 리소스에 대한 모든 사용자 활동(이벤트) 및 API 호출 내역 추적 
    - 운영 분석 및 문제 해결을 지원하기 위한 이벤트 및 로그 필터링 지원 
    - 일반적으로 API 호출 후 15분 이내에 CloudTrail에서 업데이트
    - API 호출 기록 정보 
        <small>
        - API 호출을 요청한 사용자 ID
        - API 호출이 발생한 날짜 및 시간
        - API 호출에 포함된 리소스 유형 등
        </small>
    - CloudTrail Insights 옵션
        - AWS 계정에서 비정상적인 API 활동 자동 감지

- **AWS X-Ray**
    > `추석 및 분석`, `디버깅`, `서비스 맵`

    - 애플리케이션 추적 및 시각적 분석
    - 마이크로서비스 아키텍처(MSA)로 구축된 애플리케이션과 같은 서버리스 및 분산 애플리케이션 분석 및 디버그 가능 
    - 그래프로 시각화가 가능한 API(X-Ray API) 제공 → Service Map 


#### 2.3 AWS 액세스 관리 기능 식별
- **AWS IAM(Identity and Access Management)**  
    AWS 서비스와 리소스에 대한 액세스를 안전하게 제어/관리할 수 있는 서비스   
    → 보안 요구 사항에 따라 액세스 권한 구성 가능 

    - IAM 기능 
        - IAM 유저
            - 기본적으로 새 IAM 유저 생성 시 연결된 권한 ✗ → 명시적인 권한 부여 필요 
        - IAM 그룹 
        - IAM 역할 
            - **임시로** 권한에 액세스하기 위해 수임할 수 있는 자격 증명 
        - IAM 정책
            - 최소 권한 보안 원칙 준수 
        - **MFA(Multi-Factor Authentication)** ❗️  
            - Virtual MFA device → 모바일 디바이스나 컴퓨터에 설치된 앱 사용 
            - U2F(Universal 2nd Factor) security key → 컴퓨터의 USB 포트에 연결할 수 있는물리적 장치 
            - Other hardware MFA device → 물리적 장치이지만 연결 ✗, 여섯 자리 숫자 코드를 제공하는 MFA 장치
            - ~~SMS text message-based MFA~~ `지원 종료`

- **AWS 계정 루트 사용자**
    - 루트 유저 권한 
        - 계정의 모든 AWS 서비스 및 리소스에 대한 전체 액세스 권한 보유 
        - <u>일상적인 작업, 관리 작업 용도로 사용으로 사용하지 말 것</u> 
        - Multi-Factor Authentication 활성화, 액세스 키 잠금 권장
    
    - **루트 사용자만 수행할 수 있는 테스크** ❗️  
        - **계정 설정(계정 이름, 이메일 주소, 루트 유저 비밀번호, 루트 유저 액세스 키 등의 변경)**
        - 세금 계산서 열람
        - **AWS 계정 삭제** 
        - IAM 유저 권한 복구 
        - **AWS Support plan 변경 및 취소** 
        - **Reserved Instance Marketplace 판매자 등록** 
        - Amazon S3 버킷 구성을 통한 MFA(Multi-Factor Authentication) 활성화  
        - invalid VPC ID 나 VPC endpoint ID를 포함한 Amazon S3 버킷 정책(policy) 편집 및 삭제
        - GovCloud 가입 

- **최소 권한 원칙(Principle of Least Privilege)**  
    - 그 어떠한 사용자도 필요한 것 이상으로 권한을 가지고 있어서는 안 됨 
    - 주기적으로 권한을 검사하여 미사용 권한을 삭제해주는 작업 필요 

- **AWS IAM Identity Center(AWS Single Sign-On)**  
    > `AWS Single Sign-On 후속 서비스`  

    중앙 집중식으로 사용자, 그룹 및 역할을 제어하고 관리하는 데 도움을 주는 서비스  
    (한 번의 로그인으로 조직의 여러 AWS 계정과 애플리케이션에 접근 가능)   
 
- **AWS Secrets Manager**  
    > `보안 · 기밀 보호`

    애플리케이션에서 사용하는 비밀 · 보안 정보를 안전하게 저장하고 관리하는 데 도움을 주는 서비스  

    - <u>Amazon RDS와의 통합 지원</u> → 인스턴스 암호 관리 간소화(비밀번호 정기적, 자동 교체)
    - AWS Key Management Service(KMS)를 통해 자동으로 암호화 
    - AWS Identity and Access Management(IAM)를 통해 접근 권한 제어 가능 
    - 모니터링, 버전 관리 가능 
    - 비밀 · 보안 정보 예시  
        - 데이터베이스 자격 증명
        - API 키
        - OAuth 토큰
        - SSH 키
        - TLS/SSL 인증서 및 개인 키
        - 일반 텍스트 또는 JSON 형식의 기타 민감한 정보 

- **AWS Systems Manager(SSM)**  
    클라우드와 온프레미스 환경에서 시스템과 애플리케이션의 운영을 간소화하고 자동화하는 데 도움을 주는 서비스   
    → Hybrid AWS 서비스 

    - 주요 기능
        - Patch Manager → 패치 자동화 
        - Run Command → 여러 개의 인스턴스 대상으로 동시에 명령어 실행 
        - **SSM Parameter Store**
            - 구성 데이터나 암호를 안전하게 AWS에 저장해주는 방식
            - Serverless, scalable, durable, easy SDK
            - IAM을 활용한 파라미터 엑세스 컨트롤 
        - **SSM Session Manager**  
            - EC2 인스턴스나 온프레미스 서버에 시큐어 셸 시작 가능  
            - SSH 액세스, Bastion Host, SSH 키 관리 불필요, SSH 포트(22) 불필요   

#### 2.4 보안을 위한 구성 요소 및 리소스 파악

- **AWS Trusted Advisor**  ❗️  
    > `모니터링 및 분석`

    AWS 모범 사례에 따라 **실시간 권장 사항**을 제안해주는 서비스
    
    - AWS Trusted Advisor 대시 보드에 카테고리별 요약된 권장 항목 표시  
        → `조치 권장`, `조사 권장`, `감지된 문제 없음`, `검사 제외` 항목으로 분류 제공 

    - 검사 범주 ❗️ 
        - **비용 최적화(Cost Optimization)**  
        - **성능(Performance)**  
        - **보안(Security)**  
        - **내결함성(Fault Tolerance)**  
        - **서비스 한도(Server Limits)**  
        - **운영 우수성(Operational Excellence)**

    - 각 플랜에 따라 제공되는 검사 항목 구분 
