# Instalación de OMNeT++ 6.1.0 en Ubuntu

---

## 1. Descargar OMNeT++

Descargar desde la página oficial  
Archivo descargado:

```
omnetpp-6.1.0-linux-x86_64.tgz
```

---

## 2. Descomprimir OMNeT++

```bash
sudo apt install tar
tar -xvzf omnetpp-6.1.0-linux-x86_64.tgz
cd omnetpp-6.1.0
```

---

## 3. Configurar entorno

Antes de configurar, cargar las variables de entorno:

```bash
. setenv
```

---

## 4. Crear entorno virtual

Ubuntu tiene configurado Python para proteger el sistema y no permite instalar paquetes directamente usando pip en el sistema base para evitar romper cosas. Para solucionarlo se crea un entorno virtual (virtual environment).

Esto es limpio, seguro y la forma "correcta" en Ubuntu moderno:

```bash
sudo apt install python3.12-venv
python3 -m venv mi_entorno
source mi_entorno/bin/activate
pip install setuptools numpy scipy pandas matplotlib
```

---

## 5. Instalar todas las dependencias necesarias

Se utilizó un único comando para instalar casi todas las dependencias requeridas:

```bash
sudo apt-get install build-essential gcc g++ bison flex perl python3 python3-pip qtbase5-dev qtchooser qt5-qmake qtbase5-dev-tools libqt5opengl5-dev libxml2-dev zlib1g-dev default-jre doxygen graphviz
```

| Paquete | Descripción |
|:--------|:------------|
| `build-essential` | Herramientas básicas de compilación (`gcc`, `g++`, `make`, etc.) |
| `gcc` | Compilador de C |
| `g++` | Compilador de C++ |
| `bison` | Generador de analizadores sintácticos |
| `flex` | Generador de analizadores léxicos |
| `perl` | Lenguaje de scripting usado por scripts de OMNeT++ |
| `qtbase5-dev` | Bibliotecas de desarrollo de Qt5 |
| `qtchooser` | Selector de versiones de Qt instaladas |
| `qt5-qmake` | Herramienta de construcción de proyectos Qt (`qmake`) |
| `qtbase5-dev-tools` | Herramientas adicionales de desarrollo de Qt (`moc`, `uic`, `rcc`) |
| `libqt5opengl5-dev` | Biblioteca OpenGL para Qt5, para vistas gráficas 3D |
| `libxml2-dev` | Librería de manejo de XML |
| `zlib1g-dev` | Librería de compresión zlib |
| `default-jre` | Java Runtime Environment por defecto |
| `doxygen` | Herramienta para documentar el código fuente |
| `graphviz` | Herramienta de visualización de grafos |

---

## 6. Instalar OpenSceneGraph

Para la compatibilidad con la vista 3D de Qtenv:

```bash
sudo apt-get install libopenscenegraph-dev
```

---


## 7. Configurar y Compilar OMNeT++

Configurar el entorno de compilación:

```bash
./configure
```

Compilar OMNeT++ (puede tardar varios minutos):

```bash
make
```

---

## Notas Finales

- Cada vez que se abra una nueva terminal, es necesario cargar el entorno de OMNeT++ con:

```bash
. setenv
```

- Si no se desea soporte para vista 3D (OpenSceneGraph), se puede desactivar editando el archivo `configure.user` y colocando:

```
WITH_OSG=no
```

---

# Configuración de B.A.T.M.A.N

Para INET 4.5 (biblioteca de modelos de código abierto para la simulación de redes de comunicación), la mejor opción es utilizar INETMANET ya que contiene los protocolos MANET incluyendo BATMAN, específicamente diseñados para ser compatibles con la versión de INET. Para descargarlo se utilizan los siguientes comandos:

```bash
sudo apt install git
git clone https://github.com/aarizaq/inetmanet-4.x.git
cd inetmanet-4.x
git checkout v4.2.x
find . -name "Batman" -o -name "batman"
```

Clic en File -> Import

![imagen](https://github.com/user-attachments/assets/5cbe2af0-f627-45b8-993f-bd07f863b250)

Clic en General -> Existing Projects into Workspace

![imagen](https://github.com/user-attachments/assets/65d66750-a723-4e06-8078-b4ffd0adf9a6)

Seleccionar la carpeta inetmanet-4.x -> Finish

![imagen](https://github.com/user-attachments/assets/7d17acff-691d-48c0-90f7-27323613ecf9)

Y así está disponible B.A.T.M.A.N junto con el ejemplo base a utilizar: ieee80211

**Ruta:** inetmanet-4.x/examples/adhoc/ieee80211/

![imagen](https://github.com/user-attachments/assets/40167b4e-2a17-4977-9d5f-98b2328e9edc)


## Configuración de ieee80211

**Ruta:** inetmanet-4.x/src/inet/routing/extras/Batman.ned

![imagen](https://github.com/user-attachments/assets/dc0605d4-be3a-4c37-ad08-f3c0318e23b2)

Agregar al final del archivo Batman.net el siguiente fragmento de còdigo:

```bash
gates:
    input upperIn;
    output upperOut;
    input lowerIn;
    output lowerOut;
```
En OMNeT++, los gates son puntos de entrada y salida que permiten que los módulos simples se comuniquen entre sí. Cuando se modelan redes, estos gates permiten el envío y recepción de mensajes entre capas (por ejemplo, entre la capa de red y la capa de enlace o aplicación). INETMANET a veces tiene módulos heredados o incompletos, y al personalizarlo era necesario permitir conexiones explícitas entre módulos.

**Ruta:** inetmanet-4.x/src/inet/routing/extras/batman/BatmanMain.cc

![imagen](https://github.com/user-attachments/assets/a55fb165-04b0-430b-8331-9f19295f23f7)

Hay que hacer varios cambios en el archivo BatmanMain.cc, primero, se agregaron cabeceras para obtener información de movilidad, manipular archivos y trabajar con coordenadas:

```bash
#include <fstream>  // Para escribir en archivos
#include "inet/mobility/contract/IMobility.h"  // Para acceder a la posición de los nodos
#include "inet/common/geometry/common/Coord.h"
#include "inet/common/ModuleAccess.h"
#include "inet/common/INETUtils.h"
```
Para poder obtener la posición del nodo que recibe un paquete y del nodo que lo originó, calcular la distancia entre ellos y guardar esos datos en un archivo .txt.

Segundo, se modificó handleMessageWhenUp() para calcular distancia y guardar resultados

Se añadió un bloque que:

- Obtiene el módulo de movilidad del nodo receptor.
- Encuentra el módulo de movilidad del nodo emisor (data->getOrig()).
- Calcula la distancia entre ellos.
- Guarda en un archivo llamado resultados.txt la siguiente información:

    - Tiempo de simulación
    - Nombre del nodo receptor
    - Dirección del nodo origen
    - Reenviado por
    - TTL, TQ, Hops, SeqNumber
    - Distancia en metros

Ejemplo del código:

```bash
std::ofstream outTxt("resultados.txt", std::ios::app);
outTxt << "Tiempo: " << simTime()
       << ", Nodo: " << getParentModule()->getFullName()
       << ", Origen: " << data->getOrig()
       ...
       << ", Distancia: " << distance << " m";
```
Esto para analizar el comportamiento del protocolo BATMAN en una red móvil y estudiar cómo varía la distancia entre nodos con respecto al reenvío de paquetes, TTL o calidad del enlace (TQ), en el caso de la distancia siempre va a aparecer *N/A* debido a que BATMAN no calcula la distancia completa entre un nodo origen y un destino. Su enfoque se basa en encontrar el mejor vecino de un solo salto para cada destino, en lugar de determinar la ruta óptima completa.
  
## Resumen Comandos totales

```bash
sudo apt install tar
tar -xvzf omnetpp-6.1.0-linux-x86_64.tgz
cd omnetpp-6.1.0
sudo apt install python3.12-venv
python3 -m venv mi_entorno
source mi_entorno/bin/activate
pip install setuptools numpy scipy pandas matplotlib
. setenv
sudo apt-get install build-essential gcc g++ bison flex perl qtbase5-dev qtchooser qt5-qmake qtbase5-dev-tools libqt5opengl5-dev libxml2-dev zlib1g-dev default-jre doxygen graphviz
sudo apt-get install libopenscenegraph-dev
./configure
make
sudo apt install git
git clone https://github.com/aarizaq/inetmanet-4.x.git
cd inetmanet-4.x
git checkout -b inet4.5 origin/inet4.5
```
