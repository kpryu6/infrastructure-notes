# Pod 배포 중심 k8s 구성 요소



## k8s 구성 요소 간 통신




## 오브젝트란

- 파드 (Pod)
  - 쿠버네티스에서 실행되는 최소 단위
  - 1개 이상의 컨테이너로 단일 목적의 일을 하기 위해 모인 단위
    - ex) 웹 서버
  - 언제라도 죽을 수 있음
  
  <파드와 컨테이너의 관계 그림>
  
- 네임스페이스 (Namespace)
  - 쿠버네티스 클러스터에서 사용되는 리소스들을 구분해 관리하는 그룹
  - default, kube-system, metallb-system
  
- 볼륨 (Volume)
  - 파드가 생성될 때 파드에서 사용할 수 있는 디렉토리 제공
  - 파드가 죽어도 저장과 보존이 가능한 디렉토리 제공 가능
  
- 서비스 (Service)
  - 새로 파드가 생성될 때 부여되는 새로운 IP를 기존에 제공하던 기능과 연결하는 것
  - 즉, k8s 외부에서 내부로 접속할 때 내부의 상황을 몰라도 논리적으로 연결하는 것
  
- 디플로이먼트 (Deployment)
  - 
  
---

# Why Kubernetes?

**what if**
- `하나의 운영체제에 도커를 올려 컨테이너 관리` $\Rightarrow$ `효율적`
- $\Rightarrow$ But, 시스템 무너지면 끝 $\Rightarrow$ 노드를 하나 더 만듦
- 노드가 증가하면 관리가 어려워짐

## 컨테이너 오케스트레이션
- 노드들을 관리하는 마스터 노드를 만듦 `마스터 노드 = Control Plane`