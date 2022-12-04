# 1. XENERALIDADES

## 1.1. MÁQUINAS E PROGRAMAS

### 1.1.1. Máquinas programables

Unha _máquina_ é un dispositivo ou instrumento capaz de realizar un certo traballo ou operación.  Unha _máquina programable_ é aquela que é atomática e que se concibe como unha máquina base e unha parte modificable denominada _programa_ que se _executa_ nesa máquina.

### 1.1.2. Concepto de cómputo

_Cómputo_ é a determinación indirecta duna cantidade mediante o cálculo nesa máquina.

### 1.1.3. Concepto de computador

Un _computador_ é unha máquina programable para realizar cálculos, composta por hardware e software. Os computadores actuais son _máquinas de programa almacenado_ e atenden á seguinte estrutura:

memoria
procesador  
datos de entrada -> I/O -> resultados de saída

## 1.2. PROGRAMACIÓN E ENXEÑARÍA DE SOFTWARE.

Para relizar un tratamento da información cómpre:
- Construír o computador (hardware).
- Idear e desenvolver o programa (software).
- Executar dito programa.

### 1.2.1. Programación

A *programación* é o labor de desenvolver programas, habitualmente a pequena escala. As técnicas de programción a gran escala constribúen á enxeñería de software.

### 1.2.2. Obxectivos da programación.

* *Corrección*. O programa debe funcionar como se espera.
* *Claridade*. As súas descricións debe ser claras de cara ás modificacións.
* *Eficiencia*. O programa debe aproveitar os recusos.

## 1.3. LINGUAXES DE PROGRAMACIÓN

Código máquina: moi específico e con forma de código númerico, binario, octal ou hexadecimal. Unha linguaxe de programación é unha representación simbólica dese código e son independentes da máquina.

## 1.4. COMPILADORES E INTÉRPRETES

Existen varias estratexias para executar nunha máquina un programa escrito nunha linguaxe de programación simbólica. Os programas que manipulan estes son _procesadores de linguaxes_.

* *Compilador*. Traduce d eprograma fonte a programa obxecto. Exixe dunha fase de compilación e doutra de execución. Compílanse unha vez e execútase moitas.
* *Intérprete*. Interpreta o código fonte e o executa diretamente nunha única fase.

## 1.5. MODELOS ABSTRACTOS DE CÓMPUTO

Os modelos abstractos de cómputo recollen elementos básicos e formas de comunicación abstracta, presumindo unha notación particular de linguaxe de programación. Tamén se coñecen como modelos de programación.

### 1.5.1. Modelo funcional

Está baseado no emprego de funcións, aplicación que fai corresponder a cada elemento do conxunto partida outro no conxunto de destino.
Estas funcións poden conbinarse unhas con outras para obter cómputos complexos. Neste caso prodúcese a _redución_ cando se reepraza unha función polo seu resultado (base do cálculo-λ)
Usando o símbolo ::= podemos crear unah nova función (reescritura).
Suma(a,b) a + b
Produto(a,b) a * b
Cadrado(a) ::= Produto(a,a)

### 1.5.2. Modelo de fluxo de datos

Un programa corresponde cunha rede de operadores, representando cun cadrado de entradas e saídas. Cada operador agarda por ter valores de entrada calcula o resultadoe o envía á saída. Unha rede deste tipo pode operar de maneira iterativa.

### 1.5.3. Modelo de proba lóxica

Corresponde coa programación declarativa. Decláranse feitos e regras e pregúntase por resultados. Un _feito_ é unha relación entre obxectos concretos mentres que unha _regra_ é una relacion xeral entre obxectos que cumpren certas propiedades. A partir dunha regra pódese inferir outra:`Pai(x,y) :- Fillo(y,x)`.

### 1.5.4. Modelo imperativo

Responde á _arquitectura Von Neumann_, onde o programa aprece com unha lista de instrucións e consiste en ir modificando datos obtendo pasos intermedios até conseguir un resultado final. Incorpora as interaccións e o control de fluxo.

## 1.6. ELEMENTOS DE PROGRAMACIÓN IMPERATIVA

A maioría das linguaxes de programación actuais están baseados na programación imperativa, entre eles temos C e os derivados.

### 1.6.1. Procesador, entorno, accións

* _Procesador_. Axente que entende as ordes do programa e pode executalos.
* _Entorno_. Elementos disponibles para ser usados polo procesador.
* _Accións_. Abstraccións das instrucións.

### 1.6.2. Accións primitivas e compostas

* _Accións primitivas_. Aquelas directamente realizables polo procesador.
* _Accións compostas_. Abstraccións dun gramento dun programa que realiza unha operación definida.

### 1.6.3. Esquemas de accións

Maneira en que varias accións sinxelas se combinan para realizar unha acción composta.

A _programación estruturada_ usa tres esquemas xerais: secuencia, selección (condicións) e iteración (bucles).

## 1.7. EVOLUCIÓN DA PROGRAMACIÓN
### 1.7.1. Evolución comparativa Hw/Sw
### 1.7.2. Necesidade de metodoloxía e boas prácticas

# 2. ELEMENTOS BÁSICOS DE PROGRAMACIÓN
## 2.1. Linguaxe C±

Subconxunto de C e C++ para a aprendizaxe de programación.

## 2.2. NOTACIÓN BNF

Notación formal para a definicion das estruturas sintácticas dunha linguaxe de programación. Está baseada en regras de produción que se combinan para establecer estruturas complexas.
Metasímbolos
::= de definición
| de alternativa
{} de repetición de cero ou máis elementos
[] de opción de cero ou un elemento
() de agrupación

_elemento_non_terminal_
*elemento terminal*

## 2.3. VALORES E TIPOS

Valores constantes e variables. _Tipo_: clase de valores. _Tipo abstracto de datos_: clase de valores posibles e operacións asociadas a el.

## 2.4. REPRESENTACIÓN DE VALORES constantes

_Enteiro_. Secuencia de díxitos, con opción de diciar o signo, formalmente
_díxito_ ::= 0|1|2|3|4|5|6|7|8|9
_secuencia_dixitos_ ::== _dixito_{_dixito_}
_enteiro_ ::= [+|-]_secuencia_dixitos_

*NOTA*: En C os enteiros que comeza por 0 son octais.

_Reais_: Notación decimal ou científica, formalmente:
_escala_ ::= é _Enteiro_
_real_ ::= _enteiro_. [_secuencia de dixitos_][_escala_]

_Carácter_: Entre comillas simples(''). Carácteres de control e secuencias de escape.
_String_: Secuencia de caracteres entre comillas dobres ("").

## 2.5. TIPOS PREDEFINIDOS

Colección de tipos e operacións asociadas

Definidos en C | Definidos en C++
-|-
 | void
 | bool
int | int
float | float
double | double
long double | long double
char | char

_Operacións_
int: suma, resta, multiplicación, división enteira, resto enteiro, cambio de signos.
reais: suma, resta multiplicación, división, cambio de signo.
char:

## 2.6. EXPRESIÓNS ARTIMÉTICAS

Seguen as regras matemáticas. Os valores float e double son prioritarios.

## 2.7. OPERACIÓNS DE ESCRITURA SIMPLES

O procedemento printf. Pertence ao módulo stdio. Entrada de valor con %.
d: decimal enteiro, f: fixedpoint real, e: exponencial real con notación exponencial, g: general xeral, c caracter, s string.

## 2.8. ESTRUTURA DUN PROGRAMA COMPLETO

```C++
/** Programa: nome */  Nota descrición
/* Descrición */

#include <stdio>  // Directivas

int main(){     // programa
  printf("Hi world\n");
}

```

# 3. CONSTANTES E VARIABLES

## 3.1. IDENTIFICADORES

_Identificador_ nom usado para identificar cda elemento dun programa, son alfanuméricos. Hai vaios estilos:
_lowerCamelCase_: C, C++, Java, JavaScript, TypeScript.
_UpperCamlCase_: C#.
_snake_camel_case_: Python.
_CAPITAIS_: constantes.

## 3.2. VOCABULARIO DE C

As _palabras clave_ ou vocabulario dque delimitan as construcións sintácticas de linguaxe de programación. Non se poden usar com identificadores.

## 3.3.  CONSTANTES

Unha _constante_ é un falor fixo que se utiliza nun programa. Poden ser _constantes literais_ ou _constantes simbólicas_

## 3.4. VARIABLES

Unha _variable_, en programación imperativa, valor mutable que se conserva nun espazo de mamora. A declaración pode incluír a súa inicializaión ou non. Se non se inicializa no momento da declaración, posteriormente hai que darlle un valor mediante unha sentenza de asignación. Na asignación de valor debe haber compatibilidade de tipos.

## 3.5. LECTURA SIMPLE

Procedemento scanf(string, variable). Pode ler varios valores separados por espazos en branco.

# 4. METODOLOXÍA DE DESENVOLVEMENTO DE PROGRAMAS

## 4.1. A PROGRAMACIÓN COMO RESOLUCIÓN DE PROBLEMAS

Todo programa é unha resolucioón dun problema. Desenvolver un programa implica expresar unha estratexia para resolver un problema.

## 4.2. DESCOMPOSICIÓN EN SUBPROBLEMAS

O método máis xeral de resolver problemas complexos consiste en divilos en problemas menores. Esta descomposición debe continuar ata que os subproblemas podan ser realizdos de forma diferente.

## 4.3. REFINAMENTOS SUCESIVOS

En En programación estruturadas a técnica de refinamentos sucesivos consiste nesa descomposición sucesiva. A forma en que varias accións simples noutras complexa constitúe un esquema secuencial.

### 4.3.1. Desenvolvemento dun esquema secuencial

- Identificar as accións.
- Idetificar a orde.
O esquema xeral é
Acción composta A -->
  Acción A.1.
  Acción A.2.

## 4.4. ASPECTOS DE ESTILO
### 4.4.1. Encolumnado

identación.

### 4.4.2. Comentarios

Cabeceira de programa: nome, autor, descrición.
Cabeceira de sección.
Comentarioorde. Documenta instrución complexa.
Comentarios a marxe.

### 4.4.3. Elección de nomes

Os nomes debe ser significativos. Constantes e variables substativos e acciósn con verbos.

### 4.4.4. Maiúsculas e minúsculas

Métodos: con maiúsculas.
Variables e constantes: con minúsculas.
Ambas con camel case

### 4.4.5. Constantes con nomes

Usar constantes para valores fixos.

# 5. ESTRUTURAS BÁSICAS DA PROGRAMACIÓN IMPERATIVA
## 5.1. PROGRAMACIÓN ESTRUTURADA

Metodoloxía que se fundamenta na comprensibilidade do código. Está baseada na técnica de refinamentos sucesivos.

### 5.1.1. Representación da estrutura dun programar

Cambio de diagramas de fluxo. As accións represéntase con rectángulos e as condicións con rectángulos. O fluxo de control represéntase con frechas. As estruturas básicas son a _secuencia_, a _selección_ e a _iteración_.

### 5.1.2. Secuencia

Accións que se executan sucesivamente.

### 5.1.3. Selección

Executa unha acción ou outra como resultado dunha condición.

### 5.1.4. Iteración

repetición dunha acción mentres se cumpra unha condición.

### 5.1.5. Estruras anidadas

Aniñamento dunha estrutura dentro doutra.

## 5.2. EXPRESIÓNS CONDICIONAIS

Operacións con dous resultados certo ou falso. Utilízanse expresión condicionais. Todas as linguaxes teñen unha orde avaliación dos operadores.

## 5.3. ESTRUTURAS BÁSICAS ENC

### 5.3.1 Secuencia

### 5.3.2 Sentenza if

```C++
if(condición){
  // sentenzas
} else if (condición) {
  // sentenzas
} else {
  // sentenzas
}
```

### 5.3.3. Sentenza while

```C++
while (condición) {
  // sentenza
}
```

### 5.3.4. Sentenza for
```C++
for (inicio; condición; incremento){
  // sentenzas
}
```

# 6. METODOLOXIA DE DESENVOLVEMENTO DE PROGRAMACION (II)

## 6.1. DESENVOLVMENTO CON ESQUEMAS DE SELECCIÓN E ITERACIÓN

### 6.1.1 Esquemas de selección

Seleccioan una acción entre varias posibles. Normalmente os valores máis comúns setéanse por defecto e logo vaise seleccionando os valores en función das condicións.

### 6.1.2 Esquemas de iteracións

Hai que considerar
- Accións que se van repetir
- Actualizar variables con cada iteración
- Condición de terminación
- Valores iniciais das variables

## 6.2. EXEMPLOS DE PROGRAMAS

### 6.2.1. Imprimir un triángulo
### 6.2.3. Imprimir un triángulo de Floyel

## 6.3. VERIFICACIÓN DE PROGRAMAS

_corrección_: rpoducier resultados de acordo coas especificacións.
_ensaio, test_: executar un programa con datos preparados para obter un reslltados determinado.
_depuración de Luggins_: determinar a causa dun erro e eliminalo.
_demostracón formal_: do funcionamento dun programa usa a notación lóxico-matemática.

### 6.3.1. Corrección parcial e total

1. _Corrección parcial_: se o programa termina o resultado é correcto.
2. _Corrección total_: o anterior, válido para todo dato.
Úsanse precondicións, postcondiións e asercións.

### 6.3.2. Razoamento sobre sentenzas de asignación

Analízanse as condicións inmediatamente anterioes e posteriores.

### 6.3.3. Razoamento sobre esquema de selección

Analízanse as condicións inmediatamente anteriores e, das posteriores, aquelas que se deduzan de cada alterantiva.

### 6.3.4. Razoamento sobre esquema de iteración

Consición inmediantamente anterioes ao buda (invariantes) e as condicións de repetición.

## 6.4. EFICIENCIA DE PROGRAMAS COMPLEXIDADE

### 6.4.1. Medidas de eficiencia

Cantidade de recursos que consume durante a súa execución, memoria/tempo

### 6.4.3. Crecemento asinidótico

Análise da eficiencia dun programa en función do seu comportamento conforme aumenta o tamaño do problema. Notación big O
O(1): aumento constante. ideal óptimo.
O(log n): aumento logarítmico. Moi eficiente.
O(n): aumento lineal. Eficiente.
O(n log n): aumento lineal-logarítmica. Eficiente.
O(n^2): aumento cuadrático. Menos eficiente.
O(n^m): aumento polinómico. Pouco eficiente.
O(2^n): aumento exponencial. Moi pouco eficiente.


# 7. FUNCIÓNS E PROCEDEMENTOS

## 7.1. CONCEPTO DE SUBPROGRAMA

Un _subprograma_ é unha parte de programa que se desenvolver por separado e utilízase mediante un nome simbólico. Debe usarse para fragmentos de código que teñen un certo sentido en si mesmos. Resultan útiles en:
- Programas complexos.
- Operacións análogas.

## 7.2. FUNCIÓNS

Son _subprogramas_ que calculan un valor único a partir doutros dados como argumentos.

### 7.2.1. Definición de funcións

Declaración de interfaz ou sinatura: nome, argumentos e tipo de resultado que devolve.:

`type nameFunction(type arg);`

Oefinición de _corpo_: bloque de código con constantes e variables locais. Ten unha parte declarativa e outra executiva, finalizada cunha ou varias sentenzas de retorno.

### 7.2.2. Uso de funcións.

Para usar unha función invócase co nome e pásaselle os argumentos necesarios.

### 7.2.3. Funcións predefinidas

Son aquelas que forman parte da linguaxe. C e C++ dispoñen de poucas funcións predefinidas.

### 7.2.4. Funcións estándar

Son aquelas que están definidas en librarías estándar: `stdio.h`, `ctype.h` ou `math.h`.

## 7.3. PROCEDEMENTOS

Subprogramas ques realizan unha acción pero non devolver un valor determinado.

### 7.3.1. Definición de procedementos

Declárase igual que unha función pero con palabra reservado `void` para indicar que non devolve nada.

### 7.3.2. Uso de procedementos

Invócase como una función.

### 7.3.3. Procedementos estándar

Aqueles incluídos nas librarías estándar.

##. 7.4. PASO DE ARGUMENTOS

### 7.4.1. Paso de argumentos por valor

Os elementos usados como argumentos non se modifican.

### 7.4.2. Pao de argumentos por referencia

En C++ os argumentos son modificados. Indícase na cabeceira (sinatura) coa anteposición do símbolo & ao nome do argumento formal e debe ser necesariamente variable.

En C úsase punteiros para pasar valores por referencia.

## 7.5. VISIBILIDADE. ESTRUTURA DE BLOQUES

Como norma xeral, nun punto determinado dun programa tense acceso aos elementos definidos con anterioridade, agás que estean definidos dentro de bloques de código. Polo tanto hai elemetos globais e locais.

## 7.6. RECURSIVIDADE DE SUBPROGRAMAS

Un subprograma que se invoca a si mesmo é recursivo. Necesita unha condición de saída.

## 7.7. PROBLEMAS NO USO DE PROGRAMAS

### 7.7.1. Efectos secundarios de variables globais.

_Transferencia referencial_. Propiedade de programas doados de estender. Cando un subprograma usa una variable global esta violando a transferencia referencial e crea efectos secundarios.

### 7.7.2. Redefinición de elementos

Consiste na reutilización de nomes no ámbito global e en local. Debe evitarse sempre.

### 7.7.3. Dupla referencia

A dupla referencia (aliasing) consiste en chamar a mesma variable con dous nomes distintos.

# 8. METODOLOXÍA DE DESENVOLVEMENTO DE PROGRAMAS (III)

## 8.1. OPERACIÓNS ABSTRACTAS

Os subprogramas permiten definicir operacións abstractas. Unha _abstracción_ é unha visión simplificada dunha entidade, considerando só os seus aspectos esenciais. Estas entidades son _Operacións_ que engloban a idea de _acción_ e _función_.

### 8.1.1. Especificación e realización


# APÉNDICE: OPERACIÓNS
## COMPILACIÓN EN C
O comando básico é
`$ gcc file.c`
Parámetros que pode recibir:
`-o` nome do ficheiro
`-wall` mostra erros e avisos
`-pedantic` mostra info habitual
