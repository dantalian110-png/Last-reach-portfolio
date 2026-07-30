# Last Reach — Technical Portfolio

> **Nota:** Este repositorio es una vitrina técnica de *Last Reach*, un proyecto de juego en desarrollo activo (Unreal Engine 5.8). El diseño completo del juego (GDD, balanceo, lore, contenido) se mantiene privado. Aquí comparto decisiones de arquitectura, extractos de código y el proceso de diseño técnico detrás del proyecto.

## Qué es Last Reach

*Last Reach* es un extraction shooter sci-fi PvPvE con raids cooperativas, desarrollado en Unreal Engine 5.8. El proyecto está en fase de diseño técnico y prototipo, con documentación de arquitectura desarrollada de forma iterativa junto con un proceso de auditoría técnica estricto (revisión línea por línea de cada decisión antes de implementarla).

## Decisiones de arquitectura destacadas

### Networking y Replicación
- Modelo de **servidores dedicados** con relevancia por niveles (tiered relevancy) e histéresis, para optimizar el ancho de banda sin sacrificar consistencia en combate
- Manejo de desconexiones con un modelo de **"frozen-but-vulnerable"**: el jugador desconectado queda congelado en el mundo pero sigue expuesto a riesgo, evitando exploits de desconexión defensiva

### Persistencia y Guardado
- Arquitectura **server-authoritative** para todo estado competitivo (inventario, progreso, resultados de extracción)
- Escritura **transaccional (write-through)** para evitar estados inconsistentes ante fallos de red o servidor
- Modelo de **sesión activa única** por jugador, con **generation-fencing** para manejar transferencias de sesión de forma segura (evita condiciones de carrera cuando un jugador se reconecta desde otro dispositivo)
- Resolución de casos límite: autorización mTLS entre servicios, mitigación de TOCTOU en verificación de estado de conexión, y consistencia eventual mediante saga pattern en el backend

### Proceso de diseño
Cada componente del sistema pasó por un proceso de revisión técnica estructurado: propuesta → implementación → auditoría línea por línea → aprobación. Esto incluyó identificar y resolver vulnerabilidades de seguridad (autenticación entre servicios, condiciones de carrera) antes de considerar cualquier sistema como completo.

## Stack técnico

- **Motor:** Unreal Engine 5.8
- **Arquitectura:** Servidores dedicados, backend con persistencia transaccional
- **Herramientas de desarrollo:** Flujo de trabajo asistido por Claude Code con agentes especializados para revisión de arquitectura y auditoría de código

## Sobre el diseño completo

El Game Design Document completo (facciones, sistema de progresión, economía de extracción, lore) se mantiene privado por ahora. Si te interesa conocer más detalle del diseño o del código, con gusto lo comparto en una llamada o con acceso puntual — escríbeme.

---
