# OPNsense - Depannage

## Erreur d'acces interface WAN vers LAN

> **Attention** : Les commandes ci-dessous modifient les regles du pare-feu en direct. A utiliser uniquement en environnement de laboratoire.

```bash
# Sauvegarder les regles actuelles
pfctl -sr > /tmp/rules_backup.txt

# Retirer les reply-to et route-to
pfctl -sr | sed 's/reply-to ([^)]*) //g' | sed 's/route-to ([^)]*) //g' > /tmp/rules_no_reply.txt

# Appliquer les regles modifiees
pfctl -F rules
pfctl -f /tmp/rules_no_reply.txt

# Verifier
pfctl -vvsr | grep -E "(route-to|reply-to)"

# Tester la connectivite
ping -S <IP_SOURCE> <IP_DESTINATION>
```
