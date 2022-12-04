# 1. HTML

## Definicón de etiqueta

`<etiqueta atributo"valor"></etiqueta>`

## Estrutura dunha web

```<!DOCTYPE html>
<html lang="es">
    <head>
        <meta />
    </head>
    <body>
        ...
    <body>
</html>
```

## Etiquetas de texto

`<h1> ... <h6>` . Etiquetas de cabezallo. Por SEO recoméndase un so h1 por páxina
`<p>`. Parágrafo.
`<br>`. Salto de liña.
`<hr>`. Salto de liña con división visual.
`<strong>`. Resaltado de texto con negriña.
`<em>`. Resaltado de texto con cursiva.
`<span>`. Elemento de texto seleccionado
`<blockquote>`. Cita.

## Listas

Admiten aliñamento.

`<ol>`. Lista ordenada (ordered list).
`<ul>`. Lista desordenada (unordered list).
`<li>`. Elmento de lista (list item).

## Imaxes

`<img src="" alt="" title="">`
`src` fonte da imaxe. Ligazón absoluta c:/, https:// Ligazón relativa ./
`alt` texto alternativo
'title`

## Táboas

```<table>
<thead>
<tr><th>Cabezallo</th></tr>
</thead>
<tbody>
<tr><td>Contido</td></tr>
</tbody>
<tfooter>
<tr><td>resume</td></tr>
</tfooter>
```

colspan - expande a cela n columnas (horizontalmente).
rowspan - expande a cela n filas (verticalmente).

## Formularios

```
<form>
<input type="text" name="" id="" placeholder="" value="" >
```

tipos: text, password, submit, button...

```<label for="name">
<textarea>
<select>
<options>
</select>

</form>
```

# 2. CSS

## Inserción de estilos

- Dentro da etiqueta do elemento mediante o atributo **style**. Ten a máxima prioridade.
  `<div style="border-color:black">`
- Dentro da cabeceira da paxina coa etiqueta `<style>`;

```
<style>
body {
    font-family: arial;
}
</style>
```

- Chamando a un ficheiro mediante a etiqueta `<link>`
  `<link rel="stylesheet" type="text/css href="ruta.css>`

## Selectores

A prioridade de selectores e regras é a seguinte de maior a menor:

1. Operador important
2. id
3. clase
4. etiqueta
5. posición posterior no documento

- Selector universal. Selecciona todos os elementos do sitio `*`.

```
* {
    font-family: arial
}
```

- Selector de etiqueta. Selecciona todos os elementos da etiqueta referida. `div` Selecciona todas as div

- Selector de clase. Selecciona todos os elementos co atribute class referida. `.clase` seleccionaciona os elemntos con **class="clase"**.

- Selector de id. Selecciona o elemento o atributo id referido. `#id` **id="id"**.

- Selector por atributo. Selecciona os elemento cuxo atributo referido coindice co lista de atributos. `input[type="text]` selecciona todos os inputs de tipo texto.

- Agrupación de selectores. A agrupación de selectores faise mediente comas. `div, input[type="text"]` selecciona todas as div e os inputs de tipo texto.

- Selección refinada. Pódese xustapor selectores para realizar unha selección refinada. `nav ul li` seleciona todos os elemento da lista dentro dunha lista desordenada incluída nun nav. Se hai listas aniñadas, tamén as selecciona.

- Operador de fillo directo. Para salvar o aniñamento utílizase o operardor de fillo.
  `nav > ul li` selecciona os elementos da lista, pero só da lista que sexa filla directa de nav.

- Operador **important**. O operador serve para salvar a prelación de regras, pansando a ter a regra precendente a prioridade absoluta.

```
selector {
    color: rgba(225, 225, 255, 0.6) !important;
}
```

## Fontes

Importar fonte desde ficheiro

```
@font-face {
    font-family: "nome" format="string"
    src: url(path)
}
```

Importar fotne desde a rede

```
@font-face {
    font-family: "nome"
    src: url(ulr)
}
```

`font-family` establece a familia da fonte
`font-weight` establece o grosor
`font-style` establece os estilo. italic | oblique

## cores

Nomes. Non recommendaddo.
Hexadecimais. #000 ou #000000.
RGB. rgb(0, 0, 0),
RGBA. rgba(0, 0, 0, 1).

## degradados

Un degradado é unha funcionalidade de de CSS3 qeu crea unha imaxe con dous ou mais cres, polo que o seu uso máis adecuado é con `background-image`. Existen dous tipo de degradados:

### Degradados lineares

Defínese a dirección, indicando o punto de destino -vai desde o punto oposto, e as cores. Por defecto o punto de partida é top.
`background-image: linear-gradient(red, yellow);`. Gradiente de arriba a abaixo, de vermello a amarelo.
`background-image: linear-gradient(to right, red, yellow);`. De esquerda a dereita, de vermello a amarelo.
`background-image: linear-gradient(to bottom right, red, yellow);`. En diagonal, cara a esquina superior dereita, de vermello a amarelo.
`background-image: linear-gradient(20deg, red, yellow);`. En diagonal, especifícase o punto de chegada medianta un ángulo desde o punto da posición normal.
`background-image: linear-gradient(red, yellow, green);`. Con varias cores.

`background-image: linear-gradient(red, rgba(255, 0, 0, 0,5));`. Usando transparencias.

`background-image: repeat-linear-gradient(red 10%, yellow 20%, green 30%);`. Repetición dun patrón de degradado. As porcentaxes implican os puntos de principio e fin de cada cor.

### Degradados lineares

`background-image: radial-gradient(red, yellow);`. Gradiente uniforme desde o centro.
`background-image: radial-gradient(red 5%, yellow, 95%);`. Gradiente non uniforme.
`background-image: radial-gradient(circle | ellipse, red, yellow);`. Gradiente con forma determinada.
`background-image: repeat-radial-gradient(red 5%, yellow 20%);`. Repite gradiente.

## fondo

Atallo
background: color imaxe repeat position
Onde image é un url(), repeat | repeat-x | repeat-y, right | top | left | botton | center. Esta propiedade admite unha imaxe e un texto secundario
`background: url("img/background-pattern.png"), rgb(99,99,99) repeat;`

background-size para imaxes grandes
background-atachment: move a imaxe co texto

## textos

text-align. aliñar texto left | center | right
text-ident. Identado de texto.
text-decoration. Decoración do texto none | underline
text-transform. transformación de texto capitaliza | lowercase | uppercase

letter-spacing. Espazo entre letras.
`line-height`. Establece o tamaño do interlineado. Por defecto ésa calculado sobre un factor de **1,2** do tamaña da fonte. Admite valor de ratio px, em, rem, porcentase. Antigamente usábase para centrar o texto nun div, pero é unha mala práctica.
vertical-align: aliñado vertical.

word-spacing. Espazo entre palabras.

## Pseudo clases

:first-child
:nth-child(1)
:last-child

a:link. Ligazón non visitada
a:visited: Ligazón visitada

:hover. Evento de rato por riba
:activo. Estado activo.
:focus. Estado con focos

## Transformacións

O atributo `transform` aplica unha transformación a un elemenot e aos seus derivados. Os tipos de transformacións son:
matrix(a, b, c, d, e, f). combinación do resto de transformacións.
transate(x, y). Traslación en x e y.
scale(n, n). Escala en n factores.
rotate(0deg). Rotación en n grados sexadecimais.
skew(0deg). Torsion en n grados sexadecimais.

## Transicións

Cambia un conxunto de estilos cando se produce un evento
`transition: all 0ms` é o máis habitual

## Animacións

As animacións son un coxunto de estados que definen candanseu grupo de regras de estilos. Consta de dous compoñentes, un estilo no compoñente onde se describa a animación e un conxunto de estados. Cada estado está definido nun **keyframe**.

### Descrición da animación

animation-name: nome da animación
animation-duration: duración da animación
animation-delay: retardo da animación
animation-direction. dirección
animation-iteration-vount: número de iteracións. admite infinite como valor.
animation-play-state. pausa e inicio.
animation-timing-function: ritmo da animación
animation-fill-mode: define o estado final da animación.

```
#elemento{
animación: nome duración iteracións time-function
}
```

## Fotogramas da animación

```
@keyframes nome-da-animación{
    from {
        ... estilos
    }

    to {
        estilos
    }
```

A sintaxe from ... to é un _alias_ de 0% a 100%. Cantos máis keyframes teña a a animación, máis suave sera a animación.

## Modelo de caixa

Só serve para elementos que se comportan como bloque ou para aqueles que se manipulou propiedade _display_.

margin. Marxe exterior.
padding. Marxe interior.
width. Ancho.
min-width. Ancho mínimo.
max-width. Ancho máximo.
height. Alto.
min-height. Alto mínimo.
max-height. Alto máximo.

border. borde.
border-radius. Radio de borde. Pódese establecer por esquina.

float: flota elementos rompentod o fluxo de caixas.
clear: limpa o flotados.

## sombras

text-shadow: x y difuminado cor dirección
box-shadoww: x y difuminado cor dirección

Estas etiquetas ponde ter varias sombras separadas por comas (dan sensación 3D):
`text-shadow: 0px 2px 1px #333, 0px 0px 5px #f9f9f9;`

## scrolls

overflow: hidden | visible | scroll
Pode ser x, y ou ambos.

## position

- `relative`. Modifica a posición respecto a aquela que debería ter na posicion normal. As opcións son `top`, `right`, `bottom` e `left`. Cando se indica un punto de despraza desde este. O elememto manipulado conserva o seu oco reservado. Cando se usa % como unidade toma o valor do compoñente pai.
- `absolute`. Modifica a posición respescto á orixe da páxina (0,0). As opcións son `top`, `right`, `bottom` e `left`. Un tip para centrar o elemento é setear todo a 0 e un margin auto. O elemento manipulado non conserva o seu oco reservado.
- `fixed`. Respecto da posicion (0,0) da pantalla, polo que permanece fixa. O elemento manipulado non conserva o seu oco reservado.
- `sticky`. Intermedio entre relativo e fixo.  
- `z-index`. Posición no eixo z. Unha boa práctica é usar números baixos.

## Flexbox

Flexbox é una nova técnica para aplicar o modelo de caixa que substitúe o sistema de flotados. Está incluída nativamente en CSS3. Traballa un elemento **contedor** e con varios elementos **contidos**.

### Contedor

`display`. Activa o funcionamento de flexbox. Pode ter os seguintes valores:
- `flex`. Valor por defecto. Aliña os elementos nunha fila de esquerda a dereita.
- `inline-flex`. Tamén aliña os elemntos nunha fila de esquerda a dereira pero fai que o contedor ocupe.

`flex-direction:`. Disposición de elementos en fila (D), columna ou nas versións inversas.
- `row`. Disposición en filas.
- `column`. Disposición en columnas.
- `row-reverse`. Disposición en filas de xeito inverso.
- `column-reverse`. Disposición en columnas de xeito inverso.

`flex-wrap`. Permite ou evita que os elementos sobrantes saia do contedor.
- `nowrap`. Defecto. Os elementos sobrantes sáense do contedor
- `wrap`. O elementos sobrantes forzan a ampliación automática do contedor.

`flex-flow: direction flow`. Atallo para as dúas anteriores.

`justify-content:` aliña os elementos na dirección do fluxo que se estableceu antes. O posibles valores son:
- `left`, `flex-start`.
- `center`.
- `right`, `flex-end`.
- `space-around`.
- `space-between`.
- `space-event`.

`align-item`. aliña items verticalmente. Pode ter os posibles valores:
- `baseline`.
- `flex-start`.
- `strech`.
- `flex-end`.

`align-content`. Aliña grupos con varial filas verticalmente. Non se usa o anterior.
- `baseline`.
- `flex-start`.
- `strech`.
- `flex-end`.

### Elementos contidos

`flex-basis: width | height`. Forza que se manteña a propiede indicada segundo o flex-direction seleccionado.
`flex-grow`. Establece o coeficiente de crecemento do item en relación aos outros. Por defecto 1.
`flex-shrink`. Establece o coeficiente de encollemento do item en relación aos outros. Por defecto 1.
`flex: grow shrink` . Atalllo para grow shrink.

`order`. Especifica a orde de elmentos (sen modificar o DOM).
`align-self`. Aliña un elemento prescidindo das outras regras.

## Grid

Tecnoloxía que permite definir unha grella de maquetación da web. Actúa dentro dun elemento contedor.

### Contedor
`display`. Activa o modo grid.
- `grid`. Valor por defecto. Aliña os elementos nunha fila de esquerda a dereita.
- `inline-grid`. Tamén aliña os elemntos nunha fila de esquerda a dereira pero fai que o contedor ocupe.

`grid-template-columns:`. Establece o número de columnas da grella. O número de columnas pode establecerse de varios xeitos:
- Con **auto** que iguala o ancho de cada columna: `grid-template-columns: auto auto auto auto auto`.
- Especificando o tamaño para cada columna: `grid-template-columns: 80px auto 20% 300px auto auto`.
- Especificando as diferentes proporcións para cada columna: `grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr`.

`grid-template-rows:`. Establece o número de filas da grella. O número establécese de maneira análoga ás columnas.

`justify-items: start | center | end | auto | strecht`. Aliñamento de elementos horizontalmente.
`align-item: start | center | end | auto | strecht`. Aliñamento de elementos verticalment.

#### Función repeat

A funcion repeat() úsae para repetir unha orde, aplicada ás columnas ou ás filas é moi útil.
`grid-template-columns: repeat(6, auto)`. Crea 6 columnas iguais.
`grid-template-columns: repeat(6, 1fr)`. Crea 6 columnas iguais.

### Elementos contidos

Os elementos contidos aplica varios atributos de diferente tipo.
`grid-column-start`. Determina en que liña da grella comeza unha columna.
`grid-column-end`. Determina en que liña da grella acaba a columna. Admite un valor negativo para contar dede o final.
Atallo
`grid-column: 1/-2`. Atallo que fai que o elemento ocupe da primeira columna ata a penúltima.

`grid-row-start`. Determina en que liña da grella comeza unha fila.
`grid-row-end`. Determina en que liña da grella acaba a fila. Admite un valor negativo para contar dede o final.
Atallo
`grid-row: 1/-2`. Atallo que fai que o elemento ocupe da primeira fila ata a penúltima.

`grid-area: row / col row/col`. Atallo para column e row. Determina a fila e columna iniciais ata a fila e columnas finais.

`justify-self: start | center | auto | strecht`. Autoaliñamento do elemento no eixo horizontal.
`align-self: start | center | auto | strecht`. Autoaliñamenot do elemento no eixo vertical.

### Tracks e aliñamento

Un **track** é o espazon contido entre dúas liñas de grella e pode ser unha columna ou unha fila que ocupa a totalidade da dimensión do contedor. Poden aliñarse no _contedor_:

`justify-content: start | center | end | space-around | space-between | space-evenly`. Justificación no eixo horizontal.
`align-content: start | center | end | space-around | space-between | space-evenly`. Justificación no eixo vertical.

### Grella implícita

A grella implícita créase de maneira automática cando o número de elementos desborda a grella declarada.
`grid-auto-rows:` controla o fluxo de elemento.
`grid-auto-rows:`
`grid-auto-rows:`

`auto-fill`. Enche unha fila con todas as columnas psoibles respectando maxmin();
`auto-fit`. Enche unha fila con todas as columnas psoibles sen respectar maxmin();

### Areas
As **areas** de grid é unha técnica que permite reservar espazos para compoñentes semánticos.
No compoñente contedor defínese a grella:
**_O uso de áreas é ideal para o deseño responsive_**

```
grid-template-areas:    "header header header header header header"
                        "aside main main main main links"
                        "aside main main main main links"
                        "aside main main main main links"
                        "footer footer footer footer footerfooter"
```

Nos compoñentes fillos asígnase a áreas:

```
#header{
    grid-area: header;
}

#aside{
    grid-area: aside;
}

#main{
    grid-area: main;
}

#footer{
    grid-area: footer;
}
```

## Web responsive
A maquetación responsive consiste na capacidade dunha web de adaptarse ao tipo de dispositivo.
Require

- O uso da meta etiqueta viewport
- O uso de media queries
- om uso de unidades relativas.
  width: con unidades relativas.
  min-width e max-width: con unidades absolutas.

## Viewport
Meta etiqueta que lle indica ao navegador que asigne estilos segundo o tamaño do dispositivo.

# Preprocesado SASS
Un preprocesador de css é un set que engade funcinalidades á linguaxw css.
SASS é o processador de css máis popular.

Utiliza ficheiros .sass ou .scss dependendo do estilo. O estilo _sass_ utiliza unha sintaxe baseada na indentación, mentres que a sintaxe _scss_ conserva as chaves.

Para instalar **sass** hai que usar _Nodejs_ ou usar un framework que o teña integrado, como Angular. Cando se usa fóra dun framework hai que compilar os ficheiros.

## Variables

### Declaración

A declaración de variable usa seguinte sintaxe: \$nome: valor:

`$corbase: #afafaf;`

### Uso

úsase no código de xeito directa:
`background: $corbase;`

### Interpolación

Pódese interpola unha variable coa sintaxe:
`#{$variable}`

## Nesting

O _nesting_ é o propiedade que permite aniñar selectores:

```
ul{
    display: flex;
    li{
        display: inline-block;
        list-style: none;
    }
}
```

## Herdanza de estilos

Pódese facer que se extendan os estilos

```
%selector{
    color: red;
}
selector-2{
    @extends %alert;
}

```

## Importación de ficheiros

Pódese modular os ficheiros de css e inportalos mediante a seguinte sintaxe:
@import "path/file.sass"
@use "path/files.sass"

`@import "assets/css/animations.sass";`
`@use "assets/css/animations.sass";`

## mixins

Fragmento de dódigo css reutilizable. Hai librerías . Funciona como unha especie de función

### Declaración

@mixin nome ($propiedade){
    -webkit-transform: $propiedade;
-ms-transform: $propiedade;
    transform: $propieaade;
}

### Uso

.box {
@include nome(rotate(30deg))
}

## Extensión de código

.clase {
... propiedades
}
.clase2{
@extend %clase;
}

## operadores

Agora mesmo están obsoletos. Son operadores aritméticos que permiten realizar: +, -, \*, /, %.

## condicionais

Permiten seleccionar estilos en función de condicions. Pouco útiles a estas alturas.

```
@if $variable == valor {
    ... estilos
} @else {
    ... estilos alternativos
}
```

## Bucles

```
@for $contador from through p {
    li:nth-child(#$contador)
}
```

## funcións

ten función predefinidas

# Preprocesdor LESS

Proprocesador semellante a SASS. Ficheiros .less.

## Variables

Declaración de variables
@variables

## Características

Nesting, mixing,s, operadores, loop

# Anexos

## Ferramenta para o deseño

[Pickpik](https://picpick.app/pt/)

## Propiedades css 
[6 CSS Properties Nobody Is Talking About](https://medium.com/javascript-in-plain-english/6-css-properties-nobody-is-talking-about-e6cab5138d02)

**All**
Prioriza a precedencia  das propiedades referenciadas. Por exemplo, o seguinte código

```
.header{
    color: blue !important;
    font-size: 14px !important; 
}
```
Pode ser reescrito 
```
.header{
  all:initial;
  color: blue;
  font-size: 14px; 
}
```

**Writing-mode**
Modifica a dirección do texto. Aplícase como propiedade a un elemento contendor
```
writing-mode: horizontal-tb;
writing-mode: vertical-rl;
writing-mode: vertical-lr;
```
**Background-clip**
Permite setear un elemento personalizado como fondo.

**user-select**
Habilita/deshabilita a selección do elemento por parte do usuario.

**white-space**
Xunto con `text-overflow` permite controlar o fluxo dun de texto dun elemento.

**border-image**
Permite setear unha imaxe como borde.


## Centrado en CSS
5 técnicas de centrado de elementos
[Centering in CSS](https://web.dev/centering-in-css/)
1. **Content center**
```
.content-center {
  display: grid;
  place-content: center;
  gap: 1ch;
}
```
2. **Gentle Flex**
```
.gentle-flex {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 1ch;
}
```
3. **Autobot**
```
.autobot {
  display: flex;
}
.autobot > * {
  margin: auto;
}
```
4. **Fluffy Center**
```
.fluffy-center {
  padding: 10ch;
}
```
5. **Pop & Plop **
```
.pop_plop {
    position:absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
```

# TIPS

## Ocupar alto completo
O tip consiste en establecer un contedor pai `container` e un contedor fillo `content`.
No contedor pai hai unha declaración min-height con 100vh, display grid e grid-template-rows auto 1fr auto. Isto fai que se estenada por todo o viewport . 
No contedor fillo  hai un min-height a 100%.
```css
.container {
  min-height: 100vh;
  display: grid;
  grid-template-rows: auto 1fr auto;
}
.content {
  background-color: #fefefe;
  min-height: 100%;
}
```

# RECURSOS
[posicionamento css](https://dev.to/lupitacode/guia-completa-y-practica-sobre-posicionamiento-css-fundamentos-17c)