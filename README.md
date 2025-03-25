# Proyecto red ad-hoc

## Resumen

Este informe detalla la implementación de una red ad hoc tipo **mesh** que utiliza el **protocolo BATMAN**. El proyecto contempla un mínimo de 4 nodos (PCs) con el objetivo de establecer una red de comunicación robusta y dinámica en el campus universitario. Se aborda la configuración teórica, la selección de hardware, parámetros de comunicación, y se plantean estrategias para la simulación y análisis de la red.

## Introducción

Las redes ad hoc permiten la comunicación entre dispositivos sin depender de una infraestructura centralizada. En este proyecto se opta por una **red mesh**, que se caracteriza por su capacidad de auto-organización y de establecer múltiples rutas de conexión entre nodos, ofreciendo mayor redundancia y resiliencia. Para gestionar el enrutamiento de manera eficiente, se implementará el **protocolo BATMAN** (Better Approach To Mobile Ad-hoc Networking), el cual se adapta de forma dinámica a los cambios en la topología de la red.

## Objetivos del Proyecto

### Objetivo General

Implementar una red ad hoc mesh con al menos 4 nodos (PCs) que permita la transmisión de información en el campus universitario, utilizando el protocolo BATMAN para gestionar el enrutamiento dinámico.

### Objetivos Específicos

- **Diseñar** la topología de la red basada en una estructura mesh.
- **Seleccionar y configurar** el hardware, incluyendo PCs y adaptadores inalámbricos compatibles con modo ad hoc.
- **Definir** parámetros de comunicación como la asignación de direcciones IP, frecuencia y canal inalámbrico.
- **Implementar** el protocolo BATMAN para asegurar rutas de enrutamiento dinámicas y eficientes.
- **Analizar** la cobertura, interferencias y desempeño de la red en un entorno real.

## Marco Teórico

### Redes Ad Hoc y Red Mesh

Las **redes ad hoc** son sistemas de comunicación inalámbricos que se configuran de forma dinámica y descentralizada, permitiendo la conexión directa entre dispositivos sin infraestructura fija.  
La **red mesh** es una topología de red en la que cada nodo puede comunicarse con múltiples otros nodos, creando rutas alternativas y redundantes. Esto es especialmente útil en entornos donde la cobertura y la confiabilidad son fundamentales, como en un campus universitario.

### Protocolo BATMAN

El **protocolo BATMAN** (Better Approach To Mobile Ad-hoc Networking) es un algoritmo de enrutamiento diseñado para redes ad hoc. Entre sus características destacan:
- **Enrutamiento Dinámico:** Actualiza continuamente las rutas para adaptarse a los cambios en la topología.
- **Redundancia y Resiliencia:** Permite múltiples rutas de transmisión, lo que mejora la confiabilidad de la red.
- **Optimización del Tráfico:** Selecciona rutas basadas en la calidad del enlace, reduciendo la latencia y la pérdida de paquetes.
- **Simplicidad en la Implementación:** Facilita la configuración en entornos con nodos móviles o donde la conectividad es variable.

En el caso del protocolo BATMAN, este envía pequeños paquetes llamados OGM (Originator Message) para anunciar su presencia en cada nodo de la red, estos paquetes se propagan a través de la red, permitiendo a los nodos descubrir rutas posibles, de esta manera, en lugar de calcular una única ruta óptima en toda la red, cada nodo solo decide a qué vecino enviar los datos, basándose en la cantidad de OGMs recibidos, esto hace que el protocolo sea más flexible y resistente a cambios en la red. Si un nodo recibe OGMs de varios caminos, elige el más confiable (el que recibe con mayor frecuencia) y si una ruta se interrumpe, BATMAN la descarta y utiliza otra automáticamente.

### Direccionamiento
Para el protocolo BATMAN en una red ad-hoc, el direccionamiento suele ser plano y basado en IPv4, ya que es el mas sencilo y practico al todos los nodos compartir la misma red.

### Modulación y Canalización en una Red Ad-hoc con BATMAN
La modulación define cómo se transmiten los datos a nivel físico en la señal de radio. BATMAN no define una modulación específica, sino que usa la que proporciona el hardware Wi-Fi. Dependiendo de si se prueba en 2.4 GHz, se usa OFDM (802.11g/n) para evitar DSSS (que es más lento). Si se prueba en 5 GHz, se usa OFDM con 256-QAM (802.11ac o superior) para mayor velocidad.

La canalización define en qué frecuencia específica operará cada nodo de la red BATMAN.

Para redes en 2.4 GHz:
Hay 13 canales en la mayoría de los países, pero solo 3 no se solapan:
- Canal 1 (2412 MHz)
- Canal 6 (2437 MHz)
- Canal 11 (2462 MHz)

(Normalmente se recomienda usar el canal 6)

Para redes en 5 GHz:
- Más canales disponibles (36, 40, 44, 48... hasta 165).
- Se evita canales DFS (52-64 y 100-144) ya que pueden estar restringidos en algunos países o lugares.

(Normalmente se recomienda usar el canal 36 o 44)

## Características de los nodos
### Diseño y Modelación de la Red

#### Topología de la Red

La red estará compuesta por un mínimo de 4 nodos (PCs) organizados en una **topología mesh** (sistema wi-fi). Cada nodo se conectará a varios de los otros, permitiendo la existencia de rutas múltiples y la capacidad de reconfiguración en caso de fallos. Se incluirán diagramas y esquemas que representen la distribución y las conexiones entre los nodos.

#### Ubicación de Nodos

Se plantea la ubicación de los nodos en puntos estratégicos del campus para:
- Asegurar la cobertura integral en las áreas de interés.
- Minimizar la interferencia y los obstáculos físicos.
- Garantizar rutas de comunicación redundantes en caso de que algún nodo falle o se desconecte.

#### Selección de Hardware

- **PCs:** Equipos con capacidad suficiente para ejecutar el protocolo BATMAN y gestionar la comunicación ad hoc.

#### Parámetros de Configuración

- **Asignación de IP:** Utilización de direcciones IP estáticas o dinámicas en un rango definido para la red mesh.
- **Frecuencia y Canal:** Selección de un canal de comunicación que minimice interferencias, evaluando la opción entre 2.4 GHz y 5 GHz.
- **Configuración del Protocolo BATMAN:**
  - Instalación del software BATMAN en cada nodo.
  - Ajuste de parámetros para optimizar el enrutamiento en función de la topología y condiciones ambientales.
  - Involucra el uso de herramientas como **bactl** para ver la tabla de enrutamiento, vecinos y calidad del enlace.

## Servicios
Con una red ad-hoc basada en el protocolo B.A.T.M.A.N., se puede ofrecer varios servicios descentralizados sin necesidad de un punto de acceso central. Algunos de los servicios que podrías implementar incluyen:
- Intercambio de datos: implementar servicios de transferencia de archivos entre nodos utilizando protocolos como FTP O SCP.
- Comunicación y colaboración: se habilitan aplicaciones de mensajería o VOIP para evaluar la latencia y estabilidad.
- Servicios web locales: hospedar paginas web o aplicaciones internas, un ejmeplo de esto puede ser el portal informativo para el campus.
- Monitoreo y gestión: Se intalan herramientas de supervisión para registrar el trafico, detectar anomalías y generar alertas en caso de incidencias.
- Requerimientos de seguridad y rendimiento: Se establece parámetros claros de ancho de banda y latencia máxima para cada servicio. Tambien implementar mecanismos de autenticación y cifrado (por ejemplo, WPA2 para la red ad hoc o VPN sobre la malla) para aseurar la comunicación.

## Pruebas a realizar

### Herramientas y Simulación
Para la fase de simulación se utilizarán herramientas como NS-3 o OMNeT++. Estas plataformas permitirán:
- Modelar y simular el comportamiento de la red mesh.
- Evaluar métricas de desempeño como latencia, tasa de transferencia y pérdida de paquetes.
- Validar la efectividad del protocolo BATMAN en la gestión de rutas dinámicas.

### Análisis de Riesgos y Seguridad

#### Riesgos Técnicos
- **Interferencias:** Posibles interferencias de otros dispositivos o redes en el entorno universitario.
- **Variabilidad de la Topología:** Cambios en la configuración de la red debido a la movilidad o desconexión de nodos.
- **Errores de Configuración:** Fallos en la asignación de direcciones IP o en la configuración del protocolo BATMAN.

### Medidas de Seguridad

- **Cifrado de la Comunicación:** Implementación de protocolos de seguridad (como WPA2) para proteger la información.
- **Autenticación de Nodos:** Establecimiento de mecanismos de autenticación para evitar accesos no autorizados.
- **Monitoreo y Mantenimiento:** Procedimientos para el monitoreo constante de la red y la realización de ajustes preventivos ante fallos.

### Plan de pruebas detallado

#### Cobertura y Alcance
- Realizar mediciones de intensidad de señal (RSSI) en diversos puntos del campus para identificar áreas con buena y mala cobertura.
- Mapeo de zonas con interferencias y propuesta de soluciones (cambio de canal o reubicación de los nodos).

#### Evaluación del Rendimiento
- **Latencia:** Medir los tiempos de respuesta con el comando ping, estableciendo un criterio de éxito (por ejemplo, latencia menor de 50 ms para aplicaciones VoIP).
- **Tasa de transferencia:** Usar iperf en modos TCP y UDP para evaluar la velocidad de transferencia, definiendo una tasa de transferencia mínima esperada (por ejemplo, 10 Mbps en condiciones normales).
- **Pérdida de paquetes:** Usar herramientas como mtr para analizar la estabilidad y detectar pérdida de paquetes, asegurando que la tasa de pérdida no supere el 2% en condiciones normales.

#### Pruebas de Comunicación entre Nodos
- Enviar y recibir mensajes personalizados utilizando herramientas como netcat o una aplicación de chat basada en sockets.
- Evaluar la latencia y tasa de entrega de mensajes en diferentes condiciones de la red.
- Medir la capacidad de la red para manejar múltiples mensajes simultáneamente sin degradación significativa.
- Comparar el rendimiento con diferentes tamaños de mensajes (mensajes cortos vs. largos).

#### Pruebas de Integridad y Seguridad en Mensajería
- Verificar que los mensajes no se corrompan o pierdan durante la transmisión.
- Implementar cifrado en la comunicación mediante OpenSSL o GnuPG para garantizar la seguridad de los mensajes.
- Probar retransmisión en caso de fallos en la entrega de mensajes.

#### Robustez y Resiliencia
- Simular fallos desconectando intencionalmente un nodo y verificar que la red se reconfigura automáticamente mediante BATMAN.
- Realizar pruebas de escalabilidad añadiendo nuevos nodos y evaluando el impacto en el desempeño.

#### Documentación y Registro de Resultados
- Crear plantillas para anotar resultados y observaciones durante cada prueba.
- Presentar los resultados en tablas comparativas para un análisis más claro.

## Conclusiones y Siguientes Pasos

La modelación realizada establece una base sólida para la implementación de una red ad hoc mesh utilizando el protocolo BATMAN. Con la definición de la topología, selección de hardware y parámetros de configuración, se sientan las bases para:
- La simulación y validación del comportamiento de la red.
- La implementación en campo y la realización de pruebas de cobertura y rendimiento.
- La optimización continua de la red ante posibles fallos o cambios en el entorno.

## Referencias

- [Video de YouTube: Implementación de Red Ad Hoc con BATMAN](https://www.youtube.com/watch?v=121R1wPo2Eo)
- Documentación oficial del protocolo BATMAN. https://www.open-mesh.org/projects/batman-adv/wiki/Quick-start-guide
- Guías y manuales de configuración de redes ad hoc y mesh.
