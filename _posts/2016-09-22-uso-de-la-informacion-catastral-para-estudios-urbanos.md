---
title:  "Uso de la informaci�n catastral para estudios urbanos"
header:
	teaser:
categories: 
- blog
tags:
- catastro
- sig
- estudios urbanos
---

La cartograf�a catastral constituye uno de los conjuntos de datos de m�s uso en los Sistemas de Informaci�n Geogr�fica. A pesar de estar dentro de la categor�a de cartograf�a tem�tica ([Real Decreto 1545/2007](%20https:/www.boe.es/diario_boe/txt.php?id=BOE-A-2007-20556) ), su nivel de precisi�n (entre 1:500 y 1:5.000), la cobertura a escala nacional (salvo Pa�s Vasco y Navarra), la posibilidad de descarga mediante certificado, a trav�s de la [Sede Electr�nica de Catastro](http://www.sedecatastro.gob.es/) y las [caracter�sticas de la licencia de uso](http://www.catastro.meh.es/documentos/resoluciondgc20110323_tfs.pdf) , hace que muchos sistemas cartogr�ficos, sobre todo de �mbito local, la est�n utilizando como informaci�n topogr�fica de referencia.

De forma sencilla podemos definir la informaci�n catastral como aquella que recoge la descripci�n parcelaria o superficial de los bienes inmuebles. Para un descripci�n m�s detallada podemos usar la la siguiente� descripci�n de Sereno (2009) que se aplica al catastro en Espa�a:

_"Catastro Inmobiliario es un registro administrativo dependiente del Ministerio de Econom�a y Hacienda en el que se describen los bienes inmuebles r�sticos, urbanos y de caracter�sticas especiales. La descripci�n catastral de los bienes inmuebles contenida en el Catastro Inmobiliario comprende sus caracter�sticas f�sicas, econ�micas y jur�dicas, entre las que se encuentra la localizaci�n y la referencia catastral, la superficie, el uso o destino, la clase de cultivo o aprovecha- miento, la calidad de las construcciones, la representaci�n gr�fica, el valor catastral y el titular catastral."_  

Queda patente el gran inter�s que genera la informaci�n catastral, sobre todo para su reutilizaci�n en el sector productivo, generando nuevas oportunidades de negocio, con un coste muy bajo para el usuario y un alto grado de actualizaci�n y exhaustividad. El conocimiento de la estructura de datos catastrales debe generar nuevas v�as de trabajo para las administraciones y en la investigaci�n territorial y urbana.� Pero pese a las posibilidades y libertad de acceso, la informaci�n catastral tiene� poco uso m�s all� de ser usada como cartograf�a base. La principal raz�n de estos se debe a la dificultad t�cnica existente para explotar los datos, ya que requieren de ciertos conocimientos sobre la estructura de los datos catastrales y conocer qu� informaci�n se puede extraer de ellos.

[![Superficie de la finca](https://c3.staticflickr.com/6/5284/29558797250_a061c8db66.jpg)](https://www.flickr.com/photos/115384326@N07/29558797250/in/dateposted-public/)

### Servicio de descarga

A trav�s de la [Sede Electr�nica de la Direcci�n General del Catastro](https://www.sedecatastro.gob.es/OVCFrames.aspx?TIPO=TIT), se puede hacer una descarga masiva de los datos catastrales no protegidos (todos salvo titularidad de inmuebles y valor catastral), tanto de la cartograf�a vectorial (en formato Shapefile) como de la informaci�n alfanum�rica.� Para ello es necesario disponer de un certificado digital que permita autentificar frente a Catastro al usuario que solicita los datos. La informaci�n corresponde a municipios completos, en funci�n de si es informaci�n de suelo urbano o r�stico, con y sin historia. Estos datos se publican tres veces al a�o, a primeros de febrero, de junio y de octubre. Desde este [enlace](http://www.catastro.meh.es/ayuda/manual_descargas_shapefile.pdf) puede consultarse una gu�a de descarga redactada por la SEC.

La informaci�n cartogr�fica catastral se divide en urbana y r�stica, para cada una de ellas se ha utilizado una escala de captura diferente. En el caso de la cartograf�a urbana la escala de captura est� entre 1:500 y 1:1.000, y para la cartograf�a r�stica entre 1:2.000 y 1:5.000.� Para la pen�nsula y Baleares se utiliza un sistema de coordenadas proyectado, con el datum local ETRS89, y un sistema de representaci�n cartogr�fico (o sistema de proyecci�n) Universal Transversa Mercator (UTM), husos 29, 30 y 31\. Para Canarias se utiliza el datum global WGS84 y sistema de proyecci�n UTM, husos 27 y 28.

El parcelario catastral se representa mediante cuatro geometr�as principales MASA, PARCELA, SUBPARCE y CONSTRU. El resto de geometr�as son auxiliares o contienen otros elementos cartogr�ficos, como mobiliario urbano, l�mites administrativos, r�tulos con los nombres de las calles, etc.

### Datos alfanum�ricos catastrales

La cartograf�a catastral en formato SIG constituye la base a la que se asocia multitud de informaci�n alfanum�rica descriptiva, tanto del suelo como de las construcciones. De esta forma, la plena identificaci�n catastral se completa con la suma de informaci�n cartogr�fica e informaci�n alfanum�rica.

[![Superfice contruida](https://c7.staticflickr.com/9/8324/29738357462_b5a5d141f2.jpg)](https://www.flickr.com/photos/115384326@N07/29738357462/in/dateposted-public/)

La descarga sigue los mismos mecanismos descritos obteni�ndose la informaci�n en un fichero CAT.� El fichero .CAT est� formado por texto plano tipo ASCII, donde cada registro (fila) tiene una longitud fija de 1.000 caracteres. Se descarga como un archivo comprimido en formato GZIP (extensi�n .gz). El archivo est� formada por registros de varios tipos:

*   Tipo 01 y 90: Registro de cabecera y de cola. Los registros tipo 01 y 90 son accesorios ya que aportan datos sobre la fecha de los datos y el n�mero de l�neas que tiene cada registro tipo.
*   Tipo 11: Registro de Finca. Identifica y localiza a la parcela catastral.� De esta tabla podemos obtener principalmente datos de superficie: finca, construida, bajo rasante y cubierta� Existir� uno por cada parcela catastral implicada.
*   Tipo 13: Registro de Unidad Constructiva. Representa un edificio o un conjunto de construcciones particularizadas dentro de un edificio� Existir� uno por cada unidad constructiva en cada parcela catastral.
*   Tipo 14: Registro de Construcci�n. Identifica cada uno de los locales existentes en un bien inmueble, con su descripci�n f�sica: superficie, antig�edad o tipolog�a. Existir� uno por cada construcci�n de cada unidad constructiva en cada parcela catastral
*   Tipo 15: Registro de Inmueble. Identifica cada uno de los bienes inmuebles dentro de una parcela catastral. Existir� uno por cada bien inmueble en cada parcela catastral
*   Tipo 16: Registro de reparto de elementos comunes. Identifica el elemento constructivo cuyo valor se reparte entre los dem�s elementos de construcci�n. Existir� al menos uno por cada elemento com�n que se reparte, siempre que sea necesario especificar repartos especiales.
*   Tipo 17: Registro de cultivos. Identifica cada subparcela de cultivo existente dentro de la parcela catastral. Existir� uno por cada subparcela de cultivo existente dentro de la parcela catastral.

Los datos pueden ser transformados a formato tabular o importarlos a una base de datos en la que se replique la estructura de datos y se establezcan las correspondientes relaciones. Esto permitir� realizar operaciones estad�sticas b�sicas como sumatorios, medias, m�ximas, m�nimas o agrupaciones. Ya que nuestra finalidad es explotar los datos desde un punto de vista territorial es interesante a�adir los datos alfanum�ricos a una base con capacidades espaciales como puede ser PostgreSQL-Postgis.

### Usos

Actualmente, la informaci�n catastral constituye una informaci�n geogr�fica de referencia fundamental para una gran n�mero de aplicaciones y sistemas de gesti�n de informaci�n geogr�fica tem�tica, empezando por su aplicaci�n m�s directa en la gesti�n de determinados impuestos, tanto estatales como auton�micos y locales, y siguiendo en aplicaciones m�s indirectas, como la gesti�n de usos y aplicaciones agrarias, el control y gesti�n de la ocupaci�n del suelo, la gesti�n de la propiedad inmobiliaria, la gesti�n del patrimonio inmobiliario, la gesti�n del planeamiento o de obras, etc. (Sereno, 2009).

Tras el tratamiento correspondiente de los datos y su inclusi�n en un Sistema de Informaci�n Geogr�fica, podemos decir que contamos con un conjunto de datos de gran utilidad para estudios territoriales y urbanos.� Una primera explotaci�n centrada en los datos geom�tricos nos podr�a dar **informaci�n de tipo f�sico**, dimensiones y formas las de parcelas o superficies de solar, sobre el parcelario catastral.

Al contar con la fecha de construcci�n/remodelaci�n podemos obtener resultados que trabajen con la **variable temporal** analizando la antig�edad de edificios� que reflejan los momentos de comienzo y finalizaci�n en la construcci�n de los edificios que integran cada parcela.

[![Antiguedad](https://c3.staticflickr.com/6/5208/29558795610_fc2de0c68f.jpg)](https://www.flickr.com/photos/115384326@N07/29558795610/in/dateposted-public/)

Con la informaci�n que de los c�digos de uso (UCM) se puede extraer, de manera selectiva para cada parcela,� los **usos del suelo**. A partir de estas capas pueden realizarse incluso trabajos de geomarketing vinculados por ejemplo a la identificaci�n de usos prioritarios por vial o calle.

Para el� **planeamiento urban�stico**, los datos catastrales puede ser utilizados para el an�lisis de alturas m�ximas de edificaci�n o la identificaci�n de parcelas sobre sobreedificadas o subedificas a partir de la superficie y volumen construido. Igualmente podemos generar un mapa con el inventario del suelo disponible o de tipolog�as edificatorias/constructivas.

[![N�mero de usos por parcela](https://c1.staticflickr.com/9/8316/29738356552_18183fcfb7.jpg)](https://www.flickr.com/photos/115384326@N07/29738356552/in/dateposted-public/)

En el �mbito de la **Demograf�a**, si no disponemos acceso directo al padr�n de habitantes, podemos seguir distintas metodolog�as para trasvasar de poblaci�n desde las unidades censales a las parcelas catastrales. como la desarrollada por Santos Preciado (2015)� desarrolla esta metodolog�a que permite el c�lculo demogr�fico de forma proporcional seg�n el peso del n�mero de viviendas o de la superficie residencial construida en cada una de ellas.

Esta entrada es un ejemplo de los **servicios que desde SIGdeletras podemos ofrecer como consultar�a especializada en Tecnolog�as de Informaci�n Geogr�fica con especial atenci�n a trabajos para administraciones locales**. Para cualquier duda o consulta sobre �ste o cualquier otro tipo de servicios se puede mandar un correo a la direcci�n **hola[arroba]sigdeletras.com.**

### Bibliograf�a utilizada

*   COCERO MATESANZ et al. (2014): �La cartograf�a catastral y su utilizaci�n en los estudios urbanos, en un entorno SIG. Aplicaci�n al an�lisis del municipio madrile�o de Getafe�. X_VI Congreso de Tecnolog�as de la Informaci�n Geogr�fica_. pp 648-662
*   CONEJO-FERN�NDEZ, C. y VIRG�S-SORIANO, L.I. (2001): �SIGCA 2 Cartograf�a catastral digital, disponible para todos�. _Catastro,_ 43, pp. 73-92.
*   DIRECCI�N GENERAL DEL CATASTRO. (2011): _Fichero inform�tico de remisi�n de catastro (bienes inmuebles urbanos, r�sticos y de caracter�sticas especiales)._ 18 p. Obtenido de http://www.catastro.minhap.es/documentos/formatos_intercambio/catastro_fin_cat_2006.pdf
*   DIRECCI�N GENERAL DEL CATASTRO. (2014): _Modelo de datos de cartograf�a vectorial (formato shapefile)._ 25 p. Obtenido de http://www.catastro.meh.es/ayuda/manual_descriptivo_shapefile.pdf
*   MORA-GARC�A, R.T. et al. (2015): �Reutilizaci�n de datos catastrales para estudios urbanos� en DE LA RIVA, J., IBARRA, P., MONTORIO, R., RODRIGUES, M. (Eds.) 2015 A_n�lisis espacial y representaci�n geogr�fica: innovaci�n y aplicaci�n_. pp. 295-304
*   SANTOS PRECIADO, J.M. (2015): �La cartograf�a catastral y su utilizaci�n en la desagregaci�n de la poblaci�n. Aplicaci�n al an�lisis de la distribuci�n espacial de la poblaci�n en el municipio de Legan�s (Madrid)�. _Estudios Geogr�ficos. Vol. LXXV,I 278_, pp. 309-333
*   <span style="font-weight: normal;">SERENO �LVAREZ, A. (2009):</span> �La informaci�n geogr�fica en Espa�a: especial referencia a la cartograf�a catastral�. _Catastro_ 67, pp. 31-54.