---
layout: post
title:  "Por que no funciona?"
date:   2015-09-27 17:00:00
author: Teófilo - Hernán
categories: finished
---

# Por que no funciona?

## Qué es lo que pueden averiguar con las herramientas ROS y cómo este es útil para encontrar la falla?

Con las herramientas de ROS, tales como rostopic list y rostopic node, pudimos analizar  los diferentes elementos presentes al tratar de lanzar el turtlebot. Además, con rqt_graph pudimos descubrir las conexiones entre los diferentes nodos mediante los tópicos

![Martes 07 de septiembre]({{site.baseurl}}/assets/week-progress/week02_01.jpg)

![Jueves 09 de septiembre]({{site.baseurl}}/assets/week-progress/week02_02.jpg)

![Jueves 09 de septiembre]({{site.baseurl}}/assets/week-progress/week02_03.jpg)

![Jueves 09 de septiembre]({{site.baseurl}}/assets/week-progress/week02_04.jpg)


## Cuáles son las posibles fallas que pueden detectar?

Al inspeccionar la herramienta de rqp_graph, pudimos apreciar que el nodo de gazebo está completamente aislado y sin ningún tópico que pueda conectar a otro nodo

## Qué es lo que han hecho para detectar una (o varias) fallas (de un mismo tipo) y cuáles fueron los resultados obtenidos?

Primero ejecutamos rqt_graph para mostrar los nodos y tópicos activos. Nos dimos cuenta que el nodo de gazebo no tenia conexión alguna mediante un tópicos con los demás nodos (sospechoso).

## Su diagnóstico de que está fallando y sugerencia sobre cómo se podria arreglar?

De acuerdo a lo anterior, el nodo gazebo queda totalmente aislado de los demás nodos por lo que la interacción con esta herramienta queda totalmente inhabilitada. Por ello, una sugerencia seria conectar tal nodo con el o los que corresponda para generar el tópico indicado de modo que se ROS realiza las transformaciones ad-hoc que permitan el funcionamiento ideal

## Críticas hacia las herramientas ROS

Al utilizar rqt_graph, si bien se aprecian las conexiones entre nodos y sus tópicos, no se aprecia ningún mensaje de error que permita conocer que el nodo gazebo produce un estado inesperado, por lo que para saber aquello habría que conocer de antemano las conexiones en el grafo. Sin duda, se esperaría que rqt_graph entregue alguna señal de que algo inesperado ha ocurrido.

