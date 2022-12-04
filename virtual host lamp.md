CREAR HOST VIRTUAIS EN LAMP (Debian)

DIRECTORIOS
1.- Crear a estrutura do directorio. O o parámetro -p crea os directorios intermedios que non existen na ruta
$ sudo mkdir -p /var/www/html/dominio.local

PERMISOS
2.- Outorgar permisos: -R recursivo, para os subdirectorios. $USER toma o usuario regular. Usuario e grupo. 
$ sudo chown -R $USER:USER /var/www/html/dominio.local
$ sudo chmod -R 755 /var/www/html/dominio.local

HTML
3.- Crear paginas de proba 
$ nano var/www/dominio.local/index.html

CREAR FICHEIRO DE VHOSTS
4.- Crear un novo ficheiro de virtual host. Por defecto existe un 000.default.conf. Copiamos e pegamos 
$ sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/dominio.local.conf

EDITAR FICHEIRO VHOSTS
5.- Editamos con permisos de root
$ sudo nano /etc/apache2/sites-available/dominio.local.conf

temos algo así: 
<VirtualHost *:80>
    ServerAdmin webmaster@localhost 
    DocumentRoot /var/www/html/html
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

debería quedar así
<VirtualHost *:80>
    ServerAdmin admin@dominio.local 		# email válido 
    ServerName dominio.local 				# dominio base
    ServerAlias www.dominio.local 			# denominación alternativa
    DocumentRoot /var/www/html/dominio.local 	# directorio do dominio
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

HABILITAR VHOSTS
6.- Habilitar os ficheiros de host virtual
$ sudo a2ensite dominio.local.conf

DESHABILITAR VHOSTS
7.- Deshabilitar o ficheiro por defecto
$ sudo a2dissite 000-default.conf

REINICIAR
8.- reiniciar Apache
$ sudo systemctl restart apache2

CONFIGURAR DNS HOST
9.- Configurar o ficheiro hosts local. En caso de usar un dominio non rexistrado (local ou en lan), hai que configurar o equipo para que o recoñeza 
$ sudo nano /etc/hosts

engadir ip e nome de dominio
127.0.0.1 dominio.local


INSTALAR CERTIFICADOS SSL LAMP EN LOCAL

ACTIVAR O MÓDULO SSL 
1.- Activar o módulo SSL
$ sudo a2enmod ssl

2.- Reiniciar apache
$ sudo systemctl apache2 restart

CERTIFICADO AUTOASINADO
3.- Crear o directorio
$ sudo mkdir /etc/apache2/ssl

4.- Crear chave e certificado con open ssl
$ sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt

CONFIGURAR APACHE
5.- Editar default-ssl.conf
$ sudo nano /etc/apache2/sites-available/default-ssl.conf 
debe quedar algo así:

<IfModule mod_ssl.c>
	<VirtualHost _default_:443>
		ServerAdmin admin@example.com
		ServerName localhost
		ServerAlias localhost
		DocumentRoot /var/www/html
		ErrorLog ${APACHE_LOG_DIR}/error.log
		CustomLog ${APACHE_LOG_DIR}/access.log combined
		SSLEngine on
		SSLCertificateFile /etc/apache2/ssl/apache.crt
		SSLCertificateKeyFile /etc/apache2/ssl/apache.key
		
		<FilesMatch "\.(cgi|shtml|phtml|php)$">
			SSLOptions +StdEnvVars
		</FilesMatch>
		<Directory /usr/lib/cgi-bin>
			SSLOptions +StdEnvVars
		</Directory>
		BrowserMatch "MSIE [2-6]" \
			nokeepalive ssl-unclean-shutdown \
			downgrade-1.0 force-response-1.0
			BrowserMatch "MSIE [17-9]" ssl-unclean-shutdown
	</VirtualHost>
</IfModule>


6.- Activar o host virtual
$ sudo a2ensite default-ssl.conf

7.- Reiniciar apache
$ sudo systemctl apache2 restart


CONFIGURARACIÓN DUN PROXY EN APACHE para ssl
1.- Habilitar os módulos de apache.
	sudo a2enmod proxy_http

2.- Reiniciar apache
	sudo /etc/init.d/apache2 

3.- Establecer a entrada do proxy inverso
	sinxelo
	A directiva ProxyPass especifica o mapeo de peticións entrantes ao servidor

		ProxyPass "/" "http://localhost:port"
		ProxyPassReverse "/" "http://localhost:port"