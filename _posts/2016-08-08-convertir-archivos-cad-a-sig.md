---
title:  "Convertir archivos CAD a SIG"
categories: 
- blog
tags:
- CAD
- Sistemas de Informaci�n Geogr�fica
---

Trabajar con archivos CAD en un Sistema de Informaci�n Geogr�fica no es tarea f�cil. Por regla general, cuando se dibuja en un programa CAD comi AutoCAD o MicroStation, no se hace pensando en incluir procedimientos que faciliten la conversi�n de la informaci�n espacial a un modelo de datos SIG. En esta entrada, comentar� algunas de las caracter�sticas estos archivos CAD que influir�n en su conversi�n a un SIG. A continuaci�n, y bas�ndome en mi experiencia personal, se enumerar�n los procesos b�sicos para intentar llevar a cabo con el mayor �xito posible este tipo de trabajo.

## �Porqu� pasar de CAD a SIG?

Podemos decir que hay dos motivos generales por las que nos vemos obligados a trabajar con datos CAD en un proyecto SIG. La primera causa es simplemente que **necesitemos usar como base una fuente de datos creados con CAD**. Suele ser frecuente que para escalas grandes, de 500 a 2000, la informaci�n cartogr�fica de referencia se encuentre en este formato. Quiz�s el caso que mejor ejemplifique este motivo es la generaci�n de un planeamiento urban�stico. Tras los trabajos de informaci�n y ordenaci�n, el resultado principal no deja de ser mapas tem�ticos (clasificaciones, calificaciones, usos, sistemas�) que usan como base CAD.

El segundo caso aborda la **generaci�n en formato SIG de las base cartogr�fica unificada (plano ciudad, mapa gu�a, mapa base, base topogr�fica armonizada...) de un municipio o ciudad**. Esta informaci�n geogr�fica servir� de base para m�ltiples trabajos vinculados tanto con la generaci�n de cartograf�a digital, como para la toma de decisiones sac�ndole el m�ximo rendimiento a las posibilidades metodol�gicas y t�cnicas de un sistema de informaci�n geogr�fico. La base ser� fundamental para trabajo de inventarios de infraestructuras, gesti�n de redes, mantenimiento callejero, estudios de geomarketing, actividades econ�micas y licencias, urbanismo, padr�n municipal o catastro. Este mapa base servir� para la elaboraci�n de mapas en papel� (mapas tur�sticos, planos de la ciudad, cartograf�a tem�tica) y tambi�n para generar productos cartogr�ficos digitales consumidos a trav�s de servicios OGC o mapas de teselas mediante visores cartogr�ficos.

## [![Mapa base del Visor IDE Zaragoza](https://c1.staticflickr.com/9/8491/28561488600_5528897c40_b.jpg)](https://www.flickr.com/photos/115384326@N07/28561488600/in/dateposted-public/ "virsorzaragoza")  Consideraciones sobre los datos CAD

### Formatos y versiones

Si nos centramos en SIG abiertos (gvSIG o QGIS) que suelen utilizar la librer�a GDAL (http://www.gdal.org/ogr_formats.html) debemos de tener en cuenta la lectura de archivos CAD se encuentra limitada a versiones menos recientes y liberadas. Por ejemplo, QGIS lee archivos DGN (http://www.gdal.org/drv_dgn.html) la versi�n 7/8 y lee y crea DXF en su versi�n 2000\. GvSIG a�ade la posibilidad de cargar archivos DWG.

Si necesitamos cambiar la versi�n de los archivos deberemos disponer los correspondientes programas propietarios o bien usar alguno libre como [Draftsight](http://www.3ds.com/es/productos-y-servicios/draftsight/) o el programa [TeighaFileConverter](https://www.opendesign.com/guestfiles/TeighaFileConverter)

### Geometr�as

Los datos CAD 2D constan de primitivas geom�tricas. Entre los ejemplos de geometr�a 2D est�n de forma general:

*   Puntos
*   Segmentos de l�neas y polil�neas cerradas que representan pol�gonos
*   Regiones planas 2D
*   Arcos, splines y c�rculos
*   Bloques

La conversi�n de geometr�as CAD a SIG es uno de trabajos m�s costosos. Todo depender� de los criterios de dibujo usados y el nivel de detalle y precisi�n que se haya querido dar. El proceso m�s recurrente ser� la obtenci�n o transformaci�n de los elementos poligonales a partir de l�neas. En QGIS nos ser� de gran ayuda la herramienta �Poligonizar�.  

[![Poligonaci�n en QGIS](https://c7.staticflickr.com/9/8124/28814587846_c1f298f5fa.jpg)](https://www.flickr.com/photos/115384326@N07/28814587846/in/dateposted-public/ "poligonacion") 

### Textos

La anotaci�n en un archivo CAD se mide en unidades de mapa cuando se crea. Normalmente, el texto de una l�nea y multil�neas son elementos gr�ficos independientes que no tienen capacidad inherente para vincularse con la geometr�a.

Al cargarlo un SIG, los textos ser�n representados como un punto y el valor ser� almacenado en una columna de la capa. Aqu� los principales problemas ser�n: los textos en multil�nea, ya cada salto de l�nea ser� representado por un registro en la tabla, la asociaci�n de los datos a elementos lineales como ejes de v�as, estilo y simbolog�a, codificaci�n de caracteres.  

[![Archivo DGN en QGIS](https://c3.staticflickr.com/9/8632/28561489330_f2b2af8c41_b.jpg)](https://www.flickr.com/photos/115384326@N07/28561489330/in/dateposted-public/ "Archivo DGN en QGIS") 

### Estructura de la informaci�n

Las capas de CAD organizan los datos de manera similar a las capas de un SIG; sin embargo, no siguen el modelo de entidades simples del SIG. Los autores del CAD tienen la libertad de mezclar tipos de geometr�a y otros datos en una capa individual. Tambi�n es posible utilizar el tipo y color de l�nea para clasificar mejor los datos. Como resultado, el contexto de los datos, junto con la informaci�n textual y una cantidad significativa de interpretaci�n humana pueden ser necesarios para identificar la geometr�a como una entidad SIG particular.

[![Descripcion de capas de un archivo dwg. IDE Sevilla](https://c3.staticflickr.com/9/8292/28561670770_f3c6fa7815_b.jpg)](https://www.flickr.com/photos/115384326@N07/28561670770/in/dateposted-public/ "Descripcion de capas de un archivo dwg. IDE Sevilla")

Por si no fuera bastante la organizaci�n depender� de software: AutoCAD usa el concepto capa, mientras que los archivos DGN est�n organizados en 63 niveles que junto a el color, estilo y peso definen cada una de las capas. Para la importaci�n de las fuentes CAD ser� fundamental disponer del modelo de datos usados, en la que se defina la estructura de las capas/niveles usados y la descripci�n del sistema de codificaci�n. Puede que tengamos suerte y encontremos un DWG con correcta definici�n de sus contenidos en la descripci�n de sus capas, pero tambi�n podemos encontrarnos con un listado interminable de capas definidas por c�digos y si no tenemos una tabla de equivalencias ser� casi imposible realizar la importaci�n. En el caso de los DGN es imprescindible.

[![Modelo de datos con la estructura de niveles DGN. IECA](https://c3.staticflickr.com/8/7651/28814722626_1741378a91_b.jpg)](https://www.flickr.com/photos/115384326@N07/28814722626/in/dateposted-public/ "Modelo de datos con la estructura de niveles DGN. IECA") 

### Georrefenciaci�n, escalas y rotaciones

El problema de escala define una diferencia fundamental entre c�mo los sistemas de SIG y CAD utilizan los sistemas de coordenadas. Un SIG modela el mundo y los objetos que contiene en una escala regional o global. Por el contrario, un sistema de CAD se utiliza para modelar los objetos reales a una escala que relativamente no se ve afectada por la superficie de la tierra. Esto conlleva que nos encontremos con datos que est�n en coordenadas relativas, que no trabajemos a escala real o incluso que tengamos la informaci�n rotada.  

La mejor forma de solucionar estos problemas es hacer las correspondientes correcciones en el mismo programa CAD.

### Divisiones

Aunque esto en principio pueda no parecer un problema, es muy com�n encontrarnos la cartograf�as municipales o de planes generales divididas en hojas. A todos los trabajos anteriores habr� que a�adirle la limpieza de marcos, cajas de impresi�n, leyendas y cartelas. Pero lo peor sin duda ser� el tiempo que tendremos que dedicarle a la uni�n de las geometr�as, sobre todo las que representan �reas, que quedan en los l�mites entre hojas.

### Actualizaci�n

Este aspecto no tiene en principio relaci�n con el tipo de formato CAD pero es frecuente que debido a los altos costes de los trabajos de restituci�n cartogr�fica de una ciudad no se suele contar con un cartograf�a CAD reciente. Esta situaci�n deber� ser tomada en cuenta a la hora de identificar �reas transformadas y no representadas en la fecha del vuelo y la restituci�n. Puede sernos de gran ayuda la incorporaci�n de las capas de Catastro y las ortofotograf�as existentes.

[![Comparaci�n de archivo CAD con Catastro y PNOA](https://c6.staticflickr.com/9/8306/28231314053_d87c304074_b.jpg)](https://www.flickr.com/photos/115384326@N07/28231314053/in/dateposted-public/ "Comparaci�n de archivo CAD con Catastro y PNOA") 

## Metodolog�a

Dentro de los trabajos de transformaci�n de fuentes de datos CAD a un Sistema de Informaci�n Geogr�fica debemos distinguir entre el conjunto de procesos a realizar con una herramienta CAD y aquellos que usaremos una vez convertida la informaci�n a SIG. Para cada uno estos procesos utilizaremos una o varias herramientas de nuestros paquetes inform�ticos, cuyo nombre depender� del CAD o SIG que usemos. Por ello s�lo hemos descrito el tipo de tarea a utilizar y no la herramienta usada.

### Trabajos en CAD

*   Si fuera necesario, escalado, rotaci�n y georreferenciaci�n de los archivos.
*   An�lisis y reestructuraci�n de capas/niveles. Limpieza de capas. Identificaci�n textos� y generaci�n de capas espec�ficas de informaci�n textual.
*   Depuraci�n de elementos de cartelas y marcos.
*   Uni�n de archivos (hojas), y correcci�n de geometr�as en los bordes.
*   Mejora de la base de informaci�n, a partir de procesos de limpieza y correcci�n de la  
    geometr�a seg�n las necesidades de los programas SIG: uni�n de l�neas, solape de l�neas, cierre de pol�gonos, conexi�n de redes, regeneraci�n de pol�gonos (contornos), edici�n de anotaciones.
*   Conversiones de formato/versi�n.

### Trabajos en SIG

*   Definici�n de capas y modelos de datos seg�n el an�lisis de archivos CAD
*   Conversi�n SIG (Shape, PostGIS o Spatialite) por capas/niveles.
*   Descripci�n de la codificaci�n de capas/niveles.
*   Depuraci�n entidades, correcci�n de errores geom�tricos y topol�gicos.
*   Transformaci�n de l�neas a pol�gonos de capas que lo requieran.
*   Generaci�n de atributos de capa y estandarizaci�n de la informaci�n. Creaci�n de tablas de dominios.
*   Asignaci�n por localizaci�n (punto-pol�gono) de informaci�n de CAD en formato texto.
*   Definici�n de estilos, simbolog�a y etiquetados.
*   Identificaci�n de �reas con informaci�n desactualizada (ortofotograf�a, catastro...)
*   Informe de metadatos.
        