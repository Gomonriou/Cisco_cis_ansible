# Utilisation:

## Prerequis:

Vérification de la prise en compte du protocole ssh par l'IOS
Tout d'abord, il faut vérifier que l'IOS du switch supporte ssh. La mention k9 (crypto) doit figurer dans le nom de l'IOS.
La commande pour vérifier la version de l'IOS est:

2960-RG#show version

Cisco IOS Software, C2960 Software (C2960-LANBASEK9-M), Version 12.2(55)SE, RELEASE SOFTWARE (fc2)
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 1986-2010 by Cisco Systems, Inc.
Compiled Sat 07-Aug-10 23:04 by prod_rel_team

##

Le protocole ssh peut être activé par défaut. Vérifions avec la commande suivante:

2960-RG#show ip ssh
SSH Enabled - version 2.0

Authentication timeout: 60 secs; Authentication retries: 3

## Activer le ssh 

enable
conf t
hostname Catalyst
crypto key generate rsa general-keys label SSHKEY modulus 2048
ip ssh rsa keypair-name SSHKEY
service password-encryption
enable secret 0 ENABLESECRET (toor)
username USERNAME (catalyst) password 0 PASSWORD (catatest)
aaa new-model
aaa authentication login default local-case
aaa authentication enable default enable
aaa authorization commands 15 default local
line vty 0 4
  transport input ssh
  login local

## Conf minimal
Catalyst(config)#vlan 1
Catalyst(config-vlan)#exit
Catalyst(config)#interface vlan1
Catalyst(config-if)#ip address 192.168.17.11 255.255.255.0
Catalyst(config-if)#ex
Catalyst(config)#ip default-gateway 192.168.17.254

Vérification de la config
uration du vlan d'administration
Catalyst#sh run int vlan1

## save conf
Catalyst#copy running-config startup-config
Catalyst#write 

Catalyst#reload (pour test)

## co ssh
ssh -c aes256-cbc catalyst@192.168.17.11 
mdp pour enable : toor
log ssh -> catalyst/catatest

ansible-playbook -i ~/Documents/stage_meyer/hardening_debian/Cisco_cis_ansible/examples/host ~/Documents/stage_meyer/hardening_debian/Cisco_cis_ansible/examples/playbook.yaml