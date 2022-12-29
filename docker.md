# DOCKER

Clonar un repositorio.

`docker run --name repo alpine/git clone \ https://github.com/docker/gettting-started.git`

`docker cp repo:/git/getting-started`

facer a build da imaxe

`cp getting-started`

`docker build -t docker101tutorialcl`

run o container

`docker run -d 80:80 \ --name docker-tutorial docker101tutorialcl`

## IMAXES

## CONTENEDORES

## DOCKERFILE

FROM Toma una imaxe  base. Pode aparecer varias veces no mesmo ficheiros. Poden ter alias.
LABEL Documenta a imaxe.
USER Cambia o usuario actual 
ENV Establece variables de entorno para a build da imaxe e os containers.
ARG Establece variables de entorno para a build (da imaxe, pero non dos containers). Pódese para por parámetro. Se se declara ande de FROM non ser ser accesible despois del.
RUN Executa un comando no sistema
ENTRYPOINT
CMD
WORKDIR
ADD
COPY
HEALTHCHECK Envia una verificación de actividade. 


## SWARM
É unha especie de compose avanzado para produción pero tamén se pode correr en local. 
Docker en multhost con monitoreo doado. Ten un orquestrador, accións extras e compose v3. E máis escalable, balanceable e reactivo.
Ten cinco comando avanzados principais.

## SECURITY

## DOCKER SECRETS

## DOCKER COMPOSE

## TESTING E DEBUGING

## DOCUMENTACIÓN

## ORQUETRADORES

### Stuff as a service

### Podman
Só linux. Fundamentalmente rootless. É un paquete único.

###  Kubernetes
