# docker

```
[image for EKS]

docker build -t aws-repo .
docker build -t aws-bastion .
docker build -t aws-ubuntu-repo .

docker build --platform linux/amd64 -t aws-repo .
docker build --platform linux/amd64 -t aws-ubuntu-repo .
docker build --platform linux/amd64 -t amazonlinux-chrony .
docker build --platform linux/amd64 -t aws-bastion .
docker build --platform linux/amd64 -t 123.dkr.ecr.ap-northeast-2.amazonaws.com/amazonlinux-chrony .


[save, load]

docker save amazonlinux-chrony -o amazonlinux-chrony.tar
docker save aws-repo -o aws-repo.tar
docker save aws-ubuntu-repo -o aws-ubuntu-repo.tar
docker save aws-bastion -o aws-bastion.tar


docker load -i amazonlinux-chrony.tar
docker load -i amazonlinux-chrony.tar
docker load -i aws-bastion.tar


docker run -d --name repo aws-repo
docker run -d --name ubuntu aws-ubuntu-repo
docker run -d --name aws-bastion aws-bastion


aws ecr get-login-password --region ap-northeast-2 | docker login --username AWS --password-stdin 915921166046.dkr.ecr.ap-northeast-2.amazonaws.com


aws ecr get-login-password --region ap-northeast-2 | docker login --username AWS --password-stdin 915921166046.dkr.ecr.ap-northeast-2.amazonaws.com

docker tag aws-ubuntu-repo:latest 915921166046.dkr.ecr.ap-northeast-2.amazonaws.com/aws-ubuntu-repo:latest


aws ecr create-repository --repository-name amazonlinux-chrony --region ap-northeast-2
docker tag amazonlinux-chrony:latest 915921166046.dkr.ecr.ap-northeast-2.amazonaws.com/amazonlinux-chrony:latest
docker push 915921166046.dkr.ecr.ap-northeast-2.amazonaws.com/amazonlinux-chrony:latest


aws ecr create-repository --repository-name aws-repo --region ap-northeast-2
docker tag aws-repo:latest 915921166046.dkr.ecr.ap-northeast-2.amazonaws.com/aws-repo:latest
docker push 915921166046.dkr.ecr.ap-northeast-2.amazonaws.com/aws-repo:latest


[docker-compose]
https://docs.docker.com/compose/install/standalone/

mv docker-compose-linux-aarch64 /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
chown root:root docker-compose


[docker]
usermod -aG docker bithumb_lab
usermod -aG docker devops


[change subnet]
vi /etc/docker/daemon.json 


{
  "default-address-pools": [
    {
      "base": "192.168.44.0/24",
      "size": 24
    }
  ]
}

systemctl restart docker

docker inspect 

docker inspect bridge
```

# EKS
 
```
kubectl exec -it repo-deployment-5bdc58f69-wdl4g -c rocky-repo-container -n repo -- /bin/bash
kubectl exec -it repo-deployment-5bdc58f69-wdl4g -c ubuntu-repo-container -n repo -- /bin/bash

curl -v http://localhost/rocky/appstream-8/repodata/repomd.xml



kubectl rollout restart deployment repo-deployment -n repo


kubectl describe pod aws-bastion-0 -n aws-bastion
kubectl describe svc chrony-service -n chrony



kubectl logs -f --tail=100 repo-deployment-6b8dcff754-hwhvk -n repo
kubectl logs repo-deployment-db7f75784-n5462 -c ubuntu-repo-container -n repo
kubectl logs repo-deployment-db7f75784-n5462 -c rocky-repo-container -n repo

kubectl logs repo-deployment-6b8dcff754-hwhvk -n repo



kubectl scale statefulsets aws-bastion --replicas=1 -n aws-bastion
kubectl scale statefulsets aws-bastion --replicas=0 -n aws-bastion



kubectl get pods -n aws-bastion --watch


kubectl set env daemonset/aws-node -n kube-system ANNOTATE_POD_IP=false


echo -n | timeout 1 bash -c "</dev/tcp/10.20.101.71/22" && echo "Port 22 is Open" || "Port 22 is Closed"
echo -n | timeout 1 bash -c "</dev/tcp/172.20.37.170/443" && echo "Port 443 is Open" || "Port 443 is Closed"
echo -n | timeout 1 bash -c "</dev/tcp/ftp.kaist.ac.kr/443" && echo "Port 443 is Open" || "Port 443 is Closed"
echo -n | timeout 1 bash -c "</dev/tcp/ftp.kaist.ac.kr/443" && echo "Port is Open" || "Port is Closed"
echo -n | timeout 1 bash -c "</dev/tcp/localhost/22" && echo "Port 22 is Open" || "Port 22 is Closed"
echo -n | timeout 1 bash -c "</dev/tcp/kr.archive.ubuntu.com/80" && echo "Port is Open" || "Port is Closed"



curl http://kr.archive.ubuntu.com

curl https://ftp.kaist.ac.kr/pub/rocky/9/AppStream/aarch64/kickstart/repodata/repomd.xml


debmirror --verbose \
  --method=http \
  --host=kr.archive.ubuntu.com \
  --root=ubuntu \
  --dist=jammy \
  --section=main,restricted,universe,multiverse \
  --arch=amd64 \
  --nosource \
  --ignore-release-gpg \
  /data/ubuntu



Index of /pub/rocky/8/AppStream/x86_64/os/repodata/


kubectl patch pvc repo-pvc -n repo --type='merge' -p '{"spec": {"resources": {"requests": {"storage": "1Ti"}}}}'


https://ftp.kaist.ac.kr/pub/rocky/8/AppStream/x86_64/os/repodata/repomd.xml
https://ftp.kaist.ac.kr/pub/rocky/8/AppStream/aarch64/os/repodata/repomd.xml 

https://ftp.kaist.ac.kr/pub/rocky/9/AppStream/x86_64/os/repodata/repomd.xml
https://ftp.kaist.ac.kr/pub/rocky/9/AppStream/aarch64/os/repodata/repomd.xml 


[Upgrade]


kubectl exec -it kibana-66764b9879-fv8f2 -n default -- /bin/bash
kubectl exec -it aws-bastion-0 -n repo -- /bin/bash
kubectl exec -it chrony-deployment-6f99f884d8-ffsbf -n chrony -- /bin/bash
kubectl logs -f repo-deployment-86865bc9b4-gs79v  -n repo -c ubuntu-repo-container
kubectl exec -it repo-deployment-7cb9b6bbb-8rpvr  -n repo -c ubuntu-repo-container -- /bin/bash
kubectl exec -it repo-deployment-7cb9b6bbb-8rpvr   -n repo -c rocky-repo-container -- /bin/bash
kubectl exec -it repo-deployment-7cb9b6bbb-jhwlt -n repo -c ubuntu-repo-container -- /bin/bash
kubectl exec -it repo-deployment-79665665d4-jtr5w  -n repo -c rocky-repo-container -- /bin/bash

kubectl describe nodes | grep -A5 "node.kubernetes.io/memory-pressure"

kubectl uncordon ip-172-20-162-158.ap-northeast-2.compute.internal




kubectl drain ip-172-20-162-199.ap-northeast-2.compute.internal --ignore-daemonsets --delete-emptydir-data
kubectl drain ip-172-20-165-88.ap-northeast-2.compute.internal --ignore-daemonsets --delete-emptydir-data




ip-172-20-160-158.ap-northeast-2.compute.internal
ip-172-20-167-230.ap-northeast-2.compute.internal




kubectl get statefulset


kubectl rollout status statefulset/elasticsearch-ingest -n default



kubectl rollout restart statefulset elasticsearch-data -n default

kubectl get pods -o wide --watch | grep elasticsearch-data

kubectl rollout restart statefulset elasticsearch-coordinating -n default

kubectl get pods -o wide --watch | grep coordinating

kubectl rollout restart statefulset elasticsearch-ingest -n default

kubectl get pods -o wide --watch | grep elasticsearch-ingest


kubectl rollout restart statefulset elasticsearch-master -n default

kubectl get pods -o wide --watch | grep elasticsearch-master


kubectl rollout restart deploy kibana -n default

kubectl get pods -o wide --watch | grep kibana


kubectl get pods -A -o wide --watch | grep elasticsearch-data
watch -n 5 "kubectl top nodes| grep 112"




kubectl edit 
 istiod -n istio-system




aws-dev-eks-es-cloudflare cluster
NodeGroup BOTTLEROCKET_x86_64으로 전환했습니다.



공통적으로 업그레이드 해도 daemonsets 남아있음

[devops eks]

argocd

istio

node 변경 a
[aws-dev-eks-mgmt]
  Failed to pull image "602401143452.dkr.ecr.us-west-2.amazonaws.com/amazon/aws-load-balancer-controller:v2.4.3"

  edit 에서 ap-northeast-2 으로 변경


[aws-dev-eks-es-cloudflare]  

업데이트 시 OOM -> r5.2xlarge

][]
ip-172-24-3-77.ap-northeast-2.compute.internal    243m         3%     30457Mi         100%  
ip-172-24-3-126.ap-northeast-2.compute.internal   279m         3%     30651Mi         100%      
ip-172-24-3-138.ap-northeast-2.compute.internal   166m         2%     28743Mi         94% 

kubectl describe nodes | grep -A5 "node.kubernetes.io/memory-pressure"

kubectl edit pdb istiod -n istio-system


error when evicting pods/"istiod-54b99569d5-n9cmt" -n "istio-system" (will retry after 5s): Cannot evict pod as it would violate the pod's disruption budget.


[복구 관련]



kubectl exec -it elasticsearch-coordinating-0 -n default -- bash

curl -X POST -k -u elastic:NewPassword123! "https://localhost:9200/_security/user/kibana_system/_password" \
-H "Content-Type: application/json" \
-d '{"password":"changeme"}'


NewPassword123!

kubectl get secret elasticsearch -n default -o jsonpath="{.data.elasticsearch-password}" | base64 --decode

curl -X GET -u elastic:Bitcash1!! "https://elasticsearch-master:9200/_cat/indices?v"



kubectl patch secret elasticsearch -n default -p='{"data":{"elasticsearch-password":"IAPzQa3jB3vRmyKLV58g"}}'

kubectl patch secret kibana -n default -p='{"data":{"kibana-password":"Y2hhbmdlbWU="}}'

kubectl rollout restart statefulset elasticsearch-master -n default
kubectl rollout restart statefulset elasticsearch-data -n default
kubectl rollout restart statefulset elasticsearch-coordinating -n default
kubectl rollout restart statefulset elasticsearch-ingest -n default


kubectl exec -it elasticsearch-master-0 -n default -- curl -k -X GET -u elastic:NewPassword123! "https://localhost:9200/_cluster/health?pretty"


kubectl get deploy -n default
kubectl get statefulset -n default


elasticsearch-coordinating   0/6     148d
elasticsearch-data           0/42    148d
elasticsearch-ingest         0/6     148d
elasticsearch-master         0/2     148d

kubectl scale statefulset elasticsearch-master --replicas=2 -n default
kubectl scale statefulset elasticsearch-data --replicas=42 -n default
kubectl scale statefulset elasticsearch-ingest --replicas=6 -n default
kubectl scale statefulset elasticsearch-coordinating --replicas=6 -n default
kubectl scale deploy kibana --replicas=1 -n default

kubectl delete pvc --all -n default
kubectl delete pvc kibana -n default



kubectl scale statefulset elasticsearch-master --replicas=0 -n default
kubectl scale statefulset elasticsearch-data --replicas=0 -n default
kubectl scale statefulset elasticsearch-ingest --replicas=0 -n default
kubectl scale statefulset elasticsearch-coordinating --replicas=0 -n default
kubectl scale deploy kibana --replicas=0 -n default

data-elasticsearch-data-0~42
data-elasticsearch-master-0~1

kubectl get pods -n default | grep Terminating | awk '{print $1}' | xargs -I {} kubectl delete pod {} -n default --grace-period=0 --force


kubectl set env deployment/kibana -n default KIBANA_PASSWORD="changeme2"
kubectl rollout restart deployment/kibana -n default
kubectl describe deployment kibana -n default | grep -i "KIBANA_PASSWORD"



echo -n "cash1!" | base64



echo "TmV3UGFzc3dvcmQxMjMh" | base64 --decode



NEW_PASSWORD="changeme"

kubectl exec -it elasticsearch-master-0 -n default -- \
curl -X POST -k -u elastic:NewPassword123! \
"https://localhost:9200/_security/user/kibana_system/_password" \
-H "Content-Type: application/json" \
-d "{\"password\":\"changeme\"}"



kubectl get secret


NAME                             TYPE                                  DATA   AGE
cred-harbor                      kubernetes.io/dockerconfigjson        1      2y147d
default-token-kllfq              kubernetes.io/service-account-token   3      2y154d
elasticsearch                    Opaque                                1      2y123d
elasticsearch-coordinating-crt   kubernetes.io/tls                     3      147d
elasticsearch-data-crt           kubernetes.io/tls                     3      147d
elasticsearch-ingest-crt         kubernetes.io/tls                     3      147d
elasticsearch-master-crt         kubernetes.io/tls                     3      147d
kibana                           Opaque                                1      5h24m



kubectl edit secret elasticsearch



apiVersion: v1
data:
  elasticsearch-password: TmV3UGFzc3dvcmQxMjMh
kind: Secret
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","data":{"elasticsearch-password":"SUFQelFhM2pCM3ZSbXlLTFY1OGc="},"kind":"Secret","metadata":{"annotations":{},"labels":{"app.kubernetes.io/instance":"elasticsearch","app.kubernetes.io/managed-by":"Helm","app.kubernetes.io/name":"el
asticsearch","helm.sh/chart":"elasticsearch-19.2.5"},"name":"elasticsearch","namespace":"default"},"type":"Opaque"}
  creationTimestamp: "2022-10-05T05:28:30Z"
  labels:
    app.kubernetes.io/instance: elasticsearch
    app.kubernetes.io/managed-by: Helm
    app.kubernetes.io/name: elasticsearch
    helm.sh/chart: elasticsearch-19.2.5
  name: elasticsearch
  namespace: default
  resourceVersion: "411960116"
  uid: b00dba6c-6632-4cdc-98e1-575d3d40d055
type: Opaque

```

# ASG

```
#!/bin/bash

SERVER_NAME="aws-ppp"
SERVICE_NAME="ppp"
PHASE="prod"
S3_BUCKET_DEPLOY="bithumb-service-deploy"
SERVER_IP=$(curl http://169.254.169.254/latest/meta-data/local-ipv4 |awk -F '.' '{print $3"-"$4}')
LOG_FILE="/tmp/EC2_start.log"

timedatectl set-timezone Asia/Seoul  >> ${LOG_FILE}
hostnamectl set-hostname ${SERVER_NAME}-${SERVER_IP}

# delete log.
echo -e "\n[$(date "+%Y-%m-%d %H:%M:%S")] Delete logs." >> ${LOG_FILE}
find /var/log/ -maxdepth 1 -name *.gz -delete
find /home/${SERVICE_NAME}/ -name *.log* -delete
rm -rf /home/${SERVICE_NAME}/logs
rm -rf /home/${SERVICE_NAME}/deploy


# Deploy the latest sources.
echo -e "\n[$(date "+%Y-%m-%d %H:%M:%S")] Start deploy." >> ${LOG_FILE}
aws s3 cp s3://${S3_BUCKET_DEPLOY}/${SERVICE_NAME}/${PHASE}/devops/ /home/${SERVICE_NAME}/devops/ --recursive >> ${LOG_FILE}
chown -R ${SERVICE_NAME}:service /home/${SERVICE_NAME}/devops/
chmod +x /home/${SERVICE_NAME}/devops/*.sh
su -c "/home/${SERVICE_NAME}/devops/${SERVICE_NAME}_devops.sh" ${SERVICE_NAME} >> ${LOG_FILE}

systemctl start nginx

# Updating Whatap Infra rpm download
infra_whatap_license="~~~asdassadads" && export infra_whatap_license
aws s3 cp --region ap-northeast-2 s3://bithumb-aws-infra/whatap/infra/update_whatap_infra.sh - | bash >> ${LOG_FILE}

systemctl restart whatap-infra && systemctl enable whatap-infra

# Install filebeat 
aws s3 cp --region ap-northeast-2 s3://bithumb-aws-infra/filebeat/install_filebeat.sh - | bash >> ${LOG_FILE}

# start Host-IPS.
echo -e "\n[$(date "+%Y-%m-%d %H:%M:%S")] Start Host-IPS." >> ${LOG_FILE}
/opt/ds_agent/dsa_control -r
/opt/ds_agent/dsa_control -a dsm://172.18.1.168:4120/ "policyid:10" "groupid:2"

# EC2 ready.
echo -e "\n[$(date "+%Y-%m-%d %H:%M:%S")] EC2 ready." >> ${LOG_FILE}
```


