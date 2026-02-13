# ECS (Elastic Container Service)

## 한 줄 요약
Docker 컨테이너를 실행하고 관리하는 AWS 서비스

## 비유로 이해하기
- **EC2**: 가상 컴퓨터 한 대 (Windows나 Linux가 설치된 서버)
- **ECS**: 컨테이너 관리자 (Docker 컨테이너들을 돌리는 플랫폼)

## 핵심 개념
1. **Task Definition**: 레시피 (어떤 Docker 이미지를 사용할지, 메모리는 얼마나 필요한지 등)
2. **Task**: 실제 실행 중인 컨테이너 (레시피를 보고 만든 요리)
3. **Service**: 요리사 (레시피를 보고 Task를 계속 만들어내고, 죽으면 다시 만듦)
4. **Cluster**: 주방 (Task들이 실행되는 논리적 공간)

<br/>

## 개념 및 관계도

### 다이어그램

```mermaid
%%{init: {'theme':'neutral'}}%%
graph TB
    subgraph Cluster["🏢 Cluster (주방)"]
        subgraph Service["👨‍🍳 Service (요리사)"]
            Task1["📦 Task 1 (요리1)<br/>(실행 중)"]
            Task2["📦 Task 2 (요리2)<br/>(실행 중)"]
            Task3["📦 Task 3 (요리3)<br/>(실행 중)"]
        end
        
        StandaloneTask["📦 Standalone Task<br/>(일회성)"]
    end
    
    TaskDef["📋 Task Definition<br/>(레시피, 템플릿)"]
    
    subgraph TaskDetail["Task 상세 구조"]
        Container1["🐳 Container 1<br/>(nginx)"]
        Container2["🐳 Container 2<br/>(redis)"]
        Container1 <--> Container2
    end
    
    TaskDef -->|"기반으로 생성"| Task1
    TaskDef -->|"기반으로 생성"| Task2
    TaskDef -->|"기반으로 생성"| Task3
    TaskDef -->|"기반으로 생성"| StandaloneTask
    
    Task1 -.->|"내부 구조"| TaskDetail
    
    style Cluster fill:#b3d9ff,stroke:#0066cc,stroke-width:3px
    style Service fill:#ffd699,stroke:#cc6600,stroke-width:2px
    style TaskDef fill:#d9b3ff,stroke:#6600cc,stroke-width:2px
    style TaskDetail fill:#b3ffb3,stroke:#009900,stroke-width:2px
```

**설명:**
- **Cluster (주방)**: 모든 리소스를 담는 논리적 그룹
- **Service (요리사)**: Task Definition(레시피)을 보고 Task를 계속 만들어냄, Desired Count 유지, 자동 재시작
- **Task Definition (레시피)**: Task 생성을 위한 템플릿
- **Task (요리)**: Task Definition을 기반으로 생성된 실제 실행 인스턴스
- **Standalone Task**: Service 없이 직접 실행하는 일회성 작업
- **Container**: Task 안에서 실행되는 Docker 컨테이너들

### 관계 요약
1. **Cluster** 안에 **Service**와 **Task**가 실행됨
2. **Task Definition** (템플릿)을 기반으로 **Task** (실제 실행)가 생성됨
3. **Service**는 여러 **Task**를 관리하고 개수 유지
4. **Task**는 1개 이상의 **Container**로 구성됨
5. Standalone **Task**는 Service 없이 일회성으로 직접 실행 가능

### 생성 순서

```mermaid
%%{init: {'theme':'neutral'}}%%
flowchart TD
    Start([시작]) --> CreateCluster[1. Cluster 생성]
    CreateCluster --> CreateTaskDef[2. Task Definition 작성<br/>레시피]
    CreateTaskDef --> Choice{실행 방식 선택}
    
    Choice -->|장기 실행| CreateService[3-a. Service 생성]
    CreateService --> ServiceManage[Service가 Task<br/>자동 생성 및 관리]
    
    Choice -->|일회성| RunTask[3-b. Run Task 실행]
    RunTask --> TaskRun[Task 즉시 실행]
    
    style Start fill:#cce5ff,stroke:#0066cc
    style CreateCluster fill:#ffd699,stroke:#cc6600
    style CreateTaskDef fill:#d9b3ff,stroke:#6600cc
    style Choice fill:#ffff99,stroke:#cc9900
    style CreateService fill:#b3ffb3,stroke:#009900
    style RunTask fill:#ffb3d9,stroke:#cc0066
```

**각 단계 바로가기:**
- [1. Cluster 생성](#생성-방법-aws-console)
- [2. Task Definition 작성](#생성-방법-1)
- [3-a. Service 생성](#생성-방법-2)
- [3-b. Task 직접 실행](#task)
<br/>

## 왜 사용하나?
- Docker 컨테이너를 수동으로 관리하지 않아도 됨
- 컨테이너가 죽으면 자동으로 재시작
- 로드밸런서, 오토스케일링 쉽게 연동
- Fargate 사용 시 서버 관리 없이 컨테이너만 실행 가능
