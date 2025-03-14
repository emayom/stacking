---
last_modified_at: '2025-03-14T07:36:59.737Z'
date: '2025-01-13T15:02:20.474Z'
---
# AWS Certified Cloud Practitioner(CLF-C02) 
### Domain 3: Cloud Technology and Services

#### TOC
- [3.1 AWS 클라우드에서 배포 및 운영 방법 정의](#31-aws-클라우드에서-배포-및-운영-방법-정의)

- [3.2 AWS 글로벌 인프라 정의](#32-aws-글로벌-인프라-정의)  

- [3.3 AWS 컴퓨팅 서비스 식별](#33-aws-컴퓨팅-서비스-식별)

- [3.4 AWS 데이터베이스 서비스 파악](#34-aws-데이터베이스-서비스-파악)

- [3.5 AWS 네트워크 서비스 파악](#35-aws-네트워크-서비스-파악)

- [3.6 AWS 스토리지 서비스 파악](#36-aws-스토리지-서비스-파악)

- [3.7 AWS 인공 지능 및 기계 학습(AI/ML) 서비스와 분석 서비스 파악](#37-aws-인공-지능-및-기계-학습aiml-서비스와-분석-서비스-파악)

- [3.8 시험 범위에 포함되는 다른 AWS 서비스 범주의 서비스 파악](#38-시험-범위에-포함되는-다른-aws-서비스-범주의-서비스-파악)

#### 3.1 AWS 클라우드에서 배포 및 운영 방법 정의
---
#### Knowledge of:
---

- **AWS Management Console**  
    Amazon 서비스 액세스 및 관리를 위한 브라우저 기반 인터페이스

    - GUI 기반의 <u>수동 프로비저닝</u> → 학습 및 시각적 정보 확인 유용
    - 여러 ID가 동시에 AWS 콘솔 모바일 앱에 로그인 가능

- **AWS CLI**  
    - 머신의 <u>터미널</u>을 사용하여 API 호출 
    - 스크립트를 통해 AWS 서비스 및 애플리케이션의 작업을 **자동화**
        - 수동 프로비저닝으로 인한 인적 오류 방지 가능
        - 스크립트 기반 예약, 다른 프로세스에서 트리거하는 방식으로 자동 실행 가능
        - Windows, macOS 및 Linux의 사용자 이용 가능

- **AWS SDK**
    - 프로그래밍 언어 또는 플랫폼용으로 설계된 API를 통해 AWS 서비스를 보다 간편하게 사용
    - SDK를 통해 AWS 서비스를 기존 애플리케이션과 함께 사용하거나 AWS에서 실행할 완전히 새로운 애플리케이션을 생성 가능
    - 지원 가능한 프로그래밍 언어 → C++, 자바, .NET 등

- **AWS Elastic Beanstalk**  
    > `PaaS`, `애플리케이션 배포 · 확장`  

    Amazon EC2 기반 환경 프로비저닝을 지원하는 서비스 

    - 웹 애플리케이션 및 서비스를 신속하게 배포하고 확장하는 데 사용 → 인프라가 아닌 비즈니스 애플리케이션에 집중
    - 사용자가 코드 및 구성 설정을 제공하면 다음 작업을 수행하는 데 필요한 리소스를 배포
        - 용량 조정
        - 로드 밸런싱
        - 자동 조정(Auto Scaling)
        - 애플리케이션 상태 모니터링

- **AWS CloudFormation**
    > `코드로서의 인프라`, `인프라 리소스의 선언적 관리`, `템플릿 기반(JSON/YAML)`, `자동화 반복 가능한 배포`   

    - 애플리케이션에 필요한 리소스를 모델링하고 프로비저닝 
    - 인프라를 코드로 취급 가능(Infrastructure as code) 
    - JSON, YAML 텍스트 문서 기반의 CloudFormation 템플릿을 활용   
        → **선언적인 방식**으로 사용하여 다양한 AWS 기반 리소스 정의 
    - 아키텍처를 다른 환경, 리전, AWS 계정에서 반복해야 할 때  
        → **자동화되고 반복 가능한 배포**를 만드는 데 도움
    - 대다수의 AWS 리소스를 지원

#### 3.2 AWS 글로벌 인프라 정의
---
#### Knowledge of:
---

- **AWS 리전(Region)** ❗️   
    > `최소 3AZ`
    AWS 리소스가 있는 지리적으로 구분된 영역

    - **최소 3개 이상의 물리적으로 분리된 가용 영역으로 구성**   
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
        > `저지연`
        - 사용자와 지리적으로 근접한 AWS 리전의 확장(**저지연 서비스 제공 목적**)
        - EC2, RDS, ECS, EBS, ElasticCache, AWS Direct Connect 등과 호환 

- **가용 영역(AZ; Availability Zone)** ❗️   
    리전 내의 단일 데이터 센터 또는 데이터 센터 그룹

    - AWS 글로벌 인프라의 완전히 격리된 파티션  
    - 각 가용 영역은 물리적으로 분리 → 고가용성, 내구성 보장 
    - **다중 가용 영역 배포 → 고가용성 확보**

- **엣지 로케이션(Edge Location)** ❗️   
    <u>Amazon CloudFront(CDN)가 더 빠른 콘텐츠 전송을 위해 고객과 가까운 위치에 콘텐츠 사본을 캐싱하는 데 사용</u>

- **AWS Outposts**  
    - **하이브리드 클라우드 방식**으로 인프라를 실행할 수 있도록 지원하는 서비스  
        → 온프레미스 애플리케이션을 클라우드로 옮기지 않고도 AWS의 클라우드 서비스를 사용할 수 있게

#### 3.3 AWS 컴퓨팅 서비스 식별
---
#### Knowledge of:
- AWS 컴퓨팅 서비스
---

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
            - 배치 처리 워크로드

    - **메모리 최적화 인스턴스**   
        고성능 데이터베이스와 같이 메모리에서 대규모 데이터 세트를 처리하는 워크로드에 적합 

    - **엑셀러레이티드 컴퓨팅 인스턴스**  
        부동 소수점 수 계산, 그래픽 처리, 데이터 패턴 일치 등

    - **스토리지 최적화 인스턴스**   
        로컬 스토리지의 대규모 데이터 세트에 대한 높은 순차적 읽기 및 쓰기 액세스가 필요한 워크로드를 위해 설계 
        
        데이터 웨어하우징 애플리케이션

- **컨테이너** 
    애플리케이션의 코드와 종속성을 하나의 객체로 패키징 
    
    > Docker: 소프트웨어를 _컨테이너_ 라는 표준화된 유닛으로 패키징 
    > Kubernetes: 컨테이너 시스템을 확장 관리, 조정 및 예약할 수 있는 컨테이너 오케스트레이션 

    - **Amazon Elastic Container Service(Amazon ECS)**
        컨테이너식 애플리케이션 실행 확장 고성능 컨테이너 관리 시스템 

        - Docker 컨테이너 지원
            - Docker Community Edition 및 Docker Enterprise Edition 사용 지원 
            - API 호출을 사용하여 Docker 지원 애플리케이션을 시작 및 중지

    - **Amazon Elastic Kubernetes Service(Amazon EKS)**
        완전 관리형 Kubernetes를 서비스  

        - 컨테이너식 애플리케이션을 대규모로 배포하고 관리하는 데 사용할 수 있는 오픈 소스 소프트웨어

- **서버리스 컴퓨팅**
    - **AWS Fargate**  
        > `컨테이너용 서버리스 컴퓨팅 엔진`

        Amazon ECS 및 Amazon EKS와 함께 작동하는 컨테이너용 서버리스 컴퓨팅 엔진

        - 서버를 프로비저닝하거나 관리할 필요가 없음(서버 인프라 관리 자동화)
        - 애플리케이션별 리소스를 지정하고 비용 지불
        - 설계에 따른 애플리케이션 격리 → 보안 향상 

    - **AWS Lambda**
        > `트리거`
        
        - 거의 모든 유형의 애플리케이션 또는 백엔드 서비스에 대한 코드 실행 가능
        - <u>사용한 컴퓨팅 시간에 대해서만 비용 지불</u>
            - Lambda 함수를 실행하는데 걸리는 시간, Lambda 함수에 대한 요청의 수 기준 
            - AWS 계정의 총 Lambda 함수의 수, 특정 Lambda 함수의 버전 수 → 요금에 영향 ✗
        - 서버를 프로비저닝하거나 관리할 필요가 없음
        - 최대 실행 시간 15분
        - Lambda 작동 방식
            1. Lambda에 코드 업로드 
            2. 이벤트 소스에서 트리거되도록 코드 설정
            3. 코드는 트리거될 때만 실행(웹 또는 모바일 앱에서 직접 호출 가능)

- **AWS Auto Scaling** ❗️  
    > `수요에 따라 Scale In/Out`, `내결함성`, `가용성`, `비용 절감` 
    
    애플리케이션을 모니터링하고 수요 변화에 대응 → 리소스 그룹에서 용량을 자동으로 추가/제거하는 서비스

    - 스케일링
        - 수직적 확장(Scale Up) → 하드웨어의 스펙 향상
        - 수평적 확장(Scale Out) → 인스턴스의 개수 확장, 내결함성

    - 스케일링 전략 
        > 동적 조정, 예측 조정 함께 사용 → 더 빠른 조정   
        - 수동 스케일링(Manual Scaling)

        - 동적 스케일링(Dynamic Scaling)
            - 단순 스케일링(Simple Scaling)
            - 단계적 스케일링(Step Scaling)
            - 대상 추적 스케일링(Target Tracking Scaling)

        - **예측 스케일링(Predictive Scaling)** ❗️
            - CloudWatch 기록 데이터 기반 필요량 예측

    - Auto Scaling 그룹(ASG)
        - 최소 인스턴스 크기(Minimum size)
        - 희망 인스턴스 용량(Desired capacity)  
            - 희망 Amazon EC2 인스턴스 수를 지정 ✗ → 최소 크기로 설정
        - 최대 인스턴스 크기(Maximum size)

- **Elastic Load Balancing(ELB)**

    - 로드 밸런서 기능
        - 인스턴스의 정기적인 상태 확인
        - 여러 다운스트림 인스턴스에 스프레드 로드 
        - 다운스트림 인스턴스의 실패 처리 
    - 여러 리전에 걸친 대상은 허용하지 않음

    - 로드 밸런서 유형
        - **Application Load Balancer** 
            - HTTP/HTTPS/gRPC 프로토콜
            - HTTP 라우팅 기능 
            - 정적 DNS(URL)
            - `Layer 7`에서 작동하며 극단적인 성능에는 적합하지 않음 
        - **Network Load Balancer** 
            - TCP/UDP 프로토콜
            - 정적 IP
            - **낮은 지연시간으로 초당 수백만 개의 요청 처리 가능** 
            - `Layer 4`에서 작동하며 초고성능으로 TCP, UDP 및 TLS 트래픽의 로드 밸런싱에 적합 
        - **Gateway Load Balancer** `Layer 3`
            - IP 패킷 자체에서 GENEVE 프로토콜 
            - 트래픽을 방화벽으로 라우팅 
        - ~~Classic Load Balancer~~ `Layer4 & 7`

#### 3.4 AWS 데이터베이스 서비스 파악
---
#### Knowledge of:
- AWS 데이터베이스 서비스
    - 관계형 데이터베이스
        - Amazon RDS 
        - Amazon Aurora

    - NoSQL 데이터베이스
    - 인 메모리 데이터베이스/캐시

- 데이터베이스 마이그레이션
---

- 관계형 데이터베이스 
    - **Amazon RDS** ❗️  
        - 데이터베이스 관리 작업 자동화 
            - 프로비저닝, 구성, 패치 적용, 백업, 이중화, 장애 조치, 재해 복구과 같은 데이터베이스 관리 작업을 자동화
            - On-Premise 환경에서 Amazon RDS로 _Lift and Shift(Rehost)_ 마이그레이션 가능(AWS DMS)  
            
        - 주요 데이터베이스 엔진 지원 ❗️  
            <small>
            - IBM Db2
            - MariaDB
            - Microsoft SQL Server
            - MySQL
            - Oracle Database
            - PostgreSQL
            </small>

        - 다양한 보안 옵션 제공
            - 저장 시 암호화
            - 전송 중 암호화

        - 자동 백업 기능 및 특정 시점 복구(Point-in-Time Recovery) 제공
        - **고객이 데이터, 스키마 소유 및 네트워크 제어**
        - **RDS 배포 옵션**
            - Read Replicas  
                > `비동기식 복제`, `확장성`
                - 읽기 성능 향상 → 읽기 작업이 많은 워크로드 부하 분산에 적합
                - 비동기식 복제
                - 리소스의 수평 확장
                
            - Multi-AZ 
                > `동기식 복제`, `고가용성`, `내결함성`
                - 가용 영역(AZ) 수준 장애 보호 → 리전 장애로부터 보호 ✗
                - 동기식 복제 

            - Multi-Region(Read Replicas)

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
        - 기본적으로 **저장 중 암호화(Data at Rest)** 지원
            - _Amazon RDS, Redshift, Aurora의 경우 암호화에 추가 비용 발생_ 
        - **Global Tables** ❗️
            - 여러 AWS 리전에서 저지연 접근이 가능한 데이터 복제본(Active-Active Replication) 제공 

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
        Amazon DynamoDB용 고가용성 인 메모리 캐시 서비스
        
        - 응답 시간을 한 자릿수 밀리초에서 마이크로초까지 향상시킬 수 있음
        - 비관계형 데이터를 3배나 개선하도록 설계된 기본 캐싱 계층

- **Amazon Neptune**  
    그래프 데이터베이스 서비스  

- **Amazon QLDB(Quantum Ledger Database)**
    완전 관리형 원장(금융 거래 기록 장부) 데이터베이스

    - 변경 불가능한 기록 시스템(삭제, 수정 불가능)
    - 애플리케이션 데이터에 발생한 모든 변경 사항의 전체 기록 검토 가능
   
- **Amazon Managed Blockchain**
    > `탈중앙화(decentralized)`  

    - 분산형 원장 시스템
    - 오픈 소스 프레임워크를 사용하여 블록체인 네트워크를 생성하고 관리하는 데 사용할 수 있는 서비스

- **Amazon Redshift** ❗️  
    > `OLAP(Online Analytical Processing)`, `데이터 웨어하우징`, `분석`

    - PostgreSQL 기반의 데이터베이스 
    - 빅 데이터 분석에 사용할 수 있는 **데이터 웨어하우징 서비스**
    - 여러 원본에서 데이터를 수집하여 데이터 간의 관계 및 추세를 파악하는데 도움

- **Amazon Elastic MapReduce(Amazon EMR)**
    빅데이터 분석 처리하기 위해 Hadoop 클러스터 생성 지원 

- **Amazon Athena**  
    서버리스 대화형 쿼리 서비스
    - 표준 SQL을 이용하여 Amazon S3의 데이터 분석 

- **Amazon Quicksight**  
    클라우드 기반 비즈니스 인텔리전스(BI) 서비스 → 데이터 시각화 및 대시보드 

- **AWS Glue**  
    완전 관리형 ETL(Extract, Transform, Load) 서비스

#### 3.5 AWS 네트워크 서비스 파악
---
#### Knowledge of:
- AWS 네트워크 서비스
---

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
            VPC와 인터넷 간의 연결
        - **NAT 게이트웨이 및 NAT 인스턴스**  
            - NAT(Network Address Translation) 게이트웨이      
                사설 서브넷 내의 인스턴스가 프라이빗 상태를 유지하면서 인터넷이나 다른 AWS 서비스에 연결할 수 있도록 허용 
                - AWS에서 관리
            - NAT 인스턴스  
                - 사용자가 관리
        - **보안 그룹(Security Group)** `인스턴스 · ENI 수준`   
            - 인스턴스의 가상 방화벽 역할(인스턴스 수준에서 작동)
            - 인바운드 및 아웃바운드 트래픽을 제어   
                → <u>기본적으로 모든 인바운드 트래픽을 거부, 모든 아웃바운드 트래픽을 허용</u>
            - ALLOW(허용) 규칙만 존재 
                → 특정 사용자를 차단할 수 없음 
        - **네트워크 ACL(Network Access Control List, NACL)** 
            - **서브넷 수준**에서 인바운드 및 아웃바운드 트래픽을 제어하는 가상 방화벽
            - ALLOW(허용) 및 DENY(거부) 규칙이 모두 존재 
        - **Elastic IP(EIP)**  
            - 고정된 공용 IPv4
        - **VPC 피어링(VPC Peering)**  
            > `데이터 비공개 공유`
            
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

    - **Site-to-Site VPN**   
        > `암호화된 네트워크 경로`, `빠른 설정`

        - 온프레미스 네트워크와 AWS 클라우드 네트워크 간에 **암호화된 네트워크 경로** 생성
        - **Public 인터넷**을 통해 연결 → 대역폭 제한, 보안 문제 발생 가능
        - 약 5분 정도의 빠른 설정 

    - **AWS Direct Connect(DX)** ❗️  
        > `보안`, `인터넷 우회`, `비공개 전용 네트워크 연결`, `느린 설정 & 높은 비용` 

        - <u>온프레미스 데이터 센터와 AWS 클라우드 간에</u> 빠르고 안전한 **비공개 전용 연결(private network)** 을 설정
            - 네트워크 연결을 통해 내부 네트워크를 Direct Connect 위치에 연결   
                온프레미스 라우터, Direct Connect 라우터에 연결 → 네트워크 경로의 ISP를 우회
        - 짧은 지연 시간, 최대한 높은 수준의 보안 → 느린 설정, 높은 비용 
        - 높은 수준의 규제 및 규정 준수 요구사항을 쉽게 충족, 잠재적 대역폭 문제 방지 
        - 네트워크 비용을 절감하고, 네트워크를 통과할 수 있는 대역폭을 늘리는 데 도움

    - **AWS Transit Gateway**  
        > `Hub & Spoke`, `여러 VPC 간의 연결`  
        - 여러 VPC, 온프레미스 네트워크를 하나의 중앙 허브를 통해 Amazon 가상 프라이빗 클라우드(Amazon VPC)와 온프레미스 네트워크를 연결(peering)할 수 있게 해주는 서비스  
            → Hub & Spoke 형태 
        - 전 세계로 확장하는 경우, 지역 간 피어링은 AWS 글로벌 네트워크를 사용하여 AWS 트랜짓 게이트웨이를 연결

#### 3.6 AWS 스토리지 서비스 파악
---
#### Knowledge of:
- AWS 스토리지 서비스
---

- **Instance Store**
    > `임시 블록 수준 스토리지`, `장애 · 종료 시 데이터 손실`

    - Amazon EC2 인스턴스에 **임시 블록 수준 스토리지**를 제공
    - 인스턴스 사용 비용의 일부로 포함 → 비용 효율적 솔루션
    - EC2 인스턴스를 중지 또는 종료 시, 데이터 삭제 → 임시 데이터(캐시, 임시 데이터, 로그 파일)에 적합
    - 인스턴스 간 파일 공유에 사용 불가

- **Amazon Elastic Block Store(Amazon EBS)** ❗️  
    > `고성능 블록 수준 스토리지`, `가용 영역 수준 리소스` 

    - <u>EC2 인스턴스를 중지 또는 종료하더라도 연결된 EBS 볼륨의 모든 데이터는 보존</u> 
        - 루트 볼륨의 경우, 기본적으로 인스턴스 **종료** 시 삭제(Delete on Termination) 옵션 활성화 
    - 특정한 단일 가용 영역에 EBS 볼륨 생성
        - **동일한 가용 영역의 인스턴스에만 연결 가능(가용 영역 수준 리소스)**
        - 기본적으로 볼륨은 한 번에 하나의 인스턴스에만 연결 가능(여러 볼륨을 단일 인스턴스에 연결 가능)
        - EBS Multi Attach → 하나의 EBS 볼륨을 여러 인스턴스에 동시에 연결
    - EBS 스냅샷(증분 백업) → Amazon S3에 저장 → 복구 / 다른 가용 영역(AZ) 또는 리전 간 복제

- **Amazon Elastic File System(Amazon EFS)** ❗️  
    > `파일 스토리지`, `수백 개의 EC2 인스턴스에서 동시에 액세스`

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
    > `Third-party File Systems`

    - FSx for Lustre
        - 완전 관리형
        - 고성능 컴퓨팅(High Performance Computing, HPC)용 스토리지
    - FSx for Windows File Server
        - 완전 관리형
        - 비즈니스 애플리케이션용
    - FSx for NetApp ONTAP
    
- **Amazon Simple Storage Service(Amazon S3)** ❗️  
    > `객체 스토리지 서비스`, `리전 단위`  

    - <u>데이터를 버킷에 객체(Object)로 저장</u>
    - 모든 유형의 파일(이미지, 동영상, 텍스트 파일 등)을 업로드 가능하며, 업로드 가능한 객체의 최대 파일 크기는 5TB
    - 파일 업로드 시, 권한 설정 → 파일에 대한 표시 여부 및 액세스를 제어 가능
    - Amazon S3 버전 관리 기능 → 객체 변경 사항 추적 가능 
    - Amazon S3 데이터 SQL 기반 분석 → Amazon Athena
    - 객체(Object)는 Amazon S3 관리 키(SSE-S3)로 서버 측 암호화를 사용하여 자동으로 암호화

    - **S3 Replication**
        - Cross-Region Replication(CRR) → 리전 간 복제 
        - Same-Region Replication(SRR) → 동일 리전 복제 

    - **S3 Encryption** 
        - Server-Side Encryption `Default`
        - Client-Side Encryption

    - **S3 Transfer Acceleration**  
        클라이언트와 S3 버킷 간의 장거리 파일 전송을 파일을 빠르고 쉽고 안전하게 전송할 수 있는 버킷 수준 기능

    - **Amazon S3 스토리지 클래스** ❗️   
        1\) 데이터 검색 빈도 2\) 필요한 데이터 가용성을 고려하여 클래스 선택,   

        - **S3 Standard**
            - 자주 액세스하는 데이터를 위해 높은 내구성, 가용성 및 성능을 갖춘 스토리지 제공
            - 짧은 지연 시간 및 많은 처리량 성능
            - 최소 3개의 AZ에 데이터를 저장

        - **S3 Intelligent-Tiering**
            > `액세스 패턴 모니터링`

            - 액세스 패턴을 알 수 없거나 액세스 패턴이 변경되는 데이터
            - **객체의 액세스 패턴을 모니터링** → 30일 연속 객체에 액세스하지 않으면 자동으로 계층 이동
            - 자동 비용 절감 효과

        - **S3 Standard-Infrequent Access(S3 Standard-IA)**
            - 자주 액세스하지 않지만 필요할 때 빠르게 액세스해야 하는 데이터  
                → 백업, 재해 복구 파일 또는 장기 보관이 필요한 모든 객체에 적합 
            - 최소 3개의 AZ에 데이터를 저장

        - **S3 One Zone-Infrequent Access(S3 One Zone-IA)**  
            > `단일 AZ`  
            > 낮은 액세스 빈도를 가지고 있지만 즉시 액세스 필요하며, 쉽게 재생성 가능한 경우에서 가장 비용 효율적인 방법

            - 자주 액세스하지 않지만 필요할 때 빠르게 액세스해야 하는 데이터
            - **단일 AZ에 데이터 저장**   
                - 가용성 및 복원력이 필요 없는 경우(e.g. 쉽게 재생성이 가능한 경우) 
                - S3 Standard-IA보다 비용이 20% 저렴

        - **S3 Glacier**
            > `콜드 데이터(Cold Data)`, `암호화(AES-256)`

            - 데이터 보관을 위한 안전하고 내구성이 있으며 저렴한 스토리지 제공 
            - 객체를 몇 분에서 몇 시간 이내에 검색
            - 256비트 고급 암호화 표준(AES-256)으로 서버측 자동 암호화 
            - 잠금 정책 
                - 한 번 쓰기/여러 번 읽기(WORM)

        - **S3 Glacier Deep Archive**
            - 검색시간 요구 사항이 없는 경우
            - 데이터의 장기 보관 및 디지털 보존
            - 객체를 12시간 또는 48시간 내에 데이터 검색

- **AWS Storage Gateway**
    > `하이브리드 클라우드 스토리지`

    - AWS 내 사용자의 On-Premise 데이터와 클라우드 데이터를 연결
    - 모든 데이터는 SSL을 사용하여 암호화

    - Storage Gateway 유형 ❗️  
        - File Gateway
        - Volumn Gateway
        - Tape Gateway

#### 3.7 AWS 인공 지능 및 기계 학습(AI/ML) 서비스와 분석 서비스 파악
---
#### Knowledge of:
- AWS AI/ML 서비스
- AWS 분석 서비스
---

- AI/ML 서비스
    - **Amazon Rekognition**  
        이미지 및 비디오 분석 서비스 → 사람, 텍스트, 객체 등을 인식하고 분석
    - **Amazon Transcribe**  
        음성을 텍스트로 자동 변환해주는 서비스
        - Redaction을 이용하여 개인 식별 정보(Personally Identifiable Information, PII) 자동 제거 기능 
        - 다국어 오디오에 대한 자동 언어 식별 기능 지원 
    - **Amazon Polly**  
        텍스트를 음성으로 변환해주는 머신러닝 서비스(TTS)
    - **Amazon Translate**  
        머신러닝 언어 번역 서비스
    - **Amazon SageMaker**  
        **ML 모델을 신속하게 빌드, 훈련, 배포할 수 있도록** 돕는 고차원의 완전 관리형 머신러닝 서비스
    - **Amazon Lex**  
        음성과 텍스트를 사용해 대화형 인터페이스(챗봇, 음성 비서 등)를 구축할 수 있는 서비스  
        - 자동 음성 인식(ASR) → 음성을 텍스트로 변환
        - NLU(자연어 이해)의 고급 딥 러닝 기능 → 텍스트의 의도를 인식
    - **Amazon Textract**  
        문서에서 텍스트 및 데이터 자동 추출 머신러닝 서비스
    - **Amazon Forcast**  
        예측 서비스
    - **Amazon Kendra**  
        **엔터프라이즈 검색 서비스** → 자연어 검색으로 다양한 형식(텍스트, PDF, HTML, PPT, MS Word 등) 정보 검색 가능 
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
---
#### Knowledge of:
---

- **Application Integration 서비스**
    - **Amazon EventBridge**  
        > `서버리스 이벤트 버스`

        - 이벤트 기반 대규모 애플리케이션 구축 

    - **Amazon Simple Queue Service(Amazon SQS)** ❗️  
        > `메세지 대기열`

        완전 관리형 메시지 대기열 서비스 

        - 분산 애플리케이션 간의 통신을 비동기적으로 처리
        - 메세지 손실이나 다른 서비스 사용 없이 소프트웨어 구성 요소 간에 메시지를 전송, 저장, 수신 가능 
        - 메세지 → Amazon SQS Queue → 사용자/서비스는 대기열에서 메세지 검색하여 처리 → 대기열에서 삭제 
        - 볼륨에 상관없이 소프트웨어 구성 요소 간에 메시지를 전송, 저장, 수신 가능
        - 대기열 타입 
            - Standard Queue
                - 높은 처리량
                - 최소한의 중복
                - 메세지 순서 보장 ✗
            - FIFO Queue 
                - 메세지 순서 보장

    - **Amazon Simple Notification Service(Amazon SNS)**  
        > `Pub/Sub`, `구독자`, `주제(Topic) 기반 메세지 발행`

        완전 관리형 메세지 발행/구독 서비스 

        - 최종 사용자에게도 이메일, 메세지, 푸시 알림, HTTP 요청 포함 메시지 전달 
         - 발행/구독(Pub/Sub) 방식
         - 메세지 전달 채널인 SNS Topic 생성 → **구독자 메세지 게시** 가능 
            - 구독자 → SQS 대기열, AWS Lambda 함수, HTTPS 또는 HTTP 웹 후크 같은 엔드포인트

    - **AWS Step Functions** `서버리스`, `워크플로우 시각화`

- **AWS Amplify**
- **AWS AppConfig**
- **AWS Cloud9**
- **AWS CloudShell**
- **AWS CodeArtifact**
- **AWS CodeBuild**
    완전 관리형 빌드 서비스

    사용자가 소스 코드를 자동으로 컴파일하고, 단위 테스트를 실행하고, 배포 준비가 된 아티팩트를 생성할 수 있도록 도와주는 서비스

- **AWS CodeStar**
- **AWS CodeCommit** `소스 코드 버전 제어 서비스`
- **AWS CodeDeploy**
    - <u>온프레미스에서 실행되는 EC2 인스턴스 및 인스턴스를 포함한 모든 인스턴스의 코드 배포를 자동화하는 서비스</u>
    - 인프라 구성 및 조정은 다루지않음 
    
- **AWS CodePipeline**  
- **AWS AppSync**
