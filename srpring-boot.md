# SPRING BOOT - CLOUD

## 1. Introdución aos servizos web

Un servizo web é un compoñente, un tipo particular de app web, que expón opereción a outros programas a traves da web e que é accestible mediante o protocolo http, aplicando a arquitectura cliente-servidor.
A estrutura esá formada polo compoñente da lóxica de negocio e polo controlador web que controla a interacción co exterior.
Os servizos poden ser servizos web XML ou servizos REST aos se se accen con HTTP con múltples formatos.

### 1.1. Servizos REST

Os servicos REST (Representational State Transfer) expoñen a traves de Internet unha seria de recursos ao que s pode acceder mediantes peticións HTTP.
Os recursos consisten den datos ou en operacións sobre ses datos. Cada recursos identifícase unha unha URL, metodo HTTP, parámetos, tio de reposta e tipo consumido (5 datos.)

### 1.2. API JAX-RS

API JAX-RS é unha especificación de Java EE que signifa a creación de adaptado web en servizo web Java.
Inclúea anotadións para delegar tarefas no motoro JAX-RS
O módulo web-mve propociona o soporte necesario para crear servizs web con Srping.
Anotacións: @RestControl, @GetMapping, @PostMapping, @PutMapping, @PatchMapping, @DeleteMapping, @PathVariable, @RequestBdy
Microservizo. Servizo que inclúe todo o necesario para a súa execuión e desprágase de xeito automático e independiente e inclúe o seu entorno de executión.

## 2. Creacion de microservizos

### 2.1. Microservizos con Spring Boot

Spring Boot é una variante de Spring pensado para cear microservizos e crear ficheiros .jar.
A inclusión de dependenas en maven.
Simplifícase co starte que é un conxunto de dependencias básicas maven para desenvolver o proxecto. Inclúe Spring Core, context, web, web-mvc, e jackson.
A configuración asúmese e non é necesario modificar ficheiros xml.
Para indicar parámetros de configuración úsase o ficheiros aplication.properties ou application.yml.

[esquema dunha app]

### 2.2. Propiedades

As propiedades de configuración dun proxecto Spring Boot pódese establecer no ficheiro resources/properties que adminte un formato de chave=valor ou yaml

### Estrutura dun proxecto

/controler - controlador

/model - clase clase POJO que representea a entidade

/service - lóxica de ngocio - service Interface coa lóxica - serviceImpl clase coa implementacion

/ dao - clase coa entidade etiquetada

### Clase Main

É a clase lanzadora co método estático que arrica a lanza a aplicación

```java
@SpringBootApplicacion
public class Application {
    public static void main (String[] args){
        SpringApplication.run(Application.classe, args);
    }
}
```

### 2.3. Parámetros e variables

Unha variable é un dato que se envía como parte da url a continuación da dirección do xervido

http://server/app/path/v1
protocolo - host - app - resource- variable

As variables deben mapearse ao parámetros do método do controlas mediante a anotación @PathVariable:

```java
@RestController
public class GenericController {
    @GetMappin (value="path/{x}", produces = MediaType.TEXT_PLAIN_VALUE)
    public String test (@PathVariable("x") String variable) {
        //..logic
    }
}
```

### 2.4. outros métodos HTTP

Post - asociado á alta

```java
@PostMapping(value ="path" consumes = APPLICATION_JSON_VALUE)
public void test(@RequestBody Object o){
    // ...logic
}
```

Put - actualización

```java
@PutMapping(value ="path" consumes = APPLICATION_JSON_VALUE)
public void test(@RequestBody Object o){
    // ...logic
}
```

Delete - eliminación

```java
@DeleteMapping(value="path" )
public void test(@RequestBody Object o){
// ...logic
}
```

Os parámetros da url van en formato queryString de chave valor separadas por ?
http:/server/app/path?x=valor
Este paramatros recupéranse coa etiqueta @RequestParam. Na ruta non se indica ningún nome xa que se recupara como RequetParam

```java
"https://server/app/path?x=value";

@GetMapping (value="path", produces = MediaType.TEXT_PLAIN_VALUE)
public String test (@RequestParam("x") String variable) {
    //..logic
}
```

### 2.5. Respostas

O habitual e que as responsa non sexan en texto plano, senón que envíen unha estrutura de datos en forma de JSON, a través da libraría Jackon, Spring mapea un java Bean a JSON e viceversa. Para iso usamos o valor MediaType.APPLICATION_JSON_VALUE. (Observo que xa o fai sen esta configuración).

### 2.6. Acceso a datos

O acceso a datos encapsúlase nunha capa DAO. Desde a capa de servizo interactúase con esta capa de acceso a datos. Imos usar o módulo Spring Data JPA e o driver MySQL.
Nas interfaces DAO implmentaranse cadansúa clase e extenderán JPARepositori<entidade, chave primaria> que xa implementa métodos estándar tal que:

- save(Entidade e)
- findById(Id id)
- findAll()
- deleteById(Id id)
  Tamén permiete crear métodos que identifica automaticamente a partir do nome ou a través de querey jpql de con query dentro da etiqueta @Query("select \* from ") e se conrresponden con @Transaction e @Modify

### 3.7 Interaccións entre servizos

Podemos crear un servizo que interactúe con outro. A anotación @CrossOrigin nun contralador permite admitir orixes para evita que o navegador bloquee a ptitición por política de CORS.
Spring proporciona a clase RestTemplate para char a un servizo Rest. Forma parte do módulo web de Spring. A súa creación defícnese nunha clase de configuración:

```java
@Bean
public RestTemplate getTemplate(){
    return new Rest Template
}
```

Para inxectalo nunha variable emprégase a anotación @Autowired:

```java
@Autowire
RestTemplate template
```

As peticións GET realízanse mediante o método getForObject que ten a seguinte sinatura

```java
getForObject(String url, Class<T> responseType, Object urivariables)
```

onde _url_ é a url do servizo, _responseType_ é o tipo de java ao que se convertirá o resultado e _uriVariables_ serán os valors das variables uri. A libraría Jackson encárgase do mapeo JSON-Object, por exemplo:

```java
String url = "localhost/cursos"
// recupera todos os cursos
Curso[] cursos = template.getForObject(url, Curso[].clase)
// busca un curso polo se nome
Curso curso = template.getForObject(url + "/{name}", Curso.class, "Java" );
```

Para as peticións post hai dous métodos. Se devolve un obxecto usase

```java
postForObject (String url, Object request, Class<T> responseType, Object uriVariable)
```

Se no devole resultado pódese usar

```java
postForLacation (String url, Object request, Object uriVariable)
```

Por exemplo:

```java
String url "localhost/cursos/"
// crea un novo curso
Curso curso = new Curso(...)
template.postForLocation (String url, curso);
```

Put e delete asumimos que non devolve resultado. (_pero iso é unha mala práctica, a resposta deberia estar normalizada para todo caso_)

```java
void put(String url, Object request, Object... uriVariables);
void delete(String url, Object .. uriVariables);
```

para outros escenarios temos o método exchange

```java
ResponseEntity<T> exchange(String url, HTTPMethod method, http<?> entity, Class<T> responsetype, Object ... uriVariables);
```

por exemplo

```java
Curso curso = template.getForObject(url + "/{name}", Curso.class, "Java");
curso.setDuration(70);
// devolve a lista de cursos modificada
ResponseEntity<Curso[]> rp = template.exchange(url, HTTPMethod.PUT, new HttpEentity<Curso>(curso), Curso[].class)
Cursos [] cursos = rp.getBody(), //???
```

### Interfaz RestClient

Incorporouse a Springboot na version 3.2.
Segue o estilo de programación función
Defínese nunha clase de configuracion

```java
@Bean
public RestClient getRestClient(){
    return RestClient.create();
}
```

E inxéctase igual que calquera outra obxecto de Spring

```java
@Autowired
RestClient restclient;
```

E utilizarase na cápa de lóxica de negocion de aplicación. Emprégase con chamdas encadenadas a métodos:

1. Defínese o tipo de verbo
2. Depois a url
3. Despois o retrieve() e logo devolve

```java
Product p =
    restClient.get(
                .uri(this.BASE_URL + "/product/{id}", 20)
                .retrieve()
                .body.(Product.class)
    );


Product p =
    resClient.post()
                .uri("url")
                .contentType(MediaType.APPLICATION_JSON)
                .body(new Product(...))
                .retrieve()
                .toBodyLessEntitiy()

```

## 3. Securización

Securizar un servizo consiste en permitir o acceso unicamente ao usuarios autorizados. Requírese un procese de autenticación e autorizactión que xestiona Spring Security, para o cal hai que agrega a dependencia e configuración correspondente. hai que determinar onde están os usuarios. Establécese a partir de dous métodos dunha clase de configuración

```java
@EnableWebSecurity
@Configuration
public class SecurityConfig {

    // definicion de suuario e roles en memoria
    @Bean
    public InMemoryUserDetailsManager usersDetails () throws Exception {
        List<UserDetails> users = List.of(User.withUserName("userId"). password("secret").roles("ROLES").build(), ....)
        return new InMemoryUserDetailsManager(users)
    }

    // definición de políticas a recuros
    @ Bean
    puclic SecurityFilterChain filterCharin (HTTPSecurity security) throws Exception{
        return security.build
    }
}
```

### 3.1. como acce un restTemplate a un servizo securizado

Debemos introducir credenciais na cabeceira das peticións, para iso utilizaranse interceptores. Na clase de configuración establécese ese interceptor:

```java
@Bean
public RestTemplate {
    BasicAuthenticationInterceptor intercep;
    intercep= new BasicAuthenticationInterceptor("admin", "admin");
    RestTemplate restTemplate = new RestTemplate();
    template.getInterceptors().add(intercep);
    return template;
}
```

### Como accede RestClient a un servixo autenticado

Débese definir unha cabeceira durante a petición. Inclúese mediante o método header(). No caso do exemplo os valores serán a cabeceira "Authorization" e como valor "Basic ex45jos=" que é o par usuario:pasword en base 64.

## 4. documentación de servizos

A documentación dun servizo consiste en describir que recursos disponibilize. Imos usar Spring Doe que é una libreía de Spring para documentar Servizos Rest baixo o Standar OpenAPI.
OpenAPI é un estándar aberto para a documentación de servizos REST. Admite diferentes formato, entre eles swager. Par poder usar Spring Doc necesitamos inclúrs as dependencias.
A configuración realízase establecendo propidesdes no servizo de donfiguraicion:
springdoe.packageToScan=controller
springdoe.pathToMatch=/\*\*
Cando se arrinca un micro servizo créase unha web de documenación disponible na url /content-path/swagger-ui-html
Sprin soporta anotaciósn para definir a clase
@Tag agrupo operacións
@Operation describre cada operación
@Parameter descrige cada parámetro

## 5. Empaquetado e despregue

Un microserciso empaquétase xerando un ficheiro .jar que incluíra o entorno de execuión. O despregue consiste en executar o .jar na máquina destino. Execútase con
`$java -jar ficheiro.jar`
o jar con maven xenériase con
`nvm clean package`

## 6. Spring boot cloud

Os microservizos están penasdoa para seren usado e consumidos uns por outros. Spring Cloud é un conxunto de ferramentas que axudan no despregue e configuración deste entorno.
Eureca Server é o servizo onde se rexistran os microservizos para facilitar o seu descubrimento.
Ribbon. Libraría do lado do cliente que proporcina balanceo de carga no accesso a servizos.
Spring Cloud Config é o servidor que centraliza a configuración dun conxunto de servizos
Gateway é o punto de acceso único a un conxunto de servizos.
Servidor eureka: e a pean máis importarnte. Rexistra e descubre servizos permitindo a accesso a eles se coñecer a ubicación real e o porto. Trátase dun microservizo especial que requier a dependencia Eureka servar e cuxa clase main vai anotada con @EnableEurekaServer
no application.yml hai que definir varias propiedades
server.port: 8761
eureka.client:
registerWithEureka: false
fetch-registriy: false

Para que outros servizos podan resixtrarse ou descubrir microservizos ten que incorporar a dependencia de eureka. No ficheiro de configuraión hai que darlle un nome e establer a propideade serviceUrl.
Os servizos clientes que deben descubir outros servizos tamén deben incorporar a dependencia de Eureka. No método de creación RestTemplate debe esar anotado con @LoadBalanced. Isto usará Ribbon para que se conecte con Eureka e conectarse co servizo que se estableza. Os clientes tamén debe configuar Eureka no servizo no ficheiro de application. No servizo, a url que se usará é a que usa o nome de servizo e non a url real
de `http://localhost:8080/` para a `http:/user-service`

## 7. Utilización de Gateway

É un servizo que implmenta o starter de gateway e o cliente eurka que va ter que descubrir servizos.
No ficheiro de configuración de application ten unha entrada
spring.cloud.gateway default.filters:
globalcors:

para cada ruta
routes: - id: identificador
url: lb/servizo identificador
predicates\_ patas
filters:
-rewritepath:
a ruta do cliente será a do gateway localhost:porto/servizo/enponed
primeiro debe arrancar eureka

## 8. Servidor de configuración

Trátase dun servidor que centralia a información de configuración dun conxunto de servizos dentro dun repositorio git. Cada servido faille unha petición a este servidor de configuración. Este requere a dependencia ConfigServir e a clase main vai anotada con @EnableConfigServer.
Na propiedade Spring.cloud.config.server.igt.uri establécese a url do reposto

Cada microservizao incluirá a dependencia starter Config client e tame´n inflúe un ficheiro de configuración boostrap.yml co no me de servizo e a uri do servizo de configuración. No ficheiro aplicación agregáse a propiedade
spring.config.import.optional.configservir: url (p. ex. localhost:8888)

## 9. Desprege en contenedores docker

Cando se desprega un microservido xa inclúe o runtime de java. Hi que distingur entre a imaxe/paquete que inclúe o software necesario para o seu funcionamento e os contenedores que é unha instancia da imaxe.

### Comandos docker

`docker -v` mostra a versión de docker
`docker images` mostra unha lista de imaxes na máquina
`docker ps` mostra os contenedores en execución
`docker ps -a` mostra todos os contenedores na máquina
`docker run <image>` crea e arrinca un contenedor baseado nunha imaxe
`docker rmi <image>` elimina unha imaxe
`docker rm <contenedor>` elimina un contenedor

### crear imaxes

Para crear unha imaxe doker hai que crear un ficheiro dockerfile que lle di a docker como construír a imaxe. Está composto por una serie de comandos:
FROM indica a imaxe base
ADD ficheiros que incluír
EXPOSE porto a través do cal é accesible desde outros contenedores
ENTRYPOINT comando que deb ser executado para lanzar o contendor

### Contruír imaxe

Para construír unha imaxe execútase este comando
`docker build -t nome_da_imaxe ruta_dockerfile`
por exemplo
`docker built -t book-service .` (o docker file está no directorio actual, que se indica con punto)
Cando se executa doker rm hai pasarlle o mapeado de portos
`docker un -p 9000:8000` onde o primeiro é o porto do equipo e o seguindo o porto da imaxe
Para que un servizo que está a executar dentro dun contenedor poda ser descuberto a través de Eureka, debe rexistrare a través do nome / ip e porodo do equipo físico. Para isto configúrase as propiedades
eureka.instance.hostame=book-service
eureka.instance.non-secure-port=9000
