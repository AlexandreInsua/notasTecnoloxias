# 1.  INTRODUCIÓN A JAVASCRIPT

    1.1. Usando console.log()
    A función console.log() úsase para fins de depuracións. Devolve undefined porque non ten un valor de retorno explícito. Pódese usar para mostrar cadeas de texto ou variable de calquera tipo (tipo primitivos, obxectos JSON, listas, obxectos do DOM, etc...).
    var foo = "bar";
    console.log(foo); // bar
    Os diferentes valores sepáranse con comas e existe a posilidade de usar marcadores de posición.
    var greet = "Hello", who = "World";
    console.log("%s, %s!", greet, who); // Hello, World!

    1.2. Usando a API do DOM
    O DOM (Document Object Model) é a representación da estrutura dos documentos xml. As principais operacións que se poden facer son: - Modificar propiedades: document.getElement.property = value. - Crear elementos: document.createElement, appenChild(element);
    Cando se modifica o DOM programaticamente, o código debe correr despois de crear eses elementos, por iso se pon ao codigo ao final do body.
    Un truco é encapsular estas modificacións un timeout de 0 ms.

    1.3. Usando a window.alert()
    Lanza unha ventana modal. Actualmente en desuso sustituídas por outras librerías.

    1.4. Usando a window.promt()
    Lanza unha ventana modal de introdución de resposta. Tamén en desuso.

    1.5. Udando a window.confirm()
    Lanza unha ventana de confirmación.

    1.6. Usando a API do DOM con elementos gráficos (Canvas, SVG, Imaxes);
    O DOM soporta Canvas, SVG e imaxes.

# 2.  VARIABLES EN JAVASCRIPT
    As vraibles gardan valores.

## 2.1. Definición de variables.
Estándar
    var variable = valor;

Sen inicializar
    var variable;

Agrupada
    var variable1, variable2, variable3; // aforra recursos

Sempre é mellor usar `let`e `const` para a asignación de variables.

usando desestruturación
```javascript
let person = { name: "John", age: 25, };
let { name, age } = person;


```


## 2.2. Usando as variables.

En js o tipado é dinámico (tómase en función do valor da variable) e flexible (pode mudar ao longo do código).
```javascript
let number1 = "1"; // string
let number2 = 3;
number1 = 6;
console.log(number1 / number2); // 2 (number)
```

## 2.3. Tipos de variables
 - Number: que agrupa integer, long, float, double. - NaN: indeterminación matemática. - Boolean: valor booleano. - String: cadea de caracteres ASCII. - Undefined: variable non definida. - Null: valor nulo

## 2.4. Arrays e obxectos
    Un array é un conxunto de variables:

        var array = [var1, var2];

        Un obxecto é un grupo de valores:
        var object = {"property1": "value1", "property2": "value2"}

intercambiar valores de variables
// Shorthand
[personOne, personTwo] = [personTwo, personOne];

# 3.  CONSTRUÍNDO CONSTANTES
    3.1. null
    Úsase null para representar a ausencia intencional dun valor de obxecto ou tipo primitivo. A diferenza de undefined non é unha propiedade do obxecto global.

        console.log(typeof null); // object

    3.2. Función isNaN()
    Úsase para avaliar unha expresión.
    Inicialmente era unha función global: isNaN.
    Devolve true con NaN, strings non convertibles, undefined, funcións, obxectos e arrays.
    Devolve false con numbers, con notacion científica (1.5e2 = 1.5 x 10^2), infinity, true, false, null, "", " ", "42.5", "1.3e3", "Infite", new Date().
    A partir de JS é un método de Number: Number.isNaN para evitar os problemas de conversión.  
     Devolve true non NaN e false no resto dos casos.

    3.3. NaN
    Cando unha operacion ou función matemática non pode devolver un valor especifico, devolve NaN.
    Compróbase coa función isNan() nunca co operador de igualdade.

        console.log(NaN === Nan); // false

    3.4. undefined e null
    Ambos parecen o mesmo, pero son sutilmente diferentes. - undefined é un valor global que representa a ausencia de un valor asignado
    typeof undefined === 'undefined' - null é un obxecto que indicar que lle asignou un "non valor" á variable:
    typeof null == 'object'

        Seteando unha variable como undefined esa variable non existirá. Algúns procesos, como a serialización JSON, pode espir propiedades sen definir. En troca, null indica que esa propiedade fica valeira.

        Avalíase undefined:
        - Cando unha variable se declara pero non se inicializa.
        	let foo;
        	console.log('is undefined?', foo === undefined); // is undefined? true

        - Cando se accede ao valor dunha propiedade que non existe:
        	let foo = { a: 'a' };
        	console.log('is undefined?', foo.b === undefined); // is undefined? true

        - Cando se recupera o retorno dunha funciónque non retorna un valor
        	function foo() { return; }
        	console.log('is undefined?', foo() === undefined); // is undefined? true

        - Cando se omite un argumento na chamada a unha función:
        	function foo(param) {
        		console.log('is undefined?', param === undefined);
        	}
        	foo('a'); // is undefined? false
        	foo(); // is undefined? true

        undefined tamén é unha propiedade do obxecto global window.

    3.5. Infinitos
    1 / 0 //Infinity WTF???
    Infinity é unha propiedade do obxecto global (polo tanto unha variable global) que representa a noción matemática de infinito. Ten unha contraparte en -Infinity. Son referencias a Number.POSITIVE_INFINITY e Number.NEGATIVE_INFINIVE.
    É un valor superior a calquera outro. Obtense nunha división entre cero ou unha operación que rebosa a pilla de memoria. JS non considera erro

    3.6. Constantes
    O constructor de Number ten construídas varias constantes:

        Number.MAX_VALUE; // 1.7976931348623157e+308
        Number.MAX_SAFE_INTEGER; // 9007199254740991
        Number.MIN_VALUE; // 5e-324
        Number.MIN_SAFE_INTEGER; // -9007199254740991
        Number.EPSILON; // 0.0000000000000002220446049250313, o a diferenza mínima entre 2 números.
        Number.POSITIVE_INFINITY; // Infinity
        Number.NEGATIVE_INFINITY; // -Infinity
        Number.NaN; // NaN

    3.7. Operacións que devolve NaN
    Operacións matemáticas con valores distintos de números (strings, arrays, obxectos).
    0 / 0.

    3.8. Funcións matemáticas que devove NaN
    En xeral, cando se lle pasan argumentos que non son números

        Math.floor("a"); // NaN

        Raíces negativas
        Math.sqrt(-1); // Nan, Js non soporta números imaxinarios nin complexos

# 4.  COMENTARIOS
    // monoliña

    /\*

    - multiliña
      \*/

    /\*\*

    - Documentación
      \*/

     <!-- de html (mala práctica)

# 5)  A CONSOLA
    A información mostrada pola consola de depuración / web está dispoñible a través de múltiples métodos do obxecto consola de Js e que se poden consultar a través de console.dir.

    5.1. Medindo o tempo
    console.time() e console.timeEnd() pode usarse para medir o tempo de execución de varias tarefas.

    5.2. Formatando a saída de consola
    Usando tokens (como en C)
    %s string
    %i ou %d integer
    %f float
    %o elemento do DOM
    %0 obxecto
    %c string con estilos css (pode haber varios por conso)

    5.3. Imprimindo na consola de depuración do navegador
    F12
    console.log()

        Outros métodos
        	console.info() mostra un icono de información.
        	console.warn() monstra un icono de aviso e o fondo en amarelo.
        	console.error() mostrar un icono de erro e o fonde vervello.
        	console.timeStamp() mostra o tempo (non estándar) actual e o argumento.
        	console.trace() mostra a pilla de chamadas da función que se chame.

    5.4. Logueando con console.trace()
    Saca a traza dunha función.
    function foo(){
    console.trace('Frase de log');
    }
    A traza tamén pode ser accesible como propiedade de erro.
    var e = new Error('foo');
    console.log(e.stack);

    5.5. Tabulando valores.
    console.table(array, [keys]) pode ser usada para mostrar obxectos e listas en táboa.

    5.6. Contando
    console.count(obj) conta o número de obxectos pasados como argumento.

    5.7. Lipando
    console.clear();

    5.8. Mostrando obxectos e xml dinámico
    console.dir(obj) mostra un obxecto dinámico.
    console.dirxml(obj) mostra unha representación de XML.

    5.9. Depurando con asercións
    console.asert(expresion) valida se unha expresión é verdadeira ou falsa

# 6.  TIPOS DE DATOS EN JS
    6.1. typeof
    Mostra o tipo de datos:

        	typeof "string"						string
        	typeof Date(2019, 06, 20)

        	typeof 42							number
        	typeof 23.4

			typeof 109194432895N				BigInt

        	typeof true							boolean
        	typeof false

        	typeof {}							object
        	typeof []
        	typeof null
        	typeof /aaa/
        	typeof Error()
        	typeof new Date()

        	typeof function() {}				function

        	tipeof variable1 					undefined

    6.2. Encontrando a clase dun obxecto
    A orde intanceof determina o construtor que se usou para crear un obxecto.
    Os valores primitivos non son considerados instancias de clase.
    Todo valor, incluíndo null e undefined, teñen como propiedade o construtor que foi invocado na súa construción.
    Mentres que instanceof captura a subclase, obj.contructor non.

    6.3. Obtendo o tipo de obxecto polo nome do construtor
    Cando se fai typeof de un obxecto obtense object sen especificar a clase.
    Para obter a clase opérase cunha propiedades do prototipo
    Object.protype.toString.call(myObject);
    Pódese obter como valor string, number, boolean, object, function, date, regex, array, null, undefined e error.

# 7  STRINGS
    7.1. Intro e concatenación
    En js os strings poder ser simples '', dobres "" ou template literais ``.
    Pode crearse coa función String(primitive), (primitive).toString() ou String.fromCharCode(ansi_number, ansi_number);
    Tamén se pode crear co operador new pero crea un obxecto con comportamentos diferentes.

        Para concatenear strings úsase o operador + ou a función concat()
        var foo = 'Foo', bar = 'Bar';
        console.log(foo + bar); 		// FooBar
        console.log(foo.concat(bar));	// FooBar

        Pódese concatenar un string cunha variable non string se pode ser casteada
        console.log(foo + 23); 			// Foo23
        var o = {"name": "Alexandre", "surname":"Insua"};
        console.log(foo + o);			// Foo[object Object]

    O string literal adminte a interpolación de variables
    console.log(`Exemplo de interpolación: ${foo}`)

    7.2. String revertida
    Separase cada elemento, invírtese o array, únese con carácter 0;
    string.split('').reverse().join('');

    usando o operador spread >= ES6

    7.3. Comparación de string lexicográfica
    Para comparar dúas string úsase localeCompare, que devolve 0 se son iguais 1 ou -1, tamén se pode usar < ou >
    var a = "alfa", b = "beta";
    a.localeCompare(b);

    7.4. Caracter e índices
    charAt(no); devolve o carácter que ocupa o index
    var string ="Hello, World";
    console.log(string.charAt(4)); //o

    7.5 Carácter de escape \
     var text = 'L\'albero means tree in Italian';
    console.log( text ); \\ "L'albero means tree in Italian"
    Útil para construír tags de html con clases e atributos.
    As comiñas e os apóstrofos poden usarse as entities &quot; &apos;
    Tamén se pode usar unha literal

    7.7. Eliminando espazos
    string.trim() elimina espazos en branco a ambos lados da cadea.

        Algúns navegadores admiten os métodos string.trimStart() e string.trimEnd();
        Métodos non estándar string.trimLeft(), string.trimRight();

    7.8. Partindo un array nun array
    .split(separador) divide unha string e devolve un array
    var s = "un, dous, tres, catro, cinco"
    console.log(s.split(',')); // ["un", " dous", " tres", " catro", " cinco"]
    .join(separador) une un array nun string

    7.9. Unicode
    Todas as strings en JS son unicode

    7.10. Detectando un string
    Para detectar un string úsase typeof.
    Isto non funciona con new String, neste caso hai que usar instanceof.
    Cubrindo ambas as dúas posibilidades:
    typeof value === 'string' || value instanceof String
    Tamén se podes usar a propiedade call
    Object.prototype.toString.call(value);

    7.11. Substrings (slice = fatiar),
    slice() extrae unha substring dados dous índices:
    var s = "Quoesque tandem Catilina abutere ab patientia nostra";
    console.log(s.slice(16, 25)); // Catilina

    7.12. Código de carácter
    charCodeAt() o código dun caracter
    '\*'.charCodeAt(0); // 42
    Algún caracteres unicode son dobres, recupérsanse con
    charPoindAt();

    7.13. Números representados en strings
    JS convirte number a string en base 2 a 32.
    var b = 140;
    console.log(b.toString(2)); // base 2 10001100
    console.log(b.toString(8)); // base 8 214
    console.log(b.toString()); // base 10 140
    console.log(b.toString(16)); // base 16 8c

        No caso de decimais, hai que realizar a conversion por separado.

    7.14. Funcións buscando e remprazando dentro dunha cadea
    string.indexOf('substring') devolve o primeira ocorrencia dunha substring dentro dunha string
    string.lastIndexOf('substring') devolve a última ocorrencia dunha Substrings
    string.includes('substring',index) devolve un boolean se se atopou cadea

        replace(regex | substring, replacement | replaceFunction) devolve unha cadea co remprazo.

        A función de reemprazo pode recibir varios parámetros.

    7.15. Encontrando o índice dunha substring dentro dunha string
    string.indexOf('substring', start) devolve a primeira ocorrencia dunha subcadea dentro dunha cadea a partir dun punto de inicio (opcional).

        	"harr dee harr dee har".indexOf("dee", 10); // 14

    7.16. Maiúsculas e minúscula
    string.toUpperCase(); devolve a cadea en maiúsculas
    'qwerty'.toUpperCase(); // 'QWERTY'

        string.toLowerCase(); devolve a cadea en minúsculas
        'QWERTY'.toLowerCase(); // 'qwerty'

    7.17. Repetindo unha string
    string.repeat(times); devolve a cadea n veces
    "abc".repeat(3); // Returns "abcabcabc"

        Un "truqui" é facelo así:
        new Array(n + 1).join(myString); // Returns "abcabcabc"

# 8.  O TEMPO. DATE
    8.0. Parámetros
    Parámetro Detalles
    value O número de ms desde o 1 de xaneiro de 1970 00:00:00.000 UTC
    dateAsString Data formateada como unha string
    year Ano. NB Debe proporcionarse o mes, ou se interpretará como o número de ms.
    month Mes. NB O úso de valores fóra do intervalo fará que se estenda ao seguinte valor.
    day Día. Opcional, de rango 1-31.
    hour Hora. Opcional, de rango 0-23.
    minute Minuto. Opcional, de rango 0-59.
    second Segundo. Opcional, de rango 0-59.
    millisecond Milisegundo. Opcional, de rango 0-999.

    8.1. Creando un novo obxecto Date()
    Sen argumentos
    Date() crea unha instancia da data actual
    new Date(); // Fri Jun 21 2019 17:55:46 GMT+0200 (hora de verano de Europa central)
    Con un argumento
    Date(value) crea unha instancia sumando os ms á data de referencia
    new Date(2000000000000); // Wed May 18 2033 05:33:20 GMT+0200 (hora de verano de Europa central)

        	Date(dateString) string formatada

        Con varios argumentos
        	Date(i1, i2, i3, i4, i5, i6, i7) Os argumentos son interpretados como year, month (empeza en 0), day, hour, minutes, seconds, milliseconds.
        		Date(2019, 5, 21, 18, 3, 5, 500); //  Fri Jun 21 2019 18:03:05 GMT+0200 (hora de verano de Europa central)

    8.2. Convertindo un Date a un String
    var date = new Date()

        date.toString();  // data e hora con hora local (UTC +2 en verán)
        	"Fri Jun 21 2019 18:03:05 GMT+0200 (hora de verano de Europa central)"

        date.toTimeString(); // hora coa hora local
        	"18:03:05 GMT+0200 (hora de verano de Europa central)"

        date.toDateString(); // data
        	"Fri Jun 21 2019"

        date.toUTCString(); // data e hora Tempo Universal Coordianado (UTC)
        	"Fri, 21 Jun 2019 17:12:46 GMT"
        date.toGTMSString // idem, deprecada
        	"Fri, 21 Jun 2019 17:12:46 GMT"

        date.toISOString(); // data e hora con formato ISO
        	"2019-06-21T17:12:46.160Z"

        date.toLocaleDataString([locales [, options]]); data e hora formatada segundo o local CAMBIA EN FUNCIÓN DA MÁQUINA

        	date.toLocaleString('ko');
        		"2019. 6. 21. 오후 7:12:46"
        	date.toLocaleString('pt');
        		"21/06/2019 19:12:46"

        	var options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
        	date.toLocaleDateString('pt', options);
        			"sexta-feira, 21 de junho de 2019"

    8.3. Creando un Date desde UTC
    Por defecto os obxectos Date creánse como hora local. Isto pode provocar problemas cando interaccionan máquinas que están en distintos fusos horarios.
    Para evitar problemas creánse os Date usando o UTC
    new Date(Date.UTC(2019,5,21));

        Para modificar os obxectos Date tempos os métodos set e setUTC

    8.4. Formatando o date.
    Úsase o método toLocaleDateString(locales [, options]])

        var options = {	weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' , hour:'2-digit', minute: '2-digit', second : '2-digit', timeZoneName: 'short'	}

    8.5. Obtendo os ms desde o tempo de referencia
    Date.now()
    (new Date()).getTime()

    8.6. Obtendo o data e hora actual
    (new Date()).getFullYear();
    (new Date()).getMonth();
    (new Date()).getDate(); // día
    (new Date()).getHours();
    (new Date()).getMinutes();
    (new Date()).getSeconds();
    (new Date()).getMilliseconds();

    8.7. Incrementando valores
    var d = new Date();
    d.setDate(d.getDate() + 10);

        d.toLocaleString('pt', options);
        "sexta-feira, 21 de jun de 2019 20:31:34 Horário de Verão da Europa Central"
        d.setDate(d.getDate() + 7 );
        1561746694334
        d.toLocaleString('pt', options);
        "sexta-feira, 28 de jun de 2019 20:31:34 Horário de Verão da Europa Central"

    8.8. JSON
    date.toJSON(); // convirte a data nun JSON

# 9  COMPARACIÓN DE DATAS
    9.1. Comparación de valores Date
    Os datos Date teñen un valor númerico que é co que se debe usar para compararlos.
    En caso de buscar igualdades, hai que recuperar ese valor con date.valueOf() ou con date.getTime()
    var d1 = new Date();
    var d2 = new Date();
    d1.valueOf() == d2.valueOf(); // false

        Para outras comparacións >, >=, <, <= pódese usar directamente a data
        d1 < d2;

    9.2. Calcualr a diferenza de datos Date
    Tamén se usa .valueOf() ou .getTime(), que obten a difenrenza en ms.

# 10. OPERACIONS DE COMPARACIÓN
    10.1. Igualdade/Desigualdade e tipo de conversión
    En JS, os operadores de igualdade e desigualdade abstractos (== e !=), convirten os seus operandos se non coinciden. Este casteado produce resultados inesperados:

        	"" == 0; // true A
        	0 == "0"; // true A
        	"" == "0"; // false B <- AQUI NON HAI CONVERSIÓN DE TIPOS
        	false == 0; // true
        	false == "0"; // true
        	"" != 0; // false A
        	0 != "0"; // false A
        	"" != "0"; // true B
        	false != 0; // false
        	false != "0"; // false

        Un truco para eliminar este comportamento anómalo é comparar os operandos do mesmo tipo:
        	var test = (a,b) => Number(a) == Number(b);
        	test("", 0); // true;
        	test("0", 0); // true
        	test("", "0"); // true;
        	test("abc", "abc"); // false as operands are not numbers

        Ou para strings:
        	var test = (a,b) => String(a) == String(b);
        	test("", 0); // false;
        	test("0", 0); // true
        	test("", "0"); // false;

        Number("0") e new Number("=") non son o mesmo. O primeiro realizar unha conversión de tipo, o segundo crea un novo obxecto. Como se comparan referencias e non valores, explícase:
        	Number("0") == Number("0"); // true;
        	new Number("0") == new Number("0"); // false

        Finalmente, existe a posibilidade de usar o operador de igualade estricta:
        	"" === 0; // false
        	0 === "0"; // false
        	"" === "0"; // false

    10.2. A propiedade NaN do obxecto global
    NaN é un valor numérico especial que se usa cando aparece un valor non numérico onde se agardaba un numérico (1 _ "string") , ou cando a operación non ten un valor válido (Math.sqrt(-1)).
    As comparacións de igualde ou relacionais, mesmo consigo propio, son false. Isto débese a que NaN representa un sensentido e os sensentidos non se poden operar.
    NaN == NaN // false
    (1 _ "two") === NaN //false
    NaN === 0; // false
    NaN === NaN; // false
    Number.NaN === NaN; // false
    NaN < 0; // false
    NaN > 0; // false
    NaN > 0; // false
    NaN >= NaN; // false
    NaN >= 'two'; // false
    NaN !== 0; // true
    NaN !== NaN; // true

        A partir de ES6 pódese usar o a funcion Number.isNaN(meta), para verificar se ten este valor.

        A funcion global isNaN(meta) devolve true para o NaN puro e calquera outro valor que non poida ser convertido nun número:
        	isNaN(NaN); // true
        	isNaN(0 / 0); // true
        	isNaN('str' - 12); // true
        	isNaN(24); // false
        	isNaN('24'); // false
        	isNaN(Infinity); // false
        	isNaN('str'); // true
        	isNaN(undefined); // true
        	isNaN({}); // true

    10.3. Operacións con booleanos
    O operación de conxunción (&&) e o de disxunción (||) empregan curtocircuitos para evitar traballo extra:
    En x && y, y non se avaliará se x é false,
    En x || y, y non se avaliara se y é true

        	true && true // true
        	true && false // false
        	false && true // false
        	false && false // false

        	true || true // true
        	true || false // true
        	false || true // true
        	false || false // false

        Usar o curtocircuito para evitar erros. Se o obxecto ten a propiedade executará a sentenza, pero se on a ten, comprobrá se hai obxecto. Invertir os elementos fai a expresión máis segura, pero máis lenta.
        	var obj;
        	if (obj.property && obj !== undefined) {

        	}
        Usar o curtocircuito para fornecer valores por defecto (pódese encadear sentenzas).
        	var port = PROCESS.ENV.PORT || port ||32321;

        Usar o curtocircuito para avaliar unha función de callback opcional.
        	function myMethod(cb) {
        		// This can be simplified
        		if (cb) {
        			cb();
        		}
        		// To this
        		cb && cb();
        	}

    10.4. Null e Undefined
    As diferenzas entre null e undefined
    undefined representa a ausencia accidental de valor de valor, como cando se chama a unha propiedade dun obxecto que non existe ou que aínda non foi inicializada. undefined é unha propiedade do obxecto global.
    null representa a ausencia intencionada dun valor.
    Devolve true na igualdade abstracta pero false na igualdade estrita
    null == undefined // true
    null === undefined // false

        Semellanzas entre null e undefined
        Ambos son falsables:
        	if (null) console.log("won't be logged");
        	if (undefined) console.log("won't be logged");

        Ambos non equivalen a false
        	false == undefined // false
        	false == null // false
        	false === undefined // false
        	false === null // false

    10.5. Igualdade abstracta (==)
    O operando de igualdade abstracta compara valores despois de convertirse os elementos a un tipo común.

        Examplos:
        1 == 1; // true
        1 == true; // true (operando convertido a number: true => 1)
        1 == '1'; // true (operando convertido a number: '1' => 1 )
        1 == '1.00'; // true
        1 == '1.00000000001'; // false
        1 == '1.00000000000000001'; // true (true debido a precisión perdida)
        null == undefined; // true (spec #2)
        1 == 2; // false
        0 == false; // true
        0 == undefined; // false
        0 == ""; // true

    10.6. Operadores lóxicos con booleano
    And. Devolverá true se ambos elementos son verdadeiros, no resto dos casos devolve true
    true && true // true
    Or. Devolverá true se algún dos elementos é true.
    false && false // false
    Not. Devolve falso se o elemento é true e true se o elemento é false;

    10.7. Conversión autatica de tipo
    Hai que ter en conta que os number pode ser convertidos a string ou a NaN porque JS ten ten un tipado feble e dinámico.

        var x = "Hello"; // typeof x string
        x = 5; // cambia hanges typeof x a number

        Cando se fai operacións matemáticas, JavaScript pode convertir numbers a strings:
        var x = 5 + 7; // x.valueOf() is 12, typeof x is a number
        var x = 5 + "7"; // x.valueOf() is 57, typeof x is a string
        var x = "5" + 7; // x.valueOf() is 57, typeof x is a string
        var x = 5 - 7; // x.valueOf() is -2, typeof x is a number
        var x = 5 - "7"; // x.valueOf() is -2, typeof x is a number
        var x = "5" - 7; // x.valueOf() is -2, typeof x is a number
        var x = 5 - "x"; // x.valueOf() is NaN, typeof x is a number

        Restar unha cadea de outra xera NaN (Not a Number):
        "Hello" - "Dolly" // returns NaN

    10.8. Operadores lóxicos con valores non booleanos (casteado a boolean)
    O operador lóxico OR (||), os elementos de esquerda a dereita, avalía o primeiro, se é falso, avalía o segundo.
    var a = 'hello' || ''; // a = 'hello'
    var b = '' || []; // b = []
    var c = '' || undefined; // c = undefined
    var d = 1 || 5; // d = 1
    var e = 0 || {}; // e = {}
    var f = 0 || '' || 5; // f = 5
    var g = '' || 'yay' || 'boo'; // g = 'yay'

        O operador lóxico AND (&&), se o primeiro é falso, non avalalía o segundo:
        	var a = 'hello' && ''; // a = ''
        	var b = '' && []; // b = ''
        	var c = undefined && 0; // c = undefined
        	var d = 1 && 5; // d = 5
        	var e = 0 && {}; // e = 0
        	var f = 'hi' && [] && 'done'; // f = 'done'
        	var g = 'bye' && undefined && 'adios'; // g = undefined

        Isto pode usarse para setear valores por defecto como argumento de función:
        	var foo = function(val) {
        		// if val evaluates to falsey, 'default' will be returned instead.
        	return val || 'default';
        	}

        	console.log( foo('burger') ); // burger
        	console.log( foo(100) ); // 100
        	console.log( foo([]) ); // []
        	console.log( foo(0) ); // default
        	console.log( foo(undefined) ); // default

    10.9. Array
    Cando se exectua [].toString(), retórnase "", que se avalía como numericamente 0.

    10.10. Operacións de comparación de igualdade.
    JS ten catro operacións de igualdade diferentes.
    Compárase typo e valor, onde o valor dun obxecto é a súa referencia.

        Mesmo valor estrito
        - Object.id() ES6 mesmo tipo e valor: Reflexivo, simétrico e transitivo.
        	Object.is(1, 1); // true
        	Object.is(+0, -0); // false
        	Object.is(NaN, NaN); // true
        	Object.is(true, "true"); // false
        	Object.is(false, 0); // false
        	Object.is(null, undefined); // false
        	Object.is(1, "1"); // false
        	Object.is([], []); // false

        Mesmo valor cero
        - Array.prototype.includes() ES7: Reflexivo, simétrico e transitivo.
        	[1].includes(1); // true
        	[+0].includes(-0); // true
        	[NaN].includes(NaN); // true
        	[true].includes("true"); // false
        	[false].includes(0); // false
        	[1].includes("1"); // false
        	[null].includes(undefined); // false
        	[[]].includes([]); // false

        Comparación de igualdade estrita
        - Operador === e !==: Simétrico e transitivo. Con NaN non é reflexivo
        	1 === 1; // true
        	+0 === -0; // true
        	NaN === NaN; // false
        	true === "true"; // false
        	false === 0; // false
        	1 === "1"; // false
        	null === undefined; // false
        	[] === []; // false

        Comparación de igualdade abstracta
        - Operador == e != : cando compara valores do mesmo tipo compórtase como a igualdade estricta, pero cando son diferentes realizar unha conversión de tipo:
        	undefined e null consíderanse do mesmo tipo
        	number == string, convírtese a string
        	boolean == algo, convírese o boleano a number
        	object == number | string | symbol, o object convírtese ao primitivo.
        		1 == 1; // true
        		+0 == -0; // true
        		NaN == NaN; // false
        		true == "true"; // false
        		false == 0; // true
        		1 == "1"; // true
        		null == undefined; // true
        		[] == []; // false

    10.11. Operadores relacionais (<, <=, >, >=)
    Cando os operandos son números, compáranse con normalidade
    1 < 2 // true
    2 <= 2 // true
    3 >= 5 // false
    true < false // false (implicitly converted to numbers, 1 > 0)

        Cando son string, compáranse lexicograficamente (segundo a orde do alfabeto)
        		'a' < 'b' // true
        		'1' < '2' // true
        		'100' > '12' // false ('100' is less than '12' lexicographically!)

        Cando un operando é string e o outro number, o string convírtese antes da comparación. Se o string é non numérico retorna NaN e a comparación é sempre falsa.
        		'1' < 2 // true
        		'3' > 2 // true
        		1 < 'abc' // false
        		1 > 'abc' // false

    10.12. Inegualdade (!=, !==)
    Devolve true se os operandos non son iguais. Tamén realiza unha conversión de tipo.
    No caso de obxectos, compara referencias.


    10.13 Lista de comparadores
    	== igualdade
    	=== igualdade estrita
    	!= desigualdade
    	!== desigualdade estrita
    	> maior que
    	< menor que
    	>= maior ou igual que
    	<= menor ou igual que

    10.14. Agrupando varias declaracións lóxicas
    	Pódese agrupar varias delcaracións lóxicas con parénteses.
    		if ((age >= 18 && height >= 5.11) || (status === 'royalty' && hasInvitation)) {
    			console.log('You can enter our club');
    		}

    10.15. Campos de bit para comparar estados
    	Un campo de bits é unha variable que contén varios estados booleanos como bits individuais. Un bit encendido representaría verdadeiro e desactivado sería falso. No pasado, os campos de bits utilizáronse de xeito rutinario porque aforraban memoria e reducían a carga de procesamento.
    	Aínda que a necesidade de usar o campo de bits xa non é tan importante, ofrecen algúns beneficios que poden simplificar moitos procesos tarefas.
    	Por exemplo, entrada de usuario. Ao obter a entrada das teclas de dirección dun teclado  cara arriba, abaixo, esquerda e dereita pode codificar as varias teclas nunha única 	variable con cada dirección asignada a un bit.

    	Exemplo de ler o teclado mediante un campo de bits
    		var bitField = 0; // the value to hold the bits
    		const KEY_BITS = [4,1,8,2]; // left up right down
    		const KEY_MASKS = [0b1011,0b1110,0b0111,0b1101]; // left up right down
    		window.onkeydown = window.onkeyup = function (e) {
    			if(e.keyCode >= 37 && e.keyCode <41){
    				if(e.type === "keydown"){
    					bitField |= KEY_BITS[e.keyCode - 37];
    				}else{
    					bitField &= KEY_MASKS[e.keyCode - 37];
    				}
    			}
    		}

    	Exemplo de ler como un array
    			var directionState = [false,false,false,false];
    			window.onkeydown = window.onkeyup = function (e) {
    				if(e.keyCode >= 37 && e.keyCode <41){
    					directionState[e.keyCode - 37] = e.type === "keydown";
    				}
    			}

    	Para activar un bit, utilice bitwise ou o operador | o valor correspondente ao bit. Entón, se quere configurar o segundo bit | = 0b10 acenderá. Se queres desactivar un bit, use bitwise e &
    	Usando 4 bits e alternando o segundo bit do campo de bits & = 0b1101;

    	Pódese dicir que o exemplo anterior parece moito máis complexo que asignar os distintos estados clave a unha matriz. Si, iso é un pouco máis complexo de configurar, pero a vantaxe vén ao interrogar o estado

# 11. CONDICIÓNS
    	As expresións condicionais, que inclúen palabras clave como if e else  cousa, proporcionan programas de JavaScript coa capacidade de realizar diferentes accións dependendo dunha condición booleana: verdadeira ou falsa. Esta sección cobre o uso de JavaScript de condicionais, lóxica booleana e declaracións ternárias.

## 11.1. Operadores ternario

Pódese usar para reducir as operacións de `if/else`. Isto vén ben para devolver un valor rápidamente (é dicir, para asignalo a outra variable). Por exemplo:

```javascript
let animal = 'kitty';
let result = (animal === 'kitty') ? 'bonito': 'normal';
```
Neste caso, o resultado obtén o valor "bonito", porque o valor do animal é "kitty". Se o animal tiña un valor diferente, o resultado obtería o valor "normal". Compare isto como sería o código coas condicións `if/else`.

```javascript
let animal = 'kitty';
let result = '';
if (animal === 'kitty') {
	result = 'bonito';
} else {
	result = 'nomral';
}
```

As condicións if ou else poden ter varias operacións. Neste caso, o operador devolve o resultado da última expresión.

```javascript
let a = 0;
let str = 'not a';
let b = '';
b = a === 0 ? (a = 1, str + = 'test'): (a = 2);
```
Como a era igual a 0, convértese en 1 e str convértese en "not a test". A operación que implicaba str era a última, polo que b recibe o resultado da operación, que é o valor que contén str, é dicir, 'not a test'.

Os operadores ternarios sempre esperan a condición do else,  se non, obterá un erro de sintaxe. Como ñapa  podería devolver un cero na segunda parte do operador ternario:

```javascript
let a = 1;
a === 1 ? alert ('Hey, it\'s 1!'): 0;
```

Como ves, se (a === 1) alert ('Hey, it's 1!'); faría o mesmo. Sería un char máis longo, xa que non necesita unha condición obrigatoria. Se un else  condición estaba implicado, o método ternario sería moito máis limpo.
```javascript
a === 1? alert ('Hey, é 1!'): alert ('Estraño, que podería ser?');
if (a === 1) alert ('Hey, é 1!') else ('Raro, que podería ser?');
```

Os ternarios poden ser aniñados para encapsular lóxica adicional. Por exemplo
```javascript
foo? bar? 1: 2: 3
	// Para ser claro, isto é avaliado de esquerda a dereita
	// e pode expresarse máis explicitamente como:
foo? (bar? 1: 2): 3
```
Isto é o mesmo que o seguinte:
```javascript
if (foo) {
	if (barra) {
			1
		} else {
			2
		}
	} else {
		3
}
```
Estilísticamente isto só debe usarse con nomes de variables curtas, xa que os ternarios de varias liñas poden diminuír drasticamente a lexibilidade.

As únicas instrucións que non se poden usar nos ternarios son instrucións de control. Por exemplo, non pode usar return o break con ternarios. A seguinte expresión non será válida.
```javascript
var animal = 'kitty';
for (var i = 0; i <5; ++ i) {
(animal === 'kitty')? break: console.log (i);
}
```

Para as declaracións de return, o seguinte tamén sería inválido:
```javascript
var animal = 'kitty';
(animal === 'kitty') ? return 'miau': return o "fffffff!";
```

Para facer correctamente o anterior, devolverás o ternario do seguinte xeito:
```javascript
var animal = 'kitty';
return (animal === 'miau') ? "miau": "fffffff!";
```

## 11.2. Sentenza switch
    	As sentenzas de switch comparan o valor dunha expresión con 1 ou máis valores e executa diferentes seccións de código baseado nesa comparación.
    		var value = 1;
    		switch (value) {
    			case 1:
    				console.log('I will always run');
    				break;
    			case 2:
    				console.log('I will never run');
    				break;
    		}

    	A instrución break "rompe" a instrución switch e garante que non se executa máis código dentro da instrución switch. Así se definen as seccións e permiten ao usuario facer casos de "caída".
    	Aviso: a falta de break ou declaración return para cada caso significa que o programa seguirá avaliando o seguinte caso, aínda que os criterios do caso non estean satisfeitos!
    		switch (value) {
    			case 1:
    				console.log('I will only run if value === 1');
    				// Here, the code "falls through" and will run the code under case 2
    			case 2:
    				console.log('I will run if value === 1 or value === 2');
    			break;
    			case 3:
    				console.log('I will only run if value === 3');
    				break;
    		}


    	O último caso é o caso predeterminado. Este funcionará se non hai coincidencia cos casos descritos.
    		var animal = 'Lion';
    			switch (animal) {
    				case 'Dog':
    					console.log('I will not run since animal !== "Dog"');
    					break;
    				case 'Cat':
    					console.log('I will not run since animal !== "Cat"');
    					break;
    				default:
    					console.log('I will run since animal does not match any other case');
    			}

    	Debe notarse que unha expresión de caso pode ser calquera tipo de expresión. Isto significa que pode usar comparacións, chamadas de funcións, etc. como valores de caso.


    	Criterios de inclusión múltiple para casos

    	Dado que os casos "caen" sen unha declaración de retorno ou retorno, pode usalo para crear múltiples criterios inclusivos:

    11.3. if / else if / else
    	Na súa forma máis sinxela, pode usarse unha condición if así:
    		var i = 0;
    		if (i < 1) {
    			console.log("i is smaller than 1");
    		}

    	Avalíase a condición i <1 e se se avalía  verdadeira execútase o bloque que segue. Se se avalía a false, omítese o bloque.

    	Unha condición if pódese  expandir cun outro bloque. A condición compróbase unha vez como antes, e se se avalía a falso executarase un bloque secundario (que se omitiría se a condición fose certa). Un exemplo:
    		if (i < 1) {
    			console.log("i is smaller than 1");
    		} else {
    			console.log("i was not smaller than 1");
    		}


    	Supoñendo que o outro bloque non contén máis que outro bloque (con opcionalmente outro bloque) así:
    		if (i < 1) {
    			console.log("i is smaller than 1");
    		} else {
    			if (i < 2) {
    				console.log("i is smaller than 2");
    			} else {
    				console.log("none of the previous conditions was true");
    			}
    		}

    	Despois, hai tamén un xeito diferente de escribir isto que reduce a anidación:
    		if (i < 1) {
    			console.log("i is smaller than 1");
    		} else if (i < 2) {
    			console.log("i is smaller than 2");
    		} else {
    			console.log("none of the previous conditions was true");
    		}

    	Algunhas notas importantes sobre os exemplos anteriores:
    	- Se calquera das condicións é avaliada como verdadeiras, non se avaliará ningunha outra condición na cadea de bloques e non se executarán todos os bloques correspondentes (incluído o outro bloque).
    	- O número de partes else if  é practicamente ilimitado. O último exemplo anterior só contén un, pero pode ter tantos como desexa.
    	- A condición dentro dunha instrución if pode ser calquera cousa que se poida obrigar a un valor booleano, vexa o tema sobre lóxica booleana para máis detalles;
    	- A escaleira if-else-if sae no primeiro éxito. É dicir, no exemplo anterior, se o valor de i é 0.5 entón execútase a primeira rama. Se as condicións se solapan, os primeiros criterios que se producen no fluxo de execución executaranse. A condición else, que tamén pode ser verdadeira, é ignorada.
    	Se só tes unha declaración, as chaves son tecnicamente opcionais, por exemplo.

    11.4. Estratexia
    	Un patrón de estratexia pode usarse en JavaScript en moitos casos para substituír unha instrución switch. É especialmente útil cando o número de condicións é dinámico ou moi grande. Permite que o código de cada condición sexa independente e comprobable por separado.
    	O obxecto de estratexia é un obxecto sinxelo con múltiples funcións, que representa cada condición separada. Exemplo:
    		const AnimalSays = {
    			dog () {
    				return 'woof';
    			},
    			cat () {
    				return 'meow';
    			},
    			lion () {
    				return 'roar';
    			},
    			// ... other animals
    			default () {
    				return 'moo';
    			}
    		};

    	O obxecto anterior pode usarse do seguinte xeito
    		function makeAnimalSpeak (animal) {
    			// Match the animal by type
    			const speak = AnimalSays[animal] || AnimalSays.default;
    			console.log(animal + ' says ' + speak());
    		}

    	Resultados:
    		makeAnimalSpeak('dog') // => 'dog says woof'
    		makeAnimalSpeak('cat') // => 'cat says meow'
    		makeAnimalSpeak('lion') // => 'lion says roar'
    		makeAnimalSpeak('snake') // => 'snake says moo'

    	No último caso, a función por defecto captura calquera animal non definido.

    11.5. Usando os curtocircuitos || e &&
    	Pódese usar as propiedades destes operadores para usalos como condionais:
    		var x = 10
    		x == 10 && alert("x is 10")
    		x == 10 || alert("x is not 10")

# 12. ARRAYS
## 12.1. Convertindo obxectos semellantes a arrays en arrays puros
    Que son os obxectos tipo array?
    JavaScript ten "Obxectos de tipo array", que son representacións de obxectos de matrices cunha propiedade de lonxitude. Por exemplo:
    var realArray = ['a', 'b', 'c'];
    var arrayLike = {
    0: 'a',
    1: 'b',
    2: 'c',
    length: 3
    };
    Os exemplos comúns de obxectos de tipo array son os argumentos obxecto en funcións e HTMLCollection ou NodeList obxectos devoltos de métodos como document.getElementsByTagName ou document.querySelectorAll.

        Porén, unha diferenza chave entre Arrays e Arrays-like Objects (AlO) é que os obxectos de tipo Array herdan de Object.prototype en vez de Array.prototype. Isto significa que os obxectos de tipo Array non poden acceder a métodos de prototipos comúns de Array como forEach(), push (), map(), filter() e slice():
        	var parent = document.getElementById('myDropdown');
        	var desiredOption = parent.querySelector('option[value="desired"]');
        	var domList = parent.children;
        	domList.indexOf(desiredOption); // Error! indexOf is not defined.
        	domList.forEach(function() {
        		arguments.map(/* Stuff here */) // Error! map is not defined.
        	}); // Error! forEach is not defined.

        	function func() {
        		console.log(arguments);
        	}

        	func(1, 2, 3); // → [1, 2, 3]

        Convertindo AlOs en Arrays en ES6
        	1. Array.from:
        		const arrayLike = {
        			0: 'Value 0',
        			1: 'Value 1',
        			length: 2
        		};
        		arrayLike.forEach(value => {/* Do something */}); // Errors
        		const realArray = Array.from(arrayLike);
        		realArray.forEach(value => {/* Do something */}); // Works

        	2. for ...of;
        		var realArray = [];
        		for(const element of arrayLike) {
        			realArray.append(element);
        		}

        	3. Operador Spread
        		[... arrayLike]

        	4. Object.values
        		var realArray = Object.values(arrayLike);

        	5. Object.keys:
        		var realArray = Object
        			.keys(arrayLike)
        			.map((key) => arrayLike[key]);

        Convertindo AlOs en Arrays en ES5
        	1. Use Array.prototype.slice así:
        		var arrayLike = {
        			0: 'Value 0',
        			1: 'Value 1',
        			length: 2
        		};
        		var realArray = Array.prototype.slice.call(arrayLike);
        		realArray = [].slice.call(arrayLike); // Shorter version
        		realArray.indexOf('Value 1'); // Wow! this works

        	2. Tamén pode usar Function.prototype.call para chamar directamente os métodos Array.prototype nos obxectos tipo Array, sen convertelos:
        		var domList = document.querySelectorAll('#myDropdown option');
        		domList.forEach(function() {
        			// Do stuff
        		}); // Error! forEach is not defined.
        		Array.prototype.forEach.call(domList, function() {
        			// Do stuff
        		}); // Wow! this works

        	3. Tamén pode usar [] .method.bind (arrayLikeObject) para pedir prestados os métodos da matriz e devolvelos ao seu obxecto:
        		var arrayLike = {
        			0: 'Value 0',
        			1: 'Value 1',
        			length: 2
        		};

        		arrayLike.forEach(function() {
        			// Do stuff
        		}); // Error! forEach is not defined.

        		[].forEach.bind(arrayLike)(function(val){
        			// Do stuff with val
        		}); // Wow! this works

        Modifying Items During Conversion
        	En ES6, mentres usa Array.from, podemos especificar unha función de mapa que devolve un valor mapeado para a nova matriz que se crea.
        	Array.from(domList, element => element.tagName); // Creates an array of tagName's

##  12.2. Redución valores (versión ≥ 5.1)
    O método reduce () aplica unha función contra un acumulador e cada valor da matriz (de esquerda a dereita) a redúcese a un único valor.

        Sumario da matriz
        Este método pódese usar para condensar todos os valores dunha matriz nun único valor:
        	var a = [1, 2, 3, 4].reduce(function(a, b) {
        		return a + b;
        	});
        	console.log(a) // → 10 , vai sumando cada elemento co seguinte

        Pódese pasar o segundo parámetro opcional para reducir (). O seu valor usarase como o primeiro argumento (especificado como a) para a primeira chamada á devolución de chamada (especificada como function(a, b)).
        	var a = [2].reduce(function (a, b) {
        		console.log (a, b); // impresións: 1 2
        		return  a + b;
        	}, 1);
        	console.log(a) // → 3


    	Aplanar a matriz de obxectos (Versión ≥ 5.1)
    	O seguinte exemplo mostra como aplanar unha matriz de obxectos nun único obxecto.
    		var array = [{{
    			clave: 'un',
    			valor: 1
    		},
    		{
    			clave: 'dous',
    			valor: 2
    		},
    		{
    			clave: 'tres',
    			valor: 3
    		}];

    	Versión ≤ 5.1
    		array.reduce(function(obj, current) {
    		obj [current.key] = current.value;
    			return obj;
    		}, {});


    	Versión ≥ 6
    		array.reduce (obj, current) => Object.assign (obj, {
    			[current.key]: current.value
    		}), {});

    	Versión ≥ 7
    			array.reduce((obj, current) => ({... obj, [current.key]: current.value}), {});

    	Teña en conta que as propiedades Rest/Spread non están na lista de propostas finalizadas de ES2016. Non é compatible con ES2016. Pero podemos usar o complemento de babel babel-plugin-transform-object-rest-spread para soportalo.


    	Todos os exemplos anteriores para Flatten Array resultan en:
    		{
    			un: 1,
    			dous: 2,
    			tres: 3
    		}

    	Versión ≥ 5.1
    	Mapa usando Reduce
    		Como outro exemplo de usar o parámetro de valor inicial, considere a tarefa de chamar a unha función nunha matriz de elementos, devolver os resultados nunha nova matriz. Dado que as matrices son valores comúns e a concatenación de listas é unha función ordinaria, podemos usar reducimos para acumular unha lista, como o seguinte exemplo demostra:
    			function map(list, fn) {
    				return list.reduce(function(newList, item) {
    					return  newList.concat (fn (item));
    				}, []);
    			}
    			// Uso:
    			map([1, 2, 3], function (n) {return n * n;});
    			// → [1, 4, 9]

    		Teña en conta que isto é só para ilustracións (do parámetro de valor inicial), use o mapa nativo para traballar con lista transformacións (vexa Mapping de valores para os detalles).

    	Versión ≥ 5.1
    	Busca un valor mínimo ou máximo

    	Podemos usar o acumulador tamén para manter un rexistro dun elemento de matriz. Aquí tes un exemplo para encontrar o o valor mínimo:
    		var arr = [4, 2, 1, -10, 9]
    		arr.reduce (función (a, b) {
    			return a < b ? a: b
    		}, Infinity);
    		// → -10

    	Versión ≥ 6
    	Atopa valores únicos
    	Aquí hai un exemplo que usa reducir para devolver os números únicos a unha matriz. Pasa unha matriz baleira como segundo argumento e referenciado anteriormente.
    		var arr = [1, 2, 1, 5, 9, 5];
    		arr.reduce ((prev, number) =>
    			if (prev.indexOf (number) === -1) {
    				prev.push (número);
    				}
    			return prev.
    		}, []);
    		// → [1, 2, 5, 9]

##  12.3. Mapping de valores
    	Moitas veces é necesario xerar unha nova matriz baseada nos valores dunha matriz existente.
    	Por exemplo, para xerar unha matriz de lonxitudes de cadeas a partir dunha matriz de cadeas:

    	Version ≥ 5.1
    		['one', 'two', 'three', 'four'].map(function(value, index, arr) {
    			return value.length;
    		}); // → [3, 3, 5, 4]

    	Version ≥ 6
    	['one', 'two', 'three', 'four'].map(value => value.length); // → [3, 3, 5, 4]

    	Neste exemplo, fornécese unha función anónima á función map() e a función de mapa chamarase por cada elemento na matriz, proporcionando os seguintes parámetros, nesta orde:
    		- O elemento en si
    		- O índice do elemento (0, 1 ...)
    		- Toda a matriz
    	Adicionalmente, map () proporciona un segundo parámetro opcional para establecer o valor  de this na función map. Dependendo do ambiente de execución, o valor predeterminado de this pode variar:
    		- Nun navegador, o valor predeterminado desta sempre é o obxecto window:
    			['one', 'two'].map(function(value, index, arr) {
    				console.log(this); // window (the default value in browsers)
    				return value.length;
    			});

    	Pode cambialo a calquera obxecto personalizado como este:
    		['one', 'two'].map(function(value, index, arr) {
    			console.log(this); // Object { documentation: "randomObject" }
    			return value.length;
    		}, {
    			documentation: 'randomObject'
    		});

## 12.4. Filtrando arrays de obxectos
    	O método filter () acepta unha función de filtro e devolve unha nova matriz que contén só os elementos da matriz orixinal que pasan o filtro a proba proporcionada.
    			// Suppose we want to get all odd number in an array:
    		var numbers = [5, 32, 43, 4];

    		Version ≥ 5.1
    		var odd = numbers.filter(function(n) {
    			return n % 2 !== 0;
    		});

    		Version ≥ 6
    		let odd = numbers.filter(n => n % 2 !== 0); // can be shortened to (n => n % 2)

    		odd contería a seguinte matriz: [5, 43].

    	Tamén funciona nunha matriz de obxectos:
    		var people = [{
    				id: 1,
    				name: "John",
    				age: 28
    			}, {
    				id: 2,
    				name: "Jane",
    				age: 31
    			}, {
    				id: 3,
    				name: "Peter",
    				age: 55
    		}];

    		Version ≥ 5.1
    		var young = people.filter(function(person) {
    			return person.age < 35;
    		});

    		Version ≥ 6
    		let young = people.filter(person => person.age < 35);

    	young contería a seguinte matriz:
    		[{
    			id: 1,
    			name: "John",
    			age: 28
    		}, {
    			id: 2,
    			name: "Jane",
    			age: 31
    		}]

    	Pode buscar en toda a matriz un valor como este:
    		var young = people.filter((obj) => {
    			var flag = false;
    			Object.values(obj).forEach((val) => {
    				if(String(val).indexOf("J") > -1) {
    				flag = true;
    				return;
    			}
    		});
    			if(flag) return obj;
    		});
    	Isto devolve
    		[{
    			id: 1,
    			name: "John",
    			age: 28
    		},{
    			id: 2,
    			name: "Jane",
    			age: 31
    		}]

## 12.5. Ordenando arrays
    	O método .sort() ordena os elementos dunha matriz. O método predefinido ordenará a matriz segundo a cadea os puntos do código Unicode. Para ordenar numéricamente unha matriz, o método .sort() precisa ter unha funcion de comparación.
    	O método .sort() é impuro. .sort() ordenará a propia matriz, é dicir, no canto de crear un copia ordenada da matriz orixinal, ordenará a matriz orixinal e devolveuna.

    	Orde predeterminada
    	Ordena a matriz en orde UNICODE.

    		['s', 't', 'a', 34, 'K', 'o', 'v', 'E', 'r', '2', '4', 'o', 'W', -1, '-4'].sort();
    	dá:
    		[-1, '-4', '2', 34, '4', 'E', 'K', 'W', 'a', 'l', 'o', 'o', 'r', 's', 't', 'v']
    	Os caracteres en maiúsculas movéronse por riba de minúsculas. A matriz non está en orde alfabética e os números non están en orde numérica.

    	Ordenación alfabética

    		['s', 't', 'a', 'c', 'K', 'o', 'v', 'E', 'r', 'f', 'l', 'W', '2', '1'].sort((a, b) => { return a.localeCompare(b); });
    	dá:
    		['1', '2', 'a', 'c', 'E', 'f', 'K', 'l', 'o', 'r', 's', 't', 'v', 'W']
    	O tipo anterior lanzará un erro se calquera elemento da matriz non é unha cadea. Se sabes que a matriz pode conter elementos que non sexan strings e usar a versión segura seguinte.

    	String ordenadas por lonxitude (a máis longa primeiro)
    		["zebras", "dogs", "elephants", "penguins"].sort(function(a, b) {
    			return b.length - a.length;
    		});
    	dá
    		["elephants", "penguins", "zebras", "dogs"];

    	String ordenadas por lonxitude (a máis curta primeiro)
    		["zebras", "dogs", "elephants", "penguins"].sort(function(a, b) {
    			return a.length - b.length;
    		});
    	dá
    		["dogs", "zebras", "penguins", "elephants"];

    	Números ordenados (ascendente)
    		[100, 1000, 10, 10000, 1].sort(function(a, b) {
    			return a - b;
    		});
    	dá
    		[1, 10, 100, 1000, 10000]

    	Números ordenados (descendente)
    		[100, 1000, 10, 10000, 1].sort(function(a, b) {
    			return b - a;
    		});
    	dá
    		[10000, 1000, 100, 10, 1]

    	Ordenando un array por pares e impares
    		[10, 21, 4, 15, 7, 99, 0, 12].sort(function(a, b) {
    			return (a & 1) - (b & 1) || a - b;
    		});
    		V > 6
    		array.sort((a,b)=> (a & 1) - (b & 1) || a - b);
    	dá
    		[0, 4, 10, 12, 7, 15, 21, 99]

    	Ordenando data (descendente)
    		var dates = [
    			new Date(2007, 11, 10),
    			new Date(2014, 2, 21),
    			new Date(2009, 6, 11),
    			new Date(2016, 7, 23)
    		];
    		dates.sort(function(a, b) {
    			if (a > b) return -1;
    			if (a < b) return 1;
    			return 0;
    		});
    		// the date objects can also sort by its difference
    		// the same way that numbers array is sorting
    		dates.sort(function(a, b) {
    			return b -a;
    		});

    		dá
    		Results in:
    		[
    			"Tue Aug 23 2016 00:00:00 GMT-0600 (MDT)",
    			"Fri Mar 21 2014 00:00:00 GMT-0600 (MDT)",
    			"Sat Jul 11 2009 00:00:00 GMT-0600 (MDT)",
    			"Mon Dec 10 2007 00:00:00 GMT-0700 (MST)"
    		]

## 12.6. Iteración
    	Un buble for tradicional
    	Un bucle for  tradicional ten tres compoñentes:
    		1. A inicialización: executada antes de que se execute o primeiro bloqueo
    		2. A condición: comproba unha condición cada vez que se executa o bloque de lazo e sae do circuíto se é falso
    		3. O reasignación posterior: realizada cada vez que se executa o bloque de bucle
    	Estes tres compoñentes están separados uns dos outros por un; símbolo. O contido para cada un destes tres os compoñentes é opcionais, o que significa que o seguinte é o loop mínimo posible:
    		for (;;;){
    			// do stuff
    		}

    	Por suposto, terá que incluír un if (condición === true) {break; } ou un if (condición === true) { return; } nalgún lugar dentro dese for para consegua de deixar de funcionar.
    	Normalmente, porén, a inicialización úsase para declarar un índice, a condición úsase para comparar ese índice cun valor mínimo ou máximo, e o pensamento posterior úsase para incrementar o índice:
    		for (var i = 0, lonxitude = 10; i <lonxitude; i ++) {
    			console.log (i);
    		}
    	Usar un for  para facer un bucle a través dunha matriz
    	O xeito tradicional de circular a través dunha matriz é o seguinte:
    		for (var i= 0, length = myArray.length; i < length; i ++){
    			console.log(myArray[i]);
    		}

    	para (var i = 0, lonxitude = myArray.length; i <lonxitude; i ++) {
    	console.log (myArray [i]);
    	}

    	Hai, sen embargo, moitas variacións posibles. Calquera que sexa o que mellor funciona é en gran parte unha cuestión de gusto persoal e o caso de uso específico que está a implementar. Teña en conta que cada unha destas variacións está soportada por todos os navegadores, incluídos os moi antigos.

    	O bucle while
    	Unha alternativa a un loop for é un loop de while. Para facer un loop a través dunha matriz, pode facelo:
    		var key = 0;
    		while(value = myArray[key++]){
    			console.log(value);
    		}

    	Como tradicional para os for, os bucles while son soportados mesmo polos navegadores máis antigos.
    	Teña en conta que cada bucle while pode reescribirse como un  for. Por exemplo, o while que se compón é o o mesmo xeito que este for:
    		for(var key = 0; value = myArray[key++];){
    			console.log(value);
    		}

    	for ... in
    	En js, tamén se pode facer isto:
    		for (i in myArray) {
    			console.log(myArray[i]);
    		}
    	Isto debe ser usado con coidado, porén, xa que non se comporta o mesmo que un bucle tradicional en todos os casos, e hai posibles efectos secundarios que deben considerarse.

    	for ... of (version > 6 )
    	En ES6 recoméndase uhar o bucle for-of para iterar os valores dun array:
    		Version ≥ 6
    		let myArray = [1, 2, 3, 4];
    		for (let value of myArray) {
    			let twoValue = value * 2;
    			console.log("2 * value is: %d", twoValue);
    		}

    	O exemplo mostra a diferenza entre un bucle for-ir e un for-of:
    		Version ≥ 6
    		let myArray = [3, 5, 7];
    		myArray.foo = "hello";

    		for (var i in myArray) {
    			console.log(i); // logs 0, 1, 2, "foo" //mostra os índices
    		}

    		for (var i of myArray) {
    			console.log(i); // logs 3, 5, 7			// mostra os valores dos índices numéricos
    		}

    	Array.prototype.keys()
    	O método array.prototype.keys() pódese usr para iterar sobre os índices
    		Version ≥ 6
    		let myArray = [1, 2, 3, 4];
    		for (let i of myArray.keys()) {
    			let twoValue = myArray[i] * 2;
    			console.log("2 * value is: %d", twoValue);
    		}

    	Array.prototype.forEach()
    	O método array.prototype.forEach() é unha opción  a partir de ES5. Non admite un break;
    		[1, 2, 3, 4].forEach(function(value, index, arr) {
    			var twoValue = value * 2;
    			console.log("2 * value is: %d", twoValue);
    		});

    	Array.prototype.every()
    	Desde ES5, pódese iterar unha porción dun array con Array.prototype.every(), que o itera ate que retorna false:
    		Version ≥ 5
    		// [].every() stops once it finds a false result
    		// thus, this iteration will stop on value 7 (since 7 % 2 !== 0)
    		[2, 4, 7, 9].every(function(value, index, arr) {
    			console.log(value);
    			return value % 2 === 0; // iterate until an odd number is found
    		});

    	que equivale a
    		var arr = [2, 4, 7, 9];
    		for (var i = 0; i < arr.length && (arr[i] % 2 !== 0); i++) { // iterate until an odd number isfound
    			console.log(arr[i]);
    		}

    	Array.prototype.some
    	Array.prototype.some() itera ata que devolve true
    		Version ≥ 5
    		// [].some stops once it finds a false result
    		// thus, this iteration will stop on value 7 (since 7 % 2 !== 0)
    		[2, 4, 7, 9].some(function(value, index, arr) {
    			console.log(value);
    			return value === 7; // iterate until we find value 7
    		});

    		Equivalent in any JavaScript version:
    		var arr = [2, 4, 7, 9];
    			for (var i = 0; i < arr.length && arr[i] !== 7; i++) {
    			console.log(arr[i]);
    		}

    	librerías
    	jQuery.each(), in jQuery:
    		$.each(myArray, function(key, value) {
    			console.log(value);
    		});
    	_.each(), in Underscore.js:
    		_.each(myArray, function(value, key, myArray) {
    			console.log(value);
    		});
    	_.forEach(), in Lodash.js:
    		_.forEach(myArray, function(value, key) {
    			console.log(value);
    		});

## 12.7. Desestruturación dun array
    	Un array pode ser desestruturado cando se asigna a unha nova variable
    		const triangle = [3, 4, 5];
    		const [length, height, hypotenuse] = triangle;
    		length === 3; // → true
    		height === 4; // → true
    		hypotneuse === 5; // → true

    	Pódense omitir elementos:
    		const [,b,,c] = [1, 2, 3, 4];
    		console.log(b, c); // → 2, 4

    	Tamén se pode usar o operador rest
    		const [b,c, ...xs] = [2, 3, 4, 5];
    		console.log(b, c, xs); // → 2, 3, [4, 5]

    	ou pasándo como argumento dunha función
    		function area([length, height]) {
    			return (length * height) / 2;
    		}

    		const triangle = [3, 4, 5];
    		area(triangle); // → 6

## 12.8. Eliminar elementos duplicados.
    	Desde ES5.1 en diante, pode usar o método nativo Array.prototype.filter para facer un bucle  a través dunha matriz e deixar só entradas que pasan unha función de devolución de chamada dada.
    	No seguinte exemplo, o callback comproba se o valor dado ocorre na matriz. Se o fai, é un duplicado e non se copiará na matriz resultante.
    		Version ≥ 5.1
    		var uniqueArray = ['a', 1, 'a', 2, '1', 1].filter(function(value, index, self) {
    			return self.indexOf(value) === index;
    		}); // returns ['a', 1, 2, '1']

    	Se o teu entorno soporta ES6, tamén podes usar o obxecto Set. Este obxecto permite almacenar valores únicos de calquera tipo, sexa valores primitivos ou referencias de obxectos:
    	Versión ≥ 6
    	var uniqueArray = [... new Set(['a', 1, 'a', 2, '1', 1])];

## 12.9. Comparación de arrays
    	Para unha comparación de arrays pódese usar JSON.stringify(), pero isto só funcionará se os dous obxectos son serializables por JSON e non conteñen referencias cíclicas. Pode lanzar TypeError: converter a estrutura circular a JSON.
    				JSON.stringify(array1) === JSON.stringify(array2)


    	Pode usar unha función recursiva para comparar arrays.
    		function compareArrays(array1, array2) {
    		var i, isA1, isA2;
    		isA1 = Array.isArray(array1);
    		isA2 = Array.isArray(array2);
    		if (isA1 !== isA2) { // is one an array and the other not?
    			return false; // yes then can not be the same
    		}
    		if (! (isA1 && isA2)) { // Are both not arrays
    			return array1 === array2; // return strict equality
    		}
    		if (array1.length !== array2.length) { // if lengths differ then can not be the same
    			return false;
    		}
    			// iterate arrays and compare them
    		for (i = 0; i < array1.length; i += 1) {
    			if (!compareArrays(array1[i], array2[i])) { // Do items compare recursively
    				return false;
    			}
    		}
    		return true; // must be equal
    	}

    	AVISO: Usar a función anterior é perigosa e debe envolverse nun try-catchse sospeita que hai unha oportunidade a matriz ten referencias cíclicas (unha referencia a unha matriz que contén unha referencia a si mesma):
    		a = [0] ;
    		a[1] = a;
    		b = [0, a];
    		compareArrays(a, b); // throws RangeError: Maximum call stack size exceeded
    	Nota: a función usa o operador de igualdade estricta === para comparar os elementos non de matriz {a: 0} === {a: 0} é falso (porque están apuntando a referencias de memorias distintas)

## 12.10. Volteando arrays
    	Úsase o método .reverse() para invertir a orde dos de elementos dun array
    		[1, 2, 3, 4].reverse();
    	dá:
    		[4, 3, 2, 1]

    	Nota: Por favor, teña en conta que .reverse (Array.prototype.reverse) revertirá a propia matriz. En vez de devolver unha copia inversa, devolverá a mesma matriz inversa.
    		var arr1 = [11, 22, 33];
    		var arr2 = arr1.reverse();
    		console.log(arr2); // [33, 22, 11]
    		console.log(arr1); // [33, 22, 11]

    	Tamén pode reverter unha matriz "profundamente" por:
    		function deepReverse(arr) {
    			arr.reverse().forEach(elem => {
    				if(Array.isArray(elem)) {
    					deepReverse(elem);
    				}
    			});
    			return arr;
    		}

    	Exemplo para deepReverse:
    		var arr = [1, 2, 3, [1, 2, 3, ['a', 'b', 'c']]];
    		deepReverse(arr);
    	dá
    		arr // -> [[['c','b','a'], 3, 2, 1], 3, 2, 1]

## 12.11. Clonado superficial de un array
    	Ás veces, cómpre traballar cunha matriz asegurando que non modifica o orixinal. No canto dun método de clonación, as matrices teñen un método de corte que lle permite realizar unha copia superficial de calquera parte dunha matriz. Teña presente que isto só clona o primeiro nivel. Isto funciona ben con tipos primitivos, como números e cadeas, pero non obxectos.
    	Para clonar superficialmente unha matriz (é dicir, ter unha nova instancia de matriz pero cos mesmos elementos), pode usar o seguinte
    		var clone = arrayToClone.slice();

    	Isto chama ao método integrado JavaScript Array.prototype.slice. Se pasar argumentos para cortar, pode obter máis comportamentos complicados que crean clones pouco profundos de só unha parte dunha matriz, pero para os nosos propósitos só a chamada porción () creará unha copia superficial de toda a matriz.
    	Todos os métodos utilizados para converter obxectos similares a matriz son aplicables para clonar unha matriz:
    		Version ≥ 6
    		arrayToClone = [1, 2, 3, 4, 5];
    		clone1 = Array.from(arrayToClone);
    		clone2 = Array.of(...arrayToClone);
    		clone3 = [...arrayToClone] // the shortest way

    		Version ≤ 5.1
    		arrayToClone = [1, 2, 3, 4, 5];
    		clone1 = Array.prototype.slice.call(arrayToClone);
    		clone2 = [].slice.call(arrayToClone);

## 12.12. Concatenando arrays

Para concatenar arrays temos dúas alternativas. 
Sexan os arrays 
```javascript
let array1 = ["a", "b"], array2 = ["c", "d"], array3 = ["e", "f"], array4 = ["g", "h"];
```

Version ≥ 3
Sintaxe anterior a ES6. A sintaxe anterior a ES6 usa o método `Array.concat()`. Este método muta o array que o invoca, polo que para crear un novo array, é preciso crealo de cero:
```javascript
let concatedArray = []
arrayConcat.concat(array1, array2, array3, array4)
```

Version ≥ 6
Sintaxe posterior a ES6. A sintaxe posterior a ES6 usa o operator **spread**, que opera de maneira inmutable:
```javascript
let concatedArray = [...array1, ...array2, ...array3, ...array4]
```

En ambos casos o resultado é o mesmo array: 
```javascript
concatedArray // ["a", "b", "c", "d", "e", "f", "g", "h"]
```

Tamén nos dous casos se poden combinar elementos simples xunto con arrays de variables.
```javascript
let  arrConc = array.concat("c", "d");
let arrConc = [...array, "c", "d"]
```

## 12.13. Unir dous arrays en par de chave-valor
Cando temos dúas array separadas e queremos formar un par chave-valor, pódese usar a función .reduce() do xeito seguinte
var columns = ["Date", "Number", "Size", "Location", "Age"];
var rows = ["2001", "5", "Big", "Sydney", "25"];
var result = rows.reduce(function(result, field, index) {
result[columns[index]] = field;
return result;
}, {})
console.log(result);

saída
{
Date: "2001",
Number: "5",
Size: "Big",
Location: "Sydney",
Age: "25"
}

## 12.14. Array con spread / rest
    	Spread operator

    	Version ≥ 6
    	Con ES6, pode utilizar spreads para separar elementos individuais dun array:
    		let arr = [1, 2, 3, ...[4, 5, 6]]; // [1, 2, 3, 4, 5, 6]

    		// in ES < 6, as operacións the operations above are equivalent to
    		arr = [1, 2, 3];
    		arr.push(4, 5, 6);

    	O operador de propagación (spread) tamén actúa sobre strings, separando cada carácter individual dun novo elemento de cadea.
    	Polo tanto, empregando unha función de matriz para convertela en números enteiros, a matriz creada anteriormente equivale esta:
    		let arr = [1, 2, 3, ...[..."456"].map(x=>parseInt(x))]; // [1, 2, 3, 4, 5, 6]

    	Ou, usando unha única cadea, isto podería simplificarse para:
    		let arr = [..."123456"].map(x=>parseInt(x)); // [1, 2, 3, 4, 5, 6]

    	Se non o mapeamos, o array será de strings
    		let arr = [..."123456"]; // ["1", "2", "3", "4", "5", "6"]

    	O operador spread  tamén se pode usar para pasarlle un array de argumentos a unha función:
    		function myFunction(a, b, c) {
    			console.log(a * 2, b - 10,  c + 1);
    		}
    		let args = [0, 1, 2];
    		myFunction(...args); // 0 -9 3

    		// in ES < 6, this would be equivalent to:
    		myFunction.apply(null, args);

    	O operador rest
    	Ten un comportamento o inverso a spread, fusionando varios argumentos nun:
    		[a, b, ...rest] = [1, 2, 3, 4, 5, 6]; // rest is assigned [3, 4, 5, 6]

    	Recoller argumentos dunha función:
    		function myFunction(a, b, ...rest) { console.log(rest); }
    		myFunction(0, 1, 2, 3, 4, 5, 6); // rest is [2, 3, 4, 5, 6]

## 12.15. Filtrando valores
    	O método filter() crea un array filtrado con todosos elementos que pasan o test pasado como función.
    		Version ≥ 5.1
    		[1, 2, 3, 4, 5].filter(function(value, index, arr) {
    			return value > 2;
    		});

    		Version ≥ 6
    		[1, 2, 3, 4, 5].filter(value => value > 2);

    		dá o array:
    			[3, 4, 5]

    	Filtar valores falsos
    		Version ≥ 5.1
    		var filtered = [ 0, undefined, {}, null, '', true, 5].filter(Boolean);

    		Dado que Boolean é unha función / constructor de JavaScript nativo que ten [un parámetro opcional] e o método de filtro tamén toma unha función e pasa o elemento de matriz actual como parámetro. O resultado é:
    			[{}, true, 5]

    	Outro exemplo
    	Este exemplo usa o mesmo concepto de paso dunha función que toam un argumento:

    	Version ≥ 5.1
    	function startsWithLetterA(str) {
    		if(str && str[0].toLowerCase() == 'a') {
    			return true
    		}
    		return false;
    	}
    	var str = 'Since Boolean is a native javascript function/constructor that takes [one
    	optional parameter] and the filter method also takes a function and passes it the current array as a parameter, you could read it like the following';
    	var strArray = str.split(" ");
    	var wordsStartsWithA = strArray.filter(startsWithLetterA); //["a", "and", "also", "a", "and", "array", "as"]

## 12.16. Buscando un array

A forma recomendada (desde ES5) é `usar Array.prototype.find()`:
```javascript
let people = [ { name: "bob" }, { name: "john" } ];
let bob = people.find(person => person.name === "bob");
// Or, more verbose
let bob = people.find(function(person) {
    	return person.name === "bob";
    });
```

En calquera función de JS, un bucle for tamén se pode usar:
```javascript
for (var i = 0; i < people.length; i++) {
    if (people[i].name === "bob") {
    	break; // we found bob
    }
}
```

**FindIndex**
O método `findIndex()` devolve un index no array, se un elemento do array satisfay a test fornecido. Doutro modo, retórnase -1;
```javascript
let array = [
    { value: 1 },
    { value: 2 },
    { value: 3 },
    { value: 4 },
    { value: 5 }
];
let index = array.findIndex(item => item.value === 3); // 2
let index = array.findIndex(item => item.value === 12); // -1
```

## 12.17. Convertindo un string un array.

    	.split()
    		var strArray = "StackOverflow".split("");
    		// strArray = ["S", "t", "a", "c", "k", "O", "v", "e", "r", "f", "l", "o", "w"]

    	operador spread
    		var strArray = [..."sky is blue"];
    		// strArray = ["s", "k", "y", " ", "i", "s", " ", "b", "l", "u", "e"]

## 12.18. Borrar items dun array

shift() elimina o primeiro elemento
let array = [1, 2, 3, 4];
array.shift();
dá:
[2, 3, 4]

Pop
pop() elimina o último elemento
let array = [1, 2, 3];
array.pop();
dá:
[1, 2]

O método `splice()` devolve un conxunto de elementos dun array ao mesmo tempo que os elimina do array orixinal. Recibe o argumentos a posición desde que inicia o curteo e a súa lonxitude e devolve un array cos elementos eliminados.
```javascript
let array = [1, 2, 3, 4];
let array2 = array.splice(1, 2);
console.log(array); //  [1, 4]
console.log(array2); // [2, 3]
```

delete() elimina un item sen modificar a lonxitude dun array:
var array = [1, 2, 3, 4, 5];
console.log(array.length); // 5
delete array[2];
console.log(array); // [1, 2, undefined, 4, 5]
console.log(array.length); // 5

Array.prototype.length
Asignar valor á lonxitude da matriz cambia a lonxitude a un valor dado. Se o novo valor é menor que os elementos de lonxitude da matriz elimínase do final do valor.
array = [1, 2, 3, 4, 5];
array.length = 2;
console.log(array); // [1, 2]

## 12.19. Eliminando todos os elementos
    	var arr = [1, 2, 3, 4];

    	Reescribilo
    		arr = [];

    	Seteando a lonxitude a cero
    		arr.length = 0;

    	Con splice()
    		arr.splice(0);

## 12.20. Encontrar o mínimo ou o máximo
    	var myArray = [1, 2, 3, 4];

    	Math.max.apply()
    		Math.max.apply(null, myArray); //4

    	Math.min.apply()
    		Math.min.apply(null, myArray); //1

    	A partir de ES6 pode usarse o operador spread:
    		Math.max.apply(...myArray); //4
    		Math.min.apply(...myArray); //4

##     12.21. Inicialización estándar dun array
    	Hai dúas formas de inicialiar o array:
    		var arr = [1, 2, 3, 4];
    		var arr2 = new Array(1, 2, 3, 4);

## 12.22. Unindo un array nunha cadea
    	con join()
    		console.log(["Hello", " ", "world"].join("")); // "Hello world"
    		console.log([1, 800, 555, 1234].join("-")); // "1-800-555-1234"

## 12.23. Eliminar / engadir elementos usando splice()

    	splice() pode usarse para eliminar elements dun array:
    		var values = [1, 2, 3, 4, 5, 3];
    		var i = values.indexOf(3);
    		if (i >= 0) {
    			values.splice(i, 1);
    		} // [1, 2, 4, 5, 3]

    	tamén se pode usar para agregar elementos a un array:
    		var values = [1, 2, 4, 5, 3];
    		var i = values.length + 1;
    		values.splice(i, 0, 6, 7, 8);
    		//[1, 2, 4, 5, 3, 6, 7, 8]

## 12.24. O método entries()
    	O método entries() devolve un obxecto Iterador de array que contén pares chave-valor para cada index no array:
    		Version ≥ 6
    		var letters = ['a','b','c'];
    		for(const[index,element] of letters.entries()){
    			console.log(index,element);
    		}
    	dá
    		0 "a"
    		1 "b"
    		2 "c"

## 12.25. Eliminar un valor dun array
    	Cando teña que eliminar un valor específico dunha matriz, pode usar o seguinte paquete único para crear unha matriz de copia sen o valor dado:
    		array.filter (function (val) {return val! == to_remove;});

    	Ou se quere cambiar a matriz en si sen crear unha copia (por exemplo, se escribe unha función que obteña unha matriz como unha función e manipúlala), pode usar este script:
    		while(index = array.indexOf(3) !== -1) {
    			array.splice(index, 1);
    		}

    	E se precisa eliminar só o primeiro valor atopado, elimine o while:
    		var index = array.indexOf(to_remove);
    		if(index !== -1) {
    			array.splice(index , 1);
    		}

## 12.26. Alisando arrays
    	Arrays bidimensionais
    		En ES6, pódese alisar o array co operador  ...:
    			function flattenES6(arr) {
    				return [].concat(...arr);
    				}
    			var arrL1 = [1, 2, [3, 4]];
    			console.log(flattenES6(arrL1)); // [1, 2, 3, 4]

    		Version ≥ 5
    		En ES5, podemos conseguilo con .apply():
    			function flatten(arr) {
    				return [].concat.apply([], arr);
    			}
    			var arrL1 = [1, 2, [3, 4]];
    			console.log(flatten(arrL1)); // [1, 2, 3, 4]

    	Arrays n-dimensionais
    		Dado un conxunto de nidos profundos como este
    			var deeplyNested = [4, [5,6, [7,8],

    		Pódese aplanar con esta maxia
    			console.log(String(deeplyNested).split(',').map(Number);
    			#=> [4,5,6,7,8,9]
    		ou
    			const flatten = deeplyNested.toString().split(',').map(Number)
    			console.log(flatten);
    			#=> [4,5,6,7,8,9]

    		Os dous métodos anteriores só funcionan cando a matriz está composta exclusivamente por números. Non se pode achatar unha matriz multidimensional de obxectos por este método.

## 12.27. Engadir items a un array ao principio e ao final dun array
    	Unshift
    	.unshift() agrega un ou máis items no principio dun array.
    		var array = [3, 4, 5, 6];
    		array.unshift(1, 2);
    	dá
    		[1, 2, 3, 4, 5, 6]

    	Push
    	.push() agrega un ou máis itens no final dun array.
    		var array = [1, 2, 3];
    		array.push(4, 5, 6);
    	dá
    		[1, 2, 3, 4, 5, 6]

## 12.28. Obxecto de claves-valor a array
    	Sexa
    		var object = {
    			key1: 10,
    			key2: 3,
    			key3: 40,
    			key4: 20
    		};

    		var array = [];
    		for(var people in object) {
    			array.push([people, object[people]]);
    		}
    	dá
    		[
    			["key1", 10],
    			["key2", 3],
    			["key3", 40],
    			["key4", 20]
    		]

##  12.29. Lóxica conectiva de valores
    	.some e .every permiten unha conexión lóxica cos valores de array.
    	Mentres .some combina os valores de retorno con OR, .every os combina con AND.
    	Exemplos de .some
    		[false, false].some(function(value) {
    			return value;
    		});
    		// Result: false
    			[false, true].some(function(value) {
    		return value;
    		});
    		// Result: true
    		[true, true].some(function(value) {
    			return value;
    		});
    		// Result: true

    	E exemplos para .every
    		[false, false].every(function(value) {
    			return value;
    		});
    		// Result: false
    		[false, true].every(function(value) {
    			return value;
    		});
    		// Result: false
    		[true, true].every(function(value) {
    			return value;
    		});
    		// Result: true

## 12.30. Comprobando se un obxecto é un array
    	Array.isArray (obj) devolve verdadeiro se o obxecto é un array, se non falso.
    		Array.isArray([]) // true
    		Array.isArray([1, 2, 3]) // true
    		Array.isArray({}) // false
    		Array.isArray(1) // false

    	Na maioría dos casos pódese comprobar se un obxecto é un array.
    		[] instanceof Array; // true
    		{} instanceof Array; // false

    	Array.isArray ten a vantaxe de usar un checkof de instancias en que aínda se devolverá true mesmo se o prototipo da matriz foi modificado e devolverá false se se modificou un prototipo non array a prototipo de array.
    		var arr = [];
    		Object.setPrototypeOf(arr, null);
    		Array.isArray(arr); // true
    		arr instanceof Array; // false

## 12.31. Insertar un item dun array de index específico
    	A inserción sinxela do elemento pódese facer co método Array.prototype.splice:
    		arr.splice(index, 0, item);

    	Variante máis avanzada con argumentos múltiples e soporte de encadeamento:
    		/* Syntax:
    		array.insert(index, value1, value2, ..., valueN) */
    		Array.prototype.insert = function(index) {
    			this.splice.apply(this, [index, 0].concat(
    				Array.prototype.slice.call(arguments, 1)));
    			return this;
    		};
    		["a", "b", "c", "d"].insert(2, "X", "Y", "Z").slice(1, 6); // ["b", "X", "Y", "Z", "c"]

    	E con argumentos de tipo array que fusionan e encadean soporte:
    		/* Syntax:
    		array.insert(index, value1, value2, ..., valueN) */
    		Array.prototype.insert = function(index) {
    			index = Math.min(index, this.length);
    			arguments.length > 1
    			&& this.splice.apply(this, [index, 0].concat([].pop.call(arguments)))
    			&& this.insert.apply(this, arguments);
    			return this;
    		};
    		["a", "b", "c", "d"].insert(2, "V", ["W", "X", "Y"], "Z").join("-"); // "a-b-V-W-X-Y-Z-c-d"

## 12.32. Ordenando un array multidimensional
    	Dado o seguinte array
    		var array = [
    			["key1", 10],
    			["key2", 3],
    			["key3", 40],
    			["key4", 20]
    		];

    	Pódese ordenar polo segundo item
    		array.sort(function(a, b) {
    			return a[1] - b[1];
    		})

    		Version ≥ 6
    		array.sort((a,b) => a[1] - b[1]);

    	dá
    		[
    			["key2", 3],
    			["key1", 10],
    			["key4", 20],
    			["key3", 40]
    		]

##  12.33. Comprobando os elementos dun array
    	.every() comproba que todos os elemento dun array pasan unha función de test:
    		[1, 2, 1].every(function(item, i, list) { return item === list[0]; }); // false
    		[1, 1, 1].every(function(item, i, list) { return item === list[0]; }); // true

    		Version ≥ 6
    		[1, 1, 1].every((item, i, list) => item === list[0]); // true

    		The following code snippets test for property equality
    		let data = [
    			{ name: "alice", id: 111 },
    			{ name: "alice", id: 222 }
    		];
    		data.every(function(item, i, list) { return item === list[0]; }); // false
    		data.every(function(item, i, list) { return item.name === list[0].name; }); // true



    		Version ≥ 6
    		data.every((item, i, list) => item.name === list[0].name); //

## 12.34. Copiar parte dun array

O método `.slice()` devolve unha copia superficial dunha porción dun array, sen modificalo. Recibe como parámetros o inicio e o final e ambos son opcionais. Se non recibe parámetros copa o todo o array.

Exemplo 1
```javascript
// Let's say we have this Array of Alphabets
let arr = ["a", "b", "c", "d"...];
// I want an Array of the first two Alphabets
let newArr = arr.slice(0, 2); // newArr === ["a", "b"]
```

Examplo 2
```javascript
// Let's say we have this Array of Numbers
// and I don't know it's end
let arr = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9...];
// I want to slice this Array starting from
// number 5 to its end
let newArr = arr.slice(4); // newArr === [5, 6, 7, 8, 9...]
```

## 12.35. Comprobando un elemento nun array
O método `includes()` é unha ferramento para comprobar se certo elemento está presente nun array. Devolve `true` ou `false`. Non acepta ningunha función na igualdade, unicamente buscará coincidencias con obxectos ou primitivos. 

O método `some()` é similar anterior, coa diferenza que admite unha función de igualdade como callback.
```javascript
const array = [10, 30, 50, 10, 5];
const greaterThan10 = (element) => element > 10;
console.log(array.some(greaterThan10)); // outputs true
``` 

O método `every()` é similar ao anterior, coa diferenza que só devolverá true se todos os elementos cumpren co requisitos:
```javascript
const array = [10, 30, 50, 10, 5];
const greaterThan10 = (element) => element > 10;
console.log(array.every(greaterThan10)); // outputs false
```


## Resume métodos en array

|          | principio    | posición interior                        | final     |
| -------- | ------------ | ---------------------------------------- | --------- |
| agregar  | `.unshift()` | `.splice(ini, núm. elementos, elemento)` | `.push()` |
| eliminar | `.shift()`   | `.splice(ini, núm. elementos)`           | `.pop()`  |

# 13.  OBXECTOS
    Propiedade Descrición
    value O valor a asignar á propiedade.
    writable Se o valor da propiedade pode cambiarse ou non.
    enumerable Se a propiedade será enumerada en en bucles ou non.
    configurable Se será posible redefinir ou non o descriptor de propiedade.
    get Función que se chamará que devolva o valor da propiedade.
    set Función que asigna un valor a un propiedade.

    13.1. Clonado superficial
    ES6 úsase o médodo .assign();
    const existing = { a: 1, b: 2, c: 3 };
    const clone = Object.assign({}, existing);

        Tamén se pode usar o operador spread
        	const existing = { a: 1, b: 2, c: 3 };
        	const { ...clone } = existing;

        En versión anteriores úsase un iteración:
        	var existing = { a: 1, b: 2, c: 3 };
        	var clone = {};
        	for (var prop in existing) {
        		if (existing.hasOwnProperty(prop)) {
        			clone[prop] = existing[prop];
        		}
        	}

    13.3. Método .freeze()
    Inmobiliza un obxecto bloqueando a posibilidade de variar ou engadir propiedades.

    13.3. Clonado profundo de obxectos.
    Para realizar un clonado profundo dun obxecto úsase os métodos de JSON:
    var existing = { a: 1, b: { c: 2 } };
    var copy = JSON.parse(JSON.stringify(existing));
    existing.b.c = 3; // copy.b.c will not change

    13.4. Iteración de propiedades dun obxecto
    Pódese construír un bucle for in e tomar a propiedade mediante object.hasOwnProperty(property):
    for (var property in object) {
    // always check if an object has a property
    if (object.hasOwnProperty(property)) {
    // do stuff
    }
    }

        Tamén se pode usar a función .map() ou .forEach()
        	var obj = { 0: 'a', 1: 'b', 2: 'c' };
        	Object.keys(obj).map(function(key) {
        		console.log(key);
        	});
        	// outputs: 0, 1, 2

    13.5. asign():
    Úsase para asignar propiedades a un obxecto existente:
    var user = {
    firstName: "John"
    };
    Object.assign(user, {lastName: "Doe", age:39});
    console.log(user); // Logs: {firstName: "John", lastName: "Doe", age: 39}

        ou crear unha copia superficial dun obxecto:
        	var obj = Object.assign({}, user);
        	console.log(obj); // Logs: {firstName: "John", lastName: "Doe", age: 39}

        ou fundir nun único obxecto varias propiedades de diversos obxectos
        	var obj1 = {
        		a: 1
        	};
        	var obj2 = {
        		b: 2
        	};
        	var obj3 = {
        		c: 3
        	};
        	var obj = Object.assign(obj1, obj2, obj3);
        	console.log(obj); // Logs: { a: 1, b: 2, c: 3 }
        	console.log(obj1); // Logs: { a: 1, b: 2, c: 3 }, target object itself is changed

    13.6. rest /spread de obxectos
    O operadore de spread funciona igual que asign:
    let obj = { a: 1 };
    let obj2 = { ...obj, b: 2, c: 3 };
    console.log(obj2); // { a: 1, b: 2, c: 3 };

    13.7. defineProperty()
    Permite definir unha propiedade dun obxecto a través do seu descritor:
    var obj = { };
    Object.defineProperty(obj, 'foo', { value: 'foo' });
    console.log(obj.foo);

    13.8. getters e setters
    Definidos tal que
    var person = { name: "John", surname: "Doe"};
    Object.defineProperty(person, 'fullName', {
    get: function () {
    return this.name + " " + this.surname;
    },
    set: function (value) {
    [this.name, this.surname] = value.split(" ");
    }
    });

    13.9. nomes de propiedades variables / dinámicas
    Gardar variables nunha variables:
    var dictionary = {
    lettuce: 'a veggie',
    banana: 'a fruit',
    tomato: 'it depends on who you ask',
    apple: 'a fruit',
    Apple: 'Steve Jobs rocks!' // properties are case-sensitive
    }
    Recupérase pola variable, con corchese se é un string:
    var word = prompt('What word would you like to look up today?')
    var definition = dictionary[word]
    var definition = dictionary.word

    13.10. Os arrays son obxectos.
    Non está recomendado, pero os arrays poden ser tratatos como obxectos.

    13.11. .seal()
    Evita a adición ou borrado de propiedades, pero permite a edición a diferenza de .freeze().

    13.12. Convertir o valores de obxecto a un array.
    tal que así:
    var obj = {
    a: "hello",
    b: "this is",
    c: "javascript!",
    };
    var array = Object.keys(obj)
    .map(function(key) {
    return obj[key];
    });
    console.log(array); // ["hello", "this is", "javascript!"]

    13.13. Obter as propiedades dun obxecto
    Métodos - bucle for...in - object.keys() - object.getOwnProperties()

    13.14. Propiedades só lectura
    con .defineProperty()
    Object.defineProperty(a, 'foo', { value: 'original', writable: false });

    13.15. Propiedades non enumerables
    Podemos evitar que unha propiedade non se mostre non bucles for...in
    Object.defineProperty(obj, "foo", { value: 'show', enumerable: true });
    Object.defineProperty(obj, "bar", { value: 'hide', enumerable: false });

    13.15. Bloquear a descrición de propiedade
    Object.defineProperty(obj, "foo", {value: "original value", writable: false, configurable: false });

    13.16. Obter meta propiedades
    var sampleObject = {
    hello: 'world'
    };
    Object.getOwnPropertyDescriptor(sampleObject, 'hello');
    // Object {value: "world", writable: true, enumerable: true, configurable: true}

    13.18. Descritores e nomes de propiedades.
    As propiedades son pares de nomes e descritores. O nome permite acceder a través de notación do punto ou do corchete. O descritor describe o comportamento do propiedade:
    value, writable, enumerable, configurable.

    13.19 .keys
    Retorna un array coas clave dos obxectos.
    var obj = {
    a: "hello",
    b: "this is",
    c: "javascript!"
    };
    var keys = Object.keys(obj);
    console.log(keys); // ["a", "b", "c"]

    13.20. Propiedades con caracteres especiais ou palabras reservadas.
    En caso de necesidades especiais, usar os corchetes:
    myObject['special property ☺'] = 'it works!'
    console.log(myObject['special property ☺'])

    13.21. Crear un obxecto interable.

    13.22. .entries()
    Devolve un array de pares chave-valor dun obxecto:
    const obj = {
    one: 1,
    two: 2,
    three: 3
    };
    Object.entries(obj);
    dá
    [
    ["one", 1],
    ["two", 2],
    ["three", 3]
    ]

    13.23. .values()
    Devolve un array cos valores do obxecto:
    var obj = { 0: 'a', 1: 'b', 2: 'c' };
    console.log(Object.values(obj)); // ['a', 'b', 'c']

# 14.  ARITMÉTICA- LIBRERÍA MATH

    14.1 Constantes
    As constantes que se inclúen son: o número e, Ln10, Ln2, Log10 de e, log2 de e, pi, raíz de 1/2, raíz de 2, épsilon, máximo seguro, máximo, mínimo seguro, minimo, infinito negativo, infinito positivo, infinito.

    14.2. Operador de módulo
    Devolve o resto dunha división.
    40 / 10 = 4.
    40 % 10 = 2.
    40 - 4 _ 10 = 2:
    40 = 4 _ 10 + 2
    Úsase para comprobar se un enteiro é múltiplo doutro.
    Tamén se usa para realizar un incremento dun valor nun intervalo.
    Tamén para obtere o parte fraccionar dun número % 1.

    14.3. Rendondeo
    Math.round() redondea ao enteiro máis próximo.
    Math.ceil() redondea ao enteiro superior.
    Math.floor() redondeda ao enteiro inferior.
    Math.trunc() trunca a parte decimal

        Redondear a un número de decimais. Úsase .round(), .ceil(), .floor():
        	var myNum = 2/3; // 0.6666666666666666
        	var multiplier = 100;
        	var a = Math.round(myNum * multiplier) / multiplier; // 0.67
        	var b = Math.ceil (myNum * multiplier) / multiplier; // 0.67
        	var c = Math.floor(myNum * multiplier) / multiplier; // 0.66

    14.4. Trigonometría
    Math.sin(r) seno de r
    Math.asin(r) arcoseno de r
    Math.asinh(r) arcoseno hiperbólico de r
    Math.cos(r) coseno de r
    Math.acos(r) arcocoseno de r
    Math.acosh(r) arcocoseno hiperbólico de r
    Math.tan(r) tanxente de r
    Math.atan(r) arcotanxente de r
    Math.atan(r) arcotanxente hiperbólica de r

    14.5. Operador Bitwise
    Operan a nivel de bit con integers de 32 bit

    14.6. Operador de incremento
    ++

    14.7. Exponenciación
    Math.pow()
    \*\*
    Pode usarse Math.pow() para buscar a n-esima potencia pasándolle como argumento o inverso.

    14.8. Números aleatorios
    Math.random();
    Definir un intervalo:
    Math.random() \* (max - min ) + min,

        Enteiro
        	Math.floor(Math.random() * (max - min )) + min,

    14.9. Adición +

    14.10. little big endian

    14.11. Aleatorio entre dous números
    // randomBetween(0, 10);
    Math.floor(Math.random() _ 11);
    // randomBetween(1, 10);
    Math.floor(Math.random() _ 10) + 1;
    // randomBetween(5, 20);
    Math.floor(Math.random() _ 16) + 5;
    // randomBetween(-10, -2);
    Math.floor(Math.random() _ 9) - 10;

    14.12. Simular eventos con n probabilidades
    var evento = Math.floor(posibilidades \* Math.random()); // para un dado 6.

    14.13. Subtracción -

    14.14. Multiplicación \*

    14.15. Máximo e mínimo
    De varios númerow
    Math.max(a, b)
    Math.min(a, b)
    De un array
    Math.max.apply(Math, array)
    Math.min.apply(Math, array)

        con spread
        	Math.max(... array)
        	Math.min(... array)

    14.16. Restrinxir rango de mínimo e máximo

    14.17. Ceiling e floor

    14.18. Obtendo raíces dun número
    Math.sqrt() raiz cadrada
    Math.cbrt() raiz cúbica
    Math.pow() raiz enésima

    14.19. Obtendo rando con unha distribución normal.

    14.20. Math.atan2 para encontrar un vector
    Math.atan(y, x) devolve o radio en graos s

    14.21. seno e coseno: vector

    14.22. Pitágoras
    Math.hypot() calcula a hipotenusa


    14.21. Funcións periódicas usando Math.sin()

    14.24. Division
    	/

    14.25. Decremento
    	--

# 15. OPERADORES BITWISE
    O operadors bitwise realizan operacións nos valores de bit dos datos. Os operadores bitwise transforman os operandos en enteiros de 32 bits en complemento a 2.

    Conversión a enteiros de 32 bits
    A transformación realízase prescindo dos bits máis significativos (a partir de 32º desde a dereita).

    Complemento a 2
    Un binario posto en complemento a 2 doutro é o inverso a partir o 1º 1 desde a dereita.

    Bitwise AND
    A operación AND a bit a & b devolve o valor binario con 1 onde ambos operandos binarios teñen 1 posición específica e 0 en todas as demais posicións. Por exemplo:
    13 & 7 // 5
    13: 1101
    7: 0111
    0101 : 5

    Aplicación práctica: comprobación se un numero é par:
    if(n & 1) {
    console.log("impar!");
    } else {
    console.log("par!");
    }

    Bitwise OR
    A operación AND a bit a | b devolve o valor binario con 1 onde un ou ambos operandos binarios teñen 1 posición específica e 0 onde ambos teñen 0. Por exemplo:
    13 | 7 => 15
    // 13: 1101
    // 7: 0111
    // 15: 1111

    Bitwise NOT
    A operación NON a bit ~a devolve o valor binario convertindo os 1 e 0 e á inversa:
    ~13 => -14
    // 13: 0..01101
    //-----------------
    //-14: 1..10010 (-16 + 0 + 0 + 2 + 0)

    Bitwise XOR
    A operación AND a bit a ^ b devolve o valor binario con 1 onde os operandos son diferentes 0 onde son iguais. Por exemplo:
    13 ^ 7 => 10
    // 13: 0..01101
    // 7: 0..00111
    //-----------------
    // 10: 0..01010 (0 + 8 + 0 + 2 + 0)

    Aplicación práctica
    Intercambio de valores enteiros.
    var a = 11, b = 22;
    a = a ^ b;
    b = a ^ b;
    a = a ^ b;
    console.log("a = " + a + "; b = " + b);// a is now 22 and b is now 11

    15.2. Operadores Shift <<, >>, >>>
    Desprazan n posicións cara a esquerda ou cara a dereita. >> mantén o signo no número >>> engade 0

# 16. A FUNCIÓN DE CONSTRUTOR

    16.1. Declarando a función construtor
    As funcións do constructor son funcións deseñadas para construír un novo obxecto. Dentro dunha función constructora, this refírese a un obxecto recentemente creado a cal se poden asignar valores. As funcións do constructor devolven este novo obxecto automaticamente.
    function Cat(name) {
    this.name = name;
    this.sound = "Meow";
    }

        Invócanse as funcións do constructor usando a nova palabra clave:
        	let cat = new Cat("Tom");
        	cat.sound; // Returns "Meow"

        As funcións do constructor tamén teñen unha propiedade de prototipo que apunta a un obxecto cuxas propiedades son herdadas automaticamente por todos os obxectos creados con este constructor:
        	Cat.prototype.speak = function() {
        	console.log(this.sound);
        	}
        	cat.speak(); // Outputs "Meow" to the console

        Os obxectos creados polas funcións do constructor tamén teñen unha propiedade especial no seu prototipo chamado constructor, que apunta á función usada para crealos:
        	cat.constructor // Returns the `Cat` function

        Os obxectos creados polas funcións do constructor tamén se consideran como "instancias" da función constructora polo
        operador de instancia:
        	cat instanceof Cat // Returns "true"

# 16.  DECLARACIÓNS E ASIGNACIÓNS

## 16.1. Modificando constantes:

Isto é posible:

```javascript
    const person = {
    name: "John"
    };
```
    console.log('The name of the person is', person.name);
    person.name = "Steve";
    console.log('The name of the person is', person.name);
    person.surname = "Fox";
    console.log('The name of the person is', person.name, 'and the surname is', person.surname);

## 16.2. Declarando e inicializando constantes
    const nome = valor.

## 16.3. Declaración - var: alcance de función - let: alcance de bloque - const: alcance de bloque

## 16.4. Undefined
    Cando se declara unha función sen inicializar ten valor undefined.

## 16.5. Tipos de datos
    O tipo de datos déducese dos datos. Unha variable pode recibir diferentes tipos de datos.

## 16.6. Operacións matémáticas e asignación de valores.
    += incremento
    -= decremento
    \*= multiplicación
    /= división
    \*\*= exponenciación
    %= modulo

## 16.7. Asignación

Operador de asignación =.
A declaración e asignación en dous pasos non é compatible co modo estrito.

## 16.8. Operador de coalescencia nula ?? e asignación de coalescencia nula ??=

O operador de coalescencia exexuta o lado esquerdo da expresión

```javascript
let message
message ?? "Alternative message"
// "Alternative message"
```

O operador de asginación de coalescencia nula permite asignar un valor a unha variable sempre se sexa **null** ou **undefined**.

```javascript
// estilo analítico
const message;
if (messagee === null || message === undefined){
	message = "Hello";
}
console.log(message) // "Hello"

// estilo sintético
message ??= "Bye";
console.log(message) // "Bye"
```

## 16.9 Asignacion con desestruturación 

# 17.  BUCLES
## 17.1. Bucle for estándar
    for (var i = 0; i < 100; i++) {
    console.log(i);
    }

## 17.2. Bucle for...of
    Máis conciso, evita os problemas de for...in, admite break, continue e return (forEach non).
    Soporta arrays, string, sets, map e obxecto.

        	const iterable = [0, 1, 2];
        	for (let item of iterable) {
        		console.log(item);
        	}

## 17.3. Bucle for...in
    Este buble está pensado para percorrer keys, non se recomenda con array:
    var object = {"a":"foo", "b":"bar", "c":"baz"};
    // `a` is inaccessible
    Object.defineProperty(object , 'a', {
    enumerable: false,
    });
    for (var key in object) {
    if (object.hasOwnProperty(key)) {
    console.log('object.' + key + ', ' + object[key]);
    }
    }

    18.4. Bucles while e do...while
    var i = 0;
    while (i < 100) {
    console.log(i);
    i++;
    }

        	var i = 0;
        	do  {
        		console.log(i);
        		i++;
        	} while (i < 100);

    18.5. continue nun bucle
    Salta a execución na iteración onde se cumpre a condición
    for (var i = 0; i < 3; i++) {
    if (i === 1) {
    continue;
    }
    console.log(i);
    } // 0 2

    18.6. Romper un bucle determinado
    Usáse etiquetas
    outerloop:
    for (var i = 0;i<3;i++){
    innerloop:
    for (var j = 0;j <3; j++){
    console.log(i);
    console.log(j);
    if (j == 1){
    break outerloop;
    }
    }
    } // 0 0 0 1

    18.7. Bucle do...while
    Corre como mínimo unha vez.

    18.8. Break e continue con etiquetas

# 19.  FUNCIÓNS
## 19.1. Alcance de funcións
    Cando JavaScript tenta resolver unha referencia ou unha variable, comeza a buscala no ámbito actual. Se non atopa esa declaración no ámbito actual, aumenta un alcance para buscala. Este proceso repítese ata que se atopou a declaración. Se o analizador de JavaScript alcanza o alcance global e aínda non pode atopar a referencia, lanzarase un erro de referencia.

        Se hai dúas variables co mesmo nome en diferentes alcances, prodúcese un efecto de sombra (shadow) da interna sobre a externa:
        	var a = 'hello';
        	function foo() {
        		var a = 'world';
        		function bar() {
        			console.log(a); // => 'world'
        		}
        	}

        Versión ≥ 6
        A forma en que JavaScript resolve o alcance tamén se aplica á palabra clave const. Declarar unha variable coa palabra chave const implica que non está autorizado a reasignar o valor, pero declaralo nunha función creará un novo ámbito e con iso unha nova variable.

        Non obstante, as funcións non son os únicos que crean un ámbito (se está a usar let ou const). as declaracións let e const teñen o alcance da declaración de bloque máis próxima.

##  19.2. Currying (de cociñar con curry)
    O currying é a transformación dunha función de n aridade ou argumentos nunha secuencia de n funcións que só toman un argumento.
    Casos de uso: cando os valores dalgúns argumentos están dispoñibles antes que outros, pode usar currying para descompoñer unha función nunha serie de funcións que completan o traballo por etapas, como chega cada valor. Isto pode ser útil:

        	- Cando o valor dun argumento case nunca cambia (por exemplo, un factor de conversión), pero cómpre manter a flexibilidade de establecer ese valor (en lugar de codificalo como unha constante).

        	- Cando o resultado dunha función de curry é útil antes de executar as outras funcións de curry.

        	- Para validar a chegada das funcións nunha secuencia específica.
        	Por exemplo, o volume dun prisma rectangular pode explicarse por unha función de tres factores: lonxitude (l), ancho (w), e altura (h):
        		var prism = function(l, w, h) {
        			return l * w * h;
        		}

        	Versión "cociñada":
        		function prism(l) {
        			return function(w) {
        				return function(h) {
        					return l * w * h;
        				}
        			}
        		}
        		Version ≥ 6
        		var prism = l => w => h => l * w * h;

        	Pódese chamar a secuencia de funcións coa sintaxe prism(2)(3)(5), que debe avaliar a 30.
        	Sen maquinaria extra (como nas bibliotecas), o currying está limitado a ES 5/6
        	debido á falta de valores reservados; así, mentres podes usar var a = prism(2)(3) para crear unha función parcialmente aplicada, pero non sepode usar prism()(3)(5).

##  19.3. Expresións de funcións invocadas inmediatamente (autoinvocadas)
    Ás veces non se quere que unha función sexa accesible / almacenada como unha variable. Pode crear unha expresión de función invocada inmediatamente (IIFE en breve). Estas son esencialmente funcións anónimas de auto execución. Teñen o acceso ao ámbito circundante, pero a propia función e as variables internas serán inaccesibles desde o exterior.

        Unha cousa importante a destacar sobre IIFE é que se auto executa, o IIFE non son invocatos  as funcións estándares e non se poden chamar co nome da función coa que se declaran.
        	(function() {
        		alert("I've run - but can't be run again because I'm immediately invoked at runtime, leaving behind only the result I generate");
        	}());

        Este é outro xeito de escribir IIFE. Teña en conta que o paréntese de peche antes do punto e coma foi movido e colocado xusto despois da pechadura:
        	(function() {
        		alert("This is IIFE too.");
        	})();

        Pode pasar facilmente parámetros a un IIFE:
        	(function(message) {
        		alert(message);
        	}("Hello World!"));

        Ademais, pode devolver valores
        	var example = (function() {
        		return 42;
        	}());
        	console.log(example); // => 42

        Se é necesario, é posible nomear un IIFE. Aínda que se ve con menos frecuencia, este patrón ten varias vantaxes, como proporcionar unha referencia que pode usarse para unha recursividade e pode facer que a depuración sexa máis sinxela xa que o nome está incluído
        no callstack.
        	(function namedIIFE() {
        		throw error; // We can now see the error thrown in 'namedIIFE()'
        	}());

        Aínda que envolver unha función entre paréntese é o xeito máis común de denotar ao analizador de JavaScript para esperar unha expresión, nos lugares onde unha expresión xa está esperada, a notación pódese facer máis concisa:
        	var a = function () {return 42} ();
        	console.log (a) // => 42

        Versión de frecha da función inmediatamente invocada:
        Versión ≥ 6
        (() => console.log ("Ola!")) (); // => Ola!

## 19.4. Funcións con nome
    Teñen nome
    var namedSum = function sum (a, b) { // named
    return a + b;
    }

        Diferéncianse das anónimas en
        	- Cando se fai debug, aparede o nome na traza de error.
        	- Son "izadas".
        	- Teñen un funcionamento diferente na recursión.
        	- Dependendo da versión de ES, tratan de forma diferente a propiedade nome.

        As funcións nomeadas son izadas
        Poden chamarse antes da declaración (as anónimas non).
        	foo();
        	function foo () { // using a named function
        		console.log('bar');
        	}

        Funcionamento en recursión.
        	var say = function (times) {
        		if (times > 0) {
        				console.log('Hello!');
        		say(times - 1);
        		}
        	}
        	//you could call 'say' directly,
        	//but this way just illustrates the example
        	var sayHelloTimes = say;
        	sayHelloTimes(2); // Hello!, Hello!

        Unha función anónima non se pode chamar deste xeito.

        A propiedade nome
        Varía de versión a versión
        	Version ≤ 5
        	var foo = function () {}
        	console.log(foo.name); // outputs ''

        	function foo () {}
        	console.log(foo.name); // outputs 'foo'

        	Version ≥ 6
        	var foo = function () {}
        	console.log(foo.name); // outputs 'foo'

        	function foo () {}
        	console.log(foo.name); // outputs 'foo'

        	var foo = function bar () {}
        	console.log(foo.name); // outputs 'bar'

## 19.5. Vinculando 'this' e argumentos

        Versión ≥ 5.1
        Cando se fai unha referencia a un método (unha propiedade que é unha función) en JavaScript, normalmente non recorda o obxecto ao que foi ligado orixinalmente. Se o método ten que referirse a ese obxecto como this, non será capaz de facelo, e
        ao chamalo probablemente causará un fallo.

        Pode usar o método .bind () nunha función para crear un envoltorio que inclúa o valor de this e calquera dos argumentos principais.
        	var monitor = {
        		threshold: 5,
        		check: function(value) {
        				if (value > this.threshold) {
        					this.display("Value is too high!");
        				}
        			},
        		display(message) {
        			alert(message);
        		}
        	};

        	monitor.check(7); // o valor de `this` está implicado na sintaxe do método => monitor.
        	var badCheck = monitor.check;

        	badCheck(15); //  o valor de  `this` é o obxecto window object e this.threshold é undefined,

        	var check = monitor.check.bind(monitor);
        	check(15); // O valor de `this` foi ligado explicitamente ao obxecto .

        	var check8 = monitor.check.bind(monitor, 8);
        	check8(); // We also bound the argument to `8` here. It can't be re-specified.

        	No modo estrito this é undefined por defecto.


    		Version ≥ 7
    		Operador Bind
    		O operador Bind (::) pode usarse como versión abreviada do anterior:
    			var log = console.log.bind(console); // long version
    			const log = ::console.log; // short version

    			foo.bar.call(foo); // long version
    			foo::bar(); // short version

    			foo.bar.call(foo, arg1, arg2, arg3); // long version
    			foo::bar(arg1, arg2, arg3); // short version

    			foo.bar.apply(foo, args); // long version
    			foo::bar(...args); // short version

## 19.6. Funcións con número de argumentos indeterminados
    	Depende do entorno
    	Versión ≤ 5
    	Sempre que se chama unha función, ten un obxecto de argumentos de tipo array no seu ámbito, que contén todos os argumentos pasados á función. A indexación ou a iteración sobre isto dará acceso aos argumentos, por exemplo
    		function logSomeThings() {
    			for (var i = 0; i < arguments.length; ++i) {
    				console.log(arguments[i]);
    			}
    		}
    		logSomeThings('hello', 'world');
    		// logs "hello"
    		// logs "world"

    	Versión ≥ 6
    	Desde ES6, a función pódese declarar co seu último parámetro usando o operador rest (...). Isto crea unha matriz que contén os argumentos desde ese momento:
    		function personLogsSomeThings(person, ...msg) {
    			msg.forEach(arg => {
    				console.log(person, 'says', arg);
    			});
    		}
    		personLogsSomeThings('John', 'hello', 'world');
    		// logs "John says hello"
    		// logs "John says world"

    	Tamén se pode usar a sintaxe spread
    		const logArguments = (...args) => console.log(args)
    		const list = [1, 2, 3]
    		logArguments('a', 'b', 'c', ...list)
    		// output: Array [ "a", "b", "c", 1, 2, 3 ]

## 19.7. Funcións anónimas
    	Son funcións sen nome. Úsanse parar
    		- asignalas a variables:
    			var foo = function(){ /*...*/ };
    			foo();

    		- pasalas como argumentos a unha función
    			var nums = [0,1,2];
    			var doubledNums = nums.map( function(element){ return element * 2; } ); // [0,2,4]

    		- retornar unha función
    			var hash = getHashFunction( 'sha1' );
    			var hashValue = hash( 'Secret Value' );
    			function getHashFunction( algorithm ){
    				if ( algorithm === 'sha1' ) return function( value ){ /*...*/ };
    				else if ( algorithm === 'md5' ) return function( value ){ /*...*/ };
    			}

## 19.8. Parámetros por defecto.
    	Depende da versión
    		Versión ≤ 5
    		function printMsg(msg) {
    			msg = typeof msg !== 'undefined' ? msg : 'Default value for msg.';
    			console.log(msg);
    		}
    	ou
    		function printMsg(msg) {
    			msg = msg || 'Default value for msg.';
    			console.log(msg);
    		}

    		Version ≥ 6
    		function printMsg(msg='Default value for msg.') {
    			console.log(msg);
    		}

## 19.9. Call e apply
    	As funcións teñen dous métodos integrados que permiten ao programador fornecer argumentos e esta variable de xeito diferente: call e apply.
    	Isto é útil porque as funcións que operan nun obxecto (o obxecto do que son unha propiedade) poden ser reaprovisionadas para funcionar noutro obxecto compatible. Ademais, os argumentos pódense dar nun tiro como matrices, semellante ao operador spread (...) en ES6.
    		let obj = {
    			a: 1,
    			b: 2,
    			set: function (a, b) {
    				this.a = a;
    				this.b = b;
    			}
    		};
    		obj.set(3, 7); // normal syntax
    		obj.set.call(obj, 3, 7); // equivalent to the above
    		obj.set.apply(obj, [3, 7]); // equivalent to the above; note that an array is used
    		console.log(obj); // prints { a: 3, b: 5 }
    		let myObj = {};
    		myObj.set(5, 4); // fails; myObj has no `set` property
    		obj.set.call(myObj, 5, 4); // success; `this` in set() is re-routed to myObj instea of obj
    		obj.set.apply(myObj, [5, 4]); // same as above; note the array
    		console.log(myObj); // prints { a: 3, b: 5 }

## 19.10. Aplicación parcial
    	Parecido a currying, reduce os argumentos; a diferenza deste, o número ten que ser reducido a 1.

## 19.11. Pasando argumenteos por referencia ou por valor
    	En JavaScript todos os argumentos pásanse por valor. Cando unha función asigna un novo valor a unha variable de argumento, ese cambio non será visible para o obxecto que a chama:
    		var obj = {a: 2};
    		function myfunc(arg){
    			arg = {a: 5}; // Repara que a asignación faise sobre arg, non obj
    		}
    		myfunc(obj);
    		console.log(obj.a); // 2

    	Non obstante, as chamadas (sobre as propiedades anidadas) destes argumentos serán visibles para a persoa que chama:
    		var obj = {a: 2};
    		function myfunc(arg){
    			arg.a = 5; // assignment to a property of the argument
    		}
    		myfunc(obj);
    		console.log(obj.a); // 5

    	Isto pode verse como unha chamada por referencia: aínda que unha función non pode cambiar o obxecto que chama asignándolle un novo valor, podería mudar propiedades do obxecto chamado.

    	Os argumentos  primitivos, como números ou strings, son inmutables, non hai ningunha forma de que unha función os mude:
    		var s = 'say';
    		function myfunc(arg){
    			arg += ' hello'; // assignment to the parameter variable itself
    		}
    		myfunc(s);
    		console.log(s); // 'say'

    	Cando unha función quere mudar un obxecto pasado como argumento, pero non quere mudar realmente o obxecto chamado, o argumento debe ser reasignado:
    		var obj = {a: 2, b: 3};
    		function myfunc(arg){
    			arg = Object.assign({}, arg); // assignment to argument variable, shallow copy
    			arg.a = 5;
    		}
    		myfunc(obj);
    		console.log(obj.a); // 2

    	Como alternativa á mutación no lugar dun argumento, as funcións poden crear un novo valor, baseado no argumento e devolvelo. O chamador pode entón asignalo, ata á variable orixinal pasada como argumento:
    		var a = 2;
    		function myfunc(arg){
    			arg++;
    			return arg;
    		}
    		a = myfunc(a);
    		console.log(obj.a); // 3

## 19.12. Tipoe de arugumentos, rest e spread
    	As funcións poden ter entradas en forma de variables que se poden usar e asignar dentro do seu propio ámbito. A seguinte función ten dous valores numéricos e devolve a súa suma:
    		function addition (argument1, argument2){
    		return argument1 + argument2;
    		}
    		console.log(addition(2, 3)); // -> 5

    	Argumentos obxecto
    	Os argumentos obxectos conteñen todos os parámetros da función que conteñen un valor non predeterminado. Tamén pode usarse aínda que os parámetros non sexan declarados explícitamente:
    		(function() { console.log(arguments) })(0,'str', [2,{3}]) // -> [0, "str", Array[2]]

    	Aínda que ao imprimir argumentos a saída se asemella a unha matriz, é de feito un obxecto:
    		(function() { console.log(typeof arguments) })(); // -> object

    	Parámtros rest function(...param){}
    	En ES6, a sintaxe ... cando se usa na declaración dos parámetros dunha función transforma a variable á súa dereita nun único obxecto que contén todos os parámetros restantes proporcionados despois dos declarados. Isto permite que se invoque a función cun número ilimitado de argumentos, que pasará a formar parte desta variable:
    		(function(a, ...b){console.log(typeof b+': '+b[0]+b[1]+b[2]) })(0,1,'2',[3],{i:4});
    		// -> object: 123

    	Parámetros spread : function(... varb);
    	En ES6, a sintaxe ... tamén se pode usar cando se invoca unha función colocando un obxecto / variable á súa dereita. Isto permite que os elementos do obxecto pasen a esa función como un único obxecto:
    		let nums = [2,42,-1];
    		console.log(...['a','b','c'], Math.max(...nums)); // -> a b c 42

## 19.13. Función de composoción
    	Compoñer varias funcións nun mesma é unha práctica común de programación funcional;
    	A composición fai un pipeline a través do cal transita a información e se vai modificando simplemente traballando na composición de funcións (como xuntar pezas dunha pista xuntos).
    	comeza con algunhas funcións de responsabilidade única:

    	Versión ≥ 6
    		const capitalize = x => x.replace(/^\w/, m => m.toUpperCase());
    		const sign = x => x + ',\nmade with love';

    	e cree facilmente unha pista de transformación:

    	Versión ≥ 6
    		const formatText = compose(capitalize, sign);
    		formatText('this is an example')
    		//This is an example,
    		//made with love

    	N.B. A composición lógrase a través dunha función de utilidade que normalmente chámase compoñer como no noso exemplo.
    	A implementación de compose está presente en moitas bibliotecas de utilidades JavaScript (lodash, rambda, etc.) pero tamén pode comezar cunha implementación sinxela como:
    	Versión ≥ 6

##  19.14. Obtendo o nome dunha función
    	ES6
    		function.name
    	ES5

##  19.15 Función Recursiva
    	Son funcions que se chaman a si mesmas
    		function factorial (n) {
    			if (n <= 1) {
    				return 1;
    			}
    		return n * factorial(n - 1);
    		}

##  19.16. Usando a sentenza return
    	- usando o retorno como argumento doutro funciaón
    	- rematando a función
    	Admite retornar varias liñas

##  19.17. Funcións como variables
    	var prop = (v)=> value;

## 19.18. Valores por defecto
	// Longhand
function volume(length, width, height) {
  if (width === undefined) width = 2;
  if (height === undefined) height = 2;
  return length * width * height;
}

// Shorthand
volume = (length, width = 2, height = 2) => length * width * height;

# 20.  PROGRAMACIÓN funcional

    20.1. Funcións de alto nivel
    Unha función de alto nivel é aquela que devolve outra función:
    function iAmJustFunction() {
    // do some stuff ...
    // return a function.
    return function iAmReturnedFunction() {
    console.log("returned function has been invoked");
    }
    }
    // invoke your higher-order function and its returned function.
    iAmJustFunction()();

    20.2. Mónada de identidade
    Este é un exemplo de implementación da monad identidade en JavaScript e podería servir como punto de partida para crear outras monadas.

        Usar este enfoque reutilizando as túas funcións será máis sinxelo debido á flexibilidade que proporciona esta monada e os pesadelos da composición:
        	f(g(h(i(j(k(value), j1), i2), h1, h2), g1, g2), f1, f2)

        lexible, agradable e limpo:
        	identityMonad(value)
        		.bind(k)
        		.bind(j, j1, j2)
        		.bind(i, i2)
        		.bind(h, h1, h2)
        		.bind(g, g1, g2)
        		.bind(f, f1, f2)

        	function identityMonad(value) {
        		var monad = Object.create(null);
        		// func should return a monad
        		monad.bind = function (func, ...args) {
        		return func(value, ...args);
        		};
        		// whatever func does, we get our monad back
        		monad.call = function (func, ...args) {
        		func(value, ...args);
        		return identityMonad(value);
        		};
        		// func doesn't have to know anything about monads
        		monad.apply = function (func, ...args) {
        		return identityMonad(func(value, ...args));
        		};
        		// Get the value wrapped in this monad
        		monad.value = function () {
        		return value;
        		};
        		return monad;
        	};

        Funciona con valores primitivos
        	var value = 'foo',
        		f = x => x + ' changed',
        		g = x => x + ' again';

        	identityMonad(value)
        		.apply(f)
        		.apply(g)
        		.bind(alert); // Alerts 'foo changed again'

        E tamén con obxectos
        	var value = { foo: 'foo' },
        		f = x => identityMonad(Object.assign(x, { foo: 'bar' })),
        		g = x => Object.assign(x, { bar: 'foo' }),
        		h = x => console.log('foo: ' + x.foo + ', bar: ' + x.bar);

        	identityMonad(value)
        		.bind(f)
        		.apply(g)
        		.bind(h); // Logs 'foo: bar, bar: foo'

        Probemos todo:
        	var add = (x, ...args) => x + args.reduce((r, n) => r + n, 0),
        		multiply = (x, ...args) => x * args.reduce((r, n) => r * n, 1),
        		divideMonad = (x, ...args) => identityMonad(x / multiply(...args)),
        		log = x => console.log(x),
        		substract = (x, ...args) => x - add(...args);

        	identityMonad(100)
        		.apply(add, 10, 29, 13)
        		.apply(multiply, 2)
        		.bind(divideMonad, 2)
        		.apply(substract, 67, 34)
        		.apply(multiply, 1239)
        		.bind(divideMonad, 20, 54, 2)
        		.apply(Math.round)
        		.call(log); // Logs 29

    20.3. Funcións puras
    As función puras son aquelas que: - Dada unha entrada, sempre retornan a mesma saída - Non dependen de ningunha variable externa ao seu alcance. - Non modifican o estado da aplicación (non teñen efecto laterais).

        Non modifican unha variable externa
        Función impura
        	let obj = { a: 0 }
        	const impure = (input) => {
        		// Modifica input.a
        		input.a = input.a + 1;
        		return input.a;
        	}
        	let b = impure(obj)
        	console.log(obj) // Logs { "a": 1 }
        	console.log(b) // Logs 1
        Esta función cambia obj, que é externo a ela.

        Función pura
        	let obj = { a: 0 }
        	const pure = (input) => {
        	// Non modifica  modify obj
        		let output = input.a + 1;
        		return output;
        	}
        	let b = pure(obj)
        	console.log(obj) // Logs { "a": 0 }
        	console.log(b) // Logs 1

        Non depende de variables externas
        Función impura (cando muda a variable externa, muda o resultado)
        	let a = 1;
        	let impure = (input) => {
        		// Multiply with variable outside function scope
        		let output = input * a;
        		return output;
        	}
        	console.log(impure(2)) // Logs 2
        	a++; // a becomes equal to 2
        	console.log(impure(2)) // Logs 4

        Función pura
        	let pure = (input) => {
        		let a = 1;
        		// Multiply with variable inside function scope
        		let output = input * a;
        		return output;
        	}
        	console.log(pure(2)) // Logs 2

    20.4. Funcións como argumentos
    Sexa
    function transform(fn, arr) {
    let result = [];
    for (let el of arr) {
    result.push(fn(el)); // We push the result of the transformed item to result
    }
    return result;
    }
    console.log(transform(x => x \* 2, [1,2,3,4])); // [2, 4, 6, 8]
    Como se pode ver, a función transform() acepta dous argumentos: unha función e un array. Iterará o array e aplicará a cada elemento a función.
    É semellante a array.prototype.map();

9.  PROTOTIPOS E OBXECTOS
    No JS convencional non hai clases, en cambio temos prototipos. Do mesmo xeito que a clase, o prototipo herda as propiedades, incluídos os métodos e as variables declaradas na clase. Podemos crear a nova instancia do obxecto sempre que sexa necesario, Object.create (PrototypeName); (tamén podemos dar o valor para o constructor)

    21.1. Creación ne inicializando prototipo
    object.prototype.construtor -> reescribe o construtor
    object.prototype.property/Function -> escribe/reescribe unha propiedade función

        Sexa
        	var Human = function() {
        		this.canWalk = true;
        		this.canSpeak = true; //
        	};
        	Person.prototype.greet = function() {
        		if (this.canSpeak) { // checks whether this prototype has instance of speak
        			this.name = "Steve"
        			console.log('Hi, I am ' + this.name);
        		} else{
        			console.log('Sorry i can not speak');
        		}
        	};

        O prototipo pode ser instanciada tal que
        	obj = Object.create(Person.prototype);
        	ob.greet();

        Podemos pasarlle valores ao construtor e facer o boolean true e false segundo cumpra:
        	var Human = function() {
        		this.canSpeak = true;
        	};

        	// Basic greet function which will greet based on the canSpeak flag
        	Human.prototype.greet = function() {
        		if (this.canSpeak) {
        			console.log('Hi, I am ' + this.name);
        		}
        	};

        	var Student = function(name, title) {
        		Human.call(this); // Instantiating the Human object and getting the members of the class
        		this.name = name; // inheriting the name from the human class
        		this.title = title; // getting the title from the called function
        	};

        	Student.prototype = Object.create(Human.prototype);
        	Student.prototype.constructor = Student;
        		Student.prototype.greet = function() {
        			if (this.canSpeak) {
        				console.log('Hi, I am ' + this.name + ', the ' + this.title);
        		}
        	};

        	var Customer = function(name) {
        		Human.call(this); // inheriting from the base class
        		this.name = name;
        	};

        	Customer.prototype = Object.create(Human.prototype); // creating the object
        	Customer.prototype.constructor = Customer;
        	var bill = new Student('Billy', 'Teacher');
        	var carter = new Customer('Carter');
        	var andy = new Student('Andy', 'Bill');
        	var virat = new Customer('Virat');

        	bill.greet();
        	// Hi, I am Bob, the Teacher

        	carter.greet();
        	// Hi, I am Carter

        	andy.greet();
        	// Hi, I am Andy, the Bill

        	virat.greet();

# 21. CLASSES

As clases en ES son unha funcionalidade que permiten programar seguindo paradigma da **programación orientada a obxextos**.

## 22.1. Construtor de clase
Para declarar unha clase úsase a palabra reservada `class`. O método construtor pode recibir parámetros.
En ES6 todas as clases son públicas. ?

``` Javascript
class MyClass {
    constructor(option) {
    console.log(`Creating instance using ${option} option.`);
    this.option = option;
   }
}
```

Para instanciar a clase úsase a palabra reservada `new`: 
``` Javascript
const foo = new MyClass('speedy'); // logs: "Creating instance using speedy option"
```

## 22.2. Herdanza de clase
Só traballa en POO. Os métodos os métodos da superclase son accesibles na subclase.
Para que unha clase herde doutra úsase o operador `extends`.
A subclase invoca o construtor do pai vía super() e accédese a si mesmo con `this`.

``` Javascript
class SuperClass {
    constructor() {
        this.logger = console.log;
    }
    log() {
        this.logger(`Hello ${this.name}`);
	}
}

class SubClass extends SuperClass {
	constructor() {
    	super();
        this.name = 'subclass';
	}
}

const subClass = new SubClass();
subClass.log(); // logs: "Hello subclass"
```

## 22.3. Métodos estáticos
Úsase a palabra reservada `static`. Non son accesibles desde as instancias da clase pero si desde as subclases:

``` Javascript
class MyClass {
	static myStaticMethod() {
		return 'Hello';
	}
	static get myStaticProperty() {
		return 'Goodbye';
	}
}
console.log(MyClass.myStaticMethod()); // logs: "Hello"
console.log(MyClass.myStaticProperty()); // logs: "Goodbye"
```

## 22.4. Getters e Setters

Para estblecer métodos selectores e modificador úsanse as palabras reservadas `get` e `set` respectivamente:

``` Javascript
class MyClass {
	constructor() {
		this.names = [];
	}
	set name(value) {
		this.names.push(value);
	}
	get name() {
		return this.names 
	}
}

const myClassInstance = new MyClass();
myClassInstance.name = 'Joe';
myClassInstance.name = 'Bob';
console.log(myClassInstance.name); // logs: "Bob"
console.log(myClassInstance.names); // logs: ["Joe", "Bob"]

```

## 22.5. Membros privados
    JavaScript non soporta técnicamente aos membros privados como característica da linguaxe. A privacidade - descrita por Douglas Crockford - é emulada a través de closures (ámbito de función preservado) que se xerarán cada un con cada chamada de instanciación dunha función constructora.
    O exemplo da Queue demostra como, coas funcións do constructor, o estado local pode preservarse e facerse accesible tamén mediante métodos privilexiados.
    class Queue {
    constructor () { // - does generate a closure with each instantiation.
    const list = []; // - local state ("private member").
    this.enqueue = function (type) { // - privileged public method
    // accessing the local state
    list.push(type); // "writing" alike.
    return type;
    };
    this.dequeue = function () { // - privileged public method
    // accessing the local state
    return list.shift(); // "reading / writing" alike.
    };
    }
    }
    var q = new Queue; //
    //
    q.enqueue(9); // ... first in ...
    q.enqueue(8); //
    q.enqueue(7); //
    //
    console.log(q.dequeue()); // 9 ... first out.
    console.log(q.dequeue()); // 8
    console.log(q.dequeue()); // 7
    console.log(q); // {}
    console.log(Object.keys(q)); // ["enqueue","dequeue"]

        Con cada instanciación dun tipo de cola, o constructor xera un closure.

        Deste xeito, os dous métodos propios dun tipo de cola introducen e desanúlanse (véxase Object.keys (q)) aínda ten acceso á lista que segue vivindo no seu alcance que se conservou no momento da construción.

        Empregando este patrón - emulando membros privados a través de métodos públicos privilexiados - hai que ter presente que, con cada exemplo, consumirase memoria adicional para cada método de propiedade propia (pois é un código que
        non se pode compartir / reutilizar). O mesmo é certo para o importe / tamaño do estado que se vai almacenar dentro deste peche.

## 22.6. Métodos
    Os métodos son funcións que se poden definir nas clases para realizar unha función e, opcionalmente, devolver un resultado. Poden recibir argumentos do interlocutor.
    class Something {
    constructor(data) {
    this.data = data
    }
    doSomething(text) {
    return {
    data: this.data,
    text
    }
    }
    }

        	var s = new Something({})
        	s.doSomething("hi") // returns: { data: {}, text: "hi" }

## 22.7. Nomes de método dinámicos
    Tamén existe a capacidade de avaliar expresións ao nomear métodos similares a como pode acceder ás propiedades dun obxecto con []. Isto pode ser útil para ter nomes de propiedades dinámicas, pero úsase frecuentemente en conxunto con símbolos.
    let METADATA = Symbol('metadata');
    class Car {
    constructor(make, model) {
    this.make = make;
    this.model = model;
    }
    // example using symbols
    [METADATA]() {
    return {
    make: this.make,
    model: this.model
    };
    }
    // you can also use any javascript expression
    // this one is just a string, and could also be defined with simply add()
    ["add"](a, b) {
    return a + b;
    }
    // this one is dynamically evaluated
    [1 + 2]() {
    return "three";
    }
    }
    let MazdaMPV = new Car("Mazda", "MPV");
    MazdaMPV.add(4, 5); // 9
    MazdaMPV[3](); // "three"
    MazdaMPV[METADATA](); // { make: "Mazda", model: "MPV" }

## 22.8. Xestionando datos privados con clases
    Un dos obstáculos máis comúns que utilizan as clases é atopar o enfoque axeitado para manexar os estados privados. Hai 4 solucións comúns para o manexo de estados privados:
    Usar Symbols
    Os Symbols son un tipo primitivo novo introducido en ES2015, como se define na MDN.
    Un símbolo é un tipo de datos único e inmutable que se pode usar como identificador para as propiedades dos obxectos.
    Ao usar o símbolo como unha chave de propiedade, non é enumerable, polo que non se revelarán usando un bucle for...in in ou Object.keys.
    Así, podemos usar símbolos para almacenar datos privados.
    const topSecret = Symbol('topSecret'); /_ our private key; will only be accessible on the scope of the module file _/
    export class SecretAgent{
    constructor(secret){
    this[topSecret] = secret; // we have access to the symbol key (closure)
    this.coverStory = 'just a simple gardner';
    this.doMission = () => {
    figureWhatToDo(topSecret[topSecret]); // we have access to topSecret
    };
    }
    }

        Debido a que os símbolos son únicos, debemos ter referencia ao símbolo orixinal para acceder á propiedade privada.
        	const agent = new SecretAgent('steal all the ice cream');
        	// ok let's try to get the secret out of him!
        	Object.keys(agent); // ['coverStory'] only cover story is public, our secret is kept.
        	agent[Symbol('topSecret')]; // undefined, as we said, symbols are always unique, so only the original symbol will help us to get the data.

        Pero non é 100% privado; Depende do axente. Podemos usar o método Object.getOwnPropertySymbols para obter os símbolos do obxecto.
        	const secretKeys = Object.getOwnPropertySymbols(agent);
        	agent[secretKeys[0]] // 'steal all the ice cream' , we got the secret.


    	Usando WeakMaps
    	WeakMaps é un novo tipo de obxecto que foi engadido en ES6.
    	O obxecto WeakMap é unha colección de pares chave / valor nos que as claves están referenciadas débilmente. As chaves deben ser obxectos e os valores poden ser valores arbitrarios.
    	A chave nun WeakMap mantense débilmente. Isto significa que, se non hai outras referencias fortes á chave, a recollida de lixo eliminará toda a entrada do WeakMap.
    	A idea é usar o WeakMap, como un mapa estático para toda a clase, para manter cada instancia como clave e manter os datos privados como un valor para a clave de instancia.
    	Así, só dentro da clase teremos acceso á colección WeakMap.
    	Proba o noso axente con WeakMap:
    			const topSecret = new WeakMap(); // will hold all private data of all instances.
    				export class SecretAgent{
    					constructor(secret){
    					topSecret.set(this,secret); /* we use this, as the key, to set it on our 	instance private data */
    						this.coverStory = 'just a simple gardner';
    						this.doMission = () => {
    							figureWhatToDo(topSecret.get(this)); // we have access to topSecret
    						};
    			}
    			}

    	Porque a const topSecret está definida dentro do noso módulo closure e como non o ligamos ás nosas propiedades de instancia, este enfoque é totalmente privado e non podemos chegar ao axente topSecret.

    	Definiir todos os métodos dentro do constructor
    	A idea aquí é simplemente definir todos os nosos métodos e membros dentro do constructor e usar o peche para acceder aos membros privados sen asignalos.
    			export class SecretAgent{
    				constructor(secret){
    					const topSecret = secret;
    					this.coverStory = 'just a simple gardner';
    					this.doMission = () => {
    						figureWhatToDo(topSecret); // we have access to topSecret
    					};
    				}
    			}

    	Neste exemplo tamén os datos son 100% privados e non se poden alcanzar fóra da clase, polo que o noso axente está seguro.

    	Usar convencións de nomes
    	Decidiremos que calquera propiedade privada que estea prefixada con _.
    	Teña en conta que para este enfoque os datos non son realmente privados.
    			export class SecretAgent{
    				constructor(secret){
    					this._topSecret = secret; // it private by convention
    					this.coverStory = 'just a simple gardner';
    					this.doMission = () => {
    						figureWhatToDo(this_topSecret);
    					};
    				}
    			}

##  22.9. Ligando nome de clase
    Vinculación de nome de clase
    	O nome da declaración de clase está ligado de diferentes xeitos en diferentes ámbitos:
    	1. O alcance no que se define a clase - let binding
    	2. O alcance da clase mesma: dentro de {e} na clase {} - const binding
    		class Foo {
    			// Foo inside this block is a const binding
    		}
    		// Foo here is a let binding

    	Por exemplo,
    		class A {
    			foo() {
    				A = null; // will throw at runtime as A inside the class is a `const` binding
    			}
    		}
    		A = null; // will NOT throw as A here is a `let` binding

    	Isto non é o mesmo para unha función
    	function A() {
    		A = null; // works
    	}
    	A.prototype.foo = function foo() {
    		A = null; // works
    	}
    	A = null; // works

## 22.10. Comprobacion de propiedades dun obxecto
Para evitar que se lance un erro cando se accede a unha propiedade pódese utilizar o operator ? para verificala:
```javascript
person = {
  name: "John",
  age: 25,
  address: {
    city: "LA",
    state: "California",
  },
};

// Longhand
console.log(person && person.address && person.address.country); // undefined

// Shorthand
console.log(person?.address?.country); // undefined
```

# 22. ESPAZOS DE NOMES
    23.1. Asignación directa
    Mal, declarar variables ao chou
    //Before: antipattern 3 global variables
    var setActivePage = function () {};
    var getPage = function() {};
    var redirectPage = function() {};

        Establecer espazos de nomes
        	//After: just 1 global variable, no function collision and more meaningful function names
        	var NavigationNs = NavigationNs || {};
        	NavigationNs.active = function() {}
        	NavigationNs.pagination = function() {}
        	NavigationNs.redirection = function() {}

    23.2 Espazos de nomes aniñado
    Cando están implicados varios módulos, evite proliferar nomes globais creando un único espazo de nome global. Dende alí, os sub-módulos pódense engadir ao espazo de nomes global. (A reprodución adicional diminuirá o rendemento e engadirá unha complexidade innecesaria.) Pódense usar nomes máis longos se os enfrontamentos de nome son un problema:
    var NavigationNs = NavigationNs || {};
    NavigationNs.active = {};
    NavigationNs.pagination = {};
    NavigationNs.redirection = {};
    // The second level start here.
    Navigational.pagination.jquery = function();
    Navigational.pagination.angular = function();
    Navigational.pagination.ember = function();

# 23. O CONTEXTO (THIS)
    24.1. this con obxectos simples.
    var person = {
    name: 'John Doe',
    age: 42,
    gender: 'male',
    bio: function() {
    console.log('My name is ' + this.name);
    }
    };
    person.bio(); // logs "My name is John Doe"
    var bio = person.bio;
    bio(); // logs "My name is undefined"

        No código anterior, person.bio fai uso do contexto (this). Cando a función chámase person.bio (), o contexto pasa automaticamente e rexistra correctamente "O meu nome é John Doe". Ao asignar a función a variable aínda que perde o seu contexto.
        En modo non estrito, o contexto predeterminado é o obxecto global (window). En modo estrito está predefinido como undefined.

    24.2. O uso de this para usar en funcións ou obxectos aniñados
    Un fallo común é intentar usalo nunha función aniñada ou nun obxecto, onde se perdeu o contexto.
    document.getElementById('myAJAXButton').onclick = function(){
    makeAJAXRequest(function(result){
    if (result) { // success
    this.className = 'success';
    }
    })
    }

        Aquí perdeuse o contexto (this) na función de devolución de chamada interna. Para corrixir isto, pode gardar o valor desta nunha variable:
        	document.getElementById('myAJAXButton').onclick = function(){
        		var self = this;
        		makeAJAXRequest(function(result){
        			if (result) { // success
        				self.className = 'success';
        			}
        		})
        	}

        ES6 introduciu funcións de frecha que inclúen esta unión léxica. O exemplo anterior podería ser escrito así:
        	document.getElementById('myAJAXButton').onclick = function(){
        		makeAJAXRequest(result => {
        			if (result) { // success
        				this.className = 'success';
        			}
        		})
        	}

    24.3. O contexto da función binding.
    Versión ≥ 5.1
    Cada función ten un método de ligazón bind() , que creará unha función envolta que o chamará co contexto correcto.
    var monitor = {
    threshold: 5,
    check: function(value) {
    if (value > this.threshold) {
    this.display("Value is too high!");
    }
    },
    display(message) {
    alert(message);
    }
    };
    monitor.check(7); // The value of `this` is implied by the method call syntax.
    var badCheck = monitor.check;
    badCheck(15); // The value of `this` is window object and this.threshold is undefined, so value > this.threshold is false
    var check = monitor.check.bind(monitor);
    check(15); // This value of `this` was explicitly bound, the function works.
    var check8 = monitor.check.bind(monitor, 8);
    check8(); // We also bound the argument to `8` here. It can't be re-specified.

        Unión dura
        O obxecto da unión dura é ligar "duro" unha referencia a isto.
        Vantaxe: é útil cando quere protexer obxectos particulares de perderse.
        		function Person(){
        			console.log("I'm " + this.name);
        		}
        		var person0 = {name: "Stackoverflow"}
        		var person1 = {name: "John"};
        		var person2 = {name: "Doe"};
        		var person3 = {name: "Ala Eddine JEBALI"};
        		var origin = Person;
        		Person = function(){
        			origin.call(person0);
        		}
        		Person();
        		//outputs: I'm Stackoverflow
        		Person.call(person1);
        		//outputs: I'm Stackoverflow
        		Person.apply(person2);
        		GoalKicker.com – JavaScript® Notes for Professionals 202
        		//outputs: I'm Stackoverflow
        		Person.call(person3);
        		//outputs: I'm Stackoverflow

    24.4. this no construtor de funcións
    Ao usar unha función como constructor, this ten un binding especial que se refire ao obxecto recentemente creado:
    function Cat(name) {
    this.name = name;
    this.sound = "Meow";
    }
    var cat = new Cat("Tom"); // is a Cat object
    cat.sound; // Returns "Meow"
    var cat2 = Cat("Tom"); // is undefined -- function got executed in global context
    window.name; // "Tom"
    cat2.name; // error! cannot access property of undefined

# 24. SETTERS AND GETTERS
    25.1. Sintaxe estándar
    var setValue;
    var obj = {};
    Object.defineProperty(obj, "objProperty", {
    get: function(){
    return "a value";
    },
    set: function(value){
    setValue = value;
    }
    });

    25.2. Definindo setter e getter nun novo obxecto.
    JavaScript permítenos definir getters e setters sintaxe literal dos obxectos. Aquí tes un exemplo:
    var date = {
    get date(){

        	},
        	set date(d){

        	}
        }

    25.3. Definindo setters e getters nunha clase ES6
    Exemplo de código
    class Person {
    constructor(firstname, lastname) {
    this.\_firstname = firstname; // privado
    this.\_lastname = lastname; // privado
    }
    get firstname() {
    return this.\_firstname;
    }
    set firstname(name) {
    this.\_firstname = name;
    }
    get lastname() {
    return this.\_lastname;
    }
    set lastname(name) {
    this.\_lastname = name;
    }
    }

# 25. EVENTOS
    26.1. Páxina, DOM, e carga de navegador.

        no codigo html
        <body onload="someFunction()">
        <img src="image1" />
        <img src="image2" />
        </body>
        <script>
        function someFunction() {
        console.log("Hi! I am loaded");
        }
        </script>

        no script js
        document.addEventListener("DOMContentLoaded", function(event) {
        	console.log("Hello! I am loaded");
        });

        función auto invocada
        	(function(){
        		console.log("Hi I am an anonymous function! I am loaded");
        	})();

# 26. HERDANDANZA
    27.1. Estándar co prototipo

        	function Foo (){}
        	Foo.prototype.bar = function() {
        		return 'I am bar';
        	};

    27.2. Diferenza entre object.key e object.prototype.key
    As instancias só herdan de prototipos.

    27.3. Herdanza prototípica

    27.4. Herdana pseudo-clase

    27.5. Establecendo o prototypo dun obxecto

# 27 . ENCADEAMENTO DE MÉTODOS
    28.1. Deseñeo de obxecto encadenables e encadeamento
    28.2. Encadeamento de métodos

# 28. CALLBACKS
    29.1. Exemplos de usos de callback simple
    Os callbacks ofrecen un xeito de estender a funcionalidade dunha función (ou método) sen cambiar o seu código. Este enfoque a miúdo úsase en módulos (bibliotecas / plugins), cuxo código non debería ser modificado.
    Supoña que escribimos a seguinte función, calculando a suma dunha determinada matriz de valores:
    function foo(array) {
    var sum = 0;
    for (var i = 0; i < array.length; i++) {
    sum += array[i];
    }
    return sum;
    }

        Supoña agora que queremos facer algo con cada valor da matriz, p.ex. amosarllo usando a alert(). Poderiamos facer os cambios apropiados no código de foo, así:
        	function foo(array) {
        		var sum = 0;
        		for (var i = 0; i < array.length; i++) {
        			alert(array[i]);
        			sum += array[i];
        		}
        		return sum;
        	}

        Pero, se decidimos usar console.log no canto de alert()? Evidentemente cambiar o código de foo, sempre que decidimos facer algo con cada valor, non é unha boa idea. É moito mellor ter a opción de cambiar de idea sen cambiar o código de foo. Isto é exactamente o caso dos devanditos callbacks. Só debemos cambiar ligeramente a sinatura e o corpo de foo:
        	function foo(array, callback) {
        	var sum = 0;
        		for (var i = 0; i < array.length; i++) {
        			callback(array[i]);
        			sum += array[i];
        		}
        		return sum;
        	}

        E agora somos capaces de cambiar o comportamento de foo só cambiando os seus parámetros:
        	var array = [];
        	foo(array, alert);
        	foo(array, function (x) {
        		console.log(x);
        	});

        Exemplos con funcións asíncronas
        En jQuery, o método $.getJSON() para obter datos JSON é asíncrono. Polo tanto, o paso de código nunha devolución de chamada asegura que se chama o código despois de obter o JSON.

        Sintaxe de $.getJSON():
        	$.getJSON( url, dataObject, successCallback );

        Exemplo de uso:
        	$.getJSON("foo.json", {}, function(data) {
        		// data handling code
        	});

        O seguinte non funcionaría, xa que probablemente se chamaría o código de xestión de datos antes de que se reciban os datos, porque a función $.getJSON toma un tempo non especificado e non mantén a pila de chamadas mentres espera o JSON.
        	$.getJSON("foo.json", {});
        	// data handling code

        Outro exemplo dunha función asíncrona é a función de animación () de jQuery. Porque leva unha determinada hora para executar a animación, ás veces é desexable executar algún código directamente despois da animación.
        .animate() syntax:
        	jQueryElement.animate( properties, duration, callback );

        Por exemplo, para crear unha animación de desvanecemento despois do cal o elemento desaparece completamente, o seguinte código pode ser executado. Teña en conta o uso da devolución de chamada.
        	elem.animate( { opacity: 0 }, 5000, function() {
        		elem.hide();
        	} );

        porque este último non espera que o animado () (unha función asíncrona) se complete e, polo tanto, o elemento está oculto inmediatamente, producindo un efecto non desexado.

    29.2. Continuación (síncrono e asíncrono)
    Os callbacks se poden usar para executar código unha vez completado un método ou de forma asíncrona.

    29.3. Que é un callback?

    29.4. Callbacks e this
    A miúdo cando se usa un callback se quere acceder a un contexto específico:
    function SomeClass(msg, elem) {
    this.msg = msg;
    elem.addEventListener('click', function() {
    console.log(this.msg); // <= will fail because "this" is undefined
    });
    }
    var s = new SomeClass("hello", someElement);

        Solucións
        - usar bind
        	function SomeClass(msg, elem) {
        		this.msg = msg;
        		elem.addEventListener('click', function() {
        			console.log(this.msg);
        		}.bind(this)); // <=- bind the function to `this`
        	}
        - usar funcións de frecha
        	function SomeClass(msg, elem) {
        		this.msg = msg;
        		elem.addEventListener('click',() => { // <=- arrow function binds `this`
        			console.log(this.msg);
        		});
        	}

        Moitas veces desexa chamar a un membro da función, idealmente pasando os argumentos que se pasaron ao evento na función.

        Solucións
        - usar bind
        	function SomeClass(msg, elem) {
        		this.msg = msg;
        		elem.addEventListener('click', this.handleClick.bind(this));
        	}
        	SomeClass.prototype.handleClick = function(event) {
        		console.log(event.type, this.msg);
        	};

        - usar arrow functions
        	function SomeClass(msg, elem) {
        		this.msg = msg;
        		elem.addEventListener('click', (...a) => this.handleClick(...a));
        	}
        	SomeClass.prototype.handleClick = function(event) {
        		console.log(event.type, this.msg);
        	};

        - implementar EventListener, para elementos do DOM
        	function SomeClass(msg, elem) {
        		this.msg = msg;
        		elem.addEventListener('click', this);
        	}
        	SomeClass.prototype.handleEvent = function(event) {
        		var fn = this[event.type];
        		if (fn) {
        			fn.apply(this, arguments);
        		}
        	};
        	SomeClass.prototype.click = function(event) {
        		console.log(this.msg);
        	};

    29.5. Callback usando arrow function.
    Reducir código
    Isto
    [1,2,3,4,5].forEach(function(x){
    console.log(x);
    }
    pasa a isto
    [1,2,3,4,5].forEach(x => console.log(x));

    29.6. Captura de erros e ramificación con control de fluxo.
    Pódese usar os callback para controlar o fluxo:
    const expected = true;
    function compare(actual, success, failure) {
    if (actual === expected) {
    success();
    } else {
    failure();
    }
    }
    function onSuccess() {
    console.log('Value was expected');
    }
    function onFailure() {
    console.log('Value was unexpected/exceptional');
    }
    compare(true, onSuccess, onFailure);
    compare(false, onSuccess, onFailure);
    // Outputs:
    // "Value was expected"
    //

# 29. INTERVALOS E TIMEOUTS
    30.1. setTimeout recursivo
    Truco
    function repeatingFunc() {
    console.log("It's been 5 seconds. Execute the function again.");
    setTimeout(repeatingFunc, 5000);
    }

    30.2. Intervalos
    window
    function waitFunc(){
    console.log("This will be logged every 5 seconds");
    }
    window.setInterval(waitFunc,5000);

    30.3. Intervalos
    Estándar
    var int = setInterval("doSomething()", 5000 ); /_ 5 seconds _/

        Sen superposición
        (function(){
        	doSomething();
        	setTimeout(arguments.callee, 5000);
        })()

    30.4. Eliminando intervalos.
    Mediante o obxecto global. window.setTimeOut devolve un Id.
    function waitFunc(){
    let i = 1;
    console.log(i, "This will be logged every 5 seconds");
    i++;
    }
    var interval = window.setInterval(waitFunc,500);
    window.setTimeout(function(){
    clearInterval(interval);
    },3200);

    30.5. Eliminando timeouts
    clearTimeout();

    30.6. setTimeout, orde de operacións, clearTimeout
    Problemas con setTimeout

# 30. EXPRESIÓNS REGULARES
    Flags Detalles
    g global: todas as coincidencias (non a primeira)
    i insensitive. ignora a/A
    m multiliña: ^ e \$ casan con principio/final da liña. (non da string)
    u unicode: os modelos son tratados como UTF-16
    y sticky (pegañento). coincidencias consecutivas

    Modificadores

    -     	un ou mais caracteres


    31.1	Creación de regex
    	Estándar
    	var re = new RegExpr("regex", "flags");

    	inicialización estática
    	var re = /regex/flags;

    31.2. Flags

    32.3. .test()
    	Comprobando se contén o modelo
    		var re = /[a-z]+/; //
    		if (re.test("foo")) {
    			console.log("Match exists.");
    		}

    32.4. .exec()
    	devolve un array de coincidencias,

    33.5. Métodos con strings
    	.match()	devolve arrays de coincidencias
    	.replace()  reempraza a coincidencia co modelo
    	.split() 	divide o string coa coincidencia
    	.search() 	devolve o índice da coincidencia

    31.6. Grupos RegExp
    	JavaScript admite varios tipos de grupos nas súas expresións regulares, grupos de captura, grupos que non son de captura e miradas. Actualmente, non hai soporte para buscar.

    	Captura
    	Ás veces, a coincidencia desexada depende do seu contexto. Isto significa que unha RegExp simple localizará varias coincidencias da cadea que é de interese, polo que a solución é escribir un grupo de captura (patrón). Os datos capturados pódense referenciar
    	como ...
    		- Substitución de cadeas "$ n" onde n é o nº grupo de captura (a partir de 1)
    		- O nº argumento nunha función de devolución de chamada
    		- Se o RegExp non está marcado g, o n + 1 ª elemento dun array devolto por .match()
    		- Se o RegExp está marcado g, .match() descarta capturas, usa re.exec no seu lugar

    	Hai Dicir que hai unha cadea onde todos os signos + deben ser substituídos por un espazo, pero só se seguen un carácter de letra. Isto significa que unha combinación simple incluiría ese carácter de leta e tamén se eliminaría. A captura é a solución
    	isto significa que se pode conservar a carta correspondente.
    		let str = "aa+b+cc+1+2",
    		re = /([a-z])\+/g;
    		// String replacement
    		str.replace(re, '$1 '); // "aa b cc 1+2"
    		// Function replacement
    		str.replace(re, (m, $1) => $1 + ' '); // "aa b cc 1+2"

    	Non-captura
    	Empregando o formulario (?: Pattern), funcionan dun xeito semellante para capturar grupos, agás que non almacenan o contido do grupo despois da coincidencia.
    	Poden ser particularmente útiles se se capturan outros datos dos que non quere mover os índices, pero ten que facer algunhas combinacións avanzadas de patróns, como un OR
    		let str = "aa+b+cc+1+2",
    		re = /(?:\b|c)([a-z])\+/g;
    		str.replace(re, '$1 '); // "aa+b c 1+2"

    	Mirar para adiante
    	Se a coincidencia desexado depende de algo que o segue, no canto de coincidir con iso e capturalo, é posible usar unha mirada para probalo pero non incluílo na coincidencia. Unha mirada positiva ten a forma (? = pattern), a cara adiante negativa (onde a expresión coincide só se o patrón de avance non coincide) ten o formulario (patern?!)
    		let str = "aa+b+cc+1+2",
    		re = /\+(?=[a-z])/g;
    		str.replace(re, ' '); // "aa b cc+1+2"

# 32. COOKIES
    31.1. Comprobar cookies habilidadas
    if (navigator.cookieEnabled === false)
    {
    alert("Error: cookies not enabled!");
    }

    32.2. Agregando e seteando coockies.
    var COOKIE*NAME = "Example Cookie"; /* The cookie's name. _/
    var COOKIE_VALUE = "Hello, world!"; /_ The cookie's value. _/
    var COOKIE_PATH = "/foo/bar"; /_ The cookie's path. _/
    var COOKIE_EXPIRES; /_ The cookie's expiration date (config'd below). \_/

        /* Set the cookie expiration to 1 minute in future (60000ms = 1 minute). */
        COOKIE_EXPIRES = (new Date(Date.now() + 60000)).toUTCString();
        document.cookie +=
        COOKIE_NAME + "=" + COOKIE_VALUE
        + "; expires=" + COOKIE_EXPIRES
        + "; path=" + COOKIE_PATH;

    32.3. Lendo cookies
    var name = name + "=",
    cookie_array = document.cookie.split(';'),
    cookie_value;
    for(var i=0;i<cookie_array.length;i++) {
    var cookie=cookie_array[i];
    while(cookie.charAt(0)==' ')
    cookie = cookie.substring(1,cookie.length);
    if(cookie.indexOf(name)==0)
    cookie_value = cookie.substring(name.length,cookie.length);
    }

    32.4. Eliminando cookies
    var expiry = new Date();
    expiry.setTime(expiry.getTime() - 3600);
    document.cookie = name + "=; expires=" + expiry.toGMTString() + "; path=/"

# 32. WEB STORAGE
    33.1. Usando localStorage
    versión longa
    localStorage.setItem('name', "John Smith");
    localStorage.getItem('name'); // "John Smith"
    localStorage.removeItem('name');

    33.2. versión curta
    localStorage.name = "John Smith";
    localStorage.name;
    delete localStorage.name.

    33.3. Gardando eventos
    Sempre que se establece un valor en localStorage, un evento de almacenamento será enviado en todas as outras xanelas do mesmo orixe. Isto pódese usar para sincronizar o estado entre diferentes páxinas sen recargar nin comunicar cun servidor. Por exemplo, podemos reflectir o valor dun elemento de entrada como texto de parágrafo noutra ventá.

    33.4. sessionStorage
    O obxecto sessionStorage implementa a mesma interface de almacenamento que localStorage. Non obstante, no canto de ser compartido con todas as páxinas do mesmo orixe, os datos de sessionStorage almacénanse por separado para cada ventá / guía. Os datos almacenados persisten entre as páxinas desa ventá / guía mentres estea aberta, pero é visible en ningún outro lugar.

    33.5. localStorage length

    33.6. condidións de erro
    A maioría dos navegadores, cando están configurados para bloquear as cookies, tamén bloquearán o almacenamento local. Os intentos de usalo producirán unha excepción. Non esqueza xestionar estes casos.

    33.7. localStorage.clear()

# 33. ATRIBUTOS DE DATOS (DATA)
    34.1. Accedendo aos atributos de datos
    Propiedade datase. data-
    item.dataset.id

# 34. JSON
    JSON.parse
    JSON.stringify

        var json = {
        "string": "string",
        "number": 1.3,
        "null": null,
        "obj" : {"key": "value"},
        "array": [1,2,3,4]
        }

# 35. AJAX
    AJAX significa "JavaScript asíncrono e XML". Aínda que o nome inclúe XML, JSON úsase máis a miúdo debido ao seu formato máis sinxelo e menor redundancia. AJAX permite ao usuario comunicarse con recursos externos sen recargar a páxina web.

    36.1. Enviando e recibindo dato JSON vía POST
    Versión ≥ 6
    O método fetch() require inicialmente promesas que obxectos Response. Isto proporcionará información de cabeceira de resposta, pero non inclúe directamente o corpo de resposta, que pode que nin sequera cargou. Os métodos do obxecto Response como .json () pódense usar para agardar a que o corpo de resposta se cargue e analizar.
    const requestData = {
    method : 'getUsers'
    };
    const usersPromise = fetch('/api', {
    method : 'POST',
    body : JSON.stringify(requestData)
    }).then(response => {
    if (!response.ok) {
    throw new Error("Got non-2XX response from API server.");
    }
    return response.json();
    }).then(responseData => {
    return responseData.users;
    });
    usersPromise.then(users => {
    console.log("Known users: ", users);
    }, error => {
    console.error("Failed to fetch users due to error: ", error);
    });

    36.2. Engan

# 36. ENUMERACIÓNS
    JS non soporta enumerados. A alternativa é usar as propiedades dun obxecto:
    var ColorsEnum = {
    WHITE: 0,
    GRAY: 1,
    BLACK: 2
    }
    // Define a variable with a value from the enum
    var currentColor = ColorsEnum.GRAY;

    37.4. Usando Symbols.
    Os Symbols son datos únicos, inmutable e de valores primitivos.
    const Regnum_Animale = Symbol();

# 37. MAP
    Parametro Detalles
    interable Calquera obxecto iterable
    key key do elemento
    value valor asignado
    callback función de callback que recibe value, key e o mapeo
    thisArg valor que se usar como this cando se executa o callback.

    38.1. Creando un Mapeo (Map)
    Un mapa é un mapo de key a valores.

    38.2. Limpando un map
    map.clear()

    38.3. Eliminando un elemento do Map
    map.delete(key)

    38.4. Comprabando se existe unha key
    map.has(key)

    38.5. Iterando Map.
    Hai tres métodos que devolven iteradores: .keys(), .values() e .entries(), este é por defecto.
    Tamén admite .forEach(value, key, theMap).

# 38. TIMESTAMPS
    39.1. Timestamps e alta resolución
    performance.now()
    Agora
    (new Date).getTime()
    Date.now()

# OPERADORES UNARIOS.
    40.2. Operador typeof
    Devolve un string

    40.3. Operador delete
    Elimina unha propiedade dun obxecto
    delete localStorage.customProperty;

    40.4. Operador +
    aritmético de suma

    40.5. Operador void
    void 0 devolve undefined

    40.6. Operador de negación - arimética
    number

    40.7. Operador de negación bitwise NOT ~
    Invirte os valores dos bit

    40.8. Operador de negación lóxica NOT !
    invirte o valor lóxico

29. XERADORES
    As funcións xeradoras (denotadas function\* keyword) corren como corrutinas, xerando unha serie de valores que serán requeridos a través de un iterador.

    41.2. Enviando valores a un xenerador.
    Pódese pasarlle un valor como parámetro de .next();

    41.3. Delegando noutro xerador.
    Adminte a recursividade.

    41.4. Iteración.
    Pode ser incluído dentro dun bucle for...of.

    41.5. Fluxo asíncrono con xerarods.
    Permite emuar funcións asíncrona.

    41.6. Interface iterador-observador

30. PROMESAS
    42.1. Introdución
    Un obxecto Promise representa unha operación que produciu ou pode producir un valor. As Promise fornecen dun xeito robutos de envolver o resultado (posiblemente pendente) dunha tarefa asíncrona, mitigando o problema dos callbacks aniñados profundamente (coñecido como o "inferno do callback")

        Estados e controls de fluxo
        Unha promesa pode estar nun destes estados:
        	- pending (pendente). A operación subxacente aínda non se completou e a promesa está pendente de cumprirse.
        	- fullfilled (cumprida). A operación rematous e a promesa está cumprida cumprida cun valor. Isto é análogo a retornar un valor cunha función síncrona.
        	- rejected (rexeitada). Ocorreu un erro durante a operación e a promesa está rexeitada cunha razón. Isto é análogo a lanzar un error cunha función síncrona.

        Dise que a promesa está settled ( ou resolved  - resolta) cando está cumprida ou rexeitada. Unha vez que está resolta, convértes en inmutable, e o seu estado non pode cambiar. Os métodos .then() e .catch() poden usarse para xuntar o callback cando a promesa está resolta. Estes callbacks son invocados co valor de cumprimento ou coa razón de rexeitamento, respectivamente.

        Declaración de promesa:

        	const promise = new Promise ((resolve, reject)=>{
        		// tarefa asíncrona que devolve un value
        		if (value){
        			resolve(value);
        		}else{
        			let reason = new Error(message);
        			reject(reason);
        			throw reason;
        		}
        	});

        Chamada á promesa
        	promise.then(value => {
        		// facer algo co valor, por exemplo
        		res.status(200).send(value);
        	}).catch(reason => {
        		res.status(500).send(reason);

        	});

        Esta maneira de chamar a promesa nomesmo método pode probocar unha excepcion Uncaught
        exception in Promise ou na execución da promesa ou dentro dun dos callbacks, poque que se prefire a vía de achegar o seguinte listener devolta polo then/catch previo.

        Alternativamente, pódese chamar a ambos callbas nun then simple:

        	promise.then(onFulfilled, onRejected);


    	Anexar callbacks a unha promesa que xa foi settled (resolta), ponos nunha cola de microtarefas e seran chamados cando antes (i.e. despois de executado o script). Non é necesario comprobar o estado da promesa despois de anexar os callbacks, a diferenza de moitos emisores de enventos.

    42.2. Encadeamento de promesas
    	O método then() devolve unha nova promesa. O método catch() permite encadearle un then() e o bloque funciona como un try-catch

    	En certas ocasións, pode querer "ramificar" a execución das funcións. Pode facelo devolvendo promesas diferentes dunha función dependendo da condición. Máis tarde no código, pode combinar todas estas ramas nun para chamar a outras funcións nelas ou manexar todos os erros nun mesmo lugar.

    		promise
    				.then(result => {
    					if (result.condition) {
    						return handlerFn1()
    							.then(handlerFn2);
    					} else if (result.condition2) {
    						return handlerFn3()
    							.then(handlerFn4);
    					} else {
    						throw new Error("Invalid result");
    					}
    				})
    				.then(handlerFn5)
    				.catch(err => {
    					console.error(err);
    				});

    		Así a orde de exueción das funcións será como:

    		promise --> handlerFn1 -> handlerFn2 --> handlerFn5 ~~> .catch()
    				|							 ^
    				V 							 |
    				-> handlerFn3 -> handlerFn4 -^

    		O catch capturará o erro en calquera ramo onde ocorrer.

    42.3. Agardando por promesas concorrentes múltiples.
    	O método estático Promise.all () acepta un iterable (por exemplo, unha matriz) de promesas e devolve unha nova promesa, que se resolve cando todas as promesas no iterable resolveron ou rexeitan se polo menos unha das promesas no iterable foi rexeitada.

    42.4. Reducion un array a una cadea de promesas

    	A redución con then

    	Esta variante do patrón constrúe unha cadea .then () e pode usarse para encadear animacións ou facer unha secuencia de solicitudes HTTP dependentes.
    		[1, 3, 5, 7, 9].reduce((seq, n) => {
    			return seq.then(() => {
    				console.log(n);
    				return new Promise(res => setTimeout(res, 1000));
    			});
    		}, Promise.resolve()).then(
    			() => console.log('done'),
    			(e) => console.log(e)
    		);
    		// will log 1, 3, 5, 7, 9, 'done' in 1s intervals

    	A redución con catch
    		var working_resource = 5; // one of the values from the source array
    		[1, 3, 5, 7, 9].reduce((seq, n) => {
    			return seq.catch(() => {
    				console.log(n);
    				if(n === working_resource) { // 5 is working
    					return new Promise((resolve, reject) => setTimeout(() => resolve(n), 1000));
    				} else { // all other values are not working
    					return new Promise((resolve, reject) => setTimeout(reject, 1000));
    				}
    			});
    		}, Promise.reject()).then(
    			(n) => console.log('success at: ' + n),
    			() => console.log('total failure')
    		);
    		// will log 1, 3, 5, 'success at 5' at 1s

    42.5. Agardando pola primeira de varias promesas concorrentes

    42.6. "promisificando" funcions con callbacks.
    	Dada un función
    		fooFn(options, function callback(err, result) { ... });

    	podemos promisificala
    		function promiseFooFn(options) {
    			return new Promise((resolve, reject) =>
    				fooFn(options, (err, result) =>
    					// If there's an error, reject; otherwise resolve
    					err ? reject(err) : resolve(result)
    				)
    			);
    		}

    42.7. Capturando error.
    	Na promesa lánzase o error on throw e capturase con catch.

    42.8. Unindo operacións síncronas e asíncronas
    	Nalgúns casos pode querer axustar unha operación síncrona dentro dunha promesa de evitar a repetición nas ramas de código. Tome este exemplo:

    		if (result) { // if we already have a result
    			processResult(result); // process it
    		} else {
    			fetchResult().then(processResult);
    		}

    	As ramas síncronas e asíncronas do código anterior poden conciliarse envolvendo de xeito redundante o funcionamento síncrono dentro dunha promesa:

    		var fetch = result ? Promise.resolve(result) : fetchResult();
    		fetch.then(processResult);

    	Cando capturamos o resultado dunha chamada asíncrona, é preferible gardar a promesa en lugar do resultado en si. Isto garante que só se require unha operación asíncrona para resolver varias solicitudes paralelas.

    	Hai que ter coidado de invalidar os valores gardados na caché cando se atopen condicións de erro.
    		// A resource that is not expected to change frequently
    		var planets = 'http://swapi.co/api/planets/';
    		// The cached promise, or null
    		var cachedPromise;
    		function fetchResult() {
    			if (!cachedPromise) {
    				cachedPromise = fetch(planets)
    					.catch(function (e) {
    						// Invalidate the current result to retry on the next fetch
    						cachedPromise = null;
    						// re-raise the error to propagate it to callers
    						throw e;
    					});
    			}
    			return cachedPromise;
    		}

    42.9. Retransando a chamada da función
    	Usamos setTimeout();

    42.10. Promisificando valores
    	O metodo estático Promise.resolve() pode usarse para envolver valores dentro de promesas.

    42.11. ES2017 async /await

    42.12. finally()
    	Proposta de usar finally() como método final

    42.13. forEach con promesas
    	Pode usarse un forEach sobre un iterable para que devolve unha promesa con cada elemento.

    42.14. Petición asíncrona a una API

    	Exemplo simple
    		var get = function(path) {
    			return new Promise(function(resolve, reject) {
    				let request = new XMLHttpRequest();
    				request.open('GET', path);
    				request.onload = resolve;
    				request.onerror = reject;
    				request.send();
    			});
    		};

    	Capturando o erro

    		request.onload = function() {
    			if (this.status >= 200 && this.status < 300) {
    				if(request.response) {
    					// Assuming a successful call returns JSON
    					resolve(JSON.parse(request.response));
    				} else {
    					resolve();
    			} else {
    				reject({
    					'status': this.status,
    					'message': request.statusText
    				});
    			}
    		};
    		request.onerror = function() {
    			reject({
    				'status': this.status,
    				'message': request.statusText
    			});
    		}

31. SET (CONXUNTOS)
    Colección desordenada de elementos únicos.

    43.1. Creación
    const set = new Set();

    43.2. Engadindo un valor
    set.add(element)

    43.3. Eliminado un elemento
    set.delete(element)

    43.4. Comprobando un elemento
    set.has(element)

    43.5. Limpando un conxunto
    set.clear()

    43.6. Obtendo a lonxitude
    set.size()

    43.7. Convertindoo nun array
    const array = Array.from(set)
    ou
    const array = [...set]

    43.8. Intersección e diferenzas
    const intersección (elementos comúns) = new Set(Array.form(set1).filter(x => set2.has(x)));
    const diferenza (elementos non comúns) = new Set(Array.form(set1).filter(x => set2.has(x)));

    43.9. Iteración de elementos
    Bucle for-of

32. MODALS PROMPTS
    alert(message)
    confirm(message)
    prompt(message, defaultValue)

33. EXECCOMMAND E CONTENTEDITABLE
    45.1. Escoitando os cambios en contenteditable

34. HISTORY
    Obxecto global history.

35. OBXECTO NAVEGADOR

36. BOM (MODELOS DE OBXECTO DE NAVEGADOR)
    48.1. Introdución
    Obxecto que representa a fiestra do navegador e os compoñentes.
    window.
    document. representa a web actual.
    history. representa as páxinas na historia do navigador.
    location. representa a url da páxina actual.
    navitagor. representa a información sobre o navegador.
    screen. representa inforomación sobre o dispositivo.

    48.2. Propiedades de window.

    42.3. Métodos de window.

37. O CICLO DE EVENTOS
    49.1. O ciclo de eventos nun navigador web.
    A gran maioría dos entornos JavaScript modernos funcionan segundo un ciclo de eventos. Este é un concepto común na programación de computadores que significa esencialmente que o seu programa agarda continuamente por cousas novas e, cando o fan, reacciona a elas. O ambiente do host chama ao teu programa, xerando un "retorno" ou "tick" ou "tarefa" no ciclo de eventos, que logo executa ata a conclusión. Cando remate ese xiro, o ambiente anfitrión agarda algo máis para acontecer antes de que todo comece.

    49.2. Operacións asíncronas e ciclor de eventos
    Os eventos son asíncronos.
    Como funciona isto é que cando estas instrucións se executan, din ao entorno host (é dicir, o navegador ou o tempo de execución de Node.js, respectivamente) que se apaguen e fagan algo, probablemente noutro fío. Cando o ambiente anfitrión está feito facendo isto (respectivamente, agardando 100 milisegundos ou lendo o ficheiro file.txt) publicará unha tarefa no ciclo de eventos dicindo "chamar á devolución de chamada que se me deu anteriormente con estes argumentos".
    O ciclo de eventos está ocupado facendo a súa cousa: renderizar a páxina web, escoitar a entrada do usuario e buscar continuamente tarefas publicadas. Cando ve estas tarefas publicadas para chamar á devolución de chamadas, devolverá o JavaScript. Así é como obter un comportamento asíncrono.

38. MODO ESTRITO
    Pode ser marcado para scripts ou para funcións. - Evita eliminar propiedades non borrables. - Evita estender propiedades non extendibles. - Cambiar propiedades global. - Cando se accede a unha variable non declarada dá erro. - Non permite duplicar funcións. - As funcións locais son inacccesibles fóra do bloque.

39. ELEMENTOS PERSONALIZADOS
    options.extends
    options.prototype

40. MATIPULACIÓN DE DATOS
    52.1. Formateo de número como moeda.

41. DATOS BINARIOS

42. TEMPLATE LITERALS

43. FETCH
    Método que realiza unha petición http

44. SCOPE
    56.1. Closures

    56.3. var e let

45. MÓDULOS

## BOAS PRÁCTICAS
### Recursión



## LIBRERÍAS

1. **Express**. Levanta servidores web.
2. **Socket.io**. Habilita un sockect bidireccional basado en eventos.
3. **Body-parser**. Middleware que parsea o body das peticións.
4. **Cors**. Middleware que xestiona as cors.
5. **Passport**. Librería para xestionar a autentificación.
6. **Multer**. Xestiona subida de ficheiros.
7. **Axios**. Xestiona peticións _ajax_.
8. **Morgan**. Middleware para log en _node.js_.
9. **Http-errors**. Crea erros para varios framworks.
10. **Dotenv**. Cargar as variables de entorno desde un ficheiro.
11. **Faker**. Proporciona datos falsos.
12. **Nodemailer**. Envía correos desde _node.js_.
13. **Sequelize**. ORM para SQL basado en promesas.
14. **Moongoose**. ORM para MongoDB.
15. **Jest**. Entorno para testing.
16. **Moment**. Xestion de datas.
17. **Lodash**. Xestion de estrura de datos.
18. **Chalk**. Colorea a presentación da consola.
19. **Validator**. Librería de validadores e sanitizadores.
20. **Cheerio**. Parsea texos de marcado como html.
21. **JSDoc**.  Xerador de documantacion para JS.
22. **Helmet**. Asegura Express seteando varias cabeceiras HTTP.
23. **Crypto-js**. Librería para criptografía. 




# NOVIDADES ES2020	
## globalThis

A variable `globalThis` é un alias do obxecto global independentemente do entorno. Será `window` para un navegador, `global` en Node e `self` en web workers.

## Promise.allSettled
A función `Promise.allSettled()` úsase cando hai múltiples promesas para comprobar se están `decididas` (settled), cando todas están resoltas ou rexeitadas.

## Optional chaining
A `optional chaining` é unha técnica que asegura o acceso seguro a unha propiedade dun obxecto. Cando a propiedade é `null` ou `undefined` devolve `undefined` ou o seu valor. 
O 

```javascript
const user = { name: "Alexandre", age: 20}

user.car.model // Erro,
user?.car?.model // undefined (non erro)
user?.age // 19
```

Tamén se pode usar con métodos. Só hai que engadir o operador ?. antes do parénteses da chamada ao método.

```javascript
const person = {
  name: "Mehdi",
  age: 19,
  fullName(){
   return "Mehdi Aoussiad";
  }
}
person.lastName(); //Error.
person.lastName?.(); //undefined(no error).
person.fullName?.(); //Mehdi Aoussiad
```

## BigInt

É un novo tipo de dato (diferente de number) para xestionar números enteiros grandes. Con este número pódese xestionar números maiores que Number.MAX_SAFE_INTEGER.

# PROTIPOS

Os prototipos son a base da POO en JS. 
Todos os obxectos (classes, objects, variables, functions) teñen o seu prototipo.
Un prototipo é un mecanismo mediante o que un obxecto herda as súas características do pai. O prototipo primitivo é o Object.

Para crear un prototipo úsase una función construtora, que leva o nome o obxecto que vai crear en maiúsculas:

``` Javascript
function Animal(params){
	this.params = params;
	this.doAnything(){}
}
const animal1 = new Animal;
```

O habitual era deixar os atributos na función construtora e reservar os métodos para os prototipos:

``` Javascript
Animal.prototype.doAnything() = function (){...};
```

Para simular a herdanza na función constructora introdúcese un campo convencional `super`con referencia ao obxecto pai

``` Javascript
function Dog (paramsSuper, params){
	this.super = Animal;
	this.super(paramsSuper);
	this.params = params;
}
```

Despois hai que programar o fillo como instancia do pai:

``` Javascript
Dog.prototype = new Animal();
Dog.prototype.constructor = Dog;
```

Sobreescritura dun método do pai:
``` Javascript
Dog.prototype.doAnything() = function (){ /* particular implementation*/}; 
```

Novo método
``` Javascript
Dog.prototype.doAnotherThing() = function (){...};
```

# REFERENCIAS

[One line functions](https://javascript.plainenglish.io/27-essential-one-line-javascript-functions-used-by-developers-daily-2cda9826700e)
