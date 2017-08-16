---
title:  "Extrayendo datos del DERA con Python"
categories: 
	- blog
tags:
	- Python
	- Andalucia
	- GDAL
	- IECA
---

Los **Datos Espaciales de Referencia de Andaluc�a para escalas intermedias -DERA-** "_es un repertorio de bases cartogr�ficas de diferente naturaleza geom�trica (puntos, l�neas, pol�gonos, im�genes raster) referidas al territorio andaluz_". M�s informaci�n en esta p�gina del [Instituto de Estad�stica y Cartograf�a de Andaluc�a](http://www.juntadeandalucia.es/institutodeestadisticaycartografia/DERA/).

Los datos pueden descargarse en un archivo comprimido zip por cada uno de los bloques. Dentro de cada zip la informaci�n se encuentra accesibles por capas en formato shapefile (.shp), en sistema de referencia geod�sico ETRS89 y proyectadas en UTM huso 30.

### Filtrado de datos con SIG

La extensi�n espacial de las capas es el �mbito geogr�fico de la comunidad aut�noma de Andaluc�a. Esto significa que por ejemplo en la capa _sv01_sanidad_centro_salud.shp_ se encuentran todos los centros de salud existentes en Andaluc�a y sus diferentes tipolog�as. Si queremos trabajar con una selecci�n de datos, por ejemplo por provincia, deberemos:

*   Descarga el zip correspondiente desde la web del [IECA](http://www.juntadeandalucia.es/institutodeestadisticaycartografia/DERA/)
*   Descomprimirlo el zip
*   Abrir un Sistema de Informaci�n Geogr�fica (ArcGIS, QGIS, gvSIG...)
*   Cargar la capa (ej. _sv01_sanidad_centro_salud.shp_)

Normalmente las capa del DERA incluyen informaci�n del municipio y provincia, por lo que podemos hacer una consulta por el atributo que deseemos, seleccionar los datos y crear una nueva capa a partir de la selecci�n.

Una vez que tenemos los datos en nuestro SIG, se nos pueden plantear algunas preguntas:

*   **�Qu� ocurre si la capa no dispone de un atributo como municipio o provincia que permita filtrarla?** Esto puede suceder para capas de tipo lineal o poligonal cuya extensi�n supere un l�mite administrativo.
*   **�C�mo extraer informaci�n de �mbitos geogr�ficos definidos por nosotros?** Este puede ser el caso de un barrio, o la delimitaci�n de una mancomunidad. En este caso debemos contar con la capa de delimitaci�n y a continuaci�n seleccionar los elementos geom�tricos (ej. centros de salud) mediante una consulta espacial (superposici�n, dentro de, toca...).
*   **�Y si quiero obtener todos los datos de un bloque tem�tico, como por ejemplo "Servicios", para un barrio?** En este caso, tendremos que repetir la operaci�n anterior para cada una de las capas.

### Trabajando con Python y GDAL

Algunos de los problemas que he planteado antes pueden solucionarse con las herramientas de creaci�n de modelos de procesado integradas en los SIG. En el siguiente enlace a [MappingGIS](http://mappinggis.com/2014/08/crear-un-modelo-de-procesado-en-qgis-el-model-builder-de-qgis/) hay una sencilla gu�a de c�mo hacerlo en QGIS.

Como sigo con el aprendizaje de Python que comenc� con [dxf2gmlcatastro](2016/dxf2gmlcatastro-script-python-para-convertir-de-dxf-a-gml-parcela-catastral) he decidido crear un peque�o c�digo que haga lo siguiente:

*   Descomprimir un archivo zip de capas Shape, en este caso del DERA.
*   Localizar una archivo poligonal que va a ser usado para "recortar" las capas Shape del zip
*   Crear una carpeta donde almacenar las nuevas capas recortadas.
*   Generar nuevas capas recortadas en una carpeta concreta y con un sufijo (_clip).
*   Borrar la carpeta donde se ha descomprimido el zip.

Los requisitos para ejecutar el c�digo son

*   Tener instalado Python.
*   Tener instalada la librer�a GDAL/OGR.

Un ejemplo

<pre>$ python clipShapesZip.py 'G15_Patrimonio.zip' 'clip_area.shp' 'clipFolder'</pre>

Como nota importante comentar que si el geoproceso se aplica sobre una lineal o poligonal, la funci�n har� su funci�n y "recortar�" las geometr�as a partir del la capa indicada.

<script type="text/javascript" src="https://gist-it.appspot.com/github/sigdeletras/clipShapesZip/blob/master/clipShapesZip.py"></script>
        