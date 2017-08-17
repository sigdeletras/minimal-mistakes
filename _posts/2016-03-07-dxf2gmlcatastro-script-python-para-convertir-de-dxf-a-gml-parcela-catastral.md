---
title:  "dxf2gmlcatastro. Script Python para convertir de DXF a GML parcela catastral"
header:
      teaser: "/images/header/2016-05-03-dxf2gmlcatastro.jpg"
categories: 
- blog
tags:
- Catastro
- Python
- Inspire
---

Estas �ltimas semanas conocidos y amigos que se dedican a la arquitectura, la tasaci�n inmobiliaria me han hecho consultas sobre la generaci�n del archivo GML que debe a�adirse a la descripci�n graf�ca que describe inform�ticamente las parcelas catastrales.

Laboralmente no he tenido que realizar trabajos vinculados con Catastro, por para enterarme un poco de que iba el tema tuve que leer algunos documentos t�cnicos colgados en la web de la Direcci�n General de Catastro, blog especializados y alg�n que otro foro.

Seg�n he podido, leer cuando la certificaci�n catastral descriptiva y gr�fica no coincide con la realidad es necesario elaborar una representaci�n gr�fica alternativa a la que se debe a�adir un XML con contenido geogr�fico que no es otro que el famoso GML.

Este mismo archivo es tambi�n accesible, como adjunto, en las certificaciones catastrales descriptivas y gr�ficas, desde la consulta interactiva de un bien inmueble y desde servicios web WFS.

Mi primera respuesta a fue que se usara un SIG de escritorio para pasar el DFX al GML pero parece que no es tan sencilla el esquema no est� disponible a�n en la mayor�a de los SIG (parece que en la �ltima versi�n de gvSIG 2.3 est� disponible). El formato de parcela catastral debe cumplir el est�ndar INSPIRE cadastral parcel definido en INSPIRE Data Specification on Cadastral Parcels - Guidelines version 3.0.1\. L

## �C�mo generar el GML?

La Direcci�n General del Catastro ha colgado de su web una serie de gu�as t�cnicas en las que se explica entre otros c�mo generar un GML de Parcela Catastral. En el mismo apartado hay un par de ejemplos con explicaciones comentadas de archivos GML validados para parcela catastral y para edificio.

En la gu�a se definen los siguientes pasos:

*   Paso 1: Descarga de un fichero DXF de la sede electr�nica del Catastro conteniendo la cartograf�a de la zona en la que se desea intervenir.
*   Paso 2: Edici�n del fichero con AUTOCAD (...u otro programa CAD o incluso SIG) y generaci�n de un nuevo fichero DXF.
*   Paso 3: Modificaci�n manual del fichero DXF generado y obtenci�n de coordenadas.
*   Paso 4: Generaci�n del fichero GML para adaptarlo al formato de parcela catastral.
*   Paso 5: Validaci�n del fichero GML en la Sede Electr�nica del Catastro.

Todo este proceso es bastante "artesano" y lo primero que se me ocurri� es que algunos de estos pasos (3 y 4) se podr�a automatizar con un poco de programaci�n con el fin de ganar tiempo y evitar errores que se puedan generar por la edici�n manual. Tras algunas lectura y documentaci�n pens� en generar un peque�o c�digo en Python usando la librer�a GDAL y compartirlo en GitHub para que pueda ser utilizado y espero que mejorado.

## �C�mo funciona dxf2gmlcatastro.py?

### Descargar dxf2gmlcatastro

En primer lugar debemos descargar/descomprimir o hacer un _git clone_ de los archivos python disponibles en el repositorio [dxf2gmlcatastro en GitHub](https://github.com/sigdeletras/dxf2gmlcatastro).

### Instalar Python y la librar�a GDAL.

En Ubuntu **Python** viene instalado por defecto. De todas formas si queremos comprobarlo y ver la versi�n instalada s�lo hay que ejecutar desde terminal el siguiente comando

    $ python --version
    Python 2.7.6

La librer�a [GDAL](https://pypi.python.org/pypi/GDAL/) es la que se encargar� de todas las operaciones de acceso y lectura del archivo DXF. Para usarla con Python he instalado _python-gdal_.

    $ sudo apt-get install python-gdal

Todo el trabajo se ha realizado en Ubuntu. Para [Windows](https://www.python.org/downloads/), tras instalar Python, podr�a utilizarse el administrador de paquetes Python [Pip](http://recursospython.com/guias-y-manuales/instalacion-y-utilizacion-de-pip-en-windows-linux-y-os-x/).

### Ejecutar dxf2gmlcatastro.py (v.2*)

* Agradecer al inestimable ayuda y PR de Marcos Ortega de [Indavelopers](http://www.indavelopers.com/ "indavelopers")

Desde la consola ejecutamos el comando _dxf2gmlcatastro.py_ indicando a continuaci�n la ubicaci�n del archivo DXF, el nombre del nuevo archivo GML y el c�digo EPSG del Sistema de Referencia de Coordendas del archivo DXF.

    $ pyhon dxf2gmlcatastro.py archivocad.dxf archivogmlcatasro.gml 25830

Toda la informaci�n junto a archivos de ejemplo puede consultarse en el [repositorio GitHub](https://github.com/sigdeletras/dxf2gmlcatastro "Github").

## 2do

*   <span style="text-decoration: line-through;">Permitir elegir el SRC del GML.</span> (v.2)
*   Investigar qu� es el "Identificativo local de la parcela" y se si deber�a solicitar al ejecutar el script.
*   <span style="text-decoration: line-through;">Poder elegir el archivo DXF a transformar.</span> (v.2)
*   <span style="text-decoration: line-through;">Poder elegir el archivo GML a crear.</span>(v.2)
*   Generar un GML de varias parcelas catastrales.
*   Crear un script para edificio.
*   Probarlo en otros Sistemas Operativos. (MacOS)
*   Probarlo en QGIS

## Referencias

*   [�C�MO GENERAR UN GML DE PARCELA CATASTRAL?. Direccion General de Catastro](http://www.catastro.minhap.es/documentos/portal%20generacion%20GML.pdf)
*   [Documentaci�n t�cnica. Direccion General de Catastro](http://www.catastro.minhap.es/esp/CoordinacionCatastroRegistro.asp#doctec)
*   [GML parcela catastral: como generar un fichero de coordenadas GML v�lido para Catastro. Blog GESPASUR de Pedro E. Fuster Villa](http://gespasur.blogspot.com.es/2016/01/como-generar-un-fichero-de-coordenadas.html)
*   [Representaci�n gr�fica alternativa y formato GML en la georreferenciaci�n de la propiedad inmobiliaria. Albireo Topografia](http://www.albireotopografia.es/representacion-grafica-alternativa-y-formato-gml-en-la-georreferenciacion-de-la-propiedad-inmobiliaria/)
        