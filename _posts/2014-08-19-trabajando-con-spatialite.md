---
title:  "Trabajando con Spatialite"
excerpt_separator: "<!--more-->"
comments: true
related: true
categories: 
      - 2014
tags:
      - QGIS
      - Sistemas de Informaci�n Geogr�fica
      - Spatialite
---
        
Una de las caracter�sticas que m�s me atrae de lo SIG�_open source_�es la capacidad de trabajar con gran variedad de formatos geogr�ficos tanto de tipo archivo (shape, geojson, kml,csv o dxf) como en bases de datos geogr�ficas (Postgres/PostGIS, MySQL o Geodatabase de ESRI).

Esta ventaja conlleva por otro lado un problema centrado en la elecci�n del formato de almacenamiento seg�n el tipo proyecto, encargo o trabajo SIG. Una buena entrada para comprender las ventajas/desventajas de cada sistema titulada**[Shapefiles vs bases de datos espaciales](http://mappinggis.com/2012/08/shapefiles-vs-bases-de-datos-espaciales/)**�puede encontrarse en la web MappingGIS de Aurelio Morales.

En mi caso, cuando el proyecto GIS tiene

*   cierta entidad respecto al n�mero de capas,
*   es necesario crear informaci�n geogr�fica combinado varias capas de datos mediante (views),
*   requiere campos de tipo texto exceden la capacidad de 254 caracteres o
*   se necesitan estilos gr�ficos predise�ados de visualizaci�n

mi decisi�n se decanta por el uso de una base de datos geogr�fica, normalmente�**PostgreSQL/PostGIS**.

Como bien se indica en el trabajo�**[Panorama del SIG Libre](https://panorama-sig-libre.readthedocs.org/es/latest/bbdd/index.html)**�presentado en las 8� Jornadas de SIG Libre, el uso de PostGIS dentro del sector GIS es fundamental y�_"aunque su uso a nivel general no est� tan extendido como MySQL, dentro del sector GIS su uso es casi can�nico"_. Pero existen algunas ocasiones, sobre todo cuando el usuario/cliente no tiene los conocimientos suficientes para la instalaci�n y administraci�n de bases de datos tipo Postgres/PostGIS, el volumen de datos no requeire el despliegue de una infraestructura de gran tama�o o no es necesario el trabajo la edici�n simult�nea de varios usuarios (concurrencia) donde PostgreSQL/PostGIS puede quedarnos un poco largo. En esos momentos es cuando entra en acci�n base de datos basada en ficheros�**Spatialite**.

Spatialite es ua extensi�n que agrega a SQLite el soporte para datos espaciales seg�n las especificaciones de la OGC. Podr�amos decir que�**Spatialite es a SQLite lo que PostGIS es a PostgreSQL**. La gran diferencia entre las dos sistemas de almacenamiento es que SQLite/Spatialite est� configurado por un �nico fichero lo que facilita su "portabilidad" (no s� si es muy adecuado utilizar este adjetivo pero creo que se entiende) y es bastante sencillo de instalar y configurar. Para saber m�s sobre las funcionalidades principales de Spatialite se puede acceder a la�[p�gina oficial del proyecto Spatialite](http://www.gaia-gis.it/gaia-sins/)o a este enlace de la�[documentaci�n de OSGeoLive](http://live.osgeo.org/es/overview/spatialite_overview.html)�sobre la extensi�n.

## [](https://github.com/sigdeletras/sigdeletras.github.io/blob/master/_posts/2014/2014-08-20-trabajando-con-spatialite.md#spatialite-para-rude-men)Spatialite para�_rude men_

Tras obtener los archivos binarios desde la�[p�gina oficial](http://www.gaia-gis.it/gaia-sins/)�e instalar seg�n el sistema operativo (en mi caso con sudo apt-get install spatialite-bin), podemos trabajar con Spatialite desde la terminal usando el comando�_spatialite_. A continuaci�n ten�is un ejemplo de conexi�n

    spatialite /home/user/data/spatialite/equipamientos_culturales.sqlite

y otro de una consulta.

    SELECT ROWID, "Name", "tipologia", "geometry"FROM "equipamientos_culturales"WHERE "tipologia" = "Museos";
    
Si lo nuestro no es la consola o no somos unos verdaderos�_rude men_�podemos instalar y utilizar la�**interfaz gr�fica****_spatialite_gui_**. Con esta herramienta podremos crear nuestras bases de datos, importar/exportar ficheros (shapes, csv/txt, dbf o xls), generar consultas, realizar operaciones geogr�ficas, acceder a los metadatos de la base de datos o ver el historial de operaciones entre otras operaciones. Desde esta GUI podremos tambi�n obtener una vista geogr�fica simple de nuestros datos y salvarla a un formato gr�fico como png, svg o pdf. Para la versi�n 1.5 existe un tutorial r�pido en ingl�s en este�[enlace](http://www.gaia-gis.it/gaia-sins/spatialite-gui-docs/spatialite_gui-1.5.0.pdf).

[![03_spatialite_gui](https://camo.githubusercontent.com/ff558accea4389444dd946b0e9af07c24a91fe90/68747470733a2f2f6661726d342e737461746963666c69636b722e636f6d2f333837312f31343739323639383334385f326161376463373866615f7a2e6a7067)](https://camo.githubusercontent.com/ff558accea4389444dd946b0e9af07c24a91fe90/68747470733a2f2f6661726d342e737461746963666c69636b722e636f6d2f333837312f31343739323639383334385f326161376463373866615f7a2e6a7067)

_Spatialite GUI_

## [](https://github.com/sigdeletras/sigdeletras.github.io/blob/master/_posts/2014/2014-08-20-trabajando-con-spatialite.md#trabajando-con-spatialite-con-qgis)Trabajando con Spatialite con QGIS

Para ponerlo aun m�s f�cil, desde�**QGIS**�podremos trabajar, crear y editar sin problemas datos espaciales en Spatialite, ya que este SIG permite por defecto conectarnos a este tipo bases de datos geogr�ficas. Los men�s, operaciones y accesos m�s comunes son:

*   Creaci�n de una nueva capa y su correspondiente fichero r�pidamente desde el men��_Capa>Nueva>Nueva Capa Spatialite_
*   A�adir una capa desde una una bbdd ya existente desde�_Capa>A�adir capa Spatialite_
*   Gestionar la base de datos desde el Administrador de Bases de datos del men��_Base de Datos_. Desde aqu� podremos realizar algunas tareas administrativas como crear, borrar o renombrar capas o importar/exportar archivos.

[![06_administrador_bbdd](https://camo.githubusercontent.com/a91f340882cd5112f424df2ff457edd44c48ce7e/68747470733a2f2f6661726d342e737461746963666c69636b722e636f6d2f333833372f31343739323631393133395f306261326139636664355f7a2e6a7067)](https://camo.githubusercontent.com/a91f340882cd5112f424df2ff457edd44c48ce7e/68747470733a2f2f6661726d342e737461746963666c69636b722e636f6d2f333833372f31343739323631393133395f306261326139636664355f7a2e6a7067)

_Administrador de BBDD_

Podemos tambi�n trabajar con la�**[extensi�n QSpatiaLite](https://code.google.com/p/qspatialite/)**�que incluye muchas de las operaciones que podemos realizar desde�_spatialite_gui_�pero sin salirnos de QGIS. Podemos crear sentencias SQL avanzadas o importar/exportar ficheros seg�n los formatos espaciales OGR. En el siguiente ejemplo obtenemos una tabla con el n�mero de equipamientos culturales por cada barrio del conjunto hist�rico de C�rdoba.

    SELECT  "da04_barrio_ch".'barrio' , COUNT(*) FROM  "equipamientos_culturales" ,  "da04_barrio_ch"      WHERE  Within( "equipamientos_culturales".'geometry' ,  "da04_barrio_ch".'geom' ) GROUP BY   "da04_barrio_ch".'barrio';

[![08_qgis_QspatiaLite](https://camo.githubusercontent.com/c39d0a7f9b5768ca9ad29d912cda61159a6f8b9f/68747470733a2f2f6661726d342e737461746963666c69636b722e636f6d2f333835322f31343935363331393239365f623839353030303739625f7a2e6a7067)](https://camo.githubusercontent.com/c39d0a7f9b5768ca9ad29d912cda61159a6f8b9f/68747470733a2f2f6661726d342e737461746963666c69636b722e636f6d2f333835322f31343935363331393239365f623839353030303739625f7a2e6a7067)

_Extensi�n QSpatiaLite_

Por �ltimo, y no menos importante, la �ltima versi�n de QGIS (2.4) permite�**a�adir a nuestra base de datos los estilos de visualizaci�n**�y consulta de datos definidos para nuestras capas y asignarlos como estilos por defecto. Este opci�n es realimente interesante, ya que en un mismo fichero podemos incluir el aspectos gr�ficos de nuestras capas. Para guardar el estilo, accederemos a la pesta�a�_Estilo_�del formulario�_Propiedades de la capa_. Tras definir el tipo de visualizaci�n, pincharemos el bot�n "Guardar estilo" y la opci�n "Guardar en base de datos (spatialite)"

[![09_qgis_salvar_estilo](https://camo.githubusercontent.com/25bffe657f1c1289ce37a529a18a932030579e60/68747470733a2f2f6661726d362e737461746963666c69636b722e636f6d2f353537322f31343739323631393631395f366335336265633636635f7a2e6a7067)](https://camo.githubusercontent.com/25bffe657f1c1289ce37a529a18a932030579e60/68747470733a2f2f6661726d362e737461746963666c69636b722e636f6d2f353537322f31343739323631393631395f366335336265633636635f7a2e6a7067)

_Guardar estilo en base de datos_
        