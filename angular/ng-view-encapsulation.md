# VIEW ENCAPSULATION DE ANGULAR

O mecanismo de estilado por Angular por defecto é a _encapsulación emulada_.
Por defecto os, os estilos de Angular están ailladas por compoñentes. Esta deseñado para evitar que os estilos dunha funcionalidade colidan coa doutra de dentro do desenvolvemento dunha applicación. Os navigadores non soportan o aillamento de estilos polo que se non se aplica unha metodoloxía disciplinadamente teremoes problems de mantemento de css. Un escenario diferente prodúcese cando se usa un compoñnte de terceiros. O illamento de estilos permite evitar que os estilos propios colidan con outros.

[Demo de encapsulado simulado]

Está baseado na especificidade do selector. Faino introducindo un atributo personalizado no elemento, por cada compoñente e logo aplica ese atributo como selector á regra css. Isto implica unha especificade mínimia (0,1,0). Cata compoñente ten un atributo _nghost_ e cada elemento dentro del un de tipo _ngcontext_. Ao iniciar a aplicación cada compoñente ten un atributo único asociado ao host dependendo da orden de compilación, xunto a isto cada elemento da template tamén ten cadanseu atributo.
A presenza destes atributos permítenos escribir css normalmente con maior especificidade á que teñen nunha aplicación vainilla. Porén, Angular, xa o fai por nós.
No inicio (ou en tempo de compilación) Angular relaciona estilos entre compoñentes e aplícaos isoladamente de xeito transparente. Este mecanismo non se basea no Shadow DOM, sen nestas propiedades.

## O selector de pseudo-clase :host

Canto queremos aplicar regras de estilos a un compoñente mesmo, no ficheiro de estilos asociamos, usamos o selector da pseudo-clase _:host_. Este selector asegúrase de que os estilos só teñen como albo este compoñente. Porque en tempo de execución relaciónanse as regras de css cos atributos asignados. O selector _:host_ é combinable con outros e cando se fai aniñamento a especificidade consérvase.

## O selector de pseudo-elemento ::deep

Se queremos que os estilos se propaguen en cascada nos fillos dun compoñentes podemos usar a combinación _:host ::deep_ que opite a xeración de atributo. Esta combinación pode ser util para casos de _context projection_ Este selector ten como alias _/deep/_ e _>>>_ e están deprecados para evitar malas prácticas.

## O selector de pseudo-clase :host-context

O selector :host-context aplica a estolso a elementos externos a un compoñente

## Alternativa a ng-deep

Configurar clases en función do ???, hostcontext, custom properties.
