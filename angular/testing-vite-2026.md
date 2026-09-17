# TESTING DE ANGULAR CON VITE

## Intro

Vitest é un framework de testing para JS/TS deseñado para funcionar de maneira nativa no ecosistema de Vite. O seu obxectivos principal é unha execución de test rápida con unha experiencia de desenvolvmento semellante a Jest pero aproveitando os módulos de ES e o pipeline de Vite. Funciona como un test runner que se integra ao grafo de módulos de Vite.
O ecosistema de Vite baséase nun enfoque moderno de desenvolvemento frontend no que o código se serve directamente como módulos de ES durente o desenvolvemento, evitando procesos de building completos en cada cambio. O sistema inclúe un servidor de desenvolvemento moi rápido, con optimización de dependencias mediante esbuild e un sistema extensible de plugins inspirados na arquitectura de Rollup. Iso permite que a mesma infra se usa para desenvolver apps, executalas e preparalas para producción.
A pipeline de Vite funciona como unha cadea de transformacións que se executa cada vez que se executa cada vez que se solicita un módulos. Cando o navegador ou runtime pide un ficheiro, vite resolver a ruta do módulo, analiza as súas dependencias e para o código por diferentes plugins que poden transformalo. O resultado é código JavaScript listo para executar, xerado baixo demanda e cacheado para execución posteriores.
Sobre esta infraestrutura constrúese Vitest test que reutiliza o servidor e a pipeline de Vite para executar tests sun un paso previo de compilación. Mediante Vite-Node, Vitest
Vitest pode cargar módulos, aplicar tranformacións e aplicalas en Node, distribuíndo test en múltiples testers para executalos en paralelo. Como o grafo de módulos de Vite pode detectar cambios no código e relanza automaticamente só os test afectados.
Vitest organiza os seus tests en suites mediante _describes_ e tests mediante _its_. Admite os operadores _skip_, _todo_, _only_, _skipIf_...

## Spyes

Un **spy** é un obxecto observador doutro obxecto e créase coa utilidade _vi.spyOn(object,method)_ e admite asercións habituais. Non modifica o comportamento da función a non ser de que se configura explicitamente.

## Mocks

Un **mock** reempraza o comportamento dun obxecto. ESta funcionalidad permide illar dependencias en tests unitarios. Contrúese un spy e mockease o retorno en cuxo caso o funcionamenteo interno do método non é executado, está bypaseado, é ignorado.

## Pure mock

Un **mock puro** non actúa sobre un obxecto existente, senón que se crea de cero usando a sintaxe `conts mock = vi.fn()` e mockéase o retorno.

## Limpeza

Para illar o estado dos mocks en cada test, pódese limpar o historial deo mock co método `mockClear()`.Temos dúas alternativas `clear` limpa o estado do mock pero mantén a implementación, mentres que `reset` limpa tamén o comportamento do mock. `Restoring` restaura un spy e o desconecta do obextoa o que está atado.
Idealmente os mocks non se deberían usar entre tests. Caso de partillalos nun _describe_ ou nun ficheriro de utilidades hai que estudar que estratexa é a máis adecuda. Vitest ten utilidade para limpar mocks no `afterEach` na súa configuración.

## Testing en compoñente

Partimos de que na suite de tests creamos unha instancia de Angualar da clase **TestBed** que necesita unha configuración asíncrona para cada tests. Este wrapper de Angualr ten o método `createComponent` que devolve a **fixture** que é un wrapper do compoñente que implementa as funcionalidade de Angular para testing. O **debugElement** é unha abstrcción que representa o dom do compoñente e permite interactuar co dom coa api da Angular no lugar da estándar. **component** é a representación da clse do compoñente. É importante disparar a detección de cambios para cada test cando menos unha vez.
Para configurar unha suite de test dun compoñente precisamos:

1. Declarar unha fixture. Trátase dun obxecto de utilidadades de testing qie cpmtem unha instancia do compoñente (da clae) e do dom renderizado, mais a api de Angular. Pode disparar a detección de cambios e expón utilidades de inspección.
2. Declarar unha instancia do compoñente
3. Dispor de mocks para os inputs obrigatorios.

A configuración do setup faise para cada test mediante a función _beforeEach()_ usando o obxecto _TesBed_ e `configureTestingModule()` que recibe un obxecto de configuración. Para comezar impórtase o compoñente e compílanse os compoñentes. Esta operación é asíncrona.
A continuación instanciamos o fixture con `TestBedCreateComponent(component)` e o compoñente con `fixture.componentInstance()` e seteamos os inputs con `fixture.componentRef('input name', value)`. Finalmente disparamos a detección de cambios con `fixture.detectChanges()`. Para comprobar que a configuración é correcta, creamols o primeiro test que só espera que a instancia de compoñente sexa truthy.
O fixture contén un debugElement que é unha abstracción de testing sobre o dom que proporciona utilidaddes de navegación na árbore de compoñentes, e directivas, acceder a proiedades de Angular internas, disparar eventos de xeito controlado e acceder ao elemento nativo. Para buscar nun debugElement pódese usar a función `query()` ou `queryAll()` que reciben un predicado formado pola utilidade de predicados **By** (de Angular/platform-browser) que permite buscar por selector de css ou por directiva.
En xeral, os valores de signals, computed, linkedSignals e models testeanse mediante o seu vaor e os outputs con spy en component.output, "emit". Os input, en tanto que son meras asignacións, non hai que testealas, mais sí que hay que validar os seus efectos

### Testing nun compoñente presentacional

Un compoñente presentacional é aquel que únicamente recibe datos e os mostra. Opcionalmente pode rexistrar interaccións co usuario. No cas do exemplo hai que pasarlle na configuración do módulo un providerRouter() porque o compoñente está a usar a directiva `routerLink`. Na maior parte dos casos a estratexia é testear os efectos dos inputs e das interaccións do usuario e non a pila de chamadas.

### Testing nun compoñente intelixente

Testear un compoñente contenedor de alto é máis complexo. Entendemos un compoñente complexo cando accedemos a el mediante a navegación e consume recursos a través da api http. A configuración é semellante ao compoñente presentacional, a diferenza é que importa un servizo que consume HttpClient e, polo tanto, debemos agregar aos nos provider o propio servizo e a instacia stub que simula as chamadas http en lugar de facelas realmente, son `provideHttpClient()` e `provideHttpClientTesting()` e declaramos unha variable mock `httpMock = TestBed.inject(HttpTestingController)` para poder invocar as súas modalidade.

### Tesing nun compoñente complexo

Un compeñente complexo, ademáis de incorporar outros compoñentes, trae datos da ruta, de peticións http e doutros medios. Necesitaremos crear stubs de servizos, mockear datos na configuración dos tests. De entrada, se os datos veñen da ruta, hai que mockear eses datos e testear os seus efectos no DOM. os datos da ruta e o servizo que é a súa principal dependencia debería usar stub ou mocks. Hai que ter en conta que un stub so devolve datos, un mock soporta un retorno (vi.fn()). A idea é simular o comportamento do compoñente, as súas interaccións e os seus efectos no DOM.

## Probando servizos HTTP

Para testear un servizo http precisamos unha instancia do servizo e outra de HttpTestingController, clase de utilidade de testing que permite simular e completar peticións http. Na configuración do módulo de testing en provider vai o servizo e as funcions `provideHttpClient()` e `provideHttpClientTesting()`, a diferenza dun compoñtne, as instancias inicialízanse a través to método `inject()` de TestBed. Ademáis, como se simulan peticións http, hai que comprobar que non se queda ningunha pendente no hook `afterEach()`. A estratexia para testear unha función consiste en comprobar que se fai a chamada correctamente, simlular que se complea se se envía un valor e que ese valor pasa a formar parte do estado da app. Nos servizos baseados en signals as funciósn devolveran promesas polo que hai que telo en conta cando se recuperan os resultados. O endpoint compróbase co método `expectOne()`de HttpTestinController que devolve un obxecto de testing que permite completar a petición no `flush()`. A orde é moi importante:

1. Execútase o método pero non resolve a promesa.
2. Intercepta a petición.
3. Simula a resposta.
4. Garda o resultado e valida.
   Cando unha peticion ten query params, a url de expectOne hai que pasarllo usando una funcion que recupera a url da petición. Os parámetros recupéranse de params (HttpParams) e cada parámetro individual do obxecto params mediante un get().
   Para as peticións con body, accederemos a el medinte req.request.body. Así podemos comprobar o que se envia e mockear o que se recibe para comprobar os efectos no estado.

## Testeando unha pipe

Unha pipe é unha clase que implementa unha funcion. Necesitamos unha instancia da pipe. Unha opción é declarala variable e intanciala un beforeEach() e outra declarala como constante e inicializada ao mesmo tempo. Despois só hai que implementar os tests para os diferentes casos de uso.

## Testeando unha directiva de atributo

O caso presentado é unah directiva que modifica atributos dun elemento nativo. Para poder testealo, na configuración do test precisamos mockear un compoñente host ao que se lle aplicará a directiva en tempo de testing. A fixture apuntará a este compoñente que é quen implementa a directiva. Por tanto, debugElement apunta a este compoñente fake. Adicionalmente crea variables para capturar divs dentro do elemento. A dificultade aquí radica en como testear o comportamento. os eveéntos simúlanse coa función `dispatchEvent(new Event)` do nativeElement.

## Testeando un formulario

Usa un signal form. Ten 3 dependencias: un servizo que vai mockear, un dialogRefMock e un dialogDataMock. No test inicial verifica que se cea o compoñente ecomo é formualrio e só de edición, que se carguen os datos correctamente. Validar os erros nun formulario é doado. Para cada campo pódese setear un valor inválido, marcado como tocado coa función markAsTouched e detectar os cambios. Logo testear os efectos no DOM, como a visualización dos erros. Pódese crear unha funcion auxiliar que recie bomo parámetro obrigatorio `FieldState<T>` que representa o esado dun formulario ou cun campo de formulario.

## Testeando rutas

Para testear as rutas hai que testear a lóxica envolvida que xeralmente corresponde con resolvers e guards.
Un resolver depende dun servizo de api, que se mockea, e un Router. Para fonecer o Router úsase a funcion `provideRouter()` que permite configurar a ruta cun obxecto, o path, component, resolver. Adicionalmente temos a clase RouterTestingHarnes que fornece dun arnés para simluar o funcionamento reduciondo o boilerplate necesario. Tamén é posible crear clases harness a través de estender a clase ComponentHarness. Esta clase trae utilidades de testing. Implementa un hostSelector e permite personalizar unha api pública para craer unha utilidade de testin personalizada.

## Observacións

Vitest permite exectuar os test nun navigador, como karma. Hai que pasarlle a flag `--browsers` ao comando que executa os tests.
No momento de finalicar o curso (26/4/2026) o plugin non executa os test correctamente.
