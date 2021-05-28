# Ansible-Playbook-IST

Ce Playbook permet la configuration initiale de nodes ansible disposant d'un systèmme d'exploiation Debian(64bits). 

Le Playbook exécute les tâches suivantes : 

- Création d'un compte et groupe Administrateur 
- Copie de la clé publique du serveur Ansible vers les nodes 
- Configuration du serveur SSH
- Installation des packages 
- Mise à jour du Hostname
- Configuration de Vim

Le programme a été testé sur l'OS Debian 64bits

## Paramètres

- `create_user`: Nom de l'utilisateur à créer.
- `new_hostname`: Nom d'hôte à insérer.
- `copy_local_key`: Chemin vers une clé publique SSH locale qui sera copiée en tant que clé autorisée pour le nouvel utilisateur. Par défaut, le script copie la clé de l'utilisateur système actuel exécutant Ansible.
- `sys_packages`: Liste des packages à installer.
 


## Fonctionnement du Playbook

### 1. 0btention du Playbook
```shell
git clone https://github.com/BOURGUITSamuel/Ansible-Playbook-IST
cd Ansible-Playbook-IST/
```

### 2. Personnalisation des options

```shell
vim vars/default.yml
```

```yml
#vars/default.yml
---
create_user: admin
new_hostname: admin
copy_local_key: "{{ lookup('file', lookup('env','HOME') + '/.ssh/id_rsa.pub') }}"
sys_packages: [ 'curl', 'vim', 'net-tools', 'dos2unix', 'unzip' ]
```

### 3. Lancement du Playbook

```command
ansible-playbook -l [target] -i [inventory file] -u [remote user] playbook.yml
```

