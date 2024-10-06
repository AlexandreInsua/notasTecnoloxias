# CDK DRAG AND DROP

_cdkdrag_ directiva que se aplica a un elemento para se sexa arrastrable

_ckddroplist_ directiva a un elemento para que se comporte como unha lista sensible ao evento de drop

_cdkDragPreview_ directiva que se aplica ao elemento arrastrable para que se cree dento do elemento desexado. Por defecto preview cráse no body. Pódese asignar o valor a parent ou a unha variable da template.

No elemento pai hai que capturar o evneto (cdkDropListDropped) e asinarlle un comportamento.

_cdkaDropListConnectedTo_ directia que á que se lle día unha lista con quen pode intercambiar datos.

(cdkaDropListDropped) evento que captura cando un elemento foi soltado dentro dunha lista

[cdkDropListEnterPredicate] input que recibe os datos cos que traballa a lista

## Funcións para move o itam

moveItemInArray(container, idex, item) mover un elemento dentro dunha lista.

transferArrayItem(previous container, container, previous index)

_cdkDropListGroup_ directiva que se aplica a un elemento pai de listas para habilitar o efecto drop entre elas

[cdkDropListaData]="myColletion"
