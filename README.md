# Wakanda Smart City - Sistema de Gestión de Servicios

---

**Integrantes:** * Gabriel Hernanz Rodríguez * Rodigo Yepes Rubio

## Descripción de la Solución
Sistema de microservicios basado en Spring Boot y Spring Cloud para la gestión inteligente de Wakanda. La arquitectura implementa patrones de descubrimiento de servicios, balanceo de carga en el lado del cliente y tolerancia a fallos.

### Lógica de Concurrencia
Se utiliza programación concurrente dentro de los microservicios (específicamente en `TrafficService`) utilizando `CompletableFuture` y `ThreadPoolTaskExecutor` para simular la lectura paralela de miles de sensores IoT sin bloquear el hilo principal.

### Descripción de Archivos
* **pom.xml (Raíz):** Orquestador de dependencias y versiones (Spring Cloud 2021.0.x / Spring Boot 2.7+).
* **wakanda-config-server:** Centraliza la configuración (archivos .yml) de todos los microservicios.
* **wakanda-discovery-server:** Servidor Eureka para el registro y descubrimiento dinámico.
* **wakanda-traffic-service:** Microservicio que gestiona sensores de tráfico. Implementa `@Async` para procesamiento concurrente.
* **wakanda-emergency-service:** Microservicio orquestador que consume datos de tráfico. Implementa **Circuit Breaker** (Resilience4j) para manejar caídas de otros servicios.
* **docker-compose.yml:** Despliegue de infraestructura de monitoreo (Zipkin para trazabilidad y Prometheus).
