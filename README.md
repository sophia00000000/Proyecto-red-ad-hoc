# Proyecto red ad-hoc

## Portada

**Título del Proyecto:** Implementación de Red Ad Hoc
**Materia:** Redes de Computación  
**Alumnos:** 

## Resumen Ejecutivo

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

## Diseño y Modelación de la Red

### Topología de la Red

La red estará compuesta por un mínimo de 4 nodos (PCs) organizados en una **topología mesh**. Cada nodo se conectará a varios de los otros, permitiendo la existencia de rutas múltiples y la capacidad de reconfiguración en caso de fallos. Se incluirán diagramas y esquemas que representen la distribución y las conexiones entre los nodos.

### Ubicación de Nodos

Se plantea la ubicación de los nodos en puntos estratégicos del campus para:
- Asegurar la cobertura integral en las áreas de interés.
- Minimizar la interferencia y los obstáculos físicos.
- Garantizar rutas de comunicación redundantes en caso de que algún nodo falle o se desconecte.

### Selección de Hardware

- **PCs:** Equipos con capacidad suficiente para ejecutar el protocolo BATMAN y gestionar la comunicación ad hoc.
- **Adaptadores Inalámbricos:** Que soporten el modo ad hoc y funcionen en las frecuencias seleccionadas (2.4 GHz o 5 GHz).
- **Accesorios Adicionales:** Posible uso de antenas de mayor ganancia o repetidores para mejorar el alcance en áreas críticas.

### Parámetros de Configuración

- **Asignación de IP:** Utilización de direcciones IP estáticas o dinámicas en un rango definido para la red mesh.
- **Frecuencia y Canal:** Selección de un canal de comunicación que minimice interferencias, evaluando la opción entre 2.4 GHz y 5 GHz.
- **Configuración del Protocolo BATMAN:**
  - Instalación del software BATMAN en cada nodo.
  - Ajuste de parámetros para optimizar el enrutamiento en función de la topología y condiciones ambientales.
- **Seguridad:** Implementación de medidas de cifrado y autenticación para proteger la integridad de la información transmitida.

## Herramientas y Simulación

Para la fase de simulación se utilizarán herramientas como **NS-3** o **OMNeT++**. Estas plataformas permitirán:
- Modelar y simular el comportamiento de la red mesh.
- Evaluar métricas de desempeño como latencia, tasa de transferencia y pérdida de paquetes.
- Validar la efectividad del protocolo BATMAN en la gestión de rutas dinámicas.

## Análisis de Riesgos y Seguridad

### Riesgos Técnicos

- **Interferencias:** Posibles interferencias de otros dispositivos o redes en el entorno universitario.
- **Variabilidad de la Topología:** Cambios en la configuración de la red debido a la movilidad o desconexión de nodos.
- **Errores de Configuración:** Fallos en la asignación de direcciones IP o en la configuración del protocolo BATMAN.

### Medidas de Seguridad

- **Cifrado de la Comunicación:** Implementación de protocolos de seguridad (como WPA2) para proteger la información.
- **Autenticación de Nodos:** Establecimiento de mecanismos de autenticación para evitar accesos no autorizados.
- **Monitoreo y Mantenimiento:** Procedimientos para el monitoreo constante de la red y la realización de ajustes preventivos ante fallos.

## Conclusiones y Siguientes Pasos

La modelación realizada establece una base sólida para la implementación de una red ad hoc mesh utilizando el protocolo BATMAN. Con la definición de la topología, selección de hardware y parámetros de configuración, se sientan las bases para:
- La simulación y validación del comportamiento de la red.
- La implementación en campo y la realización de pruebas de cobertura y rendimiento.
- La optimización continua de la red ante posibles fallos o cambios en el entorno.

## Referencias

- [Video de YouTube: Implementación de Red Ad Hoc con BATMAN](https://www.youtube.com/watch?v=121R1wPo2Eo)
- Documentación oficial del protocolo BATMAN. https://www.open-mesh.org/projects/batman-adv/wiki/Quick-start-guide
- Guías y manuales de configuración de redes ad hoc y mesh.
