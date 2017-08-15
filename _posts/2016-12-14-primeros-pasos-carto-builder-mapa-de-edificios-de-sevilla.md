---
title:  "Primeros pasos CARTO Builder. Mapa de edificios de Sevilla"
header:
  teaser: ""
categories: 
	- blog
tags:
	- carto
	- cartodb
	- carto builder
	- catastro
	- inspire
	- sevilla
	- edificios
---

        
Hace tiempo que ten�a pendiente probar **Builder,** la nueva herramienta de [CARTO.](https://carto.com/ "Carto Web") Junto a una gran cantidad de cambios en la interfaz y en el flujo de trabajo, a los que habr� que ir poco a poco acostumbr�ndose, existen dos novedades que hacen de Carto la empresa m�s potente a d�a de hoy� que aplicada el modelo _SaaS_ al �mbito de los �mapas�. La primera novedad es la� la incorporaci�n de asistentes para la realizaci�n de an�lisis espaciales y la segunda la posibilidad de a�adir a nuestros mapas� aplicaciones o complementos (_widgets_) basados en los datos disponibles.

En el antiguo [_Editor_](https://carto.com/docs/carto-editor/ "Carto Editor") podr�an realizar mediante consultas SQL y funciones espaciales gran cantidad de an�lisis derivados de nuestros datos geogr�ficos. Toda esta potencialidad es ahora bastante m�s accesible con [**Builder**](https://carto.com/builder/ "Carto Builder"). Gracias a un conjunto de asistentes gr�ficos, el usuario puede crear de forma r�pida complejos procesos espaciales como identificar lugar central, generaci�n de l�neas a partir de puntos, �reas de influencia, filtrado, an�lisis cluster... Para m�s informaci�n sobre estos procesos puede consultarse las [gu�as en la web](https://carto.com/learn/guides "Carto Guides") de CARTO.

![Asistentes an�lisis Carto](/images/blog/12_builder/analisis.png "Asistentes an�lisis Carto")

_Asistentes de an�lisis CARTO_

Con la incorporaci�n de� _widget_� a nuestro mapa, podemos a�adir valor a la representaci�n gr�fica de la informaci�n.� La visualizaci�n de datos estad�sticos� o gr�ficos mejora� la compresi�n de los mapas y pueden ayudar a identificar nuevos puntos de vista. Estos complementos� permiten por ejemplo, a�adir datos estad�sticos como totales, valores medios, m�ximos o porcentajes. Tambi�n� pueden usarse para presentar agrupaciones� o categor�as de datos por campos y mostrarlos� infograf�as interactivas o histogramas de series temporales.

![](/images/blog/12_builder/widgets.png)

_Ejemplos de widgets_

### Edificios de Sevilla

Como ejemplo del potencial del nuevo _dashboard_ he realizado un [**mapa de los Edificios de la ciudad de Sevilla (Espa�a)**](https://sigdeletras.carto.com/builder/55db719a-bdf4-11e6-ae20-0e05a8b3e3d7/embed "Mapa Edificios de Sevilla"). Estos datos proceden de los [servicios Inspire de Cartograf�a Catastral](%20http:/www.catastro.minhap.gob.es/webinspire/index.html "Catasttro Inspire") de la Direcci�n General de Catastro. En concreto de la capa edificios (_BU buildings_)

![Visor Carto de Edificios de Sevilla](/images/blog/12_builder/mapa.png "Visor Carto de Edificios de Sevilla")

_Click_ en la imagen para acceder al mapa ["Edificios de Sevilla"](https://sigdeletras.carto.com/builder/55db719a-bdf4-11e6-ae20-0e05a8b3e3d7/embed "Carto Mapa Edificios de Sevilla")

La representaci�n y datos sobre los edificios es gran **utilidad en el �mbito de lo p�blico** ya que permite conocer los par�metros urban�sticos de las ciudades, realizar investigaciones sobre crecimiento o estudios prospectivos. De igual manera, el conocimiento del parque edificado es fundamental para trabajos de sostenibilidad urbana vinculados con la ocupaci�n del suelo o los usos e intensidades edificatorias. En el **sector privado** estos datos est�n siendo explotados desde el punto de vista� inmobiliario y en geomarketing. Para m�s informaci�n sobre las posibilidades de la informaci�n Catastral pueden consultarse esta [entrada en el blog](http://sigdeletras.com/2016/uso-de-la-informacion-catastral-para-estudios-urbanos "Uso de la informaci�n catastral para estudios urbanos ").

Antes de subir el conjunto de datos a CARTO, el gran volumen de informaci�n descargada fue almacenada en una base de datos geogr�fica PostgreSQL-Postgis. La causa de este trabajo previo se ha ha debido a dos razones. En primer lugar, debemos de tener en cuenta el tipo [cuenta o plan](https://carto.com/pricing/ "Carto accounts") que disponemos en CARTO, que entre otras cuestiones definir� el volumen de megas disponibles. La segunda raz�n es la de poder disponer en local (SIG) de nuestros datos. Gracias a esto podremos realizar determinadas operaciones SIG de filtrado, transformaci�n y enriquecimiento con otros recursos antes de subir los datos a la web. Por ejemplo, para este ejemplo han sido seleccionados solo algunos atributos de la capa de edificios� y se le ha a�adido mediante una vista la [delimitaci�n de los barrios de Sevilla](http://www.juntadeandalucia.es/institutodeestadisticaycartografia./DERA/index.htm "Barrios DERA IECA") ofrecida por el IECA.

Tras subir nuestros datos en CARTO, contamos en primer lugar con un mapa con la representaci�n de los datos geogr�ficos de los edificios del municipio de Sevilla. Para cada edificio puede consultarse la informaci�n suministrada por Catastro (referencia, imagen, uso dominante, �rea, n�mero de viviendas�) y datos del distrito y barrio. Podemos personalizar la ventana de datos con un poco de c�digo HTML que permita� por ejemplo para a�adir un enlace a Catastro o la imagen de fachada.

![Ventana de datos asociados al Edificio](/images/blog/12_builder/ventana.png)

_Ventana HTML de datos asociados al Edificio_

Utilizando los widgets de CARTO Builder he a�adido la siguiente informaci�n complementaria:

*   **N� de edificios:** Calcula el total de edificios representados en del mapa. Al hacer zum se recalcula el total seg�n el �rea de visualizaci�n.
*   **Edificios por barrio:** Permite filtrar el conjunto de edificios por barrios.
*   **Uso dominante:** La capa catastral adjunta el uso dominante del edificio incluyendo las categor�as Vivienda, Industrial, Comercial, Agricultura, Oficinas y Edificios p�blicos.� El valor se obtiene calculando el uso� que mayor superficie tenga de todos los inmuebles de la parcela catastral donde est� el edificio.
*   **Fecha de construcci�n:** En el modelo de Inspire esta fecha se define por los atributos _beginning y end_. Para nuestra aplicaci�n ha sido cargada exclusivamente la m�s antigua y presentada en un histograma.� Este _widget_ es tambi�n din�mico ya que se puede acotar la serie temporal mediante fechas de inicio y final.

![Filtro de edificios de uso dominate de tipo comercial del barrio de El Arenal (Sevilla)](/images/blog/12_builder/uso_comercial_arenal.png "Filtro de edificios de uso dominate de tipo comercial del barrio de El Arenal (Sevilla)")

_Filtro de edificios de uso dominante de tipo comercial del barrio de El Arenal (Sevilla)_

### Conclusiones

Con la nueva plataforma de Carto queda reflejada a la perfecci�n el [nuevo rumbo que ha tomado la empresa](http://www.abc.es/tecnologia/informatica/software/abci-nuevo-golpe-cartodb-pasa-carto-y-apuesta-retorcer-mapas-interactivos-201607071529_noticia.html "Noticia ABC"). Los nuevos desarrollos est�n enfocados en permitir al usuario ahondar m�s en la informaci�n y datos presentados en los mapas y que a partir de estos� pueda realizar nuevas preguntas, obtener� conclusiones y tomar decisiones.

Si est�is interesados sobre el desarrollo de este trabajo o ver las posibilidades en vuestras entidades no dud�is en contactar conmigo a trav�s del correo **hola[arroba]sigdeletras.com**.
        