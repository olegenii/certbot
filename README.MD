# NGINX + certbot skeleton
This is a `docker-compose.yml` with 2 containers of nginx and certbot using for LetsEncrypt ssl certificate issuing.

### Create the certificate using Certbot

1. Install `git`, `docker`, `docker-compose`.
Clone this repo
```sh
  git clone
```

2. Testing certificate issue.
- Comment ssl part in nginx configuration file - `vhost.conf` because we dont have certificate now
- Start nginx container
```sh
  docker compose up -d
```
- Test issuing
```sh 
  docker compose run --rm certbot certonly --webroot --webroot-path /var/www/certbot/ --dry-run -d example.org 
``` 
You should get a success message like "The dry run was successful".

3. Uncomment certbot folder with certs in `docker-compose.yml` using as a volume both for nginx and certbot
```yml
  - ./certbot/conf/:/etc/letsencrypt/:rw
```

4. Issue a certificate

- Issue a cert
```sh
  docker compose run --rm  certbot certonly --webroot --webroot-path /var/www/certbot/ -d example.org
```
- Uncomment ssl-part in vhost.conf
- Restart `nginx`

### Renewing the certificates

```sh 
  docker compose run --rm certbot renew
```








