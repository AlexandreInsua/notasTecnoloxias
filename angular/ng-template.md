# NG-TEMPLATE PLANTILLAS EN ANGULAR

## Introdución

A directiva `ng_template` represetna unha template de Angular. O contido desta tag conén parte dunha template que poderá unirse a outras para formar a template do compoñente. Angular usa esta directiv por detras das directivas estruturais _ngfIf_, _ngFor_ e _ngSwitch_. Comecempos por un exemplo sinxelo.

```typescript
@Component({
  selector: "app-root",
  template: `
    <ng-template #buttons>
      <button class="tab-button" (click)="login()">{{ loginText }}</button>
      <button class="tab-button" (click)="signUp()">{{ signUpText }}</button>
    </ng-template>
  `,
})
export class AppComponent {
  loginText = "Login";
  signUpText = "Sign Up";
  lessons = ["Lesson 1", "Lessons 2"];

  login() {
    console.log("Login");
  }

  signUp() {
    console.log("Sign Up");
  }
}
```

Cando se proba o exemplo anterios non se renderiza nada e este é o comportamento agardado porque a etiqueta `ng-template` define unha template, pero esta non se está a usar, para iso usa a directiva estrutural `ng-container`

## A directva `ng-container`

Para evintar crear divs adicionais, podemos usar a directiva `ng-container`que nos fornece dun ámbito ao que lle podemos vincular unha directiva estrutural.

```typescript
<ng-container *ngIf="lessons">
    <div class="lesson" *ngFor="let lesson of lessons">
        <div class="lesson-detail">
            {{lesson | json}}
        </div>
    </div>
</ng-container>
```

Pero esta necesidade está en retroceso a partir da version 17 pola nova sintaxe do flow template `@if`, `@for` e `@switch`.

## A directiva `ngTemplateOutlet`

Hai outro caso de uso, que permite inxextar una template dinamicamente.

Pódese tomar a template mesma e instancias a través da directiva `ngTemplateOutlet` pasándolle a referencia da template mediante a referencia da template:

```typescript
<ng-container *ngTemplateOutlet="buttons"></ng-container>
```

Isto mostrará os botóns de logueo e deslogueo.

## Contexto da template

Dentro da etiqueta `ng-template` temos acceso ás mesmas variables que a template externa. Ademais casa template tamén pode definir un obxecto **`context`** que contén todas as variables de entrada da plantilla:

```typescript
@Component({
  selector: "app-root",
  template: `
    <ng-template #estimateTemplate let-lessonsCounter="estimate">
      <div>Approximately {{ lessonsCounter }} lessons ...</div>
    </ng-template>
    <ng-container *ngTemplateOutlet="estimateTemplate; context: ctx">
    </ng-container>
  `,
})
export class AppComponent {
  totalEstimate = 10;
  ctx = { estimate: this.totalEstimate };
}
```

Neste exemplo tempos unah variable de entrada chamada `lessonscounter`, definida usando o prefixo let-. Esta variable non está visible fóra da template. O contido desta variable está determinado pola expresión asignada á propiedade. Esta expresión avalíase contra o obxecto do contexto pasado á directiva `ngTemplateOutlet` xuntoa coa temlate que instancias.

## Referencias de template

Do mesmo xeito que podemos referencias a plantilla, podemos inxectala directamente usando o decorador `@ViewChild`:

```typescript
@Component({
  selector: "app-root",
  template: `
    <ng-template #defaultTabButtons>
      <button class="tab-button" (click)="login()">
        {{ loginText }}
      </button>
      <button class="tab-button" (click)="signUp()">
        {{ signUpText }}
      </button>
    </ng-template>
  `,
})
export class AppComponent implements OnInit {
  @ViewChild("defaultTabButtons")
  private defaultTabButtonsTpl: TemplateRef<any>;

  ngOnInit() {
    console.log(this.defaultTabButtonsTpl);
  }
}
```

Como se pode ver, a plantilla pódese inxectar como calquera outro elemento ou compoñente do DOM, proporcionando o nome da referencia ao decorador `@ViewChild`.

## Compoñentes configurables

Tomemos com exemplo un contender de pestas onde queresmo configurar a apariencia dos botóns. Primeiro defínese unha plantilla:

```typescript
@Component({
  selector: "app-root",
  template: `
    <ng-template #customTabButtons>
      <div class="custom-class">
        <button class="tab-button" (click)="login()">
          {{ loginText }}
        </button>
        <button class="tab-button" (click)="signUp()">
          {{ signUpText }}
        </button>
      </div>
    </ng-template>
    <tab-container [headerTemplate]="customTabButtons"></tab-container>
  `,
})
export class AppComponent implements OnInit {}
```

Despois no compoñente defínese una propiedade de entraa que tamén é unha plantilla:

```typescript
@Component({
  selector: "tab-container",
  template: `
    <ng-template #defaultTabButtons>
      <div class="default-tab-buttons">...</div>
    </ng-template>
    <ng-container
      *ngTemplateOutlet="headerTemplate ? headerTemplate : defaultTabButtons"
    >
    </ng-container>
    ... rest of tab container component ...
  `,
})
export class TabContainerComponent {
  @Input()
  headerTemplate: TemplateRef<any>;
}
```

Asi, hai una plantilla predefina para os botóns que será usada cnado a propiedade de input permaneza indefinida.
