---
layout: post
title:  "Primera entrega Proyecto de Configuración de Variables de Entorno"
date:   2015-11-16 17:00:00
author: Teófilo - Hernán
categories: Development_Project
github: https://github.com/hsarmiento/rqt_env
---

#Problema

#Solución

La solución denominada `rqt_env`, consiste en desarrollar una GUI utilizando paquetes de RQT-PACKAGE propios de ROS. `rqt_env`, permitirá realizar configuración de la variables de entorno tanto de ROS y de los ROBOTS de forma independiente. Esta solución tambiéntendrá diferentes configuraciones de robots guardadas,  con lo que se eliminará el ciclo de comentar-descomentar y realizar todo esto de manera más dinámica por lo se podrán cambiar las Variables de Entorno para distintos ROBOTS.
Para ver más información respecto a la solución ver en [Proyecto rqt_env](http://hsarmiento.github.io/htrob/planning_project/2015/10/26/project.html#solucin )


#Usos de rqt_env

El proyecto a desarrollar permitirá realizar las siguientes tareas en virtud de lo que actualmente se efectúa al trabajar con variables de entorno:

* Configuración mediante GUI v/s archivo `.bashrc`: la aplicación a desarrollar evitará el uso de la edición directa sobre el archivo `.bashrc`, el cual en muchas ocasiones puede generar redundancia en variables que están comentadas a lo largo de todo el archivo y que en algunos momentos podría incurrir a errores humanos al eliminar o editar variables de ROS o de otros software de manera accidental. Para ello, `rqt_env` permitirá realizar la configuración de estas variables mediante una interfaz gráfica de usuario sin la necesidad de interactuar directamente con el archivo `.bashrc`
* Configuración dinámica de variables de entorno asignadas a un robot: al poseer diferentes robots, el archivo `.bashrc` podría contener distintas variables de entorno  que en muchos casos se mantendrían comentadas y solo se descomentarían al ser utilizadas. Con `rqt_env`, este accionar se evitaría dado que las configuraciones de cada robot se guardarían en un archivo XML de modo que al aplicar los cambios, estos se incluirían en el archivo `.bashrc` sin la necesidad de una edición manual sobre éste.
* Uso de librerías estándares de ROS: `rqt_env` es desarrollado con herramientas y módulos presentes en la configuración básica que posee ROS, es decir, no es necesaria la inclusión de librerías externas que deban ser descargas e incluidas de manera  anexa a la aplicación para ser utilizada.


#Desarrollo

##Aprendizaje de RQT(QT)

El desarrollo de esta macro tarea, ejecutada en la primera semana de planificación del proyecto, consideró aproximadamente 20 pomodoros, es decir, un tiempo estimado de 10 horas. Las micro tareas elaboradas fueron las siguientes:

* Elaboración de tutoriales de ROS: el primer paso, fue interactuar con los manuales de la comunidad de ROS que entregan las pautas para desarrollar aplicaciones que utilicen RQT de forma de crear el paquete que contendrá la aplicación ([Tutorial RQT](http://wiki.ros.org/rqt/Tutorials/Create%20your%20new%20rqt%20plugin)). A pesar de seguir los pasos expuestos en el sitio, ésta no tuvo los resultados esperados.
* Aprendizaje PyQt: la aplicación será desarrollada utilizando el lenguaje Python bajo la librería de PyQt, un módulo que permita la creación de ventanas y que a su vez permitan interactuar con las acciones a través de código programable.
* Creación del archivo `.ui` (QT Designer): uno de los grandes inconvenientes al desarrollar una aplicación bajo el framework de QT, es la elaboración de la GUI mediante el archivo `.ui`, es cual es un archivo en formato XML que representa toda la estructura y elementos que poseerá la aplicación a desarrollar. Por ello, al realizar esta tarea manualmente, la cantidad de tiempo invertido crece de manera exponencial, impidiendo la ejecución de tareas de mayor importancia. Sin embargo, a través de las investigaciones efectuadas en este trabajo, se pudo encontrar una aplicación que trabaja sobre una GUI que permite crear ventanas y elementos de manera que estos se arrastran a la posición deseada y a través de una exportación, se genera el archivo .ui mencionado anteriormente. Un ejemplo de esto, es lo que aparece en la siguiente imagen.
* Prueba de ejemplos de GITHUB basados en RQT:  al comenzar con el desarrollo de la aplicación bajo los paquetes de RQT y al hacer uso de los tutoriales oficiales de ROS, no fue posible crear ni entender de manera correcta el real funcionamiento y programación de esta tarea. Por ello, una buena práctica fue testear los códigos presentes en Github que utilizarán RQT de manera de entender las acciones que realizaban cada uno de los métodos presentes en los plugins. Los plugin testeados se encuentran en la siguiente URL: [rqt_common_visualizations](https://github.com/ros-visualization/rqt_common_plugins)

**Problemas**

Al crear y ejecutar de manera inicial nuestra aplicación según lo explicado en el tutorial oficial de ROS para la creación de aplicaciones en RQT, nos fue imposible que está se ejecutará de manera correcta dado que visualizaba un error al efectuar esta tarea. Este problema estuve presente al menos unos 3 pomodoros, es decir, cercana a las 2 horas de trabajo. Finalmente, el real problema era en relación al caché presente en el sistema que impedía crear el paquete correspondiente a nuestra aplicación el cual fue solucionado eliminando éste.

`$ rm ~/.config/ros.org/rqt_gui.ini`

`$ rqt`

## Diseño de interfaz gráfica (GUI)

La segunda semana de desarrollo tuvo una duración de aproximadamente 14 pomodoros, es decir, cercano a las 7 horas de trabajo. En esta fase se ahondó en la creación de la GUI de la aplicación basándonos en lo aprendido en la etapa anterior y recogiendo los avances en cuanto a herramientas y conocimientos aprendidos.

* Uso de QT Designer para archivos `.ui`: de acuerdo lo mencionado anteriormente para QT Designer, la GUI de `rqt_env` fue creada íntegramente con este programa.
* Entender ventanas, botones y acciones de cada elemento:  uno de los grandes desafíos en vista de la utilización de QT, era conectar los elementos presentes en el XML (`.ui`) frente al código expuesto en Python. Para ello y en base a lo explicado en la etapa anterior respecto a GITHUB, fueron utilizados códigos de referencia para entender este funcionamiento.
* Creación de GUI “Final”: se elaboró el bosquejo de lo que será la GUI final, la cual inevitablemente puede sufrir pequeñas modificaciones a lo largo del desarrollo.

**Problemas**

Ya al haber conectado la GUI con el código de Python, se presentó el problema de llenar las tablas con datos a partir del último mencionado, el cual tomó una cantidad no menospreciable de pomodoros (o tiempo real). Además, uno de los integrantes del equipo de trabajo enfermó durante toda esta semana por lo que el desarrollo fue más lento de lo esperado pero completando de igual forma gran partes de las tareas planificadas en el Kanban.

## Diseño de estructura XML

La tercera y última semana de esta primera iteración tomó un total de 15 pomodoros (8 horas aproximadamente). En esta fase se desarrolló la re-estructuración del archivo XML que guardará las configuraciones de las variables de entorno seteadas en la aplicación (link a arquitectura del otro post).

* Re-creación de estructura XML: inicialmente al evaluar y planificar el proyecto,se había pensado en un concepto de estructura XML que incluía el valor de cada etiqueta como el nombre de cada variable de ROS y su valor la asignación que tendría esta variable ([Estructura XML antigua](https://github.com/tchambil/rqt_env/blob/master/htbot.xml)). Sin embargo, al estudiar más de fondo el uso de este tipo de archivos, se re-estructuró este formato para lograr una estandarización de estas variables mediante nombres que permitieran extraer, guardar y actualizar la información de manera correcta tal como se exhibe en el siguiente archivo: [Estructura XML actual](https://github.com/hsarmiento/rqt_env/blob/master/resource/env.xml)
* Conexión de GUI con XML (lectura de datos): un gran desafío del primer aprendizaje de esta etapa, era incluir todas las herramientas mencionadas anteriormente  y lograr la inclusión de cada una de éstas en una sola aplicación que permitiera entregar un primer feedback para el equipo. Así, se utilizó un XML que tuviera datos previamente cargados de forma manual, el cual fue leído por la GUI de forma que pudieran ser visualizados los datos en la aplicación `rqt_env`.
* Refactoring: debido a la gran cantidad de pruebas que fueron desarrolladas con distintos códigos de aplicaciones que hacen uso de rqt, nuestro proyecto contenía mucho código inservible y desordenado, por lo que se procedió a eliminar estas líneas que no entregaba aporte a nuestro proyecto.


#¿Qué podría saber la comunidad?
