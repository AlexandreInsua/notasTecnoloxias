# Optimizacións en observables

## 1. Evitar anidar pipes  en observables

Se se está agardando que un observable finalice para lanzar outra petición, hai que evitar facer unha a petición subseguinte dentro do callback de éxito, cambia o fluxo do observable a unha nova petición. 

Pódese mapear e filtrar os datos que veñen da primeira petición na segunda petición, cun _switchMap()_.

antes 
``` typescript
class MyClass {
	private _destroy$ = new Subject<void>();
	constructor( private readonly service: Service, private readonly serviceTwo: serviceTwo) {}

	getData(): void {
		this.service.getData()
			.pipe(takeUntil(this._destroy$))
			.subscribe( (res)=>{
				this.serviceTwo.getMoreData(res)
					.pipe(takeUntil(this._destroy$))
					.subscribe()
			})
	}
}
```
agora
``` typescript
class MyClass {
	private _destroy$ = new Subject<void>();
	constructor( private readonly service: Service, private readonly serviceTwo: serviceTwo) {}

	getData(): void {
		this.service.getData()
			.pipe(
				takeUntil(this._destroy$),
				switchMap( res => this.serviceTwo.getMoreData(res))
			)
			.subscribe()
	}
}
```

## 2. Desuscribirse sempre

Cando se hai subscricións asociadas á navegación e se cambia de ruta, pode haber observables que fiquen abertos. 
Unha alternativa é usar un _takeUtil()_. É mellor usar ese método que _take(1)_ porque este non garante que as subscricións se destrúan cando se destrúe o compoñente.

antes
``` typescript 
class MyClass {
	constructor( private readonly _router: Router){
	this._router.events
		.pipe(
			filter( response => response instanceof NavigationEnd)
		)
		.subscribe( (response: NavigationEnd)=>{
			console.log('router subscription', res);
		})
	}	
}
```
agora
``` typescript 
class MyClass implements OnDestroy {
	private _destroy$ = new Subject<void>();

	constructor( private readonly _router: Router){
	this._router.events
		.pipe(
			filter( response => response instanceof NavigationEnd),
			takeUntil(this._destroy$)
		)
		.subscribe( (response: NavigationEnd)=>{
			console.log('router subscription', res);
		})
	}

	ngOnDestroy():void {
		this._destroy$.next();
	}
}
```
