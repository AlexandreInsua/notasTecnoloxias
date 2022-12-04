https://www.youtube.com/channel/UCb8GU-z39BQxoRtg2FLY-MQ

# Prerrequisitos

node.js
java jdk
android studio

# Instalar ionic 4

 install -g ionic

# Comprobar versión

ionic -v

# Comezar un proxecto

ionic start  [nome da aplicación] [template] [--type=  ]
template: blank | tabs | sidemenu | my-first-app | blankn
type: angular | reac | vue
pregunta se integra capacitor

# Rodar unha aplicación

ionic serve
ionic serve --lab // diferentes vistas en principais sistemas Android/Window/IOS

Información do entorno
	ionic info

Información do proxecto
	ionic config get

Crear compoñente de angular. Para poder usar a compoñente hai que importala no app.module da principal
	ionic generate component [nome do component]

Crear directiva de angular. Unha boa práctica é crear un directorio específico
	ionic generate directive [nome da directiva]

Crear provider de angular. Unha boa práctica á crear un directorio especifico
	ionic generate service [nome do provider]

crear tabs de ionic DEPRECATED
	ionic generate tab [nome da tab]

crear páxinas
	ionic generate page [nome da páxina]

Crear pipe de angular
	ionic  generate pipe [nome do pipe]


Navegación 
	Non usa o router de Angular. Usa un sistema análogo ás aplicacións nativas. Cando se inicia unha aplicación, as vistas vanse agregando a unha pilla de obxectos navCntrl (navigation controller). 
	

Temas
	Conxunto de estilos para mostrar os elementos da aplicación.
	Sass 


Crear un novo tab
	- xérase unha nova páxina: 
	- impórtase en tabs.module > imports
	- en tabs.router.module impórtase e engádese outro elemento coa mesma estrutura que os anteriores
	- Engádese na lista de tabs.page.html



Compoñentes de Ionic
	ion-item
	ion-button
		
	ion-list. dentro leva items
		lines="none" elimina as liñas "full" ocupa toda a liña "inset"
		inset ="true" marxe superior e esquerda

	ion-card composta por 
		ion-card-header
			ion-card-title
			ion-card-subtitle
		ion-card-content

	ion-img src="" on line ou en assets (BP!)

	action-sheet
		- importáse a librería do action-sheet no ts do compoñente
		- crease un json que representa a action sheet ~ activity													  constructor(public sheet: ActionSheetController) {
					  }
					  async showActionSheet() {
					    const sheet = await this.sheet.create({
					      header: 'Estas son as opcións:',
					      buttons: [{
					        text: "primeiro",
					        role: "destructive",
					        icon: "alarm"
					      },
					      {
					        text: "segundo",
					        icon: "add-circle-online"
					      }]
					    });
					    await sheet.present();
					  }
		- Créase un botón para lanzar a action sheet

	ion alert
		


Módulo ngx-datatable

# ACTUALIZAR VERSIÓN ANGULAR (GLOBAL)

1. Desinstalar os paquetes anteriores de Angular Cli

	`npm uninstall -g ionic`

2. Borrar a caché

	`npm cache clean --force`

3. Instalar a última versión de angular

	`npm install -g @ionic/cli@latest`

	2020.07.30. Actualizo a versión 12.1.4. Saen 3 warnings. Creo un proxecto de cero parace ir ben.

# ACTUALIZAR PROXECTO

Para actualizar un proxecto o mellor é ir actualizando de versión a versión. A web de Angular ten unha sección específica. 

2020.08.01.
1. Borrar o `package-lock.json`
2. Comitear os cambios
3. Actualizar `ng update`
4. Actualizar `npm install --force`
5. Actualizar outras depedencias

	`npm install @ionic/angular@latest`

	`npm install @ionic/angular@latest @ionic/angular-toolkit@latest`

# CAPACITOR

## Correr unha aplicación en emulador

Agregar Adroid

`ionic capacitor add android`. Crea unha carpeta `/android` cun proxecto de Android.
Modificar o id da aplicaciíón no ficheiro `capacitor.config.ts`
Importar o proxecto en Android Studio. 
Pode dar un problema porque non encontra o script `capacitor.settings.gradle`. 
Corro `ionic capacitor sync android` e crea o ficheiro.

## Aplicar cambios

Para aplicar os cambios que se van facendo hai que executar
`ionic capacitor copy android`

Para aplicar os cambios en tempo real hai que executar (se dá algún problema hai que engadir a flag `--external`)
`ionic capacitor run android -l --host=[ip da máquina]`




# FIREBASE
Un documento é a unidade minima de información. Cada un ten un identificador único e uns campos.
Unha colección é un grupo de documentos. 
Unha colección pode almacenar coleccións.


private db: AngularFirestore;

ler un documento
```typescript
this.db.doc(url + uuid)
	.snapshotChanges().subcribe( // cambios en tempo real
		snap.data
	)  

	.get().subscribe(
	snap =>{
		snap.data();
	})

```


# EMULADOR

Usamos o emulador de Android Studio. 