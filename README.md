## FastAPI와 SQLite3를 이용한 과제 구현
### 1. 기술 스택 및 사용 도구

- **언어 및 프레임워크**: Python, FastAPI
- **데이터베이스**: SQLite3
- **인프라 도구**:
  - Docker
  - Kubernetes (Minikube)
  - Helm
  - Terraform

### 2. 프로젝트 구조
- **API Repository**
```
infra_project_API/
├── api/               
│   ├── __init__.py           
│   ├── models.py 
│   ├── schemas.py
│   ├── database.py
│   └── crud.py
├── db/                       
│   └── test.db 
├── main.py 
├── Dockerfile
├── requirements.txt
└── README.md 
```
- **Infra Repository**
```
infra_project_INFRA/
├── terraform/                    
│   ├── main.tf                   
│   ├── terraform.tfstate              
│   └── terraform.tfstate.backup
├── helm/
│   └── api-project/
│       ├── Chart.yaml 
│       ├── values.yaml 
│       └── templates/         
│           ├── deployment.yaml   
│           ├── service.yaml      
│           └── ...               
└ ── k8s/
    └── deployment.yaml
    └── service.yaml
```

### 3. 인프라 구성도
![onealog](https://github.com/aidenyoun/infra_project_INFRA/blob/main/images/infra_diagram.png?raw=true) 

- Client: 사용자가 Kubernetes 클러스터 외부에서 API 요청을 보냅니다.
  - Kubernetes Service: 클러스터 내에서 API 서버로 트래픽을 라우팅합니다.
  - API 서버 (FastAPI + SQLite3): 요청을 처리하고 SQLite3 데이터베이스에 저장하거나 데이터를 반환합니다.
- Developer: Docker, Helm, Terraform을 사용하여 애플리케이션 및 인프라를 Kubernetes 클러스터에 배포합니다.

### 4. 구축 완료 보고
1. Docker 이미지 생성
- PyCharm 터미널에서 Minikube 환경을 설정한 후, Docker를 사용해 FastAPI 애플리케이션 이미지를 빌드하였습니다.
![docker](https://github.com/aidenyoun/infra_project_INFRA/blob/main/images/create_docker_image.png?raw=true) 

2. Helm
- Helm을 통해 Kubernetes Cluster에 배포하고자 했습니다. 그 후 kubectl 
get pods을 통해 Pod 상태를 확인했습니다.
![helm](https://github.com/aidenyoun/infra_project_INFRA/blob/main/images/helm.png?raw=true) 

3. Terraform
- Kubernetes 클러스터 내에 필요한 리소스들을 Terraform을 통해 관리하고자 했습니다. Minikube를 사용했습니다.
![Terraform](https://github.com/aidenyoun/infra_project_INFRA/blob/main/images/terraform_re.png?raw=true)

4. Kubernetes 리소스 상태 확인
- kubectl get all 명령어로 정상 작동을 확인했습니다.
![k8s](https://github.com/aidenyoun/infra_project_INFRA/blob/main/images/kubectl.png?raw=true) 

5. 포트 포워딩을 통한 접근
- Pod 내부의 80번 포트를 로컬의 8000번 포트로 포워딩했습니다.
![port](https://github.com/aidenyoun/infra_project_INFRA/blob/main/images/portfowarding.png?raw=true) 

### 5. API 작동 확인
  - Health Check
![health](https://github.com/aidenyoun/infra_project_INFRA/blob/main/images/API/API_Health.png?raw=true) 

  - Create
![Create](https://github.com/aidenyoun/infra_project_INFRA/blob/main/images/API/API_CREATE.png?raw=true) 

  - Read
![Read](https://github.com/aidenyoun/infra_project_INFRA/blob/main/images/API/API_READ.png?raw=true) 

  - Update
![Update](https://github.com/aidenyoun/infra_project_INFRA/blob/main/images/API/API_UPDATE.png?raw=true) 

  - Delete
![Delete](https://github.com/aidenyoun/infra_project_INFRA/blob/main/images/API/API_DELETE.png?raw=true) 


