---
title:  "Datos geogr�ficos para la provincia de Almer�a"
excerpt_separator: "<!--more-->"
related: true
categories:
- Presentaci�n
tags:
- Almer�a
---
        
Navegando por Internet podemos apreciar que la visualizaci�n o presentaci�n de informaci�n geogr�fica en p�ginas web est� cada vez m�s presente. Hoy por hoy, no es muy complicado incluir en nuestra p�gina un mapa con la localizaci�n de nuestro negocio o la sede de un evento. La forma m�s r�pida es obtener dicho mapa directamente desde Google Maps, usando otras alternativas abiertas como [OpenStreetMap](http://www.openstreetmap.org/ "http://www.openstreetmap.org/"), o trabajar con alguna de las extensiones de mapas que incorpora Wordpress, Joomla o Drupal.�

Sin embargo, si queremos dar un paso m�s en la presentaci�n de nuestros datos, por ejemplo mostrando un mapa de densidad o una visualizaci�n tem�tica de una determinada variable, podemos usar servicios de mapas en nube como [CartoDB](http://cartodb.com/ "http://cartodb.com/") o [My Maps de Google](https://www.google.com/maps/d/ "https://www.google.com/maps/d/"). Para proyectos m�s personalizados, en las que ya es necesario tener conocimientos b�sicos de HTML, CSS y JavaScript podemos recurrir a librer�as de mapas como [OpenLayers](http://openlayers.org/ "http://openlayers.org/") o [Leaflet](http://leafletjs.com/ "http://leafletjs.com/").

El aspecto tecnol�gico vinculado a la creaci�n de un visor de mapas parece un tema bastante solucionado. Pero existe otra cuesti�n que hay que tener en cuenta: la relacionada con la generaci�n de los datos geogr�ficos a representar o incluso la obtenci�n de bases cartogr�ficos a los que vincular nuestra recopilaci�n de datos como puede ser una capa vectorial con los l�mites de los municipios de una provincia.

Con esta finalidad, la de conocer las principales fuentes de informaci�n geogr�ficas para el dise�o de un mapa en Internet, la gente de **HackLab Almer�a** organiz� el pasado d�a 12 de mayo el [Taller �Fuentes de informaci�n geogr�fica para la provincia de Almer�a�](http://hacklabalmeria.net/actividades/2015/05/12/fuentes-datos-almeria.html "http://hacklabalmeria.net/actividades/2015/05/12/fuentes-datos-almeria.html"). Durante la charla present� una recopilaci�n de enlaces a p�ginas web de la administraci�n como el Centro Nacional de Informaci�n Geogr�fica del Ministerio de Fomento o el Instituto de Estad�stica y Cartograf�a de Andaluc�a, desde la que se puede descargar informaci�n geogr�fica. Tambi�n inclu� datos sobre el estado de los datos geogr�ficos en distintas web municipales y de la provincia de Almer�a.  

[![](/images/blog/Captura.PNG)](http://sigdeletras.github.io/2015-ig-almeria/ "Enlace a la presentaci�n")

Dentro del [repositorio de Github](https://github.com/sigdeletras/2015-ig-almeria/) donde se encuentra la presentaci�n, he creado la [carpeta DATOS con conjuntos tem�ticos de datos para la provincia de Almer�a](https://github.com/sigdeletras/2015-ig-almeria/tree/gh-pages/datos) procedentes de los�*Datos Espaciales de Referencia de Andaluc�a (DERA)*. Las capas est�n en formato [geoJSON](http://geojson.org/ "http://geojson.org/") y se encuentran convertidos al sistema de coordenadas WGS84.

_�Localizaci�n de los ayuntamientos de los municipios de Almer�a. Fuente DERA_

A modo de reflexi�n, s�lo apuntar que cada vez me encuentro en este tipo de actividades con asistentes cuyos perfiles profesionales no est�n tradicionalmente vinculados al mundo �geo�, pero que empiezan a estar interesados en el uso de las Tecnolog�as de Informaci�n Geogr�ficas. Un buen ejemplo son los profesionales que trabajan en el �mbito del Periodismo de Datos o los dise�adores gr�ficos. Por otro lado, una vez que se empiezan a conocer estas herramientas, por propia evoluci�n, en estos casos se hace necesario ir adquiriendo conocimientos m�s concretos sobre tipos de formatos geogr�ficos, sistema de referencia de coordenadas o incluso plantearse empezar a manejar aplicaciones como los Sistemas de Informaci�n Geogr�fica para generar y preparar los datos geogr�ficos que van a ser presentados en Internet.
        