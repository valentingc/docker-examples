# Traefik v2
Traefik is a powerful reverse proxy that integrates nicely into docker.
This example runs traefik v2.2.0.

## Docker network
Traefik needs a docker network. In this example, the network name is `traefikv2`.
You can create it with:
```
sudo docker network create traefikv2
```

## Configuration
`docker-compose.yml`
* Change http/https ports, if you want to use different ports than 80/443 (but make sure you adapt your letsencrypt certificateProvider, then!)

`config\traefik.yaml`
* `certificatesresolvers.letsencrypt.acme.email`:
  * INSERT_EMAIL_HERE: Insert your email, used for the certificate generation, here
* `providers.docker.network`:
  * Change docker network name, if you want to use a different network than `traefikv2`


`config\acme.json`
* Create the file (docker-compose will create a folder otherwise)
* Set the correct permission for this file. Your certificates will be stored in this json file!

```
sudo touch config\acme.json
sudo chmod 600 config\acme.json
```

## HTTP -> HTTPS redirection
This is configured in the `rules\ssl-redirect.yaml` file.
If you do not want this behaviour, just remove it.