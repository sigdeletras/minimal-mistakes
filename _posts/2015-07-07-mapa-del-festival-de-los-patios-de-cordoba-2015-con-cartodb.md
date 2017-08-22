---
title:  "Mapa del Festival de los Patios de C�rdoba 2015 con CartoDB"
header:
      teaser: "/images/header/2015-10-09-gdal2.jpg"
related: true
categories: 
      - Blog
tags:
      - Webmapping
      - Carto
      - C�rdoba
      - Patrimonio

---
      
Mayo es uno de los meses m�s importantes de C�rdoba. Durante estos d�as tienen lugar algunos de los acontecimientos festivos m�s relevantes de la ciudad como las [Cruces de Mayo](http://www.spain.info/es/que-quieres/agenda/fiestas/cordoba/cruces_de_mayo.html "Cruces de Mayo") , la [Feria de Nuestra se�ora de la Salud](http://www.spain.info/es/que-quieres/agenda/fiestas/cordoba/feria_de_cordoba.html "Feria de C�rdoba") o el Festival de los Patios. En la Fiesta de los Patios, declarada [Patrimonio Cultural Inmaterial por la UNESCO en 2012](http://www.unesco.org/culture/ich/index.php?lg=es&pg=00011&RL=00846 "UNESCO"), cordobeses y turistas pueden disfrutar de estos espacio arquitect�nicos y sociales visitando los patios inscritos a concurso y cuidadosamente decorados con plantas (macetas) y otros objetos t�picos para tal evento.

Este a�o, toda la informaci�n del Festival con las fichas de cada uno los patios y muchos otros apartados ha podido ser consultada en la p�gina web [Los Patios de C�rdoba](http://patios.cordoba.es/). Revisando los contenidos, y sobre todo viendo los mapas, se me ocurri� usar la informaci�n para hacer mi propio [**mapa del Festival de los Patios de C�rdoba 2015**](https://sigdeletras.cartodb.com/viz/336c862e-f309-11e4-a1c8-0e8dde98a187/public_map%20 "mapa en CartoDB") usando el servicio de mapas en nube [CartoDB](https://cartodb.com "CartoDB"). Aunque los contenidos de la web se encuentran bajo licencia-tipo Creative Commons Reconocimiento 3.0, mi intenci�n se ha centrado en la localizaci�n de los patios y la incorporaci�n de los datos asociados mediante de enlaces a las fichas de la propia web del Festival.

### Geolocalizaci�n

El primer paso fue **generar una tabla con el listado de los patios en formato CSV** en los que inclu� el nombre, la zona, la ruta relativa de acceso a la ficha de la p�gina web y la ruta una imagen. Una vez generado este listado, el siguiente paso fue la geocodificaci�n de las direcciones de cada uno de los patios utilizando la herramienta �Geocode CSV� de [MMQGIS](https://plugins.qgis.org/plugins/mmqgis/ "MMQGIS") de QGIS. CartoDB posee su propia herramienta de geocodifiaci�n pero tiene un l�mite de operaciones que en mi caso ya hab�a sobrepasado hace tiempo.

![Archivo CSV](/images/blog/201507_patios/csv.png)

_Tabla de datos_

El funcionamiento de esta extensi�n sencillo: cargamos un archivo CSV que contenga un campo con la direcci�n, en nuestro caso el nombre del patio, la ciudad y el pa�s. La aplicaci�n nos permite geolocalizar las direcciones utilizando los servicios de Google o de OpenStreetMap. Tras revisar la precisi�n geogr�fica y ajustar la localizaci�n de algunos puntos, la capa puntual con los 48 puntos fue convertida a formato GeoJSON y subida a CartoDB.

![Web Service Geocode](/images/blog/201507_patios/Web Service Geocode_356.png)

_Configuraci�n de la herramienta de Geocoding de MMQGIS_

Los datos geogr�ficos pueden **descargarse en distintos formatos** (CSV, SHP, KML, SVG, GEOJSON) desde e enlace al conjunto de datos o _dataset_ en cartoDB desde este [enlace](https://sigdeletras.cartodb.com/tables/festival_patios_cordoba_2015/public "dataset patios cartodb"). Tambi�n es posible **hacer una llamada a la API SQL** de CartoDB desde ese mismo enlace.

### Capas auxiliares

Una de las cosas que ech� en falta en los mapas de la p�gina web oficial fue la incorporaci�n de datos tur�sticos. Esta informaci�n puede servir a los visitantes a completar el recorrido por la ciudad visitando cada uno de los patios. Por esta raz�n decid� incorporar a CartoDB una **capa puntual denominada �turismo_cordoba�** con localizaciones tur�sticas tipo monumentos, museos u oficinas de turismo. Estas datos forman parte de una capa propia procedente de varias fuentes oficiales como la Junta de Andaluc�a o el propio Ayuntamiento.

Gracias los comentarios de [Alejandro Alameda](https://twitter.com/AlxAlameda "Twitter"), vi interesante aportar la localizaci�n de las "**fuentes de agua"** Los datos de la capa proceden de OpenStreetMap y para obtenerlos utilic� la herramienta [OverPass Turbo](http://overpass-turbo.eu/ "OverPass") . Aunque faltan muchas fuentes, hay que destacar OpenStreetMap es la �nica base de datos geogr�fica donde podemos encontrar este tipo de informaci�n. Si os interesa completar los datos de vuestra ciudad echarle un vistazo a la iniciativa [�A�ade una fuente� de OpenStreetMap Espa�a](http://www.openstreetmap.es/2014/07/03/anade-una-fuente/ "OSM Espa�a").

### Simbolog�a

Una vez cargadas las tres capas y completados sus metadatos, el trabajo siguiente se centr� en el dise�o del mapa (view). CartoDB dispone de herramientas asistidas o _wizards_ que ayudan a crear una mapa interactivo est�ticamente atractivo.

![Tipos de simbolog�a usando CartoCSS](/images/blog/201507_patios/simbologia_patios.png)

_Ejemplo de simbolog�a en CartoDB_

Para la capa de patios utilic� la **simbolog�a _�category�_** que permite representar elementos geogr�ficos seg�n una columna de la tabla. Me pareci� correcto �pintar� los patios seg�n su zona lo que dio una capa puntual con siete colores, un por cada zona. A esta capa se le a�adi� una etiqueta (_label_) del mismo color que la zona con el nombre del patio. Para trabajos m�s avanzados puede ser interesante usar la pesta�a CSS que permite editar el c�digo [CartoCSS](https://www.mapbox.com/tilemill/docs/manual/carto/) de la simbolog�a. Os dejo un ejemplo del c�digo generado para la capa patios.

La capa "Turismo" fue representada tambi�n seg�n el tipo de elemento diferenciando entre Patrimonio, Museo y Oficina de Turismo. En este caso la representaci�n se realiz� usando algunos de los iconos de las galer�as incorporadas con CartoDB. Podemos utilizar subir nuestros propios iconos o hacer referencia a otros s�mbolos alojados en Internet. Para las fuentes busqu� y edit� con GIMP un s�mbolo representativo que posteriormente sub�a a CartoDB.

### Datos asociados

Al pinchar en cada uno de los patios se obtiene una� **ventana emergentes con informaci�n** sobre el nombre del patio y la zona en la que se encuentra. CartoDB permite elegir entre varias plantillas de _pop-ups_ entre las que se encuentra una que a�ade una imagen en la cabecera. Para obtener la ruta competa de la imagen cree un **campo virtual mediante SQL** denominado _imghead_ que concatenaba la direcci�n de la web oficial con el campo img de la capa m�s su extensi�n.

	SELECT *,'http://patios.cordoba.es/patios/'|| img ||'.jpg' as imghead FROM festival_patios_cordoba_2015

_C�digo SQL� para genera el campo "imghead"_

Una vez generado el nuevo campo y pinchando en la pesta�a �infoview� , debemos arrastrarlo al principio del listado de campos disponibles. En segundo lugar de esta lista ponemos el campo que queramos aparezca sobre la imagen, en este caso el nombre del patio.

![](/images/blog/201507_patios/popup.png)

_Ventana de datos con plantilla de imagen en cabecera_

Para terminar de dise�ar la ventana de datos, y accediendo en este caso a la **vista del c�digo HTML** que conforma la ventana de datos, decid� a�adir tres enlaces, uno por los idiomas disponibles, a la ficha de datos alojada en la web oficial. Aunque esto pueda parecer m�s complejo, s�lo es necesario tener algunos conocimientos de HTML para sacarle m�s partido a esta funci�n de CartoDB.

<pre><a href='http://patios.cordoba.es/patios/detallar/pag/{{link}}' target='_blank' title='Web Patios de C�rdoba'>Espa�ol</a></pre>

_C�digo HTML de ejemplo para generar enlaces a la ficha del patio oficial_

### �Herramientas del visor

El visor incorpora varias herramientas que pueden ser activadas o desactivadas desde el bot�n �Options�. Cre� interesante a�adir el t�tulo y la descripci�n del mapa, as� como las herramientas de callejero, control de capas y herramientas de zum. Para terminar, y utilizando algunas de las herramientas incorporadas en la �ltima actualizaci�n de la a�ad� un par de marcos a la vista con la imagen corporativa de la UNESCO y un texto con la procedencia de los datos.

<iframe src="https://sigdeletras.cartodb.com/viz/336c862e-f309-11e4-a1c8-0e8dde98a187/embed_map" frameborder="0" width="100%" height="520"></iframe>       