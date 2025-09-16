## Integrantes
- Cristian Eduardo Botina - A00395008
- Juan Manuel Marín - A00382037
- Óscar Andrés Gómez - A00394142

## 1. IP de la maquina
![[Pasted image 20250912155428.png]]

Se utilizará la IP 172.30.173.128.

## 2. Entrar a la dirección [Google Hacking Database - Osintux](https://www.osintux.org/documentacion/google-hacking-database)
Esta web es una base de consultas predefinidas que aprovecha el índice de Google para localizar información expuesta o mal configurada en una web, como por ejemplo, ficheros con usuarios/contraseñas, directorios sensibles, portales de login o servidores vulnerables, esto sin interactuar directamente con los objetivos. Es útil para realizar auditorías, pentesting y OSINT (búsqueda de inteligencia en fuentes abiertas) porque ahorra tiempo al apuntar búsquedas que suelen revelar fallos de seguridad, y está organizada por categorías para facilitar su uso.

## 3. Investigue que es Google Dork y cuál es su utilidad.
Básicamente, Google Dork es una técnica que usa operadores de búsqueda de Google para realizar consultas muy específicas que sirven para localizar información en páginas indexadas que normalmente no aparecerían en búsquedas normales, explotando el índice de Google para encontrar ficheros, páginas o strings concretos. Algunos de estos operadores son "site:", "filetype:", "inurl:", entre otros. Como se mencionó anteriormente, es util en estos contextos:

- **OSINT**: Es localizar información pública sobre personas, empresas o infraestructuras, tales como documentos, listados, backups, etc.
- **Pentesting**: Encontrar archivos con credenciales, paneles de administración o configuraciones expuestas sin protección.
- **Threat Intelligence**: Es buscar pistas en la web sobre activos, filtraciones, campañas maliciosas y relacionados.

En la GHDB existen varios dorks con diferentes finalidades para ser usados con estos fines.

## 4. Ejecución de comando ``“index of” / “chat/logs”``
![[Pasted image 20250912161950.png]]

Al ingresar al primero encontramos:

![[Pasted image 20250912162034.png]]

Y en el segundo:

![[Pasted image 20250912162059.png]]

Si entramos a alguno de los logs de la primera web, visualizamos una especie de chat:

![[Pasted image 20250912162145.png]]

Tras analizarlo, observamos que son logs de conversaciones que se dieron en una plataforma llamada "SpielTalk" el 30 de noviembre del 2007, donde no solo se incluyen los mensajes de los usuarios, sino también el nombre de usuario y los mensajes del sistema cuando uno se conecta al chat.

## 5. Ejecutar el comando ``filetype: sql “MySQL dump”`` y entrar al sitio del MIT
![[Pasted image 20250912162508.png]]

Básicamente se observa la estructura de una base de datos, donde se incluye:

- Host: ``sql.mit.edu``
- Nombre de base de datos: ``presbrey+scriptstp``
- Versión del servidor: ``4.1.15-Debian_0.dotdeb.1-log``
- Nombre de varias tablas: ``textpattern``, ``txp_category``, ``txp_css``, ``txp_file``, ``txp_form``, ``txp_image``, ``txp_lang``
- Datos insertados en cada tabla
- Configuraciones de codificación
- Scripts de diversos tipos

## 6.  Ejecutar el comando ``filetype: sql “MySQL dump” (pass|password|passwd|pwd)`` y entrar al primer enlace
![[Pasted image 20250912163328.png]]

Básicamente es una web llamada _Google Hacking Database_ (GHDB) en OSINTux.org, y presenta una recopilación de técnicas conocidas como _Google Dorks_, que permiten realizar búsquedas avanzadas en Google para encontrar información sensible expuesta accidentalmente en internet. Arriba muestra el comando que se solicitó y una descripción de lo que realiza, que en este caso es encontrar contraseñas en bases de datos MySQL. No se está seguro de si la práctica buscaba acceder a esta web, pero estas son las páginas que se visualizan al realizar la búsqueda:

![[Pasted image 20250914173351.png]]

Algunos links contienen información parecida al documento de MySQL que se analizó en la pregunta anterior.

## 7. Ejemplo de dos comandos con base a preguntas 2 y 3.
- ``inurl:".env" "DB_PASSWORD" OR "DB_PASS" OR "DATABASE_URL"``: Localiza ficheros de entorno (`.env`) que a menudo contienen credenciales de BD, claves API y URLs.

Si se localizan, un atacante podría:
- Conectarse directamente a la base de datos.
- Acceder a APIs externas (Stripe, AWS, Twilio...).
- Robar datos sensibles, hacer SQLi, o incluso comprometer servidores completos.

- ``inurl:"/.git/config" OR inurl:"/.git/HEAD"``: Encuentra directorios `.git` servidos por HTTP; el config o los objetos pueden revelar ramas, remotos o secretos en el código.

Si se localizan, un atacante podría:

- Obtener claves y registros importantes quemados en código.
- Identificar y analizar la lógica de negocio de una empresa.

## 8. Ejecutar el comando ``nslookup icesi.edu.co``
![[Pasted image 20250914174244.png]]

Al ejecutar el comando se observan datos como:

- **Servidor DNS utilizado**: El comando usó como servidor DNS a `gpon.net`, cuya dirección IP es `fe80::1`. Esta es una dirección IPv6 local, que corresponde a mi router. Esto indica que el sistema está configurado para usar el DNS del gateway de la red actual.

- **Nombre del dominio consultado**: Se realizó la consulta para el dominio **`icesi.edu.co`**, que corresponde a la Universidad Icesi.

- **Direcciones IP asociadas**: El dominio `icesi.edu.co` tiene dos direcciones IPv4 registradas:
	- `200.3.192.46`
	- `200.3.193.46`
	Estas son las direcciones IP de los servidores web donde está alojada la página oficial de la universidad. El hecho de tener dos IPs sugiere un uso de balanceo de carga o alta disponibilidad, lo cual es común en instituciones importantes para garantizar estar al aire todo el tiempo.

- **"Non-authoritative answer"**: Este mensaje significa que la respuesta no provino directamente del servidor DNS autoritativo del dominio (es decir, no es la fuente original de la información), sino de un servidor DNS recursivo intermedio. Aun así, la información es confiable y actualizada, ya que los servidores DNS recursivos suelen cachear datos válidos.

## 9. Sitio web https://www.lacnic.net/ 
### a) Objetivo del sitio
El sitio web LACNIC (Latin American and Caribbean Internet Addresses Registry) es la autoridad regional encargada de asignar y gestionar direcciones IP y números AS (Autonomous System) en América Latina y el Caribe. Según su web:

"Su función es asignar y administrar los recursos de numeración de Internet (IPv4, IPv6), números autónomos y resolución inversa para la región."

### b) WhoIs
![[Pasted image 20250914175833.png]]

De estos datos nos interesa información como:

- **inetnum: 200.3.192.0/24**: Rango IP asignado, útil para escaneos de red y mapeo de activos.  
- **inetnum-up: 200.3.192.0/23**: Bloque superior que incluye toda la red de la Universidad Icesi (512 IPs), clave para ampliar el alcance de búsquedas.  
- **status: reassigned**: Indica que el rango fue reasignado, puede significar cambios recientes en infraestructura o configuraciones inestables.  
- **owner: Universidad Icesi**: Vincula directamente la IP a la institución, esencial para OSINT y reportes éticos.  
- **ownerid: CO-UNIC-LACNIC**: Identificador único de la organización en LACNIC, útil para buscar otros recursos asociados.  
- **responsible: INFRAESTRUCTURA - SYRI**: Equipo interno encargado, nombre potencial de un grupo técnico o departamento.  
- **country: CO**: Ubicación geográfica, relevante para análisis legal, compliance o geolocalización de servicios.  
- **phone: +57 2 5552334 [4179]**: Número de contacto técnico, puede usarse en ingeniería social o verificación de identidad.  
- **owner-c / tech-c / abuse-c: CAG9**: Código de contacto común, permite encontrar otros registros vinculados (DNS, redes, servidores).  
- **nserver: NS1-06.AZURE-DNS.COM, NS2-06.AZURE-DNS.NET, etc.**: DNS gestionados por Azure, indica uso de nube, posible vector de ataque o exposición.  
- **e-mail: adminred@icesi.edu.co**: Contacto técnico directo, ideal para notificación de vulnerabilidades o phishing simulations controladas.  
- **changed: 20220405**: Última actualización hace 3 años, sugiere que la infraestructura está activa pero podría tener configuraciones obsoletas.  
- **created: 20040616**: El registro es antiguo, posibles sistemas heredados o servicios desactualizados aún en uso.<

### c) Lacnic Tools
![[Pasted image 20250914180936.png]]

De LACNIC Tools nos interesa información como:

- **inetnum: 200.3.193.0/24**: Rango IP específico donde se encuentra el servidor; útil para escanear hosts individuales o validar accesibilidad.  
- **status: reassigned**: Indica que el rango fue reasignado recientemente; puede significar cambios en la infraestructura, posibles configuraciones mal aplicadas o servicios desactualizados aún activos.  
- **owner: Universidad Icesi**: Confirma la propiedad del recurso; clave para vincular activos a una organización real en OSINT o reportes de vulnerabilidad.  
- **ownerid: CO-UNIC-LACNIC**: Identificador único en LACNIC; permite buscar otros recursos (IPs, ASNs) asociados a la misma institución.  
- **responsible: INFRAESTRUCTURA - SYRI**: Nombre del equipo interno encargado; puede ser un punto de contacto técnico o indicar nombre de sistema/área dentro de la universidad.  
- **country: CO**: Ubicación geográfica confirmada; relevante para análisis legal, cumplimiento normativo o priorización de riesgos regionales.

## 10. Web https://centralops.net/co/
Al ingresar la IP en esta web, aparece esta información:

![[Pasted image 20250914181359.png]]

Alguna información relevante puede ser:

- **inetnum: 200.3.193.0/24**: Rango exacto donde está la IP; útil para mapear redes y escanear hosts adyacentes.
- **inetnum-up: 200.3.192.0/23**: Bloque superior que contiene toda la red asignada a la Universidad Icesi; esencial para ampliar el rango de escaneo.
- **owner: Universidad Icesi**: Confirma la propiedad del recurso; clave para OSINT y reportes éticos.
- **country: CO**: Ubicación geográfica; relevante para análisis legal o de cumplimiento normativo.
- **tech-c / owner-c / abuse-c: CAG9**: Código de contacto técnico y de abuso; permite identificar otros registros asociados o enviar reportes formales.
- **e-mail: adminred@icesi.edu.co**: Correo directo del equipo de red; útil para notificación de vulnerabilidades o ingeniería social controlada.
- **phone: +57 2 5552334 [4179]**: Número de contacto; puede ser usado en ataques de voz o verificación de identidad.
- **nserver: NS1-08.AZURE-DNS.COM, etc.**: DNS gestionados por Microsoft Azure; indica infraestructura en la nube, posible vector de exposición o configuraciones mal aseguradas.
- **changed: 20220405**: Última actualización reciente; sugiere que la infraestructura está activa y podría tener configuraciones obsoletas o vulnerables.
- **status: reassigned**: Indica que el rango fue reasignado; puede significar cambios en la administración o migración de servicios, lo cual a veces deja puertas abiertas.

Hay mucha información repetida entre las 3 fuentes.

## 11. Entrar a nslookup
![[Pasted image 20250914181744.png]]

## 12. Ingresar comandos solicitados
![[Pasted image 20250914181829.png]]

### ¿Qué información obtiene y que puede deducir?
Se puede deducir que:
- La universidad utiliza Amazon Route 5 (AWS) como proveedor de DNS, lo que indica una infraestructura moderna, escalable y gestionada en la nube.
- Los servidores están distribuidos geográficamente (EE.UU., Reino Unido), lo que mejora la disponibilidad y reducción de latencia global.
- Al ser servidores autoritativos, son los únicos que tienen la fuente de verdad sobre el dominio, cualquier cambio en DNS debe hacerse aquí.
- Esta información es crítica para pentesting: si alguno de estos servidores tiene configuraciones débiles, un atacante podría extraer todos los registros DNS del dominio.
- También permite identificar posibles vectores de ataque: ataques DDoS contra estos servidores podrían caer el sitio web completo.

## 13. Ejecución de siguientes comandos (mx)
![[Pasted image 20250914182141.png]]

Al ejecutar `set type=mx` seguido de `icesi.edu.co`, se obtiene un único servidor de correo (MX) `icesi-edu-co.mail.protection.outlook.com` con prioridad `10`.

Se puede deducir que:
- La universidad usa Microsoft 365 / Exchange Online para gestionar su correo electrónico, lo que indica una infraestructura de nube moderna y centralizada.
- El uso de `protection.outlook.com` implica que cuentan con filtros antispam y antivirus integrados de Microsoft, lo cual es bueno para seguridad, pero también significa que todo el tráfico de correo pasa por un tercero.
- Si este servidor está mal configurado (por ejemplo, con políticas de relay abiertas o registros SPF/DKIM/DMARC débiles), podría ser explotado para enviar correos falsificados (phishing) o suplantar identidades institucionales.
- El hecho de que aparezcan los servidores DNS (NS) junto con el MX confirma que el dominio tiene una infraestructura bien definida, pero también revela superficie de ataque: si un atacante controla un subdominio o logra comprometer uno de los servidores DNS, podría redirigir el correo o interceptarlo.
- Esta información es clave para auditorías de seguridad: verificar los registros SPF, DKIM y DMARC del dominio puede revelar vulnerabilidades de suplantación de correo.

## 14. Ejecución de siguientes comandos (txt)
![[Pasted image 20250914182503.png]]

Al ejecutar `set type=txt` seguido de `icesi.edu.co`, se obtienen múltiples registros TXT que revelan:

#### Verificación de dominio para servicios externos:  
  - `google-site-verification=*` → Confirma propiedad del dominio en Google Search Console y otros servicios de Google.  
  - `google-gws-recovery-domain-verification=*` → Usado por Google Workspace para recuperación de cuenta.  
  - `MS=C140AFD1...` y `MS=ms81180656` → Verificación de propiedad en Microsoft 365 / Azure AD.  
  - `adobe-idp-site-verification=*` → Vinculación con Adobe Identity Management.  
  - `brevo-code:*` → Verificación en Brevo (ex Sendinblue), usado para envío de correo masivo.  
  - `ZOOM_verify_*` → Confirmación de dominio en Zoom para reuniones y autenticación.  

#### Registro SPF completo:  
  `v=spf1 a:midgard.icesi.edu.co ... include:spf.protection.outlook.com include:_spf.qp-mail.com include:sendgrid.net include:_spf.salesforce.com -all`  
  - Define qué servidores están autorizados a enviar correo en nombre de `icesi.edu.co`.  
  - Incluye proveedores externos clave: Outlook (Microsoft), SendGrid, Salesforce y QP-Mail.  
  - El mecanismo `-all` indica política estricta: solo los servidores listados pueden enviar correo; cualquier otro debe ser rechazado.

Se puede deducir que:
- La universidad usa múltiples servicios en la nube (Google, Microsoft, Zoom, SendGrid, Salesforce) y verifica activamente su dominio en todos ellos.  
- El registro SPF está bien configurado y es estricto (`-all`), lo cual reduce el riesgo de phishing y suplantación de correo.  
- Sin embargo, la presencia de tantos proveedores externos aumenta la superficie de ataque: si alguno se compromete (ej: cuenta de SendGrid o Salesforce), podrían enviarse correos falsificados desde `icesi.edu.co`.  
- Los tokens de verificación (como `google-site-verification`) no son secretos, pero su exposición confirma que el dominio está activamente gestionado —lo que implica que otras configuraciones (DNS, APIs, subdominios) también podrían estar expuestas.  
- Estos registros son fundamentales para evaluar la seguridad de correo electrónico y detectar posibles fugas de credenciales o configuraciones mal aplicadas en servicios terceros.

# 15 openssl icesi.edu.co
![[Pasted image 20250915165406.png]]

### Detalles importantes
- **Certificado:**
    - **CN (Common Name):** `*.icesi.edu.co` → válido para cualquier subdominio bajo `icesi.edu.co`.
    - **Organización:** Universidad Icesi, Cali, Valle del Cauca, CO.
    - **CA emisora:** DigiCert Global G2 TLS RSA SHA256 2020 CA1 (una de las principales CAs del mundo).
    - **Validez:** 11 de agosto de 2025 → 5 de septiembre de 2026.
- **Seguridad criptográfica:**
    - **Algoritmo:** RSA 2048 bits (firma).
    - **Cifrado de sesión:** ECDHE-RSA-AES128-GCM-SHA256 (protocolo TLS 1.2).
    - **Handshake:** OK, certificado verificado, cadena de confianza completa.
### Implicaciones
1. El certificado es **válido y confiable**, por lo tanto la universidad protege sus comunicaciones web con TLS moderno.
2. Usan **wildcard** para simplificar la gestión de certificados en múltiples subdominios.
3. El uso de **TLS 1.2 con ECDHE y GCM** asegura confidencialidad y forward secrecy, aunque hoy en día lo ideal es TLS 1.3.

# 16 pasos 8-15 de nuevo con otra página

![[Pasted image 20250915160925.png]]

Con el reciente auge del concepto del vibe coding, se nos ocurrió incidir en su nivel de seguridad. Photoguruai es una página para hacer headshots de fotos hecha con vibe coding, entonces probaremos que tal le va.

- Vemos entonces una única red IPv4.

### Datos útiles en este caso
- **Rango de IP asignado**: `76.76.21.0/24`. Permite saber qué hosts están bajo control de Vercel (posibles superficies de ataque si alojan apps del objetivo).
- **Organización responsable**: _Vercel, Inc._ Identifica el proveedor de infraestructura.
- **NetName / NetHandle**: `VERCEL-01 / NET-76-76-21-0-1`. Ayuda a correlacionar recursos con otros registros públicos.
- **ASN / Parent Net**: Relaciona con _NET76_, útil para ver enrutamiento y BGP.
- **Certificado embebido**: Puede dar pistas sobre dominios asociados, vigencia de certificados y configuraciones TLS.
- **Fechas de registro y actualización**: Ayudan a evaluar la madurez de la infraestructura (ej: IP asignada desde 2020).

### Datos útiles sacados de central ops
- **Certificado embebido**: puede revelar dominios internos o configuraciones TLS.
- **Reverse DNS fallido (PTR inexistente)**:
    - Puede indicar que el host no tiene nombre asociado.
    - Se usa en fingerprinting: ayuda a diferenciar servicios internos de frontales expuestos.
    - Algunos firewalls, listas blancas o filtros de correo se basan en PTR, su ausencia puede dar vectores indirectos.

![[Pasted image 20250915162037.png]]

#### nslookup en modo comando
![[Pasted image 20250915162334.png]]

### Deducciones técnicas
- **Uso de Cloudflare**:
    - DNS apunta a _nameservers de Cloudflare_.
    - Esto significa que el dominio aprovecha protección DDoS, CDN y proxy de Cloudflare.
    - El IP real del servidor no aparece aquí.
- **Infraestructura visible**:
    - _IPv4_:
        - `108.162.x.x`
        - `172.64.x.x`
        - `173.245.x.x`
    - _IPv6_:
        - Rango `2606:4700::/32` (Cloudflare)
        - Rango `2803:f800::/32` (Cloudflare en LATAM)
        - Rango `2a06:98c1::/32` (Cloudflare Europa)  
            Esto confirma distribución geográfica global.
- **Posibles pasos de recon**:
    1. Revisar _DNS históricos_ (con herramientas como SecurityTrails, DNSDumpster) para ver si alguna vez expuso un IP real.
    2. Usar _subdomain enumeration_ para detectar servicios no detrás de Cloudflare.
    3. Buscar coincidencias en certificados SSL (crt.sh) que puedan revelar endpoints directos.

![[Pasted image 20250915162627.png]]

### Información que se obtiene
- **Proveedor de correo**: Google Workspace (antes G Suite).
    - Servidores MX: `aspmx.l.google.com`, `alt1.aspmx.l.google.com`, `alt2...`, `alt3...`, `alt4...`.
    - Prioridades: `1, 5, 10` → Gmail gestiona balanceo y redundancia.
- **Implicaciones técnicas**:
    - La organización no administra directamente su propio servidor de correo → delega seguridad, antispam y disponibilidad a Google.
    - Menos probabilidad de vulnerabilidades típicas de servidores de correo mal configurados (ej: open relay, falta de TLS).
    - En un pentest, se podría revisar si existen registros **SPF, DKIM y DMARC** asociados, ya que configuraciones débiles permitirían _spoofing_ de correos del dominio.
- **Superficie de ataque indirecta**:
    - Un atacante podría intentar phishing dirigido usando el dominio si no hay políticas estrictas de autenticación.
    - El hecho de usar Gmail corporativo implica dependencia de Google, pero reduce la exposición de infraestructura propia.

![[Pasted image 20250915164330.png]]

### Lo que indica cada registro
- **`google-site-verification=...`**  
    → El dominio está vinculado a servicios de Google (ej: Google Search Console, Google Workspace). Sirve para confirmar propiedad del dominio ante Google.
- **`apple-domain=SVc6CpThnBMu0qUK`**  
    → Similar, pero para Apple. Puede indicar integración con servicios como iCloud Mail, Apple Business Manager o validaciones de apps.
- **`v=spf1 include:icloud.com include:_spf.google.com ~all`**  
    → Registro **SPF** (Sender Policy Framework).
    - Autoriza que correos enviados desde **iCloud** y **Google** sean considerados válidos para este dominio.
    - El `~all` (softfail) significa que correos enviados desde otros orígenes **no están explícitamente prohibidos**, solo marcados como sospechosos → deja cierta puerta abierta al _spoofing_.
### Implicaciones en seguridad
- **Correo**: El dominio permite enviar emails legítimos desde dos proveedores distintos (Google + iCloud). Esto amplía la superficie y debe estar controlado.
- **Spoofing**: El uso de `~all` en vez de `-all` implica que aún podrían colarse correos falsificados en algunos servidores mal configurados.
- **OSINT**: Los tokens de verificación confirman que el dominio está gestionado por Google y Apple → útil para perfilar qué ecosistema de servicios utiliza la organización.

![[Pasted image 20250915164906.png]]
![[Pasted image 20250915164931.png]]

### Lo que se puede leer de esta salida
- **Certificado SSL**:
    - **Subject**: `CN=photoguruai.com` → válido para el dominio.
    - **SAN (Subject Alternative Names)**: incluye `photoguruai.com` y `*.photoguruai.com`.
    - **Emisor**: Google Trust Services (CA reconocida).
    - **Validez**: del **14 de agosto de 2025** al **12 de noviembre de 2025**.
    - Algoritmo: ECDSA con SHA-256 → moderno y seguro.
- **Cadena de certificados**:
    - Certificado final (photoguruai.com).
    - Intermedio: **Google Trust Services WE1**.
    - Raíz: **GTS Root R4**, firmado por **GlobalSign Root CA**.
- **Parámetros de conexión TLS**:
    - **Protocolo**: TLS 1.3 (el más actual).
    - **Cipher Suite**: `TLS_AES_256_GCM_SHA384` → robusto y recomendado.
    - **Curva**: X25519 (intercambio de claves rápido y seguro).
    - **Renegociación**: no permitida (TLS 1.3 lo elimina).
    - **Compresión**: deshabilitada (evita ataques como CRIME).
- **Tickets de sesión**:
    - Se observan _New Session Tickets_ → permiten reusar sesiones sin renegociar el handshake, optimizando rendimiento.

### Implicaciones de seguridad
1. **Cifrado fuerte y actualizado** → No hay vulnerabilidades básicas (como uso de TLS 1.0/1.1 o RSA débil).
2. **Certificado válido** → Emitido por una CA confiable, aceptado en navegadores.
3. **Wildcard certificado** → Cubre subdominios (`*.photoguruai.com`), lo que facilita despliegues, pero también significa que si un subdominio es comprometido, el atacante puede usar un certificado válido.
4. **Vigencia corta** → El certificado dura solo 3 meses, típico de certificados gestionados automáticamente (ej: con Let’s Encrypt o Google ACME).