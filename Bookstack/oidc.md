# BookStack - SSO OIDC (Keycloak)

## Configuration

Apres avoir cree un nouveau client dans le Realm Keycloak (voir [Keycloak - Creation d'un client](../Keycloak/keycloak.md#creation-dun-client-application)), recuperer les informations suivantes et les reporter dans le `.env` :

- `OIDC_CLIENT_ID`
- `OIDC_CLIENT_SECRET`
- `OIDC_ISSUER` (URL du Realm)

## Verification

L'authentification doit rediriger vers Keycloak et permettre la connexion via les comptes federes FreeIPA.
