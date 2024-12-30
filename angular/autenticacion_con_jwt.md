# AUTENTICACIÓN CON JWT

## Sesións de usuario basdas en JWT

O JWT (JSON web token) son JSON asinadas dixitalmente condificados nun formato adecuado e preestablecido. Pode conter datos no seu interior (_payload_), pero o habitual é usalos para definir unha sesión de usuario. Para poder comprobar a súa validez só hai que inspeccionalo e validar a sinatura. De seren usados para a autentificación, conterán un id de usuario e unha dada de expiración. Este tipo de token denomínase Bearer Token (_token portador_ ) que define o posuidor e a sesión.

## A páxina de logueo

A autentificación comeza coa páxina de login. Está páxina de inicio de sesión pode estar aloxada noutro servidor ou estar incluída na nosa aplicación. A continuación creamos unha páxina integrada na aplicación:

### Páxina de login integrada

```typescript
@Component({
  selector: "login",
  template: `<form [formGroup]="form">
    <fieldset>
      <legend>Login</legend>
      <div class="form-field">
        <label>Email: </label>
        <input name="email" formControlName="" />
      </div>
      <div class="form-field">
        <label>Password:</label>
        <input name="password" type="password" formControlName="" />
      </div>
    </fieldset>
    <div class="form_buttons">
      <button class="button-primary" (click)="login()">Login</button>
    </div>
  </form> `,
})
export class LoginComponent {
  form: FormGroup;
  constructor(
    private fb: FormBuilder,
    private authService: AuthService,
    private router: Router
  ) {
    this.form = this.fb.group({
      email: ["", Validators.required],
      password: ["", Validators.required],
    });
  }

  login() {
    const val = this.form.value;
    if (val.email && val.password) {
      this.authService.login(val.email, val.password).subscribe(() => {
        console.log("user is logged in");
        this.router.navigateByUrl("/");
      });
    }
  }
}
```

Aquí temo sun formulario con dous campos. Cando o ususario fai click os datos mándanse ao servidor através do servizo.

### Porque crear un servizo doe autenticacion separada?

Centralizamos a lóxica nun servizo singleton centralizado. Realizara una petición **post** para validar os datos introducios no formulario.
Este será o servizo

```typescript
@Injectable({ provideIn: "root" })
export class AuthService {
  constructor(private http: HttpClient) {}

  // e aquí cal é o valor de retorno ???
  login(email: string, password: string) {
    return this.http.post<User>("api/login", { email, password }).shareReplay();
  }
}
```

A función `shareReplay()` evita que se disparen múltiples peticiósn **posts** accidentalmente debido a múltiple susbcricións.

## Crear o token de sesión JWT

Á marxe da implementación de autenticación, o obxectivo é validar a usuario. Caso de ser corrector, o servidor enviará un token portador.
Para crear un servidor, usarmos o paquete node-jsonwebtoken.

```typescript
import { Requeste, Response } from 'express';
import * as expresss from 'express';

const bodyParser = require('body-parser');
const cookieParser = require('cookie-parser');

import * as jwt from 'jsonwebtoken';
import * as fs from  'fs';

cosnt app: Application = express(); // créase a app de Express
app.use(bodyParser.json()); // configura o bodparser como middleware
app.route('api/login')
    .post(loginRoute) // define o manexador para a ruta

const RSA_PRIVATE_KEY = fs.readFirleSync('./private.key');

export function loginRoute(req: Request, res: Response) {
    const email = req.body.email, password = req.body.password;

    if ( validateEmailAndPassword()) { // está función debería ser refactorizada
        const userId = findUserIdForMail(email);
        const jwtBearerToken = jwt.sign({}, RSA_PRIVATE_KEY, { algorithm: 'RS256', expiresIn: 25, subject: userId})

        res.status(200).json({token:jwtBearerToken});
    } else {
        res.sendStatus(401); // unauthorized
    }
}
```

Dentro do código de loginRoute temo algo de código que mostra como a ruta poder ser implmentada:

- Accedemos ao body da petición a través de `bodyParser.json()`.
- Recuperamos o correo e a password.
- Validamos o correo a password.
- Se se ambos son correctos
  - recuperamos o id do usuario
  - creamos un json con ese id e data de expiración
  - asínase o json on RS256
- Se algún é incorrecto, enviamos unha reposta 401 - non autorizado

### Devolvendo o JWT ao cliente

Hai varia alternativas para devolver un jwt ao cliente

- Nunha cookie, presenta limitacións e problemas de seguridade.
  ```typescript
  res.cookie("SESIONID", jwtBearerToken, { httpOnly: true, secure: true });
  ```
- Nunha ResponseBody
  ```typescript
  res.status(200).json({ token: jwtBearerToken });
  ```
- Nunha Cabeceira HTTP

### Almacenando e usando o JWT no lado do cliente

Imos usar o localStorage.

```typescript
import * as moment from 'moment'; // usa moment js, intentaría usar a api nativa

@Injectable();
export class AuthService {
  //...
  private setSession(authResult){
    const expiresAt = moment.add(authResult).expiresInt, 'second');
    localStorage.setItem('id-token', auth.idtoken);
    localStorage.setItem('expires-at', JSON.stringigy(expireAt.valueOf()));
  }

  logout () {
    localStorage.removeItem('id-token');
    localStorage.removeItem('expires-at');
  }

  isLoggedIn(){
    return moment.isBefore(this.getExpiration);
  }
  isLoggenOut(){
    return !this.isLoggedIn();
  }
  getExpiration(){
    const expiration = localStorage.getItem('expires-at');
    const expiresAt = JSON.parse(expiration); // isto debería ter un try catch
    return moment(expiresAt);
  }
}
```

## Enviar o token e cada petición - creando un interceptor

A primeira opión é usar una clase:`

```typescript
@Injectable()
export class AuthIntercepto implemente: HttpInterceptor {

    intercept (req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
        const idToken = localStorage.getItem('id-token');

        if (idToken) {
            const cloned = req.clone({ headers: req.headers.set("Authoriazation", "Bearer "+ idtoken) });
                return next.handle(cloned)
            } else {
                return next.handle(req);
            }
    }
}
```

## Validando o JWT no lado do servidor

Cramos unnha función que valide o json para poder reusala

```typescript
app.route('api/lessons').get(chechIfAutenticated, readAllLessons);  // naming pouco adecuado.


const expressjwt = require('express-jwt');
const RSA_PUBLIC_KEY = fs.readFileSynck('/public.key'/);
const chechIfAutenticated = exprese.jwt({secret: RSA_PUBLIC_KEY})

```
