# Traefik and portainer configuration

In this repo, you can find the configuration files of traefik and portainer that help you to set-up these libraries without interrupt.

### Traefik

To use and setting up the traefik, you should update and add your domain into these files content:

> ./traefik/docker-compose.yml

```yml
- "traefik.http.routers.traefik.rule=Host(`traefik.domain.com`)"
---------------------------------------------------^^^^^^^^^^
- "traefik.http.routers.traefik-secure.rule=Host(`traefik.domain.com`)"
----------------------------------------------------------^^^^^^^^^^
```

and also change the default email to your email address:

> ./traefik/data/traefik.yml

```yml
email: example@example.com
```

and finally run the traefik by the following command:

```bash
$ docker-compsoe up -d
```

### Portainer

To use and setting up the portainer, you should update and add your domain into the docker-compose file:

> ./portainer/docker-compose.yml

```yml
- "traefik.http.routers.portainer.rule=Host(`portainer.domain.com`)"
-------------------------------------------------------^^^^^^^^^^
- "traefik.http.routers.portainer-secure.rule=Host(`portainer.domain.com`)"
--------------------------------------------------------------^^^^^^^^^^
```

### Usage

To use the traefik as a dns manager to connect the domain to the docker containers, add these labels into your docker-compose file:

```yml
labels:
	- "traefik.enable=true"
	- "traefik.docker.network=web"
	- "traefik.http.routers.indra.entrypoints=http"
	- "traefik.http.routers.indra.rule=Host(`yoursubdomain.domain.com`)"
-----------------------------------------------------------^^^^^^^^^^
```

> Make sure your application runs by port 80, if you are exposing the application in another port, read to the traefik docs
