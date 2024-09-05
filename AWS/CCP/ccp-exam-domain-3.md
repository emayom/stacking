# AWS Certified Cloud Practitioner(CLF-C02) 
### Domain 3: Cloud Technology and Services 🌕🌕🌕🌘🌑
#### 3.1 AWS 클라우드에서 배포 및 운영 방법 정의
- **AWS Management Console**  
    Amazon 서비스 액세스 및 관리를 위한 브라우저 기반 인터페이스

    - GUI 기반의 <u>수동 프로비저닝</u> → 학습 및 시각적 정보 확인 유용
    - 여러 ID가 동시에 AWS 콘솔 모바일 앱에 로그인 가능

- **AWS CLI**  
    - 머신의 <u>터미널</u>을 사용하여 API 호출 
    - 스크립트를 통해 AWS 서비스 및 애플리케이션의 작업을 **자동화**
        - 수동 프로비저닝으로 인한 인적 오류 방지 가능
        - 스크립트 기반 예약, 다른 프로세스에서 트리거하는 방식으로 자동 실행 가능

- **AWS SDK**
    - 프로그래밍 언어 또는 플랫폼용으로 설계된 API를 통해 AWS 서비스를 보다 간편하게 사용
    - SDK를 통해 AWS 서비스를 기존 애플리케이션과 함께 사용하거나 AWS에서 실행할 완전히 새로운 애플리케이션을 생성 가능
    - 지원 가능한 프로그래밍 언어 → C++, 자바, .NET 등

- **AWS Elastic Beanstalk** `관리 도구`  
    Amazon EC2 기반 환경 프로비저닝을 지원하는 서비스 

    - 인프라가 아닌 비즈니스 애플리케이션에 집중
    - 사용자가 코드 및 구성 설정을 제공하면 다음 작업을 수행하는 데 필요한 리소스를 배포
        - 용량 조정
        - 로드 밸런싱
        - 자동 조정(Auto Scaling)
        - 애플리케이션 상태 모니터링

- **AWS CloudFormation** `관리 도구`   
    코드형 인프라 도구

    - 인프라를 코드로 취급 가능(Infrastructure as code)
    - JSON, YAML 텍스트 문서 기반의 CloudFormation 템플릿을 활용   
        → **선언적인 방식**으로 사용하여 다양한 AWS 기반 리소스 정의 
    - 아키텍처를 다른 환경, 리전, AWS 계정에서 반복해야 할 때  
        → **자동화되고 반복 가능한 배포**를 만드는 데 도움
    - 대다수의 AWS 리소스를 지원

#### 3.2 AWS 글로벌 인프라 정의
- **AWS 리전(Region)** ❗️   
    AWS 리소스가 있는 지리적으로 구분된 영역

    - **최소 2개 이상의 물리적으로 분리된 가용 영역으로 구성**   
        (가용 영역은 최소 1개 이상의 데이터 센터로 구성 → 불가항력으로부터 대비)  
    - 각 리전은 지역 법률과 국가 법령이 적용되며 독립적  
    - 고속 광섬유 네트워크를 통해 다른 리전과 연결 
    - 리전 선택 시 고려사항  
        - 데이터 거버넌스 및 법적 요구 사항 준수
        - 고객과의 근접성(지연 시간 고려)
        - 기능 가용성
        - 요금

- **AWS Wavelength 영역 및 AWS Local Zones**
    - AWS Wavelength 영역 → 5G 엣지 컴퓨팅
    - AWS Local Zones 
        - 사용자와 지리적으로 근접한 AWS 리전의 확장(저지연 서비스 제공 목적)
        - EC2, RDS, ECS, EBS, ElasticCache, Direct Connect 등과 호환 

- **가용 영역(AZ; Availability Zone)** ❗️   
    리전 내의 단일 데이터 센터 또는 데이터 센터 그룹

    - 각 가용 영역은 물리적으로 분리 → 고가용성, 내구성 보장 
    - **다중 가용 영역 배포 → 고가용성 확보**

- **엣지 로케이션(Edge Location)** ❗️   
    <u>Amazon CloudFront(CDN)가 더 빠른 콘텐츠 전송을 위해 고객과 가까운 위치에 콘텐츠 사본을 캐싱하는 데 사용</u>

- **AWS Outposts**  
    - **하이브리드 클라우드 방식**으로 인프라를 실행할 수 있도록 지원하는 서비스  
        → 온프레미스 애플리케이션을 클라우드로 옮기지 않고도 AWS의 클라우드 서비스를 사용할 수 있게

#### 3.3 AWS 컴퓨팅 서비스 식별
- **Amazon EC2 인스턴스 유형**
    - **범용 인스턴스**   
        컴퓨팅, 메모리, 네트워킹 리소스를 균형 있게 제공

        - 적합한 워크로드 
            - 애플리케이션 서버
            - 게임 서버
            - 엔터프라이즈 애플리케이션용 백엔드 서버
            - 중소 규모 데이터베이스

    - **컴퓨팅 최적화 인스턴스**  
        고성능 프로세서 제공 

        - 적합한 워크로드 
            - 고성능 웹 서버
            - 컴퓨팅 집약적 애플리케이션 서버
            - 게임 전용 서버

    - **메모리 최적화 인스턴스**   
        고성능 데이터베이스 
        메모리에서 대규모 데이터 세트를 처리하는 워크로드

    - **엑셀러레이티드 컴퓨팅 인스턴스**  
        부동 소수점 수 계산, 그래픽 처리, 데이터 패턴 일치 등

    - **스토리지 최적화 인스턴스**   
        데이터 웨어하우징 애플리케이션

#### 3.4 AWS 데이터베이스 서비스 파악
- 관계형 데이터베이스 
    - **Amazon RDS** ❗️  
        - 데이터베이스 관리 작업 자동화 
            - 프로비저닝, 구성, 패치 적용, 백업, 이중화, 장애 조치, 재해 복구과 같은 데이터베이스 관리 작업을 자동화
            - 기존 온프레미스 환경에서 Amazon RDS로 Lift and Shift 마이그레이션을 통해 관계형 데이터베이스 실행 가능
            
        - **주요 데이터베이스 엔진 지원** ❗️  
            → 메모리, 성능 또는 I/O에 최적화된 6개의 데이터베이스 엔진에서 사용 가능
            - Amazon Aurora
            - PostgreSQL
            - MySQL
            - MariaDB
            - Oracle Database
            - Microsoft SQL Server

        - 다양한 보안 옵션 제공
            - 저장 시 암호화
            - 전송 중 암호화

        - 자동 백업 기능 및 특정 시점 복구(Point-in-Time Recovery) 제공
        - Multi-AZ 배포 기반 → 고가용성 제공
        - **고객이 데이터, 스키마 소유 및 네트워크 제어**

    - **Amazon Aurora**  
        클라우드 기반 엔터프라이즈급 관계형 데이터베이스

        - MySQL, PostgreSQL 호환  
            - 표준 MySQL 데이터베이스보다 최대 5배, 표준 PostgreSQL 데이터베이스보다 최대 3배 빠름
        - 데이터베이스 리소스의 안정성 및 가용성을 유지하면서도 불필요한 입/출력(I/O) 작업을 줄여 데이터베이스 비용을 절감
            - 상용 데이터베이스 비용의 1/10 수준
        - 스토리지 10GB 단위로 최대 128TB까지 자동 증가
        - 6개의 데이터 복제본을 3개의 가용 영역에 복제, Amazon S3로 지속적인 백업 제공
            - 특정 시점 복구 제공(Point-in-Time Recovery)
            - 최대 15개의 읽기 전용 복제본 배포 가능

- NoSQL 데이터베이스
    - **Amazon DynamoDB**  
        - 키-값 데이터베이스 서비스
        - **서버리스 데이터베이스** 
            - <u>서버 프로비저닝, 패치 적용 및 관리 불필요</u> 
            - 소프트웨어 설치, 유지 관리, 운영 불필요 
        - 자동 조정
            - **용량 변화에 맞춰 자동으로 크기 조정하면서도 일관된 성능 유지** 
        - 밀리초 단위 응답 시간 → 대규모 처리 가능 
        - 높은 확장성 및 유연성 
            - 페타 바이트 크기 확장 가능

    - **Amazon DocumentDB**  
        MongoDB 워크로드를 지원하는 문서 데이터베이스 서비스

- 인 메모리 데이터베이스/캐시
    - **Amazon MemoryDB**  
        - Redis 호환 인 메모리 데이터베이스 서비스

    - **Amazon ElastiCache** ❗️ `비영속적인 캐시`  
        - 인 메모리 캐시 서비스 
        - 자주 사용되는 요청의 읽기 시간을 향상시키기 위해 데이터베이스 위에 캐싱 계층을 추가하는 서비스
        - Redis 및 Memcached를 지원(NoSQL)
        
    - **DynamoDB Accelerator(DAX)**  
        - DynamoDB용 인 메모리 캐시 서비스
        - 응답 시간을 한 자릿수 밀리초에서 마이크로초까지 향상시킬 수 있음
        - 비관계형 데이터를 3배나 개선하도록 설계된 기본 캐싱 계층

- 그외 데이터베이스
    - **Amazon Neptune**  
        - 그래프 데이터베이스 서비스  

    - **Amazon QLDB(Quantum Ledger Database)**
        - 원장 데이터베이스 서비스
        - 변경 불가능한 기록 시스템 
        - 애플리케이션 데이터에 발생한 모든 변경 사항의 전체 기록 검토 가능
   
- **Amazon Managed Blockchain**
    - 분산형 원장 시스템
    - 오픈 소스 프레임워크를 사용하여 블록체인 네트워크를 생성하고 관리하는 데 사용할 수 있는 서비스

- **Amazon Redshift** ❗️  
    - 빅 데이터 분석에 사용할 수 있는 **데이터 웨어하우징 서비스**
    - 여러 원본에서 데이터를 수집하여 데이터 간의 관계 및 추세를 파악하는데 도움

- **AWS Database Migration Service(AWS DMS)**   
    관계형 데이터베이스, 비관계형 데이터베이스 및 기타 유형의 데이터 저장소를 마이그레이션할 수 있는 서비스  
    → 데이터베이스 마이그레이션 도구  

    - 원본 데이터베이스와 대상 데이터베이스는 유형이 동일할 필요가 없음 

    - 마이그레이션 유형
        - **동종 마이그레이션**  
            스키마 구조, 데이터 유형, 데이터베이스 코드가 원본과 대상 사이에서 호환 
            <small>
            - MySQL → Amazon RDS for MySQL
            - Microsoft SQL Server → Amazon RDS for SQL Server
            - Oracle → Amazon RDS for Oracle
            </small>

        - **이종 마이그레이션** 
            1. AWS Schema Conversion Tool을 사용하여 변환
            2. DMS를 사용하여 원본 데이터베이스의 데이터를 대상 데이터베이스로 마이그레이션

    - 사용 사례 
        - 개발 및 테스트 데이터베이스 마이그레이션 
        - 데이터베이스 통합 
        - 연속 복제 

#### 3.5 AWS 네트워크 서비스 파악
- **Amazon Virtual Private Cloud(Amazon VPC)**  
    AWS 리소스에 경계를 설정하는 데 사용할 수 있는 가상 네트워크 서비스  
    → 사용자가 AWS 리소스를 <u>논리적으로 격리된</u> 가상 네트워크 환경에서 운영할 수 있도록

    - 특정 리전과 연결, 특정 리전 내에서 작동하는 가상 네트워크(여러 리전 → 여러 VPC) 
    - 구성 요소
        - **서브넷(Subnet)**   
            VPC 내의 네트워크 파티션(가용 영역 수준 리소스)  
            - 공용 서브넷(Public Subnet) → 인터넷 접근 가능
            - 사설 서브넷(Private Subnet) → 인터넷 접근 제한 
        - **라우팅 테이블(Routing Table)**  
            네트워크 트래픽을 전달할 위치를 결정하는 데 사용되는 라우팅이라는 규칙 집합
        - **인터넷 게이트웨이(Internet Gateway, IGW)**  
            VPC 인스턴스가 인터넷에 바로 연결되도록 도움 
        - **NAT 게이트웨이 및 NAT 인스턴스**  
            - NAT(Network Address Translation) 게이트웨이    
                → 사설 서브넷 내의 인스턴스가 프라이빗 상태를 유지하면서 인터넷에 연결할 수 있도록  
            - NAT 인스턴스  
                → self-managed
        - **보안 그룹(Security Group)** `인스턴스 · ENI 수준`   
            - 상태 저장  
            - 기본적으로 모든 인바운드 트래픽을 거부 
        - **네트워크 ACL(Network Access Control List, NACL)** 
            - **서브넷 수준**에서 작동하는 방화벽 역할 
            - ALLOW(허용) 및 DENY(거부) 규칙이 모두 존재 
        - **Elastic IP(EIP)**  
            - 고정된 공용 IPv4
        - **VPC 피어링(VPC Peering)**  
            AWS의 네트워크를 사용해 다른 VPC와 프라이빗으로 연결함  
            → 마치 동일한 네트워크처럼 동작하도록 
        - **VPC 엔드포인트(VPC Endpoint)**
            - AWS PrivateLink

- **Amazon Route 53**  
    관리형 DNS(Domain Name System) 웹 서비스  

    - 사용자 요청을 AWS에서 실행되는 인프라에 연결
    - DNS 레코드 관리 기능  
        - 다른 도메인 등록 대행자가 관리하는 기존 도메인 이름의 DNS 레코드 전송 가능  
            → 단일 위치에서 모든 도메인 이름을 관리
    - 라우팅 정책 
        - 단순 라우팅 → 상태 확인 ✗
        - 지역 근접 라우팅
        - 지연 시간 기반 라우팅
        - IP 기반 라우팅
        - 지역 DNS → 지역 로케이션을 기반 라우팅
        - 가중치(Weighted) 기반 라운드 로빈 → 트래픽 분산

- **AWS 엣지 서비스** 
    - **Amazon CloudFront** ❗️  
        > _Domain 1. AWS 관리형 서비스의 종류와 특징 참고_ 
    
    - **AWS Global Accelerator**  
        - AWS 글로벌 네트워크를 이용하여 글로벌 애플리케이션의 가용성, 성능 개선할 때 사용
        - AWS 엣지 로케이션을 통해 연결하려는 리전까지 빠른 접근 가능 
            - TCP, UDP 트래픽 라우팅에 최적화
            - 멀티 리전 애플리케이션의 트래픽을 라우팅하는데 사용 

- **AWS 네트워크 연결 옵션** 
    - **AWS Client VPN**  
        - OpenVPN 기반 VPN 클라이언트를 사용
        - AWS VPC에 안전하게 접근하고 싶을 경우 
        - 온프레미스 → Customer Gateway(CGW), AWS → Virtual Private Gateway(VGW) 필요 

    - **Site to Site VPN**
        - **Public 인터넷**을 통해 연결 → 대역폭 제한, 보안 문제 발생 가능
        - 약 5분 정도의 빠른 설정 

    - **AWS Direct Connect(DX)** ❗️  
        - 온프레미스 데이터 센터와 AWS 클라우드 간에 빠르고 안전한 **비공개 전용 연결(private network)** 을 설정
        - 짧은 지연 시간, 최대한 높은 수준의 보안 → 느린 설정, 높은 비용 
        - 높은 수준의 규제 및 규정 준수 요구사항을 쉽게 충족, 잠재적 대역폭 문제 방지 
        - 네트워크 비용을 절감하고, 네트워크를 통과할 수 있는 대역폭을 늘리는 데 도움

    - **AWS Transit Gateway**  
        - 여러 VPC(대규모)와 온프레미스 네트워크를 하나의 중앙 허브를 통해 연결(peering)할 수 있게 해주는 서비스  
            → Hub & Spoke 형태 

#### 3.6 AWS 스토리지 서비스 파악
- **EC2 인스턴스 스토어**
    - Amazon EC2 인스턴스에 임시 블록 수준 스토리지를 제공
    - EC2 인스턴스를 중지 또는 종료 시, 데이터 삭제   
        → 장기간 보관하지 않을 임시 데이터(캐시, 임시 데이터, 로그 파일)에 적합

- **Amazon Elastic Block Store(Amazon EBS)** ❗️  
    - <u>EC2 인스턴스를 중지 또는 종료하더라도 연결된 EBS 볼륨의 모든 데이터는 보존</u> 
        - 루트 볼륨의 경우, 기본적으로 인스턴스 **종료** 시 삭제(Delete on Termination) 옵션 활성화 
    - 특정한 단일 가용 영역에 EBS 볼륨 생성
        - **동일한 가용 영역의 인스턴스에만 연결 가능(가용 영역 수준 리소스)**
        - 기본적으로 볼륨은 한 번에 하나의 인스턴스에만 연결 가능(여러 볼륨을 단일 인스턴스에 연결 가능)
        - EBS Multi Attach → 하나의 EBS 볼륨을 여러 인스턴스에 동시에 연결
    - EBS 스냅샷(증분 백업) → Amazon S3에 저장 → 복구 / 다른 가용 영역(AZ) 또는 리전 간 복제

- **Amazon Elastic File System(Amazon EFS)** ❗️  
    - 관리형 파일 시스템
    - **여러 가용 영역에서 액세스 가능(리전 리소스)**
        - 데이터를 여러 가용 영역(AZ)에 걸쳐 자동으로 복제, 중복 저장  
            → 하나의 가용영역이 파괴되더라도 다른 AZ에서 서비스 제공 가능(높은 가용성, 데이터 내구성)
    - **여러 인스턴스 동시에 액세스 가능**
        - Linux 기반 EC2 인스턴스 지원(Windows 인스턴스는 지원되지 않음)
    - 볼륨 자동 확장/축소 → 프로비저닝, 관리 필요 ✗
        - 페타바이트(PB) 단위 데이터 저장 가능
    - EFS 스토리지 클래스
        - Standard → 자주 액세스하는 데이터, 높은 성능 
        - Infrequent Access (IA) → 드물게 액세스하는 데이터, 비용 절감 효과
    
- **Amazon FSx** 
    - FSx for Lustre
        - 완전 관리형
        - 고성능, 확장 가능한 파일 스토리지(HPC용 스토리지)
    - FSx for Windows File Server
    - FSx for NetApp ONTAP
    
- **Amazon Simple Storage Service(Amazon S3)** `객체 수준 스토리지 서비스`  
    - <u>데이터를 버킷에 객체로 저장</u>
    - 모든 유형의 파일(이미지, 동영상, 텍스트 파일 등)을 업로드 가능하며, 업로드 가능한 객체의 최대 파일 크기는 5TB
    - 파일 업로드 시, 권한 설정 → 파일에 대한 표시 여부 및 액세스를 제어 가능
    - Amazon S3 버전 관리 기능 → 객체 변경 사항 추적 가능
    - **Amazon S3 스토리지 클래스** ❗️   
        1\) 데이터 검색 빈도 2\) 필요한 데이터 가용성을 고려하여 클래스 선택   
        - S3 Standard
            - 자주 액세스하는 데이터용으로 설계
            - 최소 3개의 AZ에 데이터를 저장
        - S3 Standard-Infrequent Access(S3 Standard-IA)
            - 자주 액세스하지 않지만 필요에 따라 고가용성이 요구되는 데이터  
                → 백업, 재해 복구 파일 또는 장기 보관이 필요한 모든 객체에 적합 
            - 최소 3개의 AZ에 데이터를 저장
        - S3 One Zone-Infrequent Access(S3 One Zone-IA)
            - 단일 가용 영역에 데이터 저장 
        - S3 Intelligent-Tiering
            - 액세스 패턴을 알 수 없거나 자주 변화하는 데이터
        - S3 Glacier
            - 데이터 보관용
            - 객체를 몇 분에서 몇 시간 이내에 검색
            - 잠금 정책 
                - 한 번 쓰기/여러 번 읽기(WORM)
        - S3 Glacier Deep Archive
            - 데이터 보관용
            - 객체를 12시간 이내에 검색

- **AWS Storage Gateway**

#### 3.7 AWS 인공 지능 및 기계 학습(AI/ML) 서비스와 분석 서비스 파악

- AI/ML 서비스
    - **Amazon Rekognition**  
        이미지 및 비디오 분석 서비스 → 사람, 텍스트, 객체 등을 인식하고 분석
    - **Amazon Transcribe**  
        음성을 텍스트로 자동 변환해주는 서비스
        - Redaction을 이용하여 개인 식별 정보(Personally Identifiable Information, PII) 자동 제거 기능 
        - 다국어 오디오에 대한 자동 언어 식별 기능 지원 
    - **Amazon Polly**  
        텍스트를 음성으로 변환해주는 서비스(TTS)
    - **Amazon Translate**  
        실시간 언어 번역을 제공하는 자동 번역 서비스
    - **Amazon SageMaker**  
        **ML 모델을 신속하게 빌드, 훈련, 배포할 수 있도록** 돕는 고차원의 완전 관리형 머신러닝 서비스
    - **Amazon Lex**  
        음성과 텍스트를 사용해 대화형 인터페이스(챗봇, 음성 비서 등)를 구축할 수 있는 서비스  
    - **Amazon Textract**  
        문서에서 텍스트 및 데이터 자동 추출 서비스
    - **Amazon Forcast**  
        예측 서비스
    - **Amazon Kendra**  
        엔터프라이즈 검색 서비스 → 자연어 검색으로 다양한 형식(텍스트, PDF, HTML, PPT, MS Word 등) 정보 검색 가능 
    - **Amazon Personalize**  
        개인화된 추천 시스템 구축 서비스 
    - **Amazon Comprehend**  
        완전 관리형 서버리스 자연어 처리(NLP) 서비스 → 텍스트에서 인사이트를 추출, 관계성 분석 

- 데이터 분석을 위한 서비스
    - **Amazon Athena**  
    - **Amazon Kinesis**  
    - **AWS Glue**  
    - **Amazon QuickSight**  

#### 3.8 시험 범위에 포함되는 다른 AWS 서비스 범주의 서비스 파악