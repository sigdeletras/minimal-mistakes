---
title:  "Edici�n de Informaci�n Geogr�fica en Web con GeoWE"
categories: 
- blog
tags:
- Geowe
- Webmapping
---

Como se indica en su [p�gina web](http://www.geowe.org/), **GeoWE** _es un proyecto software orientado a la edici�n de Informaci�n Geogr�fica en Web, cuya culminaci�n toma la forma de una aplicaci�n cliente disponible para edici�n en diversos dispositivos. Se trata de una iniciativa de c�digo abierto basada en el framework Google Web Toolkit (GWT), cuyo desarrollo y mantenimiento se lleva a cabo por parte de un equipo experimentado en SIG, abierto a todo el mundo a colaborar en el proyecto_.

El primer contacto que tuve con el equipo GeoWe fue en el pasado [Geonquietos C�rdoba](https://wiki.osgeo.org/wiki/Category:Geoinquietos_C%C3%B3rdoba) y tras comenzar a utilizar esta estupenda aplicaci�n y conocer al magn�fico [equipo](http://www.geowe.org/index.php?id=equipo) que est� detr�s del proyecto he de reconocer que me he convertido en un aut�ntico _groupie_ de GeoWE.

Tras nuestra �ltima reuni�n, con caf� y dulzaina incluida, he decido apoyar al proyecto testeado la aplicaci�n y [aportando](https://github.com/geowe/geowe-core/issues) los _bugs_, mejoras o comentarios que me van surgiendo.

[![](/images/blog/05_geowe/twitter.png)](https://t.co/YPhmW58EjP "merendola")

Pienso que la mejor manera de conocer GeoWE es us�ndolo, por lo que aqu� os dejo una pr�ctica sencilla para empezar a utilizar este SIG Web.

Por cierto, la gente de GeoWE est� presentando la aplicaci�n en las pr�ximas [Jornadas de SIG Libre de Girona](http://www.sigte.udg.edu/jornadassiglibre/)...me han dicho que llevan camisetas;-)

## Objetivo

*   Vamos a crear una capa de tipo poligonal para dibujar unas parcelas sobre el servicio WMS de Catastro.
*   Para cada pol�gono recopilaremos la referencia catastral, su direcci�n postal y su correspondiente enlace a la Sede de Catastro.
*   Una vez obtenidos los datos con GeoWE, los salvaremos a el archivo en local para poder trabajar con el el en un SIG.

## Abrimos GeoWE

Desde nuestro pc, tablet o tel�fono, podemos acceder a GeoWE en la siguiente direcci�n [http://demo-geowe.rhcloud.com/App.html](http://demo-geowe.rhcloud.com/App.html).

Para empezar nuestro "trabajo" lo primero que hacemos es centrar la vista del mapa a nuestra zona de inter�s. La herramienta **Geolocalizaci�n** que est� situada en el men� superior izquierda nos permite centrar el mapa de distintas maneras.

![](/images/blog/05_geowe/24.png)

*   Localizaci�n por direcci�n (ej. Calle Lucano, C�rdoba)
*   Utilizando el servicio [what3Words](http://what3words.com/es/). Nuestra zona de trabajo est� codificada como "estar�.sent�.prisa".
*   Geocoding por coordenadas (latitud/longitud) o ubicaci�n actual.

En la barra de iconos situados a la derecha encontramos la herramienta de **"Informaci�n"** que nos informa de la capa activa, sistema de coordenadas en las que estamos trabajando, longitud y latitud y la escala . Podemos igualmente cambiar el SRC y obtener las coordenadas del punto ya que, al pinchar en una localizaci�n en el la vista del mapa, las coordenadas se quedan fijadas.

![](/images/blog/05_geowe/25_coordendas.png)

## A�adir mapas base

Nuestras parcelas van ser dibujadas sobre la capa WMS de Catastro, por lo que primero debemos cargarla para tenerla activa en nuestro Administrador de capas. Para ello accedemos a **Men�>Mapa>Cat�logo** y a�adimos el servicio de Catastro.

![](/images/blog/05_geowe/30_catalogo.png)

GeoWE cuenta ya con un importante n�mero de servios de mapas en su cat�logo (Google, Bing, IGN, Catastro, OSM..), pero podemos a�adir nuestros otros servicios WMS desde el **Men�>Mapa>Capa>Raster** y a continuaci�n **A�adir capa WMS**. A continuaci�n introducimos la URL del servicio WMS, el nombre de la capa y el formato de imagen.

![](/images/blog/05_geowe/31_wms_catastro.png)

## Crear capa vectorial

Nuestra intenci�n es dibujar una serie de manzanas catastrales con geometr�a de pol�gonos. El primer paso es generar dicha capa en GeoWE desde **Men�>Capa>A�adir**.

![](/images/blog/05_geowe/32_a�adir_capa_vectorial.png)

Las opciones de **"A�adir"** son m�ltiples: desde cero o vac�a, a�adir capa desde una URL, pegar c�digo, subir un archivo o descargar desde un servicio WFS. Los formatos disponibles de subida son GeoJSON, KML, GML y WKT.

En este caso vamos a crear una capa nueva que se llamar� "parcelas_catastro", en ETRS89 UTM30N (EPSG:25830).

Podemos comprobar que nuestra capa est� creada accediendo a **Men�>Capas>Vector**. Desde el "Administrador de capas" podemos:

*   A�adir/Eliminar capas.
*   Hacer [zum](http://dle.rae.es/?id=cWlLJHL) a la capa.
*   Obtener informaci�n de la capa.
*   Descargar a local en formatos GeoJSON, KML, GML, WKT y CSV.
*   A�adir y modificar los atributos.

## Dibujando geometr�as

Desde **Men�>Dibujo>Pol�gono** seleccionaremos el tipo geogr�fico y empezaremos a dibujar nuestros pol�gonos. En este men� se encuentra tambi�n otras herramientas de edici�n que podemos usar para desplazar geometr�as o redibujar nodos.

![](/images/blog/05_geowe/36_dibujo.png)

GeoWE permite dibujar de forma precisa activando la opci�n de **"Snapping"** que utiliza los nodos de geometr�as existentes para ajustar las nuevas ediciones.

![](/images/blog/05_geowe/37_opciones_edicion.png)

Si queremos realizar operaciones espaciales m�s complejas como **uniones, divisiones, buffer**... podemos ejecutarlas desde la pesta�a **"Espaciales"**.

## A�adiendo atributos

Como he indicado, la finalidad de este ejercicio es la de dibujar una serie de manzanas catastrales y obtener una serie de atributos como la referencia catastral, la direcci�n, el tipo de construcci�n, etc.

Una vez dibujadas las manzanas vamos a a�adir las columnas de atributos que vamos a completar. Para ello vamos al "Administrador de capas" desde **Men�>Capas>Vector**. Tras seleccionar nuestra capa "parcelas_catastro" pinchamos en el bot�n **"Atributos de capa"**. En el formulario iremos a�adiendo tantos atributos como queremos. Para esta capa hemos a�adido tres: parcela, direcci�n y enlace.

![](/images/blog/05_geowe/40_atributos.png)

Para completar los datos de cada uno de los pol�gonos dibujados utilizaremos la opci�n **"Info/Edit"** de la barra **"Utilidades"** de GeoWE. A medida que vayamos pinchando en cada pol�gono nos aparecer� un formulario para ir completando la informaci�n de capa manzana.

Los datos podemos obtenerlos de forma visual o directamente desde Catastro usando la opci�n **"WMS info"**.

![](/images/blog/05_geowe/42_edicion_atributos.png)

## Salvando los datos en local.

Una vez que hemos terminado nuestra edici�n con GeoWE podemos exportar a local nuestra capa. Desde **Men�>Capas>Vector** seleccionamos nuestra capa y pinchamos en el bot�n **"Exportar"**. Una vez activa esta herramienta definimos el formato a exportar y el Sistema de Coordenadas para a continuaci�n descarga el fichero.

Una vez almacenados en nuestro equipo ya tenemos disponible nuestra capa geogr�fica creada con GeoWE para poder utilizarla en el caso que queramos con nuestro SIG de cabecera.

![](/images/blog/05_geowe/42_qgis.png)
        