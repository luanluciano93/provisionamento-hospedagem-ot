# Provisionamento de Hospedagem de Otserv
Este é um manual é usado para provisionar completamente uma máquina Ubuntu para hospedagem OTS.

### Configurações:
- Ubuntu 18.04
- MariaDB e Nginx
- TFS 1.3 e ZnoteACC


### Executando o comando:
Um script para executar em uma máquina independente para provisioná-lo. Se o usuário "otsmanager" não existir, ele será criado com a senha: "otsmanager".

```bash
#!/bin/bash -ex
apt-get update
apt-get install -y -q python-simplejson git-core ansible
ansible-pull -i localhost, -U https://github.com/luanluciano93/otshosting-provisioning.git -d /srv/otshosting-provisioning --purge -t default
```

### Tags disponíveis:
* systemd - ativa o registro em diário persistente (padrão)
* general - software e integração (padrão)
* mysql - MariaDB servidor SQL (padrão)
* php-fpm - Suporte PHP para o site (padrão)
* nginx - servidor web (padrão)
* pma - phpMyAdmin para facilitar a administração (padrão)
* tfs - TFS na última revisão compilado e instalado automaticamente (padrão)
* znote - ZnoteAAC instalado e configurado automaticamente (padrão)
