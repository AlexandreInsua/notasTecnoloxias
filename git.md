# NOTAS DE GIT / GITHUB / GITLAB

## Introdución

**Git** é unha ferramenta para o control de versións, que permite facer o seguemento de cambios nun proxecto rexistrando cada cambio en _commits_. O sistema traballa con tres estados para cada ficheiro monitorizado (_track_): a _working area_, a _staging area_ e o _repository_.

En xeral trabállase con unha branch principal, estable, e outras de desenvolvemento. Posteriormente, vanse fusionando as branches de desenvolvemento coa principal. Git incorpora os cambios dunha branch noutra se non hai conflitos. En caso de habelos é posible que haxa que resolvelos manualmente.

Cando se produce un conflito git pinta no ficheiro o texto conflitivo nas branches. Hai que escoller entre ambos e comitear os cambios.

Os repositorios git teñen un ficheiro `gitignore` que lle indican a git ficheiros que debe ignorar. Normalmente son ficheiros de credenciais, ficheiros compilados, temporais ou de dependencias. Cada unha das súas liñas son as rutas dos ficheiros

**HEAD** é o commit actual.

Para obter o enésimo commit anterior a un dado úsase o til: `[hash]~n`.

Os comandos adminten un parámetro `-h` que pinta o manual do comando.

As páxinas git diferencian varias estratexias de merge. **Merge commit** é aquela que crea un commit para a merge (a estándar). **Merge rebase** fai un rebase, de forma que os commits da branch mergeada quedarán por riba dos anteriores. **Merge squash** implica que todo o diff (con diferentes commits) pasa a ser un único commit.

## Instalación

En Windows, descargar o instalador e seguir as instrucións.
En Linux da familia Debian, `apt-get install git`.

## Configuración

`git --version`. Mostra a versión actual.

`git config --global username "[username]"`. Configuración global de usuario.

`git config --global mail "[mail]"`. Configuración global de correo electrónico.

`git config --list`. Mostra a configuración local.

`git config --global alias.[alias] '[comando]`. Crea un alias para un comando.

`git config --global init.defaultBranch [name]`. Establece o nome da branch principal por defto.

`git config --global --get-regex alias`. Mostra os alias creados.

`git config --global --unset alias.[alias]`. Elimina un alias.

## Creación de repositorio

`git init`. Inicializa ou reinicializa un repositorio.

## Comandos básicos

`git add`. Engade ficheiros á _staging area_. Con `.` engage todos. Con `-p` ou `--patch` permite seleccionar os cambios que se van engadir, pero non aplica a ficheiros novos. Marcado de ficheiros A: agregated, M: modified, U: untracked.

`git apply`. Permanece á escoita do que metemos por teclado, como se for unha consola.

`git commit`. Engade os ficheiros da _staging area_ ao repositorio local. Necesita `-m` para agregar descripción. Con `-am` engade todos os ficheiros modificados ou borrados pero non os pendentes de seguir. Con `--amend` abre a edición do último commit. Con `-S` permite asinar o commit.

`git diff [hash] [hash]`. Lista de modificacións que non están incluídas na _staging area_ ou entre varios commit. Podese gardar  a súa saída nun ficheiro .patch para estudar os cambios.

`git reset [hash]`. Elimina o último commit ou un especificado (hai que usalo con precaución para evitar conflitos). Se non se especifica un commit, revirte o último _add_ Deixa os cambios na _working_ Con `--hard` elimina os cambios de _working_ e _staging_ con `--soft` elimina o commit pero non os cambios.

`git revert [hash] `. Revirte os cambios dun commit. Con `-n` non comitea a reversión.

`git show `. Mostra a informacion sobre o que pida, por exempolo un commit `git show [hash]`.

`git stash`. Garda os cambios e os oculta. `list` lista os stash apillados. `apply` aplica o último stash. `drop` borra o último stash.

`git status`. Monitorea o estado de seguemento dos ficheiros. Con `-s` lista ficheiroes e directorios.

`git tag [name] -m "[description]" ?[hash]`. Especifica a versión do proxecto usando una tag. Para actualizala en remoto hai que facer un `git push --tags`. Se engadimos o hash dun commit, quedan asociados. `-d` elimina un tag. `-a` anota a versión.

## Branching e merging

`git branch`. Mostra as branches existentes e sinala a actual.

`git branch [name]`. Crea unha branch. Con `-D` borra a branch. Cada feature debe ter a súa branch. Con `-m` modifica o nome dunha branch. Con `-a` mostra as branches remotas.

`git checkout -- [file name]`. Desfai unha modificación pendente de agregar ao _staging_.

`git checkout [hash]`. Vai a un commit.

`git checkout [name]`. Cambia á branch seleccionada. Con `-b` crea a branch e se move a ela.

`git grep [code]`. Busca código. Está baseado no comando `grep` dos sistemas unix. 

`git merge [name] *[name]`. Une a branch seleccionada coa master. `--abort` aborta a merge. Se non vai a haber conflitos pódese aplicar a estratexia **octopus** para facer un merge de varias branches ao mesmo tempo. Con `--squash` sintetiza os cambios mergeados nun único commit, que debe ser feito manualmente.

`git restore [name]`. Desfai os cambios nun ficheiro no _working_. Con `--staged` move o ficheiro do _stagint_ ao _working_. Con `--staged --worktree` desfai os cambios de todos os lados.

`git switch [name]`. Cambia de branch. Con `-c` móvese á branch creada. Con `-D` resetea a branch.  Con `--orphan` crea unha branch en branco (útil para branches de documentación). 

## Sharing and updating projects

`git clone [url] ?[directory]`. Clona un respositorio. Pódese engadir o diretorio de destino.git

`git fetch [remote]`. Verifica se hais cambios e os descarga do remto remoto.

`git push [remote] [branch]`. Actualiza o repositorio remoto cos cambios comiteados. Con `-u` , por exemplo `git push -u origin master`. Cando se fai un **push** traballa con correspondencia entre as branch local e remota, non sube todo o repositorio. Con `--all` sube todas branchs.

`git pull [branch]`. Actualiza o repositorio local cos cambios comiteados no remoto. Admite o parámetro `--rebase` ordenandoos os commits cronoloxicamente. Permite aplanar commits en local antes de seren pusheados. Rescribe o historial e é bastante interactivo. Se non está configurada a branch hai que especificala, por exemplo `git pull origin master`. 

`git remote add [name] [url]`. Vincula un repositorio cun repositorio remoto. Normalmente o nome é remote. 

## Inspection and comparison

`git bisect`. Percorre os commits e permite descargar aqueles que provocan un erro. Hai que iniciar unha sesión de "bisección" con `git bisect start` e péchase con `git bisect reset`.  Os commits márcanse con `git bisect bad` e `git bisect good [hash]` respectivamente. 

`git blame [path] | [hash]`. Identifica quen e cando realizou un cambio. 

`git log`. Listado de commits. Co parámetro `--oneline` mostra unha lista simplificada co commit. Con `--graph` pinta unha representación gráfica das branches. Con `--all` mostra os commits de todas as branches.  Con `-[number]` limita o número de post mostrados. Con `-p` ou `--patch` mostra as diferenzas entre os commits.

`get reflog`. Alias para git log. Mostra un log das referencias do HEAD.

## Conventional commits

É unha convención para escribir commits con relevancia comunicativa. Ao principio de cada commit vai a palabra clave (fix, feat, refactor, test, release, docs, chore), o _scope_, a descrición, o corpo e o rodapé. A referencia completa está en [Conventional commits](https://www.conventionalcommits.org/).

## Submódulos

Un submódulo consiste en importar un repositorio dentro de outra, como pode ser unha librería ou unha funcionalidade. En lugar de `git clone` úsase `git submodule` e conserva as mesmas funcionalidades que un repositorio, polo que se pode actualizar cun **pull**. Para que funcione un submódulo hai que descargalo, rexistralo e clonalo.
 * `git submodule add [url] [path]`. Por convención este código de terceiros gárdase no directorio `vendor`. O repositorio crea un ficheiro `.gitmudules` con metadatos e crea cada submodulo como un ficheiro de metadatos.
 * `git submodule init`. Rexistra un submódulo.
 * `git submodule update --remote`. Clona ou actualiza o submódulo. Con `--recursive` actualiza todos os submódulos.
 * `git pull --recurse-submoules`. Fai o mesmo que anterior.

## References

[Documentación oficial](https://git-scm.com/),
[Curso en makigas](https://www.youtube.com/watch?v=jSJ8xhKtfP4&list=PLTd5ehIj0goMCnj6V5NdzSIHBgrIXckGU)