# AWS Certified Cloud Practitioner(CLF-C02) 
### Domain 4: Billing, Pricing, and Support 🌕🌘🌑🌑🌑
#### 4.1 AWS 요금 모델 비교
- **On-Demand Instances** 
    - **사용한 컴퓨팅 시간**에 대해서만 비용을 지불
        - 중단할 수 없는 불규칙한 단기 워크로드가 있는 애플리케이션에 매우 적합
        - 애플리케이션 개발 및 테스트, 예측할 수 없는 사용 패턴 애플리케이션에 적합
        - 1년 이상 지속되는 워크로드에는 권장하지 않음(비용 절감 측면)

- **Amazon EC2 Savings Plans** `사용량 약정`  
    - 1년 또는 3년 기간 동안 <u>일정한 컴퓨팅 사용량을 약정</u>
        - **컴퓨팅 사용량이 일정한 워크로드에 매우 적합**
    - 온디맨드 요금에 비해 최대 72%까지 비용 절감
    - 약정 초과 사용량 → 일반 온디맨드 요금 부과

- **Reserved Instances** `기간 약정`  
    - 표준 예약 및 컨버터블 예약 인스턴스는 **1년 또는 3년** <u>기간 약정</u>
        - 정기 예약 인스턴스는 1년 약정으로 구입 가능
        - 3년 약정 옵션 → 더 큰 비용 절감
    - 약정 종료 시, 중단 없이 Amazon EC2 인스턴스 계속 사용(온디맨드 요금 부과)
        - 인스턴스 종료, 인스턴스 속성과 일치하는 새 예약 인스턴스 구입 시 중단

- **Spot Instances**
    - 시작 및 종료 시간이 자유롭거나 중단을 견딜 수 있는 워크로드에 적합
    - <u>미사용 Amazon EC2 컴퓨팅 용량 사용</u> → 온디맨드 요금의 최대 90%까지 비용 절감
    - Savings Plans와 달리, 계약이나 일정한 컴퓨팅 사용량에 대한 약정 필요 ✗

- **Dedicated Instances**
    - **사용자 전용**의 Amazon EC2 인스턴스 용량을 갖춘 물리적 서버
    - 모든 Amazon EC2 옵션 중에서 전용 호스트가 가장 비용이 많이 듬

#### 4.2 결제, 예산 및 비용 관리를 위한 리소스 이해
- **AWS Organizations** ❗️  
    - 모든 AWS 계정의 <u>중앙 집중식 관리</u> 
    - 조직 내 모든 계정 간 사용량 **통합 결제** (대량 구매 요금 할인, 예약 인스턴스 할인 및 Savings Plans)
    - **AWS 계정 생성 자동화 API 제공**
    - **Service Control Policies(SCP)를 통한 계정 권한 제한 가능**
        - IAM 정책은 권한을 부여, SCP는 권한을 제한하거나 필터링 

- **AWS Budgets** ❗️  
    서비스 사용량이 예산 금액(임계값)을 초과하거나 초과할 것으로 예상되는 경우 **사용자 지정 알림** 설정 가능  
    → 과금 방지 

    - 최초 2개의 예산 생성까지 무료, 이후 예산 당 일별 요금 과금(0.02 USD)
    - 예산 당 최대 5개의 SNS 알림 지원 
    - 예산 정보는 하루에 최대 세 번 업데이트
    - 예산 종류 
        - Usage
        - Cost
        - Reservation
        - Saving Plans

- **AWS Cost and Usage Report(AWS CUR)**  
    종합적이고 상세한 AWS 비용 및 사용량 보고서
    
    - AWS 서비스 메타 데이터 포함(서비스 및 리전, 인스턴스 유형, 태그 등)
    - 하루에 한 번 CVS 파일 형식으로 AWS S3 버킷에 보고서 업데이트 
    - Athena, Redshift, QuickSight로 리포트 데이터 통합 분석 가능 

- **AWS Cost Explorer** ❗️  
    시간 경과에 따라 **AWS 비용 및 리소스 사용량을 시각화**하여 분석/관리할 수 있는 콘솔 기반 도구

    - 발생 비용 기준 상위 5개 AWS 서비스의 비용 및 사용량에 대한 기본 보고서 포함
    - 최대 12개월 이전의 데이터 소급 분석 → 앞으로 12개월 동안의 비용 예측 가능 
    - Cost Explorer API를 통해 비용 및 사용량 데이터 쿼리 가능(각 요청마다 0.01 USD 비용 발생)

- **AWS Billing Conductor**  
    AWS Marketplace 채널 파트너 (파트너) 및 조직을 위한 맞춤형 청구 서비스

- **AWS Pricing Calculator**  
    특정 AWS 솔루션 아키텍처에 대한 월간/연간 **비용 추정 도구**  
    - 비용 산출 결과 보고서 생성 및 다운로드 가능 


#### 4.3 AWS 기술 리소스 및 AWS Support 옵션 파악
- **AWS Support 플랜** ❗️    
    Developer, Business 및 Enterprise Support 플랜 → 월 단위로 비용을 지불  

    - **Basic** 
        - 모든 AWS 고객 무료 제공
        - 24시간 연중무휴 고객 서비스, 설명서, 백서, AWS re:Post
        - 일부 AWS Trusted Advisor 검사
        - AWS Personal Health Dashboard

    - **Developer**
        - Basic Support
        - Cloud Support Associate에게 업무 시간에 웹을 통해 액세스

    - **Business**
        - Basic 및 Developer Support
        - **모든 AWS Trusted Advisor 검사**
        - 클라우드 지원 엔지니어에게 연중무휴 24시간 전화, 웹 및 채팅 액세스
        - 인프라 이벤트 관리

    - **Enterprise On-Ramp**
        - Basic, Developer 및 Business Support
        - 추가 요금 지불시 AWS re:Post 프라이빗 액세스 가능 
        - Technical Account Manager 풀  
        
    - **Enterprise**
        - Basic, Developer, Business 및 Enterprise On-Ramp Support
        - 기술 지원 관리자(Technical Account Manager, TAM) 액세스  
            → 인프라 이벤트 관리, Well-Architected 검토, 운영 검토 제공 

- **AWS Marketplace**      
    - Independent Software Vendor(ISV)의 소프트웨어 리스팅 수천 개가 포함된 **디지털 카탈로그**  
    - 써드파티 소프트웨어, 서비스, 데이터를 손쉽게 검색하고 평가하고 구독(구매), 배포, 관리 가능 
    - 즉시 구입하여 사용 가능, 유연한 결제 옵션 제공
    - 신뢰 가능한 세부 정보 및 제품 리뷰 제공 → 정보에 입각한 의사결정 가능 
