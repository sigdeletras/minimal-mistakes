---
title:  "\"Espa�a Finisecular\" visor de consulta Minutas Cartogr�ficas del IGN"
header:
      teaser: "/images/header/206-02-23-visorminutas.jpg"
categories: 
	- Blog
tags:
- Webmapping
- Leaflet
- Servicios OGC
---

**Espa�a finisecular** es **un visor web de visualizaci�n del [servicio de mapas WMS �de las Minutas Cartogr�ficas](http://www.ign.es/wms/minutas-cartograficas?request=GetCapabilities&service=WMS)** mantenido por el Instituto Geogr�fico Nacional e incluido en la Infraestructura de Datos Espaciales de Espa�a.�<span style="font-size: 12.16px; line-height: 1.3em;">Para saber m�s sobre este servicio se puede consultar esta e[ntrada en el Blog de la IDEE](http://blog-idee.blogspot.com.es/2015/09/servicio-de-mapas-de-minutas.html).</span>

<span style="font-size: 12.16px; line-height: 1.3em;">Desde este visor, accesible desde la direcci�n [sigdeletras.com/visorminutas/](http://sigdeletras.com/visorminutas/), se acceder a la capa cartogr�fica continua generada a partir del recorte y la georreferenciaci�n de los mapas manuscritos en papel conservados en el Archivo T�cnico del IGN. Estos mapas, seg�n se refleja en la p�gina del IGN, �son el resultado de los trabajos previos a la realizaci�n del Mapa Topogr�fico Nacional y se realizaron principalmente entre 1870 y 1950 y fueron �dibujados a escala 1:25.000, con una precisi�n de obtenci�n de la informaci�n correspondiente a escala 1:50.000.</span>

Los datos, de gran valor para trabajos o estudios hist�ricos sobre el territorio nacional, ofrecen informaci�n de gran inter�s vinculaba principalmente a la red de comunicaciones, pero tambi�n incluyen datos sobre nombres geogr�ficos, construcciones, top�nimos red hidrogr�fica �o cultivos entre otros.

###   
<iframe style="border: 1px solid black;" src="http://sigdeletras.com/visorminutas" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" width="100%" height="350"></iframe>

<small>[Ver mapa m�s grande](http://visorminutas.sigdeletras.com/)</small>

### **Funciones principales**

#### Consulta visual de la informaci�n geogr�fica

Junto a la posibilidad de visualizar la informaci�n geogr�fica, el visor �Espa�a finisecular� permite la comparaci�n de los mapas de las minutas con otros servicios de ortofotograf�as y mapas tanto reciente como antiguos. Para ello se ha incluido una barra que permite aplicar transparencia a la capa de las minutas.

<span style="font-size: 12.16px; line-height: 1.3em;">Las capas disponibles en esta primera versi�n del Visor:</span>

*   <span style="font-size: 12.16px; line-height: 1.3em;">[Ortofotos m�xima actualidad del PNOA]((http:/www.ign.es/wms-inspire/pnoa-ma?request=GetCapabilities&service=WMS).</span>
*   <span style="font-size: 12.16px; line-height: 1.3em;">[Cartograf�a Catastral](http://ovc.catastro.meh.es/Cartografia/WMS/ServidorWMS.aspx?request=GetCapabilities&service=WMS) de la Direcci�n General del Catastro.</span>
*   <span style="font-size: 12.16px; line-height: 1.3em;">[Primera edici�n de cada hoja del Mapa Topogr�fico Nacional 1:50.000](http://www.ign.es/wms/primera-edicion-mtn?request=GetCapabilities&service=WMS) (MTN50).</span>
*   [<span style="font-size: 12.16px; line-height: 1.3em;">OpenStreetMap</span>](http://www.openstreetmap.org/)
*   <span style="font-size: 12.16px; line-height: 1.3em;">Sobre las minutas, tambi�n puede activarse los [l�mites administrativos de Espa�a](http://www.ign.es/wms-inspire/unidades-administrativas?request=GetCapabilities&service=WMS).</span>

#### Consulta de datos

Activando la opci�n **�Consulta de datos de minutas�** se realiza una petici�n GetFeatureInfo al WMS de las minutas de la que se obtiene la la fecha de creaci�n de la minuta entre otros datos.

![](/images/blog/04_wms.jpg)

Desde esta misma consulta, se puede acceder al **enlace de descarga de la minuta** existente en el Centro de Descargas del CNIG. Los archivos georrerenciados completan la informaci�n del servicio al permitir consultar informaci�n de inter�s incluida en las leyendas, cartelas y anotaciones manuscritas. Estos archivos pueden ser cargados en cualquier Sistema de Informaci�n Geogr�fica.

#### Buscador de nombres geogr�ficos

Usando la extensi�n [Geocoder,](https://github.com/perliedman/leaflet-control-geocoder) se ha incluido una buscador que accede a la base de datos de nombres geogr�ficos [Nominatim](http://wiki.openstreetmap.org/wiki/Nominatim).

![](/images/blog/01_loc.jpg)

#### <span style="line-height: 1.3em;">Opciones de compartir</span>

De desarrollo propio, se ha incluido en la barra de herramientas la opci�n de obtener el correspondiente c�digo HMTL para i**ncluir el visor en otras p�ginas web**. Tambi�n se ha a�adido un bot�n para compartir el visor en **Twitter**.

![](/images/blog/02_measue.jpg)

#### Mediciones

Gracias a la extensi�n �[Leaflet.measure](https://github.com/ljagis/leaflet-measure)�se ha habilitado la herramienta, en ingl�s, de captura de longitudes y �reas.�

![](/images/blog/03_embeber.jpg)

### Tecnolog�a<span style="font-size: 12.16px; line-height: 1.3em;">�</span>

El dise�o del visor est� basado en la plantilla�[Bootleaf](http://bmcbride.github.io/bootleaf/)�utilizando la�[Bootstrap](http://getbootstrap.com/)�y la librer�a JavaScrip de mapas�[Leaflet](http://leafletjs.com/).
        