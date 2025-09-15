## Integrantes
- Cristian Eduardo Botina - A00395008
- Juan Manuel Marín - A00382037
- Óscar Andrés Gómez - A00394142

## Instalación del Servicio SSH
1. Máquina virtual iniciada

![[Pasted image 20250901144632.png]]

2. Actualizar sistema

![[Pasted image 20250901144916.png]]

3. Instalar SSH

![[Pasted image 20250901145017.png]]

4. Instalar programas clientes de suite de SSH

![[Pasted image 20250901145215.png]]

5. Crear cuenta adicional

![[Pasted image 20250901145328.png]]

6. Acceder al usuario

![[Pasted image 20250901150256.png]]

7. Verificar identidad del servidor

![[Pasted image 20250901150143.png]]

Es la misma que sale al sesión.

## Estudio del Handshake de SSH

1. Instalar Wireshark en Windows.

![[Pasted image 20250901151250.png]]

2. Iniciar captura de datos

![[Pasted image 20250901153001.png]]

3. Conectarse por Putty a máquina de Linux

![[Pasted image 20250901153339.png]]

4. Filtrar conexión por IP

![[Pasted image 20250901153518.png]]

### Preguntas
1. Busque los paquetes del protocolo SSH. De acuerdo con la explicación del profesor, ¿qué tipos de paquetes observa, y en qué orden? Incluya una captura de pantalla.

R/ Algunos de los paquetes que se observan son:

![[Pasted image 20250901153742.png]]

Es decir, dos tipos de paquetes:

- **TCP (3-way handshake)** → SYN, SYN-ACK, ACK (puerto 22).
- **SSH Protocol negotiation**:
    - Protocol version exchange.
    - Key Exchange Init (cliente y servidor).
    - Diffie-Hellman exchange.
    - New Keys.
    - Paquetes **encrypted** posteriores.

El orden es:
	1. TCP handshake
	2. intercambio de versiones SSH
	3. negociación de algoritmos
	4. intercambio de claves (DH/ECDH)
	5. confirmación con “New Keys”
	6. tráfico cifrado.

2. ¿Qué algoritmos de cifrado soporta el SERVIDOR? ¿En qué modalidades? ¿Qué algoritmos de autenticación de contenido soporta el servidor? Compare con los algoritmos de cifrado y autenticación de contenido soportados por el CLIENTE, y muestre las diferencias, si las hay. ¿Cuáles fueron los algoritmos de cifrado y autenticación elegidos finalmente en la negociación?

R/ Para ver qué algoritmos de cifrado soporta el servidor, expandimos la sección de protocolo SSH en el paquete **Key Exchange Init** enviado por el servidor.

![[Pasted image 20250901154921.png]]

El **servidor** soporta:

- **Algoritmos de intercambio de claves (KEX):** [curve25519-sha256@libssh.org](mailto:curve25519-sha256@libssh.org), ecdh-sha2-nistp256, ecdh-sha2-nistp384, ecdh-sha2-nistp521, diffie-hellman-group-exchange-sha256, diffie-hellman-group14-sha1.
- **Algoritmos de host key:** ssh-rsa, rsa-sha2-512, rsa-sha2-256, ecdsa-sha2-nistp256, ssh-ed25519.
- **Cifrado (encryption):** [chacha20-poly1305@openssh.com](mailto:chacha20-poly1305@openssh.com), aes128-ctr, aes192-ctr, aes256-ctr, [aes128-gcm@openssh.com](mailto:aes128-gcm@openssh.com), [aes256-gcm@openssh.com](mailto:aes256-gcm@openssh.com).
- **Autenticación de contenido (MAC):** umac-64/128, hmac-sha2-256/512 (con y sin modo ETM), hmac-sha1.
- **Compresión:** none, [zlib@openssh.com](mailto:zlib@openssh.com).

El **cliente** soporta:

- **KEX:** sntrup761x25519-sha512, mlkem768x25519-sha256, mlkem1024nistp384-sha384, mlkem768nistp256-sha256, curve448-sha512, curve25519-sha256, ecdh-sha2-nistp256, etc.
- **Host key:** ssh-ed448, ssh-ed25519, ecdsa-sha2-nistp256/384/521, rsa-sha2-512, rsa-sha2-256, ssh-rsa, ssh-dss.
- **Cifrado:** aes256-ctr, aes192-ctr, aes128-ctr, aes-cbc, rijndael-cbc, [chacha20-poly1305@openssh.com](mailto:chacha20-poly1305@openssh.com), aes128/256-[gcm@openssh.com](mailto:gcm@openssh.com), 3des.
- **MAC:** hmac-sha2-256/512, hmac-sha1, hmac-md5 (y variantes etm).
- **Compresión:** none, zlib, [zlib@openssh.com](mailto:zlib@openssh.com).

**Comparación:**

- El servidor ofrece un conjunto más reducido, priorizando cifrados modernos (chacha20, AES-CTR, AES-GCM).
- El cliente es más amplio, incluye algoritmos antiguos (3DES, MD5, CBC) y experimentales/post-cuánticos (sntrup, mlkem).
- Ambos coinciden en AES-CTR, AES-GCM, chacha20-poly1305 y HMAC-SHA2 → lo que permite la negociación.

**Algoritmos elegidos finalmente en la negociación:**

- **Intercambio de claves (KEX):** curve25519-sha256 (ECDH).
- **Host key:** normalmente rsa-sha2-256 o ssh-ed25519 (depende de tu servidor).
- **Cifrado:** aes128-ctr (cliente ↔ servidor).
- **MAC:** hmac-sha2-256.
- **Compresión:** none.

3. Con base en la información sobre el algoritmo Diffie-Hellman suministrada por el profesor, determine si en el handshake que capturó se empleó Diffie-Hellman tradicional, o Diffie Hellman de curvas elípticas. Si se empleó Diffie-Hellman tradicional, incluya capturas de pantalla donde se vean los parámetros P y G, y las claves públicas e y f. Si se empleó Diffie Hellman de curvas elípticas, incluya capturas de pantalla donde se vean el nombre del polinomio de curva elíptica empleado, y las claves públicas Q_C y Q_S.

R/ El handshake empleó Diffie Hellman de curvas elípticas, descrito en la columna "info". La clave Q_C se observa aquí:

![[Pasted image 20250901160533.png]]

Y la clave Q_S:

![[Pasted image 20250901160836.png]]

4. Analice el tráfico capturado. ¿Es posible ver la contraseña, o el texto retornado por el servidor en el momento del login?

No es posible, ya que los siguientes paquetes están encriptados:

![[Pasted image 20250901161048.png]]

Eso significa que SSH protege tanto la contraseña del usuario como el texto del login y del shell.

## SSH: Autenticación de Doble Factor con Clave Pública

### Configuración del servidor SSH

1. Acceder a la terminal y ejecutar `sudo nano /etc/ssh/sshd_config`

![[Pasted image 20250901161509.png]]

2. Quitar símbolo de comentario a las líneas descritas:

![[Pasted image 20250901161632.png]]

3. Reiniciar servicio de SSH

![[Pasted image 20250901161801.png]]

4. Abrir PUTTYgen para generar claves. Se siguieron los pasos descritos. Se utilizó la contraseña "password"

![[Pasted image 20250903094017.png]]

5. Abrir PUTTY para conectarse a la máquina de Linux

![[Pasted image 20250903094110.png]]

6. Crear directorio .ssh, darle permisos para que solo yo pueda acceder y entrar

![[Pasted image 20250903094213.png]]

7. Crear el archivo authorized_keys usando el comando `nano` y copiar y pegar el contenido de PUTTYGen

![[Pasted image 20250903094525.png]]

8. Grabar el archivo, aceptar el nombre y guardar

![[Pasted image 20250903094622.png]]

9. Dar permisos de lectura y escritura solo para el dueño y salir

![[Pasted image 20250903094724.png]]

## Uso del Par de Claves para la Autenticación

1. Acceder al archivo de la clave privada y digitar la contraseña

![[Pasted image 20250903095009.png]]

Pageant se minimizó correctamente.

2. Acceder a PUTTY y ensayar autenticación

![[Pasted image 20250903095242.png]]

La conexión se estableció automáticamente sin la necesidad de escribir la contraseña.

3. La guía explica el proceso para inhabilitar la autenticación por SSH para hacer el equipo más seguro, pero no se realizaron los pasos para no dificultar el desarrollo de la guía.

## Uso de WinSCP

1. Descargar WinSCP y abrir el programa

![[Pasted image 20250903100028.png]]

2. Introducir dirección IP y campo User Name. Ignorar la contraseña porque Pageant está corriendo. Entra sin problemas.

![[Pasted image 20250903100610.png]]
![[Pasted image 20250903100638.png]]

3. Observar información de la conexión con el comando Session | Server-Protocol Information

![[Pasted image 20250903100903.png]]

### Preguntas
5. ¿Qué algoritmo de cifrado están empleando su cliente WinSCP y el servidor Linux?

R/ Según la última pestaña a la que se accedió, ambos están usando el algoritmo AES-256 SDCTR (AES-NI accelerated).

6. Cree un archivo de texto en Windows, y transfiéralo a la máquina Lubuntu empleando WinSCP. Capture el tráfico de la sesión completa de WinSCP, empleando Wireshark. De acuerdo con la captura, ¿cuál protocolo de capa de aplicación se emplea para la conexión y la transferencia de los archivos?

R/ Se creó el archivo "texto.txt":

![[Pasted image 20250903101804.png]]

Se transfirió el archivo con el WireShark capturando:

![[Pasted image 20250903101955.png]]

En el WireShark, se observan los siguientes paquetes transferidos entre ambas máquinas virtuales:

![[Pasted image 20250903102156.png]]

El protocolo usado para la transferencia de paquetes es el SSH. En la ventana anterior de "Server and protocol information" de WinSCP, se especificó que el protocolo usado para transferencia de archivos es el SFTP-3. Cuando accedemos a uno de los paquetes, observamos un envío de información al puerto 22 usando SSH, lo que confirma el uso del protocolo mencionado.

![[Pasted image 20250903142458.png]]

Fuente para justificar el uso del protocolo: [router-proxy-firewall - How to do a SFTP Packet Trace using Wireshark? | DaniWeb](https://www.daniweb.com/hardware-and-software/networking/threads/456646/how-to-do-a-sftp-packet-trace-using-wireshark)

7. Más allá de los paquetes iniciales del intercambio, ¿es posible ver algo más de texto plano en la comunicación? (por ejemplo, algo del texto que escribió en el archivo). Finalmente, ¿qué podría concluir con respecto a la seguridad del protocolo?

R/ No es posible ver ningún texto relacionado con el archivo enviado ni los comandos del protocolo, ya que todo el contenido se cifra antes de transmitirse.  
Sin embargo, sí se puede observar información de red como las direcciones IP de origen y destino, el puerto, los tamaños de los paquetes y los algoritmos de cifrado usados.

Se concluye que, aunque un tercero pueda capturar el tráfico entre los equipos, no podrá acceder al contenido del archivo ni a los comandos de transferencia, lo que demuestra que el protocolo proporciona confidencialidad y seguridad en la transmisión.

## SSH: Autenticación de Doble Factor con Token por Software
1. Ingresar a la cuenta y eliminar el archivo "authorized_keys"

![[Pasted image 20250903105220.png]]

2. Salir y tratar de ingresar de nuevo. Se solicita nuevamente la contraseña para ingresar

![[Pasted image 20250903105322.png]]

3. Entrar al usuario user (con permisos de administrador) y actualizar el sistema. Instalar librerías y paquetes solicitados

![[Pasted image 20250903105708.png]]

4. Se ejecutaron todos los comandos solicitados

```sh
mv master.zip googleauth.zip
unzip googleauth.zip
cd google-authenticator-libpam-master
./bootstrap.sh
./configure
make
sudo make install
cd
```

![[Pasted image 20250903105921.png]]

5. Comprobar instalación

![[Pasted image 20250903110049.png]]

6. Editar archivo de configuración de PAM-SSH y SSH_CONFIG

![[Pasted image 20250903110419.png]]

![[Pasted image 20250903110556.png]]

7. Crear link al módulo PAM de Google Authenticator. Se ejecutaron los comandos:

```sh
sudo mkdir /lib/security sudo ln -s /usr/local/lib/security/pam_google_authenticator.so /lib/security/pam_google_authenticator.so
```

8. Iniciar sesión en el otro usuario y ejecutar el comando `google-authenticator`

Tras seguir los pasos de la guía, se obtiene correctamente el QR, se inserta la clave privada en una app de autenticación y se escribe el código de la app de autenticación

![[Pasted image 20250903113920.png]]

Aparecen los códigos de emergencia y se termina de configurar.

9. Se intenta acceder por PUTTY al sistema y se escribe el código de verificación de la app

![[Pasted image 20250903114152.png]]

Se logra acceder correctamente ingresando el código y la contraseña del usuario, ofreciendo así doble verificación.

### Preguntas
8. Mencione dos ventajas y dos desventajas de este sistema de autenticación.

R/ Ventajas:
- Aumenta significativamente la seguridad, pues combina contraseña más el token dinámico.
- El código cambia constantemente, reduciendo el riesgo ante robo de credenciales.

Desventajas:
- Requiere que el usuario tenga siempre el dispositivo con la app de autenticación.
- Si se pierde o daña el dispositivo y no se guardaron los códigos de emergencia, el acceso puede bloquearse.

9. Conclusiones

R/ El laboratorio permitió comprobar la importancia de SSH como protocolo seguro frente a alternativas obsoletas como Telnet. Mediante el uso de Wireshark capturamos y analizamos el handshake, verificando la negociación de algoritmos de cifrado e integridad, y constatamos que ni credenciales ni archivos quedan expuestos en texto plano. Con PUTTY se realizaron las conexiones SSH y con PUTTYgen se generaron claves públicas y privadas para implementar autenticación robusta. También se empleó WinSCP para transferir archivos usando SCP y SFTP, confirmando que la transferencia se realiza de manera cifrada. Finalmente, con Google Authenticator configuramos la autenticación de doble factor basada en TOTP, demostrando cómo se refuerza la seguridad del acceso remoto. Por lo tanto, la práctica mostró que la combinación de SSH con autenticación multifactor y herramientas adecuadas constituye un entorno confiable y resistente frente a ataques de intercepción.

10. ¿Qué aprendieron en este laboratorio?

R/ Aprendimos a instalar y configurar SSH en Linux, y a conectarnos desde Windows usando PUTTY, entendiendo en detalle el proceso de autenticación y el establecimiento de una conexión segura. Aprendimos a utilizar PUTTYgen para generar pares de claves y omitir la autenticación tradicional por contraseña agregando un archivo de autenticación. También exploramos la transferencia segura de archivos mediante WinSCP, validando el uso de protocolos SCP y SFTP, validándolo con el uso de Wireshark. Finalmente, aprendimos a configurar Google Authenticator como segundo factor de autenticación, comprobando la utilidad de los códigos dinámicos de un solo uso desde la App de autenticación. En conjunto, el laboratorio nos enseñó a usar herramientas de administración y análisis de red en escenarios prácticos de ciberseguridad, afianzando los conceptos teóricos de cifrado, autenticación y confidencialidad en comunicaciones remotas.