## Integrantes
- Cristian Eduardo Botina - A00395008
- Juan Manuel Marín - A00382037
- Óscar Andrés Gómez - A00394142

## Caso práctico: El nuevo servidor de la San Marino
### 1. Riesgos para la seguridad del sistema
¿Qué elementos de este caso representan riesgos para la seguridad del sistema? Enuméralos y relaciónalos con conceptos del curso (como superficie de ataque, privilegios, cifrado, etc.).

#### Respuesta
Algunos elementos identificados que representan riesgos para la seguridad del sistema en el contexto de la problemática son:

##### 1. Acceso SSH como root desde cualquier IP  
Permite un punto de acceso directo con privilegios máximos, amplía la superficie de ataque y elimina trazabilidad, vulnerando el principio de privilegios mínimos.

##### 2. Cuentas de usuarios inactivas por más de 6 meses  
Esas cuentas pueden ser objeto de compromisos (por contraseñas débiles) sin que haya actividad aparente, ya que representan cuentas huérfanas y aumentan la exposición del control de acceso.

##### 3. Servicios FTP y Telnet habilitados aunque no se usan  
Protocolos obsoletos que envían credenciales en texto claro, ampliando la superficie de ataque y posibilitando intercepción (no cifrado).

##### 4. Firewall deshabilitado  
Sin filtrado de tráfico, se pierde control sobre puertos abiertos o accesos indebidos, afectando la defensa en profundidad y la protección de la red perimetral.

##### 5. Sistema sin actualizaciones  
Vulnerabilidades conocidas no parchadas permiten exploits ya documentados, por lo que la integridad del sistema puede ser comprometida.

##### 6. No hay registro ni rotación de logs  
Sin logs no hay forma de detectar intrusiones, auditorías o incidentes, asi que se afecta la capacidad de monitoreo y evidencia (confidencialidad, integridad y disponibilidad del sistema quedan ciegas).

##### 7. Contraseñas en texto plano en archivos de configuración  
Si alguien accede a esos archivos, obtiene credenciales directamente, ya que no hay uso de cifrado ni hashing seguro, por lo que rompe la confidencialidad de credenciales.

##### 8. Falta de política de revisión de privilegios o backups  
Privilegios pueden crecer inadvertidamente o cuentas pueden quedar con excesos sin revisión. Por lo tanto, sin backups, hay pérdida de disponibilidad en caso de fallo o contaminación maliciosa.

### 2. Acciones de hardening
Propón al menos 5 acciones concretas que Liza y Juan debería implementar para aplicar hardening al servidor. Relaciónalas con las mejores prácticas vistas.

#### Respuesta
Para fortalecer el servidor, proponemos las siguientes acciones concretas:

1. Deshabilitar el acceso SSH directo como root y usar cuentas normales con permisos mediante sudo.
2. Eliminar o desactivar servicios innecesarios como FTP y Telnet para reducir la superficie de ataque.
3. Volver a activar y configurar correctamente el firewall, permitiendo solo los puertos necesarios.
4. Habilitar actualizaciones automáticas o periódicas del sistema para corregir vulnerabilidades conocidas.
5. Configurar la generación, auditoría y rotación de logs para mantener trazabilidad y detección de incidentes.
6. Eliminar o deshabilitar cuentas inactivas para evitar accesos no controlados.
7. Cifrar las contraseñas en archivos de configuración o usar mecanismos seguros de almacenamiento.
8. Establecer políticas claras de backup y revisión de privilegios para garantizar disponibilidad y control.

### 3. Clasificación según el triángulo CID
Clasifica las acciones propuestas según los siguientes aspectos del triángulo CID:  
- Confidencialidad
- Integridad
- Disponibilidad

Para responder esta pregunta ayúdate con una tabla donde en una columna esté situación encontrada, que pilar afecta del triángulo CID, nivel de riesgo y solución propuesta.

#### Respuesta
Realizamos la siguiente tabla con base a las acciones que propusimos en el punto anterior:

|Situación encontrada|Pilar CID afectado|Nivel de riesgo|Solución propuesta|
|---|---|---|---|
|Acceso SSH como root|Confidencialidad / Integridad|Alto|Deshabilitar login root y usar sudo|
|Cuentas inactivas|Confidencialidad / Integridad|Medio|Eliminar o suspender cuentas inactivas|
|FTP y Telnet activos|Confidencialidad|Alto|Desactivar servicios no utilizados|
|Firewall deshabilitado|Confidencialidad / Disponibilidad|Alto|Configurar y activar firewall|
|Sin actualizaciones|Integridad|Alto|Activar actualizaciones automáticas|
|Sin registros ni rotación|Integridad / Disponibilidad|Alto|Configurar logs y auditoría|
|Contraseñas en texto plano|Confidencialidad|Alto|Usar cifrado o vaults de contraseñas|
|Sin política de backups|Disponibilidad|Alto|Implementar copias de seguridad y revisión de privilegios

### 4. Recomendaciones del benchmark CIS
Utilizando el benchmark adecuado del CIS, identifica para cada aspecto a resolver en este servidor que recomendación sería la adecuada ubicando página, titulo, análisis de como la recomendación ayuda a solucionar la vulnerabilidad.

#### Respuesta
Dado que se utilizó un prompt para responder a esta pregunta, se adjunta la conversación de la misma y, con él, el resultado:

https://chatgpt.com/share/68eda0d9-0574-800f-ae7e-811e6f166ddd

### 5. Prompt utilizado con ChatGPT
Para el punto anterior ayúdate con chatgpt y entrega el prompt que diseñaste para que te ayudara a resolver esta pregunta.

#### Respuesta

Para responder a la pregunta anterior, diseñamos el siguiente prompt:

>Quiero que actúes como experto en seguridad de sistemas Linux y benchmarks CIS. Te daré un escenario con vulnerabilidades (acceso root SSH abierto, servicios FTP/telnet activos, sin actualizaciones, sin logging, contraseñas en texto plano, etc.). Necesito que identifiques para Ubuntu 24.04 LTS las recomendaciones del CIS Benchmark Ubuntu 24.04 v1.0.0 que mitiguen esas vulnerabilidades, indicando la sección o página del benchmark, el título de la recomendación, una explicación de cómo mitiga la vulnerabilidad específica y cómo implementarla en ese servidor.