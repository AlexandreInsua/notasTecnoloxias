https://101node.io/blog/how-to-write-production-ready-node-express-app/

# Iniciar un proxecto
$ npm init

Cando se usa un proxy as cabeceiras debe ser idénticas na api e no proxy para evitar problemas de cors.

# Actualizar Node

1. Instalar última versión LTS seguindo as indicacións da web (https://nodejs.org)[https//nodejs.org].

    2021-07-30. Instalo a versión 14.17.4. Adicionalmente Instala python e python3 3.9.6 porque necesita compilar parte do código.
    2022-02-18. Instalo a versión 16.14.0. Actualiza a python 3.10.2.

2. Actualizar npm globalmente 

    `$ npm install -g npm@latest`

    2021-07-30. Instalo a versión 7.20.3.
    2022-02-18. Inatalo a versión 8.5.1.

3. Borrar a caché de npm

    `$ npm cache clean --force` A flag é necesaria.

    



