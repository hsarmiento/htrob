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

La solución denominada `rqt_env`, consiste en desarrollar una GUI utilizando paquetes de RQT-PACKAGE propios de ROS. `rqt_env`, permitirá realizar configuración de la variables de entorno tanto de ROS y de los ROBOTS de forma independiente. Esta solución tambiéntendrá diferentes configuraciones de robots guardadas,  con lo que se eliminará el ciclo de comentar-descomentar y realizar todo esto de manera más dinámica por lo se podrán cambiar las Variables de Entorno para distintos ROBOTS.
Para ver más información respecto a la solución ver en [Proyecto de Configuración de Variables de Entorno](http://hsarmiento.github.io/htrob/planning_project/2015/10/26/project.html#solucin )
