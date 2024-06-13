# Ansible for EKS configuration
- Istio
- EFS
- Loki
- Prometheus

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
