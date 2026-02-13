# OPNsense - VLAN

## Creation du VLAN

Se rendre dans **Interfaces > Devices > VLAN** :

1. Dans **VLAN TAG**, entrer un numero non utilise
2. Dans **Parent**, selectionner l'interface physique concernee

![VLAN Create](Images/opnsense-vlan-create.png)

![VLAN Tag](Images/opnsense-vlan-tag.png)

## Assignation de l'interface

Assigner le VLAN a une interface :

![Assign Interface](Images/opnsense-assign-interface.png)

Activer l'interface en cochant **Enable** dans l'onglet correspondant :

![Enable Interface](Images/opnsense-enable-interface.png)

Attribuer une IP statique correspondant au sous-reseau du VLAN :

![Static IP](Images/opnsense-static-ip.png)
