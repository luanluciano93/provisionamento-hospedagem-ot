[DOCUMENTAÇÃO no wiki](https://github.com/DevelopersPL/otshosting-provisioning/wiki)

Provisionamento de Hospedagem de Otserv
=======================
Este é um manual usado para provisionar completamente uma máquina Ubuntu para hospedagem OTS nas seguintes configurações:
__Ubuntu 18.04__
__MariaDB e Nginx__
__TFS 1.3 e ZnoteACC__

Um script para executar em uma máquina independente para provisioná-lo. Se o usuário "otsmanager" não existir, ele será criado com a senha: "otsmanager".

```bash
#!/bin/bash -ex
apt-get update
apt install -y -q python-simplejson git-core ansible
ansible-pull -i localhost, -U https://github.com/luanluciano93/otshosting-provisioning.git -d /srv/otshosting-provisioning --purge -t default
```

Tags disponíveis:
* systemd - ativa o registro em diário persistente (padrão)
* general - software e integração (padrão)
* mysql - MariaDB servidor SQL (padrão)
* php-fpm - Suporte PHP para o site (padrão)
* nginx - servidor web (padrão)
* pma - phpMyAdmin para facilitar a administração (padrão)
* tfs - TFS na última revisão compilado e instalado automaticamente (padrão)
* znote - ZnoteAAC instalado e configurado automaticamente (padrão)

## Provisionamento baseado em cloud-init

Um script cloud-init para provisionar uma instância do cloud usando este manual:
```
#cloud-config
users:
  - name: otsmanager
    gecos: OTS Manager
    lock-passwd: false
    
disable_root: true
ssh_pwauth: True
timezone: Europe/Warsaw

package_upgrade: true
package_update: true

packages:
 - python-simplejson
 - git
 - ansible
 - aptitude
 
runcmd:
  - 'ansible-pull -i localhost, -U https://github.com/luanluciano93/otshosting-provisioning.git -d /srv/otshosting-provisioning --purge'
```
