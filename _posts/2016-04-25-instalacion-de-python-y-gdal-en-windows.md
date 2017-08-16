---
title:  "Instalaci�n de Python y GDAL en Windows"
  categories: 
  - blog
  tags:
  - catastro, python, script, gdal, windows
---

Dentro del programa de la [11� reuni�n de Geoinquietos C�rdoba](http://wiki.osgeo.org/wiki/Reuni%C3%B3n_11_Geoinquietos_C%C3%B3rdoba) voy a realizar de mini taller donde explicar c�mo se usa el script Pyhton [**dxf2gmlcatastro**](https://github.com/sigdeletras/dxf2gmlcatastro) que estoy generando para convertir un archivo CAD DXF al formato GML definido por tras la [Resoluci�n conjunta Catastro-Registro](http://www.catastro.minhap.es/documentos/formatos_intercambio/Formato%20GML%20parcela%20catastral.pdf).

Desde hace unos meses he empezado a aprender Python y su aplicaci�n temas geo. Este ejercicio de programaci�n me est� sirviendo bastante para ir adquiriendo los conocimientos b�sicos de este lenguaje. Adem�s de las lecturas y pruebas, la ayuda de Marcos Ortega de [Indavelopers](http://www.indavelopers.com/) est� siendo crucial.

Un r�pido sondeo ha puesto de manifiesto que la mayor�a de las personas que asistente a las reuniones de geoinquietos usan Windows. Aunque todo la programaci�n est� hecha en Linux (Ubuntu), he montado una m�quina virtual con Virtual Box para ver los pasos a dar para poder ejecutar el script en este sistema operativo. Existe una manera m�s r�pida de configurar GDAL para Python que es instalando OSGeo4W y usar la _shell_ incorporada. Pero como siempre es un buen momento para aprender he decido tomar el camino m�s largo y aprovechar para escribir esta entrada.

## Instalaci�n de Python

Para instalar Python es necesario entrar en el apartado de descargas de la p�gina de [Pyhton](https://www.python.org/downloads/windows/)) y bajarse la versi�n del lenguaje que se quiera instalar seg�n el sistema operativo. Para esta gu�a hemos utilizado _Python 3.4.4 - 2015-12-21 Windows x86 MSI installer_.

Una vez descargada, ejecutamos el archivo e instalamos seg�n la configuraci�n por defecto. El �nico aspecto al que en principio hay que atender es a marcar, si no lo est�, la casilla que a�ade python.exe a nuestro PATH.

![](/images/blog/01.png)

Terminada la instalaci�n, accedemos a _Sistema>Configuraci�n avanzada del sistema_ y pinchamos en el bot�n _Variables del entorno_. Desde aqu�, podemos comprobar que se ha a�adido la ruta a la carpeta de Python, en nuestro caso "C:\Python34", para la variable PATH. Editamos esta variable y a�adimos tambi�n las rutas C:\Python34\Lib\site-packages\ y C:\Python34\Scripts.

## Instalaci�n de GDAL

Para poder usar la biblioteca geoespacial [GDAL](https://es.wikipedia.org/wiki/GDAL) con Python es necesario tener instalados los binarios con anterioridad. Esta parte de la entrada recoge la gu�a en ingl�s del siguiente [enlace](http://sandbox.idre.ucla.edu/sandbox/tutorials/installing-gdal-for-windows).

Lo primero es saber la versi�n del compilador que estamos utilizando. Para ello buscamos en nuestros programas IDLE (Python GUI) dentro de la carpeta de Python y lo ejecutamos. En la informaci�n de inicial podemos apreciar la versi�n del compilador (MSC v.1600). En este mismo texto obtendremos la arquitectura de nuestra m�quina (32 o 64 bits).

![](/images/blog/02_ilde.png)

Recopilados estos datos, entramos en la web [www.gisinternals.com](http://www.gisinternals.com/release.php) para acceder a los archivos de GDAL seg�n nuestra configuraci�n (ej. release-1600-gdal-1-11-3-mapserver-6-4-2). Una vez en la p�gina de descarga, localizaremos el enlace del core de GDAL (Generic installer for the GDAL core components), descargamos e instalamos. Para nuestro equipo el archivo descargado ha sido _gdal-111-1600-core.msi_

Tras la instalaci�n, tendremos que volver a editar de nuevo las variables del entorno y a�adiremos a PATH, precedida de punto y coma, la direcci�n de la carpeta de GDAL de nuestro equipo (ej. ;C:\Program Files (x86)\GDAL).

A continuaci�n debemos a�adir dos variables nuevas:

*   GDAL_DATA que apunte a la carpeta gdal-data (C:\Program Files (x86)\GDAL\gdal-data)
*   GDAL_DRIVER_PATH que apunte a la carpeta gdalplugins (C:\Program Files (x86)\GDAL\gdalplugins)

Para comprobar que hemos realizado correctamente la instalaci�n accederemos al S�mbolo del sistema como administrador y escribiremos _gdalinfo --version_. Si todo es correcto obtrendremos la versi�n de GDAL instalada

![](/images/blog/03_gdalinfo.png)

## Instalaci�n de Python _bindings_

Para poder utilizar GDAL con Python vamos a instalar los _bindings_ que se encuentran en la misma web que hemos descargado los archivos binarios de GDAL. Un _binding_ es una adaptaci�n de una biblioteca para ser usada en un lenguaje de programaci�n distinto de aquel en el que ha sido escrita.

Como partimos de una instalaci�n de Python 3, descagaremos e instalamos el archivo _GDAL-1.11.3.win32-py3.3.msi_

Para terminar, vamos a acceder de nuevo la GUI de Python IDLE y escribiremos el siguiente c�digo importando GDAL en Python

```python
import gdal

```

Si no nos devuelve ning�n mensaje de error, hemos terminado nuestra instalaci�n.

Si quer�is empezar trastear con Python y GDAL os recomiendo seguir los ejemplos de [Python GDAL/OGR Cookbook.](https://pcjericks.github.io/py-gdalogr-cookbook/index.html). Tambi�n puede puede revisar el curso ["Geoprocessing with Python using Open Source GIS"](http://www.gis.usu.edu/%7Echrisg/python) de la Utah State University.
        