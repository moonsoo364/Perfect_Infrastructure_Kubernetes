# Azure를 이용한 쿠버네티스 입문 실습
- 참고 도서 : [완벽한 IT 인프라 구축의 자동화를 위한 Kubertes 실습](https://product.kyobobook.co.kr/detail/S000000833240)
- 저자 : Asa Shinho
- 간략 내용 : Microsoft Azure를 이용한 K8S 실습 및 K8S의 핵심 개념 설명

# 작업 이력
- 250920 :환경 설정 (Azure CLI, Kebectl)
- 250921 : 리소스 그룹 및 ACR, AKS 자원 생성 명령어 실습

# 핵심 명령어 정리
## Resource Group
- Azure에서 사용하는 **리소스(가상머신, 스토리지, 네트워크, AKS 등)**를 논리적으로 묶어 관리하는 그룹이다.
- 권한 관리, 비용 관리, 리소스 정리 시 그룹별로 나누면 관리하기 용이하다.
### RG 명령어
리소스 그룹 생성
```bash
az group create --resource-group $ACR_RES_GROUP --location koreacentral
```
리소스 그룹 조회

```bash
az group show --name $ACR_RES_GRO
```
Register 등록 및 조회
```bash
az provider register --namespace Microsoft.ContainerRegistry
az provider show -n Microsoft.ContainerRegistry

```
## ACR 
ACR(Azure Container Registry) 
- Docker 호환 프라이빗 컨테이너 이미지 레지스트리 서비스
- 컨테이너 실행에 필요한 애플리케이션 이미지와 OCI 아티팩트를 저장, 관리, 배포할 수 있음
### ACR 명령어
ACR 생성

```bash
az acr create --resource-group $ACR_RES_GROUP --name $ACR_NAME --sku Standard --location koreacentral
```

acr 조회

```bash
az acr show --name $ACR_NAME --resource-group $ACR_RES_GROUP
```
acr 삭제

```bash
az acr delete --name $ACR_NAME --resource-group $ACR_RES_GROUP --yes
```
컨테이너 이미지 acr에 푸시

```bash
git clone https://github.com/ToruMakabe/Understanding-K8s
cd ./Understanding-K8s/chap02/
```

Azure 웹 에서  계정 결제 가능(pay as you go)로 변경 후 아래 명령어 실행 

```bash
az acr build --registry $ACR_NAME --image photo-view:v1.0 v1.0/
```

컨테이너 이미지 조회
```bash
az acr repository show-tags -n $ACR_NAME --repository photo-view
```
## 