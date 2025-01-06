# OWASP PROACTIVE CONTROLS

(Open Web Application Security project)

Trátase de boas prácticas para manter a seguridade dunha aplicación web.

## Control de seguridade (security control)

Cando falamos de control de seguridade, salvagarda ou contramedida referímonos a aquilo que hai que evitar, detectar, contrarrestar e minimizar problemas de seguridade.
Os controis de seguridade da aplicación axudan os desenvolvedores a escribir código seguro.
Os controis proactivos OWASP é una lista priorizaa de técnicas de seguridade e guías.

### 1. Verificación temperá (verify for security early and often)

Hai que incluír os test de seguridade como parte dos tests. Un factor que agrega seguridade é o despregamento continuo. Hau unha guía para definir requisitos de seguridade. Primeiro defínese e logo automatízanse os tests prara poder chegar a CI/CD.
Behavior-Driven Development (BDD) It's a security-testing framework. Usa una linguaxe natural para definir os test (given, when, then). Automtiza tests de seguridade, combina varias ferramentas de seguridade.

### 2. Consultas parametrizadas (parametrize queries)

Está relacionado coa inxección de consultas sql con contido malicioso a través de datos de entrada dunha aplicacion. A técnica de prevención consiste na parametrización de consultas impedindo que se executen comandos sql maliciosos. O punto é que os parámetros están tipados e nun executarán comandos.

### 3. Codificar datos

En todo momento estamos a recibir datos dun usuario. Hai que codificalos para previr a execución de scripts maliciosos. Hai que sanitizar estas entradas.

### 4. Validar inputs

Hai que considerar todos os inputs como maliciosos e validalos. Iso inclúe headers, cookies, get, post, parámetros, etc...
Todo pode ser manipulado por un atacante (incluíndo a mesma url). Os riscos máis habituais son a inxección sql, crosss siting scripting, redirecións, inputs, utilizar sanitizadores. Pensar en que ataques se poderían dar.

### 5. Controles de Identificación (autenticación) e autorización

Hai que controlar el crackeo de passwors. Hai que implementar 2F , preguntas de seguridade, enviar código, controlar as sesión, forzar cambios de password, etc...

### 6. Implementar controles de acceso

Hai que forzar todas as peticións a verificar o control de acceso. Implementar a denegación por defeto, evitar os hardcodeos e comprobar no servidor cando se accede a una feature. Rol e petición de autorización.

### 7. Protexendo os datos

Hai que encriptar os datos en transito (https) confidenciais, integros auténticos.
Configuración sts (strict transport security). Forzar peticións https. Pining de certificado. TOFU trust on first use.

### 8. Loginng e instrusión

Usar o login para detectar intrusions.

### 9. Uso de frameworks e librerías

Convén non reinventar a roda.

### 10. Captura de erros e excepcións

É boa práctica centralizar o tratamento de excepcións. Hai que evitar mostrar información de erros que se podan aproveitar para realizar ataques.
