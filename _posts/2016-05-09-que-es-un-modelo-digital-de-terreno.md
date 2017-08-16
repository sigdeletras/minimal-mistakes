---
title:  "Qu� es un Modelo Digital de Terreno"
categories: 
- blog
tags:
- QGIS
- Sistemas de Informaci�n Geogr�fica
- Arqueologia
- MDT
---

Un **_Modelo Digital de Terreno (MDT)_** es una estructura num�rica de datos que representa la distribuci�n espacial de una variable cuantitativa y continua. El tipo de MDT m�s conocido es el **Modelo Digital de Elevaciones (MDE)**, un caso particular de aquel, en el que la variable representada es la cota del terreno en relaci�n a un sistema de referencia concreto (Fuente:[Wikipedia](https://es.wikipedia.org/wiki/Modelo_digital_del_terreno)).

Su campo uso es muy variado:

*   Extracci�n de los par�metros del terreno.
*   Trazados de perfiles topogr�ficos.
*   Creaci�n de mapas en relieve.
*   Tratamiento de visualizaciones en 3D.
*   Planificaci�n de vuelos en 3D.
*   Creaci�n de modelos f�sicos (incluyendo creaci�n de mapas de relieve).
*   Rectificaci�n geom�trica de fotograf�as a�reas o de im�genes sat�lites.
*   Los an�lisis del terreno en geomorfolog�a y geograf�a f�sica.
*   Apoyo en an�lisis estad�sticos (precipitaci�n, insolaci�n-temperatura, flujos h�dricos, erosi�n, distribuci�n de h�bitats, etc.)
*   Modelos clim�ticos (sombras, incidencias del sol, umbr�as)
*   Modelos hidrol�gicos (l�neas de flujo,�reas subsidiarias, caudales)
*   An�lisis visual

Para trabajos localizados en Espa�a, la fuente fundamental de Modelos Digitales de Elevaci�n es el **Instituto Geogr�fico Naciona**l. Sus Modelos Digitales del Terreno se obtienen mediante interpolaci�n de modelos digitales del terreno de 5 metros de paso de malla procedentes del Plan Nacional de Ortofotograf�a A�rea (PNOA). La **descarga de los datos** se realiza a trav�s de la direcci�n [http://centrodedescargas.cnig.es/CentroDescargas/](http://centrodedescargas.cnig.es/CentroDescargas/)

 ![MDT de descarga en la web del CNIG](/images/blog/05_mde/mde_cnig.png "MDT de descarga en la web del CNIG")

<span style="font-size: small;">_MDT disponibles para descarga en la web del CNIG_</span>

Los Sistemas de Informaci�n Geogr�fica como **QGIS** incorporan un conjunto de herramientas que permiten realizar procesos de conversi�n, tratamiento y an�lisis de MDE. Entre las operaciones m�s frecuentes se encuentran:

*   Obtenci�n de **curvas de nive**l en formato vectorial y si lo deseamos exportar estos datos a formato DXF para su trabajo con CAD.
*   Generaci�n de p**erfiles longitudinales.**
*   **Visualizaci�n 3D**.
*   Generaci�n de **mapas de sombras** que nos ayuden a una mejor comprensi�n de la topograf�a y el relieve existente sin la necesidad - de acudir a un mapa topogr�fico.
*   Mapas de **orientaci�n**
*   Obtenci�n de **mapas de pendientes** que son extensamente usados en trabajos de an�lisis arqueol�gico del territorio, sobre todo - como parte de c�lculos de an�lisis de visibilidad, costo de desplazamiento o caminos �ptimos.
*   La **reclasificaci�n** es una operaci�n matem�tica sobre archivos raster que permite generar nuevos valores a partir de determinados criterios y operaciones. Por ejemplo, al generar un mapa de pendientes en porcentajes tendremos para cada celda un valor comprendido entre 0 y 100.

![](/images/blog/05_mde/pendientes.png)

 <span style="font-size: small;">_Ejemplo de mapa usos posibles de suelo seg�n pendiente_</span>

En el Curso online [�Sistemas de Informaci�n Geogr�fica y Arqueolog�a"](http://www.almagre.es/cursos-formacion/curso-online-sistemas-de-informacion-geografica-qgis-y-arqueologia) se tratar� con m�s amplitud las posibilidades que los MDT tienen en el campo de los an�lisis de territorio pasados y se obtendr�n los conocimientos para el manejo de esta relevante fuente de informaci�n geogr�fica con el Sistema de Informaci�n Geogr�fica QGIS.        