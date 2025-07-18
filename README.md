# company-infra-c (EFK)

회사/팀의 **EFK**을 **Kubernetes 기반 Helm Chart & GitOps(CI/CD)** 로 자동화 관리하는 프로젝트입니다

## 개요
- company-infra 내에  있던 다양한 서버 들을  EFK 로 받아와  배포하며 Name space를 분리해 관리를 용이하게 만들 엇습니다.
- **ArgoCD** 선언적으로 Git Ops 자동배포
- **Jenkins** 이미지 빌드 자동화 helm chart 템플릿 관리
- **EFK** `default` **네임스페이스** 에 자동 배포 됩니다.
- 실제 YAML/Helm Chart 파일은 [여기](https://github.com/wlals2/company-infra-finish-c/tree/main/templates)에서 확인할 수 있습니다.

## 주요 기술스택

- **Kubernetes**
- **Helm** (Chart, values.yaml, manifest 템플릿)
- **Jenkins** (CI: Docker 이미지 빌드 및 레포 등록)
- **ArgoCD** (CD: GitOps, Helm repo, 자동 배포)
- **Docker**
- **Linux**
- (기타: EFK Stack, 기타 오픈소스 서비스 등)
- **EFK**

## 폴더/파일 구조
```
~/test/company-infra-c/
├─ tmemplates/
│   ├─ Elaistcsearch/
│   ├─ Fluentbit/
│   ├─ Kibana/
├─ charts/                    
├─ values.yaml
├─ Chart.yaml
├─ helm-chart
```
## 자동화 배포 흐름

1. **Jenkins**  
   - Docker 이미지 빌드 & registry push  
   - Helm Chart 소스 GitHub에 커밋/푸시
2. **ArgoCD**  
   - GitOps 기반, Helm Chart(혹은 values.yaml) 변경 감지 시 자동 배포  
   - Helm repo를 통한 Chart 설치 및 배포 관리
3. **Kubernetes**  
   - company-infra 네임스페이스에서 각 서비스가 자동 배포 및 운영
   - EFK는 default 네임스페이스에서 별도 운영

## 설치 및 사용 방법

> **본 프로젝트는 완전 자동화(ArgoCD + Jenkins)되어 있으므로, 기본적으로 직접 kubectl, helm 명령어를 사용할 필요가 없습니다.**

### 1. 선행 조건

- Kubernetes 클러스터 (네임스페이스: `company-infra`)
- ArgoCD, Jenkins, Docker 설치/연동
- 필요한 시크릿, PVC 등 사전 준비

### 2. 배포 흐름

- **Jenkins**:  
  - 코드/이미지 변경시 자동 빌드 & 이미지 registry push
  - Helm Chart/template 수정시 GitHub에 자동 push
- **ArgoCD**:  
  - 변경사항 감지 시 자동으로 Helm Chart 기반 배포
  - (Helm repo로 관리하는 경우 helm install/upgrade 자동화)

#### 트러블 슈팅 및 서버 내에 설정 중에 EFK  내려가면 설정 내용이 내려 갈 수 있기 때문에 company-infra 트러블 슈팅에는 방해 안되게 default 또는 다른 네임 스페이스 에 배포
