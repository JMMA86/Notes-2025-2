Investigar:
- Tipos de autenticación B2B, B2C.
- Cómo configurar un dominio en Docker.
- Qué es DRP.
- Investigar Twelve Factor Apps.

**1. Tipos de autenticación B2B y B2C**

- **B2B (Business to Business)**: Autenticación pensada para empresas que interactúan entre sí. Suele usar **SSO corporativo**, **SAML**, **OpenID Connect**, **LDAP**, integración con Active Directory o certificados digitales. Permite que un empleado use sus credenciales corporativas para acceder a servicios de otra empresa.

- **B2C (Business to Consumer)**: Autenticación para clientes finales. Se usan **correo/contraseña**, **OAuth2 con redes sociales** (Google, Facebook, Apple), **MFA** (doble factor), **Magic Links**. Prioriza facilidad de uso y escalabilidad más que integraciones corporativas.

**2. Cómo configurar un dominio en Docker**

- Paso básico: Mapear el puerto de tu contenedor a la máquina host y configurar DNS para apuntar tu dominio a la IP pública del servidor.

- Ejemplo:
    1. En el servidor, ejecutar contenedor:
        ```bash
		docker run -d -p 80:80 --name miapp imagen
        ```

    2. Apuntar dominio desde el panel de tu proveedor (A → IP del servidor).

    3. Opcional: Usar **nginx** como _reverse proxy_ dentro o fuera de Docker para servir el dominio y manejar HTTPS con **Let’s Encrypt** (Certbot).

    4. También puedes usar **docker-compose** con `nginx-proxy` + `letsencrypt-companion` para automatizar.

**3. DRP**
- Es un **plan de recuperación ante desastres**: conjunto de procedimientos y herramientas para restaurar sistemas y datos tras fallas graves (ciberataques, fallos de hardware, desastres naturales).

- Incluye copias de seguridad, redundancia, failover, pruebas periódicas y tiempos de recuperación (RTO/RPO).

**4. Twelve-Factor Apps**  
Metodología para desarrollar apps SaaS modernas, portables y escalables. Los 12 principios:

1. **Codebase**: Una sola base de código, múltiples despliegues.
2. **Dependencies**: Declarar y aislar dependencias.
3. **Config**: Configuración en variables de entorno.
4. **Backing services**: Tratar servicios externos como recursos adjuntos.
5. **Build, release, run**: Separar claramente estas etapas.
6. **Processes**: Ejecutar como procesos sin estado.
7. **Port binding**: Exportar servicios vía puerto.
8. **Concurrency**: Escalar mediante procesos.
9. **Disposability**: Inicios/paradas rápidas y seguras.
10. **Dev/prod parity**: Mantener entornos similares.
11. **Logs**: Tratar logs como flujos de eventos.
12. **Admin processes**: Ejecutar tareas admin como procesos puntuales.