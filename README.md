# ansible-lamp-install-mv
Ansible (code qui va dans une machine virtuelle faire l'installation de LAMP-SERVER)

Ansible LAMP Install

Ce référentiel contient un ensemble de scripts Ansible pour installer automatiquement un serveur LAMP (Linux, Apache, MySQL, PHP) dans une machine virtuelle cible.

Étape 1: Mise À Jour Des Paquets Et Installation D'Ansible
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

Avant de commencer, assurez-vous que vous avez Ansible installé sur votre machine hôte :

	-sudo apt update
	-sudo apt install ansible

Étape 2: Configuration Du Fichier D'Inventaire
'''''''''''''''''''''''''''''''''''''''''''''''

Le fichier d'inventaire /etc/ansible/hosts doit être configuré avec les informations des machines cibles où vous souhaitez installer LAMP.

[group_name]
host1 ansible_host=IP_address ansible_user=username ansible_ssh_private_key_file=/path/to/private_key

[all:vars]
ansible_python_interpreter=/usr/bin/python3

Assurez-vous de remplacer group_name, host1, IP_address, username et /path/to/private_key par les valeurs appropriées pour votre configuration.

Étape 3: Vérification De La Connectivité
'''''''''''''''''''''''''''''''''''''''''

Pour vérifier la connectivité entre la machine Ansible et la machine virtuelle cible, effectuez les opérations suivantes :

    Copiez la clé SSH de la machine Ansible vers la machine cible :

  
	-ssh-copy-id user@ip

Vérifiez la connectivité avec la machine virtuelle cible en utilisant la commande ansible :

	-ansible vms -i inventory.ini -m ping

Assurez-vous de remplacer user et ip par les informations appropriées pour votre configuration.

Étape 4: Exécution
'''''''''''''''''''

Maintenant, vous pouvez exécuter le playbook Ansible pour installer automatiquement LAMP sur la machine cible :

	-ansible-playbook -i inventory.ini lamp-installation.yml --ask-become-pass

Le paramètre --ask-become-pass vous sera demandé pour fournir le mot de passe de superutilisateur.

Après l'exécution du playbook, le serveur LAMP sera installé sur la machine cible automatiquement.

N'hésitez pas à personnaliser le playbook lamp-installation.yml en fonction de vos besoins spécifiques.

Note : Assurez-vous de sauvegarder et de conserver en sécurité les fichiers contenant les informations sensibles tels que les clés privées.
	-

