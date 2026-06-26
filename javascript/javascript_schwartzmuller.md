## Introdución

O curso é unha referencia completa de JavaScript. É unha linguaxe de tipado dinámico e feble. Compílase xusto a tempo no motor de execución do navegador ou en entornos como Node.js e Bun.js. Naceu para facer webs máis dinámicas e modificar contido sen recargar a páxina. A web funciona no paradigma cliente-servidor.

O motor JavaScript parsea e compila o código xusto a tempo, normalmente a bytecode e ás veces a código nativo, e logo executa para aplicar cambios no HTML. O contexto principal de execución en JavaScript é un único fío no navegador, con fíos separados en Web Workers. Tipado dinámico significa que os tipos se determinan en tempo de execución e non en tempo de compilación. O tipo dunha variable pode cambiar durante a execución.

Os tipos de datos infírense automaticamente, polo que non hai que explicitalos. No navegador, JavaScript pode manipular HTML e CSS, pero non interactúa co sistema local. No servidor, executa en Node, Deno, Bun ou outros entornos de execución.

Resumo:

- JavaScript é unha linguaxe dinámica e compilada xusto a tempo.
- O navegador é o entorno de execución principal.
- O tipado dinámico permite que os valores cambien de tipo en tempo de execución.

## Execución de código de JavaScript

O código execútase de arriba abaixo. Hai que ter en conta a orde das instrucións.

### Funcións

Unha función agrupa instrucións e execútase máis tarde. Úsanse para illar código e crear ámbitos propios.

### Obxectos

Un obxecto é unha colección de datos relacionados en pares chave-valor.

### Importacións

- `defer` carga o script despois do parseo do HTML e conserva a orde de execución.
- `async` carga o script en paralelo e execútase cando está listo; non garante orde.
- Funciona só con scripts externos.

Resumo:

- O flujo de execución segue a orde do código.
- Funcións crean ámbitos e reutilizan instrucións.
- `defer` e `async` cambian cando se executan os scripts.

## Detrás de bambalinas

### ES5 e ES6

Son versións do estándar ECMAScript. ES6 (ES2015) introduciu a sintaxe moderna de JavaScript.

### var, let e const

- `var`: alcance de función ou global; ten hoisting.
- `let` e `const`: alcance de bloque.
- `const` impide reasignar o identificador, pero non fai o obxecto inmóbil.
- `use strict` activa o modo estrito.

### Parseado e compilación

- Parsear: o motor lê e analiza o código.
- O compilador xera bytecode e/ou código nativo xusto a tempo.
- O navegador ofrece APIs que o motor pode usar.

### Execución de código

- Heap: memoria para obxectos e referencias.
- Stack: memoria para valores primitivos e chamadas.
- Contexto de execución: controla variables e ámbito.
- O call stack xestiona chamadas a funcións.
- O event loop procesa tarefas asincrónicas.

### Valores primitivos e por referencia

- Primitivos: `undefined`, `null`, `boolean`, `number`, `string`, `bigint`, `symbol`.
- Copiase o valor no stack.
- Referencias: obxectos, arrays e funcións.
- Copiase a referencia ao heap.
- A comparación por valor e por referencia é diferente.

### Garbage collector

### Getters e setters

Usa `get` e `set` para definir propiedades calculadas ou validar valores.

Resumo:

- `get` devolve un valor calculado.
- `set` valida ou transforma o valor ao asignalo.

## OOP

- OOP serve para reusar código e modelar entidade reais.
- Os campos de clase inicíanse despois de executar o constructor do pai.
- `Object.getOwnPropertyDescriptor(obj)` mostra o descriptor dunha propiedade.
- `Object.defineProperty(obj, prop, descriptor)` define unha propiedade con control fino.

Resumo:

- A OOP organiza código en clases e instancia.
- Os descriptores dan control sobre enumerabilidade, escritura e valor.

## PROTOTIPOS

- As funcións construtoras crean obxectos con prototipos.
- O prototipo é un obxecto que contén métodos compartidos.
- A cadea de prototipos remata en `Object.prototype`.
- `Object.getPrototypeOf(obj)` obtén o prototipo.
- `Object.setPrototypeOf(obj, proto)` cambia o prototipo, pero afecta ao rendemento.
- `Object.create(proto)` crea un obxecto cun prototipo específico.

Resumo:

- A herdanza en JavaScript baséase en prototipos.
- Non modifiques prototipos en tempo de execución de forma habitual.

## APIs DO NAVEGADOR

- `dataset`: acede a atributos `data-*` dun elemento.
- `getBoundingClientRect()` devolve tamaño e posición respecto ao viewport.
- `offsetLeft`/`offsetTop` refírense ao `offsetParent`.
- `clientTop`/`clientLeft` devólven tamaños de bordo.
- `window.innerWidth`/`innerHeight` e `document.documentElement.clientWidth`/`clientHeight` miden dimensións.
- `<template>` conserva contido non renderizado.
- Carga dinámica de scripts optimiza rendemento; coida a seguridade.
- Temporizadores: `setTimeout`, `clearTimeout`, `setInterval`, `clearInterval`.
- `location`, `history`, `navigator` e `Date` son APIs globais útiles.

Resumo:

- O navegador ofrece APIs para medir e manipular a UI.
- A carga dinámica mellora a experiencia se se fai con seguridade.
- Coida compatibilidades ao usar APIs modernas.

## TRABALLANDO CON EVENTOS

- Usa `addEventListener` para rexistrar eventos e poder eliminalos despois.
- `preventDefault()` evita o comportamento por defecto.
- `stopPropagation()` detén a burbulla; `stopImmediatePropagation()` interrompe outros listeners.
- Event delegation centraliza eventos nun pai e reduce listeners.
- Podes disparar eventos con métodos como `element.click()`.

Resumo:

- `addEventListener` é o método recomendado.
- Controla a propagación con `stopPropagation` cando sexa necesario.
- A delegación mellora rendemento en listas grandes.

## CONCEPTOS AVANZADOS DE FUNCIÓNS

- Funcións puras non teñen efectos laterais.
- Funcións impuras modifican estado externo.
- Side effects son cambios fóra da función.
- Factory functions devolven outras funcións.
- Closures gardan referencias ao ámbito exterior.
- IIFE executa a función inmediatamente.
- Recursión: unha función chámase a si mesma.

Resumo:

- Prefire funcións puras para mellorar testabilidade.
- Usa closures para encapsular estado privado.
- IIFE e recursión son patróns útiles pero hai que controlar pila.

## NUMBERS E STRINGS

- `Number.MAX_SAFE_INTEGER` e `Number.MIN_SAFE_INTEGER` definen o rango seguro de enteiros.
- A suma `0.2 + 0.4` non é exacta por representación binaria.
- `BigInt` para enteiros arbitrarios.
- Xeración aleatoria: `Math.floor(Math.random() * (max - min) + min)`.
- Tagged templates permiten procesar cadeas con funcións.
- Regex: `test()`, `exec()`, `match()`.

Resumo:

- Os números teñen precisión limitada; usa `BigInt` cando sexa preciso.
- Regex é a ferramenta básica para cadeas complexas.

## CÓDIGO ASÍNCRONO

- JavaScript é monofío; a asincronía evita bloqueo.
- Callbacks foron o primeiro patrón asincrónico.
- Promesas: `resolve`, `reject`, `then()`, `catch()`, `finally()`.
- `async/await` facilita a lectura do código asincrónico.
- `Promise.all()` espera varias promesas; `Promise.race()` retorna a primeira.

Resumo:

- O event loop xestiona tarefas asincrónicas.
- Prefire promesas ou `async/await` sobre callbacks anidados.

## HTTP REQUEST

- `XMLHttpRequest` é legacy.
- `fetch` é a API moderna e baseada en promesas.

Resumo:

- Usa `fetch` para solicitudes HTTP modernas.

## LIBRERÍAS DE TERCEIROS

- Pros: aceleran o desenvolvemento cun código probado.
- Contras: aumentan o bundle e poden introducir riscos de seguridade.
- Avalía librerías por actividade, versións, tests e dependenzas.

Resumo:

- Emprega librerías por valor engadido e revisa a manutención.

## MÓDULOS DE JS

- Usa `type="module"` para habilitar módulos.
- `export default` vs exportacións nomeadas.
- `import()` dinámico carga módulos en runtime.
- Un módulo execútase unha soa vez no primeiro import.

Resumo:

- Os módulos organizan e encapsulan código.
- `import()` é útil para carga condicional.

## TOOLING & WORKFLOWS

- Servidos de desenvolvemento, bundlers (webpack, rollup, esbuild).
- Babel para transformar código.
- ESLint e formatters para calidade.

Resumo:

- As ferramentas axudan con compatibilidade e calidade.

## BROWSER STORAGE

- `localStorage` e `sessionStorage` gardan pares clave-valor simples.
- Cookies para sesións e configuracións no backend.
- `IndexedDB` para almacenamento estruturado no cliente.

Resumo:

- Usa `IndexedDB` para datos complexos; `localStorage` para pequenas opcións.

## BROWSER SUPPORT

- Polyfills cubren funcionalidades ausentes en navegadores antigos.
- `<script nomodule>` serve contido para navegadores non compatibles con módulos.

Resumo:

- Emprega polyfills só cando sexa necesario.

## META PROGRAMACIÓN

- `Symbol` crea claves únicas para propiedades.
- Iterators e generators permiten controlar iteracións.
- `Reflect` e `Proxy` permiten meta-programación e interceptación de operacións.

Resumo:

- `Proxy` e `Reflect` son poderosos, úsanse con coidado.

## SEGURIDADE

- Todo o código cliente é accesible a terceiros.
- XSS: evita inserir HTML non confiable; usa sanitización.
- CSRF: protexe con tokens e controla cookies.
- CORS: configura cabeceiras no servidor.

Resumo:

- Non confíes en datos do cliente; valida no servidor.

## DEPLOYING

- Hosting estático para SPAs; hosting dinámico para backend completo.
- Fluxo: `dev/test` → optimizar → `build` de produción → deploy.
- Exemplos: Firebase Hosting, Vercel, Heroku.

Resumo:

- Sempre publica o build de produción optimizado.

## PERFORMANCE E OPTIMIZACIÓN

- Start-up time: tempo ata poder interactuar.
- Run time: fluidez e ausencia de lag.
- Minimizar bundle e reducir peticións HTTP.
- Usar CDN e lazy-loading para recursos pesados.
- Evitar manipulacións ineficientes do DOM.
- Medir en producción con `performance` e ferramentas.

Resumo:

- Mide sempre en contornas reais.
- Menos código e menos peticions melloran a experiencia.

## WEB COMPONENTS

- Web Components inclúen Custom Elements, Shadow DOM, templates e slots.
- Un Custom Element extende `HTMLElement` e debe chamar `super()` no constructor.
- Non accedas ao DOM desde o constructor; usa `connectedCallback()`.

Resumo:

- Web Components permiten encapsulación e reutilización sen framework.
