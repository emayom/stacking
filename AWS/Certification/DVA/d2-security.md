---
last_modified_at: '2025-03-16T15:17:06.201Z'
date: '2025-03-16T15:17:06.201Z'
---
# AWS Certified Developer - Associate (DVA-C02) 
## Domain 2: Security

#### TOC
- [2.1 애플리케이션 및 AWS 서비스에 대한 인증 또는 권한 부여를 구현합니다.](#21-애플리케이션-및-aws-서비스에-대한-인증-또는-권한-부여를-구현합니다)
    - [AWS IAM](#aws-identity-and-access-managementiam)
    - [MFA](#mfamulti-factor-authentication)
    - [AWS STS](#awssecurity-token-servicests)
    - [Amazon Cognito](#amazon-cognito)
    - [AWS Directory Service](#aws-directory-service)

- [2.2 AWS 서비스를 사용하여 암호화를 구현합니다.](#22-aws-서비스를-사용하여-암호화를-구현합니다)
    - [봉투 암호화(Evelope Encryption)](#봉투-암호화evelope-encryption)
    - [AWS Encryption SDK](#aws-encryption-sdk)
    - [AWS KMS](#aws-kmskey-management-service)
    - [AWS CloudHSM](#aws-cloudhsmhardware-security-module)
    - [AWS Certificate Manager(ACM)](#aws-certificate-manageracm)
    - [AWS Private CA](#aws-private-certificate-authority)

- [2.3 애플리케이션 코드에서 민감한 데이터를 관리합니다.](#23-애플리케이션-코드에서-민감한-데이터를-관리합니다)
    - [AWS Secrets Manager](#aws-secrets-manager)
    - [AWS Systems Manager Parameter Store](#aws-systems-manager-parameter-store)
    - [AWS Nitro Enclaves](#aws-nitro-enclaves)

## 2.1 애플리케이션 및 AWS 서비스에 대한 인증 또는 권한 부여를 구현합니다.
---
#### Knowledge of:

- 최소 권한 원칙(Principle of Least Privilege) 
    - 그 어떠한 사용자도 필요한 것 이상으로 권한을 가지고 있어서는 안 된다.  

- 전달자 토큰(Bearer Token)
    - HTTP Authorization에서 Bearer 타입의 인증을 위해 사용되는 토큰
        - JWT(JSON Web Token)
        - OAuth → `불투명한(Opaque) 문자열`
            - Access Token: API 요청 시 클라이언트를 인증하는 데 사용
            - Refresh Token: 새로운 액세스 토큰을 발급받을 때 사용
        - AWS STS(AWS Security Token Service)

- 역할 기반 액세스 제어(RBAC)
    > [!NOTE]  
    > 최소 권한 원칙을 실현하는 중요한 방식 중 하나
    - 사용자(User)에게 직접 권한을 부여하는 대신, 역할(Role)을 생성하고 역할에 권한을 할당한 후, 사용자가 해당 역할을 부여받도록 하는 방식

- ID 페더레이션(Identity Federation)
    - 외부 ID 제공자(Identity Provider, IdP)를 신뢰하여 인증(Authentication)을 위임하는 방식  
        → 사용자가 AWS 계정에 임시로 액세스하도록 허용

        - 연결 가능한 IdP
            - SAML 2.0 → 엔터프라이즈 Single Sign-On(SSO)
            - OpenID Connect(OIDC)
                - OAuth 2.0 기반 ID 인증을 위한 프로토콜 
                - Google, Facebook, Apple ID, Amazon Cognito 등이 OIDC를 지원 → Federated Identity(소셜 로그인)
            - Amazon Cognito

- 페더레이션 액세스(Federated Access)
    - ID 페더레이션을 통해 인증된 사용자에게 AWS 리소스 접근 권한(Authorization)을 부여하는 과정
    - IAM 사용자(User) 계정을 별도로 생성하지 않고, 역할(Role)과 AWS STS를 사용하여 임시 보안 자격 증명을 발급

- AWS 관리형 정책과 고객 관리형 정책의 차이점
    > AWS 관리형 정책과 고객 관리형 정책은 모두 자격 증명 기반 정책(Identity-based Policies)에 속한다. 

    - 제공자
    - 커스터마이징 가능 여부
    - 업데이트 관리 
    - 사용 계정 범위
---

### AWS Identity and Access Management(IAM)

> [!NOTE]  
> **IAM 작동 흐름**   
> 보안 주체(Principal) → 인증(Authentication) → 요청(Request) → 인가(Authorization) → 작업 또는 연산(Action(Console) or Operation(API/CLI)) → 리소스(Resource)

- IAM의 구성 요소 
    - 사용자(Users)
    - 그룹(Groups)
    - 역할(Role)
    - 정책(Policy)

#### IAM 사용자
- 사용자 이름 및 암호 조합 또는 액세스 키 집합의 형태로 <u>**영구적인 자격 증명 세트**</u>
- IAM 사용자 생성 시 고려 사항
    - 액세스 권한 제어
        - AWS Management Console → 사용자 이름 및 암호 조합
        - AWS CLI, SDK, API를 통한 프로그래밍 방식 → 액세스 키 집합 (Access Key ID & Secret Access Key)
    - 최소 권한 원칙 적용
    - IAM 그룹 활용
    - 강력한 비밀번호 정책 설정
    - MFA 활성화

#### IAM 그룹

> [!IMPORTANT]  
> IAM 그룹은 자격 증명을 관리하지 않으며, 그룹에 할당된 정책에 따라 권한을 **상속**받는다. 

- 동일한 권한을 부여받은 사용자들의 집합 = 권한 관리 단위
- IAM 그룹 구성 규칙  
    - 그룹에는 여러 사용자가 포함될 수 있으며, 사용자는 여러 그룹에 속할 수 있다.
    - 그룹은 다른 그룹에 속할 수 없다.
    - AWS 계정의 모든 사용자를 자동으로 포함하는 기본 사용자 그룹은 없다. 
    - 생성 가능한 그룹 수, 그룹에 포함될 수 있는 사용자 수는 제한되어 있다. 

#### IAM 역할 
- 15분~36시간 사이의 유효 기간이 지나면 자동으로 만료되는 <u>**임시 보안 자격 증명**</u>
    -  IAM 역할 기반의 임시 자격 증명 사용이 필요한 경우  
        → AWS STS에서 임시 자격 증명 발급(AssumeRole API 사용) 

- IAM 역할 구성 요소
    - 신뢰 정책(Trust Policy) → 어떤 주체가 이 역할을 사용할 수 있는지
    - 권한 정책(Permissions Policy) → 이 역할이 어떤 AWS 리소스에 접근할 수 있는지

- IAM 역할의 사용 사례
    - AWS 서비스 간 권한 부여
        - EC2 인스턴스에서 S3 버킷 접근 허용  
    - 교차 계정 액세스 
    - Lambda 함수 권한 관리
        - Lambda가 DynamoDB, S3 등과 연동할 때 IAM 역할을 사용하여 필요한 권한만 부여
    - 페더레이션 액세스(Federated Access)
    - CI/CD 배포 권한 부여

#### IAM 정책 
- AWS 리소스에 대한 접근 권한을 정의하는 JSON 형식의 규칙

- 정책의 평가 순서 ❗️
    1. 명시적 거부(Explicit Deny)
    2. 명시적 허용(Explicit Allow)
    3. 기본적으로 거부(Implicit Deny, 기본적으로 모든 요청은 거부됨)

- 정책 유형 
    - **자격 증명 기반 정책(Identity-based Policies)**  → 사용자(User), 그룹(Group), 역할(Role)에 적용되는 정책  
        - 관리형 정책(Managed Policy)
            - AWS 관리형 정책
            - 고객 관리형 정책 
        - 인라인 정책(Inline Policy) → 특정 사용자, 그룹, 역할에 직접 연결된 정책 
    - **리소스 기반 정책(Resource-based Policies)** → 특정 AWS 리소스(S3, Lambda, SQS 등)에 직접 적용되는 정책

- 정책 예시(JSON)
    ```json
    // ex) AWS 관리형 정책을 이용하여 특정 S3 버킷에 대한 권한 설정 
    {
        "Version": "2012-10-17",    
        "Statement": [
            {
                "Effect": "Allow",
                "Action": "s3:PutObject",   
                "Resource": "arn:aws:s3:::example-bucket/*" 
            },
            {
                "Effect": "Deny",
                "Action": "s3:DeleteObject",
                "Resource": "arn:aws:s3:::example-bucket/*"
            }
        ]
    }
    ```    

- 정책 구성 요소 
    > [!NOTE]  
    > `Version`, `Id`를 Optional top-level element로 구분한다.
    
    - **`Version`** 
        - 정책의 JSON 문법 버전 (2008-10-17, 2012-10-17(recomm) `권장`)
    - **`Id`**
        - 정책의 식별자
    - **`Statement`** 
        - 정책의 규칙을 정의하는 단일 혹은 배열
        - 구성 요소 
            - `Sid`(Statement ID) 
                - Statement의 고유 식별자 
            - `Effect`
                - `Allow` or (explicit) `Deny`
                    - 기본적으로 리소스 액세스는 `Deny`된다. 
                    - `Deny`는 `Allow`보다 우선권을 가진다.
            - `Principal` or `NotPrincipal` 
                > 리소스 기반 정책 정의 시 반드시 필요 

                - `Principal`: 리소스에 접근할 수 있는 특정 AWS 계정, 사용자, 역할 등을 지정
                - `NotPrincipal`: 특정 주체를 제외한 모든 엔터티에 정책을 적용할 때 사용

            - `Action` or `NotAction` `필수`
                >  서비스:동작 형식 (ex:  `s3:PutObject`) 

                - `Action`: 허용 또는 거부할 작업을 지정
                - `NotAction`: 특정 작업을 제외한 모든 작업을 허용 또는 거부할 때 사용 

            - `Resource` or `NotResource`
                > ARN(Amazon Resource Name) 형식 (ex: `arn:aws:s3:::example-bucket`)  

                - `Resource`: 정책이 적용될 리소스
                - `NotResource`: 특정 리소스를 제외한 모든 리소스에 정책 적용할 때 사용 

            - `Condition`
                - 정책 적용 조건 (IP 제한, MFA 사용 여부 등) 

            - Variables and tags
                - 동적 정책(Dynamic Policies)
                    ```json
                    {
                        "Version": "2012-10-17",
                        "Statement": [
                            {
                            "Effect": "Allow",
                            "Action": "s3:PutObject",
                            "Resource": "arn:aws:s3:::user-bucket/${aws:username}/*"
                            }
                        ]
                    }
                    ```
            - Supported data types

#### IAM 보안 도구 
- IAM Credentials Report → `account-level`
    - IAM 사용자에 대한 자격 증명 사용 상태를 보여주는 CSV 형식의 보고서  
        - 각 사용자의 MFA 설정 여부
        - 암호 상태
        - 액세스 키의 사용 내역 등

- IAM Access Advisor → `user-level`
    - IAM 사용자 또는 역할이 가지고 있는 각 AWS 서비스에 대한 권한 사용 여부를 추적하고, 서비스별 접근 기록 확인 → 불필요한 권한 식별 및 제거 (최소 권한 원칙 준수)

### MFA(Multi-Factor Authentication)
- Virtual MFA device `디바이스에 설치된 앱 사용` 
- U2F(Universal 2nd Factor) Security Key  `USB 포트 연결 물리장치`
- Other Hardware MFA device `여섯 자리 숫자 코드 제공 물리장치` 
    - Gemalto
    - SurePassID (for AWS GovCloud(US))
- ~~SMS text message-based MFA~~ `지원 종료`

### AWS Security Token Service(STS)
- AWS 리소스에 대한 액세스를 제어할 수 있는 임시 보안 자격 증명(Temporary Security Credentials) 생성 
    - 유효기간 → 최소 15분 ~ 최대 36시간 (기본 1시간)
    - 임시 보안 자격 증명 구성 요소 
        - Access Key ID : AWS 리소스에 대한 액세스를 인증하는 임시 액세스 키   
        - Secret Access Key : Access Key ID와 짝을 이루는 비밀 키, 요청 서명 및 인증에 사용 
        - Session Token : 임시 보안 자격 증명의 유효성을 증명하는 세션 토큰 
        - Expiration : 임시 자격 증명의 만료 시간 

- 임시 보안 자격 증명 발급 방법 
    - AWS CLI
    - AWS SDK
    - AWS Management Console
    - Lambda 함수
    - Third-Party Tools 및 SSO

#### AWS STS API
- **`AssumeRole`**  
    - IAM 역할(Role)을 임시로 가정하여 AWS 리소스에 접근
    - 동일 계정 내 또는 다른 AWS 계정 간 권한 위임

- `AssumeRoleWithSAML`
    - SAML 기반의 인증을 사용하여 역할(Role) 가정

- `AssumeRoleWithWebIdentity`
    - 웹 ID 제공자(Google, Facebook, Amazon Cognito 등)와 연동하여 역할(Role) 가정

- **`GetSessionToken`** ❗️ `STS + MFA 결합`
    - 주로 MFA를 사용하거나 권한이 제한된 사용자에게 임시 자격 증명을 제공하는 데 사용
        - IAM 정책 조건에서 `sts:GetSessionToken` 액션에 대해 `"aws:MultiFactorAuthPresent": "true"` 조건 설정 가능 → 보안 강화 
    - 최대 12시간 동안만 유효한 임시 자격 증명 제공

- `GetFederationToken`
    - 연합(Federation)된 사용자에게 AWS 서비스 액세스를 제공할 때 사용

- **`GetCallerIdentity`**
    - 현재 실행 중인 IAM 사용자 또는 역할(Role)의 ARN을 반환
- **`DecodeAuthorizationMessage`**
    - AWS 정책 평가 오류 메시지를 디코딩하여 분석할 때 사용

### Amazon Cognito
- 사용자 인증 & 인가 및 데이터 동기화 서비스 
    - IDaas(IDentity as a Service) 
    - 모바일 및 웹 애플리케이션에서 사용자의 데이터를 여러 디바이스 간에 동기화(Sync)
    - 소셜 로그인 및 게스트 로그인을 포함한 패더레이션 액세스 지원

#### 사용자 풀(Cognito User Pools) → `사용자 인증(Authentication) 담당`

- 사용자의 가입, 로그인, 비밀번호 재설정 등을 처리하는 서비스
    - 사용자 인증 정보 저장 및 관리
    - 기본 로그인, 회원가입, 사용자 관리 대시보드 UI 제공 → Cognito Hosted UI
    - 표준 인증 프로토콜(OAuth2, OIDC, SAML)을 사용하여 외부 ID 제공 업체와 통합 가능
    - Lambda, ALB, API Gateway 등 다른 AWS 리소스들과 통합 가능 

#### 자격 증명 풀(Cognito Identity Pools) → `권한 부여(Authorization) 담당` 
> [!NOTE]  
> 사용자 풀을 통한 로그인 → 자격 증명 풀을 통한 임시 자격 증명 발급 가능 

- IAM 역할과 결합하여 사용자가 AWS 리소스에 접근할 수 있도록 임시 자격 증명을 제공
    - 인증된 사용자
    - 인증되지 않은 사용자(게스트)
    - 사용자 풀 및 소셜 로그인을 통해 인증된 사용자 

### AWS Directory Service
- AWS 환경에서 AD(Active Directory)를 사용하기 위한 서비스

- Directory Service 종류 
    - **AWS Managed Microsoft AD (AWS Directory Service for Microsoft AD)**
        - Microsoft AD를 AWS에서 관리형 서비스로 제공
        - Microsoft AD의 모든 기능을 그대로 AWS 클라우드에서 사용 가능 
        - Windows 기반 애플리케이션(예: SQL Server, SharePoint)과의 통합 가능

    - **AD Connector**
        - 온프레미스 AD를 AWS와 연동하여 AWS 리소스에 대한 인증 요청을 **프록시** 처리
        - AWS에 별도의 디렉터리를 생성하지 않고, 기존 AD를 유지하면서 AWS 서비스와 연동 가능

    - **Simple AD**
        - 소규모 조직에 적합한 standalone 디렉토리 서비스 (500명 ~ 최대 5,000명)
        - Microsoft AD의 일부 기능만 사용 가능 (경량 AD 호환 서비스)
            - 유저와 그룹 멤버 관리
            - EC2 인스턴스 접속
            - Kerberos 기반의 SSO 등

- AWS IAM Identity Center(SSO)와 온프레미스 Microsoft AD 연결
    - AWS IAM Identity Center와 AWS Managed Microsoft AD 연동 (권장) 
        - AWS Managed Microsoft AD를 생성
        - 온프레미스 AD와 신뢰 관계(Trust Relationship)를 설정 → `양방향 트러스트(2-way trust`
        - IAM Identity Center에서 AWS Managed AD를 디텍터리 소스로 설정 
        - AWS 리소스 및 애플리케이션에 대한 SSO 구성 

    -  AWS IAM Identity Center와 온프레미스 AD를 직접 연동

## 2.2 AWS 서비스를 사용하여 암호화를 구현합니다.
---
- AWS 암호화 스택
    - 물리 계층: 보안 시설 및 AES-256 기반 광학적 암호화
    - 데이터 링크 계층: MACsec 기반 AES-256(IEEE)
    - 네트워크 계층: VPC 암호화, 교차 리전 연결 암호화, AWS VPN
    - 전송 계층: Amazon s2n., NLB - TLS, ALB, CloudFront, ACM 통합 
    - ✅ **애플리케이션 계층**: AWS Encryption SDK, KMS를 활용한 암호화

- 암호화 유형 
    - **전송 중 암호화(Encryption in Transit)**
        - 데이터가 네트워크를 통해 전송될 때 암호화 
        - HTTPS(SSL/TLS)

    - **저장 중 암호화(Encryption at Rest)** → 데이터 스토리지 서비스(S3, EFS)
        - 서버 측 암호화(Server-Side Encryption, SSE)
            - 전송된 데이터를 저장하기 전 서버 측에서 암호화하고, 읽을 때 복호화  
                → 모든 암호화와 해독이 서버에서 이루어짐
            - 고객 관리 통제 하에 AWS KMS에 암호화 키(CMK) 보관

        - 클라이언트 측 암호화(Client-Side Encryption, CSE)
            - 사용자가 데이터를 AWS에 전송·업로드 하기 전에 직접 암호화  
                → 일반적으로 AWS KMS, AWS Encryption SDK, S3 Encryption Client, DynamoDB Encryption Client 또는 기타 타사 암호화 도구나 서비스를 사용

- 암호화 방식에 따른 키 유형
    - 대칭 키(Symmetric Key)
        - 암호화와 복호화에 같은 키 사용 (AES-256, 3DES 또는 TDES)
    - 비대칭 키(Asymmetric Key)
        - 공개 키(Public Key)를 통해 암호화, 개인 키(Private Key)를 통해 복호화 (RSA, ECC)

- SSL/TLS
    - 클라이언트와 서버 간에 데이터의 무결성과 기밀성을 보장할 수 있는 암호화 프로토콜  
        → 상호 간의 통신은 암호화되어 전달되며, 중간에서 데이터를 탈취 당해도 안전 
    - SSL/TLS 핸드 셰이크 프로세스 
        1. Client Hello
            - 브라우저가 지원하는 SSL/TLS 버전 정보 
            - 브라우저가 지원하는 암호화 방식(Cipher Suites)
            - 클라이언트가 생성한 임의의 난수
            - 기타 
        2. Server Hello
            - 서버가 Cipher Suites 선택 
            - 서버의 공개 키가 포함된 SSL 인증서 전달 
            - 서버가 생성한 임의의 난수
            - 기타 
        3. 서버 인증서 확인 
        4. Premaster Secret 생성 및 전송
        5. Premaster Secret 복호화 
        6. 핸드 셰이크 종료 및 통신 시작

- SSL/TLS 인증서 
    - 서버의 신원을 확인하고, 클라이언트와 서버 간의 암호화된 통신을 보장하는 인증서

- AWS 관리형 및 고객 관리형 AWS KMS 키의 차이점
    - 제어 수준
        - 키 정책 및 권한 관리
        - 키 삭제 및 복제
    - 키 생성 및 저장 비용 발생 여부 

- 키 보호 
    - 키 암호화(Key Encryption)
    - 키 액세스 제어(Key Access Control)
    - 키 교체(Key Rotation)
    - 키 격리(Key Isolation)
    - 키 폐기(Key Deletion)
---

### 봉투 암호화(Evelope Encryption)

> [!NOTE]  
> `클라이언트 측 암호화`

![Image](https://github.com/user-attachments/assets/2ee43cff-85e5-4518-b96b-28f6d3d656c4)

- 봉투 암호화 과정 
    - 데이터 자체를 암/복호화하기 위한 **데이터 키(Data Key)** 발급 
         - `GenerateDataKey` API 호출 → 평문 데이터 키(Plaintext Data Key), 암호화된 데이터 키(Encrypted Data Key) 생성 
    - 생성된 평문 데이터 키를 사용하여 데이터 암호화 → 암호화된 데이터는 Ciphertext로 저장
        - `Encrypt` API 호출 → 평문 데이터를 평문 데이터 키로 암호화
    - 데이터 키를 **마스터 키(Master Key / CMK)** 로 암호화 
    - 암호화된 데이터(Ciphertext)와 암호화된 데이터 키(Encrypted data key)를 안전하게 저장

- 클라이언트 애플리케이션에서의 AWS KMS 기반의 봉투 암호화 
    - AWS Encryption SDK → 일반적인 애플리케이션에서 데이터를 안전하게 암호화하고 싶을 때 
    - AWS Database Encryption SDK → DynamoDB의 필드 단위 암호화를 구현하고 싶을 때 
    - Amazon S3 Encryption Client → 클라이언트 측에서 S3에 저장하는 데이터를 암호화하고 싶을 때 

### AWS Encryption SDK
- 데이터를 보호하기 위해 암호화 및 복호화 기능을 제공하는 오픈 소스 클라이언트 측 암호화 라이브러리
- 주요 프로그래밍 언어(C, .NET, Go, Java, JavaScript, Python, Rust, CLI)에서 구현 및 상호 운용성 지원 
- 핵심 기능 
    - 암호화 및 복호화 
        - 다양한 암호화 알고리즘 지원  
            → 기본적으로 봉투 암호화(Envelope Encryption) 방식을 사용
    - AWS KMS와 통합되어 암호화 키를 안전하게 관리
    - 키 캐싱 
        - 데이터를 암호화할 때마다 새로운 데이터 키를 `GenerateDataKey` API로 요청하는 대신, 이미 생성된 키를 재사용

### AWS KMS(Key Management Service)
> [!IMPORTANT]   
> KMS 키는 리전별로 생성 및 관리되며, 기본적으로 동일한 KMS 키는 두 리전에 존재할 수 없다. 

- 중앙 집중식 키 관리 → 단일 제어 지점(Single Point of Control)
- 높은 보안성 → FIPS 140-2 인증을 받은 HSM에 키 저장 및 보호
- 자동 키 로테이션(Automatic Key Rotation) 및 수명 주기 관리 
    - 고객 관리형 키(CMK)는 기본적으로 자동 키 로테이션이 비활성화되어 있음. (활성화 필요)
- AWS CloudTrail과 통합, API 요청 로깅을 통해 보안 감사 및 규정 준수 지원
- 대부분의 AWS의 서비스와 통합 (Amazon S3, EBS, RDS, Redshift, Lambda, CloudTrail 등)
    - S3 버킷이 SSE-KMS(AWS KMS 관리형 키)를 사용한 암호화를 설정하면, 객체를 저장하거나 검색할 때 AWS KMS 키에 대한 별도 권한이 필요

#### KMS 키 유형 (Master Keys)
- AWS 소유 키(AWS Owned Key)
    - AWS 서비스에서 자체 관리 → **사용자 액세스 제어 불가**
    - 비용: 무료 

- AWS 관리형 키(AWS Managed Key)
    - AWS가 관리하지만, 사용자가 생성하고 관리할 수 있는 키
    - 비용: 무료 

- 고객 관리형 키(Customer Managed Key)
    - 사용자가 직접 생성, 관리, 정책 설정
    - 비용: $1 / month

#### 암호화 및 복호화 관련 KMS API
- `Encrypt`	
    - `Encrypt` API 호출로 직접 암/복호화를 요청할 경우 원본 데이터의 사이즈는 4KB로 제한된다.  
        → <u>4KB를 초과하는 데이터의 암호화가 필요하다면 봉투 암호화(`GenerateDataKey` 호출)를 통해 암호화</u>
- `Decrypt`	
- `ReEncrypt`	
- `GenerateDataKey`	
    - 평문 데이터 키(Plaintext Data Key) + 암호화된 데이터 키(Encrypted Data Key) 생성
- `GenerateDataKeyWithoutPlaintext`	
    - 암호화된 데이터 키만 생성 (평문 데이터 키는 반환 ❌)
- `GenerateRandom`

#### KMS Key Policies
- KMS 키에 대한 액세스를 제어하는데 사용되는 정책
- 정책 유형 
    - **기본 KMS 키 정책(Default Key Policy)**
        ```json 
        {
            "Sid": "Enable IAM User Permissions",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::111122223333:root"
            },
            "Action": "kms:*",
            "Resource": "*"
        }
        ```

        - KMS 키 생성 시 사용자 지정 키 정책을 명시하지 않으면, 기본 키 정책을 자동으로 적용  
            → AWS 계정의 모든 IAM 주체가 모든 KMS 작업을 수행할 수 있도록 전체 액세스 권한을 부여

    - **사용자 지정 키 정책(Custom Key Policy)**
        - 사용자가 직접 설정하여 세부적으로 설정하는 키 정책
        - KMS 키의 교차 계정 액세스 시 유용
        - 다른 계정이 KMS 키를 사용하도록 권한 부여 
            - 계정간 스냅샷 복사

#### 다중 리전 키(Multi-Region Keys, MRK)
- 여러 리전에서 동일한 암호화 키를 사용할 수 있도록, 한 리전의 기본 키(primary key)를 다른 리전으로 복제하여 사용할 수 있는 키 
    - 다중 리전 키는 전역 키가 아니며, 각 리전에서 독립적으로 관리되어야 한다. (정책)
    - 다중 리전 키(replica keys)는 동일한 키 ID와 동일한 키 구성 요소를 갖는다.  
        → 한 리전에서 암호화한 다음 다른 리전에서 복호화 가능
    - 키 복제 
        1. AWS KMS Console 또는 AWS KMS API를 통해 다중 리전 기본 키 생성
        2. 리전별 복제 키 생성 
        
- 사용 사례 
    - 재해 복구
    - 글로벌 데이터 관리
        - 전역 클라이언트 측 암호화
        - DynamoDB 전역 테이블 암호화
    - 분산 서명 애플리케이션
    - 다중 리전 액티브-액티브 애플리케이션

### AWS CloudHSM(Hardware Security Module)
> [!IMPORTANT]   
> AWS에서 하드웨어 보안 모듈을 제공, 운영 및 보안 관리는 고객이 직접 수행한다. 

- HSM 내부에서 자체적으로 사용자 및 그룹을 관리 → **IAM을 통한 액세스 제어 불가**
- FIPS 140-2 레벨 3 인증을 받은 HSM을 사용하여 암호화
- VPC 내에 배포되어 네트워크를 통해 액세스하며, VPC Peering을 사용하여 여러 VPC 간의 암호화 키 공유 가능

#### CloudHSM 키 유형 

- 대칭키(Symmetric Key)
- 비대칭키(Asymmetric Key)
- 디지털 서명 및 해싱(Digital Signing & Hashing)
    
#### CloudHSM Client 

- AWS CloudHSM 서비스를 사용하여 HSM 인스턴스와 상호작용하는 데 필요한 소프트웨어 클라이언트 (리눅스 및 윈도우 환경에서 설치 가능)
- 주요 기능
    - AWS CloudHSM 서비스와 SSL/TLS 연결을 설정
    - 암호화 키를 생성, 저장, 사용, 삭제

### AWS Certificate Manager(ACM)
> 웹사이트에 대한 HTTPS 연결 설정

- AWS에서 SSL/TLS 인증서를 쉽게 프로비저닝, 관리, 배포하는 서비스
- 공용 TLS 인증서(무료) 및 사설 TLS 인증서를 모두 지원
- 주요 기능
    - 발급된 인증서 자동 갱신 
    - AWS 리소스(ex: ELB, CloudFront, API Gateway 등)와 통합하여 인증서 배포 

### AWS Private Certificate Authority(Private CA)
> 내부 애플리케이션, 프라이빗 네트워크, IoT 장치 등에서 사용하는 사설 인증서 관리
- AWS에서 사설 SSL/TLS 인증서를 쉽게 프로비저닝, 관리, 배포하는 서비스
- AWS Certificate Manager(ACM)과 통합하여 관리 가능 

## 2.3 애플리케이션 코드에서 민감한 데이터를 관리합니다.
---
#### Knowledge of:
- 데이터 분류 
    - 중요도와 민감도를 기준으로 네트워크의 데이터를 식별하고 분류하는 프로세스
    - [[참고] 데이터 분류 모델 및 체계](https://docs.aws.amazon.com/whitepapers/latest/data-classification/data-classification-models-and-schemes.html)
        - 정부 분류 체계(government classification schemes)  
            → 법률, 정책 및 행정 지침에 따라 설정된 표준 제공 
        - 상업적 분류 체계(commercial classification schemes)

- 민감 데이터 
    > [!NOTE]  
    > AWS Macie를 통해 민감 데이터를 감지하고, AWS Glue를 통해 변환하거나 안전하게 처리할 수 있다. 

    - 자격증명(Credentials): AWS Secret Access Key, JWT, HTTP 인증 헤더 등
    - 금융정보: 계좌 번호, 신용 카드 번호 등
    - 개인건강정보(PHI): 미국의 개인 건강 정보 및 특정 국가의 의료 관련 정보 
    - 개인식별정보(PII): 여권 번호, 운전면허 번호, 전화 번호, HTTP 쿠키 등
--- 

### AWS Secrets Manager  
> [!NOTE]  
> 기본적으로 단일 리전에서만 관리하지만, 다중 리전 복제를 통한 공유 가능 

- <u>보안이 필요한 비밀정보(secrets)</u>를 안전하게 관리하는 서비스
    - 데이터베이스 자격 증명
    - API 키
    - OAuth 토큰
    - SSH 키
    - TLS/SSL 인증서 및 개인 키
    - 일반 텍스트 또는 JSON 형식의 기타 민감한 정보 

- 주요 기능
    - AWS KMS를 통한 비밀 자동 암호화
    - AWS IAM 기반의 세분화된 액세스 제어 
    - AWS CloudTrail & CloudWatch Log와 통합 → 감사 및 모니터링 
    - 비밀 정보 버전 관리 (업데이트할 때마다 버전 생성, 변경 내역 추적 및 롤백 가능)
    - 자동화된 암호 교체 
    - 다중 리전 비밀정보 복제(Multi-Region Secret Replication)  
        → Primary Secret와 복제본을 지속적으로 동기화 

- 사용 사례 
    - 사용자 지정 Lambda 함수를 활용한 Amazon RDS 비밀번호 관리 자동화

### AWS Systems Manager Parameter Store
- <u>애플리케이션의 환경 변수나 애플리케이션 설정값과 같은 구성 데이터</u>를 저장하는 서버리스 서비스 
- **리전 내 여러 가용 영역(AZ)** 에서 호스팅되기 때문에 파라미터를 안정적으로 저장 

- 주요 기능
    - AWS KMS를 통한 **선택적** 암호화
    - AWS IAM 기반의 세분화된 액세스 제어 
    - 파라미터를 저장소에 계층 구조(hierarchy)로 저장
    - 파라미터 버전 관리 (업데이트할 때마다 버전 생성, 변경 내역 추적 및 롤백 가능)

- 사용 사례 
    - 애플리케이션의 설정 값(데이터베이스 URL, API 키 등)을 파라미터로 저장, 동적으로 로드 (하드코딩 방지)
    - 여러 환경(dev, test, prod 등)에 대한 맞춤 구성 관리
    - 자동화된 배포 프로세스에서 최신 구성 정보를 자동 반영

#### Parameter Store Tiers 

| 티어 | 총 파라미터 개수 제한 <br/> (per AWS account & region) | 최대 크기 | 파라미터 정책 | 비용 | 
|-----|---------|---------|---------|---| 
| **Standard** | 10,000 | 4KB | 불가능 | 무료 |
| **Advanced** | 100,000 | 8KB | 가능 | $0.05/parameter/month

#### Parameters Policies (for Advanced)
- 파라미터 집합을 관리하는데 사용되는 정책
- 파라미터 당 최대 10개의 정책 할당 가능
- 정책 유형
    - `Expiration` (파라미터의 만료 날짜 설정)
        > 만료 날짜와 시간에 도달하면 Parameter Store에서 파라미터를 삭제
        ```json 
        {
            "Type": "Expiration",
            "Version": "1.0",
            "Attributes": {
                "Timestamp": "2018-12-02T21:34:33.000Z"
            }
        }
        ```
    - `ExpirationNotification` (만료 전 알림 설정)
        > 만료 전 Amazon EventBridge 이벤트를 시작
        ```json 
        {
            "Type": "ExpirationNotification",
            "Version": "1.0",
            "Attributes": {
                "Before": "15",
                "Unit": "Days"
            }
        }
        ```

    - `NoChangeNotification` (파라미터 미갱신 알림 설정)
        >  지정된 기간 동안 파라미터가 수정되지 않은 경우 Amazon EventBridge 이벤트를 시작
        ```json 
        {
            "Type": "NoChangeNotification",
            "Version": "1.0",
            "Attributes": {
                "Before": "20",
                "Unit": "Days"
            }
        }
        ```

### AWS Nitro Enclaves
- 클라우드에서 아주 민감한 데이터(ex: PHI, PII)를 처리해야 할 경우, 독립적으로 **격리된 가상 환경(VM)** 을 제공하는 서비스 
