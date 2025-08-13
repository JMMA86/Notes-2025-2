
# 1. ¿Cuál es la diferencia entre criptografía y criptoanálisis?

## Criptografía

R// Se podría decir con la referencia que son dos caras de la misma moneda. **La criptografía** es el arte y la ciencia de crear sistemas de comunicaciones seguros. Su **principal objetivo** es alterar los mensajes de tal manera que resulten incomprensibles para receptores no autorizados.

- **Confidencialidad:** Asegurar que solo el destinatario previsto pueda acceder a la información.
- **Integridad:** Garantizar que la información no ha sido alterada durante su transmisión.
- **Autenticidad:** Verificar la identidad del remitente y del receptor.
- **No repudio:** Impedir que un remitente niegue haber enviado un mensaje.

## Criptoanálisis

Es la disciplina que se encarga de romper estos sistemas criptográficos con el propósito de encontrar vulnerabilidades en estos algoritmos de cifrados con el ejercicio de desconocer la clave secreta. Los criptoanalistas emplean una variedad de métodos, que van desde el análisis de frecuencias de letras en un texto cifrado hasta complejas técnicas matemáticas y computacionales.

Un ejemplo histórico notable es el desciframiento del código de la **máquina Enigma** alemana durante la Segunda Guerra Mundial por parte de Alan Turing y su equipo, un hito en la historia del criptoanálisis.

## 2. Explique brevemente como es el proceso de cifrado.

Pasos para cifrar:

_**Texto Plano:** Es la información original y legible que se quiere proteger, como un mensaje, un archivo o cualquier otro dato.

_**Algoritmo de Cifrado:** Es un conjunto de reglas matemáticas complejas que dictan cómo se transformarán los datos. (Algunos algoritmos conocidos son AES, RSA y Twofish.)

_**Clave de Cifrado:** Es un conjunto de valores matemáticos, como una cadena de bits, que funciona como el ingrediente secreto para el algoritmo. (La clave es fundamental, ya que el mismo texto plano cifrado con claves diferentes dará como resultado un texto cifrado distinto.)


Para que el destinatario autorizado pueda leer el mensaje, necesita realizar el proceso inverso, llamado **descifrado**. Para ello, utiliza la clave correspondiente (que puede ser la misma o una diferente, dependiendo del tipo de cifrado) para revertir la codificación y volver a obtener el texto plano original.

Existen dos métodos principales de cifrado:

- **Cifrado Simétrico:** Utiliza una única clave secreta tanto para cifrar como para descifrar la información.
- **Cifrado Asimétrico:** Emplea un par de claves: una clave pública para cifrar (que se puede compartir) y una clave privada para descifrar (que se mantiene en secreto).

## 3. Investigue cómo funciona el Cifrado Cesar (Caesar ́s cypher) y moviendo 5 posiciones hacia adelante cifre lo siguiente: CRYPTOGRAPHY IS FUN. Utilice el alfabeto inglés, es decir, sin Ñ.


En simples palabras si el mensaje es "ABC" y son 3 posiciones pues seria moverse 3 posiciones en el alfabeto y quedaría $\to$ "DEF".

**A B C D E F G H I J K L M N O P Q R S T U V W X Y Z**


HOLA $\to$ KROD


 CRYPTOGRAPHY IS FUN $\to$ HWDUYTLWFUMD NX KZS


## 4. Investigue como funciona el cifrado Vigenère (Vigenère cipher) y cifre la frase: CRYPTOGRAPHY IS FUN usando BOAT como clave. Utilice el alfabeto inglés, es decir, sin Ñ.


Pasos para cifrar: 

1. **Preparar la Clave:** Se toma la palabra clave y se repite las veces que sea necesario para que su longitud coincida con la del mensaje que se va a cifrar.
2. **Asociar Letras:** Cada letra del mensaje original se asocia con una letra de la clave repetida.    
3. **Cifrar:** Cada letra del mensaje se desplaza según el valor de la letra de la clave que le corresponde (A=0, B=1, C=2, etc.).

**A B C D E F G H I J K L M N O P Q R S T U V W X Y Z**


| A   | 0   |
| --- | --- |
| B   | 1   |
| C   | 2   |
| D   | 3   |
| E   | 4   |
| F   | 5   |
| G   | 6   |
| H   | 7   |
| I   | 8   |
| J   | 9   |
| K   | 10  |
| L   | 11  |
| M   | 12  |
| N   | 13  |
| O   | 14  |
| P   | 15  |
| Q   | 16  |
| R   | 17  |
| S   | 18  |
| T   | 19  |
| U   | 20  |
| V   | 21  |
| W   | 22  |
| X   | 23  |
| Y   | 24  |
| Z   | 25  |

C R Y P T O G R A P H Y  I S  F U N
B O A T B O A T B O A T B O A T B


Letra cifrada = (Letra del mensaje + Letra de la clave)


| Mensaje | Clave | Valor Mensaje (P) | Valor Clave (K) | Suma (P+K) | (P+K) mod 26 | Letra Cifrada |
| ------- | ----- | ----------------- | --------------- | ---------- | ------------ | ------------- |
| C       | B     | 2                 | 1               | 3          | 3            | D             |
| R       | O     | 17                | 14              | 31         | 5            | F             |
| Y       | A     | 24                | 0               | 24         | 24           | Y             |
| P       | T     | 15                | 19              | 34         | 8            | I             |
| T       | B     | 19                | 1               | 20         | 20           | U             |
| O       | O     | 14                | 14              | 28         | 2            | C             |
| G       | A     | 6                 | 0               | 6          | 6            | G             |
| R       | T     | 17                | 19              | 36         | 10           | K             |
| A       | B     | 0                 | 1               | 1          | 1            | B             |
| P       | O     | 15                | 14              | 29         | 3            | D             |
| H       | A     | 7                 | 0               | 7          | 7            | H             |
| Y       | T     | 24                | 19              | 43         | 17           | R             |
| I       | B     | 8                 | 1               | 9          | 9            | J             |
| S       | O     | 18                | 14              | 32         | 6            | G             |
| F       | A     | 5                 | 0               | 5          | 5            | F             |
| U       | T     | 20                | 19              | 39         | 13           | N             |
| N       | B     | 13                | 1               | 14         | 14           | O             |


## 5. Investigue que fue la máquina Enigma y en que año aproximadamente fue usada y bajo que contexto.

La máquina Enigma fue un dispositivo de cifrado electromecánico, lo que significa que usaba una combinación de piezas mecánicas (rotores que giraban) y circuitos eléctricos para codificar mensajes. Su objetivo principal era transformar un mensaje legible (texto plano) en un texto cifrado aparentemente aleatorio, que solo podía ser descifrado por otra máquina Enigma configurada exactamente de la misma manera.

La verdadera genialidad y complejidad de Enigma residía en que, **con cada letra que se tecleaba, el primer rotor avanzaba una posición**. Una vez que el primer rotor completaba una vuelta, hacía girar al segundo, y así sucesivamente, como el odómetro de un coche. Esto significaba que si escribías "AAAA", la primera 'A' podría cifrarse como 'G', la segunda como 'X', la tercera como 'Q' y la cuarta como 'D'. Era un cifrado polialfabético en constante cambio, lo que lo hacía increíblemente difícil de romper.

### Contexto historico

**Período de Uso:** Aunque fue inventada en los años 20 para fines comerciales, la máquina Enigma fue adoptada, modificada y usada masivamente por las fuerzas armadas de la **Alemania Nazi** aproximadamente desde principios de los **años 30 y durante toda la Segunda Guerra Mundial (1939-1945)**.

El uso de la Enigma se enmarca en la doctrina militar alemana del **Blitzkrieg ("guerra relámpago")**. Esta estrategia se basaba en ataques rápidos y coordinados entre divisiones de tanques (Panzer), la fuerza aérea (Luftwaffe) y la infantería. Para que esta coordinación fuera efectiva, se necesitaba una comunicación constante, rápida y, sobre todo, secreta.

La creencia alemana en la invulnerabilidad de la Enigma era tan alta que basaron casi toda su seguridad en ella. Sin embargo, gracias al trabajo pionero de los matemáticos polacos antes de la guerra y, posteriormente, a los esfuerzos masivos de los criptoanalistas británicos en **Bletchley Park**, liderados por figuras como **Alan Turing**, el código Enigma fue finalmente descifrado. Este logro, mantenido en secreto durante décadas, fue uno de los factores más decisivos para la victoria Aliada, ya que permitió anticipar los movimientos alemanes y se estima que acortó la guerra en al menos dos años, salvando millones de vidas.

## 6. Explique como funciona el cifrado simétrico y ¿cuál es su principal desventaja?


2 personas se desean enviar un mensaje estos ya tienen una clave secreta acordada usando algoritmos simétricos como el AES codifican este mensaje usando el mismo algoritmo y la misma llave pueden ser capaces de descifrar el mensaje si tienen conocimiento de esta, si un 3ero intercepta el mensaje solamente vera el codificado sin poder conocer su contenido.

**Ejemplos de algoritmos simétricos:** AES (el estándar actual), DES, 3DES, Blowfish.

### **¿Cuál es su Principal Desventaja?**

La principal y más significativa desventaja del cifrado simétrico es **El Problema de la Distribución de la Clave (Key Distribution Problem)**.

Este problema se resume en la siguiente pregunta: **¿Cómo pueden estas 2 personas compartir la clave secreta de forma segura la primera vez, sin que nadie más la intercepte?**

Por lo que el dilema se resumen en:
- No pueden enviarse la clave a través de un canal no seguro (como un email normal), porque un atacante podría interceptarla. Si el atacante obtiene la clave, toda la seguridad del sistema se derrumba, ya que podrá descifrar todos los mensajes futuros.
- Esto crea un problema circular: para establecer un canal de comunicación seguro, necesitan una clave secreta, pero para compartir esa clave secreta, necesitan un canal de comunicación seguro.

## 7. Explique como funciona el cifrado asimétrico y cuáles son sus principales ventajas y desventajas. De ejemplos de protocolos y/o aplicaciones que funcionen con este tipo de cifrado.


La idea central del cifrado asimétrico es el uso de un **par de claves** matemáticamente vinculadas para cada persona. Estas dos claves son diferentes, pero lo que una cifra, solo la otra puede descifrarlo. El par se compone de:

1. **Clave Pública:** Esta clave se puede compartir con cualquiera. Es como la dirección de tu casa o tu número de cuenta bancaria. No es secreta y la puedes publicar o enviar libremente.
2. **Clave Privada:** Esta clave es **absolutamente secreta** y nunca debe ser compartida con nadie. Es como la llave de la puerta de tu casa o la contraseña de tu cuenta bancaria. Solo tú la tienes.
#### **Caso de Uso 1: Enviar un Mensaje Confidencial**

Imaginemos que Alice quiere enviar un mensaje secreto a Bob.

1. **Bob comparte su clave pública:** Bob le envía a Alice (y a quien quiera) su clave pública. No hay riesgo en esto.
2. **Alice cifra el mensaje:** Alice toma su mensaje (texto plano) y lo cifra usando la **clave pública de Bob**. El resultado es un texto cifrado.
3. **Alice envía el mensaje cifrado:** Lo envía a través de un canal inseguro, como internet.
4. **Bob descifra el mensaje:** Cuando Bob recibe el mensaje, usa su propia **clave privada** para descifrarlo. Como su clave privada es la única que puede revertir el cifrado hecho con su clave pública, solo él puede leer el mensaje.

Incluso si un atacante (Eve) intercepta el mensaje y también tiene la clave pública de Bob, no puede descifrar el mensaje. La clave pública solo sirve para "cerrar la caja", no para abrirla.

#### **Caso de Uso 2: Firmar un Mensaje (Autenticación)**

Ahora, Alice no solo quiere que su mensaje sea secreto, sino que quiere que Bob esté 100% seguro de que fue ella quien lo envió. Para esto se usa la firma digital, invirtiendo el uso de las claves.

1. **Alice crea la firma:** Alice toma su mensaje y lo pasa por una función "hash" (que crea un resumen único del mensaje). Luego, cifra ese hash con su **propia clave privada**. El resultado es la firma digital.
2. **Alice envía el mensaje y la firma:** Envía el mensaje original (puede ser sin cifrar) junto con la firma digital.
3. **Bob verifica la firma:** Bob recibe el mensaje y la firma. Para verificar, usa la **clave pública de Alice** para descifrar la firma. Si funciona, revela el hash original.
4. **Bob compara:** Bob toma el mensaje que recibió y le aplica la misma función hash. Si el resultado coincide con el hash que obtuvo de la firma descifrada, tiene dos certezas:
    - **Autenticidad:** La firma solo pudo ser creada con la clave privada de Alice, por lo que el mensaje es auténtico.
    - **Integridad:** El mensaje no fue alterado en el camino, ya que los hashes coinciden.


### **Principales Ventajas y Desventajas**

#### Ventajas

1. **Soluciona el Problema de la Distribución de Claves:** Esta es su mayor ventaja. No necesitas un canal seguro para intercambiar claves. Simplemente puedes hacer pública tu clave de cifrado sin ningún riesgo.
2. **Permite las Firmas Digitales:** Proporciona los mecanismos de **autenticidad** (probar quién es el autor) y **no repudio** (el autor no puede negar haber enviado el mensaje), algo que el cifrado simétrico no puede hacer por sí solo.
3. **Escalabilidad:** Es ideal para sistemas abiertos como internet, donde necesitas establecer una comunicación segura con entidades (personas, servidores) que no conoces de antemano.

#### Desventajas

1. **Lentitud:** Es significativamente más lento que el cifrado simétrico. Los cálculos matemáticos que requiere son mucho más complejos y consumen mucha más potencia de procesamiento.
2. **Problema de la Autenticidad de la Clave Pública:** ¿Cómo puedes estar seguro de que la clave pública que tienes de "Banco XYZ" realmente pertenece al banco y no a un impostor? Este problema se soluciona con una infraestructura llamada **PKI (Public Key Infrastructure)**, donde entidades de confianza llamadas **Autoridades de Certificación (Certificate Authorities - CA)** emiten certificados digitales que vinculan una clave pública a una identidad verificada.
3. **Claves más Grandes:** Las claves asimétricas son mucho más largas que las simétricas (por ejemplo, 2048 o 4096 bits) para ofrecer el mismo nivel de seguridad, lo que requiere más almacenamiento y ancho de banda.


## 8. ¿Qué es un hash y para que puede ser útil?

Un **hash** (también llamado "resumen" o "huella digital") es el resultado de un proceso criptográfico que transforma cualquier bloque de datos en una cadena de caracteres única y de longitud fija.

Imagina una licuadora digital: sin importar lo que le metas (una palabra, una imagen, un libro entero como "Don Quijote"), siempre producirá un batido del mismo tamaño. De manera similar, una función hash tomará cualquier dato de entrada y generará una salida (el hash) que siempre tendrá la misma longitud.

### **¿Para Qué Puede Ser Útil un Hash?**

La utilidad de los hashes radica en estas propiedades, y se aplican en áreas cruciales de la informática y la seguridad digital:

**1. Verificación de la Integridad de Datos y Archivos:**  
Esta es una de sus aplicaciones más importantes. Imagina que descargas un programa de internet. El desarrollador publica el archivo junto con su hash correspondiente.

- **Proceso:** Una vez que descargas el archivo, puedes usar una herramienta para calcular su hash en tu propio ordenador.
- **Utilidad:** Si el hash que tú generas coincide exactamente con el publicado por el desarrollador, tienes la certeza de que el archivo no ha sido alterado ni corrompido durante la descarga. Si los hashes no coinciden, significa que el archivo es diferente al original, posiblemente porque contiene un virus o se dañó.

**2. Almacenamiento Seguro de Contraseñas:**  
Ningún servicio online seguro debería guardar tu contraseña en texto plano. En su lugar, almacenan un hash de tu contraseña.

- **Proceso:** Cuando creas una cuenta, el sistema toma tu contraseña, la "hashea" y guarda ese hash en su base de datos. Cuando inicias sesión, el sistema vuelve a hashear la contraseña que introduces y compara el resultado con el hash que tiene almacenado.
- **Utilidad:** Si un ciberdelincuente logra robar la base de datos, solo obtendrá la lista de hashes, no las contraseñas originales. Como el hash es irreversible, no puede usarlo para averiguar tu contraseña.

**3. Firmas Digitales y Criptomonedas:**  
En el mundo de las firmas electrónicas y el blockchain, los hashes son fundamentales.

- **Proceso:** Para crear una firma digital, se genera un hash del documento y luego se cifra ese hash con la clave privada del firmante.
- **Utilidad:** Esto garantiza tanto la **integridad** (el documento no ha sido modificado desde que se firmó) como la **autenticidad** (se puede verificar que solo el poseedor de la clave privada pudo haber creado esa firma) En las criptomonedas, las transacciones se agrupan y se "hashean" para crear los bloques de la cadena (blockchain), asegurando la inmutabilidad del registro.


**4. Detección de Malware y Contenido Duplicado:**  
Los programas antivirus mantienen bases de datos con los hashes de archivos maliciosos conocidos.

- **Proceso:** El antivirus puede escanear tu ordenador, calcular el hash de tus archivos y compararlos con su lista negra.
- **Utilidad:** Si un hash coincide, el antivirus identifica y elimina el malware de forma eficiente. De manera similar, servicios como Dropbox usan hashes para detectar si un archivo que intentas subir ya existe en sus servidores, ahorrando espacio y ancho de banda.