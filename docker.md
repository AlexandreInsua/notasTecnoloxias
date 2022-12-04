# DOCKER

Clonar un repositorio.

`docker run --name repo alpine/git clone \ https://github.com/docker/gettting-started.git`

`docker cp repo:/git/getting-started`

facer a build da imaxe

`cp getting-started`

`docker build -t docker101tutorialcl`

run o container

`docker run -d 80:80 \ --name docker-tutorial docker101tutorialcl`
