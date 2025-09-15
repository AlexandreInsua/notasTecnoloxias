# NG MAT DATE TABLE

## Importar os módulos necesarios

- MatInputModule. Contén os compoñentes e directivas para manexar os inputs.
- MatTableModule. É o módulo principal que ten a directiva mat-table e os compoñentes e directivas relacionadas.
- MatPaginatorModule. Módulo para paxinar datos. Por usarse separadademente dos módulo de táboas.
- MatSortModule. Módulo opcional que permite agregar as cabeceiras ordenables.
- matProgressSpinnerModule. Módulo que inclúe un indicador de progreso.

## Introdución

A Material Data Table é un compoñente xenérico que serve para mostar datos tabulados. Pódese estilar con css pero non é necesario.
Podemos crear unha táboa de datos onde a táboa á un dive sen css. No exemplo unha lista de leccións dun curso con tres columnas.

```html
<mat-table class="lessons-table mat-elevation-z8" [datesource]="datesource">
  <ng-container matColumnDef="segNo">
    <div *matHeaderCellDef>#</div>
    <div *matCellDef="let lesson">{{leson.segNo}}</div>
  </ng-container>
  <ng-container matColumnDef="description">
    <div *matHeaderCellDef>Description</div>
    <div *matCellDef="let lesson">{{leson.definition}}</div>
  </ng-container>
  <ng-container matColumnDef="duration">
    <div *matHeaderCellDef>Duration</div>
    <div *matCellDef="let lesson">{{leson.duration}}</div>
  </ng-container>
  <mat-header-row *matHeaderRowDef="displayedColumns"> </mat-header-row>
  <mat-row *matRowDef="let row; columns:displayedColumns"> </mat-row>
</mat-table>
```

### Material data table columns definitions

A directiva matColumnsDef só define unha key. Dentro do ng-container defínese a configuración da columna. A orde dos elementos container non determina a orde de renderizado.

### Directiva auxiliares.

Hai outras directivas auxiliares para marcar o rol de cada sección da template:
· matheaderCellDef: define a cabeceira dunha columna
· matCellDef: define cada celda dentro dunha columna
Esta directvas non engades estilos

### Aplicando estilos

A fonte de datos e deseño reactivo da táboa de datos.
A táboas de datos unha API baseada en observables. Isto implica que a tába é agnóstica da orixe de datos (BE, caché, etc...). A táboa subscríbe a un observable fornecidos pola fonte de datos.

### Principos básicos de deseño de táboas de datos

Coa implementación baseada de API baseada en observables a táboa non só é agnóstica da fonte de datos senón que tamén ignora que provoca a chegada de datos.
Estas causas pode ser:
· A táboa é renderizada inicialmente.
· O usuario activa un paxinador.
· O usuario activa un ordenador.
· O usuario activa unha busca no cadro.

Porque non usar un MatTableDataSource?
Non se usa aquí porque é un elemento que está deseñado para filtrar, ordenar e paxinar un array do lado do cliente. Aquí estas operacións serán realizadas do lado do servido, neste caso da API pública.

### Obtendo os datos do backend

Para obter od datos, a nosa fonte de datos vai usar un servizo de leccións. Trátase dun servizo estándar basada en observables sen estado que usa un cliente http:

```typescript
import { Injectable, inject } from "@angular/core";
import { HttpClient, HttpParams } from "@angular/common/http";
import { Observable, map } from "rxjs";
import { Lesson } from "...domain/lesson";

@Injectable ({ provideIn: 'root'});

export class CourseService {
    private http = inject(HttpClient);

    findLessont(
        coureseId: number,
        filter: "",
        sortOrder: 'asc',
        pageNumber= 0,
        pageSize = 3
    ): Observable<Lesson[]> {}
    return this.http.get('/api/lessons', {
        params: new HttpParams()
            .set('courseId', courseId.toString())
            .set('filter', filter)
            .set('sortOrder', sortOrder)
            .set('pageNumber', pageNumber.toString())
            .set('pageSize', pageSize.toString())
    }).pipe(
        map(
            (res:any) =>res['payload'];
        )
    );
}
```

Os argumenteos que se pasan son transparentes e cubren as funcionalidades para paxinar, ordenar e filtrar os resultados.

### Implementando unha datasource

O compoñente consiste nunha clase que implementa a interface DataSource<T>. Cando se implementa cómpre indicar o tipo de dato da colección que se vai mostrar. A clase necesita implemenar os métodos _connect()_ e _disconnect()_. Ambos métodos proporcionan un argumento de tipo collecionViewer que proporciona información sobre como se mostran os datos. Tamén implementa un campo de clase do tipo BehaviorSubject<T> que recibe como tipo a collección, neste caso Lesson[] e inicializa un array valeiro.
· O método connect(). O compoñente da táboa chámao cando se arranca a táboa, que agarda a que devolva un observable que contén os datos que a táboa necesita. Neste caso, o observable emitirá unha lista de leccións. Cando o usuario interactúe sobre a táboa, o observable emitirá un novo valor. Implementamos un BehaviorSubjes privado que emitirá os valores recuperados do backend. Usamos un subject porque é un bo xeito de escribir código independentement da orde que se vai realiar: chamar BE, enlazar datos, etc.
Na implementación final, tamén se usa un indicador de carga:

```typescript
import { CollectionViewer, DataSource } from "@angular/cdk/collection";
import { BehaviorSubse, Observable, catchError, finalis, of } from "rxjs";

import { CourseService } from "./course-service";
import { Lesson } from ".../domain/lesson";

export class LessonsDataSource implements DataSource<Lesson> {
    private lessonsSubject<Lesson[]> ([]);
    private loadingSubject<boolean>(false);
    public loading$ this.loadingSubject.asObservable();

    constructor (private readonly courseService){ }

    connect(collectionViewer: CollectionViewer): void {
        this.lessonsSubject.complete();
        this.loadingSubject.complete();
    }

    loadLessons( courseId:number, filter = "", sortDirection = "asc", pageIndex = 0, pageSize = 3 ) {
        this.loadingSubject.next(true);
        this.courseService.findLessons( courseId, filter, sortDirection, pageIndex, pageSize)
            .pipe(
                cancthError(()=> of([])),
                finalize (lessons => this.loadingSubject.next(false))
            )
            .subscribe(lessons = this.lessonsSubject.next(lessons))
    }
}
```

### Implementación do indicador de carga

Debido a que a táboa ten un deseño reactivo, impleméntase un indicador de carga expoñendo un observable booleano que se inicia a false e que emite un valor tre cando se están cargando os datos.

### Implementación do método connect

O método _connect()_ necesita emitir un observable que emite os datos sen expor o lessonsSubject directament. Facelo implicaría ceder o control de cando e como se emiten os datos.

### Implementación do método disconnect

O método _disconnect()_ é invocado unha soa voez pola táboa de datos no momento da destrución do compoñente. Neste método completamos os observables creados internamente para evitar fugas de memoria.

### Implementación do método loadlessons

Este é un método público que se invocará cando o usuario realizar varias accións para cargar unha páxina con datod. O primeiro que fai é emitir un true no subject que xestiona a carga. Despois, a través do servizo, realiza unha petición http. Se os datos chegan correctamente, emitiranse de volta á táboa a traves do observable do método _connect()_. Se se produce un erro na petición, o observable do método devolverao e capturaremolo utilizando o operador _catchError()_ e emitiremos un array valeiro usando o operador _of()_. En ambos casos emitiremos un false na carga de datos.

## Ligando a fonte de datos coa táboa de datos

A táboa de datos vaise mostrar como parte da vista dun compoñente. Este compoñente terá como campos de clase:
· Un dataSource: LessonsDataSource, que define unha instancia da clase e se lle pasará á táboa a través da template.
· DisplayedColumns = ["segNo", "description", "duration"], que define a orde visual das columnas.

### Método ngOnit

Neste método chámase o método _loadLessons()_ do datasource para disparar a carga da primeira páxina de leccións, A datasource chama o servizo, que dispara a petición http para buscar os datos. Entón a datasource emite os datos a través do subject que fai que o observable devolta por _connect()_ emita a páxina de leccións. O compoñente da tába esta subscrito ao observable de _connect()_ e recupera a nova páxina de leccións. A táboa mostra a nova páxina se saber de onde proven os datos nin que provocou a súa chegada. Neste punto está mostrando sempre a primeira páxina con un tamaño de tres elementos e sen criterios de busca.

### Mostrando o indicador de carga

Usaremos o observable de loading do datasource e mostraremos nun spinner.

```html
<div class="course">
  <div class="spinner-container" *ngIf="dataSource.loadin$ | async">
    <mat-spinner></mat-spinner>
  </div>
  <mat-table>...</mat-table>
</div>
```

Como podemos ver, estamos usando a pipe async e un ngIf para mostrar ou ocultar o indicador de carga. Tamén se pode user este indicador cando se transicionan estre páxians usando a paxinación, ordenado ou filtrado.

### Agregando o paxinador

O compoñente paxinador de material que se vai usar é un xenérico que trae unha API baseada en observables. Podería ser usado para paxinar calquera cousa, non só unha táboa de dtos. O seu uso na vista é a seguinte:

```html
<div class="course">
  <div class="spinner"></div>
  <mat-table></mat-table>
  <mat-paginator
    [length]="course?.lessonsCount"
    [pageSize]="3"
    [pageSizeOptions]="[3,5,10]"
  ></mat-paginator>
</div>
```

Como se pode ver, non hai nada na vista unindo o paxinador coa táboa, iso faise ao nivel do compoñente de typescript. O paxinador só necesita saber o número total de elementos e se configura o tamaño de páxina nalgunha opción de configuración.

#### Unindo o paxinador co fonte de datos.

Este vai ser o contido co courseComponent.ts

```typescript
@Component({
    selector: 'course',
    templateUrl: './course.component.html',
    stylesUrl: ['./course.component.css']
})

export class CourseComponent implements AfterViewInit, OnInit {
    course: Course;
    dataSource: LessonsDataSource;
    displayedColumns: ["seqNo", "description", "duration"];
    @ViewChild(MatPaginator) paginator: MatPaginator;

    constructor(private courseService: CourseService, private route: ActivatedRoute) {}
}

ngOnInit(){
    this.course = this.route.snapshot.data['course'];
    this.dataSource = new LessonsDataSource(this.courseService);
   this.dataSource.loadLessons(this.course.id, "", "asc", 0, 3)
}

ngAfterViewInit() {
    this.paginator.page //??
    .pipe(
        tap(()=> this.loadLessonsPage())
    )
    .subscribe();
}

loadLessonsPage() {
    this.datasoure.loadLessons(this.course.id, "", "asc", this.paginator.pageIndex, this.paginator.pageSize);
}
```

ngOnInit. Empezamos co curso que é un obxecto disponible a través dos datos da ruta, polo que hai un resolver funcionando por detrás. O recurso é obtido do backend durante a navegación o que garante que estea cargado antes de mostrar a vista. Tamén se carga a primeira páxina directamente.

#### Como se une o paxinador á fonte de datos

A ligazón entre o paxinado e a fonte de datos faise no ngAfterViewInit. Úsase este hook do ciclo de vida do compoñente consltado a través do viewChild está dispoñible. O paxinador ten una API baseada en observables e a propiedade page como observable, que emite un valor sempre que o usuario interactúa cons botóns ou co despregable. Para cargar novas páxina subscribímonos a este observable e chamamos á función do datasource loadLessons(). Aquí úsase o operador _tap()_ dentro dun _pipe()_, porque se se fai no subscribe (que é posible) non se usa o valor emitido polo observable.

#### Engadindo cabeceiras ordenadas

Para facer que as cabecieras sexan ordenables hai que anotalas coa directiva mat-sort, por exemplo:

```html
<mat-table
  class="lessons matelevation-z8"
  [datasource]="datasource"
  matSort
  matSortActive="segNo"
  matSortDirection="asc"
  martSortDisableClear
>
  <ng-container matColumnDef="segNo">
    <mat-header-cell *matHeaderCellDef>
      <mat-sort-header>#</mat-sort-header>
    </mat-header-cell>
    <mat-cell *matCellDef="let lesson"> {{lesson.segNo}} </mat-cell>
  </ng-container>
</mat-table>
```

Ademais da directiva matSort engádense outras auxiliares:
· matSortActive. Esta directiva permite informarlle á táboa de datos cal é a columna de ordenación da táboa.
· matSortDirection. É compañeira da anterior, permite especificar a orde inicial.
· matSortDisableClear. Veces precísase especificar un terceiro estado "desordenado" onde podemos limpar a orde. Esta directiva deshabilita esta opción polo que a táboa está sempre ordenada.

#### Unindo a cabeceira de columnas ordenable coa fonte de datos

Igual que na paxinación, a cabeceira ordenable emite un observable que emite nun valor sempre que o usuario interactúa coa cabeceira.

```typescript
@Component({
    selector: 'course',
    templateUrl: './course.component.html',
    stylesUrl: ['./course.component.css']
})

export class CourseComponent implements AfterViewInit, OnInit {
    course: Course;
    dataSource: LessonsDataSource;
    displayedColumns: ["seqNo", "description", "duration"];
    @ViewChild(MatPaginator) paginator: MatPaginator;
    @ViewChild(MatSort) sort: MatSort;

    constructor(private courseService: CourseService, private route: ActivatedRoute) {}
}

ngOnInit(){
    this.course = this.route.snapshot.data['course'];
    this.dataSource = new LessonsDataSource(this.courseService);
   this.dataSource.loadLessons(this.course.id, "", "asc", 0, 3)
}

ngAfterViewInit() {
    // reset paginator after sorting
    this.sort.sortChange.subscribe(() =>this.paginator.pageIndex = 0);
    merge(this.sort.sortChange, this.paginator.page)
    .pipe(
        tap(()=> this.loadLessonsPage())
    )
    .subscribe();
}

loadLessonsPage() {
    this.datasoure.loadLessons(this.course.id, "", "asc", this.paginator.pageIndex, this.paginator.pageSize);
}
```

O observale de ordenación mistúrase co de paxinación a través do operador para forzar que o paxinador recupere a primeira páxina.

#### Filtrado

O primeiro que necesitamos é agregar un campo de busca á vista. Está é a version final da vista:

```html
<div class="course">
  <mat-input-container>
    <input matInput placeholder="Search lessons" >#</input>
  </mat-input-container>
  <div class="spinner-container" *ngIf="dataSource.loadin$ | async">
    <mat-spinner></mat-spinner>
  </div>
  <mat-table
  class="lessons matelevation-z8"
  [datasource]="datasource"
  matSort
  matSortActive="segNo"
  matSortDirection="asc"
  martSortDisableClear
>
  <ng-container matColumnDef="segNo">
    <mat-header-cell *matHeaderCellDef>
      <mat-sort-header>#</mat-sort-header>
    </mat-header-cell>
    <mat-cell *matCellDef="let lesson"> {{lesson.segNo}}</mat-cell>
  </ng-container>

  <ng-container matColumnDef="description">
    <mat-header-cell *matHeaderCellDef>
      <mat-sort-header>Description</mat-sort-header>
    </mat-header-cell>
    <mat-cell *matCellDef="let lesson"> {{lesson.description}}</mat-cell>
  </ng-container>

    <ng-container matColumnDef="duration">
    <mat-header-cell *matHeaderCellDef>
      <mat-sort-header>Duration</mat-sort-header>
    </mat-header-cell>
    <mat-cell *matCellDef="let lesson"> {{lesson.duration}} </mat-cell>
    </ng-container>

    <mat-header-row *matHeaderRowDef="displayedColumns"></mat-header-row>

    <mat-row *matRowDef="let row; comluns: displayedColuns"></mat-row>
</mat-table>

<mat-paginator [length]="course?.lessonsCount" [pageSize]="3" [pageSizeOptions]="3,5,10"></mat-paginator>
</div>
```

Como se pode ver, o input-container está usanod a proxección de de contido o que provee de acceso de propiedades nativas do input e compatibilidade cos formularios de Angular

#### Versión final do compoñente

```typescript
@Component({
    selector: 'course',
    templateUrl: './course.component.html',
    stylesUrl: ['./course.component.css']
})

export class CourseComponent implements AfterViewInit, OnInit {
    course: Course;
    dataSource: LessonsDataSource;
    displayedColumns: ["seqNo", "description", "duration"];
    @ViewChild(MatPaginator) paginator: MatPaginator;
    @ViewChild(MatSort) sort: MatSort;
    @ViewChild('input') input: ElementRef;

    constructor(private courseService: CourseService, private route: ActivatedRoute) {}
}

ngOnInit(){
    this.course = this.route.snapshot.data['course'];
    this.dataSource = new LessonsDataSource(this.courseService);
    this.dataSource.loadLessons(this.course.id, "", "asc", 0, 3);
}

ngAfterViewInit() {
    fromEvent(this.input.nativeElement, 'keyup')
        .pipe(
            debounce(150),
            distinctUntilChanges(),
            tap(
                ()=> {
                    this.paginanor.pageIndex = 0;
                    this.loadLessonsPage();
                }
            )
        )
        .subscribe();
    // resete the paginator after sorting
    this.sort.sortChange.subscribe(() =>this.paginator.pageIndex = 0);
    // and sort or paginate events, load a new page
    merge(this.sort.sortChange, this.paginator.page)
    .pipe(
        tap(()=> this.loadLessonsPage())
    )
    .subscribe();
}

loadLessonsPage() {
    this.datasoure.loadLessons(
        this.course.id,
        this.input.nativeElement.value,
        this.sort.direction,
        this.paginator.pageIndex,
        this.paginator.pageSize
    );
}
```

Vermo que se lle está asignando unha referencia ao input no DOM e loge se inxecta no compoñente usando o viewchile. A partir desta referencia podemos crear un observable a partir do evento ao elemento e xenenar unha petición ao servidor.
O operador distincUntilChanges() elimina os valores duplicados
