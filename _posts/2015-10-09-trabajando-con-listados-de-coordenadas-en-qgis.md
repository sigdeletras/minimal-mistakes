---
title:  "Trabajando con listados de coordenadas en QGIS"
header:
      teaser: "/images/header/2015-10-09-cabecera_ategua.png"
categories: 
 - Blog
tags:
 - Formaci�n
 - QGIS
 - Sistemas de Informaci�n Geogr�fica
 - Arqueolog�a
---

En numerosas ocasiones el resultado de la toma de datos en campo con un GPS, una estaci�n total o capturando datos sobre bases cartogr�ficas es un listado de coordenadas que identifican una serie de localizaciones, como podr�an ser elementos arqueol�gicos, un elemento poligonal como un entorno de protecci�n o un corte, o una estructura lineal tipo infraestructura o camino.

<iframe style="border: 1px solid black;" src="/webpamming/visorategua/" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" width="100%" height="350"></iframe>

_Visor Zona Arqueol�gica de Ategua.BIC y entorno de protecci�n. [Ver mapa m�s grande](/webpamming/visorategua/)_

Este tipo de informaci�n geogr�fica, me refiero al listado de coordenadas, suele ser solicitado por administraciones p�blicas como parte de los informes finales de proyectos y pueden encontrarse en boletines y publicaciones de la administraci�n. Saber extraer esta informaci�n de nuestras entidades geogr�ficas digitales o convertir estos datos en informaci�n que pueda ser tratada con una herramienta inform�tica, como un SIG, puede ser un aprendizaje interesante y de gran utilidad desde el punto de vista profesional.

El [Sistema de Informaci�n Geogr�fica QGIS](http://www.qgis.org/es/site/), posee herramientas directas para convertir listados de coordenadas en formato tabla (CSV o TXT) en entidades geogr�ficas puntuales. Si en las tablas existe otra columna que nos sirva para agrupar los datos,por ejemplo un c�digo de yacimiento, estos datos pueden pasar a convertir de forma autom�tica en l�neas y estas a su vez en pol�gonos.

![ATEGUA. Banco im�genes IAPH. Autor: J.C. Cazalla](/images/blog/201510_visorategua/70_0006241.jpg "ATEGUA. Banco im�genes IAPH. Autor: J.C. Cazalla")

_Vista panor�mica de Ategua. Fuente: Banco de im�genes IAPH. Autor: Cazalla, Juan Carlos_

Supongamos que tenemos un listado de coordenadas que identifican un bien arqueol�gico y tambi�n su entorno de protecci�n. En este caso vamos a obtener los datos del [**yacimiento arqueol�gico de Ategua**](http://www.iaph.es/patrimonio-inmueble-andalucia/resumen.do?id=i2768) en la provincia de C�rdoba. Los datos de las coordenadas del BIC y su entorno est�n disponibles en el Bolet�n Oficial de la Junta de Andaluc�a [(BOJA)� n� 244 de 16/12/2005](http://www.juntadeandalucia.es/boja/2005/244/35 "BOJA") . Lamentablemente� estos datos no est�n en el PDF en formato imagen por lo que tendremos que ir copiando manualmente las coordenadas en una hoja de c�lculo en la que se incluya� el n�mero de orden la coordenada, el valor de X y el valor de Y. Como tenemos la informaci�n tanto del BIC como del entorno , vamos a a�adir una nueva columna al principio que denominaremos entidad, donde quedar� reflejado si la coordenadas es de la Zona Arqueol�gica o del Entorno.

Una vez obtenidos los datos, pasaremos la tabla a formato CSV, utilizando las opci�n de Guardar como de nuestro programa de hoja de c�lculo, en mi caso Calc de LibreOffice. El formato csv no es m�s que un texto plano donde cada fila es un registro de la tabla, y en que los valores por columnas se encuentra separado por comas. Es un formato est�ndar que suele poder cargarse en la mayor�a de los programas que trabajan con datos tabulares como las bases de datos o las hojas de c�lculo, o en nuestro caso los SIG.

![](/images/blog/201510_visorategua/datos.png)

_Listado de coordenadas en hoja de c�lculo y archivo CSV._

Una vez que tengamos nuestro csv, abrimos QGIS y seleccionamos el Sistema de Coordenadas de Referencia en el que se encuentren los v�rtices. Aunque en el BOJA, no se hace referencia al SRC, aunque deber�a, por la fecha estos datos est�n en ED50 UTM30N.

Para a�adir la tabla de coordenadas, usamos la opci�n **�A�adir capa de texto delimitado�** del men� A�adir Capa. Indicaremos la ubicaci�n del archivo CSV, indicaremos el tipo y comprobaremos que QGIS a seleccionado las columnas correctas para las coordenadas X e Y. Una vez revisado las opciones, pulsamos en aceptar y tendremos representados las coordenadas de� nuestra tabla en puntos. La capa se genera de forma temporal por lo que si queremos trabajar con ella podemos guardarla en Shape o almacenarla en nuestra base de datos PostGIS o SpatiaLite. Para una mejor compresi�n de los datos podemos cargar cartograf�a base o alguna ortofoto como las del PNOA.

![](/images/blog/201510_visorategua/carga_csv.png)

Para pasar los datos puntuales a lineales o poligonales y mejorar la compresi�n de la informaci�n, vamos a utilizar dos procesos de la caja de Herramientas.

*   **_Point to path_** nos generar� una l�nea seg�n el orden de los puntos (Campo de Orden) y utilizar� los datos de la columna entidad para agrupar los trazados (Campo de Grupo).
*   Con **_Lines to Polygon_** generaremos una nueva capa poligonal a partir de las l�neas. Tendremos que tener en cuenta que nos generar� un pol�gono para la delimitaci�n de la Zona Arqueol�gica y otro para el Entorno de Protecci�n� por lo que una vez ejecutado ser� interesado obtener dos capas poligonales con cada una de las entidades.

![](/images/blog/201510_visorategua/proceso.jpg)

Este manual forma parte del temario del [**curso� _on line_ �Sistemas de Informaci�n Geogr�fica y Arqueolog�a�**](http://www.almagre.es/cursos-formacion/curso-online-sistemas-de-informacion-geografica-qgis-y-arqueologia "Curso Almagre") organizado por Almagre. Para m�s informaci�n puede consultarse la p�gina del curso en la web del curso.
        