# NOTAS TYPESCRIPT 

## Tipos
Boolean
String
Number
Array
Tupla
Enum

```Typescript
let enum PetEnum {
    DOG = 'Can';
    CAT = 'Gato';
}
```
Any
Unknown
Void: tipo valeiro que agrupa undefined e null.

## Definición de variables e constantes
var global
let local
const constante

Declaración de variable sen inicializar
let myVariable: boolean;
myVariable = true;

Declaración de variable inicializada.
let myVariable = true;

let list: number = [1,2,3]
let list2: Array<number> = [1,2,3]
let tupla: [string, number]
tupla = ["string", 0]

## Definición de clase

TS sé admite un único construtor:

```Typescript
class MyClass{
    private _id: string;

    constructor(id){
        this._id = id;
    }

    get id{
        return this._id
    }

    greet(name): string{
        return `Hi, ${name}!`;
    }
}

```

##  Defición de interface

```Typescript
class MyClass{
    private _id: string;
    private optative?: string;

    greet(name);
}
```

## Modulos e namespace

importa con import
exporta con export

Un namespace exporta un conto de elementos exportados. Axuda a organizar paquetes.

```Typescript
namespace name{
    export ...
}
```

## xenericos

```Typescript
function compare<T>(arg1, arg2: T): T{
    return arg1 > arg2 ? arg1 : arg2;
}
```

## Decoradores ou anotacións.