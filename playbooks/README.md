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

## (deprecated) 3. 직접 하나 하나 playbook 실행 

```bash
# 루드 디렉토리에서 명령어 수행

# aws-cli, aws configure, kubectl 클러스터 연결
ansible-playbook playbooks/eks-initial-configuration.yml -i inventory.ini

# helm, eksctl 설치
ansible-playbook playbooks/helm-eksctl-setup.yml -i inventory.ini

# load balancer controller 생성 및 istio 설정
ansible-playbook playbooks/alb-controller-and-istio.yml -i inventory.ini
```

## 4. master playbook 실행 (site.yml)
```bash
# 프로젝트 루트 디렉토리에서 실행
ansible-playbook site.yml -i inventory.ini
```