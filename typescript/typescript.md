# Typescript

## Introdución

Typescript é unha extensión de Javascript que lle engade tipado estático e outras características. O tipado estático permite especificar varlores e operacións ás variables mediante o seu tipo. Úsase en proxectos de tipo NodeJs e se pode instalar como un paquete de Node. Pódese facer localmente para un proxecto en concreto ou globalmente. O recomendado é facelo de maneira separada para cada proxecto co comando estándar:
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

Cando se asigna un valor inicial a unha variable TS infire o tipo da variable, polo que a partir des momento xa non é posbile usar outro tipopara esa variable. Considérase boa práctica usar a inferencia e evitar unha declaración redundante como `const isPossible: boolean = true` quedaría mellor `const isPossible: true`.

### Tipos de datos primitivos

En TypeScript tráballanse con seguintes tipos de datos primitivos:

- **boolean**: tipo de dato que admite dous valores un verdadeiro ou positivo (**true**) e outro falso ou negativo (**false**) `let isGood: boolean`.
- **number**: tipo de dato que admite valores numéricos enteiros e reais (1,2,-3, 2.5) `let age:number = 19, price:number = 13.99` .
- **string**: tipo de dato que admite cadeas de caracteres. Admite comiñas simples ou dobres e template strings. `let name: string = "Alexandre"`.

### Tipos de datos especiais

- **any**: Representa calquera tipo de dato indicándolle ao compilador que suspenda a coerción de tipos. É util para traballar con datos dinámicos pero hai que elimina os beneficios do tipado `let value:any = "Ola"; value=12; value=true`.
- **unknown**: Tipo especial que permite que unha variable poda recibir calquera tipo de dato, pero unha vez que se asigna o valor, ya no se podrá reasignar cun dato de tipo de dato diferente `let value:unknown = 3`.
- **null**: Representa un valor nulo ou ausente `let user:null = null`.
- **undefined**: Representa un valor non inicializado `let user:undefined`.
- **void**: representa un tipo de retorno _null_ ou _undefined_:
  ```typescript
  function logMessage(message: string): void {
    console.log(message);
  }
  ```

### Tipos de datos compostos

Os tipos de datos compostos son aqueles tipos que se xeneran a partir de outros:

- **union**: Para o escenario onde una variable pode almacenar valores de dous ou máis tipos temos un tipo especial que consiste na unión que concatena dous ou máis tipos usando o operador pipe "|", como por exemplo `cont courseId: number | string`. Especifica que unha variable pode ser de varios tipos diferentes:

```typescript
let identifier: string | number;
identifier = "ABC123"; // válido
identifier = 456; // tamén é válido
```

- **intersection**: Combina varios tipo nun único. O valor debe satifacer todos os tipos simultáneamente.

```typescript
type Address = { street: string; city: string };
type Contact = { email: string; phone: string };

type UserInfo = Address & Contact;

let userInfo: UserInfo = {
  street: "Main Street",
  city: "New York",
  email: "example@example.com",
  phone: "123-456-7890",
};
```

### Tipos de datos agrupados

Os tipos de datos agrupados representan coleccións de datos individuais.

- **array**: Representa unha colección aberta de elementos dun tipo específico. Admite dúas sintaxes `type[]` ou `Array<type>`:

```typescript
const evenNumbers: number[] = [2, 4, 6];
const oddNumbers: Array<number> = [1, 3, 5];
```

- **tuple**: Representa unha coleción pechada de elementos con cadanseu tipo: `let tuple: [string, number] = ["Alexandre", 42]`;

### Tipos de datos personalizado

- **object**: Representa un tipo de datos estructurado en forma de pares de clave valor: `let person: {name: string; dob: number} = {name: "Alexandre; dob:34};`
- **type alias**: Permiete definir un tipo personalizado para obxectos ou combinacions de tipos:

```typescript
type User = {
  name: string;
  age: number;
  isActive: boolean;
};
```

- **interface**: Define un contrato que un obxecto debe cumprir. A diferenza do typo alias, poden entrar a formar parte dunha xerarquía, ser implementado por unha clase de JS, ou estendido por outra clase.

```typescript
interface Vehicle {
  brand: string;
  model: string;
  start(): void;
}
```

- **enum**: Define un conxunto de constantes:

```typescript
enum Direction {
  North,
  East,
  South,
  West,
}
```

### Tipos de datos avanzados

- **never**: representa función ou bloques de código que nunca rematan correctamente porque lanzan error ou son bubles infinitos:

```typescript
function launchError(message: string) {
  throw new Error(message);
}
```

- **readonly**: Asegura que unha propiedade é inmutable.

```typescript
type Point = {
  readonly x: number;
  readonly y: number;
};

let point: Point = { x: 10, y: 20 };
// point.x = 15; // Error: Cannot assign to 'x' because it is a read-only property.
```

Pódese definir un alias para un tipo construído nunha asignación mediante o operator **_type_**: `type Person = {name: string; dob: number};`.

### Tipos e funcións

Nas funcións pódese asignar tipos aos parámetros e valores de retorno. Para os valores de retorno tamén funciona a inferencia de tipos. O tipo de valor de retorno **_void_** significa que unha función nun ten un valor de retorno.

### Tipos de función personalizados

TypeScript permite crear tipos personalizados para funcións usando a palabra reervada type:

```ts
type customTypedFunction = (param: type) => returnType | void;
```

O caso de uso son contextos onde se recibe unha función de callback que debe ser tipada.

```ts
type OnCourseCreated = (course: Course) => void;

const createCourse = (
  title: string,
  subtitle: string,
  lessonCount: nubmer,
  callback: OnCourseCreate
) => {
  const course = { title, subtitle, lessoncont };
  callback(course);
  return course;
};
```

## Xenéricos

O xenérico xorde como una necesidade de abstracción. Cando se programa unha funcionalidade abstracta que pode recibir diferentes tipso de valores, en lugar de usar un arry ou unknown, márcase como xenérico e cando se usa establécese o valor concreto do tipo.

Por exemplo, esta función recibe un array cuxo tipo de datos se debe especificar cando se invoca:

```typescript
function inserAtBegining<T>(array: T[], value: T): T[]{
    return [value, ....array];
}

const newArray = insertAtBegining([1,2,3], 0);
```

## POO en Typescript: Clases e interfaces

A declaración de clases realízase coa palabra reservada **_class_**. Úsase para obxectos que se prevén que se podan instanciar. Pódese controlar o acceso aos campos de clase mediante a palabran reservada **_private_**. Typescript adminte unha notación alternativa mediante a que se poden declarar no construtor os campos de clase sen necesidade de o facer con antelación.

#### Clase Student (versión tradicional)

```typescript
class Student {
  private _firstName: string;
  private _lastName: string;
  private _age: number;
  private _courses: string[];

  contructor(name: string, surname: string, age: number) {
    this._firstName = name;
    this._lastName = surname;
    this._age = age;
    this._courses = [];
  }

  get name() {
    return this._firstName;
  }

  enroll(courseName: string) {
    this._courses.push(courseName);
  }
}
```

#### Clase Student (versión alternativa)

```typescript
class Student {
  contructor(
    name: string,
    surname: string,
    age: number,
    courses: string[] = []
  ) {}

  get name(): string {
    return this.name;
  }

  get courses(): string[] {
    return this.courses;
  }

  enroll(courseName: string): void {
    this.courses.push(courseName);
  }
}
```

### Interfaces

Unha interface é unha definición de tipos propia de TypeScript que cando se compila non ten rastro en JavaScript. Unha interface está pensada para ser implementada por clases para habilitar un aquel de herdanza múltiple.
Ao igual que unha clase define propiedades e métodos, pero os métodos non teñen corpo, senón que se teñen que definir cando unha clase a implementa. Ao final é un conxunto de requisitos que unha clase debe satisfacer.

```typescript
interface Drawable {
  isDrawable: boolean;

  draw(): void;
}
```

## xenericos

```Typescript
function compare<T>(arg1, arg2: T): T{
    return arg1 > arg2 ? arg1 : arg2;
}
```

## Decoradores ou anotacións.

## Modulos e namespace

importa con import
exporta con export

Un namespace exporta un conto de elementos exportados. Axuda a organizar paquetes.

```Typescript
namespace name{
    export ...
}
```
