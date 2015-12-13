---
layout: post
title:  "Segunda entrega Proyecto de Configuración de Variables de Entorno"
date:   2015-12-14 17:00:00
author: Teófilo - Hernán
categories: Development_Project
github: https://github.com/hsarmiento/rqt_env
---

#Problema

A grandes rasgos, al realizar modificaciones de variables de entorno para ROS, éstas se deben efectuar sobre el archivo `.bashrc`. Sin embargo, al efectuar esta tarea pueden existir errores humanos al modificar variables de otros software o tener diversas líneas comentadas para distintas configuraciones, las cuales deben ser descomentadas para ser utilizadas. Para obtener más información al respecto, visitar propuesta de proyecto `rqt_env` en el siguiente link: [Proyecto de Configuración de Variables de Entorno](http://hsarmiento.github.io/htrob/planning_project/2015/10/26/project.html)

#Solución

La solución denominada `rqt_env`, consiste en desarrollar una GUI utilizando paquetes de RQT-PACKAGE propios de ROS. `rqt_env`, permitirá realizar configuración de la variables de entorno tanto de ROS y de los robots de forma independiente. Esta solución también tendrá diferentes configuraciones de robots guardadas,  con lo que se eliminará el ciclo de comentar-descomentar y realizar todo esto de manera más dinámica para cambiar las Variables de Entorno para distintos robots.
Para ver más información respecto a la solución ver en [Proyecto de Configuración de Variables de Entorno](http://hsarmiento.github.io/htrob/planning_project/2015/10/26/project.html#solucin )

#Primera iteración

Los avances desarrollados en la primera iteración son explicados en el siguiente post: http://hsarmiento.github.io/htrob/development_project/2015/11/16/first_iteration.html

#Desarrollo

## CRUD XML
A lo largo de esta tarea, que involucraba la totalidad de la semana 4 más la mitad de la semana 5, fueron realizadas todas las tareas que implicaban seleccionar, agregar, editar y eliminar desde el XML a la GUI (interfaz gráfica de usuario). De acuerdo a lo planificado, esta macro tarea fue contabilizada con 26 pomodoros (aproximadamente 13 horas) pero que en la ejecución de esta generó un superhábit de 5 pomodoros, es decir, un total de 31 pomodoros.

Por otro lado, las acciones sobre el XML se realizaron utilizando la librería de Python estándar de manejo de este tipo de archivos, el cual tiene como nombre `xml.etree.ElementTree`

La descripción de las micro tareas realizadas se presenta a continuación:

* Leer contenido de variables de general y para cada robot: a partir del XML (`env.xml`), se leen las variables que no han sido eliminadas para así ser visualizadas en los widget pertinentes a cada sección. Lo anterior, se logra de acuerdo a los atributos presentes en cada etiqueta de variable que tenga un valor de `deleted=0`, tal como el siguiente ejemplo:


```<general>      
	<variable deleted="1" name="ORBIT_SOCKETDIR" value="/tmp/orbit-robotica" />		
	<variable deleted="0" name="PYTHONPATH" value="/home/robotica/catkin_ws/devel/lib/python2.7/dist-packages:/opt/ros/indigo/lib/python2.7/dist-packages" />
	     <variable deleted="0" name="ROS_ROOT" value="/opt/ros/indigo/share/ros" />	
		<variable deleted="0" name="ROSLISP_PACKAGE_DIRECTORIES" value="/home/robotica/catkin_ws/devel/share/common-lisp" />	
		<variable deleted="1" name="ROS_DISTRO" value="indigo" />	
</general>
```


* Agregar variables de general y robot: para el caso de una variable general del entorno de ROS, esta simplemente se inserta dentro de las etiquetas `<general>...</general>` con su respectivo nombre y valor. Para el caso de agregar un nuevo robot, este se agrega entre las etiquetas `<robots> ... </robots>`. Además, por cada robot se insertan las etiquetas `<robot> ... </robot>` las cuales poseen atributos de identificador (o alias), eliminación (deleted) y uso actual (status). Para cada una de estas etiquetas, es posible agregar N nodos que representan las variables que cada robot poseerá. 

```<robots>
	  <robot deleted="0" id="turtlebot1" status="1">
			<variable deleted="0" name="TURTLEBOT_NAME" value="turtlebot" />
			<variable deleted="0" name="TURTLEBOT_TYPE" value="turtlebot" />
			<variable deleted="0" name="TURTLEBOT_BASE" value="kobuki" />
			<variable deleted="0" name="ROS_MASTER_URI" value="http://172.43.69.421:78312" />
			<variable deleted="0" name="ROS_HOSTNAME" value="localhost" />
    </robot>
</robots>
```
* Edición de variables: para este caso, simplemente se busca el nodo a editar de acuerdo a su nombre(para el caso de variables generales) y en el caso de robots, se encuentra el identificador correspondiente y luego se analizan las variables a editar. Dado que la librería usada no necesita crear un archivo temporal para realizar esta acción, la modificación se efectúa directamente sobre ella.
* 
* Eliminación de variables: si bien, la eliminación de variables podía efectuarse directamente sobre el XML, esto no aseguraba nada sobre el archivo bash. Para ello, se predispuso primero cambiar el estado de cada variable a `deleted=1` y luego cuando este fuera exportado al archivo final (bash), se eliminaría del XML.



## Exportación de XML a  archivo bash

El desarrollo de esta macro tarea involucraba la mitad de la semana 5, la cual trataba en eliminar y exportar las variables que habían sido asignadas en la GUI mediante la utilización de un archivo XML, para luego "parsear" tales valores de modo que fueran incluido en un archivo bash adicional. De esta forma, este último archivo sería incluido en el archivo original `.bashrc` original, permitiendo así que las configuraciones nunca fueran realizadas directamente sobre el ya mencionado. De acuerdo a lo planificado al comienzo de la semana, esta macro tarea contaría con utilización de 29 pomodoros, los cuales fueron superados en creces por los 36 pomodoros que realmente se realizaron.

La descripción de las micro tareas se efectúa a continuación:

* Aplicar unset a variables eliminadas: probablemente una de las tareas que más tiempo tomo dentro del desarrollo. La idea principal de esta acción era desarrollar un mecanismo que evitará la realización del comando `source` sobre el archivo `.bashrc` en una terminal. Sin embargo, ésta no pudo ser efectuada ya que la aplicación del comando `source` se hace sobre el actual entorno de trabajo, es decir, si un programa en Python hace la llamada de este comando, su resultado solo se verá expresado sobre ese programa pero no sobre el sistema operativo completo. De esta forma, el uso del comando `source`sobre cada terminal no pudo ser alterado. La aplicación del comando `unset` (el cual libera la asignación de una variable de entorno) se efectuó escribiendo al comienzo del archivo bash adicional, llamado `.htbash`, todas las variables que serían eliminadas a través de la GUI.
```
unset ROS_PACKAGE
```

* Aplicar export a variables asignadas: para exportar los valores desde el XML al archivo `.htbash`, desde la GUI de la aplicación se presiona el botón Apply para así efectuar esta acción. De esta manera, la aplicación busca todos los valores que no han sido eliminados (y que estén activos para el caso de un robot) para luego ser incoporados en el `.htbash`
```
export ROS_HOSTNAME=localhost
```
* Validación de estados de botones en GUI: para no producir estados que alterarán las acciones de la aplicación, se incorporó validación de los estados de los botones de la GUI, es decir, la activación y desactivación de éstos de acuerdo a los las acciones que se ejecutarán.
* Inclusión de archivo .htbash adicional a .bashrc: tras la generación del archivo `.htbash` (el cual contiene la información de las variables asignadas o elimadas de ROS), es de vital importancia que este sea incluido en el archivo `.bashrc` de modo que tras aplicar el comando `source`, los cambios sean consistentes con lo configurado en la aplicación.

![Ventana final]({{site.baseurl}}/assets/project/window_env.png)

## Testing, Documentación y Refactoring
Estas tareas fueron consideradas en la última semana de trabajo, es decir, semana 6 (y parte de la semana 7 correspondiente a la presentación final). A pesar de en un comienzo solo se incluía el manejo de estas tareas, fueron incorporadas otros detalles pequeños que fueron encontrados al realizar el refactoring, tales como estados incosistentes en relación a mensajes o botones. La estimación en tiempo alcanzaba los 42 pomodoros (para ambas semanas, incluyendo la presentación) pero fue superadas en 15 pomodoros, entregando un total de 57 divisiones de tiempo.

La descripción de las micro tareas son explicadas a continuación:

* Testing: se utilizó la técnica de Unit Testing, el cual comprende una serie de técnica para asociar valores esperados con valores entregados por la aplicación, para así comparar y analizar si son realmente verídicos. Así, fue integrada librería de Python, `unittest`, que permitía efectuar tales acciones. Con esto, fueron probadas las principales funcionalidades, tales como la lectura de datos desde el archivo XML así como la exportación al archivo `.htbash`
* Documentación: esta tarea incluye la incorporación del archivo `README.md` que permite una rápida explicación e instalación del proyecto en la ventana principal del repositorio. También se añadió la documentación más detallada correspondien a la wiki del proyecto, la cual puede ser observada en el siguiente link [Wiki rqt_env](https://github.com/hsarmiento/rqt_env/wiki).
* Refactoring: corresponde a la tarea de eliminar y mejorar el código presente hasta el momento.

#Análisis de planificación estimada

En esta segunda etapa de desarrollada y ya contando con una planificación pre realizada antes de cada semana, se contabilizaron un total de 97. Sin embargo, el total real de pomodoros fue 124 pomodoros, superando así en un 27% lo que fue estimado en el comienzo de cada semana. 

![Gráfico pomodoros]({{site.baseurl}}/assets/project/pomodoros.PNG)


## Análisis de zona crítica
Para explicar(en parte) la diferencia anteriormente mencionadas, es posible analizar el gráfico de frecuencia de código expuesto por Github para conocer la caída en la cantidad de líneas por día/semana. Así, en la imagen expuesta a continuación, se aprecia un caída a partir del día 23 de noviembre, que coincide con la semana 5, tramo en el cual se comenzó con el trabajo de exportación de XML a `.htbash`, el cual sufrió muchos retrasos al no encontrar una solución para el comando `source` sobre la solución generada.

![Frecuencia de código]({{site.baseurl}}/assets/project/code_frecuency.png)




