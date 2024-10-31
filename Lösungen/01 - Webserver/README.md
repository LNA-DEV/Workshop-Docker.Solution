# Webserver

- Befasse sie sich mit den vorher genannten Befehlen
- Pullen sie einen Webserver (nginx)
- Starte sie diesen Webserver mit einem offenen Port
- Öffne sie die Website

```sh
# Docker zieht das neueste Nginx-Image von Docker-Hub und startet einen Container
docker run --name my-nginx -p 8080:80 -d nginx
```
