## ¿Qué es DevOps?

### Definición de DevOps
- DevOps es un **conjunto de prácticas** destinadas a **reducir el tiempo entre un cambio en el sistema y su despliegue en producción**, manteniendo **alta calidad**.
- No se enfoca en herramientas específicas, sino en **lograr objetivos**: entrega rápida y confiable.

### Objetivos clave
- **Calidad del cambio:** seguridad, disponibilidad, fiabilidad, etc.
- **Calidad del proceso de entrega:** debe ser **repetible y confiable**.
- Inicia cuando un desarrollador hace un commit y termina cuando el código pasa pruebas en producción.

## Prácticas comunes de DevOps
1. **Incluir a Ops desde los requisitos**: considerar sus necesidades desde el inicio.
2. **Desarrolladores responsables de incidentes iniciales** tras un despliegue.
3. **Proceso de despliegue uniforme y obligatorio** para Dev y Ops.
4. **Despliegue continuo**: pruebas automáticas desde el commit hasta producción.
5. **Infraestructura como código**: scripts de despliegue tratados como software.

### Ejemplo real: IMVU
- Hacen **50 despliegues diarios**.
- Cada commit pasa por una batería de pruebas automáticas (~9 min) antes de desplegarse en algunos servidores.
- Si no hay errores, se despliega en todo el clúster; si hay problemas, se revierte automáticamente.
- Cada error genera una nueva prueba para prevenir repeticiones.

## Motivación: ¿Por qué DevOps?
- **Problema central**: lanzamientos lentos y costosos.
- **Objetivo**: reducir tiempo al mercado y evitar errores en despliegues.
- Las tareas manuales y la falta de coordinación causan errores y demoras.

## Barreras y desafíos
- **Cultura organizacional**: algunas industrias (como salud o finanzas) temen al riesgo más que valoran la rapidez.
- **Intereses enfrentados**:
    - _Dev quiere lanzar código rápido_.
    - _Ops quiere mantener estabilidad_.
- **Silos departamentales**: cada área cuida sus intereses.
- **Soporte de herramientas**: requiere experiencia, configuración y mantenimiento.
- **Costos personales**: tareas que pasan de Ops a Dev pueden ser más caras.

## Estructura de equipos DevOps
- **Equipos pequeños** (regla de “dos pizzas” de Amazon).
- Roles principales:
    - **Team Lead**: facilitador.
    - **Team Member**: desarrolla y entrega.
    - **Service Owner**: coordina con otros equipos y stakeholders.
    - **Reliability Engineer**: monitoriza y responde a fallos post-despliegue.
    - **Gatekeeper**: decide si el software pasa a la siguiente etapa.
    - **DevOps Engineer**: gestiona herramientas del pipeline (CI/CD, scripts, config).

## Relación con Agile
- DevOps complementa Agile enfocándose en la **entrega continua** y la **automatización del pipeline**.
- Impacta las tres fases del desarrollo ágil:
    1. **Inicio**: planificación, requisitos, coordinación con Ops.
    2. **Construcción**: CI/CD, pruebas automatizadas.
    3. **Transición**: despliegue, monitoreo y rollback por el mismo equipo.

## Coordinación eficiente
- DevOps busca **reducir la necesidad de coordinación manual**.
- Usa automatización (versionado, CI/CD, monitoreo) para evitar errores y acelerar entregas.
- Minimiza coordinación entre equipos al usar:
    - Arquitecturas desacopladas (microservicios).
    - Definiciones claras de responsabilidades y datos.