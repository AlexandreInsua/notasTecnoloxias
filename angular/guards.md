## Autentificación en Angular

Nun escenario de cliente-servidor a validación de credenciais debe facerse do lado do servidor porque de facrse do lado do cliente web todo o código Javascript está exposto a todos os ususarios e pode ser manipulado.

Nas aplicacións monolíticas tesmos o cencepto de sesión, pero en Angular como é unha SPA manéxase de forma diferente porque FE e BE están desacopladas.

Como o BE é una API a técnica que se aplica radica no uso dun token de autentificación. O cliente envía os datos de autenficación e o servidor responde cun token que só o servidor pode descodificar. O cliente garda este token e xúntao ás peticións seguintes para que sexan autorizadas.

## Guards en Angular

Necesitamos un sisteme de gardas para as rutas en Angular. Un Guard é un servizo que implementa a interface CanActivate. Esta implementa un método `canActivate()` que manexa a lóxica para decidir se se permite navegar a unha ruta que necesita autorización ou redirixir a outra segura.

Un exemplo de garda de logo que sevolver se hai un usuario logueado poderá ser algo como este:

```Typescript
@Injectable({provideIn: 'root'})
export class AuthGuard implements CanActivate {
    private authService;

    constructor(){
        this.authService = inject(AuthService);
    }

    canActivate(route: ActivateRouteSnapshot, state: RouterStateSnapshot): boolean | URLTree | Observable<boolean | URLTree> | Promise<boolean | URLTree>{
        return this.authService.user$.pipe(
            take(1),
            map( user => !!user)
        )
    }
}
```
Necesita o operador `take(1)` para asegurarse de que non hai comportamentos estraños por recibir emisións diferentes do observable.

Despois no ficheiro de rutas, actívase a garda mediante a propiedade `canActivate`:

```Typescript
{
    path: 'recipees',
    canActivate: [AuthGuard]
}
```

Unha alternativa na garda pode ser devolver unha ruta completa. Neste caso para cando non se está logueado redirixe ao compoñente de autentificación:
```Typescript
    return !!user || this.router.createURL(['auth'])
```

