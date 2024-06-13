## 1. Ansible 사용을 위한 설정 파일 작업

```bash
# 루드 디렉토리에서 명령어 수행
cp host_vars/bastion-1.yml.template host_vars/bastion-1.yml

cp vars.yml.template vars.yml

# 값 넣어주기 
```

## 2. host 에 연결 확인

```bash
# 루드 디렉토리에서 명령어 수행
# 해당 명령어로 연결 확인
ansible bastion-1 -m ping -i inventory.ini
```

## (Optional) 3. 직접 하나 하나 playbook 실행 

```bash
# 루드 디렉토리에서 명령어 수행

# 1. aws-cli, aws configure, kubectl 클러스터 연결
ansible-playbook playbooks/aws-cli-and-cluster-context-setup.yml -i inventory.ini

# 2. helm, eksctl 설치
ansible-playbook playbooks/helm-eksctl-setup.yml -i inventory.ini

# 3. load balancer controller 생성 및 istio 설정
ansible-playbook playbooks/alb-controller-and-istio-setup.yml -i inventory.ini

# 4. istio-ingressgateway 및 istio-ingress 설정 -> route53에서 a레코드 ingress로 생성된 로드밸런서로 변경 필요함
ansible-playbook playbooks/istio-ingressgateway-and-ingress-setup.yml -i inventory.ini -v

# 5. efs 설정
ansible-playbook playbooks/efs-setup.yml -i inventory.ini -v

# 6. loki 설정
ansible-playbook playbooks/loki-setup.yml -i inventory.ini -v

# 7. prometheus 설정
ansible-playbook playbooks/prometheus-setup.yml -i inventory.ini -v
```

## 4. master playbook 실행 (site.yml)
```bash
# 프로젝트 루트 디렉토리에서 실행
ansible-playbook site.yml -i inventory.ini
```