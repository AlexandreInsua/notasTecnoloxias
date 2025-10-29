# HACKING ÉTICO

## 1.Introdución

### 1.1. Conceptos básicos

- Aplicación web. Ferramente de software que lle permite aos usuario interactua a través dun navegador cun servidor. Non necesitan ser instaladas. A información é persistida no servidor.
- URL. Direción única para identificar un recurso. Consta de protocolo + host + ruta
- Arquitectura cliente-servidor. Funciona mediante peticións e respostas.
- Capas de presentación. Cliente.
- 2ª capa de servido con lóxica de negocio.
- 3ª capa procesamento da información.
- Métodos, verbos HTTP, protocolo HTTP: get + params, post + body, put, patch, delect, options, head, options
- Códigos de resposta: 1xx informcion, 2xx correcta, 3xx redireccion, 4xx incorrecta, 5xx errors
- Formato de petición e resposta. Método + protocolo, hosto, user agent, cabeceiras e coockies, protocolo e código, cabeceiras, corpo

### 1.2. tipos de auditoria

Criterios e obxectivo
Caixa nega: trata de simular un ataque exterior e parte só dunha url
Caixa gris: intermedia
Caixa branca: simula un ataque interior con información de baixo nivel da aplicación. Rara

### 1.3. Fases de auditoría

0. Planificación. Define as características
1. Recolección da información. Pasiva: a través de fontes públiccas, Activa: interactúa co obxecto (url), Técnicas OSINT
2. Exploración de vulnerabilidades. Confirmar vulnerabilidades: executar ataques para comfirmar feblezas. Buscar e explotación de vulnerabilidades e obtención de evidencias.
3. Elaboración do informe. Resumo de achados. Informe executivo de algo nivel non técnico, informe técnico de baixo nivel e detalle e evidencias, reproducións e solucións a vulnerabilidades.

### 1.4. OWASP

Open web application security project.
Proxectos: OWASP top ten (2017), Web security testing guide 2020. 12 categorías, 47 controis.

#### OWASP top ten (2017)

- 1. Inxección en puntos de interación co usuario onde envia un string nos puntos de interacións (inputs, urls..)
- 2. Perda de autenticación. Acceso non autorizado nas app con parte privada.
- 3. Exposión de datos sensibles en transporte ou almacenamento.
- 4. Entidade externa de XML. Inserir contido malicioso en XML (tamen en SOAP).
- 5. Perda do control de acceso. Autorización. Pódese accer a operacións para as que non se ten permisos.
- 6. Configuración de seguridade incorrecta.
- 7. Secuencia de comandos de sitions cruzdos (XSS). Cross sitting scripting, inxección de javascript malicioso
- 8. Deserialización insegura.
- 9. Uso de compoñents con vulnerabilidaddes coñecidas. Dependencias.
- 10. Rexistro e monitoreo insuficiente.

## 2. Recoñecemento da web

### 2.1. Estrutura da web

1. Ficheiros por defecto.
   Os ficeiros por defecto propocional información sobre directorios e subdirectorios da web. Son exemplos destes ficheiros por defecto todos aqueles que se poden encontrar de xeito público e que están presentes por defecto. Os máis habituais son robots.txt, sitemap.xml, humans.txt, security.txt.

2. Descubremento de directorios a través de ficheiros. robots.txt filra directorios para que non sexan indexados polos robots. Soe ser accesible através de domain/robots.txt. Os admins poden limitar o acceso a este recurso. Sitemap.xml ten a mesma función, pero en apps xml, accesible en domain/sitemap.xml. Security ten informaciónd de seguridade e humans.txt de desenvolvmento.

3. Descubremento de directorios a través de métodos http. Averiguar que métodos soporta o servidor. Unha peticion OPTIONS facilita inforamción, tamén TRACE. Hai un script en bash para probar cada método. Isto permite determinar a partir do código de respos para descubrir por forza bruta o map da web.

#### 2.3. Crawling.

Analizar o comportamento da páxina baseando en redireccions e analizando as urls presents no código fonte. É una forma de web scrapping.

#### 2.4. Finger printing

Obter información en base ao que nos mostra. Analizar o código fonte: comentarios, tecnoloxías usadas, librarías usadas, funcionalidades, lóxica da aplicación do lado do cliente. Analizar os metadados dos ficheiros públicos. Podemos obter usuarios de dominio, sistema operativo, etc. Ferramenta FOCA. Outra técnia é a traves das respostas do servidos e das súas cabeceiras. Mediande un curl ou un proxy de aplicacións como BURP.

#### 3.5 mensaxes de erro

Poden supoñer un filtro de información. Accesos non autorizados, uso de tipos non esperados, caracteres non agardados, números de parámetros.

### 2.2. Canal de comunicación

1. Securizar o canal do lado do servidor. O protocolo HTTP usa en claro e non ten mecanismos para evitar que sexan interceptados. Porto 89 e man in the midle. O protocolo HTTPS usa o porto 443 e implementa un mecanismo de cifrado. Estes non impiden o man in the midle, especialmente cos certificados auto asinados ou por unha autoridade non recoñecida.

2. A primeira petición a un dominión é hattp e o servidor responderá con https e coa cabeceira Strict Transport Security. Un MIM pode eliminar esta cabeceria para que o cliente siga enviando peticións http.

3. Criptografía simétrica. Existe unha única chave K que se utiliza para descifrar e cifrar. O problema consiste en compartir esta chave.

Critografía asimétrica de chave publica e privada. A pública cifra e a privada descrifa. Un usuario comparte a súa clave para para que lle podan mandar mensaxes cifradas que logo el pode descifrar usando a clave privada. É un sistema que garante a confidencialidde, integridade autenticadión e non repudio da información.

Outra técnica asimétrica consiste en alterar a orde mensaxes de tal xeito que sae envia unha mensaxe coñecida xunto cifrado coa clave pública para desencriptar a mensaxe. O modelo misto emplica dous pasos diferenciados. O primeiro paso úsae a asimétrica para cifrar unha chave que se utilizará no resto da comunicación de xeito simétrio.
A infraestrutra de clave pública é un conxundo de árbores con entidades universalmente recoñecidas, entidades intermedias e entidades finais que asinan e verifican certificados. Un certificado dixital e´unha chave pública asinada por unha entidade certificadora.

4. TLS handshake é un protocolo de comunicación cliente servidor para realizar esta comunicadión cifrada que soporta o certificado. Durante esta comunicación, compártese o certificado, os algoritmos de cifrado e as chaves privadas. Existen vulnerabilidades asociadas a algoritmos de cifrado. Existen ferrametnas para recuperar as vulnerabilidades dun seridor.

### 2.3. Xestion de identidades.

Autenticación: acceso á parte autenticada (privada) dunha aplicacion.
Autorización: proceso que permite verificar que un usuario cumpre os requisitos para accer a determinados recursos.
Perfil ou rol: atributo de identificacón dun usuario basado nas súas accións, permisos ou nivel de privilexios.

O proceso de autenticación pode efectuarse a trafés dun formulario mediante credenciais, certificados dixitais, apikeys, tokens de autenticación, etc...
Nos paneiw de autenciano non hai que mostrar excesiva información para evitar ataques de forza brutra contra logins.

Contrasinais. Considérase un contrasinal forte cnado inclúe máis de 8 caracteres alfanuméricos e carantes especiais que non se reutilicen. Hai que evitar contrasinais habituais. Activar 2FA. Controlar o proceso cando se cambia a passwor e sempre pedir a orixinal.

Spraging. Próbase unha passwor par todos os ususarios.

Cookies. Http non almacena o estado das peticiós. Para ito utilízanse as cookies de sesión e poden identificar usuario e petición. Cando o cliente realiza a primeira petición reciba na responsta unha cookie que o identifica e se inclúe nas subseguitnes peticións.

Interceptación de sesion (Hijacking) Un MIM pode interceptar cookies de sesión con ataques XSS ou Web-cache. O método TRACE é vulnerable.

Filtración de sesión. O servidor acepta cookies creadas polo usuario e non reasigna a cookie de sesión en cada iteración. As cookies deben ter os atributos secre e httponly para que só se podan enviar en canais cifadas e en peticións http e non con javascript.

Web cache. Os datos sensibles permanence na chache do navegador. Existen cabeceira que envían ao servido para que non cachee a información sensible.

Fallos de atuorización. Hai que centrarse nos roles. Podemos encontrar fallo de autorización horizontal, no mesmo nivel de autorización. Un fallo de autorización vertical será o acceso a rercursos deferentes do seu nivel.
IDOR é un tipo de autorización que consiste en acceder a outros recursos a través de ids correlativas.

Methos overidind. Cambiar o método http para ober a info dun recurso.

## 3. Explorando vulnerabilidades

### 3.1. Conceptos previos

Toda entrada e susceptibe de ser un vector de entrada. Por tanto, hai que identificar os posibles vectores de entrada, entender o impaco que puider ter unha vulnerabilidades de ser explotada con éxito e entender as contramedidas que se poden tomar para conxurar as ameazas. As diferentes vulnerabilidades poden agruparse en varios grupos:

- Erros de configuración da app web.
- Erros de configuración do servidor da app.
- Falla de validación de parámetros de entrada.
- Exposición de información sensible.
- Manexo incorreco de excepción e erros
  Traba con BurpSuit. Kali linxu xa a integra.

### 3.2. Validación de datos

Para poder su BurpSuite configura un proxy e logo no navegador en settings, navigator.

### 3.2.1. SQL injection

É una vulnerabilidade que lle permite ao atacante inxectar instrucción SQL de xeito malicioso dentro do código SQL programado para a manipulación da base de datos. A finalidade deste ataque é poder modificar o comportamento das consultas a través de parámetros non desexados. Podendo falsificar identidades, obter e divulgar infomación da base de datos ou alterar a estrutura da base de datos, ser administrador...
A causa é a mala filtración das variables ou parámetros de entera e as consecucias son a fuga de información, a execución de comandos e a alteración da base de datos.
Pódese explotar inxectando un parámetro de appliación ou en formularios de rexisto, busca, etc.
Temos a técnica da tautoloxía `'or '1'='1`, `'or 1=1--`, pódes facer con GET ou POST

- SQLi - in band. Realízase a consulata sql sen romper a consulta orixinal sen romper a consulta orixinal usando operadores como a unión. Necesitamos saber o número de columnas, o tipo de datos de cada columna e require ensaio para deterimar o tipo de columnas.
- SQLi- out band. Inxección onde a resposta á consulta obtense por un canal diferente ad da inxección. Baseda en error. o dbc que mostra a app web. Provócase forznado un erro de tipado.
- SQLi Bind injection- boolean-based. Inxección baseada en expresións booleandas que nos indican que a url responde estas inxeccións e asúa vez produce cambios na app como se tal se son verdadeiras.
- SQLi time based.- Inxección basada en realizar un busca dicotómica dos datos almacenados na bd baseada en tempos de resposta que ofrece a app en función da validez da consluta.
- SQLi time based using heavy queries - Inxección baseada no tempo pero con funcións extensivas en cómputo que xeral un retardo en tempo.

Sqlmap é unha ferramenta en pyton qpara realizar ataques sqli automatizso.

### 3.2.2. OS command injection (shell injection)

Vulnerabilidade que permite a execución de comando arbitrarios do so no sercidor que está executando a app e que pode comprometer completamente a app e todos os seus datos. Débes a un filtrado incorrecto do caracteres introducidos polo usuario que permita a contatenación de comandos executados. Permite acceder a ficheiros sensibles, acceder e modificar configuracións, fugas de información ou execución de comandos.

### 3.3.3. Cros site scripting (XSS)

Cross site scripting (XSS) constitúe un tipo de inxeccion de código JavaScript (VBSCript, ActiveX, HTML, etc) que ten como obxectivo non atacar a máquina que presta o servixo, senón o resto de usuarios que accen a ditos servizos web, utilizando como pasarela unha aplicación vulnerable que se seá a executar no servizo implicando. Consíguese executar código no cliente. A principal causa é un filtrado incorrecto nos parámetros de entra que envía o usuario. O atacante envía un código malicioo na app e cando un usuario visita a app execútase no navigador do usuaro lexítimo. O impacto é o roubo de cookies, modificación do funcionamento da web, afectacón da imaxe, redireccionamento a sitios maliciosos.

- XSS tipos reflexado. É indirecto e non persitente por que non queda almacenada no servidor, só se executa no cleinte e pode tratar de enganar á vítima.
- XSS almacenado. O código inxectado é interpretado nun cliente pero ademási almacénase no navigador e vai propagar o ataque a moitos usuarios. Por exemplo, nun hentrada de Post
- XSS - DOM. En ningún momento interven o servidor. Dentro do DOM o .write, .location, .URL, e .referer son sen sensible a este tipo de ataque.

### 3.3.4. File inclusión

É unha vulnerabilidade que afecta com maior frecuencia ás app que dependen do tempo de execución. Prdúcese cando unha aplicación crea unha ruta de acceso ao código executable usando unha variable controlada polo
atacante de xeito que lle permite controlar que ficheiro se executa en tempo de execución de scripts.

- Local File Inclusion (LFI). Permite executar ficheiros localmetne no servidor e ter acceso a ficheiros de configuración, passwords, etc, usando como entrada algún parámetro da entrada. Por exemplo, executar `/etc/password` no serviod e mostralo na web.
- Remote File Inclusion (RFI). Permite o enlace ficheiros remota denr do servido para aquelas app que permite executar ficheiros remotos, comando uc de shell.

### 3.3.5. XML External entity (XXE)

Vulnerabilidade que presentan as apps web que aceptan contido XML input. Este ataque acepta referencias a entidades XML externas e estan son procesadas.
O posible impacto é acceso a información sensible, acceso a configuracion se sistema, execución remos ta comandos e denegación de servizos. Esta vulnerabilidade está baseada no uso de entidades a través do Document type definition e a entidades personalizadas.

- XXE envio de peticións xml. Enviaránse unha ptición embebida dentro dun ficheiro xml.

### 3.3.6. Subida de ficheiros

Vulnerabilidade que consiste en aproveitar a funcionalidde de subir ficheors para subir ou acceder a calquera tipo de ficheiros.
Pódese subir un ficheiro con extensión de fonte, modificar o content-type. ou modificar o contido do ficheiro.

## 3.3. Vulnerabilidade web

### 3.3.1. Cross site requetes forgery (CSRF)

Falsificar petición de sitios cruzados. Consiste en engañar a un usuario para que execute peticións sen o seu consetemento. Par isto necesitamos unha app con parte privada. Implica enxeñería social

### 3.3.2. Clickjacking

Superposición dun elemento iframe sobre outro co fin de captura o click dun ususrio sen que este sexa consciente coa fin de provocar unha acción non desexada por parte do usuario.

### 3.3.3. Lóxica de negocio

Esta técnica consiste en analizar a lóxica de negocio da appp para identificar e explotar posibles puntod e inxección, comprobar as validacións de datos no servidor e no cliente e observar o seu comportamento.
