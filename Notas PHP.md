# NOTAS PHP

## 0. XENERALIDADES

Os ficheiros teñen que estar un servidor web. Fóra del non funcionan. Teñen a extensión `.php`. O código vai precedido da etiqueta `<?php`.
Os comentarios poden ser:

`// monoliña`
`# monoliña`
`/* multiliña */`
`/** documentación */`
`<?= ""?>` atallo de echo


Includes
Permiten invocar outros ficheiros

include 'path';
include_once 'path': non inclúe un ficheiro xa incluído.
require 'path': bloquea a execución en caso de erro.
require_once 'path': non inclúe un ficheiro xa incluído.

## 1. VARIABLES E TIPOS DE DATOS

As variables decláranse usaando o signo do dólar. O estilo preferente é _snake_camel_:
`$nome_de_variable = "valor";`

Os tipos de datos son os seguintes:

* *Boolean*. Valor booleano *true* ou *false*
* *Integer*. Valor numérico enteiro.
* *Double*. Valor numérico que adminte valores decimais.
* *String*. Valor de texto de conxunto de caracteres.
* *Array*. Valor de conxunto de variables.
* *Object*. Valor de obxecto.
* *Null*. Valor nulo.
* *Uknow*. Valor descoñecido.

Declaración de constantes co método `define(NOME_DA_CONSTANTE, $valor_da_constante)`.
Existen os seguintes métodos:
`gettype($var);`: devolve o tipo de dato.
`settype($var, "tipo");`: establece o tipo de dato.
`is_integer();`:
`is_double();`:
`is_string();`:

Hai 3 ámbito para a variables:
Superglobais
Son variables nativas da linguaxe.
de servidor
`$_SERVER['SERVER_ADDR']`
`$_SERVER['SERVER_NAME']`
`$_SERVER['SERVER_SOFTWARE']`
`$_SERVER['HTTP_USER_AGENT']`
`$_SERVER['USSER_ADDR']`

de petición
`$_GET['nome_do_parametro']`.
`$_POST['nome_do_parametro']`
`$_REQUEST['nome_do_parametro']`

Globais
Decláranse fóra dunha función e están disponibles en todo o script. Pode chamarse desde calquera punto dentro del, incluíndo alcances aniñados.

Locais
Decláranse dentro dunha función e só están disponibles dentro desta.

## 2. OPERADORES

Aritméticos: suma (`+`), resta (`-`), produto (`*`), división (`/`), resto ou módulo (`%`).
Incremento: pre (`++$var`), post (`$var++`).
Decremento: pre (`--$var`), post (`$var--`).
Asignación: simple (`=`), combinados(`+=`, `-=`, `*=`, `/=` e `%=`).
De comparación: igualdade - compara por valor: (`==`), identidade - compara por valor e tipo (`===`), distinto valor (`!=`, `<>`), non idéntico (`!==`), maior que (`>`), maior ou igual que (`>=`), menor que (`<`), menor ou igual que (`<=`).
Lóxicos: copulativo (`AND`, `&&`), discuntivo (`OR`, `||`), negación (`NOT`, `!`)

## 3. ESTRUTURAS DE CONTROL CONDICIONAIS
if, else if, else

```php
if (condición){
  //sentenzas
} else if {
  //sentenzas
} else {
  //sentenzas
}
```

switch

```php
switch ($variable){
  case valor:
    // sentenzas
    break;
  default:
}
```

## 4. ESTRUTURA DE CONTROL DE ITERACIÓN
while

```php
while(condición){
  //sentenzas.
  // debe incluir unha instrución que xestione a fin do bucle.
}
```
do-while

```php
do{
  // sentenzas
} while (condición)
```

for clásico
```php
for (inicialización; condición, incremento){
  // sentenzas
}
```

##. 5. FUNCIÓNS

Declaración
O valor por defecto para os parámetros e o valor de retorno son optativos.
```php
function nome_da_funcion($parametros = valor_por_defecto){
  // sentenzas
  return $value;
}
```

Invocación
Se na declaración os parámetros teñen valor por defecto,
```php
nome_da_funcion($argumentos);
```

funcións predefinidas

var_dump(). volca a info da variable.
date($format: string). crea un obxeto de data.
time(): timestamp.
sqrl($number): raíz cadrado.
rand($min, $max): número aleatorio.
pi():
round($val, $precisión): redondeo
isset($var): devolve se existe ou non unha variable.
trim($var): limpa espazos en branco arredor dun string.
unset($var): elimina una variable da memoria.
empty($var): comproba se a variable existe, o seu valor non é valeiro ou cero.
strlen($var): lonxitude dun string.
strpos($var, $busca): encontra un treito no string.
str_replaces($search, $replace), substitúe un texto.
strtolower($string): pasa un string a minúsculas.
strtoupper($string): pasa un string a maiúsculas.
