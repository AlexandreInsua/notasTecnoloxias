# TESTING DE ANGULAR CON VITE

## Intro

Vitest é un framework de testing para JS/TS deseñado para funcionar de maneira nativa no ecosistema de Vite. O seu obxectivos principal é unha execución de test rápida con unha experiencia de desenvolvmento semellante a Jest pero aproveitando os módulos de ES e o pipeline de Vite. Funciona como un test runner que se integra ao grafo de módulos de Vite.
O ecosistema de Vite baséase nun enfoque moderno de desenvolvemento frontend no que o código se serve directamente como módulos de ES durente o desenvolvemento, evitando procesos de building completos en cada cambio. O sistema inclúe un servidor de desenvolvemento moi rápido, con optimización de dependencias mediante esbuild e un sistema extensible de plugins inspirados na arquitectura de Rollup. Iso permite que a mesma infra se usa para desenvolver apps, executalas e preparalas para producción.
A pipeline de Vite funciona como unha cadea de transformacións que se executa cada vez que se executa cada vez que se solicita un módulos. Cando o navegador ou runtime pide un ficheiro, vite resolver a ruta do módulo, analiza as súas dependencias e para o código por diferentes plugins que poden transformalo. O resultado é código JavaScript listo para executar, xerado baixo demanda e cacheado para execución posteriores.
Sobre esta infraestrutura constrúese Vitest test que reutiliza o servidor e a pipeline de Vite para executar tests sun un paso previo de compilación. Mediante Vite-Node, Vitest
Vitest pode cargar módulos, aplicar tranformacións e aplicalas en Node, distribuíndo test en múltiples testers para executalos en paralelo. Como o grafo de módulos de Vite pode detectar cambios no código e relanza automaticamente só os test afectados.
Vitest organiza os seus tests en suites mediante _describes_ e tests mediante _its_. Admite os operadores _skip_, _todo_, _only_, _skipIf_...

## Spyes

Un **spy** é un obxecto observador doutro obxecto e créase coa utilidade _vi.spyOn(object,method)_ e admite asercións habituais. Non modifica o comportamento da función a non ser de que se configura explicitamente.

## Mocks

Un **mock** reempraza o comportamento dun obxecto. ESta funcionalidad permide illar dependencias en tests unitarios. Contrúese un spy e mockease o retorno en cuxo caso o funcionamenteo interno do método non é executado, está bypaseado, é ignorado.

## Pure mock

Un **mock puro** non actúa sobre un obxecto existente, senón que se crea de cero usando a sintaxe `conts mock = vi.fn()` e mockéase o retorno.

## Limpeza

Para illar o estado dos mocks en cada test, pódese limpar o historial deo mock co método `mockClear()`.
