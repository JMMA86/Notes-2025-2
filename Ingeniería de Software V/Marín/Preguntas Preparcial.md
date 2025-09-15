## Conceptos
1. ¿Qué es la nube?
   R/ Servicios de computación (almacenamiento, servidores, bases de datos, etc.) accesibles a través de internet.

2. ¿Contenedores vs VM?
   * VM: emula un sistema operativo completo.
   * Contenedor: comparte el SO host, más liviano y rápido.

3. ¿Por qué es importante que una app sea resiliente y altamente disponible?
   R/ Para garantizar que siga funcionando frente a fallos y siempre esté accesible para los usuarios.

4. ¿Qué significa escalabilidad en el contexto de DevOps?
   R/ Capacidad de una app/sistema de aumentar o reducir recursos según la demanda.

## Comparaciones
1. Web tradicional vs una en la nube
   * Tradicional: infraestructura fija, limitada.
   * Nube: flexible, escalable y bajo demanda.

1. Monolito vs microservicios
   * Monolito: una sola aplicación grande.
   * Microservicios: varios servicios pequeños independientes.

1. Despliegue manual vs despliegue automático
   * Manual: lento, propenso a errores.
   * Automático: rápido, consistente y repetible.

## Emparejar con problemática
1. Mi sitio web se cae cuando hay muchos visitantes: **Escalabilidad en la nube.**
2. Quiero que mi aplicación funcione aunque falle un servidor: **Alta disponibilidad y resiliencia.**
3. Necesito que mi sistema crezca automáticamente según la demanda: **Autoscaling en la nube.**
4. Mi aplicación tarda mucho en responder a las consultas de los usuarios: **Optimización y uso de caching/bases distribuidas.**

## Otras preguntas
1. ¿Por qué usar contenedores?
   R/ Porque son ligeros, portables y facilitan la integración y despliegue.

2. ¿Qué significa DevOps?
   R/ Cultura y prácticas que integran desarrollo y operaciones para entregar software más rápido y confiable.

3. ¿Ventajas de la nube?
   R/ Escalabilidad, flexibilidad, reducción de costos y acceso global.

4. ¿Qué beneficios tiene la automatización en el contexto de DevOps?
   R/ Más velocidad, menos errores, despliegues consistentes y mayor productividad.

## Conceptos adicionales
1. **¿Qué es Shift Left?**
   R/ Es la práctica de adelantar las actividades de pruebas, seguridad y calidad hacia las etapas iniciales del desarrollo para detectar errores antes y reducir costos.

2. **¿Qué es IaaS, PaaS y SaaS?**

   * **IaaS (Infrastructure as a Service):** Provisión de servidores, redes y almacenamiento. Ej: AWS EC2.
   * **PaaS (Platform as a Service):** Entorno listo para desplegar aplicaciones sin gestionar la infraestructura. Ej: Heroku.
   * **SaaS (Software as a Service):** Aplicaciones listas para usar a través de internet. Ej: Gmail, Office 365.

3. **Mejor descripción para un contenedor**
   R/ Un contenedor es una unidad estandarizada de software que empaqueta código, librerías y dependencias necesarias para ejecutar una aplicación de forma aislada y portátil.

4. **Procesos corriendo en el host del sistema de kernel de Linux**
   R/ Los contenedores no tienen un kernel propio; comparten el del host y utilizan *namespaces* y *cgroups* para aislar procesos, red y recursos.

5. **¿Cómo correr los contenedores con full privilegios?**
   R/ Usando `docker run --privileged` (permite acceso total al host, aunque no se recomienda por motivos de seguridad).

6. **Schedule de containers**
   R/ Es la asignación automática de contenedores a nodos en un clúster, considerando recursos disponibles y reglas. Kubernetes, por ejemplo, usa el *scheduler* para decidir en qué nodo se ejecuta cada pod.

7. **Ventajas de usar contenedores en la nube**

   * Portabilidad entre entornos.
   * Mejor aprovechamiento de recursos.
   * Escalado más rápido y flexible.
   * Integración con CI/CD.

## Patrones y arquitecturas
1. **Nombrar 3 patrones de alta prioridad y explicar por qué son críticos**

   * **Circuit Breaker:** evita que fallos en un servicio cascaden al resto del sistema.
   * **Retry con backoff:** reintenta llamadas fallidas con tiempos crecientes, mejora resiliencia.
   * **Autoscaling:** ajusta automáticamente los recursos según la demanda, optimizando costos y disponibilidad.

2. **Diferencia entre Circuit Breaker y Retry**

   * **Retry:** intenta recuperar una operación fallida repitiéndola.
   * **Circuit Breaker:** corta temporalmente las llamadas a un servicio fallando, evitando sobrecargarlo y protegiendo al sistema.

3. **¿Cuándo usarías CQRS vs arquitectura tradicional?**

   * **Arquitectura tradicional:** adecuada para aplicaciones simples con bajo volumen de datos.
   * **CQRS (Command Query Responsibility Segregation):** útil cuando las operaciones de lectura y escritura son muy diferentes en volumen, se necesita escalabilidad o consistencia eventual.

4. **¿Qué patrón implementarías para manejar filtros de tráfico?**

   * **API Gateway / Reverse Proxy con patrón de *Rate Limiting* y *Traffic Shaping*.**
     Este patrón controla peticiones entrantes, aplica filtros, limita abusos y redirige tráfico a los servicios adecuados.

## Preguntas Parcial Anterior
1. Explique claramente la relevancia de dos de prácticas de DevOps
	R/ Integración continua: Es relevante por que reduce errores, pues al estar integrando constantemente, los conflictos y problemas se identifican mas
	rapido y se tiene mayor margen para corregirlos
	
	Entrega continuas: al tener un despliegue automatizado, se extrae la posibilidad de algun error humano y es abstrae la complejidad del despliegue
	para que cualquier miembro del equipo pueda responder a necesidades de despliegue sin tener conocimiento, lo que mejora la colaboración en
	los equipos.

2. Empareje las siglas con su descripción:
	- On Premises: El usuario compra y configura los servidores y red físicos obteniendo su propia infraestructura.
	- IaaS: El usuario configura su propia red, almacenamiento, procesos y otros recursos sobre los recursos ofrecidos por el proveedor cloud.
	- PaaS: El usuario puede desplegar aplicaciones desarrolladas o adquiridas sobre la infraestructura cloud del proveedor.
	- SaaS: El usuario tiene la capacidad de utilizar aplicaciones ofrecidas por el proveedor cloud

3. Organice en orden los pasos en el ciclo de DevOps partiendo de planeación:
	- Planeación
	- Construcción
	- integracion continua
	- Despliegue
	- Operación
	- Retroalimentación continua

4. Sustente si se encuentra de acuerdo o no con la siguiente afirmación:
	R/ Los monolitos generalmente permiten aprovechar mejor los recursos de hardware
	
	Estoy en desacuardo con la afirmación porque los monolitos "generalmente" no permiten aprovechar mejor los recursos de hardware debido a su
	alto acoplamiento, pues si se quisiera escalar alguna para de la aplicación independientemente no podria hacerlo sin duplicar toda la app, sin
	embargo, solo es estoy en desacuerdo porque dice, generalmente, hay ocasiones donde los monolitos pueden aprovechar mejor el hardware que
	por ejemplo unos microservicios, como en aplicaciones pequeñas.

5. Sobre la virtualización, es correcto afirmar:

	a. permite la ejecución de múltiples contenedores en un mismo sistema operativo.
	b. **permite tener servidores muy robustos que pueden ejecutar muchas máquinas virtuales en un solo nodo.**
	c. **permite la ejecución de múltiples máquinas virtuales sobre un hardware compartido**

6. La rápida elasticidad de la nube hace referencia a:

	a. que los servicios los puede configurar el usuario bajo demanda
	b. el usuario controla elasticamente la localización de sus servicios.
	c. el cobro de los servicios es elastico acorde a su utilización
	d. **que la cantidad de instancias de los servicios puede crecer o decrecer acorde a la demanda**

7. Sobre los microservicios es correcto afirmar

	a. requiren mucho tiempo para iniciar y detener los componentes
	b. Utilizan el paradigma con estado para mantener la información de las operaciones en curso.
	c. **Permiten dividir una gran aplicación en pequeños componentes**
	d. Requiren que los componentes se corran en la nube

8. Enuncie 4 beneficios relevantes al aplicar DevOps

	- Se identifican de manera temprana los errores en el código
	- Se disminuyen los errores en el ciclo de desarrollo
	- Mejora la colaboración y comunicación entre equipos
	- Mejora la confiabilidad del producto entregado

9. Sobre los monolitos es correcto afirmar

	a. son fáciles de escalar comparados con los microservicios
	b. son fáciles de ejecutar/desplegar comparados con los microservicios
	c.son fáciles de mantener comparados con los microservicios
	d. pueden ser desacoplados al desplegarlos