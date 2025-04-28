# Instalación de OMNeT++ 6.1.0 en Ubuntu

---

## 1. Descargar OMNeT++

Descargar desde la página oficial:  
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

## Comandos totales resumen

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
```
