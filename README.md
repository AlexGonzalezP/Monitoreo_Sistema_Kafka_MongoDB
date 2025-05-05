# Ejercicio Práctico: Pipeline de Procesamiento y Agregación de Métricas de Sistema con Python, Kafka y MongoDB Atlas

## Curso: Big Data Aplicado

### Descripción General

Este proyecto simula un sistema de monitorización de infraestructura en el que varios servidores (simulados) reportan periódicamente métricas de rendimiento. Estas métricas se transmiten en tiempo real mediante Apache Kafka, se almacenan en crudo en MongoDB Atlas, y se procesan para calcular KPIs agregados que también se almacenan en otra colección de MongoDB para análisis posterior.

### Objetivo del Proyecto

- Simular métricas de rendimiento (CPU, memoria, disco, red, errores) desde múltiples servidores.
- Enviar estas métricas en tiempo real a través de Kafka.
- Consumir y almacenar estas métricas en MongoDB Atlas.
- Calcular KPIs agregados cada 20 mensajes recibidos.
- Almacenar los KPIs en una segunda colección para su análisis y visualización.

### Arquitectura

- **Productor de métricas (Python)**: Genera métricas simuladas para varios servidores y las envía al topic de Kafka `system-metrics-topic-iabd06`.
- **Kafka**: Middleware de mensajería que actúa como intermediario entre el productor y el consumidor.
- **Consumidor (Python)**: Escucha el topic de Kafka, almacena cada mensaje en MongoDB Atlas (colección `system_metrics_raw_iabd06`) y cada 20 mensajes calcula KPIs, que almacena en la colección `system_metrics_kpis_iabd06`.

### Herramientas Utilizadas

- **Apache Kafka**: Middleware para el envío y consumo de mensajes.
- **Python**: Scripts para generar, consumir y procesar las métricas.
- **MongoDB Atlas**: Base de datos en la nube para almacenar métricas y KPIs.
- **Docker Compose**: Para levantar el entorno de Kafka.

### Instrucciones Generales

1. **Levantar Kafka**:
   - Usa el archivo `docker-compose.yml` proporcionado para iniciar el broker de Kafka.
   - El broker estará disponible en `IP_LOCAL:29092`.

2. **Ejecutar el Productor**:
   - El script `productor_metrics_iabd06.py` simula el envío de métricas para cinco servidores cada 10 segundos.
   - Las métricas incluyen CPU, memoria, disco, red y errores.

3. **Ejecutar el Consumidor**:
   - El script `consumidor_metrics_iabd06.py` escucha el topic de Kafka, almacena las métricas crudas y cada 20 mensajes calcula KPIs agregados.
   - Los KPIs incluyen promedios de uso de recursos, suma de errores y tasa de procesamiento.

4. **Almacenamiento en MongoDB Atlas**:
   - Las métricas se almacenan en `system_metrics_raw_iabd06`.
   - Los KPIs se almacenan en `system_metrics_kpis_iabd06`.

### KPIs Calculados

- Promedio de uso de CPU (`cpu_percent_avg`)
- Promedio de uso de Memoria (`memory_percent_avg`)
- Promedio de I/O en disco (`disk_io_mbps_avg`)
- Promedio de tráfico de red (`network_mbps_avg`)
- Suma de errores (`error_count_sum`)
- Tasa de procesamiento (`tasa_procesamiento_msg_seg`)

---

### Autor

Alumno del curso *Big Data Aplicado*, IABD06.
