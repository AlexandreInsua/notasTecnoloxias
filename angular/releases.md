# Angular 16
 
## Angular signals

É unha libraría que permite definir valores reactivos e expresar dependencias entre elas. Por exemplo neste compoñente:

```Typescript
import { Component, Signal } from '@angular/core';

@Component({
    selector: 'my-app',
    standalone: true,
    template: `
                {{fullname()}}
                <button (click)="setName('John')">Click me!</button>
              `
})

export class App {
    firstName = signal('Jane');
    lastName = signal('Doe');
    fullName = completed(() => `${this.firsName} ${this.lastName}`) // ollo! isto é unha función

    constructor(){
        effect(() => console.log('Name changed:' this.fullName()));
    }

    setName(newName: string){
        this.firstName.set(newName);
    }
}
```

créase un valor calculado fullName que depende (reaciona?) dos sinais `firstName` e `lastName`. Tamén declaramos un **efecto** que se executará cando cambie o valor de calquera dos sinais. Cando se modifica o valor de `firstName` loguea a mensaxe na consola (Renderiza o novo valor?).

Pódese transformar un sinal nun observable: 

```Typescript
import { Component, OnInit, Signal } from '@angular/core';
import { toObservable } from '@angular/core/rxjs-interop';

@Component({ ... })
export class App implements OnInit {
    count = signal(0);
    count$ = toObservable(this.count);

    ngOnInit(){
        this.count$.subscribe( ()=> ... );
    }
}
```
Aquí hai un exemplo de como transformar un observable a un sinal para evitar o uso do pipe async:

```Typescript
import { Component, Signal } from '@angular/core';
import { toSignal } from '@angular/core/rxjs-interop';
import { DataService } from './services/dataservice';

@Component({ 
    selector: 'my-app',
    template: `<li *ngFor="let row of data()"> {{row}} </li>` 
 })
export class App {
    dataService = inject(DataService);
    data = toSignal(this.dataService.data$, []);
}
```
Tamén se introduce o novo operador de RXJS `takeUntilDestroyed`.
O seguinte paso é traballar en compoñentes baseados en observables.

## Renderizado do lado do servidor e hidratación

Hai un novo sistema de renderizado do lado do servidor que xa non renderiza a app de cero, senón que busca nodos do DOM que existen mentres crea as estruturas de datos e os event listeners. Configuráse no ficheiro `main.ts`:

```Typescript
import { bootstrapApplication, provideClientHydratation } from '@angualar/platform-browser';

bootstrapApplication(RootCmp, { providers: [provideClientHidratation]});
```

Tamén melloraron o comando **ng add** e soporte para Content Security Policy.

## Mellora da cli

Crea a app sen moódulos co comando `ng new --standalone` que produce compoñentes, directivas e pipes standalone por defecto.
Configura o Zone.js no boostrapApplication no `main.ts`: 

```Typescript
import { bootstrapApplication } from '@angular/platform-browser';

bootstrapApplication(App, {providers: [ provideZoneChangeDetion({eventCoalescing: true})]});
```

Agora úsase *Vite* pra correr o comando `ng serve` que mellora experiencia de desenvolvemento. Hai que configuralo no `angular.json`:

```json
"architect": {
    "build": {
        "builder": "@angular-devkit/build-angular:browser-esbuild"
    }
}
```

## Testing con jest

Hai soporte para Jest. Pódese instalar con `npm jest -D` e actualizar o angular.json:

```json
"projects": {
    "my-app": {
        "architect": {
            "test": {
                "builder": "@anguar-devkit/build-angular:jest",
                "options": {
                    "tsConfig": "tsconfig.spec.json",
                    "polyfills": ["zone.js", "zone.js/testing"]
                }
            }
        }
    }
}
```

## Autocomplete en inportacións de templates

O servizo da language permite autoimportacións en compoñentes e pipes.

## Mellora de experiencia de desenvolvemento

## Marcar un input como obrigatorio:
```Typescript
@Input({required: true}) title: string = ""
```
## Pasar router data como imput:
```Typescript
const routes = [ 
    {path: 'about',
     loadcomponent: inport('./about'),
     resolve: {contact: () => getContact()}} 
]

@Component({ ... })
export class AboutComponent {
    // O valor de 'contact' pásase desde a ruta ao input.
    // Isto dificulta algo a lexibilidade e a traza da información
    @Input() contact?: string; 
}
```

## CSP soporte para estilos en liña

## ngOnDestroy flexible

A partir desta versión pódes inxetar unha dependencia de destrución:

```Typescript
import { Injectable, DestroyRef } from '@angular/core';

@Injectable({ ... })
export class AppService {
    destroyRef = inject(DestroyRef);
    destroy (){
        destroyRef.onDestroy(()=> /* clean up */);
    }
}
```

## Etiquetas autoconclusivas

Antes 
```html
<component [prop]="value"></component>
```

Agora
```html
<component [prop]="value"/>
```