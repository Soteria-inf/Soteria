# OPNsense

Pare-feu, routeur et serveur DHCP/DNS de l'infrastructure. OPNsense assure la segmentation reseau par VLAN et le filtrage du trafic.

## Prerequis

- VM ou machine dediee avec OPNsense installe
- Acces a l'interface web d'administration
- Interfaces reseau configurees (WAN, LAN)

## Guides

- [Aliases et nomenclature](aliases.md)
- [VLAN](vlan.md)
- [DHCP et DNS](dhcp-dns.md)
- [Depannage](troubleshooting.md)

## Rappels de securite

- Limiter l'acces a l'interface d'administration (reseau de gestion uniquement)
- Sauvegarder la configuration apres chaque changement majeur
- Tenir OPNsense a jour
