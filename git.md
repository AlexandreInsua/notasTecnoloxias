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

`git status`. Monitorea o estado de seguemento dos ficheiros. Con `-s` lista ficheiroes e directorios.

`git reset --hard`. Restaura a un estado anterior.

`git tag [name] -m "[description]"`Especifica a versión do proxecto usando una tag. 

## Branching e merging

## Sharing and updating projects

`git remote add origin [url]`. Vincula un repositorio cun repositorio remoto.

`git push [branch]`. Actualiza o repositorio remoto cos cambios comiteados.

`git pull`. Actualiza o repositorio local cos cambios comiteados no remoto. Se non está configurada a branch hai que especificala, por exemplo `git pull origin master`.



## Inspection and comparison

`git log`. Listado de commits. Co parámetro `--oneline` mostra unha lista simplificada co commit.
