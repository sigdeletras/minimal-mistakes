---
title:  "Trabajando con datos LiDAR. Algunos ejemplos del Conjunto Arqueol�gico de Madinat al-Zahra"
categories: 
- blog
tags:
  - LiDAR
  - Arqueolog�a
  - Patrimonio
  - LAStools
---

El LiDAR (de light detection and ranging) es una t�cnica de teledetecci�n �ptica que utiliza la luz de l�ser para obtener una muestra densa de la superficie de la tierra produciendo mediciones exactas de x, y y z. LiDAR, que se utiliza principalmente en aplicaciones de representaci�n cartogr�fica l�ser a�reas, est� surgiendo como una alternativa rentable para las t�cnicas de topograf�a tradicionales como una fotogrametr�a. Cada punto LiDAR que es postprocesado puede tener una clasificaci�n que define el tipo de objeto que reflej� el pulso l�ser. Los puntos LiDAR se pueden clasificar en varias categor�as que incluyen suelo o terreno desnudo, parte superior de cubierta forestal y agua. (Fuente: [http://desktop.arcgis.com/](http://desktop.arcgis.com/es/arcmap/10.3/manage-data/las-dataset/what-is-lidar-data-.htm))

Esta fuente de datos tienen m�ltiples aplicaciones: modelos digitales del terreno y de superficies (con edificios y vegetaci�n), estudios de zonas inundables, detecci�n autom�tica de edificaciones nuevas, estudios de visibilidad y cobertura de antenas, inventarios forestales (cobertura arb�rea y de matorral, las alturas m�ximas de la vegetaci�n, la presencia de matorral o regeneraci�n avanzada), etc.

Gracias al [Plan Nacional de Ortograf�a A�rea](http://pnoa.ign.es/presentacion) contamos con cobertura de datos LiDAR para Espa�a (distintas fechas seg�n Comunidades Aut�nomas). Los datos LiDAR del PNOA tienen una una densidad de 0,5 puntos/m y una precisi�n altim�trica obtenida es mejor de 20 cm RMSE Z. Los datos se distribuyen a trav�s del [Centro de Descarga del CNIG](http://centrodedescargas.cnig.es/CentroDescargas/buscadorCatalogo.do?codFamilia=LIDAR) en ficheros digitales de 2x2 km de extensi�n. El formato de descarga es LAZ (formato de compresi�n de ficheros LAS).

![](/images/blog/cnig.png)

### LiDAR en Arqueolog�a

Los datos LiDAR est�n siendo usados de profusamente utilizados en el campo de la Arqueolog�a. La densidad de la cobertura y la posibilidad de poder obtener modelos digitales del terreno de detalle est�n dando magn�ficos resultados sobre todo en la detecci�n de estructuras de gran tama�o (murallas, zanjas, construcciones) en zonas de densa vegetaci�n. Los ejemplos son numerosos, pero pueden ilustrar bien este texto los trabajos del grupo de investigaci�n [Roman Army](http://romanarmy.eu/es/)� sobre arqueolog�a militar romana en el norte de Espa�a o el proyecto [Cambodian Archaeological Lidar Initiative (CALI)](http://angkorlidar.org/) que investiga la red de ciudades medievales del imperio Jemer sepultadas bajo la jungla en Camboya.

![](/images/blog/lidar_romana.png)

_Imagen: Jo�o Fonte e Luis Gon�alves 2016\. [O uso combinado de LiDAR, QGIS e LAStools aplicado ao estudo de paisagens arqueol�gicas](http://qgis.pt/apresentacoes_qgis2016/QGISPT-Fonte-Seco.pdf)._

### Algunos ejemplos para el Conjunto Arqueol�gico de Madinat al-Zahra

Mi inter�s por los datos LiDAR se centran, a d�a de hoy, m�s en las posibilidades que ofrece en �mbitos urbanos y su estudio desde el punto de vista geogr�fico. Este inter�s no ha impedido que,tras la reciente apertura de los datos LiDAR para Andaluc�a, haya realizado algunas pruebas con distintos software ([LAStools](https://rapidlasso.com/) de Martin Isenburg y [FrugoViewer](http://www.fugroviewer.com/)) espec�ficos y tambi�n con QGIS sobre algunos yacimientos emblem�ticos de la provincia de C�rdoba (Ategua, Torreparedones, Madinat al-Zahra, etc).

![](/images/blog/07_medina_lidar/pnoa.png)

_Localizaci�n del Conjunto Arqueol�gico de Madinat al-Zahra (C�rdoba) sobre WMS ortofotograf�al del PNOA � Instituto Geogr�fico Nacional de Espa�a)_

La imagen de m�s impacto es la obtenida para el �mbito de la [ciudad palatina de Madinat al-Zahra](https://es.wikipedia.org/wiki/Medina_Azahara). Los resultados no son nada novedosos ya que en la documentaci�n planim�trica del Plan Especial de Protecci�n del Conjunto ya exist�a un plano estructuras no excavadas� seguramente obtenidos a partir de alg�n tipo de prospecci�n geof�sica.

�![](/images/blog/07_medina_lidar/pepma.png)

_B2 - Estructura urbana de Madinat al-Zahra. Interpretaci�n de los restos no excavados. PEPMA (Fuente: [GMU C�rdoba](http://www.gmucordoba.es/planes-especiales))_

Junto a los restos visibles en la actualidad el mapa de sombras generado a partir de la nube de puntos filtrados (s�lo terreno) es bastante espectacular, pudi�ndose nuevas estructuras no documentas en el plano del PEPMA.

�![](/images/blog/07_medina_lidar/lidar_sombras.png)

Generaci�n del mapa de sombras con los datos filtrados no es definitiva. Podemos ir modificando los p�metros de altitud/azimut de la luz y factor del valor Z (exageraci�n vertical)� para obtener nuevos conjuntos de datos.

�![](/images/blog/07_medina_lidar/parametros.png)
        