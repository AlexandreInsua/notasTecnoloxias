# Typescript

## 1. Introdución

Typescript é unha extensión de Javascript que lle engade tipado estático e outras características. O tipado estático permite especificar valores e operacións ás variables mediante o seu tipo. Úsase en proxectos de tipo NodeJs e se pode instalar como un paquete de Node. Pódese facer localmente para un proxecto en concreto ou globalmente. O recomendado é facelo de maneira separada para cada proxecto co comando estándar:
`$ npm i typescript@version`
Unha vez instalado é unha boa práctica configuralo.

## 2. Configuración

A configuración de Typescript realízase a través dun ficheiro de configuración denominado `tsconfig.json`. Para crear o ficheiro úsase o comando
`$ npx tsc --init` para instalación local.

O ficheiro de configuración ten por defenco moitas opcións, pero admite outras entradas. Podes agregar as seguintes novas chaves:

- exclude: para excluír ficheiros da transpilación. Admite o \* como wildcard. Exclúense _node_modules_ por defecto. Se exlúmios algún ficheiro hai que engadir o node_modules para evitar problemas.
- include, para incluar os ficheiros que se deben compilar especificamente. Por defecto inclúense todos.
- compileOpcions: ten as opcións de compilación. As máis importantes son:
  · target: defina a que versión de JavaScript se transpila
  · module:
  ·lib: define que apis de ECMScript están disponibles
- type checking: é unha sección que conten as configuracións estrictas, que son as recomendables:
  · noUnusedLocal
  · noUnusedParameters
  · noFalltroudCasesSwitch
- SourceMas: matep entre ts e js para debugueo
- rootDir: ruta de ficheiros transpilados
- outDir: ruta de ficheiros transpidlados
- strict compilatiosn: conxunto de opcions que obrida a realizar unha compilación estricta.
  Chect actions: miscelánea de compilaciósn.

## 3. Transpilación

Unha ven instalado e creado un ficheiro de typescript, hai compilalo a javascript nativo. Para isto exécutase o comando
`$ npm tsc`

## 4. Tipos de datos

TypeScript verifica os tipos durante o tempo de compilación, mentres que JavaScript faino en tempo de execución, polo que TypeScript revela erros con anticipación a JavaScript.
Os tipos de datos son conxuntos de datos que unha variable pode recibir e as operacións que lle están asociadas. Cando se intenta asignar a unha variable un valor de tipo diferentes, dára un error de tipo _"Type 'type' is not asignable to type 'type'_ en tempo de transpilación, pero non de execución porque o que se executa é JavaScript. Dado que TypeScript usa un tipado dinámico os error produciranse durante o desenvolvemento e non en tempo de execución.

Para definir o tipo de dato dunha variable úsase o operador de tipado ":" á dereita da variable e o tipo.

Cando se asigna un valor inicial a unha variable TS infire o tipo da variable, polo que a partir des momento xa non é posbile usar outro tipopara esa variable. Considérase boa práctica usar a inferencia e evitar unha declaración redundante como `const isPossible: boolean = true` quedaría mellor `const isPossible = true`.

### 4.1. Tipos de datos primitivos

En TypeScript tráballanse con seguintes tipos de datos primitivos (os mesmos que en JavaScript):

- **boolean**: tipo de dato que admite dous valores un verdadeiro ou positivo (**true**) e outro falso ou negativo (**false**) `let isGood: boolean`.
- **number**: tipo de dato que admite valores numéricos enteiros e reais (1,2,-3, 2.5) `let age:number = 19, price:number = 13.99` .
- **string**: tipo de dato que admite cadeas de caracteres. Admite comiñas simples ou dobres e template strings. `let name: string = "Alexandre"`.
- **literal type**: tipo de dato que representa o valron concreto dunha cadea: `let saludo: 'ola' = 'ola'`;
  Pódese usar un template literal para crear tipos derivados:

`type ReadPermissions = "no-read" | "read";`
`type WritePermissions = "no-write" | "write";`
`type FilePermissions = '${ReadPermissions}-${FilePermissions}'` // produto cartesiano das opcións anteriores

Pódese combinar con outras funcionalidades

```typescript
type DataFile = {
  data: string;
  permissions: FilePermissions;
};

type DataFileEventName = `${keyof DataFile} changed`;

type DataFileEvents = { [key in DataFileEnvetName]: () => void };
```

E definimos un tipo a partir doutro.

O compilador de TypeScript tamén é capas de inferir tipos de datos a partir dun valor explícito. Por iso é boa práctica tipar unha variable que se declara paro que non se inicializa pero non tipala cando si se declara e inicializa:
`const isPossible = true //queda tipada como boolean`.

### 4.2. Tipos de datos especiais

- **any**: Representa calquera tipo de dato indicándolle ao compilador que suspenda a coerción de tipos. É util para traballar con datos dinámicos pero hai que elimina os beneficios do tipado `let value:any = "Ola"; value=12; value=true`.
- **unknown**: Tipo especial que permite que unha variable poda recibir calquera tipo de dato, pero unha vez que se asigna o valor, xa non se podrá reasignar cun dato de tipo de dato diferente `let value:unknown = 3`.
- **null**: Representa un valor nulo ou ausente `let user:null = null`.
- **undefined**: Representa un valor non inicializado `let user:undefined`.
- **void**: representa un tipo de retorno _null_ ou _undefined_:
  ```typescript
  function logMessage(message: string): void {
    console.log(message);
  }
  ```

### 4.3. Tipos de datos compostos

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

### 4.4. Tipos de datos agrupados

Os tipos de datos agrupados representan coleccións de datos individuais.

- **array**: Representa unha colección aberta de elementos dun tipo específico. Admite dúas sintaxes `type[]` ou `Array<type>`:

```typescript
const evenNumbers: number[] = [2, 4, 6];
const oddNumbers: Array<number> = [1, 3, 5];
```

- **tuple**: Representa unha coleción pechada de elementos con cadanseu tipo: `let tuple: [string, number] = ["Alexandre", 42]`;

### 4.5. Tipos de datos personalizados

- **object**: Representa un tipo de datos estructurado en forma de pares de clave valor: `let person: {name: string; dob: number} = {name: "Alexandre; dob:34};`
- **type alias**: Permite definir un tipo personalizado para obxectos ou combinacions de tipos. Tamén se chaman custom types:

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

### 4.6. Tipos de datos avanzados

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

- **Record**: tipo de utilidade que permite definir a estrutura dun obxecto `Record<string, number>`

- **Derivado**: Un tipo derivado creáse a partir da sentenza **typeof**, que en TypeScript permite crear un tipo novo a partir dun xa existente:

```typescript
let obj = {};
type MyObj = typeof obj;
```

**keyof** é unha palabran reservada de TypeScript que permite extraes as keys dun objeco e almacenalas nun tipo derivado, con que podemos ter funcións moi flexibles, por exemplo:

```typescript
// Funnción que obtén a propiedade dun obxecto
function getProperty<T extends Object, K extends keyof T>(obj: T, key: K) {
  const value = obj[key];

  if (value === undefined || value === null) {
    throw new Error("Accessing undefined or null value");
  }

  return value;
  // return !!value ? value : throw new Error("Accessing undefined or null value");
}
```

Deste xeito tempos a inferencia do tipo funcionando de principio afin.
Indexed access types é unha característica que permite extraer parte dun obxecto para crear un novo tipo derivado:

```typescript
type AppUser {
  name: string;
  age: number;
  permissions = {
    id: string;
    title: string;
    description: string;
  }

  type Permisions = AppUser['permissions']
}
```

#### Tipos condicionais.

Podese asintar un tipo dinamicamente

```typescript
type getelementeType<T> = T extends any[] ? T[number] : never,
```

Tamén se pode usar esta sintaxe com tipo de retorno dunha función.

#### Mapped types

Consiste en obter un tipo obxecto derivado doutro obxecto preivo. É unha funcionalidade que está pensada para casso de uso onde haxe obxectos relacionados:

```typescript
type Operations = {
  add: (a: number, b: number) => number;
  subtract: (a: number, b: number) => nubmer;
};

type Results = {
  add: number;
  subtract: number;
};
```

Podemos redefinir o segundo tal que

```typescript
type Results<T> = { [key in keyof T]: number}: // isto percore as claves de T para asinalas como chaves en Results,
```

Póde definir unha propiede como opcional coa interrogacion `[key in keyof T]?: number`
Se no obxecto inicia habia propiedades opicionais con interrogación- eliminarandes esa opcionalidade:
`[key in keyof T]?: number`
readonly
`readonly [key in keyof T]?: number`
`-readonly [key in keyof T]?: number`

#### Interdicion types

Propiedade que permite crear un tipo a partir doutro usando o operador &. Podese usar type alias ou conseguir o mesmo resultado usando interfaces

#### Types guards

Cando un tipo unión de varios obxectos con diferentes propiedades usado nun msmo lugar e necesita ter en conta as propiedaes hai que establecer unha garda do tipo `property in object`

#### Discriminate unions

Outra alternativa é usar a union discrimida usando unha propiedade que indica o tipo de obxecto. Esta técnica indica o tipo de obxecto.
Outra técnica é usar _instanceof_ cando se está a trballaro con clases.
Nos tres casos con un único if é dabondo para distinguir entre obxectos.
Pódese encapsular a comprobación de tipo nunha funion e as versións modernas de ts devolve un perdicado de tipo que achega a info extra.

#### function overloads

É unha funcionalidade de typeScript que permite definir varios tipos de parámetros ou de retor para unha mesma funcion e poder discriminar e traballar mellor cos tipos.

#### Index type feature

Existe unha sintaxe para facer un obxecto flexible chamada index type feature e consise en usar como chave unha dinámica props, que é un placeholder:

```typescript
type Store {
  [props:string]
}

const store = { name: "MyStore", owner: { name: "Alex", }}
```

### 4.7. Tipos e funcións

Nas funcións pódese asignar tipos aos parámetros e valores de retorno. Para os valores de retorno tamén funciona a inferencia de tipos polo que algúns afirman que se pode deixar sen ecplicitar para que actúe a inferencia.. O tipo de valor de retorno **_void_** significa que unha función nun ten un valor de retorno.

```typescript
function add(a:number, b:number){ return a + b } // return nummber

type AddFn = typeof add; // number

type returnValueType<T> = T extends O (..args: any[]) => R ? R :never // return value

type AddFnReturnType = returnValueType<AddFn> // number
```

Hai que ter en conta que TypeScript fornece do tipo **Function** para aqueles casos de uso onde unha variable pode ser tipada como unha función que por súa vez tamén é tipada usando para iso unha función de frecha.

O mesmo aplica ás función de callback. Así podemos controlar a flexibilidade dos callbacks creando tipos personalizados. As funcións de callbck poden devolver algo mesmo cnado na definición se marcou que non devolver nada o son de tipo void. Never é outro tipo de valor de retorno que se utiliza cando a función non devolve nada porque se corta a execución da aplicación. Úsase tipicamente cando se ponde lanzar excepcións.

#### 4.7.1. Tipos de función personalizados

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

### 4.8. Xenéricos

O xenérico xorde como una necesidade de abstracción. Cando se programa unha funcionalidade abstracta que pode recibir diferentes tipso de valores, en lugar de usar un arry ou unknown, márcase como xenérico e cando se usa establécese o valor concreto do tipo.

Por exemplo, esta función recibe un array cuxo tipo de datos se debe especificar cando se invoca:

```typescript
function inserAtBegining<T>(array: T[], value: T): T[]{
    return [value, ....array];
}

const newArray = insertAtBegining([1,2,3], 0);
```

A definición dun xenérico pode agregar unha constraint:

```typescript
function mergeObj<T extends Objects>(a:T, b:T): ojb:T{
    return {...a, ...b};
}

const newArray = insertAtBegining([1,2,3], 0);
```

## 5. POO en Typescript: Clases e interfaces

A declaración de clases realízase coa palabra reservada **_class_**. Úsase para obxectos que se prevén que se podan instanciar. Pódese controlar o acceso aos campos de clase mediante a palabran reservada **_private_**. Typescript adminte unha notación alternativa mediante a que se poden declarar no construtor os campos de clase sen necesidade de o facer con antelación.

### 5.1. Definición de clase

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

### 5.2. Definición de Interfaces

Unha interface é unha definición de tipos propia de TypeScript que cando se compila non ten rastro en JavaScript. Unha interface está pensada para ser implementada por clases para habilitar un aquel de herdanza múltiple.
Ao igual que unha clase define propiedades e métodos, pero os métodos non teñen corpo, senón que se teñen que definir cando unha clase a implementa. Ao final é un conxunto de requisitos que unha clase debe satisfacer.

```typescript
interface Drawable {
  isDrawable: boolean;
  isPrintable?: bolean; // propiedade opcional

  draw(): void;
}
```

## 6. Decoradores ou anotacións

Un decorador é unha feature de metaprogramación, código que interactúa con outro código. A idea que que un decorador cambia o elemento que eta relacionado. TypeScript soporta os decoradores de ECMAScript. Os decoradores están orientados á POO polo que se relacionan con clases, campos, setters, getters e métodos de clase.

### 6.1. Decoradores de ECMAScript

Un decorador é unha función cunha sintaxe específica. Recibe como parámetro un target e un contexto, por exemplo:

```typescript
funtion logger(target: any, ctx: ClassDecoratorContext){
  console.log("Logging");
}

@loger
class Person {
  name = "Alex";
  greet(){
    console.log ("Hi, I'm " , this.name)
  }
}
```

Utiliza factorias de decorador permite deseñar metacódigo que pode ser reutilizado. Por exemplo:

```typescript
function withTemplate(template: any){
  const hookEl = document.getElementeById(hookId);
  cosnt p = new constructor();

  if (hookEl){
    hookEl.innterHtml = template;
    hookEl.querySelector("h1").textContent = p.name;
  }
}

@withTemplate("<h1>My object</h1>", 'app')
class Person(){
  <div id="app"/>
  Alex // renderizdo
}
```

Este decorador pode agregar a clases.

```typescript
return function<T extends {new(...arg:any[])}:[props]>(originalContructor: T){
  return class extends originalConstructor{
    contructor(..args: any[]);
    super();
    // logic
  }
}
```

Unha factoría de decoradores é unha función que produce decoradores. Para iso basta rodear unh decorador con unha función que a rodea:

```typescript
 function  replacer<T>(initValue: T) {
  return función replaceDecorator(target:undefined, context: ClassFieldDecoratiorContext){
    return (initialValue) => {
      return initValue;
    }
  }
};

Class Person{
  @replacer("Alex")
  name = "";

}
```

Os decoreadores de accesos e métodos permiten devolver valores modificados, pero non os de campod de clase ou de parámetros.

Pode devolver unha nova función pero para poder conservar o contexto hai que preparala convenientemente:

```typescript
return function (this: any) {
  target.apply(this);
};
```

### 6.2. Decoradores experimentais de TypeScript

Cómpre modificar a configuración de typescript para establecer o target a "es6" e experimental decorators a true.
Un decorado é unha función que recibe como parámetro o contructor da clase. Por convención escríbese con maiúsculas. Por exemplo,

```typescript
function Logger (contructor:Function){
  console.log(contructor)
}

@Logger
Class Person() {
  name = "Alex";
}
```

Outra posibilidade é contruír unha factoría de decoradores de clase, que é unha función que devolve unha función anoónimma

```typescript
function Logger (...args: any[]){
  return function Logger (contructor:Function){
    console.log(contructor)
  }
}

@Logger
Class Person() {
  name = "Alex";
}
```

A función que decora unha propiedade recibe dous paramétros: target: any e propertyName: string | Symbol.
A función que decora un accesor recibe tres parámetros: target: any, name: string, descriptor: PropertyDescriptor.
A función que decora un métod recibe tres parámetros:target: any, name: string, descriptor: PropertyDescriptor.
A función que decora un parámetro recibe tres parámetros: target: any, name: string | Symbol, position: number,

Nun decorador de clase pódese devolver a clase orixinal modificada. Para isto necesitamos que a factoría sexa xenérica e que o decorador devolva unha función contructora a través de palabra reservada `class`

#### 6.2.1. Decoradores de clase

Para crear un decoreador de clase a función debe cumprir unha serie de requisitos. Debe estar tipada como xenérica para poder recibir os argumentos que conviñer e deb retornar unha clase anómica que estenda o tipo recibido. Nesta clase recibida setearáns as novas propiedades. Por exemplo:

```typescript
function logger<T extends new (...args: any[]) => any(target:T, context: ClassDecoratorConntex)> {
  return class extends target{
    age = 35;
  }
}

@logger
Person{
  name = 'Alex';
  greet(){
    console.log("Hi, I'm", this.name)
  }
}

const alex = new Person();
alex.age // 35
```

### 6.2.2. Decoradores de métodos

Para crear un decoreador de método tamén hai que definir unha función que recibe como parámetro o target de tipo Function e un contecto de tipo ClassMethosDecoratorContext. Por exemplo, este é un decorador que fai un autobind do método de clase.

```typescript
function autobind(target(...arg: any[] =>any, context: ClassMethosDecoratorContext)){
  contend.addInitilizer(function(this:any)){
    this[context.name]=this[context.name].bind(this);
  }
}


class Person{
  name = 'Alex';

  @autobind
  greet(){
    console.log("Hi, I am", this.name);
  }
}

const alex = de Person();
const greet = alex.greet
greet(); // Hi, I am Alex <- funciona porque a función esá logueada.
```

### 6.2.3. Decoradores de campo de clase

Tamén se definen a traves unha función que recibe un target de tipo undefined e un contexto de tipo ClassFieldDecoratorContext e retorna unha funcion que recibe o valor inicital e devolve un novo valor e sobreescribiría o valor do campo. Por exemplo:

```typescript
function fiellLogger(target: undefined, context: ClassFieldDecoratorContext) {
  return (initialVlaue: any) => {
    return "";
  };
}
```

## 7. Módulos e namespace

### 5.1. Módulo de ECMAScript

Importa funcionalidades con `import`.
Exporta funcionalidades con `export`.

### 5.2. Namespace

Un `namespace` agrupa código relacionado que está en diferentes que está relacionado en diferentes ficheiros.

O ´codigo partillado rodéase nun ficheiro aparte por un obxecto indicado coa palabra reservada `namespace` e no código principal referénciase cada ficheiro e ródéase co memos obxecto. Ten problemas de verbosidade.
exporta un conto de elementos exportados. Axuda a organizar paquetes.

```Typescript
namespace name{
    export ...
}
```
