
## Peticións http
Todos os métodos dos HttpCliene teñen un parámeto opción chamado options que éun obxecto onde se poden configurar as headers da peticiónque pode recibir un obxecto de tipo HttpHeaders ou un obxecto que conté un número indeterminado de pares de chave-valor onde a chave á un string e o valor é outro string ou un array de strings. 

Outra posibilidade é enviar query params dentro destas options. Pra isto establécese a propiedade params que recibe un tipo de dato HttpParams ou un obxecto con un número indetermindado de chaves-valor. Como particularidade ten unha sintaxe propia para o seu seteo:

```TypeScript
params: new HttpParams().set()('print', 'pretty');
```

O HttpClient de Angular devolve os datos dunha petición por defecto, pero hai técnicas para obter a resposta completa. O obxecto options ten unha propiedade observe que dtermina o tipo de observable que será devolto. Por defecto está seteado a `body`, pero admite outras posibilidades como `response` para a resposta completa e `events` para os eventos da patición.

O HttpClient tamén admite a configutación do tipo de resposta mediante a propieddade responseType de options. Por defecto está seteado a `json`, pero adminte outras: `text`para texto plano, `blob` para ficheiros e `array buffer` para fluxos de datos binariso en bruto. Os Obxectos de tipo blob teñen un tipo MIME asociado.

## Interceptors

Un interceptor en Angular é unha clase que modifica as peticións http antes de que se envíen ao servidor. Pódense usar para agregar cabeceiras, manexar erros, cachear, etc. Ten a forma dun servizo que implementa a interface HttpInterceptor. Esta ten un método `intercept()` que recibe dous paramámetros: `req: HttpRequest` e un obxecto `next: HttpHandler`. O primeiro representa a petición orixinal e o segundo é unha función factoría que modifica a primeira e devolve un observable `<HttpEvent<angy>>` que representa a resposta da petición.

Para utilizar un interceptor hai que rexitralo nun módulo (normalmente no AppModule). Na propiedade `providers` dáse de alta con esta sintaxe:

```Typescript
{provide: HTTP_INTERCEPTORS, useClase: MyInterceptor, multi: true};
```
A propiedade `multi` establece se se poden implementar varios interceptors. Neste caso, a orde é relevante porque as peticións vanse procesar de arriba a abaixo e cando se procese a resposta de abaixo a arriba. 

Un exemplo de interceptor que toma as cabeceiras da ptición orixinal e lle engade outra sería como o seguinte:

```Typescript
expor class AuthIntercepto implements HttpInterceptor {
    intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>>{
        const newReq = req.clone({ headers: req.headers.append('X-Auth-Custom', 'key')});
        return next.handle(newReq);
    }
}
```

Tamén é posible manipular a resposta da petición mapeando o observable que devolve a petición: 

```Typescript
    return next.handle(newReq)
        .pipe(
            tap(event => {
                if (event.type === HttpEventType.Response){
                    console.log(event.bogy);
                }
            })
        );
```

## Resolvers

Un resolver é unha peza de código que se executa antes de que se cargue unha rutapara asegurarse de que os datos dos cais depende a ruta están disponibles. É un servizo que interpreta a interface `Resolver<T>` que recibe o tipo de dato que vai resolver. A interface ten un método `resolve(route: ActivateRouteSnapshot, state: RouteStateSnapshot)` cuxos parámetros son os datos sobre a ruta e o estado actual do router.

Dentro do método `resolve` invócase o método do servizo correspondente se necesidae de subscribirse (porque o Resolver xa o fai por dentro). Un exemplo de resolver para unha aplicación de receitas pode ser a seguinte:

```Typescript
@Injectable({provideIn: 'root'})
export class RecipesResolverService implements Resolver <Resource[]>{
    
    constructor(private readonly dataService: DataService ){ 
    }
    resolve(route: ActivateRouteSnapshot, state: RouteStateSnapshot): Recipe[] | Observable<Recipe[]> | Promise<Recipe[]>{
        return this.dataService.fetchAllRecipes();
    }
}
```

Para usar o resolver hai que modificar o módulo de rutas onde está declarada a ruta onde queremos que se aplique o resolver: 

```Typescript
{
    path: "id",
    component: RecipeDetailComponent,
    resolver: [RecipesResolverService] 
};
```