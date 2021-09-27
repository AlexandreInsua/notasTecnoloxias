probas unitarias - unidade de codigo clase ou función
probas de integración - integración de compoñentes 
probas de aceptación e2e - de caixa negra uso de GUI 



# TESTING EN ANGULAR +2
Testear a aplicación Angular axuda a comprobar que funciona como se agarda.

## Prerrequsitos
Antes de escribir tests para a aplicación Angular, deberíase ter coñecemento básico de HTML, CSS, JavaScript, fundamentos de Angular e Angular CLI. 
A documentacón de testing fornece de trucos e técnicas  para tests unitarios e de integración en aplicacións de ángular a través dunha aplicación simple creada con Angular CLI. Esta aplicación de exemplo é moi parecida ao on tutorial _Tour of Heroes_.

## Preparación das probas
Angular CLI descarga e instala todas as cousas que necesitas para testear unha aplicación Angual co framework de testing Jasmine.
O proxecto que se crea vía CLI está automaticamente preparada para testear. 
Comandos para lanzar as probas
`ng test` constrúe a app no _modo de observación_ (watch mode) e lanza o runner de probas Karma.

A consola mostrará a información das probas.
A última liña do log é a máis importante. Morstra a informació de éxito dos test que correu Karma.
Tamén se abre unha instancia de Chrome que mostra a saída dos test en formato HTML.
A maior parte da xente encontra a saída por navegador máis doada de ler que a consola. Podes facer clis na fila do test para volver só esa proba ou facer click nunha descriión para volver a correr o grupo seleccionado.
Mentres tanto, o comando `ng test` está observando os cambios.
Pódese facer un cambio menor nunha compoñente e gardar. Os tests volverán a correr, o navegador refrescarase e aparecerá un novo resultado das probas.

## Configuración
O CLI encárgase da configuración de Jasminne e Karma automaticamente. 
Pódese axustar as opcións editando o ficheiro `karma.conf.js` na raíz do proxecto e `test.js` no directorio `src/`.
O ficheiro `karma.conf.js` é o ficheiro de configuració parcial de karma. O CLI contrúe a configuración en tempo de execución en memoria, baseandose na estrutura da aplicación espedificada no ficheiro `angular.json` xunto con `karma.conf.js`.

### Outros frameworks de test
Tamén se poden facer probas unitarias nunha aplicación Angular con outras librerías e runners. Cada librería e runner ten o seu propios procedementos de instalación, configuración e sintaxe.

### Nome de ficheiros de test e localación
Os ficheiros de test teñen a extensión **spec.ts** e cada vez que se xera un compoñente, o CLI crea o ficheiro de test. Así o `app.component.ts` e o `app.component.spec.ts` son irmáns no mesmo directorio. Convén adoptar dúas convencións canto a ficheiros de test.

#### Colocar o ficheiro spec preto do ficheiro que proba.



https://medium.com/boolean-chile/creando-pruebas-unitarias-para-un-servicio-en-angular-807732534d78

https://medium.com/boolean-chile/serie-introducci%C3%B3n-a-las-pruebas-de-software-c42f2d6db876

https://angular.io/guide/testing

https://github.com/ionic-team/ionic-unit-testing-example

https://github.com/ionic-team/ionic-unit-testing-example

https://enappd.com/blog/beginners-guide-to-ionic-angular-unit-testing-part-1/151/

https://github.com/ionic-team/ionic-weather-starter