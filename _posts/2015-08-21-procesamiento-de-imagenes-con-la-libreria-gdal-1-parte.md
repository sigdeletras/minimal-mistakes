---
title:  "Procesamiento de im�genes con la librer�a GDAL (1� parte)"
header:
      teaser: "/images/header/2015-07-07-gdal.jpg"
related: true
categories: 
      - Blog
tags:
      - GDAL
---
        
**GDAL** ([http://www.gdal.org/](http://www.sigdeletras.com/)) es una biblioteca de software para la lectura y escritura de formatos de datos geoespaciales publicada bajo la MIT License por la Fundaci�n [OSGeo](%20http:/www.osgeo.org/ "OSGeo"). Con esta librer�a se pueden realizar multitud de operaciones de transformaci�n y procesamiento sobre gran variedad de datos [raster](http://www.gdal.org/formats_list.html "Raster") y [vectoriales](http://www.gdal.org/ogr_formats.html "Formatos vectoriales").

En la siguiente serie de entradas vamos a tratar algunos los comandos destinados a obtener informaci�n de un raster (gdalinfo), convertir archivos a otros formatos (gdal_translade) y cambiar el sistema de referencia de coordenadas� de im�genes referencias� (gdalwarp).  

Para saber m�s sobre esta librer�a se pueden consultar los siguientes art�culos.

*   [Gu�a de inicio r�pido GDAL/OGR](http://live.osgeo.org/es/quickstart/gdal_quickstart.html "enlace")
*   [Raster Processing Tutorial](https://trac.osgeo.org/gdal/wiki/UserDocs/RasterProcTutorial%20 "Raster Processing Tutorial")
*   [Workshop GDAL FOSS4GE 2015](http://download.osgeo.org/gdal/workshop "WorkshopGDAl FOSS4GE")

### �Terminal o SIG?

La librer�a GDAL es utilizada por gran n�mero de paquetes geom�ticos (https://trac.osgeo.org/gdal/wiki/SoftwareUsingGdal) como por ejemplo QGIS, gvSIG o ESRI ArcGIS 9.2+. Desde los men�s de cualquiera de estos clientes SIG podemos acceder a las funciones de GDAL utilizando los formularios dise�ados para ello. **Si podemos utilizar sin complicaciones las funciones desde un Sistema de Informaci�n Geogr�fica �qu� sentido tiene utilizar los comandos?**. Para mi, la primera raz�n es el simple hecho de conocer, aprender y saber a manejar distintas herramientas vinculadas con la informaci�n geogr�fica. El segundo motivo, y no por ello el menos interesante, funcional y divertido es el intentar dar soluciones m�s efectivas mediante programaci�n a operaciones que se repitan o en las que est�n incluidas multitud de ficheros.

### Instalaci�n de GDAL

Comenzamos con la instalaci�n de la librer�a. En mi, en un equipo con **Ubuntu** he a�adido repositorio de fuentes, actualizado e instalado a librer�a usando los siguientes comandos.

	$ sudo add-apt-repository ppa:ubuntugis/ubuntugis-unstable  
	$ sudo apt-get update  
	$ sudo apt-get install gdal-bin

Una vez instalado podremos hacer una verificaci�n mediante este comando.

	$ gdalinfo --version

Para equipos con **Windows** lo m�s recomendable es utilizar el [instalador OSGeo4W](https://trac.osgeo.org/osgeo4w/ "Osgeo4w"), aunque tambi�n est� la alternativa de [FWTools](http://fwtools.maptools.org/ "fwtools").

Como no me quiero meter en follones con la instalaci�n en **Mac** por no haberla probado, aqu� un dejo un [enlace](https://www.mapbox.com/tilemill/docs/guides/gdal "Instlaci�n GDAL en Mac") que puede ayudar.

### Usando _gdalinfo_� para obtener informaci�n sobre un archivo

Podemos utilizar el comando gdalinfo para obtener gran cantidad de informaci�n de un determinado fichero de imagen. Si queremos podemos tambi�n comprobar los tipos de formatos soportados por GDAL con el comando _gdalinfo �formats_.

Si nos encontramos en el directorio donde se encuentra el archivo, desde Linux s�lo debemos abrir nuestro terminal, escribir el comando seguido del nombre y extensi�n del fichero. En el caso de estar en otro directorio debemos a�adir la ruta y el nombre m�s extensi�n del raster.

	$ gdalinfo mapa.tif

o

	$ gdalinfo utm.tif /home/user/mapa.tif

Entre otros datos obtendremos: tipo del fichero, tama�o, SRC, tama�o del p�xel, metadatos, coordenadas de las esquinas y centro o la informaci�n de las bandas.

Si volvemos a escribir el comando, pero esta vez seguido del s�mbolo mayor que (>) con un nombre y la extensi�n txt (ej. utm_metados.txt), se genera un fichero con los datos. Esta opci�n es bastante interesante si queremos incorporar un fichero adjunto de metadatos a nuestra imagen.

	$ gdalinfo mapa.tif > mapa_metados.txt

### Cambios de formato con _gdal_translate_

La utilidad b�sica de [_gdal_translate_](http://www.gdal.org/gdal_translate.html "gdal_translate") es la de hacer una copia de un fichero existente en otro formato de los reconocidos por la librer�a.

Por ejemplo, al georreferenciar una imagen que s�lo requiera escalado y traslaci�n, lo normal es que se generar un archivo� de tipo _world file_ con los datos del p�xel y la coordenada de la esquina. Estos ficheros se sombran de igual manera que la imagen y tienen una extensi�n acabada en la letra w. (pnw, .jpgw/.jpegw o .wld). Si utilizamos este sistema de multiarchivo la informaci�n geogr�fica no es intr�nseca al archivo, por lo que no podremos saber el Sistema de Referencia de coordenadas en que se encuentra la imagen. Para solventar este escollo es preferible trabajar con archivos en formato GeoTiff.

Para convertir el archivo a formato GeoTiff usamos gdal_translate y a�adimos el fichero de origen y el nombre del nuevo fichero con su extensi�n.

	$ gdal_translate -of GTiff mapa.jpg mapa.tif

Una vez realiza la conversi�n es interesante comprobar la diferencia de datos vinculados al fichero usando de nuevo el comando _gdalinfo_.

Lo normal es que utilicemos la librer�a GDAL con im�genes georreferenciados, pero puede ser tambi�n �til para pasar de formato otros archivos sin coordenadas previas. Por ejemplo, podemos convertir un plano en PDF a un archivo TIF, establecer la resoluci�n de la imagen de salida o incluso obtener una zona concreta del PDF usando� _-projwin_.

	$ gdal_translate in.pdf out300.tif� --config GDAL_PDF_DPI 300 -projwin 792 144 9450 5600

Despu�s utilizando un SIG o la misma librer�a podr�amos asignarles las coordenadas para su georreferenciaci�n.

### Opciones de compresi�n

Podemos ir m�s all� usando los distintas opciones del comando. y por ejemplo definir las opciones de configuraci�n para aplicar compresi�n a fichero y reducir su tama�o. Usando el comando y la opci�n �-co� se podr� asignar al nuevo fichero un algoritmo de compresi�n que puede reducir el peso del nuevo.

	$ gdal_translate -of GTiff -co COMPRESS=DEFLATE -co PREDICTOR=2 -co TILED=YES� mapa.jpg mapa.tif

No voy a entrar en las diferentes algoritmos de compresi�n de im�genes que podemos utilizar pero s� os dejo unos enlaces que son de gran inter�s. S�lo indicar que existen opciones que nos permiten reducir casi a un 50% el peso de un fichero sin perder calidad en la imagen.

*   [GDAL: efficiency of various compression algorithms. Rudi Thiede & filed under QGIS.](http://linfiniti.com/2011/05/gdal-efficiency-of-various-compression-algorithms/)
*   [GeoTiff Compression for Dummies. Thursday, February 19, 2015\. Paul Ramsey](http://blog.cleverelephant.ca/2015/02/geotiff-compression-for-dummies.html)
*   [GeoTiff compression benchmarking en Fernerkundung.](http://fernerkundung.github.io/GeoTiff-compression-benchmarking/)
*   [GeoTiff compression comparasion por� Kersten Clauss� en Digital Geography](http://www.digital-geography.com/geotiff-compression-comparison)