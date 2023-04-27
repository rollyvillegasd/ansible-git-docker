# Install GIT and Docker with Ansible

### Ansible
[Ansible](https://github.com/rollyvillegasd/ansible-ntp) Configuración de ansible

### Validar versión de Ansible
```sh
subscription-manager repos --enable rhel-7-server-ansible-2.6-rpms
yum install -y ansible
ansible --version
```

### Copiar repositorio en /opt/ansible
```shell
.
├── inventories
│   └── vmware
│       └── group_vars
│           └── all
├── playbooks
│   ├── install-docker.yaml
│   └── install-sw-base.yaml
└── roles
    ├── 01-sw_base
    │   ├── defaults
    │   │   └── main.yml
    │   ├── files
    │   ├── handlers
    │   │   └── main.yml
    │   ├── meta
    │   │   └── main.yml
    │   ├── README.md
    │   ├── tasks
    │   │   └── main.yml
    │   ├── templates
    │   ├── tests
    │   │   ├── inventory
    │   │   └── test.yml
    │   └── vars
    │       └── main.yml
    ├── 02-docker
    │   ├── defaults
    │   │   └── main.yml
    │   ├── files
    │   ├── handlers
    │   │   └── main.yml
    │   ├── meta
    │   │   └── main.yml
    │   ├── README.md
    │   ├── tasks
    │   │   └── main.yml
    │   ├── templates
    │   ├── tests
    │   │   ├── inventory
    │   │   └── test.yml
    │   └── vars
    │       └── main.yml

```

### Verificar sintanxis de playbook
```sh
ansible-playbook --syntax-check playbooks/install-sw-base.yaml -v -K
ansible-playbook --syntax-check playbooks/install-docker.yml -v -K
```
```text
 ansible-playbook --syntax-check playbooks/install-sw-base.yaml -v -K
Using /etc/ansible/ansible.cfg as config file

playbook: playbooks/install-sw-base.yaml

```
### Ejecutar playbook
```sh
ansible-playbook playbooks/install-sw-base.yaml -v -K
ansible-playbook playbooks/install-docker.yaml -v -K
```
```text
ansible-playbook playbooks/install-docker.yaml -v -K
Using /etc/ansible/ansible.cfg as config file
BECOME password:
```
```text
ansible-playbook playbooks/install-docker.yaml -v -K
Using /etc/ansible/ansible.cfg as config file
BECOME password:
```
```text
PLAY RECAP ***********************************************************************************************************
worker02.example.com : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
worker01.example.com : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

### Validar versiones instaladas
```sh
[root@worker01 ~]# java --version
openjdk 11.0.16.1 2022-08-12 LTS
OpenJDK Runtime Environment (Red_Hat-11.0.16.1.1-1.el8_6) (build 11.0.16.1+1-LTS)
OpenJDK 64-Bit Server VM (Red_Hat-11.0.16.1.1-1.el8_6) (build 11.0.16.1+1-LTS, mixed mode, sharing)
[root@worker01 ~]# git --version
git version 2.31.1
[root@worker01 ~]# docker version
Client: Docker Engine - Community
 Version:           23.0.5
 API version:       1.42
 Go version:        go1.19.8
 Git commit:        bc4487a
 Built:             Wed Apr 26 16:16:37 2023
 OS/Arch:           linux/amd64
 Context:           default

Server: Docker Engine - Community
 Engine:
  Version:          23.0.5
  API version:      1.42 (minimum version 1.12)
  Go version:       go1.19.8
  Git commit:       94d3ad6
  Built:            Wed Apr 26 16:14:13 2023
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.6.20
  GitCommit:        2806fc1057397dbaeefbea0e4e17bddfbd388f38
 runc:
  Version:          1.1.5
  GitCommit:        v1.1.5-0-gf19387a
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
[root@worker01 ~]# cat /etc/redhat-release
Red Hat Enterprise Linux release 8.6 (Ootpa)
[root@worker01 ~]#
```

By
-------
- Rolly Villegas Delgado  -  vdrolly@gmail.com

