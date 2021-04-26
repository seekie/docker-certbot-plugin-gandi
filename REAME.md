1. Obtain a Gandi API token (see [Gandi LiveDNS API](https://doc.livedns.gandi.net/))
2. Create a `gandi.ini` config file with the following contents and apply `chmod 600 gandi.ini` on it:
  ```
  certbot_plugin_gandi:dns_api_key=<APIKEY>
  ```
3. Generate wildcard certificate
  ```
  docker run -it --rm \
    -v '<path-to-certbot-config>:/etc/letsencrypt' \
    -v '<path-to-gandi.ini>:/gandi.ini' \
    seekie/docker-certbot-plugin-gandi:latest \
      certonly -a certbot-plugin-gandi:dns --certbot-plugin-gandi:dns-credentials /gandi.ini \
      -d domain.com \
      -d \*.domain.com \
      --server https://acme-v02.api.letsencrypt.org/directory
  ```
4. Renew certificate
  ```
  docker run -it --rm \
    -v '<path-to-certbot-config>:/etc/letsencrypt' \
    -v '<path-to-gandi.ini>:/gandi.ini' \
    seekie/docker-certbot-plugin-gandi:latest \
      renew -q -a certbot-plugin-gandi:dns --certbot-plugin-gandi:dns-credentials /gandi.ini \
      --server https://acme-v02.api.letsencrypt.org/directory
  ```
