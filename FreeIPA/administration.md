# FreeIPA - Administration

## Creation d'un administrateur

Dans l'interface web FreeIPA : **Utilisateurs > Utilisateurs actifs > Ajouter**.
Creer un utilisateur puis l'ajouter au groupe **admins** afin de lui attribuer les privileges d'administration.

### Rappels de securite

- Utiliser un compte administrateur distinct du compte personnel
- Activer des mots de passe forts et uniques
- Limiter l'appartenance au groupe **admins** au strict necessaire

Pour verifier la jonction depuis le client :

```bash
realm list
```

![Realm List](Images/freeipa-realm-list.png)

## Politique de mot de passe

Se rendre dans **Politique > Politique de mot de passe** :

![Password Policy](Images/freeipa-password-policy.png)

Cliquer sur **Ajouter** et selectionner le groupe cible. La priorite est un chiffre : la valeur la plus elevee sera celle appliquee.

![Password Group](Images/freeipa-password-group.png)

> **Note** : Par defaut, la politique `global_policy` s'applique a tous les utilisateurs avec une priorite de 0.

## Gestion des droits sudo

### Autoriser toutes les commandes sudo

Se rendre dans **Politique > Sudo > Regles sudo > Ajouter**.

Specifier les utilisateurs ou groupes concernes, puis les machines sur lesquelles les droits s'appliquent.

> **Note** : Par defaut, les droits sudo sont desactives.

### Autoriser des commandes specifiques

1. Aller dans **Politique > Sudo > Commandes sudo** et ajouter les commandes souhaitees :

![Sudo Command](Images/freeipa-sudo-command.png)

![Sudo Command Add](Images/freeipa-sudo-command-add.png)

2. Creer une regle sudo dans **Politique > Sudo > Regles sudo > Ajouter** :

![Sudo Rule](Images/freeipa-sudo-rule.png)

> **Note** : Compter environ 10 minutes apres redemarrage du poste client pour que les regles sudo soient appliquees.
