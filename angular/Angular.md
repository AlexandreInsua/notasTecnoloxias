# ANGULAR

## Introdución

Angular é unha plataforma de desenvolvemento (ou framework de frontend) construído en [Typescript](https://www.typescriptlang.org/). Angular estrutúrase en **components** (ficheiros typescript .ts) e **templates** (ficheiros html).
Un **component** e un bloque de codigo ts que inclúe unha clase e o decorador `@Component()` que especicifica un selector, un template e opcionalmente unha folla css.
Unha  **template** inclúe codigo html, variables interpoladas (interpolation con `{{variable}}`), e vencelladas (property bindind con `[property]="value`), eventos vingulados (event binding con `(event)="funcion()"`), e directivas.
Angular funciona mercé ao principio de **inxección de dependencias** en virtude da cal se declaran esas dependencias correndo a súa instanciación por conta da plataforma.
**Angular cli** é unha interface de liña de comamndos propia que permite realizar múltiples accións.
Angular fornece de varias librerías propias como son: o Router, Forms, HttpClient, Animations, PWA, Schematics.




INSTALAR ANGULAR
	npm install -g @angular/cli


INICIAR UN PROXECTO
	mkdir projectDirectory
	cd projectDirectory

COMANDOS DE ANGULAR CLI (command line interface)
	ng help				// Obviamente, axuda
	ng doc 				// lanza API de angular
	ng --version 		// versión de angular, node, SO e compoñentes de angular
	ng -v 
	ng serve			// arrinar a app
		--port=000		// establecer port
		--host			// establece host
		--check-host=disabled
						// deshabilita comprobación de porto
	ng install 			// instala unha app (descarga node modules se é necesario)

	ng build			// compila o proxecto no directorio /dist
		--prod	//
		--dev 			// compila entorno desenvolvemento
		--base-href ./	// modifica a base de link da web para deploy en host
		--bh ./
		--output-hashing none // quitar numero de hash nos ficheiros js 
		--output-path	// ruta de compilación, por defecto /dist
		--aot 			//



	ng new projectName 	// crea o scalfolding do proxecto
						// pregunta se crea un Router (ficheiro de rutas)
						// pregunta polo formato de follas de estilo, css ou preprocesados
	cd projectName 
	npm start 
	ng serve 			// arrinca o proxecto
		--port=000		// establece un porto diferente do predeterminado

	ng 	g(erate)		// xerar elementos
		c(omponent)		// compoñente: elemento con modelo de documento
						// app.module -> declarations
		s(ervice)		// servizo: elemento que contén un conxunto de funcións sen modelo de documento
						// app.module -> providers
		m(odule)		// módulos
						// app.module ->
		m app-router --flat --module=app 	// xeración de router

		p(ipe)			// pipes: filtros que se aplican a variables
			--module module_name 	// hai que especificar en que módulo se declaran 
		d(irective)		// directiva
			--module module_name 	// hai que especificar en que módulo se declaran 

APP.MODULE
	Declara todos os compoñentes e servizos que forman parte da aplicación.

APP.ROUTER
	Xestiona as rutas da aplicación. En angualar as rutas teñen unha estrutura nodular.
	Require RouterModule e Routes

A COMPOÑENTES DE ANGULAR

CICLO DE VIDA DAS COMPOÑENTES
	Os hooks son funcións que permiten acceder a diferentes momentos da compoñente:

	- constructor()
	- ngOnChanges. Execútase cada vez que se detecta un novo valor de entrada. 
	- ngOnInit. Inicializa o contido da compoñente e só se executa unha vez. Non ten acceso ao DOM porque aínda non está cargado.
	- ngDoCheck. Execútase despois do init e cando detecta cambios na compoñente.
		· Os ngAfter afectan ao template.
			ngAfterContentInit. Execútase cando o contido se carga.
			ngAfterContentChecked. Execútase cando algo do contido se modifica.
			ngAfterViewInit. Execútase cando se cargan view e viewchild.
			ngAfterViewChecked.  Execútase cando se modifica view e viewchild.
	- ngOnDestroy. Execútase cando se destrue a compoñente.

PIPE
	Predeseñadas : uppercase, lowercase

DIRECTIVAS
	Esquema que modifica os elemento do DOM
	- de compoñente
	- de estrutura html. 
	- de atributos. 

DIRECTIVAS DE ESTRUTURA 
	ngIf. 
	 	*ngIf=nome_da_variable
	ngFor
		*ngFor let elemento of lista_de_elementos
	ngSwitch
		[ngSwitch]="variable" 
		*ngSwitchCase="value" 
		*ngSwitchDefault


INPUT
	Decorador para entrada de datos nunha compoñente filla desde a compoñente nai
	import { Input } from '@angular/core'
	ts 		 		@Input('etiqueta') variable;
	html parent 	[etiqueta]="valor"	

OUTPUT
	Decorador para a saida de datos nunha compñente nai desde a compoñente filla. Necesitamos crear un evento.
	child 
		ts		import { Output, EventEmitter } from angular core
				@Output() variableEmitida = new EventEmitter<type>();
				funcionEmitir(){this.variableEmitida.emit(dato emitido)}
		html 	()=funcionEmitir()

	parent
		html 	 (variableEmitida)="funcionRecibir($event)"
		ts 		funcionRecibir(e){ // e }

RENDERER E LISTENER - Interactividade
Render - Obxecto que permite manexar elmentos do DOM.

OBSERVABLES / SUBSCRIPCIÓNS
	Un observable é obxecto produto dunha petición (equivalen ao callback de js vainilla)

VIEWCHILD
	ViewChild @angular/core
	@ViewChild('selector') elemento; 
	Vistas herdadas. En Angular cada etiqueta de html considérase como unha vista. Cada elemento pódese identificar asignado un id coa sintaxe #selector. 

INTERFACES
	Modelo de datos (ao igual que unha clase) que inclúe métodos abstractos e propiedades constantes.

ANIMÁCIÓNS
	Similares ás animacións con css, pero se crean desde código ts. Deséñanse unha animación e cárgase no array animations na compoñente. Na vista establecese o trigger que o lanza.

	app.module
		import { BrowserAnimationsModule } from '@angular/platform-browser/animations'
		imports: 
	component ts
		import { trigger, state, style, animate, transition } from '@angular/animations';
		@Component
		animations: [
		trigger('nome-do-trigger'), 
			state('nome do estado', style({ JSON })),
			trasition('inicial => final ', animate('animacion')),
			]
		var estado: string;
	component html
		[@nome-do-trigger]="estado"

ANIMÁCIÓNS CON KEYFRAMES
	Os keyframes son puntos de ruptura nunha animacion. Para programar unha transición con keyframes úsase a seguinte sintaxe, onde a duración vai en ms e o offset indica a proporcion do tempo de 0 a 1: 
	transition('inactive => active', [animate(000, keyframes([
        style({propiedade: 'valor', offset:0}),
        style({propiedade: 'valor', offset:1}),
      ]))]),

ANGULAR ELEMENTS
	Ferramenta de A6+ que permite xerar compoñentes web component/custom components para Angular.
	Instálase a libraria
		ng add @angular/elements
	Compílanse a compoñente para independizalo  de ng

ANGULAR MATERIAL
	INTRO
		Kit de compoñentes de deseño previamente testeadas. Impórtase como unha librería. Son módulos que se importan con npm.
		
		Instalación de dependencias
		OLLO é importante que coincida a version de angular @8.0.0
		npm install --save @angular/material @angular/cdk @angular/animations
		
		app module ts --> importación 
		import { BrowserAnimationsModule } from '@angular/platform-browser/animations'
		
		styles css --> importación de estilos
		@import '~@angluar/material/prebuilt-themes/indigo-pink.css';

		As compoñentes impórtanse no app module e úsanse no html.

	CAMBIAR CORES Theming
		Créase un ficheiro custom.scss (SAX) na raíz.
		copy-paste de paleta de documentación.
		Modifícanse os valores das variables seguindo o sistema predefinido.
		en angular.json styles incluir o ficheiro  npm start

	CAMBIAR TIPOGRAFIAS
		Class mat-typography chama ao valor definido en material
		chamada index.html con link

		En custom.scss pásaselle unha configuración de tipografía nunha función
			$custom-typography: mat-typography-config{ $font-family: "serif",
			$button: mat-typography-level{10px, 30px, 300}};

	MÚLTIPLES TEMAS
		En appComponent class="alternative-theme"
		En custom.scss 
		.alternative-theme {
			/* Inclúese o código de tema COS NOMES DAS VARIABLES MODIFICADOS para que non se pisen. */
		}

	BOOSTRAP 4
		Incorporar boostrap
			npm i --save bootstrap jquery popper.js 
			convertimos o styles.css a scss
			mudamos o nome en angular.json -> npm install
			en styles.scss importamos 
				@import '~boostrap/scss/bootstrap';
				@import '~boostrap/scss/bootstrap-reboot';
				@import '~boostrap/scss/bootstrap-grid';

	ANGULAR MATERIAL INTERACCIÓNS
		As interaccións entre compoñentes programanse no ts da compoñente onde están programados.	
RXJS

TESTING


LIBRERÍAS JS DE TERCEIROS
	Para implementar unha libería de terceiros, por exemplo JQuery, hai varias alternativas:
		1º.- Que esté incluída nos módulos de node
				import { modulo } from 'modulo'
		2º.- Que a libraría teña versión npm
				npm install --save nome_libraria
				import * as modulo from 'modulo'
		3º.- Gardar a librería js en assets
				npm install @types/node --save-dev 
				configúrase tsconfig.ts en types ["node"]
				const modulos = require('assets/modulo.js')
		4º.- declarala en index.htlm
				declare var modulo;

APACHE CORDOVA
	Apache Cordova é un framework permite crear app multiplataformas con tecnoloxías web. Está pensado para dispositivos móbiles. O proxecto de Cordova créase dentro do proxecto de angular. 

ANGULAR ELECTRON
	Electron é un framework que permite crear app de escritorio con tecnoloxías web. A idea é desenvolver unha aplicación web en angular e logo compilala. 

ANGULAR UNIVERSAL
	Angular universal. Ferramenta que permite prerrenderizar as compoñentes de aplicación para seren vistos por boots. Angular 7 xa incorpora esta funcionalidade de xeito nativo.

SEO


BOAS PRÁCTICAS 




## PROBAS UNITARIAS

Karma + Jasmine

Seguindo a metodoloxía TDD, primeiro se escriben os test en base aos requirimentos que a app de debería ter e logo se escribe o código que satisfai os requisitos e pasan as probas.

As probas unitarias testean a funcións públicas dun compoñente. Estas deberían ser funcións puras de retorno de valor.
Xunto con cada compoñente hai un ficheiro .spec.ts que conten as probas unitarias.


### Filosofía dos 3 A
Preparar, actuar e verificar. (En inglés Arrange, Act, Assert). 
Prepárase un escenario para unha batería, lánzase a función que queremos testar e verificamos o resultado. 

1. Impórtase o ficheiro que se quere testear
```javascript
import { Component } from './component';
```

2. As baterias de test agrúpanse mediante a sintaxe `describe`. Se a lóxica é moi complexa, dentro da bateria de probas de cada compoñente, cada función tería tamén o seu propio describe

```javascript
describe('Tests for AppComponent', ()=>{ 
	// Aquí van os diferentes test.

	describe('Tests for myFunction', ()=>{ 
	// Aquí van os diferentes test.
	})
})
```

3. Cada test vai dentro dunha delararcion **it** (de _item_) que inclúe unha descrición e unha función. Dentro da función instánciase o componente que inclúe a función, execútase a función e compróbase o resultado.

```javascript
it('should return nine', ()=>{
	// arrange
	let c = new Component();
	// act
	let result = c.myFunction(a, b);
	// assert
	expect(result).toEqual(9);
});
```
### beforeEach
Trátase dunha función de preparación para cada item.

por exemplo 
```javascript
let c;
beforeEach(()=>{
	c = new Component();
});
```
### Focus
Un foco é unha técnica que consiste en correr unicamente algunha batería de probas ou algún item en concreto. Para focar un elemento, agrégase un f ao describe ou ao item: `fdescribe` ou  `fit`.


### Mocking
Simulación controlada de obxectos que imitan o comportamento dos obxectos reais.


### Api básica de Jasmine
#### Matchers (comparadores)
- expect(element).isNan(); é un non número
- expect(element).toBeDefined(); variable definida
- expect(element).toBeUndefined(); variable indefinida
- expect( 1 + 2 == 3).toBeTruthy(); é verdadeiro
- expect( 1 + 2 == 4).toBeFalsy(); é falso
- expect( 5 ).toBeLessThan(10); menor que 
- expect( 5 ).toBeGreaterThan(10); maior que 
- expect( 'string' ).toMatch(/regex/); contén a regex
- expect( collection ).toContain(element); o array conten o elemento ? que pasa cos obxectos.


### Testear servizos (implica mockear un http )




### Comando de probas
`npm test` - Corre `ng test`. 
`ng test`- Corre as probas, abrindo un navegador e mantén o navegador aberto.
`ng test --watch=false` - Corre as probas, abrindo un navegador e pecha o navegador aberto 
despois da execución.
`ng test --single-run` - deprecado

`ng test --code-coverage` - xenera o reporte de cobertura de test (crea a carpeta de coverage)

`http-server coverage` - lanza un servidor para mostrar o informe html (require ter instalado o paquete de ndoe http-server)



PROBAS DE INTEGRACIÓN

PROBAS E2E

# ACTUALIZAR VERSIÓN ANGULAR (GLOBAL)

  1. Desinstalar os paquetes anteriores de Angular Cli. `npm uninstall -g @angular/cli`

  2. Borrar a caché `npm cache clean --force`

  3. Instalar a última versión de angular  `npm install -g @angular/cli@latest`

2020.07.30. Actualizo a versión 12.1.4. Saen 3 warnings. Creo un proxecto de cero parace ir ben.

# ACTUALIZAR PROXECTO

Para actualizar un proxecto o mellor é ir actualizando de versión a versión. A web de Angular ten unha sección específica. 

2020.07.30.

Actualizo un proxecto da 9 á 10. 
Hai que borrar o package-lock.json
O ng update require un repositorio limpo.
 `ng update @angular/cli @angular/core`
Hai que facer un `npm install --force` para faga a instalación de dependencias.
		
Actualizo un proxecto de 10 a 11. 

Actualizao un proxcto de 11 a 12.
Na versión 12 cambia a compilación a produción a `ng build --configuration production`.

# REFERENCIAS
Moldeo Interactive Angular en español
://www.youtube.com/watch?v=k1uM6YeEx6g&list=PLHgpVrCyLWApLDoezmOfrUXb-IMoDs5Ls&index=1


Validadores personalizados para formularios reactivos
https://blog.angular-university.io/angular-custom-validators/?utm_source=newsletter&utm_medium=email&utm_campaign=angular_custom_form_validators_complete_guide&utm_term=2021-06-12


Estratexia de captura de erros en observables e funcionamento do retryWhen
https://blog.angular-university.io/rxjs-error-handling/?utm_source=newsletter&utm_medium=email&utm_campaign=rxjs_error_handling_complete_practical_guide&utm_term=2021-06-21

Guías de angular
https://blog.angular-university.io/
ngIf
https://blog.angular-university.io/angular-ngif/?&utm_source=newsletter&utm_medium=email&utm_campaign=did_you_know_about_all_these_features_of_angular_ngif&utm_term=2021-08-18
	

importar un mapa de leaflet
https://www.digitalocean.com/community/tutorials/angular-angular-and-leaflet