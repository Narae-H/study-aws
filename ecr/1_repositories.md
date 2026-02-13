
## ECR (Elastic Container Registry)

### 개념
- AWS에서 제공하는 완전 관리형 Docker 컨테이너 레지스트리
- Docker 이미지를 저장, 관리, 배포함
- ECS Task Definition에서 ECR 이미지 참조 가능
- Private repository로 접근 제어 가능

### 사용 방법

#### Naming Convention (MSA 구조 예시)

**ECR Repository 이름:**
- 형식: `{project}/{service}`
- 예시: `myproject/user-service`, `myproject/order-service`
- 규칙:
  - 소문자만 사용
  - 슬래시(`/`)로 프로젝트와 서비스 구분
  - 환경별 분리 불필요 (태그로 구분)

**Image Tag:**
- **Semantic Versioning**: `v1.0.0`, `v1.2.3`
- **Git SHA**: `abc1234` (짧은 commit hash)
- **환경 + 버전**: `stg-v1.0.0`, `prod-v1.0.0`
- **날짜 + 버전**: `20240115-v1.0.0`

**ECR 구조 예시:**
```
123456789.dkr.ecr.ap-northeast-2.amazonaws.com/
├── myproject/user-service:v1.0.0
├── myproject/user-service:v1.1.0
├── myproject/order-service:v2.0.0
└── myproject/payment-service:v1.5.0
```

#### ECR Repository 생성 및 이미지 푸시
- AWS Console에서 ECR 서비스 접속
- **Create repository** 클릭
- Repository 이름 입력 (예: `myproject/user-service`)
- 로컬에서 Docker 이미지 빌드
- ECR에 로그인 후 이미지 푸시

#### Task Definition에서 ECR 이미지 사용
- Task Definition 생성 시 Image URI에 ECR 이미지 경로 입력
- 형식: `123456789.dkr.ecr.ap-northeast-2.amazonaws.com/myproject/user-service:v1.0.0`

<br/>
