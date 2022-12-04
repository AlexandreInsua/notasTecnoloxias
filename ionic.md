# APUNTES IONIC

## 1. INTRODUCIÓN

Unha aplicación **nativa** usa o SDK e a linguaxe para cada plataforma. Es dispositivos móbiles implica desenvolver para Android en _Java_ ou _Kotlin_ e para Iphon con _Swift_ ou similar.
Unha aplicación **híbrida** aproveita o **Web-view** das aplicacións, que é unha compoñente que usa HTML, CSS e JS creado coa linguaxe nativa. Unha aplicación híbrida unifica a produción e o mantemento.
Unha aplicación híbrida consuma máis recursos.
Poden acceder a características nativas a través de pluggins.

### Lazyload

Ionic usa a técnica da carga lazyload. Isto implica que carga rápido .

### Estrutura dos compoñentes

module.ts
html
scss
spec.ts
ts
router.module.ts

### Carpeta enviroments

Lugar onde se establecen variables globais.

## 2. COMPONENTES BÁSICOS

### 2.1. Header

Compoñente de cabeceira. Como vai ser un compoñente aniñado dentro dunha páxina pode recibir os parámetros como valores input:
**header.ts**

```
@input() titulo:string;
```

**header.html**

```
<ion-header>
   <ion-title> {{ titulo}} </ion-title>
</ion-header>
```

**page.ts**

```
seccion = 'Entrada';
```

**page.html**

```
<app-header [titulo]="seccion">
```

### 2.2. Action Sheet

Un action sheet (_folla de accións_) é un diálogo que mostra un conxunto de accións.

### 2.3. Alert

É un diálogo que presenta presenta información ou a recolle. Aparece no top do content e pode ser pechado manualmente. Pode ter header, subheader e message.

### 2.4. Avatar

Está incluido na sección de media
É un compoñente circular que rodea unha imaxe ou un obxecto.

### 2.5. Button

Botón tradicional

### 2.6. Card

Compoñente estandar para punto de entrada

### 2.7. Checkbox

Compoñente para selección múltiple.

### 2.8. DateTime

Usa tipo de dato formato ISO 8601

### 2.9. Fab

Botón flotante

### 2.10. Sistema de grid

propiedade size funciona para todos os tamaños
hai 4 tamañso
size lg grandes, md medianas, sm pequenas, xs moi pequenas

### 2.11 Scroll infinito

O efecto de scroll dependendo de array inicial, se o length é moi grande, non collerá o efecto.
Aproximadamente hai que facer coincidir o tamaño co espazo da pantalla

O efecto do scroll cancélase con 'event.target.complete()'

### 2.13 Inputs e formularios

### 2.14 List

### 2.15 Loading

### 2.16 Menu

### 2.17 Modal

O datos envíanse do pai ao fillo dentro da propiedade componentsProp cando se chama e recíbense en Inputs.
Do fillo ao pai como un json en this.modalCtrl.dismiss() e se recibie un {data} en modal.onDidDismiss()

### 2.18 Popover

### 2.19 Progres / range

En Ionic, todo elemento que cambia responde a un evento **ionChange** que pode ser capturado

### 2.20 ion refresher

Elemento para lanzar o elemento pull-to-refresh.
Para parar o spinner hai que invocar a función event.target.complete(),

### 2.21 searchbar

Elemento para aplicar un filtro de busca nunha lista de elementos.

### 2.22 segment

Fila que agrupa varios bottons relacionados.

### 2.23 ion skeleton text

Compoñente para renderidar contido placeholder.

### 2.24 ion slides

Permite crear un slide elegante basado en Swiper

### 2.23. ion-split-pane

Compoñente que permite crear layouts multi-vista. Permite aproveitar o espazo segundo o dispostivo. Por exemplo, mostrar o menú e a page. Colócase na raíz da app.
Hai que indicarlle mediante o contentId que o menu vai ser renderizado dun lado.
Nun principio as opcións do menú non aparecerán. no `ion-menu-toggle` hai que seter `autoHide` a **false**

### 2.24 ion tabs

Compoñente de navegación. Pódense usar varias tabs para unha páxina.
Cada tab é un compoñente que se redirixe mediante unha ruta filla, children no routing-module e se cargar mediante lazy loading mediante a sintaxe `loadChildren`.

### 2.25 ion toast

Aviso breve.

## 3. CORRER EN DISPOSITIVOS EMULADOS E REAIS

#### 3.0.1 DevApp Ionic (deprecado en favor de cpacitor)

Lanzr aplicación

> ionic serve -c

### 3.1. Configuración de máquina virtual Android

Hai unha guía de instalación en Guide.
Configuración da máquina en Android Studio.
A máquina ten que ter habilitadas as opcións de debuggin.

#### 3.1.1. Cordova

Configuración inicial en entorno Instalation guide (node, npm, git)

### 3.1.1.1. Correr en máquina virtual

Require AStudio + SDK. É importante revisar a configuración das variables de entorno.

> ionic cordova prepara android : prepara a plataforma android. crea o config.xml e os resources de android. Crea un proxecto importable en AStudio
> ionic cordova build android: crea o apk en
> cordova run android

### 3.1.1.1. Correr en máquina real

Hai que ter as opcións de debugging activadas

> ionic cordova run --list
> ionic cordova run android - selecciona o dispositivo por defecto

**Actualizar cambios en real**.
Hai que correr co modo life reload
ionic cordova run android -l : activa o modo liefe reload

En IOS, ver documentación.

#### 3.1.2. Capacitor

### 3.1.2.1. Correr en máquina virtual

Executar comandos

> ionic build : crear wwww
> ionic capacitor add android: xera a pasta `android` que se pode importar en Android Studio

> ionic capacitor copy android : xera novo build

Para poder facer cambios na app e importalos no no Android Studio execútase o seguine comando
ionic capacitor run android -l --host=YOUR_IP_ADDRESS: Emite cambios

Debugging: en consola de AS. ou en DevTools/Remote devices

### 3.1.2.1. Correr en dispositivo físico

Conectar o dispositivo e seleccionado en AStudio

> ionic capacitor copy android

### 3.1. Configuración de máquina virtual Ios

Necesitamos correr unha mac
(ver hackintosh como alternativa)
Na documentación de Ionic hai documentación sobre o proceso.

## 4 NOTAS APLICACIÓN DE NOTICIAS.

O apikey do servizo colócase en enviroments/enviroments.ts

### Arquitectura da aplicación
Dentro do directorio /app colocaremos os seguintes
/components. 
/interfaces (ou models) cos modelos de datos
/pages coas páxinas
/services 
app

As **componentes** son aqueles elementos que se poden repetir. Na aplicación de noticias vai ser a lista de noticias e cada un dos items.
Van en `declarations` e en `exports`no seu propio módulo para poder ser usadas noutras partes da aplicacion. Para ser usadas, impórtase o modulo de componentes no módulo correspondente.



## 

## COMANDOS

`> ionic start nome tipo` - inicia unha aplicación

`> ionic cordova platform add android`
`> ionic cordova platform rm android` - borra unha plataforma
`> ionic cordova resources` - crea recursos para as plataformas
`> ionic cordova run --list` - devolve unha lista de dispostivos conectados
`> ionice cordova run android --target=[disposivo]` - corre no dispositivo que se indique

### debugging

Operador **debugger** lanza debugueo en devTools;
`console.log({variable})` lanza un console.log de variable e o seu valor

### Comandos ng

modificador `--dry-run` en ng corre un comando, mostra o que vai facer pero non o executa
modificador `--flat` na creación dun módulo, créao no directorio raíz, sen crear un directorio propio.

### Petadas

Problema de execución de scripts
Pode ocorrer que a consola en VSC non poda correr un script. É un problema de permisos.
Hai que abrir a powershell modo admin e correr:
`Get-ExecutionPolicy` -> restricted
`Set-ExecutionPolicy Unrestricted`
https://www.alexmedina.net/habilitar-la-ejecucion-de-scripts-para-powershell/

viewchild
úsase para facer referencia a un elemento do dom

####

@ViewChild(Elemento) nomeVvariable: TipoElemento

prefire usar a pipe async á subscripcion de datos


#### AppBrowser
Pluggin que permite abrir unha url no browser por defecto do navegador.
En app.component hai un obxecto this.statusBar que controla o estilo por defecto da barra superiro de control.

#### Socialsharing
Pluggin para partillar contidos en redes sociais. 

En dispositivos físico o localstorage non se usa porque se o dispositivo necesita espazo, borrao. Servizo de localdata para xestionar o pluggin de storage.

### Pwa
Require un service worker e un manifest. Cande se agrega o módulo de node de pwa crea un ficheiro json de configuración, o manifest.json e os iconos de aplicación.
