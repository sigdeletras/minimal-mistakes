---
title:  "SIG en la nube. Creando una capa a partir de un listado con coordenadas con GeoWE"
header:
	teaser: ""
categories: 
	- blog
tags:
	- GeoWE
	- Formatos geogr�ficos
	- CSV
	- SIG
	- webmapping
---

Gracias a los comentarios y aportes de la comunidad� y el buen hacer de los desarrolladores del proyecto, **[GeoWE](http://geowe.org/)** va incorporando a sus funcionalidades herramientas que hace cada vez m�s sencillo realizar operaciones SIG en la nube. Aunque ya estaba disponible la carga de ficheros CSV con la informaci�n geogr�fica en formato WKT, en la versi�n Beta 1.3.8 se ha a�adido la posibilidad de **cargar CSV pero con las coordenadas en columnas X e Y**. Esta mejora resuelve� un issue que puse en el [repositorio GitHub de GeoWE](https://github.com/geowe/geowe-core/issues/238). Es un buen ejemplo del flujo din�mico de trabajo que mantienen sus creadores.

Esta nueva mejora puede servir para cargar capas de puntos o v�rtices de trabajos topogr�ficos. Puede� usarse igualmente para visualizar sobre una cartograf�a base los listados de coordenadas de ubicaci�n o delimitaci�n publicados en boletines o documentos oficiales.

### Un ejemplo: Localizaci�n de mojones de deslinde

El siguiente [enlace al Bolet�n Oficial del Estado](https://www.boe.es/diario_boe/txt.php?id=BOE-A-2016-5377) recoge una Orden por la que se aprueba el deslinde entre los t�rminos municipales de Mendavia (Navarra) y Arr�bal (La Rioja). El documento a�ade al final una relaci�n de coordenadas en el sistema geod�sico de referencia ETRS89, proyecci�n UTM huso 30, de las posiciones de los mojones del Acta.

Antes de poder ver cargar la informaci�n en GeoWE, el **primer paso es convertir este listado a formato CSV**. Hemos copiado la tabla a una hoja de c�lculo, ordenandos las columnas para que los datos X e Y queden al final y reemplazando de forma masiva el s�mbolo decimal de coma a punto. Para terminar salvamos en formato CSV (deslinde.csv) delimitado por punto y coma. En los comentarios de issue pod�is ver un ejemplo del modelo a seguir.

![Conversi�n de datos](/images/blog/12_geowe_csv/datos.png)

_Conversi�n de tabla en PDF a archivo CSV_

Para representar los datos, abrimos GeoWE y accedemos a _Men�>Capa>A�adir_. Una vez abierto el di�logo. pincharemos **en la pesta�a "Archivo" cargaremos desde local el archivo CSV** (deslinde.csv). Antes de cargar, indicaremos el nombre de la capa, por ejemplo "Deslinde", el sistema de referencia EPGS:25830 (ETRS89 UTM30N) y el formato CSV. Tras hacer clic en "Aceptar", GeoWE nos presentar� el resultado de la capa, representando de forma puntual cada coordenada de nuestro listado.

![Carga de archivo CSV](/images/blog/12_geowe_csv/geowe_puntos.png)

_Carga de archivo CSV en GeoWE_

### Creaci�n de l�nea de deslinde con _snapping_

Gracias a las herramientas de GeoWE podemos algo m�s all�. Imaginemos que queremos crear una capa lineal a partir de los puntos cargados y que los v�rtices de la capa deben coincidir exactamente con los de a Orden.

En primer lugar, crearemos una capa vectorial vac�a desde _Men�>Capa>A�adir._� Indicaremos el nombre de la nueva capa por ejemplo "Deslinde_lin" y el SRC. Generada la capa y para trabajar con precisi�n, activaremos la herramienta "_Snapping"_ que se encuentra el men� _"Capa"_. Para empezar a dibujar nuestro trazado, usaremos desde el men� _"Dibujo"_ la opci�n _"L�nea"_ y acercaremos el curso a cada uno de los puntos hasta que veamos que se acerca autom�ticamente �l e iremos dibujan la l�nea.

�![Creaci�n de capa lineal con snapping](/images/blog/12_geowe_csv/geowe_lin.png)

_Generaci�n de capa lineal con la herramienta Snapping_

Generada la l�nea del l�mite, podemos salvar los resultados en distintos formatos geogr�ficos est�ndares en nuestro ordenador en local o repositorio GitHub desde la herramienta de _�Exportar datos�_ del Administrador de capas.

### An�lisis espacial. Parcelas afectadas

GeoWE a�ade en su versi�n Beta algunas operaciones de an�lisis. Entre ellas podemos encontrar la opci�n de **�rea de influencia o buffer**. Podr�amos usar este geoproceso para identificar las parcelas catastrales afectadas por este nuevo deslinde. Si fu�ramos los t�cnicos municipales de los ayuntamientos afectados usar�amos dicha referencia para comunicarla a los afectados, pasar la incidencia a Catastro y actualizar nuestro SIG Municipal.

Desde el men� _Capa>An�lisis_ seleccionamos la opci�n _"Buffer"_, a�adimos la distancia de 100 metros e indicamos que se calcule la influencia sobre la capa "Deslinde_lin"  

Si a**�adimos el servicio WMS de� Catastro desde el cat�logo de GeoWE**, podemos comprobar que las parcelas afectadas por el nuevo deslinde se sit�an al sureste. Para poder obtener la referencia catastral, marcaremos como activa la capa de catastro desde el _�Administrador de capas�_ y activaremos la herramienta _"WMS info"_ para obtenerla [informaci�n catastral](https://www1.sedecatastro.gob.es/CYCBienInmueble/OVCConCiud.aspx?del=26&mun=19&UrbRus=R&RefC=26019A001004280000DX&Apenom=&esBice=&RCBice1=&RCBice2=&DenoBice=.) pinchando dentro de la parcela.

C![Consulta de Parcela Catastral](/images/blog/12_geowe_csv/geowe_catastro.png)

_Consulta de informaci�n Catastral desde WMS_

### Pon un SIG Web en tu vida

Con una conexi�n de Internet, sin necesidad de instalar y configurar� en mi equipo ning�n SIG, y a partir de un listado de coordenadas en PDF he podido realizar un trabajo t�cnico de una complejidad media. Poco a poco iremos viendo, que **a igual que otros flujos de trabajo se est�n ya realizando en la nube (ej. Google Drive), con herramientas como GeoWE este tipo de procedimientos SIG seguir�n este mismo camino.**  

PD: ... que alguien le indique a Catastro que no ha actualizado en su servicio de mapas los nuevos l�mites municipales entre los t�rminos Mendavia y Arr�bal ;-)
        