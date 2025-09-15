**1. ¿Qué es la identificación?**  
La identificación es el mecanismo mediante el cual una entidad (como un usuario) que solicita acceso a un sistema proporciona una etiqueta que lo identifica. Esta etiqueta se llama **identificador (ID)** y permite al sistema reconocer quién está solicitando acceso, aunque aún no se haya verificado su identidad. Por ejemplo, un nombre de usuario o un correo electrónico.

**2. ¿Qué es la autenticación?**  
La autenticación es el proceso de **validar y verificar la identidad** de un usuario (o sistema) que solicita acceso. Es la prueba de que el usuario es quien dice ser. Por ejemplo, ingresar una contraseña, usar una tarjeta inteligente o escanear una huella dactilar.

**3. ¿Qué es la autorización?**  
La autorización es el proceso que determina **qué recursos puede acceder un usuario autenticado** y **qué acciones puede realizar** con ellos. Una vez que se verifica la identidad del usuario, el sistema le otorga privilegios específicos según listas de control de acceso (ACL) o matrices de permisos.

**4. ¿Qué es la responsabilidad (accountability)?**  
La responsabilidad (también llamada **auditabilidad**) es el mecanismo que garantiza que **todas las acciones realizadas en un sistema**, ya sean autorizadas o no, **puedan atribuirse a una identidad autenticada**. Esto se logra mediante registros (logs), auditorías y seguimiento de actividades, lo que permite rastrear quién hizo qué y cuándo.

**5. ¿Qué puede usarse como un ID de usuario?**  
Un ID de usuario puede ser cualquier información única que identifique a una persona dentro del dominio de seguridad. Ejemplos incluyen:
- Nombre completo
- Inicial del nombre y apellido (por ejemplo, jsmith)
- Número de identificación único
- Código compuesto (por ejemplo, combinando departamento y número aleatorio)
- Dirección de correo electrónico

El ID debe ser único y estar asociado a una sola entidad.

**6. ¿Qué es un solicitante (supplicant)?**  
Un **solicitante (supplicant)** es una entidad (usuario o sistema) que **solicita acceso a un recurso o sistema**. Es quien presenta sus credenciales (como un nombre de usuario o una contraseña) durante el proceso de autenticación.

**7. ¿Qué es un factor de autenticación?**  
Un **factor de autenticación** es un mecanismo o método utilizado para **probar la identidad de un usuario**. Representa una categoría de prueba que el sistema utiliza para verificar que el solicitante es quien dice ser.

**8. ¿Cuáles son los tres tipos de factores de autenticación?**  
Los tres tipos de factores de autenticación son:

1. **Algo que el usuario sabe** (something you know):  
   Como una contraseña, PIN o frase de paso (passphrase).

2. **Algo que el usuario tiene** (something you have):  
   Como una tarjeta inteligente, una tarjeta con chip, un token (llavero generador de códigos) o un teléfono móvil.

3. **Algo que el usuario es o puede producir** (something you are):  
   Basado en características biométricas, como huellas dactilares, reconocimiento facial, escáner de iris, voz o firma dinámica.

> Cuando se combinan dos o más factores (por ejemplo, contraseña + token), se habla de **autenticación fuerte** o **autenticación de dos factores**.