# Wildfly-server

Création d'un serveur Wildfly dans un container LXC avec Ansible

1) Lancer le script de création de container Ubuntu :
>> sh 01_create_ubuntu.sh

2) Accéder au container via SSH :
>> ssh @IP_Container

3) Modifier l'inventaire Ansible :
éditer le fichier inventory.ini pour y ajouter l'@IP de notre container dans le groupe wildfly

4) Lancer le playbook Ansible :
>> sh 02_run_playbook.sh

5) Accéder au serveur wildfly à partir d'un navigateur web de la VM : 
http://@IP_Container:8080


## Astuce - accès au container de la VM depuis notre PC physique :

Dans la VM : 
1) >> sudo apt install  iptables-persistent

2) >> sudo su

3) redirection de l'IP de notre VM sur le container :
>> iptables -t nat -A PREROUTING -i [nom_carte_reseau] -p tcp --dport [n°port] -j DNAT --to @IP_Container:[n°port]

exemple : 
>> iptables -t nat -A PREROUTING -i enp0s8 -p tcp --dport 8080 -j DNAT --to 10.123.219.55:8080

4) >> iptables-save >  /etc/iptables/rules.v4

Depuis notre PC physique : 
5) Dans un navigateur web, entrez l'@IP de la VM suivi de :8080 - exemple : http://10.123.219.55:8080

La page wildfly par défaut doit s'afficher
