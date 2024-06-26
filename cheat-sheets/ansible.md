# Installation

debian / ubuntu
>automate this with a shell script to reduce overhead
```bash
sudo apt update && \
sudo apt install -y software-properties-common && \
sudo add-apt-repository -yu ppa:ansible/ansible && \
sudo apt install ansible -y
```

mac
```bash
brew install ansible
```

# Playbook

run playbook
```bash
# linux
ansible-playbook --ask-become-pass --ask-vault-pass -t docker --skip-tags brew local.yml
# mac
ansible-playbook --ask-become-pass --ask-vault-pass -t mac local.yml
```

run playbook on remote git repo
```bash
# have to use vault-pass-file because ansible team decided to deprecate --ask-vault-pass on ansible-pull
# linux
ansible-pull -U git@github.com:NoseferatuWKF/ansible.git --ask-become-pass --vault-pass-file password --skip-tags brew
# mac
ansible-pull -U git@github.com:NoseferatuWKF/ansible.git --ask-become-pass --vault-pass-file password -t mac
```