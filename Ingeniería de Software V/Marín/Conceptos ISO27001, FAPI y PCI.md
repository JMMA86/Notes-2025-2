### **1. ISO 27001**

- **Qué es:**  
    Es un estándar internacional publicado por la _International Organization for Standardization_ (ISO) que define los requisitos para implementar un **Sistema de Gestión de Seguridad de la Información** (SGSI).
    
- **Objetivo:**  
    Proteger la confidencialidad, integridad y disponibilidad de la información mediante la gestión de riesgos y controles de seguridad.
    
- **En qué consiste:**
    - Establece políticas y procedimientos para manejar la seguridad.
    - Identifica riesgos y define medidas de control (técnicas, físicas y organizativas).
    - Requiere un ciclo de mejora continua (Planificar → Hacer → Verificar → Actuar, PHVA).
    
- **Ejemplo práctico:**  
    Una empresa certificada en ISO 27001 puede demostrar a sus clientes que gestiona los datos de forma segura y sigue estándares reconocidos mundialmente.
    

---

### **2. FAPI** _(Financial-grade API)_

- **Qué es:**  
    Es un conjunto de especificaciones de seguridad desarrollado por la **OpenID Foundation** para APIs usadas en entornos financieros o de alta seguridad.
    
- **Objetivo:**  
    Garantizar que las APIs que manejan información financiera o sensible cumplan requisitos de autenticación, autorización y protección de datos mucho más estrictos que los estándares web básicos.
    
- **En qué consiste:**
    - Basado en OAuth 2.0 y OpenID Connect, pero endurece la seguridad (ej. cifrado obligatorio, firmas digitales, validación estricta de tokens).
    - Diseñado para proteger contra ataques como _man-in-the-middle_, robo de tokens, _phishing_ y manipulación de datos.
        
- **Ejemplo práctico:**  
    En un sistema bancario, una aplicación de terceros que quiere acceder a tu cuenta debe pasar por FAPI para asegurar que la conexión y los datos estén totalmente protegidos.
    

---

### **3. PCI DSS** _(Payment Card Industry Data Security Standard)_

- **Qué es:**  
    Es un estándar de seguridad creado por el **PCI Security Standards Council** (formado por empresas como Visa, MasterCard, American Express, Discover y JCB).
    
- **Objetivo:**  
    Proteger la información de tarjetas de pago (crédito y débito) y prevenir fraudes.
    
- **En qué consiste:**
    - Requiere controles técnicos y administrativos para asegurar los datos de las tarjetas.
    - Incluye requisitos como: cifrar datos, restringir el acceso, monitorear redes, usar firewalls, realizar auditorías periódicas, etc.
    - Aplica a cualquier organización que procese, almacene o transmita datos de tarjeta.
        
- **Ejemplo práctico:**  
    Un e-commerce que procesa pagos debe cumplir PCI DSS para asegurar que los datos de la tarjeta no sean robados durante la transacción.
    

---

|Característica|**ISO 27001**|**FAPI (Financial-grade API)**|**PCI DSS**|
|---|---|---|---|
|**Tipo de estándar**|Norma internacional de gestión de seguridad de la información.|Conjunto de especificaciones técnicas de seguridad para APIs financieras.|Estándar de seguridad para datos de tarjetas de pago.|
|**Organismo responsable**|ISO (International Organization for Standardization) y IEC.|OpenID Foundation.|PCI Security Standards Council (Visa, MasterCard, etc.).|
|**Enfoque principal**|Proteger la información en general (confidencialidad, integridad, disponibilidad).|Garantizar seguridad robusta en APIs que manejan datos financieros o de alta sensibilidad.|Proteger datos de titulares de tarjetas y prevenir fraudes.|
|**Alcance**|Cualquier organización, sector o tamaño.|Servicios financieros, banca abierta, fintech, APIs de alto riesgo.|Empresas que procesan, almacenan o transmiten datos de tarjetas.|
|**Base tecnológica**|No se limita a una tecnología; abarca políticas, procesos y controles.|Basado en OAuth 2.0 y OpenID Connect con requisitos de seguridad reforzados.|Controles técnicos y operativos específicos para sistemas de pago.|
|**Certificación**|Sí, mediante auditoría externa acreditada.|No es una certificación formal, sino una conformidad técnica (implementación).|Sí, mediante auditorías y cumplimiento anual.|
|**Ejemplo práctico**|Empresa certificada ISO 27001 demuestra seguridad integral de sus datos.|API bancaria que cumple FAPI para permitir acceso seguro a cuentas por apps de terceros.|E-commerce que sigue PCI DSS para proteger datos de tarjetas durante pagos.|
