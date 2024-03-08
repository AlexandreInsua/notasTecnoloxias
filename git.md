# NOTAS DE GIT / GITHUB / GITLAB

## Introdución

**Git** é un sistema de control de versións distribuído, que permite facer o seguemento de cambios nun proxecto rexistrando cada cambio en _commits_. Un _repositorio_ é un conxunto de ficheiros coas sáus versión e historia de cambios. O repositorio é diference do _workspace_ que é a carpeta que o engloba dentro do sistema de ficheiros e que pode conter outros ficheiros .git ou outros ficheiros.

Git está baseado no _**commit**_ que é unha instantánea do estado dos ficheiros do repositorio nun momento dado. Non funciona sobre directorios (Se queremos rexistrar un, debemos crear dentro un ficheiro valeiro). Os commits orgánizanse nunha liña de tempso denominada _branch_.

Por outra parte **Github** é un servizo de hospedaxe de repositorios git con servizos adicionais.

Cando se inicializa un repositorio co comando `git init [repo name]` crea un directorio e un repositorio de git. No seu interior hai un ficheiro .git.

O sistema traballa con tres estados diferentes:

- O _working directory_: que contén todos os ficheiros e directorios da aplicación.
- A _staging area_: que é a área de preparación dos traballos e onde de fai seguemento dos ficheiros monitorizados (_tracked_).
- O _repository_: que contán os cambios comfirmados (_commited_). Un repositorio remoto pode ser considerado como un estado máis.

O fluxo de traballo constes en realizar un cambio nun ficheiro no directorio de traballo, pasalo á área de preparacion con `git add` e pasalo ao repositorio con `git commit`. Podése devolver un ficheiro da área de preparación á directorio de traban con `git rm --cached [file name]`.

Git traballan con _branches_, que son etiquetas que se lle dá a un conxunto de commits. En xeral trabállase con unha branch principal, estable, e outras de desenvolvemento. Posteriormente, vanse fusionando as branches de desenvolvemento coa principal.

Hai 3 teipos de fusión (merge):

- _fast-forward merge_. É o caso máis simple. Ocorre cando non se detecta taballo adicional na branch pai. Simplemente lévanxe os commits a esa rama pai.
- _automatic merge_. Ocorre cando non se detectan cabios conflitivos. Nese caso creáse un novo commit de merge preservando as dúas ramas.
- _manual merge_. Cando git detecta cambios conflitivos entra nun estado especial de merge conflitivos que impide commitear o merge ata que non se resoven os cambios. Feito isto, creáse o commit de merge.

Git incorpora os cambios dunha branch noutra se non hai conflitos. Cando hai cambios simultáneos nas mesma liñas en ramas diferentes inténtase fusionar unha noutra, git non é capaz de facelo se xeito automatico e entro en estado de conflito. No prompt da terminal aparece ao lado da bransch a palabra `!merging`.
Cando se produce un conflito git pinta no ficheiro o texto conflitivo nas branches. Hai que escoller entre ambos e comitear os cambios.

As páxinas git diferencian varias estratexias de merge. **Merge commit** é aquela que crea un commit para a merge (a estándar). **Merge rebase** fai un rebase, de forma que os commits da branch mergeada quedarán por riba dos anteriores. **Merge squash** implica que todo o diff (con diferentes commits) pasa a ser un único commit.

Git pode marchar un pundo do repositorio establecendo unha etiqueta (_tag_) nun pundo determinado. Hai dous tipos de tag:

- _tag lixeira_. Non ten información asociada.
- _tag anotada_. Ten información asociada.

Ademais de branchs, tags e outras etiquetas para os commits, temos os punteiros. O máis importante é **HEAD**, que é o último commit da rama actual.

O almacén de cambios (_stash_) funciona com unha pilla LIFO. Pódense ir gardando os cambios pero só se pode recuperar de un en un pero non se pode recuperar o seguinte nun espazo de traballo co cambios pendentes: ou se eliminan ou se confirman.

Para obter o enésimo commit anterior a un dado úsase o til: `[hash]~n`.

Os repositorios git teñen un ficheiro `gitignore` que lle indican a git ficheiros que debe ignorar. Normalmente son ficheiros de credenciais, ficheiros compilados, temporais ou de dependencias. Cada unha das súas liñas son as rutas dos ficheiros.

## Instalación e axuda

En Windows, descargar o instalador e seguir as instrucións.
En Linux da familia Debian, `apt-get install git`.

`git --version`. Mostra a versión actual.
Os comandos adminten un parámetro `-h` que pinta o manual do comando.

## Configuración

A configuración mínima exixe setear o nome de usuario e o correo electrónico. A bandeira `--global` establece que se refire á configuración global. Cando non se usa o comando, os cambios aplícanse localmente ao repositorio onde se estea.

`git config --global --list`. Mostra a configuración.

`git config --global -e`. Editoa o ficheiro de configuración global. O ficheiro é accesible a traves de `cat ~/.gitconfig`

`git config --global user.name "[username]"`. Configuración global de usuario.

`git config --global user.mail "[mail]"`. Configuración global de correo electrónico.

`git config --global core.editor "[editor]"`. Configura o editor por defecto. E.g.: para notemap++ `git config --global core.editor "notepad++ -multiInst -no-session"`.

`git config --global diff.tool "[name]"`. Establece a ferramenta para mostrar os cambios. E.g.: `git config --global diff.tool "p4merge"`.

`git config --global diff.tool.[name].path "[path]"`. Establece o path para a ferramenta de cambios.

`git config --global diff.tool.[name].prompt false`. Obvia a saída da por termina da ferramenta de cambios.

`git config --global merge.tool "[name]"`. Establece a ferramenta para realizar as fusións. E.g.: `git config --global merge.tool "p4merge"`.

`git config --global merge.tool.[name].path "[path]"`. Establece o path para a ferramenta de fusións.

`git config --global merge.tool.[name].prompt false`. Obvia a saída da por termina da ferramenta de fusións.

`git config --global --get-regex alias`. Mostra os alias creados.

`git config --global alias.[alias] '[comando]`. Crea un alias para un comando.

`git config --global --unset alias.[alias]`. Elimina un alias.

`git config --global init.defaultBranch [name]`. Establece o nome da branch principal por defto.

## Creación de repositorio

`git init`. Inicializa ou reinicializa un repositorio.

## Comandos básicos

`git add`. Engade ficheiros á _staging area_. Con `.` engage todos. Con `-p` ou `--patch` permite seleccionar os cambios que se van engadir, pero non aplica a ficheiros novos. Con `-A` actualizar todos os ficheiros. Con `-u` Actualiza os ficheiros xa trackeados Marcado de ficheiros A: agregated, M: modified, U: untracked.

`git apply`. Permanece á escoita do que metemos por teclado, como se for unha consola.

`git commit`. Engade os ficheiros da _staging area_ ao repositorio local. Necesita `-m` para agregar descripción. Con `-am` engade todos os ficheiros modificados ou borrados pero non os pendentes de seguir, por exemplo os que se crean de novo. Con `--amend` abre a edición do último commit. Con `-S` permite asinar o commit.

`git diff [hash1] [hash2]`. Compara as diferenzas entre dous commits, onde o primeiro é o orixinal (como main) e o segundo o de traballo (como developtment). Lista de modificacións que non están incluídas na _staging area_ ou entre varios commit. Moras as fontes de entrada, os metdados, os marcadores dos cambios e os fragmentos de diferenzas. Como git traballa por liñas, se se modifica unha, mostra un borrado e unha inserción. Pódese engadir o parámetro `--color-words` para que mostres as diferanzas palabra a palabra. Podese gardar a súa saída nun ficheiro .patch para estudar os cambios.

`git reset [hash]`. Utilízase para mover o HEAD a un commit específico, polo que se elimian os commits posteriores nesa branch. (hai que usalo con precaución para evitar conflitos). Se non se especifica un commit, revirte o último _add_ Deixa os cambios na _working directory_ Con `--hard` elimina os cambios de _working directory_ e _staging area_. Con `--soft` elimina o commit pero non os cambios dos _working directory_. Con `--mixed` aplica os cambios só no directorio de traballo, os cambios confirmados non se perden.

`git revert [hash] `. Revirte os cambios dun commit. Con `-n` non comitea a reversión.

`git stash`. Garda os cambios e os oculta. `list` lista os stash apillados. `apply` aplica o último stash. `drop` borra o último stash. `pop` recupera o cambio no stash e o borra.

`git status`. Monitorea o estado de seguemento dos ficheiros. Con `-s` lista ficheiroes e directorios.

`git tag`. Especifica una tag lixeira.
`git tag [name] -m "[description]" ?[hash]`. Especifica unha tag no proxecto. Para actualizala en remoto hai que facer un `git push --tags`. Se engadimos o hash dun commit, quedan asociados. `-d` elimina un tag. `-a` anota a versión. `-f` modifica unha tag anotala

## files

`git mv [name1] [name2]`. Cambia o nome dun ficheiro.

`git rm [name]`. Elimina un ficheiro.

## Branching e merging

`git branch`. Mostra as branches existentes no repositorio e sinala a actual.

`git branch [name]`. Crea unha branch. Con `-D` borra a branch. Cada feature debe ter a súa branch. Con `-m` modifica o nome dunha branch. Con `-a` mostra as branches remotas.

`git checkout -- [file name]`. Retrotrae os cambios do ficheiro ao último commit pos que desfai unha modificación pendente de agregar á _staging area_.

`git checkout [hash]`. Vai a un commit.

`git checkout [name]`. Cambia á branch seleccionada. Con `-b` crea a branch e se move a ela.

`git grep [code]`. Busca código. Está baseado no comando `grep` dos sistemas unix.

`git merge [name] *[name]`. Une a branch seleccionada coa master. `--abort` aborta a merge. Se non vai a haber conflitos pódese aplicar a estratexia **octopus** para facer un merge de varias branches ao mesmo tempo. Con `--squash` sintetiza os cambios mergeados nun único commit, que debe ser feito manualmente.

`git restore [name]`. Desfai os cambios nun ficheiro no _working_. Con `--staged` move o ficheiro do _stagint_ ao _working_. Con `--staged --worktree` desfai os cambios de todos os lados.

`git switch [name]`. Cambia de branch. Con `-c` móvese á branch creada. Con `-D` resetea a branch. Con `--orphan` crea unha branch en branco (útil para branches de documentación).

## Sharing and updating projects

`git clone [url] ?[directory]`. Clona un respositorio. Pódese engadir o diretorio de destino.git

`git fetch [remote]`. Verifica se hai cambios e os descarga do remoto remoto.

`git push [remote] [branch]`. Actualiza o repositorio remoto cos cambios comiteados. Con `-u` , por exemplo `git push -u origin master`. Cando se fai un **push** traballa con correspondencia entre as branch local e remota, non sube todo o repositorio. Con `--all` sube todas branchs.

`git push [remote] :[branch | tag]`. Borra unha rama ou unha tag no repositorio remoto.

`git pull [branch]`. Actualiza o repositorio local cos cambios comiteados no remoto (fai un `fetch` e `merge` dos cambios). Admite o parámetro `--rebase` ordenandoos os commits cronoloxicamente. Permite aplanar commits en local antes de seren pusheados. Rescribe o historial e é bastante interactivo. Se non está configurada a branch hai que especificala, por exemplo `git pull origin master`.

`git remote add [name] [url]`. Vincula un repositorio cun repositorio remoto. Normalmente o nome é remote.

## Inspection and comparison

`git bisect`. Percorre os commits e permite descargar aqueles que provocan un erro. Hai que iniciar unha sesión de "bisección" con `git bisect start` e péchase con `git bisect reset`. Os commits márcanse con `git bisect bad` e `git bisect good [hash]` respectivamente.

`git blame [path] | [hash]`. Identifica quen e cando realizou un cambio.

`git log`. Presenta a lista dos commits que forman parte do repositorio, o **historial**, por orde cronolóxica inversa. Co parámetro `--oneline` mostra unha lista simplificada co commit. Con `--graph` pinta unha representación gráfica das branches. Con `--all` mostra os commits de todas as branches. Con `-[number]` limita o número de post mostrados. Con `-p` ou `--patch` mostra as diferenzas entre os commits.

`git ls-files`. Mostra os ficheiros que están a ser trackeados.

`get reflog`. Mostra un log das referencias do HEAD. Isto é o rexistro das referencias de git que inclúe dotods as accións que comban as referencias de HEAD e as referencias das ramas, com cambios de HEAD, de rama, reseteos, commits e merges.

`git show `. Mostra a informacion sobre o que pida, por exempolo un commit `git show [hash]?`. Se non se indica nada mostra a información du último commit.

## Conventional commits

É unha convención para escribir commits con relevancia comunicativa. Ao principio de cada commit vai a palabra clave (fix, feat, refactor, test, release, docs, chore), o _scope_, a descrición, o corpo e o rodapé. A referencia completa está en [Conventional commits](https://www.conventionalcommits.org/).

## Submódulos

Un submódulo consiste en importar un repositorio dentro de outra, como pode ser unha librería ou unha funcionalidade. En lugar de `git clone` úsase `git submodule` e conserva as mesmas funcionalidades que un repositorio, polo que se pode actualizar cun **pull**. Para que funcione un submódulo hai que descargalo, rexistralo e clonalo.

- `git submodule add [url] [path]`. Por convención este código de terceiros gárdase no directorio `vendor`. O repositorio crea un ficheiro `.gitmudules` con metadatos e crea cada submodulo como un ficheiro de metadatos.
- `git submodule init`. Rexistra un submódulo.
- `git submodule update --remote`. Clona ou actualiza o submódulo. Con `--recursive` actualiza todos os submódulos.
- `git pull --recurse-submoules`. Fai o mesmo que anterior.

## References

[Documentación oficial](https://git-scm.com/),
[Curso en makigas](https://www.youtube.com/watch?v=jSJ8xhKtfP4&list=PLTd5ehIj0goMCnj6V5NdzSIHBgrIXckGU)
