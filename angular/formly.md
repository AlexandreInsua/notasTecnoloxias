# Formly

## Configuración

Hai que agregar as dependeinas de formly/core e a libreria de estilos que se vai usar. No caso de material, tamén hai que setear o tema de estilos no `project.json`. No `appConfig.ts` hai que agrea o `provideAnimation()` e `importProfiderFrom(FormlyModule.forRoot())`.
No compoñente que se use o formulario hai que importar o FormlyModule, o módulo de estilos e o ReactiveFormModule.

## Propiedades e opcións.

Un formulario de Formly ten como inputs o form, os fields, o model e options e outputs (model change). O campo key dun field erlaciona o formuladi co modelo.

## Validacións

Poden setear no módulo raiz ou individualmente para cada campo. Para isto segundo hai varias opcions. A que parece máis simple, pero menos reutilizable é usar a propiedade validators ou asyncValidator con unha expresión e unha mensaxe.

## Expresións de formly

As expresións permiten cambiar dinamicamente as propiedades dun campo. Tamen permite aplicar un renderizado condicional. Ambos casos adminten manexar unha propiedade do modelo ou mediante unha función. Pódese capturar cando unha expesión cambia a través da propiedade options.fieldChanges que inclúe as expresións e emite un evento coa información.

## Extensións personalizadas

Unha expresión personalizada permite establecer funcionalidades transversais a todos os campos. Para definir unha extensión hai que crear un obxectio de tipo FormlyExtension que implementa unha interfaz que habilita a implementación de 3 métodos. Hai que rexistrala na configuración no módulo na entrada extensions. Aplicarase automaticamente a todos os formularios. Admiten unha propiedade prioridade.

## FormlyFielPresets

Esta funcionalidade permite reutilizar campos e está disponible no seu módulo. Definese baixo a entrada presets na configuración do módulo. Úsase como un campo normal pero o tipo vai precedido de #.

## Json Schema

É un servizo que transforma un json nun obxectio FormlyFieldConfig.

## Custom types

Hai templates prefabricadas disponibles.
Para crear un tipo personalizdo hai que definir unha clase que estende de FieldType<FieldTypeConfig>. Na template hai que psarun un tipo, un [formControl], un [formlyAttributes]="field". Os tipos personalizados hai que rexistralos na configuración do módulo en declarations e setear un alias. Para usalo na configuración dun formulario da declaración do campo asígnaselle un type co nome da clase ou a alias declarado.

## Custom wrappers

Permiene envolver un campo cun compoñente. O material ten un label, mostra mensaxes de validacións, mostra a description e os requiriods. Para definir un wraper personalizado crease unha clase que estende de Field Wrapper e que contén na template un ng-container \*field<Component> que hai que rexistrar naas declarations dun módulo e asignar un alias. Para usalo na configuración do módulo, o campo implmente a propiedades wrappers que referencia o wrappers. Para definir un wrapper por defecto na declaracion de types personalizados modifícase a configuración do módulo.
