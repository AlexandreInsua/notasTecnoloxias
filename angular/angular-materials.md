# Angular material

## Engadindo Angular material

Executamos o comando

`add material`

Este comando modifica o package e o package-lock.js. Agrega compo dependencias @angular/materiel e @angular/ckdk.
No app.module importa o BrowserAnimationsModule.
No index.html linkea a fontes, estilos e iconos.
No styles.scss agrega estilos globais
En angular.json en styles agrega os estilos dun tema.

corro ng generate @angular/core: standalon

replace-in-file
Executo os script 3 veces
1º. Converte compñentes, directivas e pipes a standalone
2º. Converte app en moduleless
3º. Elimina os módulos

Para usar os módulos de maerial hai que importas no main.ts e no compoñente de que se trate

-- main.ts --

```TypeScript
import { importProviderFrom } from "@angular/core";
import { MatSlideToogleModule } from "@angular/material/slide-toogle";
import { BrowserModule, bootstrapApplication } from "@angular/platform-browser";
import { provideAnimations } from "@angular/platform-browser/animations";
import { AppComponent } from "./app/app.component";

bootstrapApplication(AppComponent, {
    providers : [
        importProvidersFrom(BrowserModule, MatSlideToogleModule),
        provideAnimations()
    ]
}).catch( err => console.error(err));

```

O _main.ts_ nunha aplicación sen módulos inicidia a aplicación coa funcion `bootsrapApplication` que recibe dous parámetros. O primeiro é o compoñente que vai servir de arranque da aplicación e que é o punto de entrada da app. O segundo é un obxecto de configuración. Este vai recibier una propidade **providers** que é un array dos módulos de Angular que se queiran utlizar.
Repito os pasos do comando _add material_ menos a adición dun tema. No project.json hai unha opción de styles. Engao as dependencias @angular/ckk e @angular/material coa mesma versión que as outras de angular.

Para crear un compoñente hai que indicar o directore apps/recipes/ser/app usando a console de nx
