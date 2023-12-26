# Aplicacions Angular con Redux + Inmutable.js (arquitectura flux)

Un dos problemas problemas das aplicacións SPA é que o estado se controla do lado do cliente. O acceso ao estado pode ser un problema a medida que escala o proxecto. Acumúlanse os buas e as condicións de carreira (_race conditions_) que se arrastran, polo que permitir o acceso sen restricións pódese ir das mans e volver a aplicación inmatenible.

Unha alternativa é manter un estado inmutable e un mecanismo controlado para obtelo modificalo e subtituilo. Isto aumenta a performance en relación coa detección de cambios.

## Tipos de estado

Hai tres tipos de estado:

- Estado interno de compoñente. Canda compoñente ten o seu propio estado.
- Estado global de ui. Define a configración de ui que ten o usuario (p. ex. o idioma).
- Estado de datos da aplicación, que define o estado da apliación (p. ex. unha lista de itens nunha tenda en liña).

## A arquitectura Flux

A arquitectura Flux provén inicialmetne da comunidade React e manexa catro conceptos: Actions, Dispatchers, Store e View.

### A vista (View)

A vista é a árbore de compoñentes de Angular. En Flux cada un deles funciona como unha función pura. Recibe datos e os renderiza per non se modifican directamente na lista.

### O almacén (Store)

O almacén é a noción fundamentas de Flux. É un conteedor para o estado da aplicación. O estado existe dentro do almacén e non pode ser modificado directamente pola vista. Unha aplicación pode ter varios almacéns. Resulta esencial que os datos do almacén sexan inmutables.

### As accións (Actions)

Como os datos do almacén son inmutables, a única forma de modificalos é enviar unha acción que dispara a creación dun novo estado. Por tanto, non se modifica o estado senón que se crea unha nova versión do estado modificada. Unha acción é un obxecto de mensaxe que informa dun evento e contán toda a información para crear un novo estado.

### O despachador (Dispatcher)

O despachador infórmalle a todos os almacén interesadas das accións en recibilos. Por tanto, unha acción pode ter efecto en varios puntos da aplicación.

## O contender de estado Redux

Redux é un contenedor de estado para crear apps de tipo Flux. Segue unha interpretación particular que implementa un único store. As accións poden ser rodeadas por un wrapper que as loguea.

## Deseñando o estado da app

Cando se deseña una aplición Flux hai que definier os contidos do estado. Tipicamente terá forma de json.

### Creando unha acción Redux

As accións defínense como funcións que deovlen un obxecto de tipo Action:

```TypeScript
function addTodo(newTodo: Todo): Action {
    return {
        type: ADD_TODO,
        newTodo
    }
}

function toggleTodo(todo: Todo): Action {
    return {
        type: TOGGLE_TODO,
        todo
    }
}
```

Estas función crean as actions, pero non as despachan.

### Manexando actions

Para definir como o estado cambia segundo a acción, escribimos una función reductora que ten una signatura semellande á do operador funcional reduce:

```TypeScript
(state, action) => state
```

Dado un estado inicial e unha acción, a función reductora devolver un novo estado.

### Creando un redutor Redux

Seguindo o fragmento anterior, ste sería o redutor, para o estado dos datos da aplicación:

```TypeScript
function todos(state: List, action) {
    switch (action.type) {
        case ADD_TODO:
            return state.push(action);
        case TOGGLE_TODO:
            return state.push(action);
        default:
            return state;
    }
}
```

O redutor unicamente bifurca o cálculo do novo estado e delégado noutras funcións ou calcúlao directamente. Tamén se necesina un redutor para o estado global da UI:

```TypeScript
function uiState(state: LIst, action) {
    switch (action.type) {
        case BACKEND_ACTION_STARTED:
            return {
                actionOngoing: true,
                message: action.message
            };
        case BACKEND_ACTION_FINISHED:
            //...
    }
}
```

Podemos combinar redutores que actúan en diferentes partes do estado usando a API Redux `combineReducers`:

```TypeScript
const todoApp = combineReducers({ uiState, todos});
```

Isto crea un único redutor que delega o procesado dunha parte do estado a redutores máis pequenos.

### Crear un stores Redux

Neste caso engadiresmos un middlewarea para loguear a actividade:

```TypeScript
import { createStore, applyMiddleware } from 'redux';

const createStoreWithMiddleware = applyMiddleware(createLogger()) {
    createStore
}

const store = createStoreWithMiddleware(
    todoApp,
    {
        todos: List([]),
        uiState:initialState
    });
```

Aquí pasámoslle o redutor combinado e o estado inicial. Agora está listo.

## Integrando Redux con Angular

Como se vai necesitar en varios puntos da aplicación, cada compoñente que necesite unha acción, necesitará acceder ao store. Para iso disponibilizarase mediante a inxeción de dependcias. Crearemos unha clase Redux:

```TypeScript
import { ReduxStore } from 'angular2-redux-store';

@Injectable()
class TodoStore extends ReduxStore {
    constructor () {
        super(store);
    }
}
```

Agora xa se pode usar en calquera compoñente e despachar accións

```TypeScript
class TodoListComponent {
    constructor( private store: TodoStore) {
        toggleTodo(todo) {
            this.store.dispatach(toggleTodo(todo));
        }
    }
}
```

A arquitectura iria dentro dunha carpeta store

```
/store
    ├── todoStore.ts
    ├── todoActions.ts
    ├── todoReducers.ts
```

## Construíndo datos inmutables

Non hai ningún beneficio en usar Redux se os datos seguen sendo mútables. Para poder converer una collección en inmutable usaremos a libraría Inmutable.js.

```TypeScript
let todo1 = { id: 1, description: "Todo 1", completed: false};
let list = Inmutable.list([todo1]);
```

A lista implementa toda a API das array, pero de tal xeito que son métodos inmutables, polo que non modifican a lista preexistente, senón que devolve un obxecto con outra referencia de memoria.
