# JAVA

## INSTALACIÓN

### Instalación en Windows

#### Instalación automatizada

A instalación automatizada faise mediante a descarga do instalador da web de Oracle na ligazón [https://oracle.com/technologies/downloads](https://oracle.com/technologies/downloads). Para uso persoal o JDK segue a ser gratuíto. Descárgase o instalador msi e instálase.

Para comprobar que se realizou a instalación correctamente, ábrese unha terminal e execúse o comando `java -version` ou `javac -version`. O primeiro executa o ficheiro jar e o segundo o executable do compilador.

Cando hai instaladas varias versións, hai que configurar as variables de sistema seguindo os pasos da instalación manual.

#### Instalación manual

Descárgase o ficheiro comprimido da web de Oracle ou a versión openJDK [https://jdk.java.net](https://jdk.java.net). O ficheiro descomprímese nun lugar adecuado. Recoméndase en `C:\Program Files\Java`.

A continuación, hai que agregar a versión de Java ás variables de entorno. Debe ter o nome JAVA_HOME e o valor `C:\Program Files\Java`. Ademais, hai que agregar unha nova entrada na variable PATH co valor `C:\Program Files\Java\bin`

#### Desisntalación

A desinstalación estándar realízase desde agregar e quitar programas.

### Instalación en Linux (Ubuntu)

https://www.solvetic.com/tutoriales/article/8641-desinstalar-java-en-linux/
https://www.compuhoy.com/respuesta-rapida-como-desinstalar-java-en-linux/
https://miracomosehace.com/desinstalar-java-linux-eliminar-archivos/
https://www.enmimaquinafunciona.com/pregunta/23856/como-desinstalar-completamente-java
https://www.enmimaquinafunciona.com/pregunta/23341/como-puedo-instalar-java
https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-on-ubuntu-20-04-es
https://www.oracle.com/java/technologies/downloads/#java17
https://novicestuffs.wordpress.com/2017/04/25/how-to-uninstall-java-from-linux/
https://www.makeuseof.com/install-java-ubuntu/
https://linuxhint.com/uninstall-java-ubuntu/
https://fedingo.com/how-to-uninstall-java-in-ubuntu/

#### Instalación manual

#### Desinstalación

Borrar Java do sistema
`sudo apt remove default-jdk default-jre` borrar o JDK e o JRE de sistema.

Obter os paquetes jdk
`dpkg --list | grep jdk`

Borrar os paquetes
`sudo apt remove <nome do paquete>` por exemplo `sudo apt remove jdk-11.0.10`

# INTRODUCIÓN

Para poder xestionar a información é necesario estructurala de algún xeito.
Partimos de que hai _tipos de datos_ _simples_ (booleano, numérico, caráctter) e _complexos_ (matrices ou arrays) que fan referencia a datos máis simples. Unha _estrutura de datos_ é un almacén de datos que determina unha organización de datos (como se almacenas e recuperan) a cercanía dos datos relacionadas a relación entre eles e con unha representación única. Ademáis de almacenar e recuperar os datos, habilitarán máis operacións como cambiar de sito, ou eliminiar. Un _tipo de datos_ é unha estrutura de datos máis unha serie de operacións comúns ligado a unah representación concreta.
Un _tipo abstracto de datos_ abstrae a representanción concreta e a implementacioón. Mantén unhas operacións que indican que se pode facer con un TAD. Para cada TAD hai que ter en conta:

- O perfil e o comportamento das operacións (que se pode facer).
- Estudar o comportamento das operacións (como se definen).
- Escoller a estrutura de datos para a súa representación.
- Implmentar o tipo de datos segundo a estrutura de datos.
- Definiar se a esetrutura é mellorables ou necesita cambios.

Colección
Contenedores
Conxunto
Multicoxunto
Secuencias
Lista
Pila
Cola
Árbores
Xerais
Binarios
Busca binaria

## Capítulo I: estrutura primitiva de Java

Compilación: tipos primitivos (boolean, byte, short, int, long, float, double, char). Operadores básicos: de asignación, aritmétidos, binarios, aritméticos unarios, conversións de tipo.
Intrucións condicionais: operadores de igualdade e relacionais, operadores lóxicos. Instruccións if,while, for, do-while, switch e operador ternario. Instrucións break e continue.
Métodos: métodos sobrecargados. Clases de almacenamento.

## Capítulo II: tipos de referencia

Referencia. Unha variable de referencia é aque que almacena a dirección de memoria onde reside un obxecto. As direccións de memoria son asignadas polo sistema en tempo de execución discrecionalmente segundo os recursos disponibles. Unha variable de referencia pode non almacenar ningunha referencia a un obxecto senón una referencia nula. Java non permite referencias a variables primitivas.
As únicas operacións permitidas con referencias son a asignación (=) e a comparación (== ou !=). Outras operacións tratan co obxecto referenciado: a conversión de tipo, a verificación instance of e o uso do operador de punto para acceder a un campo ou invocar un método do obxecto almacenado.

### Obxectos e referencias

Un obxecto é una instancia de calquera dos tipos non primitivos. As variables de referencia almacenas referencias a obxectos, a direnza das variables primitivas, que almacenan un valor.

### O operador de punto (.)

O operador de punto (.) permite acceder a métodos dun obxecto ou os seus compoentes individuais segundo as restriccións de acceso.

### Declaración de obxectos.

Cando se declara unha variable de referencia non esta a crear ningún obxecito e a referencia é null. Para crea un obxecto úsase o operador new, por exemplo:

```java
Button b = new Button();
```

### O recolector de lixo

En Java, cando un obxecto xa non é referenciado por ningunha variable e, polo tanto, xa non é usado, a posición de memria é reclamada automaticamente polo que pasa a estar disponible.

O operador de asignación (=) funciona de forma diferente dependendo do tipo de variables implicadas. Se son de tipo primitivo, creará candansúa copia do valor, En troca, se son de tipo obxecto almacenas a mesma posición de memoria polo que se se modifica o obxecto a través de unha, a outra accedera tamen ao obxecto modificado. Cando é necesario copiar un obxecto non se una o operador de asignación, senón o método `clone()`.
_Paso por parámetros_
O paso de parámetros realízase mediante a referencia, polo que os cambios realizados dentro dun obxecto serán visibles fóra del.

## O significado do operador de igualdade (==)

Para os tipos primitivos é _true_ se os valores almacenados son idénticos. Para os tipos obxectos será _true_ só se as dúas referencias fan referencia ao mesmo obxecto. O mesmo aplica ao operador de desigualdade (!=). Todos os obxectos poden compararse co operador `equals()` que comprova o seu estado pero nalgúns obxectos compórtase igual que o operador de igualdade e compara referencias.

## 2.3 Cadeas

Tipo de referencia String. Compórtase com un obxecto inmutable, agás nos operadores de concatenanción "+" e "+=". Sempre que hai un obxecto de tipo String e este operador intentará crea un novo obxecto String. Este operador é asociativo á esquerda polos que "a" + 1 + 2 dá "a12" e 1 + 2 + "a" dá "3a". A comparación de cadeas realízase mediante o método `equals()`, que compara o estado dos obxectos referenciados polas variables. O método `compareTo()` realiza unha comparación lexicográfica e devolve un número positivo, cero ou negativo. Outros métodos importantes son `length()`que devolve a súa lonxitude e `charAt()` que devole o carácter nunha posición que se pasa por parámetros. O método `substring()` devolve un novo String a partir do fragmento dentro do inicial. Ademais da conversión mediante o uso de operadores de concatenación, calquera obxecto pode invocar o método `toString()` que devolve a súa representación en forma de string.

## 2.4. Matrices

Un _agregado_ é unha colección de entidades almacendas nunha unidade. Unha matriz é o mecanismo básico para almacenar variables do mesmo tipo e compórtase de xeito moi semellante a un obxecto. Accédese a cada entidade o operador de indexación de matriz. Unha matriz é un obxecto que se inicializa como tal, coa salvedade de que nese momento indícase o número de valores que vai almacenar. Cada un deses valores esta inicializado con referencia nula. Existe varias sintaxe para inicializar un array:

```java
int[] array = new int[10];
int array[] = new int[10];
```

e con lista de inicializadores:

```java
int[] array = {1,2,3,4,5};
```

_Expansión dinámica de array_
É unha téncia que nos permite construir matrices de tamaño arbitrario e facelas máis grandes ou pequenas en tempo de execución. Consiste en gardar unha referencia á matriz orixinsal, modificar a matriz orixinal pertinente, ocpar os datos mediante un bucle e desreferencias a matriz auxiliar:

```java
int[] orixinal = {1,2,3,4,5};
int[] aux = orixinal;
orixinal = new int[10],
for(int i = 0; i< aux.length; i++){
    orixinal[i] = aux[i];
}
aux = null;
```

Esta técia é custosa. O que se fai é multipliar o tamaña por unha constante para evitar estar copiando a matriz continuamente.
_ArrayList_ é un tipo que implementa o método `add()` que incrementea o tamapa en un e engade un novo elemento, na posición adecuada, expandeno a súa capacidade. Unha _matriz multidimensional_ é aquela á que se accede mediante máis dun índice.

## 2.5. Tratamento de excepcións

O bloque try-catch-finally. Excepcións en tempo de execución. Cláusula `throw`e `throws`.

## 2.6. Entrada e saída

Lévase a cabo mediante o paquete _java.io_.
_Operaciósn básicas de fluxos_. para realizar operacións de E/S cara ou desde a terminal, un ficheiro ou internet, o programador crea un fluxo de datos (stream) asociado. Un vez feito isto todos os comandos de E/S dirixiranse cata ese fluxo de datos. Existen 3 fluxos definidos para a terminal: `System.in`, para entrada, `System.out`para a saída e `System.err` para o erro.
O tipo `Scanner` fornece métodos para ler liñas `nextLine`, obxectos `next` ou valores primitivos `nextInt`, etc..., tamen fornecde de métodos verificadores `hasNextLine`, `hasNext`, `hasNextInt`.
_Ficheiros secuenciais_. Para tratar con un ficheiro, creamos un obxecto FileReader. O tratamento é semellante ao fluso de terminal coa salvedade de que hai que fechalo unha vez finalizado para evitar fugas de memoria.

## OBXECTOS E CLASES

_Programación orientada a obxectos_. Paradigma de programación baseado no concepto obxecto. Un obxecto é un tipo que contén una estrutura, un estado e operacións que permiten acceder a ese estado e manipulalo.
Unha clase ten un a _especificacion_ (que fai) pública e unha _implementación_ (como o fai) privada.

## HERDANZA

A herdanza é un principio fundamenta da POO para reutilizar código e está baseada na relación É-UN e forman xerarquías. As relacións TEN-UN forman relacións de composición que non son propias da herdanza. Ha que lembrar que a diferenza enre tipos estáticos e dinámicos e a súa compatibilidade e as referencias polimórficas.
_Interfaz_, campos finnais, estáticos e métodos públicos e abstracatos é unha clase abstracta.

## Estruturas de datos básicas

_Interfaces, iteradores, collección e contenedores_
Interfaces. Vans usar para representar un TAD, van estar anotadas con `@params` e `@return`, `@pre` e `@post`.
Iterador. Interfas para recoror un TAD. Están xerados polo tipo de datos. Poden ser curstos de producir e poden violar a semántica do TAD: Operacións: hai máis elementos, obter o seguinte elemento, e volver ao principio.
colección. colección de elementos sen restricións adicionais: tamaño, valeirar, está valeira, pertence un elemento, obter un elemento.
Contenedor. Colección de elementos sen orde onde se pode negadir e elininar un elemento. Operacións: engadir un elemento, eliminar un elemento e percorrer os elementos.
Conxunto. Contenedor onde cada elemento está só unha vez. Representa o concepto matemático de conxunto finito. Operacións: unión, interxección, diferenza e subconxunto.
Multiconxunto. Contenedor onde cada elemento pode esar varias veces. Operacións: unión, interxección, diferenza, submulticonxunto, multiplicidade de elementos, engdar varios elementos, eliminar varias intancias de elementos.

# Api das coleccións

Esta API propociona soporte ara estruturas de datos reusables. Unha estruturas de datos e unha representación de datos e das operacións permitidas para eses datos. A separación entre _interface_ (o que fai) da súa _implementación_ (como o fai) foram parte do paradigma da POO.

_O patrón Iterator_
O patrón Iterator considera un obxecto que controla a iteración a través dunha colección. Esta clase interadora implementará unha interface con métodos abstractos que se aplicarán nos tipos concretos. Un obxecto iterador controla a súa posición dentro da colección, realiza os movementos e devolver o elemento na posición apuntada.

_Factorías e iteradores baseadas en herdanza_
Un esquema de iteración baseada en herdanza define unha interface iteradora. Os clientes programan de acordo con ela. pra isto usa unha factoria que crea unha nova instancia dunah clase iteradora que cumpre coa interface.
_Contenedores e iteradores_
A interface Collection representa un grupo de obxectos coñecidos como elementos. Usa xenéricos e soporta as seguintes operacións: isEmpty, `size`, `add`, `contains`, `remove`, `clear`, `toArray` e `iterator`.
A interface Iterator representa un obxecto que nos permite iterar a través dunha colección. Contén os métoso `hasNext`, `next`, `remove`. Cada colección de fiene a súa implementación deste interface.
_Algoritmos xenéricos_
A clase Collections ten métodos estáticos que operan sobre obxectos de tipo Collections.
Obxecto función con Comparatos ou Comparable. A clase estática Collections proporciona o método factoría `reverseOrder`. Busca binaria e ordenación.
