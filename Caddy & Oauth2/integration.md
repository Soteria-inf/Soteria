# Integration Caddy + OAuth2 Proxy

Modifier le Caddyfile pour que le reverse proxy redirige vers l'application uniquement apres verification d'identite :

```
webserv.<DOMAIN> {
        handle /oauth2/* {
                reverse_proxy 127.0.0.1:4180 {
                        header_up X-Real-IP {remote_host}
                        header_up X-Forwarded-Uri {uri}
                }
        }

        handle {
                forward_auth 127.0.0.1:4180 {
                        uri /oauth2/auth
                        header_up X-Real-IP {remote_host}
                        copy_headers X-Auth-Request-User X-Auth-Request-Email

                        @needlogin status 401
                        handle_response @needlogin {
                                redir * /oauth2/start?rd={scheme}://{host}{uri}
                        }
                }

                reverse_proxy <IP_WEBSERVER>:80
        }

        log {
                output file /var/log/caddy/serveurweb.access.log
        }
}
```

Les headers supplementaires (`X-Real-IP`, `X-Forwarded-Uri`) sont optionnels mais permettent a l'application de tracer les requetes et facilitent le debogage.
