# AWS Certified Cloud Practitioner(CLF-C02) 
### Domain 1: Cloud Concepts
#### 1.1 AWS 클라우드의 이점 정의
- **클라우드 컴퓨팅이란?**  
    - <u>on-demand delivery</u>  
        컴퓨팅 파워, 데이터베이스 저장소, 애플리케이션, 다른 IT 리소스들을 온디맨드로 제공하는 것
    - <u>pay-as-you-go pricing</u>  
        클라우드 서비스 플랫폼을 통해 종량 과금제 방식 제공
    - provision exactly the right type and size of computing   
      필요한 컴퓨팅 리소스의 유형과 크기에 따라 프로비저닝 가능
    - almost instantly 
    - simple way to access    

- **클라우드 컴퓨팅의 6가지 이점** 
    - 고정 비용을 가변 비용으로 전환 
        - 초기 자본 지출(CAPEX) 절감 
        - 총 소유 비용(TCO)와 운영 비용(OPEX) 절감
    - 규모의 경제(economies of scale)의 이점
      - 높은 규모의 경제 달성을 통한 단위당 비용 감소 
    - 용량 추정 불필요 
    - 조직 민첩성 증가
    - 데이터 센터 운영 및 유지 비용 불필요
    - 글로벌 배포 가능

- **클라우드 컴퓨팅 모델**
    | On-premises | IaaS | PaaS | SaaS | 
    | --- | :---: | :---: | :---: |
    | Applications | - | - | ✓ |
    | Data | - | - | ✓ | 
    | Runtime | - | ✓ | ✓ | 
    | OS | - | ✓ | ✓ | 
    | Virtualization | ✓ | ✓ | ✓ | 
    | Servers | ✓ | ✓ | ✓ | 
    | Storage | ✓ | ✓ | ✓ | 
    | Networking | ✓ | ✓ | ✓ | 

    - IaaS(Infrastructure as a Service)
        - 높은 유연성과 관리 제어 기능 제공 
        - Amazon EC2 (on AWS), GCP, Azure, Rackspace, Digital Ocean, Linode
    - PaaS(Platform as a Service)
        - 애플리케이션 배포 및 관리에 집중 
        - Elastic Beanstalk (on AWS), Heroku, Google App Engine(GCP), Window Azure(Microsoft)
    - Saas(Software as a Service)
        - 서비스 제공 업체가 완전히 운영 및 관리 
        - Many AWS services, Google Apps(Gmail), Dropbox, Zoom

- **클라우드 컴퓨팅 배포 모델**
    - Private Cloud(e.g. rackspace)
        - 온프레미스 방식(on-premises)
        - 단일 조직 (외부에 노출되지 않음)
        - 완전 제어
        - 강화된 보안 제공 

    - Public Cloud(e.g. MS Azure, Google Cloud, AWS)
        - 서드파티(third- party) 클라우드 서비스 제공 업체가 소유, 운영하는 클라우드 리소스를 인터넷을 통해 제공

    - Hybrid Cloud
        - (Private + Public) Cloud
        - 일부 서버 온프레미스로 유지, 일부 클라우드 확장 
        - 일부 민감 에셋 제어, 유연함 및 비용 효율성 만족 

#### 1.2 AWS 클라우드의 설계 원칙 파악
- **AWS Well-Architected Framework의 원칙** 
    - **운영 우수성(Operational excellence)**  
        - 소프트웨어를 올바르게 구축하는 동시에 우수한 고객 환경을 지속적으로 제공하기 위한 노력

        - 설계 원칙
            - 비즈니스 성과를 중심으로 팀 구성
            - 실행 가능한 인사이트를 위한 관찰성 구현
            - 자동화가 가능한 부분은 안전하게 자동화
            - 되돌릴 수 있도록 변경 사항을 조금씩 자주 적용
            - 운영 절차를 자주 개선
            - 장애 예측(Anticipate failure)
            - 모든 운영 이벤트와 장애로부터 배운 내용을 바탕으로 개선
            - 관리형 서비스 사용

    - **보안(Security)**  
        클라우드 기술을 활용하여 보안을 강화하고 데이터, 시스템 및 자산을 보호하는 능력

        - 설계 원칙
            - 강력한 자격 증명 기반 구현(최소 권한의 원칙)
            - 추적 기능 활성화
            - 모든 계층에 보안 적용
            - 보안 모범 사례 자동화 
            - 전송 및 저장 중인 데이터 보호
            - 데이터에 쉽게 액세스할 수 없도록 유지
            - 보안 이벤트에 대비

    - **안정성(Reliability)**  
        워크로드의 기능이 필요한 때에 기능을 정확하고 일관되게 수행하는 역량

        - 설계 원칙
            - 장애 자동 복구
            - 복구 절차 테스트
            - 수평적 확장으로 워크로드 전체 가용성 증대
            - 용량 추정 중지(오토 스케일링)
            - 변경 사항 관리 자동화 

    - **성능 효율성(Performance efficiency)**  
        - 설계 원칙
    - **비용 최적화(Cost optimization)**  
        - 설계 원칙
    - **지속 가능성(Sustainability)**  
        - 설계 원칙

#### 1.3 AWS 클라우드 마이그레이션의 이점과 전략 이해
- **클라우드 채택 전략**

#### 1.4 클라우드 경제성의 개념 이해
