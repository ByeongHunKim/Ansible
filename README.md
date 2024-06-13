# Ansible

## Key Concepts

### Inventory
- 서버를 그룹별로 분리하기 위한 파일
- 동일한 설정이 필요한 서버를 그룹별로 묶어 효율적으로 관리
- [공식문서](https://docs.ansible.com/ansible/latest/getting_started/get_started_inventory.html#inventories-in-ini-or-yaml-format) 에서 간단한 설정의 경우 INI 파일이 직관적이고 쉽게 읽을 수 있지만, 관리하는 노드의 수가 많아질 때는 YAML 형식이 더 합리적인 선택이 될 수 있다고 명시되어있음

### Playbook
- Ansible은 기본적으로 playbook.yml 파일에서 작업을 정의
- 추후 EKS provisioning 이후 필요한 resource configuration 작업들 추가 예정
- **Ansible을 통해 Bastion Host에 접속 후 yml 실행으로 자동화 하는 것이 목표**

---

## 1. Installation Guide (MacOS)
```bash
brew install ansible
```

---

## 2. Prerequisites Before Install
- route53
   - domain
- acm
   - acm apply
- efs
  - efs stack
---

## 3. Prerequisites After Install
- `host_vars/bastion-1.yml` 수정
  ```bash
  cp host_vars/bastion-1.yml.template host_vars/bastion-1.yml
  ```
  - ansible_host
    - Bastion Host EC2 instance IP
  - ansible_user
    - ec2-user
  - ansible_ssh_private_key_file
    - SSH file directory
- `vars.yml` 수정
  ```bash
  cp vars.yml.template vars.yml
  ```
  - aws_access_key
    - your_aws_access_key
  - aws_secret_key
    - your_aws_secret_key
  - region
    - aws region
  - cluster_name
    - eks cluster name
  - kubectl_version
    - default ( v1.29.1 )
  - policy_name
    -  default ( AWSLoadBalancerControllerIAMPolicy )
  - acm_arn
    - domain acm arn
    - will be connected to istio ingress alb
  -  efs_stack_name
  - loki,prometheus_domain

---
## 4. Check Connection with Host (bastion-host)
```bash
ansible bastion-1 -m ping -i inventory.ini 

# output

# bastion-1 | SUCCESS => {
#     "changed": false,
#     "ping": "pong"
# }

```

---
## 5. Run Master Playbook
```bash
ansible-playbook site.yml -i inventory.ini
```

---
