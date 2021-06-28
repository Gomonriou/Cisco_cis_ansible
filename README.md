# Disclaimer 

This repo is in progress

# Requirement :

## Check if you can use SSH

Checking that the IOS supports the ssh protocol
First of all, you have to check that the IOS of the switch supports ssh. The mention k9 (crypto) must appear in the name of the IOS.

    2960-RG#show version

    Cisco IOS Software, C2960 Software (C2960-LANBASEK9-M), Version 12.2(55)SE, RELEASE SOFTWARE (fc2)
    Technical Support: http://www.cisco.com/techsupport
    Copyright (c) 1986-2010 by Cisco Systems, Inc.
    Compiled Sat 07-Aug-10 23:04 by prod_rel_team



The ssh protocol can be enabled by default. Let's check :

    2960-RG#show ip ssh
    SSH Enabled - version 2.0

    Authentication timeout: 60 secs; Authentication retries: 3

## Enable SSH 

    enable
    conf t
    hostname HOSTNAME
    crypto key generate rsa general-keys label SSHKEY modulus 2048
    ip ssh rsa keypair-name SSHKEY
    service password-encryption
    enable secret 0 ENABLESECRET 
    username USERNAME secret PASSWORD 
    aaa new-model
    aaa authentication login default local-case
    aaa authentication enable default enable
    aaa authorization commands 15 default local
    line vty 0 4
      transport input ssh
      login local

## Minimum configuration

    Catalyst(config)#vlan 1
    Catalyst(config-vlan)#exit
    Catalyst(config)#interface vlan1
    Catalyst(config-if)#ip address 192.168.17.11 255.255.255.0
    Catalyst(config-if)#ex
    Catalyst(config)#ip default-gateway 192.168.17.254

    Vérification de la config
    uration du vlan d'administration
    Catalyst#sh run int vlan1

## Save configuration

    Catalyst#copy running-config startup-config
    Catalyst#write 

    Catalyst#reload (pour test)

# Use :

## CHANGE DEFAULT VARIABLE (defaults/main.yml) !!

## Tags 

* scored

Failure to comply with "Scored" recommendations will decrease the final benchmark score.
Compliance with "Scored" recommendations will increase the final benchmark score.

* not_scored

Failure to comply with "Not Scored" recommendations will not decrease the final
benchmark score. Compliance with "Not Scored" recommendations will not increase the
final benchmark score.

* level_1
1. be practical and prudent;
2. provide a clear security benefit; and
3. not inhibit the utility of the technology beyond acceptable means.

* level_2
1. are intended for environments or use cases where security is paramount.
2. acts as defense in depth measure.
3. may negatively inhibit the utility or performance of the technology.

## Commands

#Get extra log when running playbook with debuging
```Bash
ansible-playbook -i host run.yaml  -vvvv
```

#Run one tag only
```Bash
ansible-playbook -i host run.yaml --tags="scored"
```

#Skips tags
```Bash
ansible-playbook -i host run.yaml --skip-tags="level_2" --skip-tags="not_scored"
```


## TO DO 

1. rework 1.2.4
2. rework all section & finsh 1.1.X like 1.1.1? 
3. debug radius_4 & 5
4. 1.4.3 remove automatically user without secret -> 'no username {{item}}'
5. 2.3.1.4 loop for multiple servers
5. review SNMP 1.5.2-3-4 (Not urgent)
6. Do section 3 (Not urgent)
