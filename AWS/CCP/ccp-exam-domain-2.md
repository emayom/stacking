# AWS Certified Cloud Practitioner(CLF-C02) 
### Domain 2: Security and Compliance
#### 2.1 AWS 공동 책임 모델(Shared Responsibility Model) 정의
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
- **AWS Shield**   
    DDoS 공격으로 부터 웹 애플리케이션 보호하는 관리 서비스 
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
    → 웹의 비정상 트래픽을 탐지하고 차단하기 위한 방화벽(단순 방화벽: TCP/IP 레벨에 포함된 정보 기반)

    - Layer7(L7)의 웹 취약점 공격으로부터 보호 
    - Application Load Balancer(ALB), Amazon API Gateway REST API, Amazon CloudFront 등의 리소스 유형 보호 
    - Web ACL(Access Control List)를 사용하여 보호 
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
    AWS Organizations의 여러 계정과 애플리케이션 <u>전반의 방화벽 규칙을 중앙에서 구성하고 관리</u>할 수 있는 보안 관리 서비스  

#### 2.3 AWS 액세스 관리 기능 식별

#### 2.4 보안을 위한 구성 요소 및 리소스 파악
