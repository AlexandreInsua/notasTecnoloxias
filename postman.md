# Postman

## Introdución

Postman é un cliente API para desenvlver, testear, compartir e documentar APIs.

## Peticións (Requests)

Unha petición (_request_) é una petición http contra un endpoint dun servidor. As principais son 
- GET. Pide datos dun recurso.
- POST. Crea un novo recurso cos datos que se pasan como parámetro.
- PUT. Actualiza un recurso por completo cos datos que se pasan como parámetro.
- PATCH. Actualiza un recurso parcialmente cos datos que se pasan como parámetro.
- DETELE. Elimina un recurso.
- HEAD. Pide a cabeceira dun recurso.

## Coleccións

Unha colección é un grupo de peticións. Pódense ter carpetas no seu interior. As coleccións son as bases das operacións avanzadas.

## Variables

Son elementos que poden tomar diferentes valores para seren reusadas en diferentes lugares. Créanse no entorno global ou no entorn de cada colección. Invócanse mediante a chave dobre {{}}. Tamén se poden incluír nos scripts (que se escriben en JavaScript) mediante os métodos `pm.enviroment.get(string "name" )`. Tamen se poden setear con esta sintaxe `pm.enviroment.set("name", value)`.

## Entornos (Enviroments)

Son conxunto de variables, parellas de chaves-valor. Teñen o mesmo nome que as coleccións.

## Scripts

Son scripts que se executan antes dunha petición. Están escritos en JavaScript.

## Tests

Son probas unitarias que se executan despois da petición. Pódense crear en diferentes niveis.

## Debug

Debuguease a travén da consola. Mostra a traza dos script, peticións e respostas. Tamén hai disponibles unha devtools.

## Liña de comandos

Pódese usar a ferramenta Newmann, que é un paquete de node para establecer unha ferramenta de liña de comandos.

## Execución desde Jenkins

Crease un jbo cun stem en Jenkins que executa o comando de Newman para correr unha colección de peticións.

## Workspaces

Os espazos de traballo son áreas onde se agrupan, organizan e xestionan coleccións.

## Data Driving Testing

A partir de ficheiros csv oujson pódense executar peticións. É unha opción disponible cando se executa unha colección. Para os csv a primeira liña é o nome das variables e o resto son valores para cada petitión. O json debe ter un array de obxectos chave valor. Nos tests hai que usar a sintase `data.property` e `data.key`  ou `data["property"]` e `data["key"]`. As collecctións pódense executar remotamente a traves duna url que se crea a traves do boton share e usando Newman para tal fin.

## Peticións SOAP

Pódense executar unha petición SOAP, cunha petición POST, seteando as cabeceiras, usando a url e o texto do xml no corpo da petición.

## Encadenamento de API (API chaining)

Úsanse tests para gardar os datos na resposta nunha variable global que se reutiliza no petición. Hai un obxecto responseBody que se pode parsear con JSON.

## Autorizacións

As autorizacións realízanse na pestaña de Authentification para cada chamada. Por tanto pódese crear unha colección que se autentifiquen, logo obteñen datos e logo modifícanse combinando a executión da colección e o encademamento de API.