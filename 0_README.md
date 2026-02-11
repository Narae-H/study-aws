이 저장소는 AWS를 학습하면서 정리한 내용을 기록한 것입니다. 
 기초 개념부터 실습, 서비스별 사용 방법까지 정리하고 있으며, 각 항목은 마크다운 파일로 나누어 구성되어 있습니다. 

# 목차
## 💻 EC2 (Elastic Compute Cloud)
- [1. Instances](./ec2/1_instances.md)  
  인스턴스 생성, 타입, 템플릿, Spot, RI, Savings Plans 등  
- [2. Images (AMI)](./ec2/2_images.md)  
  AMI 개념, 사용자 정의 이미지, AMI Catalog 등  
- [3. Elastic Block Store (EBS)](./ec2/3_elastic_block_store.md)  
  볼륨, 스냅샷, 라이프사이클 매니저  
- [4. Network](./ec2/4_network.md)  
  Elastic IPs, Placement Groups, Network Interfaces
- [5. Network](./ec2/5_security.md)  
  Security Groups, Key Pairs  
- [6. Load Balancing](./ec2/5_load_balancing.md)  
  로드 밸런서 유형, 타겟 그룹, Trust Store  
- [7. Auto Scaling](./ec2/6_auto_scaling.md)  
  Auto Scaling Groups 개념 및 설정
<br/>

## ECS (Amazon Elastic Container Service)
- [1. Clusters](./ecs/1_clusters.md)
  클러스터, 서비스, 타스크 생성 등

# 📝 정리 기준
- **서비스별로 파일 분리**하여 구조화
- **공식 문서 요약 + 실습 기반 정리**
- 직접 실습하며 이해한 내용을 중심으로 서술
- ⚠️ AWS는 자주 바뀌므로 최신 문서는 [AWS 공식 문서](https://docs.aws.amazon.com/) 참고하기
<br/>

# 📚 참고 자료
- [AWS 공식 문서](https://docs.aws.amazon.com/)
- [AWS Skill Builder](https://skillbuilder.aws/)