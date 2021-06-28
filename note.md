# SHOW LINE

The CTY line-type is the Console Port. On any router, it appears in the router configuration as line con 0 and in the output of the show line command as cty. The console port is mainly used for local system access using a console terminal.

The TTY lines are asynchronous lines used for inbound or outbound modem and terminal connections and can be seen in a router or access server configuration as line x. The specific line numbers are a function of the hardware built into or installed on the router or access server.

The AUX line is the Auxiliary port, seen in the configuration as line aux 0.

The VTY lines are the Virtual Terminal lines of the router, used solely to control inbound Telnet connections. They are virtual, in the sense that they are a function of software - there is no hardware associated with them. They appear in the configuration as line vty 0 4.

# AAA
https://learningnetwork.cisco.com/s/article/introduction-to-aaa-implementation

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