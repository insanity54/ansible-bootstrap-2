# ansible-bootstrap

installs everything needed for a remote host to use ansible

big up http://euphonious-intuition.com/2013/01/bootstrapping-a-cluster-with-ansible-debian-6-and-oracle-java-7/

greets


## Usage

Download this role using ansible-galaxy.

In your playbook's main.yml, disable gathering facts. Then add this ansible-bootstrap role as your first role. Example playbook--

```
---
- hosts: monitoring
  sudo: no
  gather_facts: no # <-- disabled so bootstrap role has a chance to install python
  vars_files:
    - vars/public.yml
    - vars/private.yml
  roles:
    - {role: bootstrap, tags: bootstrap} # <-- python is installed here, followed by gather_facts (setup module)
    - {role: pip, tags: pip}
    - {role: ruby, tags: ruby}
    - {role: ufw, tags: ufw}
    - {role: postfix, tags: postfix}
    - {role: apache2, tags: apache2}
    - {role: nagios, tags: nagios}
    - {role: provision, tags: provision}
```
