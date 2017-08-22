---
title:  "Editores de informaci�n geogr�fica en Internet"
excerpt_separator: "<!--more-->"
related: true
categories: 
- Blog
tags:
- Webmapping
---
     
Cada vez son m�s los profesionales que interesados en la publicaci�n de sus datos geogr�ficos en Internet se acercan por primera vez al mundo de las Tecnolog�as de la Informaci�n Geogr�fica. Durante las charlas, los talleres o por correo me suelen pedir que les recomiende alguna herramienta para empezar a generar sus datos, normalmente pensando que una vez creados, estos puedan ser accesibles en Internet.
<!--more-->
Pienso que una buena manera de comenzar es utilizar algunas de las herramientas y/o servicios para la creaci�n de datos geogr�ficos que nos ofrece la Red. Si las necesidades de edici�n, an�lisis y publicaci�n de datos se hacen cada vez m�s exigentes siempre tendremos la oportunidad de dar el salto los Sistemas de Informaci�n Geogr�fica de escritorio como [QGIS](http://www.qgis.org/es/site/ "QGIS") o [gvSIG](http://www.gvsig.com/es/productos/gvsig-desktop/descargas "gvSIG"), o empezar a hacer pinitos con las librer�as de mapas en web como [Leaflet](http://leafletjs.com/ "http://leafletjs.com/") u [OpenLayers](http://openlayers.org/ "http://openlayers.org/").

# Geojson.io

[Geojson.io](http://geojson.io/#map=2/20.0/0.0) se describe a s� mismo como una herramienta r�pida y simple para crear, visualizar y compartir mapas. Suelo utilizarla con bastante asiduidad para generar datos espaciales de forma r�pida, a�adirles atributos, guardarlos en formato GeoJSON para incluirlos en visores de mapas web. Aunque parece sencilla en apariencia, tiene gran cantidad de herramientas y soporta formatos geogr�ficos como GeoJSON, KML, GPX, CSV o TopoJSON. Podemos trabajar de forma an�nima o usar nuestra cuenta GitHub y trabajar con la informaci�n de nuestros repositorios.

<div style="text-align: center;"><iframe src="http://bl.ocks.org/d/269a7dd4cf989631ffd9" frameborder="0" width="100%" height="500"></iframe>

_Visor geojson.io_

</div>

# _My Maps_ de� Google

Si tenemos una cuenta Gmail podemos acceder a [My Maps](https://www.google.com/maps/d/?hl=es "My Map Google")� o lo que era hace poco GoogleMap Engine Lite, para generar mapas sobre el callejero, la imagen sat�lite o cualquier estilo basado en Google Map. _My Map_ est� totalmente vinculado con Google Drive, por lo que podemos trabajar con archivos CSV, XLSX o KML almacenados en nuestra cuenta y dise�ar nuestro mapa a partir de los mismos. Si nos sentimos c�modos trabajando con Google Drive podemos probar [Fusion Tables](https://support.google.com/fusiontables/answer/2571232).

<div style="text-align: center;">![www.gislounge.com](http://www.gislounge.com/wp-content/uploads/2013/03/google-engine-lite.png)

_Ejemplo de mapa creado con GoogleMap Engine en www.gislounge.com_

</div>

# uMap

[uMap](http://umap.openstreetmap.fr/es/) es una herramienta de c�digo abierto que puede servir de alternativa a _My Map_ de Google. La gran diferencia es que nuestros datos se localizar�n sobre mapas basados OpenStreetMap, pero por lo dem�s las funcionalidades son numerosas. uMap nos permite, al igual que geojson.io trabajar con gran variedad de formatos geogr�ficos, a los que se suma los datos de [OpenStreetMap](http://www.openstreetmap.org/ "OpenStreetMap") , vincular nuestros mapas a nuestra cuentas cuentas de GitHub, OpenStreetMap, Twitter o Bitbucket o incluir los mapas en nuestra web. Un aspecto que me interesa es gran variedad de opciones relativas a simbolog�a y usos de CSS, la opci�n de trabajar con m�ltiples capas, las presentaciones de mapas estilo diapositivas...

<div style="text-align: center;"><iframe src="http://umap.openstreetmap.fr/es/map/centros-vecinales-almeria_39435?scaleControl=false&amp;miniMap=false&amp;scrollWheelZoom=false&amp;zoomControl=true&amp;allowEdit=false&amp;moreControl=true&amp;datalayersControl=true&amp;onLoadPanel=undefined&amp;captionBar=false" frameborder="0" width="100%" height="500px"></iframe>

_Mapa con la localizaci�n de los centros vecinales de Almer�a. [Ver pantalla completa](http://umap.openstreetmap.fr/es/map/centros-vecinales-almeria_39435)_

</div>

# Carto

[Carto](https://carto.com/ "Carto") es un servicio de mapas en la nube de f�cil manejo para el usuario principiante. De forma sencilla podemos ir generando nuestros propios datos o partir de datos ya creados que podremos importar desde nuestro equipo, Google Drive o Dropbox. La informaci�n podr�n ser manejada en formato tabla o editada desde el mapa. Mediante su asistente se puede generar con rapidez mapas tem�ticos, de intensidad o �calor�, agrupados o din�micos utilizando el estilo Torque. La informaci�n asociada a cada geometr�a puede ser consultada mediante ventanas emergentes que se dise�an usando alguna de las plantillas disponibles.

Pero si ya tenemos algunos conocimientos, Carto nos permite igualmente hacer consultas complejas gracias a que los datos se almacenan en una base de datos geogr�fica PostGIS, crear nuestra propia simbolog�a usando CartoCSS, acceder, consultar y actualizar la informaci�n mediante su API o dise�ar nuestros propios mapa usando la librer�a Javascript Carto.js.

<div style="text-align: center;"><iframe src="https://sigdeletras.carto.com/viz/336c862e-f309-11e4-a1c8-0e8dde98a187/embed_map" frameborder="0" width="100%" height="500"></iframe>

_Ejemplo con Carto. Mapa del Festival de los Patios de C�rdoba 2015_

</div>

Me interesa vuestra opini�n �hab�is utilizado alguno de estos servicios?, �qu� os han parecido?, �recomendar�ais otras herramienta?        