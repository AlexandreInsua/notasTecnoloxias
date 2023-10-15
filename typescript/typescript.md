# Typescript

## Introdución
Typescript é unha extensión de Javascript que lle engade tipado estático e outras características. O tipado estático permite especificar varlores e operacións ás variables mediante  o seu tipo. Úsase en  proxectos de tipo NodeJs e se pode instalar como un paquete de Node. Pódese facer localmente para un proxecto en concreto ou globalmente. O recomendado é facelo de maneira separada para cada proxecto co comando estándar:
`$ npm i typescript@version` 
Unha vez instalado é unha boa práctica configuralo.

## Configuración
A configuración de Typescript realízase a través dun ficheiro de configuración denominado `tsconfig.json`. Para crear o ficheiro úsase o comando
`$ npx tsc -init`

## Transpilación
Unha ven instalado e creado un ficheiro de typescript, hai compilalo a javascript nativo. Para isto exécutase o comando
`$ npm tsc`

## Tipos de datos
Os tipos de datos son conxuntos de datos que unha variable pode recibir e as operacións que lle están asociadas. Para definir o tipo de dato dunha variable úsase o operador de tipado ":" á dereita da variable e o tipo. 
Os tipos de datos primitivos son:
    - Booleano: que poder ser verdadeiro ou falso: `let isGood: boolean` 
    - Number: datos de tipo numérico, que adminte a notación decimal con punto: `let pi: number`
    - String: cadea de caracteres: `let name: string`
    - Null: `let nothing: null`
    - Undefined: `let something: undefined`
    - Symbol:

Os tipo de datos complexos son
    - Array. Un array é un conxunto de valores do mesmo tipo `let array: boolean[]`
    - Object. Un objes é unha estrutura de datos que se define por un conxunto de pares chave-valor: `let person: {name: string; dob: number}`

Cando se asigna un valor inicial a unha variable TS infire o tipo da variable, polo que a partir des momento xa non é posbile usar outro tipopara esa variable. Considérase boa práctica usar a inferencia e evitar unha declaración redundante como `const isPossible: boolean = true`.

## Tipo unión

Para o escenario onde una variable pode almacenar valores de dous ou máis tipos temos un tipo especial que consiste na unión que concatena dous ou máis tipos usando o operador pipe "|", como por exemplo `cont courseId: number | string`.

## Tipo alias

Pódese definir un alias para un tipo construído nunha asignación mediante o operator **_type_**: `type Person = {name: string; dob: number};`.

## Tipos e funcións

Nas funcións pódese asignar tipos aos parámetros e valores de retorno. Para os valores de retorno tamén funciona a inferencia de tipos. O tipo de valor de retorno **_void_** significa que unha función nun ten un valor de retorno.

## Xenéricos

O xenérico xorde como una necesidade de abstracción. Cando se programa unha funcionalidade abstracta que pode recibir diferentes tipso de valores, en lugar de usar un arry ou unknown, márcase como xenérico e cando se usa establécese o valor concreto do tipo.

Por exemplo, esta función recibe un array cuxo tipo de datos se debe especificar cando se invoca:

```typescript
function inserAtBegining<T>(array: T[], value: T): T[]{
    return [value, ....array];
}

const newArray = insertAtBegining([1,2,3], 0); 
```

## Clases

A declaración de clases realízase coa palabra reservada **_class_**. Úsase para obxectos que se prevén que se podan instanciar. Pódese controlar o acceso aos campos de clase mediante a palabran reservada **_private_**. Typescript adminte unha notación alternativa mediante a que se poden declarar no construtor os campos de clase sen necesidade de o facer con antelación.

#### Clase Student (versión tradicional)
```typescript
class Student {
    private _firstName: string;
    private _lastName: string;
    private _age: number;
    private _courses: string[];

    contructor (name: string, surname: string, age: number){
        this._firstName = name;
        this._lastName = surname;
        this._age = age;
        this._courses = [];
    }

    get name() {
        return this._firstName;
    }

    enroll(courseName: string){
        this._courses.push(courseName);
    }
}
```

#### Clase Student (versión alternativa)
```typescript
class Student {
    
    contructor (name: string, surname: string, age: number, courses: string[] = []){
    }

    get name(): string {
        return this.name;
    }

    get courses(): string[]{
        return this.courses;
    }

    enroll(courseName: string): void{
        this.courses.push(courseName);
    }
}
```

## Interfaces

Unha interface é unha definición de tipos propia de TypeScript que cando se compila non ten rastro en JavaScript. Unha interface está pensada para ser implementada por clases para habilitar un aquel de herdanza múltiple. 
Ao igual que unha clase define propiedades e métodos, pero os métodos non teñen corpo, senón que se teñen que definir cando unha clase a implementa. Ao final é un conxunto de requisitos que unha clase debe satisfacer.

```typescript
interface Drawable {
    isDrawable: boolean;

    draw(): void;
}
```