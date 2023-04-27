# JavaScript Internals

É unha linguaxe de programación interpretada polo navegador en tempo real. Ademais é monofío (_single threaded_) polo que unha función que necesite certo tempo para ser executada, bloqueará o resto.

## JavaScript Engine

Cada navedatado ten o seu propio motor (_engine_) que intepreta a linguaxe. Este motor está formado por dúas zonas de memoria, o **Heap** e o **Stack**.

## Heap

É a rexión de memoria que almacena a definición de obxectos complexos. Ten carácter dinámico e é controlado periodicamente polo recolledor de lixo (_garbage collection_).

## Stack

O **Stack** é unha estrutura de datos LIFO que almacena as variables locais dunha función invocada, incluíndo as funcións "internas". A **Call stack** é una pila que consiste en todas as función invocadas até o momento. Unicamente se pode executar unha función cada vez.

## JavaScript runtime

A execución da **call stack**.

## Web APIs

As **Web APIs** son conxuntos de funcións que proporcionan función para realizar chamadas de rede, manipulación do DOM, procesar recursos como vídeos ou audios. Cando se executa unha función que pertence a unha web API, como `setTimeout()`, delégase a súa execución ao contedor web API, que se executa no navidador nun fío diferente do fío de JavaScript.

## Event queue

JavaScript depende en parte das función de call back que se executan cando ocorre un evento. O runtime ten un compoñente, o **event queue** que unha cola de mensaxe FIFO.

## Event loop

É un bucle infinito que verifica o contido do event queue. As funcións chegan á pilla de execución a través deste loop. 

## Resumo

