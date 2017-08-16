---
title:  "C�mo usar m�dulos de Python en QGIS. Un ejemplo con dxf2gmlcatastro"
categories: 
- blog
tags:
- Catastro
- Python
- GDAL
- QGIS
---

Como he venido comentando en las dos �ltimas entradas, en el repositorio de GitHub de SIGdeletras pod�is encontrar el script [**dxf2gmlcatastro**](https://github.com/sigdeletras/dxf2gmlcatastro) permite transformar un archivo de parcela catastral CAD con extensi�n DXF al formato GML establecido por Catastro para conseguir su validaci�n gr�fica en la Sede Electr�nica del Catastro.

Tras verlo con algunos compa�eros, presentarlo en las �ltima reuni�n de [Geoinquietos C�rdoba](http://wiki.osgeo.org/wiki/Reuni%C3%B3n_11_Geoinquietos_C%C3%B3rdoba) y recibir varios correos de personas interesadas en usarlo, la conclusi�n a la que he llegado es la de que por muy �til que sea una herramienta **si la gente no sabe utilizarla ya se est� perdiendo el sentido b�sico que motiva su creaci�n.**

En esta l�nea, y poco despu�s de publicar el _script_, [�scar Mart�nez de M�squeSIG](https://twitter.com/masquesig?lang=es "Twitter de m�squesig") escribi� una estupenda entrada en la que explicaba [c�mo usar dxf2gmlcatastro en gvSIG](https://masquesig.com/2016/03/16/script-para-convertir-dxf-a-gml-con-gvsig-2-3-gracias-a-sigdeletras/). Siguiendo las reflexiones de �scar, podemos decir que integrar c�digo en un SIG como gvSIG, o en nuestro caso [QGIS](http://www.qgis.org/en/site/), permite:

*   Al poder integrar el c�digo en un SIG que trabaja con Python y GDAL, el uso inicial de la librer�a es m�s f�cil.
*   No estamos limitados a la instalaci�n en un [sistema operativo concreto](2016/instalacion-de-python-y-gdal-en-windows) ya tanto gvSIG como QGIS son SIG multiplataforma.
*   Podemos mejorarlo usando las funcionalidades que nos ofrece el propio SIG (cuadros de dialogo, interfaz visual...).
*   Se podr�a integrar en la barra de herramientas o incluso convertirlo en una extensi�n.

En conclusi�n y como dice �scar �**�que pueda llegar a m�s gente, que al final es para lo que lo hacemos�.**

## Definir la variable PYTHONPATH

La variable PYTHONPATH es utilizada en QGIS para acceder a los m�dulos de Python. Esta variable ya se define durante la instalaci�n apuntando a una carpeta denominada Python dentro del directorio de instalaci�n del programa, o en la carpeta _.qgis2_ en Linux. A pesar de ello, vamos a a�adir una ruta nueva m�s accesible donde vamos a guardar nuestro m�dulo.

Los pasos a seguir son los siguientes:

*   Abrir QGIS.
*   Ir al men� _Configuraci�n>Opciones.
*   En la pesta�a _Sistema_, buscamos el apartado _Entorno._
*   Activamos la opci�n _�Usar variables personalizadas��
*   Pinchamos en el bot�n _�A�adir�_ y definimos la variable con las siguientes opciones:
    *   Aplicar: �Poner a continuaci�n�
    *   Variable: PYTHONPATH
    *   Valor: Carpeta donde vamos a guardar nuestros archivos Python (ej. C:\scriptsqgis)
*   Pinchamos en _Aceptar_ y reiniciamos QGIS.

 ![](/images//blog/05_importarmodulo/01_pythonpath.png)

## Usar dxf2gmlcatastro en QGIS.

Lo primero que debemos hacer es descarga el c�digo, o hacer un _git clone, _ de dxf2gmlcatastro desde el [repositorio de GitHub](https://github.com/sigdeletras/dxf2gmlcatastro) y copiar los archivos en la carpeta definida en PYTHONPATH (ej. C:\scriptsQGIS).

![](/images//blog/05_importarmodulo/02_1_github.png)

Lo primero es comprobar que QGIS accede a la nueva ruta que hemos a�adido a PYTHONPATH. Una vez ejecutado de nuevo QGIS,  vamos a abrir la consola de Python integrada (_Complementos > Consola de Python)_ y escribimos _import dxf2gmlcatastro_ y despu�s pulsamos "Intro". Si hemos seguido correctamente los pasos anteriores no nos deber�a devolver ning�n error.

![](/images//blog/05_importarmodulo/02_consola.png)

A continuaci�n vamos a ejecutar la funci�n _crea_gml_ de dxf2gmlcatastro que convertir� nuestro archivo DXF al GML de Catastro. Dentro de la funci�n tendremos de a�adir los argumentos que nos indiquen:

*   D�nde se encuentra el archivo DXF (ej. 'C:\carpeta\archivoparcela.dxf')
*   El lugar y el nombre del GML(ej. 'C:\carpeta\gmlcatastro.gml')
*   El c�digo EPSG del Sistema de Referencia de Coordenadas del DXF. (Los SRC admitidos son 25828, 25829, 25830 y 25831)

```
dxf2gmlcatastro.crea_gml('C:\carpeta\archivoparcela.dxf', 'C:\carpeta\gmlcatastro.gml', '25830')

```

Si todo ha ido correcto podemos cargar el nuevo GML en QGIS y comprobar que se ha generado correctamente y que incluye los atributos seg�n el modelo de Inspire.

![](/images//blog/05_importarmodulo/04_qgis.png)

## Crear un script con PyQGIS personalizado

Una vez que disponemos de _dxf2gmlcatastro_ podemos crear otros fragmentos de c�digo para integrarlo en QGIS. Aqu� os dejo un ejemplo que carga el GML en QGIS.

Para crear este archivo hemos usado el editor de c�digo de QGIS y una vez terminado lo hemos salvado en nuestro equipo con el nombre _catastroQGIS.py_. S�lo deberemos cargar el archivo en el terminal de Python de QGIS y cambiar la ruta y nombre de los archivos para utilizarlo cada vez que queramos.

![](/images//blog/05_importarmodulo/03_pyqgis.png)
El archivo _catastroQGIS.py_ se encuentra en la [carpeta _ejemplo_ del repositorio GitHub](https://github.com/sigdeletras/dxf2gmlcatastro/blob/master/ejemplo/catastroqgis.py "Ejemplo para QGIS")
        