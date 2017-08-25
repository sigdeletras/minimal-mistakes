---
title:  "Gu�a r�pida para empezar con PostGIS en Windows"
excerpt_separator: "<!--more-->"
comments: true
related: true
categories: 
      - 2014
tags:
      - PostGIS
---
        
Acabo de mandar un correo r�pido a un amigo que me ha pedido informaci�n de c�mo empezar con trabajar con PostGIS en Windows. Es un relaci�n sencilla de pasos y enlaces pero creo que puede ayudar.

_"PostGIS es un m�dulo que a�ade soporte de objetos geogr�ficos a la base de datos objeto-relacional PostgreSQL, convirti�ndola en una base de datos espacial para su utilizaci�n en Sistema de Informaci�n Geogr�fica. Se publica bajo la Licencia P�blica General de GNU."_

_Wikipedia dixit_

## [](https://github.com/sigdeletras/sigdeletras.github.io/blob/master/_posts/2014/2014-05-20-guia-rapida-para-empezar-con-postgis-en-windows.md#instalaci%C3%B3n)Instalaci�n

*   Seguir los pasos expuestos en la siguiente gu�a�[http://postgis.net/windows_downloads](http://postgis.net/windows_downloads)
*   La descarga directa de la �ltima versi�n se encuentra en este enlace[http://download.osgeo.org/postgis/windows/pg93/](http://download.osgeo.org/postgis/windows/pg93/)

## [](https://github.com/sigdeletras/sigdeletras.github.io/blob/master/_posts/2014/2014-05-20-guia-rapida-para-empezar-con-postgis-en-windows.md#administraci%C3%B3n)Administraci�n

*   Adem�s de la consola, se puede utilizar como GUI de administraci�n�[pgAdmin](http://www.pgadmin.org/)

*   Si se quiere trabajar desde web se puede instalar�[phppgadmin](http://phppgadmin.sourceforge.net/doku.php), siempre que tengamos un servidor web a mano. (ej.[WAMP](http://www.wampserver.com/en/))

## [](https://github.com/sigdeletras/sigdeletras.github.io/blob/master/_posts/2014/2014-05-20-guia-rapida-para-empezar-con-postgis-en-windows.md#crea-una-bbdd-con-funcionalidades-geogr%C3%A1ficas)Crea una bbdd con funcionalidades geogr�ficas

*   Una vez instalado Postgres/PostGIS y utilizando, por ejemplo pgAdmin, se debe crear una base de datos con funciones espaciales utilizando la plantilla PostGIS (Template PostGIS).

## [](https://github.com/sigdeletras/sigdeletras.github.io/blob/master/_posts/2014/2014-05-20-guia-rapida-para-empezar-con-postgis-en-windows.md#a%C3%B1adir-shape-a-postgis)A�adir shape a PostGIS

*   Para a�adir un shp se puede utilizar algunas de estas formas, perfectamente descritas en la entrada�["C�mo importar shapefiles a PostGIS"](http://mappinggis.com/2013/02/como-importar-shapefiles-a-postgis/)�de Aurelio Morales en MappingGIS.

## [](https://github.com/sigdeletras/sigdeletras.github.io/blob/master/_posts/2014/2014-05-20-guia-rapida-para-empezar-con-postgis-en-windows.md#para-saber-algo-m%C3%A1s)Para saber algo m�s

*   Os recomiendo la web del workshop�["Introduction to PostGIS](http://workshops.boundlessgeo.com/postgis-intro/index.html)�de la gente de Boundless.
        