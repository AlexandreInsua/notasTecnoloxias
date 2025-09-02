# DETECCION DE CAMBIOS EN ANGULAR

## Definición

O mecanismo de deteción de cambios de Angular é un mecanismo que utiliza para saber cando se debe actualiar toda ou parte da vista dun cmpoñente en cas de que os datos cambiaran.
Na definición por defecto dispárase na raíz da aplicación e vaise transmitindo en dirección descendente a través dos compoñentes fillos. Cando a app é moi grande todos estes cambios afectan á performance. Os inputs e outputs compáranse por referencia.
Pódese exluír da detección de cambios invocando unha instancia de zona ngZon e executando o código fóra de Anguar coa `ngzone.runOutsideAngular()`

## Como esta implementada a detección de cambios en angular

Angular pode detecar cando os datos do compoñente cambian e pode renderizar estos cambios automaticamente na vista, pero isto consume recursos. Isto débese a quen podemos anular o tempo de execución por defecto.

## Sobreescribindo os mecanismos por defecto do navegador

No momento de arranque, Angular sobrescribe varia API de baixo nivel como o AddEventListener coa sua propia versión

```javascript
// nova versión do AddEventListener
function addEventListener(eventName, callback) {
  callRedAddEventListener(evennName, function () {
    // first call the original callback
    calback(/*...*/);
    // and then run Angular-specific funtionality
    var changed = angular.runChangedDetection();
    if (changed) {
      angular.renderUIPart();
    }
  });
}
```

Esta nova implemenación, ademais de chama o callback rexistrado, dálle a Angular a posibilidade de executar un cambio.

## Como traballa este parcheo de baixo nivel

Este parcheo dos API de baixo nivel dos navegados faise usando a travé da librería zone.js. Unha _zona_ é un contexto de execuión que sobrevive a múltiples turnos de execuión da máquina virtual de JavaScript. É un mecanismo xenérico que podeos usar para engadir a funcionalidade extra ao navegador. Angular, internamente, usa zonas para activar a detección de cambios, pero admite outros usos.

## APIs asíncronas soportadas

Os mecanimos do navegador parcheados son:

- Os eventos do navegador (click, mouse over, key up, etc...).
- As funcións setTimeout() e setInterval()
- As peticións http.

Existen outras AP parcheadas polo navegador, para activar de xeito transparente a detección de cambios de Angular, como os webSockets. Se unha API asíncrona do navegador non está soportada pola zone.js, a detección de cambios non funcionará. Unha vez activadas a detección de cambios, como funciona?

## A árbore de detección de cambios

Cada compoñente de Angular ten un detector de cambios asociado, que se crea no inicio da aplicación. Por exemplo, tomaremos un compoñente:

```typescript
@Component({
  selector: "todo-item",
  template: ` <span class="todo noselect" (click)="onToggle()"
    >{{ todo.owner.firstName }} - {{ todo.description }} - Completed:
    {{ todo.completed }}</span
  >`,
})
export class todoItem {
  @Input() todo: Todo;
  @Output() toggle = new EventEmitter<Todo>();

  onToggle(): void {
    this.toggle.emit(this.todo);
  }
}
```

Pódese ver en tempo de execución como é o detector de cambios, pero é unha peza de JS construído no inicio de apliacions.

Para cada expresion usada na templeta, comopara o valor actual o valor anterior desa propiedade. Se son diferentes establce a flag `isChanged` a `true.`.

O detector de cambios tamén verifica o obxecto anidadao pero só para as propiedades que se usan na templae. Isto é así para todos compoñentes. Tampouco se realiza a comprobación da id do Todo porque non se usa na template.

Isto é así porque un dos obxectivos é ser transparetne e fácil de usar para qu eos usuarios non teñan que facer grandes esforzos para debuguear o framework e coñecer os mecanismos internos.

## Comparacións por referencia

Angular debe dar soporte ao feito de que Javascript os obextos son inmutables. Por iso a detecciónde cambios non funcion seguindo a comparación por referencia, senón polas propiedades usadas na template.

O detector de cambios fai referencia á propiade `todos` do compoñente da lista. Que pasa aquí.

## Unha ollada á JavaScript Virtual Machine

Todo isto ten que ver con como trabala a JS VM. O código para comparar propiedades on pode ser optimizado doadamente a código nativo, no compilador JIT na JSVM. En xeral, a detección de cambios é rápida, predecible e simple de razonar.

## O modo de detección de cambios onPush

Se o compoñente faise reamente grande, podemos configurar o compoñente `TodoList` para que se actualice unicamente cando a lista de Todos cambia. Para isto configúrase o compoñente no decorador:

```typescript
changeDetection: ChangeDetectionStrategy.OnPush;
```

Ocorre

- cando cambia un parámetro de entrada/output
- eventos do DOM, network, observables

Agregamos dos botóns. un mara que modfiue o primeiro elemetno e outro para agrear un Todo á lista. O código queda así:

```typescript
@Component({
  selector: 'app',
  template: `<div><todo-list [todos]="todos"></todo-list></div>
<button (click)="toggleFirst()">Toggle first</button>
<button (click)="addTodo()">Add todo</button>`
})
export class App {
    todos:Array<Todo>: initialData;

    toggleFirst(){
        this.todos[0].completed = !this.todos[0].completed;
    }

    addTodo(){
        let newTodos = this.todos.slice(0);
    }
}
```

O primeiro botón non funciona porque o métoo muta un elemento da lista e o compoñnte non pode detectqar isto porque a referencia do input non muta.
O segundo botón funciona porque crea una lista de todos e reempreza a variable co lista compiada, poque se detecta o cambio de referencia. Pero se mutamos a lista non funciona, necesitamos unha lista nova.

## OsPush compara os inputs por referencia?

Se cambiamos no TodoItem a onPush e facemos click sobre el seguirá funciónando porque está estratexia non só comproba os inputs, senón que tamén comproba os eventos e tamén cando un observable dispara un evento. Aínda que mellora o rendemento o seu uso aumenta a complexidade. Un xeito de evitar istó é uar obxectos inmutables de xeito que é seguro usar onPush. Como sempre se crean novo s elementos, sempre son detectados. Unha técnica é usar Inmutables.js.

A detección de cambios é unidireccional. Cando os datos dun controlador se actualiza, execútase a detección de cambios e se actualiza a vista. Pero a actualización da vista non dispara por si mesma máis cambios.

## Como disparar a detección de cambios?

Unha maneira é usar callbacks de lifecycle. Por exemplo, en TodoList component disparamos un callback a outro compoñente que cambia o bindings

```typescript
ngAfterViewChecked(){
  if(this.callback && this.clicket){
    conosle.log("changing status...");
    this.callback(Math.ramdom());
  }
}
```

Mostrará un erro "Expression has changed after it wasa checked". Esta mensaxe só se mostrará en modo de desenvolvemento. En modo producción non se porque no primeiro modo a detección de cambios execútase dúas veces.

## Xestionar a detección de cambios

Podemos desactivar a detección de cambios e activala onde querems usando unha instancia do detector de cambito e a executamos manualmente invocando o método `detectChanges()`.

## Trampas de OnPush

O punto de partida é un compoñente Home que ten como fillo un compoñente Newsletter. Ten esta template:
`<newletter [user]="user" (subscribe)="subscribe($event)"/>
<button (click)="changeUserName()">Change user name</button>`

e o compoñente:

```typescript
export class HomeComponente {
  user: User = { firstName: "Alexandre", lastName: "Insua" };

  cosntructor(service: NewsletterService) {}
  subscribe(email: string): void {
    this.service.subscribe(email);
  }
  changeUserName() {
    this.user.firsName = "Bob";
  }
}
```

O compoñente newsletter ten un formulario e o compoñente recibe input o usuario e emite un evento personalizado cando se subscribe.

## Detección de cambio por defecto e mutabilidade

Cando probamos este exemplo clicando no botón changeName funcionará como se espera o que significa que:

1. Inicialmente móstrase "Ola Alexandre" que é o valor incial definindo no compoñente Home.
2. Cando se faga click non botón do compoñente, cambiará a dicir "Ola Bob" establecido no método. Esta implementación con mutabilidade directa funciona porque a detección de cambios por defecto é compatible cando hai expresión no template que se deben comprobar, neste caso {{user?.firstName}}

## OnPush e mutabilidade directa

Se cambias a estratexia a onPush, deixa de funcionar. A vista xa non reflicte os cambios no modelo. Isto ocorre porque mutamos un obxecto directamente. como OnPush compara referencias e estas non cambias, o detector de cambios non se dispara.

## Evitar mutación directa con OnPush

Se cambiamos a implementación do método para crear un obxecto en vez de modifical, resolvemos isto

## OnPush e event handlers

Hai outras sistuación onde pode haber problemas. Os eventos do DOM tamén dispara a detección de cambios OnPush.

## On Push e observables

Para facer un escenario realista, creamos un servizo que devolve os datos do ususario. consumimos o observale na template cun pipe async. Isto seguirá funcionando porque desde o punto de viscta do compoñnte newsletter recíbese unahh nova instancia.

## Pasando un observable como @Input a OnPush

En lugar de subscribirmos na tamplate, pasámoslle o observable ao compoñente fillo. A template do fillo é tal que :
`{{(user$ | async).firstName }}`
Aínda que o obxecto non cambia, a pipe async fai que Angular saiba que a emision de valores vai ter impacto na template, polo que dispara a deteción de cambios.

## Compoñentes anidados
