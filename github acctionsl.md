# GITHUB ACTIONS

Son accións que se poden programar en repositorios de Github para implementar accións de CI/CD.

Os scripts de teñen o formato yaml. [wiki](https://es.wikipedia.org/wiki/YAML)
e pódese crear varios workflows para o mesmo repo.

En yaml os elementos aníñanse mediante a identación e os arrays teñen dobre sintaxe, con guión ou con corchete.

Deben ter un nome `name`, un evento que os lanza e as tarefas que realiza `job`.

Cada `job` ten un nome, un entorno de execuón e uns pasos `steps`. Cada job pódese lanzar nunha máquina independente facer que uns agarden por outros e para poder paralelizalos co que se aforran recursos. Poden compartir información que se garda un _artifact_. Tamén se poden cachear dependencias.

Cada paso ten un nome `name` e acións que realiza `run`, que veñen a ser comandos.

Por defecto as máquinas está valeiras, polo que o primeiro paso é pasarlle o proxecto de repo.

As accións admiten recursividade.

Cando teñen éxito devolven 0, en caso contrario, un valor que soe ser o código de erro.

Existe un marketplace onde xa hai accións predefinidas que poden ser invocadas e que aforran escribir código.

Hai accións para facer todo tipo de tarefas: evitar builds redundantes, lanzar tarefas propias, paralelizar test e2e, facer deploys, etc...

Os _secrets_ son variables de configuraición que poden ser invocadas nas actions. Está nas **Setings** do repo.

Existe un obxecto global _github_ que contén toda a información do contexto e tamén pode ser invocado nas accións.

Para protexer branches pódese configurar nas **Settings** no apartado **branches**.


- `npm i --no-audit --no-fund --no-optional` skipea comprobacións durante o install

- `npx cypres run ` corre o comando _on fly_ e aforra minutos

## Refencias
Tuto de Midudev [youtube](https://www.youtube.com/watch?v=sIhm4YOMK6Q&t=1s)

````yaml
# exemplo
# nome do workflow
name: name of workflows

on:
  # evento de push
  push:
    # en ramas
    branches:
      - "**" # todas
    # en pull request
    pull_request
      -"**" # todas
jobs:
  # nome do traballo
  build;
    # entorno de execuón
    runs-on: ubuntu-latest
    # pasos
    steps:
      - uses: actions@/setup-node@v3 # acción de github actions
        with:
          node-version: 16 # argumento para a configuraión do wf
      - name: Show files # comnando de shell
        run: ls -l
```
