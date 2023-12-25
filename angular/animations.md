## Angular Animations

As animacions de Angular setéanse no decorador @Component na propiedade `animations`. Nesta propiedade vai ir un arrain con varios elementos.

Os primeiro é a funcion `trigger` (de ng/core) que recibe dous parámetros, un o nome da animación e outro que será a definció da animación que vai ser tamén un array.

Na template a sintaxe é [@nome]="expresion" que vicula a animacion con una propiedade do esado do compoñente que, cando mude, disparará a animación.

O segundo parámeto da función `trigger` é un array que define a transición. Esta definición consiste en varios estados e varias transicións.

Un estado defínese coa función `state`que recibe como parámetro o valor da expresión bindeada no template e un función `style`que recibe un obxecto co estilo css que se vai a aplicar a este estado. Para poder disparar a animación haberá unha función que muda o vlor da expresión do template (ou a expresión resólvese como parte do ciclo de vida do compoñente).

A propiedade `animations`, ademáis da función `trigger`, implementan a función `transition` que se encarga de manexar (e suavizar) o efecto da animación.

A función `transition` recibe dous parámetros. O primeiro é un strin que representa a dirección de cambio de estado e o segundo é a función `animate`. Esta función recibe como primeiro argumento o tempo en milisegundos e pode un segundo de tipo `style()`. A función `transition` pode recibir varios estados e animación para obter resultados máis complexos., enviando en lugar desta función como segundo parámetros un array composta de `style()` e `animate()`. Trátase do estado inicial e animación sucesivas.

Existe un valor especial nos estados, o _void_ que contrloa o estado dun elemento que aparece ou desparece. Tamén existe un o valor _\*_ que representa calquera estado.

Estas animacións pódense cambicar con keyframes estándares.

As animacións para unha transición tamén se poden agrupar co método `group()`e que se executan ao mesmo tempo.

Finalmente, estas animacións incoporarn un eventos se que poden capturar coa sintaxe de binding `(@animation)="expresion"`. Deste xeito pódese executar certa lóxica cando se dispara una animación.
