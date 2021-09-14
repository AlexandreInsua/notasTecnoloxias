# NOTAS DE GIT / GITHUB / GITLAB

## Introdución

## Instalación

## Configuración

`git config --global username "[username]"`. Configuración global de usuario.

`git config --global mail "[mail]"`. Configuración global de correo electrónico.

## Creación de repositorio

`git init`. Inicializa un repositorio.

## Comandos básicos

`git add`. Engade ficheiros á _staging area_. Con `.` engage todos. Marcado de ficheiros A: agregated, M: modified, U: untracked

`git commit`: Engade os ficheiros da _staging area_ ao repositorio local. Necesita `-m` para agregar descripción. Con `-am` engade todos os ficheiros modificados ou borrados pero non os pendentes de seguir. Con `--amend` abre a edición do último commit.

`git tag [name] -m "[description]"`. Especifica a versión do proxecto usando una tag. Para actualizala en remoto hai que facer un `git push --tags`.

`git reset --hard`. Restaura a un estado anterior.

`git status`. Monitorea o estado de seguemento dos ficheiros. Con `-s` lista ficheiroes e directorios.

## Branching e merging

`git branch`. Mostra as branches existentes e a actual.

`git branch [name]`. Crea unha branch.

`git checkout [name]`. Cambia á branch seleccionada.

`git merge [name]`. Une a branch seleccionada coa master.

## Sharing and updating projects

`git clone [url]`. Clona un respositorio.

`git push [remote] [branch]`. Actualiza o repositorio remoto cos cambios comiteados. Con `-u` , por exemplo `git push -u origin master`

`git pull [branch]`. Actualiza o repositorio local cos cambios comiteados no remoto. Se non está configurada a branch hai que especificala, por exemplo `git pull origin master`.

`git remote add origin [url]`. Vincula un repositorio cun repositorio remoto.

## Inspection and comparison

`git log`. Listado de commits. Co parámetro `--oneline` mostra unha lista simplificada co commit.
