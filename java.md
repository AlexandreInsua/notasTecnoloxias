# JAVA

## INSTALACIÓN

### Instalación en Windows

#### Instalación automatizada

A instalación automatizada faise mediante a descarga do instalador da web de Oracle na ligazón [https://oracle.com/technologies/downloads](https://oracle.com/technologies/downloads). Para uso persoal o JDK segue a ser gratuíto. Descárgase o instalador msi e instálase. 

Para comprobar que se realizou a instalación correctamente, ábrese unha terminal e execúse o comando `java -version` ou `javac -version`. O primeiro executa o ficheiro jar e o segundo o executable do compilador.

Cando hai instaladas varias versións, hai que configurar as variables de sistema seguindo os pasos da instalación manual.

#### Instalación manual

Descárgase o ficheiro comprimido da web de Oracle ou a versión openJDK [https://jdk.java.net](https://jdk.java.net). O ficheiro descomprímese nun lugar adecuado. Recoméndase en `C:\Program Files\Java`.

A continuación, hai que agregar a versión de Java ás variables de entorno. Debe ter o nome JAVA_HOME e o valor `C:\Program Files\Java`. Ademais, hai que agregar unha nova entrada na variable PATH co valor `C:\Program Files\Java\bin`

#### Desisntalación

A desinstalación estándar realízase desde  agregar e quitar programas.

### Instalación en Linux (Ubuntu)

https://www.solvetic.com/tutoriales/article/8641-desinstalar-java-en-linux/
https://www.compuhoy.com/respuesta-rapida-como-desinstalar-java-en-linux/
https://miracomosehace.com/desinstalar-java-linux-eliminar-archivos/
https://www.enmimaquinafunciona.com/pregunta/23856/como-desinstalar-completamente-java
https://www.enmimaquinafunciona.com/pregunta/23341/como-puedo-instalar-java
https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-on-ubuntu-20-04-es
https://www.oracle.com/java/technologies/downloads/#java17
https://novicestuffs.wordpress.com/2017/04/25/how-to-uninstall-java-from-linux/
https://www.makeuseof.com/install-java-ubuntu/
https://linuxhint.com/uninstall-java-ubuntu/
https://fedingo.com/how-to-uninstall-java-in-ubuntu/



#### Instalación manual

#### Desinstalación

Borrar Java do sistema
`sudo apt remove default-jdk default-jre` borrar o JDK e o JRE de sistema. 

Obter os paquetes jdk 
`dpkg --list | grep jdk`

Borrar os paquetes
`sudo apt remove <nome do paquete>` por exemplo `sudo apt remove jdk-11.0.10`


