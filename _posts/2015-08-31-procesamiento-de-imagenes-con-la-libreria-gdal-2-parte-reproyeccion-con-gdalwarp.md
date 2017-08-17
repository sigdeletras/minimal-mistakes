---
title:  "Procesamiento de im�genes con la librer�a GDAL (2� parte). Reproyecci�n con gdalwarp"
header:
      teaser: "/images/header/2015-10-09-gdal2.jpg"
categories: 
- Blog
tags:
- GDAL
---

Este art�culo continua la [entrada anterior](blog/procesamiento-de-imagenes-con-la-libreria-gdal-1-parte "GDAL 1") en la se expusieron algunos de los usos de los comandos _gdalinfo_ y _gdaltranslate_ de la librer�a GDAL. En el siguiente texto nos vamos a centrar en el comando _gdalwarp_. Este comando se usa para hacer reproyecciones del Sistema de Referencia de Coordenadas de una imagen georeferenciada.

### Reproyecci�n de una imagen georeferenada con gdalwarp

El uso b�sico es sencillo: partimos de la base de que la imagen ya posee un SRC definido, tras el comando indicaremos el SRC de salida usando el [c�digo EPSG](https://es.wikipedia.org/wiki/European_Petroleum_Survey_Group "EPSG") (ej. -t_srs "EPSG:4326"), el fichero a reproyectar y el nombre la imagen proyectada.

<pre>$ gdalwarp� -t_srs "EPSG:4326"� -of GTiff img.tif img4326.tif</pre>

Las opciones de _gdalwarp_ son muchos m�s variadas establecer un valor sin datos (_- dstnodata_) o usar una archivo vectorial para recortar la imagen de salida (_-cutline_). Todas las opciones pueden consultarse en la siguiente direcci�n [http://www.gdal.org/gdalwarp.html](http://www.gdal.org/gdalwarp.html "gdalwarp")

### De ED50 a ETRS89

En Espa�a, a partir del 1 de enero de 2015� y seg�n� el Real Decreto 1071/2007 , de 27 de julio, por el que se regula el sistema geod�sico de referencia oficial en Espa�a, _"...toda la cartograf�a y bases de datos de informaci�n geogr�fica y cartogr�fica producida o actualizada por las Administraciones P�blicas deber� compilarse y publicarse conforme a lo que se dispone en este real decreto_� o lo que es lo mismos debe estar encontrarse en el ETRS89\. M�s informaci�n en esta [p�gina del IGN](http://www.ign.es/ign/layoutIn/faqgd.do).

Para facilitar la transformaci�n del datum ED50 a ETRS89, el Instituto Geogr�fico Nacional ha generado dos rejillas (Pen�nsula y Baleares) en formato NTV2\. Estas rejillas pueden ser descargadas desde la [web del IGN](http://www.ign.es/ign/layoutIn/herramientas.do "Rejilas NTV2").� Las rejillas pueden a�adidas� usadas en la mayor�a de los SIG pero tambi�n podemos utilizarla directamente usando GDAL con el comando gdalwarp. En la web de [Mappingis](http://mappinggis.com/2015/03/como-transformar-de-ed50-a-etrs89-en-qgis-con-ntv2/) podr�is encontrar un art�culo de su uso en QGIS.

Si queremos trasformar con _gdalwarp_ una imagen en ED50 UTM30N (EPGS:23030) a ETRS89 (EPGS:25830), lo primero ser� descargar la correspondiente rejilla a nuestro ordenador. Tras el comando debemos a�adir los SRC de entrada (_-s_srs_) y salida (_-t_srs_), pero en esta ocasi�n a�adiendo los par�metros de la librer�a PROJ.4 e indicando la ruta de la rejilla del IGN tras la opci�n _nadgrids_.

Suponiendo que hemos almacenado la rejilla de la pen�nsula en nuestro disco duro C: en la carpeta "rejillas", el comando quedar�a as�:

<pre>$ gdalwarp -s_srs "+init=epsg:23030 +nadgrids=C/:rejilla/PENR2009.gsb +wktext" -t_srs "+init=epsg:25830 +nadgrids=null +wktext" -of GTiff img23030.tif img25830.tif</pre>

### Un poco de programaci�n: procesando de m�ltiples im�genes con _gdalwarp_

Como he comentado al principio, todo este textazo tiene en primer lugar una funci�n did�ctica para mi. El segundo aspecto por el que merece utilizar los comando de estas librer�as es el hecho de poder crear nuestros propios fragmentos de c�digo o _scripts_ que nos ayuden a mejorar nuestra vida..al menos desde el punto de vista inform�tico. Creo que en esta b�squeda de la felicidad, podr�a ser interesante hacer un un peque�o _script_ que por ejemplo convirtiera a formato GeoTiff y mejorara el tama�o de, �porqu� no?, 200 ficheros.

Creamos un _script_ utilizando el _shell_ de Linux con la extensi�n _sh_ (ej. ed50etrs89.sh). El _script_ est� pensado para ser utilizado desde el terminal de Linux. Si alguno se lo trabaja para Windows o Mac, y quiere que lo ponga en la entrada avisad por correo.

El c�digo hace lo siguiente:

*   Localiza las im�genes con la extensi�n JPG que se encuentran en el mismo directorio del archivo� ed50etrs89.sh
*   Reproyecta� y comprime las im�genes a ETRS89 UTM 30N usando la rejilla del IGN localizada en en mismo directorio del _script_.
*   Salva las im�genes con el sufijo �_25830�� y en formato GeoTiff
*   Usa gdalinfo para generar una archivo de texto con los metadatos de las im�genes reproyectadas.

Si es necesario le asignamos, los correspondientes permisos de ejecuci�n con chmod

<pre>$ chmod +x ed50etrs89.sh</pre>

Y a continuaci�n, lo ejecutamos

<pre>$ ./ed50etrs89.sh</pre>
        