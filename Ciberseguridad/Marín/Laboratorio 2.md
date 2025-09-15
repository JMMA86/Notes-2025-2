## Integrantes
- Cristian Eduardo Botina - A00395008
- Juan Manuel Marín - A00382037
- Óscar Andrés Gómez - A00394142

## Creación De Una Autoridad De Certificación
IP de máquina virtual: 10.0.2.15
Contraseña utilizada para la passphrase: password

Después de seguir todos los pasos, se crearon dos archivos:
- `ca.crt`: Certificado de clave pública de la CA
- `ca.key`: Clave privada de la CA

El contenido del certificado es un conjunto de mucha información y direcciones:

![[Pasted image 20250908143942.png]]

## Creación del Certificado del Servidor
Se generaron los siguientes archivos:

- **server.key**: Clave privada del servidor (protegida inicialmente con passphrase).
- **server.csr**: Solicitud de certificado del servidor, contiene la clave pública y la información de identidad.
- **server.crt**: Certificado del servidor, firmado por la CA y válido por un año.
- **server.key.secure**: Versión protegida de la clave privada.
- **server.key**: Versión sin passphrase de la clave privada (para uso directo en Apache).

El certificado incluye como **Common Name (CN)** la dirección IP del servidor.

![[Pasted image 20250908145137.png]]

## Generación de una Versión Insegura de la Clave Privada del Servidor
Se creó una versión sin passphrase de la clave privada para evitar tener que digitar la contraseña cada vez que arranque el servidor web.

Archivos resultantes en el directorio de trabajo:

- **server.key.secure**: Clave privada protegida con contraseña.
- **server.key**: Clave privada sin protección (para uso directo en Apache).

![[Pasted image 20250908145440.png]]

# Instalación Y Configuración De Apache Como Un Servidor Web Seguro
- Se instaló **Apache2** en la máquina virtual.
- Se creó el directorio `/etc/apache2/ssl` y se copiaron allí los archivos del servidor:
    - `server.key` (clave privada insegura)
    - `server.crt` (certificado firmado por la CA)

- Se habilitó el módulo SSL (`a2enmod ssl`) y se deshabilitó la compresión (`a2dismod -f deflate`).
- Se activó la configuración de sitio seguro (`default-ssl.conf`) y se modificaron los parámetros:
    - **ServerName** y **ServerAdmin** con la IP del servidor.
    - Rutas a `server.crt` y `server.key`.

- Se creó un archivo **index.html** de prueba en `/var/www/html`.
- Se reinició el servicio Apache (`apache2ctl restart`).

![[Pasted image 20250908151529.png]]

### 1. Explique para qué sirven los cambios que acaba de hacer.
Estos cambios sirven para:

- **Copia de certificados y claves en `/etc/apache2/ssl`**: Permite que Apache acceda al certificado del servidor y a su clave privada para establecer conexiones seguras.
- **Permisos restringidos (chmod 400)**: Aseguran que solo el administrador pueda leer los archivos, protegiendo la clave privada.
- **Habilitar módulo SSL (`a2enmod ssl`)**: Activa en Apache la capacidad de usar HTTPS.
- **Deshabilitar compresión (`a2dismod -f deflate`)**: Evita que la compresión interfiera en el análisis de tráfico con Wireshark y protege contra ciertos ataques (como BREACH).
- **Activar `default-ssl.conf` y modificar parámetros**:
    - **ServerName / ServerAdmin**: Identifican el servidor por su IP en los accesos.
    - **SSLCertificateFile / SSLCertificateKeyFile**: Indican a Apache qué certificado y clave usar en las conexiones HTTPS.
- **Creación del `index.html`**: Sirve como página de prueba para verificar el acceso HTTP y HTTPS.

## Prueba del Servicio Web Seguro
Se accedió a la web http://10.0.2.15 mientras se capturaban paquetes en Wireshark.

### 2. Revise los paquetes capturados. ¿Qué puede ver en el contenido?
En Wireshark se observa la solicitud y respuesta HTTP, donde el contenido HTML viaja en texto claro. Observo en el **TCP Stream** la solicitud y respuesta del servidor para acceder a la web. Se desplegó el contenido del archivo `index.html` creado anteriormente de forma correcta (200).

![[Pasted image 20250908152549.png]]

Ahora, se trató de acceder al servidor en modo seguro (https://10.0.2.15).

### 3. ¿Qué mensaje de error obtiene? ¿Por qué?
Obtengo el siguiente mensaje de error:

![[Pasted image 20250908152734.png]]

donde se menciona que mi conexión **no es segura** y que la web fue configurada inapropiadamente.

Se siguieron los pasos para agregar correctamente el certificado del archivo ``ca.crt`` en la configuración del navegador:

![[Pasted image 20250909071139.png]]

Luego, se intentó acceder de nuevo a la web pero en modo seguro, y me dejó acceder sin problemas:

![[Pasted image 20250909071239.png]]

### 4. ¿Qué pasa ahora? ¿Por qué?
Puedo ingresar a la web porque CA **valida el certificado del servidor** y permite la conexión segura.

Se capturaron los paquetes con el filtro del puerto 443:

![[Pasted image 20250909072150.png]]

### 5. ¿Qué observa en la captura?
Se observa solo el intercambio inicial TLS, el resto de la comunicación está cifrada. Sin embargo, se logra observar el certificado con la información configurada anteriormente.

![[Pasted image 20250909072803.png]]

### 6. ¿Puede ver el contenido de la página en texto claro?
**No.** Lo único que se observa es parte del contenido del certificado, el resto está protegido por TLS.

### 7. Interprete la negociación que se ve al inicio de la conexión
Al inicio de la conexión HTTPS se observa la negociación TLS (handshake). En esta fase:

- El cliente envía un **ClientHello**, indicando las versiones de TLS y los algoritmos de cifrado que soporta.
- El servidor responde con un **ServerHello**, elige los algoritmos de cifrado y envía su certificado digital para autenticarse.
- El cliente valida el certificado contra la CA instalada.
- Se intercambian claves (mediante RSA o Diffie-Hellman, según el algoritmo negociado) y se genera una **clave de sesión**.
- A partir de ese momento, toda la comunicación queda cifrada con esa clave simétrica.

## Conclusiones
### ¿Qué conceptos utilizó para ejecutar esta práctica?
Para el desarrollo de la práctica utilicé conceptos relacionados con la infraestructura de clave pública (PKI), como la creación de una Autoridad de Certificación (CA) y la generación de certificados digitales. También apliqué conocimientos de criptografía asimétrica (RSA) para la firma y verificación de certificados, y de criptografía simétrica para el cifrado de las sesiones establecidas con HTTPS. Además, se trabajó con el protocolo TLS/SSL para asegurar las comunicaciones, se configuró el servidor Apache para soportar conexiones seguras, y finalmente se empleó Wireshark como herramienta de análisis de tráfico para comparar las diferencias entre el intercambio de información en HTTP y en HTTPS.

### ¿Qué aprendió en esta práctica?
En esta práctica aprendí a crear y configurar una Autoridad de Certificación propia, así como a generar e instalar certificados digitales en un servidor web para habilitar el acceso seguro mediante HTTPS. También comprendí la importancia de que el navegador reconozca y confíe en la CA para establecer la conexión sin advertencias de seguridad. Pude evidenciar, mediante Wireshark, cómo el tráfico en HTTP viaja en texto claro, mientras que en HTTPS está cifrado y no es legible, lo que refuerza la importancia del uso de TLS en la protección de la información. Finalmente, entendí mejor la negociación inicial TLS y cómo a partir de ella se establecen parámetros de seguridad que garantizan la confidencialidad, autenticidad e integridad de los datos transmitidos.