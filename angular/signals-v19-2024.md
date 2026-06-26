# MODERN ANGULAR WITH ANGULAR

## Introdución

### Zone.jx

Introducíronse na v16 (2023) como _developer preview_ e son estables desde a v19 (2024). Trátase dun novo enfoque de manexar a reactividade. É unha nova forma de manexar os cambios. A detección de cambios clásica baseáse na libraría _Zone.js_
Cando se produce un evento do DOM, Web API ou timer, Zone.js detéctaos e verifica todas as variables usadas no DOM para actualizadas ou non. Este é o comportamento de detección de cambios por defecto. Executa a deteccion de cambios en toda a árbore de compoñentes cando se produce calquera evento asíncrono:

- Eventos do DOM
- Timers
- Promesas
- Observables
- Chamadas http

A presenza destes eventos sobrecarga a performance da aplicación porque comproba todos os posibles cambios e aumenta a bundle porque incorpora unha libraría de terceiros.

Porén OnPush dispárase cando

- Cambia a referencia dun input
- Eventos personalizdos
- Pipe async
- Disparos manualmente

### Signals

O sistema de signals é diferente poque prescinde do anterior. Unha sígnal é un contenedor de valores que permite controlar o seu estado e os seus dependentes de tal xeito que cando muda o seu estado dispárase a deteción de cambios nestes (os dependentes) e, no final, mostralos na template se é o caso. Para cada signal, Angular constrúe un grafo dirixido que reflicte estas dependencias. **O obxectivo final é desfacerse de Zone.js**.
A migración pode facerse propiedade a propiedade con pasos mínimos, ou comezando de cero con signals.

## Obxectos, arrays e inmutabilidade

## API das signals

### Signals

A API das signals está inclúida no paquete principal de Angular:

```typescript
import { Component, signal } from "@angular/core";
```

A continuación sobre calquera outra propiedade aplíacase a función `signal<T>(initialValue)` que crea un obxecto que encapsula o valor do dato e garda os seus dependentes para poder reaccionar aos cambios de xeito granular. Un signal declárase de xeito propotípico:

```ts
const myVar = signal<T>(defaultValue);
```

Neste momento o valor xa non é accesible ou modificable directameente, senón que hai que recorrer aos métodos da API
E ten os seguintes métodos

```ts
const myVar2 = myVar(); // get
myVar.set(newValue); // set
myVar.update((oldValue) => newValue); // update
```

Para poder ober o valor dunha signal no template,hai que executar o seu getter. Cando o valor da signal cambie, Angular detéctao e envia o novo valor aos seus consumidores.

### Computed

As signals computadas son signals de só lectura cuxo valor calcúlase e a partir doutras signals e actualízase cando se actualizan estas. Reciba unha función de callback que devolve un valor baseado a partir daquelas.

```ts
const mycomputed = computed(() => this.myVar() + this.myVar2()); // cada vez que mude unha ou outra, actualizase o valor computado
```

### Effect

Un efecto colateral é unha resposta a calquera cambio na cadea reactiva de sinais. Esta pensado para repercutir un cambio fóra do contexto reactivo dos sinais en resposta a un cambio de valor dun sinal. Debería ter un uso limitado. Necesita ser usado nun contexto de inxección de dependencias.

### Computed signals

Signal de só lectura que se calcula a partir doutra signal e reecciona aos cambios

```ts
const mycomputed = computed(() => this.myVar());
```

Cálcúlase cando menos unha vez. Cando se invoca unha signal dentro da función xa se establce a dependencia automaticamente.

### Signal effect

Un efecto colaeral é unha funcio que se dispara cando se detecta un cambio nalgunha signal declarara no seu interior:

```ts
effect(() => fn);
```

Execútase cando menos unha vez e sempre que unha signal invocada mude o se valor. Hai que usalo con moderación poara aqueles casos de usus que están fóra do contexto de reactividade de sinais de Angular. Por exemplo, o estado dun formulario no localStorage.
O uso de effect pode implicar memory leaks na destrucción dun compoñente se non se limpan conrrectamente as referencia ás variables. Angular fará a limpeza só se coñece o contexto de inxección de dependencias, por iso hay que definilo no constructor, para ter a certeza de que funcióna esa limpeza. Cando non se fai así, pode ocorrer un erro en consola polo que se fai necesario facer esa limpeza manualmente. Para isto hai que pasarlle o inxector de depencias:

```ts
private readonly injector = inject(Injector);
private readonly loggerService = inject(LoggerService);

constructor () {
    afterNextRender (()=>{
        effect(()=>{
            this.loggerService(this.mySignal())
        },
        {injector: this.injector}
        )
    })
}
```

A función effect devolve unha referencia do tipo EffectRef que se pode usar para facera limpeza da referencia en non se quere delegar no mecanismo automático do colector de lixo mediente o método `effectRef.destroy()`:

```html
<button type="button" (click)="manualCleanUp()"></button>
```

```ts
manualCleanUp(): void{ this.effectRef.destroy(); } `
```

Outro caso de uso é o callback de limpeza, que executa un callback para limpar referencias e execútase cando un effect é destruído:

```ts
constructor(){
    this.effectRef = effect((cbCleanUp)=>{
        const counter = this.counter() // signal

        // non funciona dentro de closures
        cosnt timemout = window.setTimeout(()=>{
            console..log({`value: ${counter}`});
        }, 1000);

        cbCleanUp(()=>{
            window.clearTimeout(timeout)
        })
    })
}
```

## CRUD con signals

RSJS pasa a ser opcional (en teoría, en realizadade pasa a usarse para fluxos complexos). Cambia o modelos de reactividade en Angular. Esta recollido na discusién téncia sub _RFC-31 Signal for Angular reactivity_. A idea é implementar un sistema de reactidade síncrono e acoutar os casos de uso de RXJS, concretamente para os escenarios de orquetración de operacións asíncronas complexas, por iso manteñen o módulo de interoperabilidade. E unha aproximación de RXJS mínimo. A primeira opción é usar _fetch_ nativo:

```typescript
async getAllCourses(): Promise<Course[]> {
    const response = await fetch(`${this.env.apiroot}/courses`);
    const payload = await response.json();
    return payload.courses;
}
```

A forma de usalo nun compoñente é encapsulalo dentro dunha función coa sintaxe estándar de ES:

```typescript
async loadAllCourses() {
    try {
        const courses = await this.service.getAllCourses;
        this.courses.set(courses);
    } catch (error){
        this.loggerService.log('error', error);
    }
}
```

e recomenda usar esta función no constructor (non en OnInit)

```typescript
constructor() {
    this.loadAllCourses();
}
```

Alternativamente, pódese facer no OnInit ou usando o "novo" método _afterNextRender_.

**Input signals**

```typescript
input<T>(defaultValue, options);
```

ou

```typescript
input.required<T>(defaultValue, options);
```

Admite un paráametro de configuración que permite personalizdo

```typescript
{alias:string, transform:cbFn}
```

### HttpClient con async/await

A filosofía cosniste en transformar os observables en promesas cantos antes. O caso de uso principal é a necesidade de integrar servizos con interceptores. rxjs fornece da función _firstValueFrom()_ que reaaliza a transformación dun observable en tanto que valor devolto por un HttpClient nunha promesa. Retorma a promesa logo de o Observable emitir o primeiro valor e cancela a susbcrición. Se o observable emite un erro a promesa rexéitase con erro. Se o observable completouse antes de emitir un valor, a promesa rexéitase cun erro valeiro.

### Loader indicator

Server de demo para partillar un estado entre compoñoentes vía un servizo que implementa un signal. A idea é que o servizo garda o estado nunha signal privada que se exporta noutra pública como só lectura mediante o método _asReadOnly()_. O estado manipúlase con métodos mutadores públicos.
Como este loader está pensado para as chamadas asíncronas uas un interceptor. Para isto créase un interceptor funcional que activa o loader cando lanza unha petción e o desactiva cando optén a resposta do erro.
Adicionalmente, podemos ter o caso de precisar obviar este funcionamento, como ver caso dun gardadao en segundo plano. Para isto úsase o contexto Http Http en HttpContext de Angular. Para iso defínese unha constante HttpContext que se inxecta na peticion e serve de flag para ser consumido no interceptor. Para establecer que unha chamada obvia o indicador de carga faise no servizo mediante o obxecto de configuración, onde recibe unha entrada `context` cunha nova instrución de contexto.

### Notificación de mensaxes

Trátase de implementar unha solución para mostrar mensaxes de erros. Hai navegadores que poden bloquear os popups. A idea é ter un serviza centralizado para manexala.

### Autenticación

Partimos dun servizo que partilla o perfil autenticado tamén basado en signal. O esquema é semellanten ao anterior. Temos unha signal privada que mantén o estado e unha derivada que expón o valor como só lectura, ben signal computada, ben como signal con _asReadOnly()_.
Temos un método de login que realiza a chama ao backend e modifica o estado da signal e cachéaa no navigador. O método de logout borra o estado e limpa a caché. Adicionalment, existe un método para recuperar os datos da caché.

## Model

O model é un primitivo da API de signal que fornece de enlazamento bidireccional. É un valor editable que pertence ao estado do compoñente. Úsase cando o valor é un primitivo, vén dun campo de formulario, non necesita validacións complexas e está vinculado a un compoñente en concreto (estado local). Ideal para buscadores, fillor locais, inputs aillados, controis de UI simples como toggles, checkboxes, radios, selects, preferencias locais.
Se o estado é distribuído ou require validación avanzada debería usarse outra cousa.

## Signal template queries

Podemos facer unha query contra a template mediante a API _viewchild_. Cando se fai contra un elemento do DOM, obténse unha referencia ao elemento que accede ao elemento nativo. Cando se fay a query contra un compoñente accede por defecto ao seu valor pero pódese modificar, mediante un obxecto de configuración.
Tamén é posible facer unha query conra unha directiva, como o tooltip.
A directiva _viewChildren_ é semellante, pero retorna varios elementos polo que a template reference debe ser a mesma para eses elementos. En ambos casos podemos acceder aos valores medinte un effect polo que podemos prescindir de hooks tipo afterViewInit.
_contentChild_ view query está pensada para escenarios de content projection, porque viewChild ou viewChildren non poden acceder ao contido proxectado. Funciona de xeito semellante pero a referencia da template deber ir no contido proxectado, non na directiva ng-content.

## Interoperatividade

### ToObservable

A función _toObservable()_ transforma un signal nun observable. Cando se usa fóra dun contexto de inxección hay que pasarlle o contecto vía un inxector coa seguinte sintaxe:

```typescript
private readonly injector = inject(Injector);
private courses  = signal<Course[]>()

functionExecutedOutOfInjectionContext(){
    const courses$ = toObservable(this.courses, { injector: this.injector});
}
```

_toObservable()_ usa un effect internamente para poder facer un seguemento dos cambios dos valores do signal ao longo do tempo. Cómpre ter en contan que o effect (e o computed só se produce cando o valor da signal está estabilizado no ciclo de detección de cambios correspondentes )

### ToSignal

A función _toSignal()_ que transforma un observable a un signal. Subscrébese a el e a medida que emite valores son reflexados no valor do signal. Recibe como parámetros un observable e un obxecto de configuración que pode recibir o inxector e o valor inicial da signal ou a sincronización forzada co observable para que capture o valor inicial que emite. O inxector debe enviarse canso se executa fóra dun contexto de execución. Para a captura de erros hai dúas técnicas. Se se captura no observable, hai que configurar a signal para que rexeito o erros:

```typescript
const courses$ = this.coursesApi.getAll().pipe(
  catchError((error) => {
    this.logger(ERROR, error);
    throw error;
  }),
);
const couses = toSignal(this.courses$, { rejectErrors: true });
```

A alternativa é envolver a signal nun bloque try-catch para xestionar o erro.

### Linked Signals

Primitivo pensado para os casos onde computed non é de abondo. A función _linkedSignal_ devolver unha signal escribible e recibe como párametro un obxecto de configuración con dúas propiedades. **source**, que recibe unha signal ou un obxecto con varios signal e **computation** que recibe unha función que realiza un cálculo determinado. Esta función dispárase con cada cambio dos signals que se usan para realizar o cálculo. Non entanto, a recomendación é usar computed e reservar esta para escenarios concreto e complexos.

### Resourse API (experimental na v19)

Trátase dun novo primitivo para facer peticións a unha api. Serve para facer peticións get conta un recurso ou backend. Incorpora moitas funcionlidades por defecto. Recibe un obxecto de configuración cos params que se poden ser completados incorporando signals, e un loader que configura a petición.
