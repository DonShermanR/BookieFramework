==============================
BOOKIE Framework - Manual de Usuario
==============================

Introducción
============
El **BOOKIE Framework** es una interfaz gráfica creada con **PyQt5** que permite ejecutar distintos scripts relacionados con el manejo de bases de datos y análisis de cookies. La aplicación está diseñada para facilitar la interacción con los scripts de una manera intuitiva, utilizando botones con íconos y descripciones claras.

Requisitos
==========
- **Python 3.8 o superior**
- **PyQt5**: Instalable utilizando `pip install pyqt5`
- Scripts adicionales ubicados en las rutas especificadas dentro del código fuente.

Instalación
===========
1. Clonar o descargar el código del proyecto.
2. Asegúrese de tener **Python 3.8 o superior** instalado.
3. Instalar las dependencias con el siguiente comando:


Interfaz de Usuario
===================
La ventana principal del framework está dividida en varias secciones:

1. **Encabezado Principal**: Contiene el logo de la Escuela Politécnica Nacional y el título del proyecto.
2. **Botones de Funcionalidades**: Un conjunto de botones que permiten acceder a las diferentes características del framework.

Descripción de la Interfaz
==========================

Ventana Principal
-----------------
- **Título**: La ventana tiene como título "BOOKIE Framework".
- **Tamaño**: La ventana se ajusta automáticamente al 50% del tamaño de la pantalla.
- **Estilo**: Fondo blanco, con textos y botones estilizados con colores azul (#4285F4).

Botones Disponibles en la Ventana Principal
-------------------------------------------
- **Merge Databases**: Abre un submenú para fusionar bases de datos de historial y cookies.
- **Show Statistics**: Abre un submenú para visualizar estadísticas de bases de datos.
- **Normalize Databases**: Abre un submenú para normalizar las bases de datos de URLs y cookies.
- **CookieScout Algorithm**: Ejecuta el script del algoritmo CookieScout.
- **BOOKIE Browser**: Ejecuta el navegador BOOKIE.
- **Help**: Muestra información de ayuda.
- **Exit**: Cierra la aplicación.

Submenús
========

### Submenú - Merge Databases
Este submenú permite seleccionar entre dos opciones:

1. **Merge History Databases**: Ejecuta el script para fusionar bases de datos de historial.
2. **Merge Cookies Databases**: Ejecuta el script para fusionar bases de datos de cookies.

### Submenú - Show Statistics
Permite visualizar estadísticas relacionadas con las bases de datos:

1. **URLs Database Statistics**: Muestra estadísticas de la base de datos de URLs.
2. **Cookies Database Statistics**: Muestra estadísticas de la base de datos de cookies.

### Submenú - Normalize Databases
Este submenú ofrece dos opciones para normalizar bases de datos:

1. **Normalize URLs Database**: Ejecuta el script para normalizar la base de datos de URLs.
2. **Normalize Cookies Database**: Ejecuta el script para normalizar la base de datos de cookies.

Instrucciones para Ejecutar Scripts
===================================
Los scripts son ejecutados mediante los botones dentro de la aplicación. Cuando se presiona un botón asociado a un script, se utiliza el módulo **subprocess** para ejecutarlo.

Cada script está asociado a un botón en particular. Las rutas de los scripts se encuentran en el diccionario `script_paths` en el código fuente.

Ejemplo:
--------
Si el usuario presiona el botón **Merge History Databases**, se ejecutará el script `1.1MergeHistoriales.py`.

Errores Potenciales
===================
En caso de que ocurra un error al ejecutar un script, el framework mostrará el error en la consola, incluyendo el nombre del script y el tipo de excepción.

Estilos de Botones
==================
Los botones dentro del framework están estilizados con las siguientes características:
- **Color de fondo**: Azul (#4285F4).
- **Texto**: Blanco, con tamaño de fuente 18 px y negrita.
- **Iconos**: Los botones tienen íconos asociados que representan gráficamente la acción que realizan.



