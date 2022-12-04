# FICHEIROS BATCH


Borrar directorio recurrentemente
    `RD /S directorio`


## REFERENCIA DE COMANDOS

### 0. CONSOLA

`CLS`. Borra a pantalla.

### 1. SISTEMA

`ASSOC`. Mostra as asciacións entre tipo de ficheiros.

`CHKDSK [!volume]` Comproba o disco e mostra un informe de estado. Admite  `/F` corrixe erros en discos, `/R` encontra sectores defectuosos e recupera información, `/X` desmonta a unidade previamente

`DEFRAG [volumes] [operacións] [opcións]`. Realiza a defragmentación do volume que se indique.

`DRIVERQUERY`. Mostra os controladores do equipo. Admite o parámetro `-V`para obter máis información.

`POWERCFG`. Rastrexa o uso de enerxia da computadora.

`SCHTASKS`. Accede ao Programador de tarefas.

`SFC`. **Necesita privilexios**. Examina a integridade de todos os ficheiros do sistema protexidos e reempraza as versións incorectas polas correctas. Admite `/SCANNOW` examina a integridade de todos os ficheiros protexidos do sistema e repara os ficheiros con problemas, `/SCANFILE [file]` examina a integridade do ficheiro referenciado e o repara de se detectar problema, `/VERIFYLE [file]` examina a integridade do ficheiro referenciado, `/VERIFYONLY` examina a integridade de todos os ficheiros do sistema, pero non realiza ningunha comprobación.

`SHUTDOWN`. Programa o apagado do equipo. Admite `/R` reinicia o equipo,  `/S` apaga o equipo,  `/T [00]` especifica o tempo de espera antes do apagado (en segundos).

`SYSTEMINFO`. Mostra a información de configuración do sistema operativo.

`TASKKILL`. Forza a detección dun proceso. Admite  `/IM [name]` para especificar o nome do executable, `/PID [id]` para especificar o id do proceso.

### 2. TRABALLO CON FICHEIROS

`DIR`
`dir *node_modules* /AD /b /s > node_modules.log`. Busca as carpetas que inclúan "node_modules" na súa ruta e garda a saida nun fickeiro

`FC [options] [file 1] [file 2]`. Compara dous ficheiros ou conxuntos de ficheiros e mostra as diferenzas entre eles. Adminte `/B` mostra a saída binaria,  `/C` omite a distinción entre maiúsculas e minúsculas,  `/L` compara ficheiros en texto ASCII, `/U` compara ficheiros en texto Unicode.

### 3. REDES

`GETMAC`. Obtén a dirección MAC do equipo.

`IPCONFIG`. Mostra a configuración de rede do equipo. Admite `/ALL` para mostrar información detallada, `/FLUSDNS` para actualizar a dirección DNS, `/RELEASE` para liberar as conexións, `/RENEW` para renovar a IP asignada.

`NETSTAT`. Mostra a lista de portos abertos e as direccións IP relacionadas.

`PING`. Fai ping contra un dominio ou IP para comprobar a conexión.

`PATHPING`. Fai un ping avanzado contra un dominio ou IP para comprobar a conexión.

`ROUTE [-f] [-p] [-4|-6] command [destination] [MASK subnetmask] [gateway] [METRIC costmetric] [IF interface]`. Manipula a táboa de enrutamento. O parámetro `-f` borra as táboas da porta gateway, `-p` persiste a táboa. `command` admite `print`, `add`, `delete`, `change`.

`TRACERT`. Fai unha traza do paquete enviados rastrexando canto tempo toma o salto en cada servidor.


buscar os ficheiros de node_modules
  `FOR /d /r . %d in (node_modules) DO @IF EXIST "%d" echo %d"`

eliminar os ficheiros de node_modules
  `FOR /d /r . %d in (node_modules) DO @IF EXIST "%d" rm -rf "%d"`
