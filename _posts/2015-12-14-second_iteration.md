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

``
<general>       
		<variable deleted="1" name="ORBIT_SOCKETDIR" value="/tmp/orbit-robotica" />		
		<variable deleted="0" name="PYTHONPATH" value="/home/robotica/catkin_ws/devel/lib/python2.7/dist-packages:/opt/ros/indigo/lib/python2.7/dist-packages" />
	     <variable deleted="0" name="ROS_ROOT" value="/opt/ros/indigo/share/ros" />	
		<variable deleted="0" name="ROSLISP_PACKAGE_DIRECTORIES" value="/home/robotica/catkin_ws/devel/share/common-lisp" />	
		<variable deleted="1" name="ROS_DISTRO" value="indigo" />	
</general>
``

* Agregar variables de general y robot: para el caso de una variable general del entorno de ROS, esta simplemente se inserta dentro de las etiquetas `<general>...</general>` con su respectivo nombre y valor. Para el caso de agregar un nuevo robot, este se agrega entre las etiquetas `<robots> ... </robots>`. Además, por cada robot se insertan las etiquetas `<robot> ... </robot>` las cuales poseen atributos de identificador (o alias), eliminación (deleted) y uso actual (status). Para cada una de estas etiquetas, es posible agregar N nodos que representan las variables que cada robot poseerá. 
```xml
<robots>
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
* Eliminación de variables: si bien, la eliminación de variables podía efectuarse directamente sobre el XML, esto no aseguraba nada sobre el archivo bash. Para ello, se predispuso primero cambiar el estado de cada variable a `deleted=1` y luego cuando este fuera exportado al archivo final (bash), se eliminaría del XML


## Exportación de XML a  archivo bash



## Testing

## Documentación


#Análisis de planificación estimada

## Tiempo(pomodoros) estimado vs Tiempo real de desarrollo

## Análisis de zona crítica





