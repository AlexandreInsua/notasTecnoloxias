# NOTAS DE GIT / GITHUB / GITLAB

## Introdución

**Git** é unha ferramenta para o control de versións, que permite facer o seguemento de cambios nun proxecto rexistrando cada cambio en _commits_. O sistema traballa con tres estados para cada ficheiro monitorizado (_track_): a _working area_, a _staging area_ e o _repository_.

En xeral trabállase con unha branch principal, estable, e outras de desenvolvemento. Posteriormente, vanse fusionando as branches de desenvolvemento coa principal. Git incorpora os cambios dunha branch noutra se non hai conflitos. En caso de habelos é posible que haxa que resolvelos manualmente.

Cando se produce un conflito git pinta no ficheiro o texto conflitivo nas branches. Hai que escoller entre ambos e comitear os cambios.

**HEAD** é o commit actual.

Cando se fai un **pull** traballa con correspondencia entre as branch local e remota, non sube todo o repositorio.

## Instalación

En Windows, descargar o instalador e seguir as instrucións.
En Linux da familia Debian, `apt-get install git`.

## Configuración

`git --version`. Mostra a versión actual.

`git config --global username "[username]"`. Configuración global de usuario.

`git config --global mail "[mail]"`. Configuración global de correo electrónico.

`git config --list`. Mostra a configuración local.

## Creación de repositorio

`git init`. Inicializa un repositorio.

## Comandos básicos

`git add`. Engade ficheiros á _staging area_. Con `.` engage todos. Marcado de ficheiros A: agregated, M: modified, U: untracked

`git commit`: Engade os ficheiros da _staging area_ ao repositorio local. Necesita `-m` para agregar descripción. Con `-am` engade todos os ficheiros modificados ou borrados pero non os pendentes de seguir. Con `--amend` abre a edición do último commit.

`git diff [hash] [hash]`. Lista de modificacións que non están incluídas na _staging area_ ou entre varios commit.

`git tag [name] -m "[description]" ?[hash]`. Especifica a versión do proxecto usando una tag. Para actualizala en remoto hai que facer un `git push --tags`. Se engadimos o hash dun commit, quedan asociados

`git reset [hash]`. Elimina o último commit ou un especificado (hai que usalo con precaución para evitar conflitos). Deixa os cambios na _working_ Con `--hard` elimina os cambios de _working_ e _staging_ con `--soft` elimina o commit pero non os cambios.

`git revert [hash] `. Revirte os cambios dun commit. Con `-n` non comitea a reversión.

`git status`. Monitorea o estado de seguemento dos ficheiros. Con `-s` lista ficheiroes e directorios.

## Branching e merging

`git branch`. Mostra as branches existentes e sinala a actual.

`git branch [name]`. Crea unha branch. Con `-D` borra a branch. Cada feature debe ter a súa branch. Con `-m` modifica o nome dunha branch.

`git checkout -- [file name]`. Desfai unha modificación pendente de agregar ao _staging_.

`git checkout [hash]`. Vai a un commit.

`git checkout [name]`. Cambia á branch seleccionada. Con `-b` crea a branch e se move a ela.

`git merge [name]`. Une a branch seleccionada coa master.

## Sharing and updating projects

`git clone [url] ?[directory]`. Clona un respositorio. Pódese engadir o diretorio de destino.git

`git push [remote] [branch]`. Actualiza o repositorio remoto cos cambios comiteados. Con `-u` , por exemplo `git push -u origin master`

`git pull [branch]`. Actualiza o repositorio local cos cambios comiteados no remoto. Se non está configurada a branch hai que especificala, por exemplo `git pull origin master`. 

`git remote add origin [url]`. Vincula un repositorio cun repositorio remoto.

## Inspection and comparison

`git log`. Listado de commits. Co parámetro `--oneline` mostra unha lista simplificada co commit. Con `--graph` pinta unha representación gráfica das branches. Con `--all` mostra todos dos commits.
