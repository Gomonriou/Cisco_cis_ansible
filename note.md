# les lignes


# ACL
Les ACL Standard (de 1 à 99) -> Elles vérifient l’IP source uniquement.
Les ACL étendues (de 100 à 199) -> Elles vérifient l’IP source, l’IP de destination, le protocole, les ports.

Fonctionement du masque:

The source/source-wildcard of 0.0.0.0/255.255.255.255 means "any".
The source/wildcard of 10.1.1.2/0.0.0.0 is the same as "host 10.1.1.2".

## exemples
access-list 1 permit 192.168.1.0 0.0.0.255 -> ACL (numéro 1) qui autorise le réseau 192.168.1.0
Router(config)#int fa0/0
Router(config-if)#ip access-group 1 out