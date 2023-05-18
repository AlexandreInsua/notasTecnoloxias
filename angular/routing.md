# Routing avanzado

As rutas principais mónstranse no router-outline principal, as rutas fillas móstranse en cada un dos router-outline embebidos e as rutas en router_outlines nomeados.

Un router_outline nomeado é aquel que ten un atributo `name`. Un caso de uso é un compeñente que se mostra nun lateral, por exemplo un side menú, que normalmnente depende da ruta. Neste caso subscribímonos á ruta no seu construtor, por exemplo:

```Typescript
export class SideMenuComponent {
    constructor(private readonly route: ActivatedRoute){
        this.route.params.subscribe(
            params => console.log(params);
        )
    }
}
```

Este compoñente recibe una notificación cada vez que o compoñente cambia, polo que reacciona a eles.

A configuración deste compoñente como ruta auxiliar realízase no módulo de rutas correspondente establecenceo a propiedade `outlet`:

```Typescript
{
    path:'father',
    component: Fathercomponent,
    children: [
        {
            path: '',
            component: ChildComponent
        },
        {
            path: '',
            outlet: 'sidemenu',
            component: SideMenuComponent
        }
    ]
}
```

Deste xeito cando se vai á ruta `/father` teremos o seguinte:

1º- Carga o compoñente fillo no router-outlet embebido.
2º- Carga o compoñente auxilar no router-outlet auxiliar coa propiedade `name="sidemenu"`.

Se agregamos unha ruta parametrizada, debemos configurala tamén para o elemento auxiliar:
```Typescript
{
    path:'father',
    component: Fathercomponent,
    children: [
        {
            path: '',
            component: ChildComponent
        },
        {
            path: ':id',
            component: ChildComponent
        },
        {
            path: '',
            outlet: 'sidemenu',
            component: SideMenuComponent
        },
        {
            path: ':id',
            outlet: 'sidemenu',
            component: SideMenuComponent
        }
    ]
}
```

En escenarios moi avanzado por ser necesario navegar dentro do side menu, o que se fai programaticamente pasando varias rutas:

```Typescript
this.router.navigate([{outlets:{primary:path, sidemedu:path}}, {relativeTo: this.route}])
```