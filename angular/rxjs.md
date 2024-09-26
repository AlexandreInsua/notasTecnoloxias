# A reactividade en Angular

## O concepto de Stream e de Observable

Como o Frontent é inherentemente asíncrono, necesitamos ferramentas para implementalo. Un **Stream** (_fluxo_) é un un conxunto de valores no tempo. Pode ser un conxunto de valores emitidos por unha API ou de eventos ocorridos no navegador ou como resultado da execución de ferramentas da web API estándar. Todo o que sucede no navegador é subsceptible de ser tratado como un stream.

Necesitamos un xeito de crear streams, subscribirmonos a eles, reaccionar a novos valores e combinar fluxos para construír novos streams.

Un Observable é un tipo de datos primitivo que implementa unha API como un array, incluíndo métodos funcionais, pero é diferente dun stream. Precisamente, é unha abstracción uqe permite manexar streams de datos.

Por tanto _Streams_ e _Observables_ snon son os mesmos. Un _Stream_ é unha secuencia continua de datos, mentres que un _Observable_ é unha abstracción que represnta un fluxo de datos asíncronos que pode emitir un ou varios valores, é un xeito de acceder a un stream e necesita ser subscrito para ser usado. Por convención, os nomes dos observables en Angular teñen un signo do dólar ao final.

## Intro a RxJs

**Reactive Extensión for JavaScript** (_RxJs_) é unha librería que implementa observables par Js. Por exemplo, o fluxo de datos `0, 1, 2, 3, 4`, emitido un valor cada segundo implementado usando RxJs é

`const obs = interval(1000).pipe(take(5))`

Emitidos os cinco valores, o Observable complétase e xa non emite máis valores. `interval(100)` crea un stream e emite un valor cada segundo. `take(5)` é un exemplo de operador que toma un Observable e devolve outro. `pipe()` é un operador que ten una sintaxe análoga á pipe de Unix: recibe un valor e devolve outro.

## Introdución á programación funcional reactiva

A **programación funcional reactiva** (_functional reactive programming, FRP_) é un paradigma que afirma que un programa pode ser feito enteiramente a través de fluxos. O desenvolvemento consiste en crear os streams adecuados, combinalos, e subscribirse a eles para reaccionar aos novos valores.

A idea principal consiste en construír programas declarativos onde o estado está gardado no DOM ou nos streams e non no código. Esta ausencia de estado refírese a compoñentes intelixentes que teñen servizos de datos, no a compoñentes puros que poden querer manter algunah variable de estado interno a xeito de flag.

## Como funcionan os Observables

Hais dous tipos de observables

- **Cold** (_frío_): non xera valores se non ten ningunha subscrición activada.
- **Hot** (_quente_): xera valores aínda que non teña ningunha subscrición activada.

Un Observable pode ser compartido ou non.

## Operadores de RxJs máis usados

Angular usa os operadores de RxJs de dous xeitos:

- Como un mecanismo de implementación interna, como pode ser os EventEmiters, Subject, BehaviorSubject, etc...
- Como parte dalgunha API pública, como formularios ou as peticións do módulo de HTTP.

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

Toma os valores dun observable e devolve outro observable que emite aqueles valores oaqueles que satisfagan unha condición xestionada por unha función que recibe como parámtro:

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

### O operador concat

O operador contat realiza varias peticións ao mesmo tempo. Recibe varios observables e devolve un só. Agarda a que o observable se complete antes de pasar ao seguiten.

## Operadores de mapeo de orde superior (Higher order RxJs mapping operators)

Para entender estes operadores antes hai que entender as estratexias _concat_, _merge_, _switch_ e _exhaust_ para entender os seus operadores de mapeo correspondente.

### O operador map de RxJxMap

O operadores _map_ toma un stream de entrada e crea outro stream de saída con valores derivados. Por exemplo, para un input stream con valores {1, 2, 3} e un mapeo tal que map(x => x\*10) temos un output stream con valores {10, 20, 30}. Por tanto o operador map consiste en asignar ou mapear os valores do observable de entrada.

Aquí hai un exemplo de como se usaría para xestionar unha petición http:

```TypeScript
const http$: Observable<Course[]> = this.http.get('api/courses);
http$.pipe(
    tap(()=> console.log("HTTP Request executed")),
    map( response => Object.values(res['payload']))
)
.suscribe(
    courses => console.log("Courses": courses)
)
```

Aquí estamos facen unha petición http que devolve un obxecito Json. A resposta está envolvendo os datos dentor da propiedade _payload_. Para chear a esta propiedade aplicamos o operador _map_ que mapea a resposta e extrae o valor da propiedade payload.

Nun mapeo de orde susperior en lugar de mapear un valor plano a outro, imos mapear desde un valor a un observable. O resultado é un observable de orde superior cuxos valores son tamén observables aos que nos podemos subscribir de xeito separado.

Este tipo de mapeo ocorre a cotío. Por exemplo, temos un formulario reactivo que está a emitir valores dun formulario válido no tempo a través dun observable:

```TypeScript
@Component({
    selector: 'course-dialog',
    templateUrl: './course-dialog.html'
})
export class CourseDialogComponent implements AfterViewInit {
    form: FormGroup;
    course: Course;
    @ViewChild('saveButton') saveButton: ElementRef;

    constructor(
        private fb: FormBuilder,
        private dialogRef: MatDialogRef<CourseDialogComponent>,
        @Inject(MAT_DIALOG_DATA) course: Course
    ) {
        this.course = course;
        this.form = this.fb.group({
            description: [course.description, Validators.required],
            category: [course.category, Validators.required],
            releaseAt: [new Date().getTime(), Validators.required],
            longDescription: [courese.logDescription, Validators.required]
        })
    }
}
```

O formulario reactivo preve un observable this.formValueChanges que emite os últimos valores do formulario a medida que o usuario interactúa con el. Ese será o obsrvate base. Queremos gardar os valores a medida que se van producindo para implementar unha función de pregardado para evitar gardar cambios en caso de recarga. Para facer isto necesitamos tomar o cambio e faer unha petición contra o backend e isto levariamos ao antimodelo de subscricións anidadas:

```TypeScript
this.form.valueChanges
    .subscribe(
        formValue => {
            const httpPost$ = this.http.put(`api/course/${courseId}`, formValue);
            httpPost$.subscribe();
        }
    )
```

Isto levaríanos a añiñar o código multiples vese que é algo que queremos evitar. Denominaresmo Observable interno ao novo httpPost$.

## Evitando subscripcións aniñadas

Queremos facer todo isto de xeito máis conveniente. Queremos tomar ese valor e convertilo nun observable de gardado. Isto creará un observable de orde superior onde cada valor corresponde con unha petición de gardado. Queremos subscribirnos a cada un desde observables de rede e recibir todas as respostas de rede nunha soa vez para evitar aniñamentos. Iso faise cos operadores de orde superior. Por que necesitamos 4 operadores diferentes?

Imaxinemos que suceden se se emiten múltiples valores, nunha sucesión rápida, a través do observable valueChanges e a operación de gardado tarda certo tempo:

- Debemos agardar a que se complete unha solicitude de gardado antes de realizar outra?
- Debemos facer varios gardados en paralelo?
- Debemos cancelar varios gardados en curso e iniciar un novo?
- Debemos ignorar novos intentos de gardado mentres hai un garade en curso?

No exemplo de subscricións añiñadas, estamos a disparar operacións de gardado en paralelo. Non queremos iso porque non hai garantía de que o backend xestiona os gardados secuencialmente e de o último valor válido do formulario sexa o que o backend almacene.

### Entendo o concatenado de observables

Para implementar os gardados secuenciais, imos introducir a noción de concatenación de observables. Aquíe hai un exemplo coa función _concat_ de RxJS:

```Ts
const series1$ = of('a', 'b');
const series2$ = of('x', 'y');
const result1$ = concat(series1$, series2$).
result1$.subcribe(console.log)
```

ten como saída

```Ts
// a
// b
// x
// y
```

Como vemos os valors son o resultado de concatenar os valores emitidos polos obervables series1$ e series2$. Pero isto sucede porque os observables se están observando.

O que sucede é que a función concat se subscribe ao primeiro observable pero non ao segundo. Cando series1$ emite un valor, este reflíctese no result$, que emite ese valor. Cando series1$ emite un segundo valor, reflectirase no result$, que emite ese valor. Entón series1$ complétase e concat, subscríbe a series2$, como se pode ver na saída. A concatenación consiste en completar observables.

Volvendo ao exemplo do formulario, , debemos asegurarnos de que os valores do formulario se gardan secuencialmente. Por tanto, debemos tomar cda valor emitido e asignarllo a httpPost$. Lote tepos que subscribirmos a el pero queremos que o gardado se complete antes de subscribirmos ao seguinte observable.

Para garantir a secuencialidade debemos concatenar os múltiples observables httpPost$. A continuación, subscribiremonos a cada httpPost$ e xestionaremos o resultado de cada solicitue. Necesitamos un operador que:

- Realiza unha operación de orde superior, tome o valor emitido por valueChange e o transforme nun observable httpPost$.
- Unha operación concat, concatenando os múltiples observables htttpPost$ para asegurarnos de que un gardado http non se realiza outro gardando antes de que se complete o anterior. O que necesitamos é o operador concatMap.

### O operator concatMap

Así é como luce a solución:

```Ts
this.form.valueChanges
    .pipe(
        concatMap( formValue => this.http.put(`api/course/${courseId}`, formValue))
    )
    .subscribe(
        {
            saveResult => // handle successful,
            error => //handel error
        }
    )
```

Como primeiro beneficio, xa non hai subscricións aniñadas. Ademais agora os valores do formulario vanse facer secuencialmente. De se inspeccionar a rede no navegador cada petición empeza so cando a anterior está completada. Esta sería a implementación lóxica para unha feature de gardado de borrador, pero pode enriquecerse con outros operadores.

### Fusionando observables

Un escenario difrente do anterior é cando necesitamos que as operacións se realicen en paralelo. Neste caso temos que mudar a estratexia de combinación de observables. A fusón (merge) non agardará a que un observable se completa antes de subscribirse a un segundo, senón que se subscribre ao mesmo tempo e emite os valores de cada observable a medida que van chegando. Para ilustrar isto tomemos un exemplo onde os observables nunca se completan.

```Ts
const series1$ = interval(1000).pipe(map(x =>  x * 10));
const series2$ = interval(1000).pipe(map(x =>  x * 100));
const result$ = merge(series1$, series2$);
result$.subscribe(console.log)
```

O resultado combina os valores emitidos por ambos observables

```Ts
// 0
// 0
// 10
// 100
// 20
// 200
```

Os resultados dos observables de input aparecen inmediatamente despois de emitirse. Se un observable de input se completa, o operador merge continuará emitindo os valroes doutros observables.

### O operador MergeMap

Toma cada vaor dos observables de input e os mapea nun observable interno ao que se subscribe.
A medida que os observables de input emiten valores son emitidos polos observable interno. Isto significa que podemos ter varios observables emitindo valores en paralelo. No log da rede veremos que as peticións se realizan en paralelo e posiblemente se completen desordenadamente.

### Conmutando observables

A noción de conmutación está próxima á de fusión porque non agardamos a que ningún observable se complete. Cando un novo observable comeza a emitir desuscríbese do anterior, antes de subscribirse ao novo.

### O operador switchMap

Cando un segundo observable emita un valor, desuscríbese do primeiro e subscríbese ao sgundo emitindo ese valor. Un caso de uso poder ser un input de busca:

```Ts
const searchText$: Observable<string> = fromEvent(this.input.nativeElement, 'keyup')
.pipe(
    map( event => event.target.value),
    startWith(''),
    debounceTime(400),
    distinctUntilChanged()
)

const lessons$: Observable<Lesson[]> = searchText$.
.pipe(
    switchMap( search = this.loadLessons(search))
)
.subscribe();

function loadLessons(search: string): Observable<Lesson[]>{
    const params = new HttpParams().set('search', search);
    return this.http.get(url, {params})
}
```

O rexistro de rede mostrará que as peticións anteriores se cancelan cano se diparan as seguintes.

### A estratexia exhaustiva

Existen escenarios onde queremos ingnorar novos valores ata que os valores anteriores se procesn completamente. Por exemplo, un click no botón de gardado. Unsando o operador exhaustMap conseguiremos.

### O operador ExhaustoMap

### Escoller operador

Sacuencialidade -> concatMap
Paralelismo -> mergeMap
Cancelación -> switchMap
Completado -> exhaustMap

## Tratamento de erros

O operador `catchError()` captura un erro no observable para ser manexaod retornando outro observable ou lanzando un erro.

O operator `throwError()`crea un observable que creará un ero e o enviará ao consumidor inmediatamente despois da subscrición.
