Apache **Kafka** es una **plataforma de mensajería distribuida** y de **procesamiento de flujos de datos en tiempo real**.  
Se usa principalmente para **publicar, suscribir, almacenar y procesar** grandes volúmenes de datos de manera confiable y muy rápida.  

**Conceptos principales de Kafka:**

1. **Producer (productor)** → Es el que envía mensajes (eventos) a Kafka.  
2. **Consumer (consumidor)** → Es el que lee los mensajes desde Kafka.  
3. **Topic (tópico)** → Es como un "canal" o "categoría" donde se publican los mensajes.  
4. **Partition (partición)** → Cada tópico puede dividirse en particiones, lo que permite paralelismo y escalabilidad.  
5. **Broker** → Servidor de Kafka que almacena y distribuye los mensajes.  
6. **Cluster** → Conjunto de brokers que trabajan juntos para dar alta disponibilidad y tolerancia a fallos.  
7. **Zookeeper (antes, ahora opcional)** → Servicio que coordinaba los brokers, aunque las versiones recientes de Kafka pueden funcionar sin él.  

**¿Por qué es útil?**
- Maneja **millones de mensajes por segundo**.  
- Sirve para **integración de sistemas** (como un bus de datos).  
- Permite **procesamiento en tiempo real** (ejemplo: detectar fraudes en pagos al instante).  
- Se usa para **event-driven architectures** (arquitecturas orientadas a eventos).  

### 🛒 **Ejemplo: E-commerce con Kafka**
Un usuario compra un producto en una tienda. Esa sola acción **genera muchos eventos** que deben ser atendidos por distintos sistemas al mismo tiempo:

1. **El usuario paga** → El **Producer** (aplicación de pagos) envía un mensaje a Kafka en el tópico **`pagos`**.  

2. Kafka guarda el evento en una **partición del tópico**.  

3. Varios **Consumers** leen el mensaje:  
   - **Sistema de facturación** → Genera la factura.  
   - **Sistema de inventario** → Descuenta el producto vendido del stock.  
   - **Sistema de envíos** → Prepara la orden para envío.  
   - **Sistema de notificaciones** → Le manda al cliente un correo o notificación de confirmación.  

**Todos reciben el evento al mismo tiempo**, sin que el sistema de pagos tenga que hablar directamente con cada uno.  

### ¿Por qué usar Kafka aquí?
- Si mañana agregas un nuevo servicio, por ejemplo, un **sistema de análisis de compras** para recomendar productos, simplemente lo conectas como un **nuevo Consumer al tópico `pagos`**, y empieza a recibir los eventos sin cambiar el resto.  
- Kafka puede manejar **miles de compras por segundo** sin caerse.  

Kafka actúa como un **megáfono inteligente**: un sistema anuncia un evento (compra realizada) y todos los que estén interesados lo escuchan al mismo tiempo y reaccionan.  