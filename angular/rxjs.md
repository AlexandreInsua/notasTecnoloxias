# A reactividade en Angular

##  O concepto de Stream e de Observable

Como o Frontent é inherentemente asíncrono, necesitamos ferramentas para implementalo. Un **Stream** (_fluxo_) é un un conxunto de valores no tempo. Pode ser un conxunto de valores emitidos por unha API ou de eventos ocorridos no navegador ou como resultado da execución de ferramentas da web API estándar. Todo o que sucede no navegador é subsceptible de ser tratado como un stream.

Necesitamos un xeito de crear streams, subscribirmonos a eles, reaccionar a novos valores e combinar fluxos para construír novos streams.

Un Observable é un tipo de datos primitivo que implementa unha API como un array, incluíndo métodos funcionais, per é diferente dun stream.

## Intro a RxJs

**Reactive Extensión for JavaScript** (_RxJs_) é unha librería que implementa observables par Js. Por exemplo, o fluxo de datos `0, 1, 2, 3, 4`, emitido un valor cada segundo implementado usando RxJs é 

`const obs = interval(1000).pipe(take(5))`

Emitidos os cinco valores, o Observable complétase e xa non emite máis valores. `interval(100)` crea un stream e emite un valor cada segundo. `take(5)` é un exemplo de operador que toma un Observable e devolve outro. `pipe()` é un operador que ten una sintaxe análoga á pipe de Unix: recibe un valor e devolve outro.

## Introdución á programación funcional reactiva

A **programación funcional reactiva** (_functional reactive programming, FRP_) é un paradigma que afirma que un programa pode ser feito enteiramente a través de fluxos. O desenvolvemento consiste en crear os streams adecuados, combinalos, e subscribirse a eles para reaccionar aos novos valores.

A idea principal consiste en construír programas declarativos onde o estado está gardado no DOM ou nos streams e non no código. Esta ausencia de estado refírese a compoñentes intelixentes que teñen servizos de datos, no a compoñentes puros que poden querer manter algunah variable de estado interno a xeito de flag.

## Como funcionan os Observables

Hais dous tipos de observables

* **Cold** (_frío_): non xera valores se non ten ningunha subscrición activada.
* **Hot** (_quente_): xera valores aínda que non teña ningunha subscrición activada.

Un Observable pode ser compartido ou non. 

##  Operadores de RxJs máis usados

Angular usa os operadores de RxJs de dous xeitos:

* Como un mecanismo de implementación interna, como pode ser os EventEmiters, Subject, BehaviorSubject, etc...
* Como parte dalgunha API pública, como formularios ou as peticións do módulo de HTTP.

### Map

Toma os valores dun observable, tranfórmao cunha función que recibe como parámetro e devolver outro observable ao que hai que subscribirse para obter os seus valores:

```TypeScript
const observable$ = interval(500)
                        .pipe(
                            take(5),
                            map(i => 2 * 1);
                        )
observable$.subscribe(
    val => console.log(val); // 0, 2, 4, 6, 8
);
```

### Filter

Toma os valores dun observable e devolve outro observable que emite aqueles valores  oaqueles que satisfagan unha condición xestionada por unha función que recibe como parámtro:

```TypeScript
const observable$ = interval(500)
                        .pipe(
                            take(5),
                            map(i => i % 2 === 0);
                        )
observable$.subscribe(
    val => console.log(val); // 2, 4
);
```

### Reduce

Toma os valores dun observable e devolve outro observable que emite un único valor que se establece en función dunha función que recibe como parámetro, xunto co valor inicial que é reducido:

```TypeScript
const observable$ = interval(500)
                        .pipe(
                            take(5),
                            reduce((state, value)=>  state + value, 0)
                        )
observable$.subscribe(
    val => console.log(val); // 10 (= 0+1+2+3+4)
);
```

### Scan

Toma os valores dun observable, realiza unha redución como o método reduce, pero devolve un observable que emite os valores intermedios e o final do proceso da redución:

```TypeScript
const observable$ = interval(500)
                        .pipe(
                            take(5),
                            scan((state, value)=>  state + value, 0)
                        )
observable$.subscribe(
    val => console.log(val); // 0, 1, 3, 6, 10
);
```

### O operador share

Cada vez que nos subscribimos a un observal desencadena a instanciación dunha cadea de procesamento por separado. Tomemos o seguinte código por exemplo:

```TypeScript
const observable$ = interval(500)
                        .pipe(
                            take(5),
                            tap( i => console.log("obs value " + i))
                        )
observable$.subscribe(
    val => console.log("Observer 1 " + val); 
);

observable$.subscribe(
    val => console.log("Observer 2 " + val); 
);
```

O seu output será

```
obs value 0
Observer 1 value 0
obs value 0
Observer 2 value 0
obs value 1
Observer 1 value 1
obs value 1
Observer 2 value 1
...
```

O operador share permite compartir unha subscrición de unha cadea de procesamoento con outros subscritores: 
```TypeScript
const observable$ = interval(500)
                        .pipe(
                            take(5),
                            tap( i => console.log("obs value " + i)),
                            shareReplay()
                        )
observable$.subscribe(
    val => console.log("Observer 1 " + val); 
);

observable$.subscribe(
    val => console.log("Observer 2 " + val); 
);
```

Ten este output

```
obs value 0
Observer 1 value 0
Observer 2 value 0
obs value 1
Observer 1 value 1
Observer 2 value 1
...
```