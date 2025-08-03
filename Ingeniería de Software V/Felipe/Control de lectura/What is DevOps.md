
### **¿Qué es DevOps?**

DevOps es un conjunto de prácticas **orientadas a reducir el tiempo** entre el momento en que se hace un cambio en el sistema (código) y cuando dicho cambio se implementa en producción, **sin sacrificar calidad**.
No se enfoca solo en herramientas, métodos ágiles o colaboración, sino en **alcanzar objetivos**: rapidez y alta calidad en entregas.

### **Objetivos y Principios**

- **Alta calidad** tanto del código como del proceso de entrega.
- **Automatización** de pruebas, integración, entrega y monitoreo.
- Involucrar a operaciones desde la definición de requisitos.
- Desarrolladores deben tener responsabilidad en incidentes.
- Infraestructura como código (scripts y configuraciones tratados como software).


### **Ejemplo Real: IMVU**

IMVU despliega código **hasta 50 veces al día**:

- Cada commit dispara una **suite de pruebas automáticas** (~9 min).
- El código aprobado se despliega a unos pocos servidores (canarios).
- Si no hay problemas, se expande a toda la infraestructura.
- Si hay errores, el código se revierte automáticamente.
- Cada error que no fue detectado se convierte en una nueva prueba.



### **¿Por qué DevOps?**

Responde al problema de **lanzamientos lentos**, que reducen el valor de nuevas funcionalidades.

Problemas comunes:

- Procesos manuales y frágiles.
- Falta de coordinación entre Dev y Ops.
- Errores de compatibilidad o configuraciones.
- Ejemplo: Knight Capital perdió $440 millones por error de despliegue.



### **Perspectiva DevOps**

Dos enfoques clave:
- **Automatización total** de pruebas, despliegue y monitoreo.
- **Mayor responsabilidad del equipo de desarrollo**, reduciendo la necesidad de operaciones dedicadas.

### **DevOps + Agile**

DevOps complementa Agile en sus 3 fases:

1. **Incepción**: Ops participa en requisitos, planes de lanzamiento y compatibilidad.
2. **Construcción**: Pruebas automatizadas, integración y despliegue continuo.
3. **Transición**: El equipo Dev despliega, monitorea y decide rollback.



### **Estructura del equipo**

- Equipos pequeños (regla de las 2 pizzas).
- Roles principales:
	- **Service Owner**: coordina con externos y prioriza tareas.
    - **Reliability Engineer**: monitorea y soluciona errores post-despliegue.
    - **Gatekeeper**: autoriza avances entre fases del pipeline.
    - **DevOps Engineer**: administra herramientas y automatización.

### **Coordinación**
DevOps busca minimizar la coordinación innecesaria:
- Menos reuniones, más automatización.
- Arquitectura bien definida ayuda a evitar conflictos entre equipos.
- Reutilización vs duplicación: mejor duplicar un poco que frenar la entrega.

---

### **Barreras para adoptar DevOps**

- **Culturales**: Dev quiere cambiar; Ops quiere estabilidad.
- **Industria**: Finanzas o salud requieren regulación y control, limitando autonomía.
- **Costos**: Automatizar toma tiempo y recursos.
- **Personal**: Los Devs ya tienen mucha carga de trabajo.