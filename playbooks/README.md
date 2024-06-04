```bash
# 루드 디렉토리에서 명령어 수행
cp host_vars/bastion-1.yml.template host_vars/bastion-1.yml

# 값 넣어주기 
```

```bash
# 해당 명령어로 연결 확인
ansible bastion-1 -m ping -i inventory.ini
```

```bash
# 먼저 eks-initial-configuration.yml 에 변수 삽입 ( 개선 필요 )
ansible-playbook playbooks/eks-initial-configuration.yml -i inventory.ini
```