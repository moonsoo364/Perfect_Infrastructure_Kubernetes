#  쿠버네티스 노드에 label 할당

노드 상태 확인
```
kubectl get node
```
노드에 라벨 할당
```
kubectl label node ${node_id} server=webap
```
노드에 라벨이 할당되었는 지 확인
```
kubectl get node --show-labels
```

# 포드를 특정 노드에 할당하여 실행 

작성된 메니피스트 파일을 실행
```
kubectl create -f Pod/labels-node.yaml
```
클러스터 안에 노드 확인
```
kubectl get pod --ouput=wide
```
확인이 끝났으면 포드 삭제
```
kubectl delete -f Pod/labels-node.yaml
```