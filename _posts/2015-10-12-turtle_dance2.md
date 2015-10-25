---
layout: post
title:  "Baile Tortuga con Action lib"
date:   2015-10-12 17:00:00
author: Teófilo - Hernán
categories: Finished
---

# Baile Tortuga con Action Lib

## Tareas realizadas
Para el desarrollo de este trabajo se consideró los pasos definidos anteriormente, tal como se muestra en la imagen.

![Viernes 09 de octubre]({{site.baseurl}}/assets/week-progress/turtledance.png) 
Primeramente, implementamos los tutoriales de la wiki tanto lado servidor y cliente. Se implementa el ejemplo de "fibonacci_server.py". Esto se hace para tener claro el panorama el funcionamiento del accionlib.

Posteriormente, se crea un "package" de nombre htrob_actionlib donde se realiza la respectiva configuración para la implementación de nuestro propósito. Para ello se hace un test mediante un ejemplo sencillo que permita determinar si es par o impar. 

Finalmente, se procede a implementar los pasos definidos en "Baile Tortuga I". Se ha completado la implementación del lado del servidor estamos trabajando el lado de cliente.

###Resultados

Codigo: <a href="https://github.com/tchambil/bailetortuga2">Ver. Anterior</a> >>>>  <a href="https://github.com/tchambil/turtle2_actionlib">Ver. Actual</a>


Video: 
 

### Críticas
- Se debe de modificar demasiados archivos para agregar un mensaje.
- No está claro el porqué importar el "package msg", esto nos demoró en entender.
- Los mensajes automáticos se crean en la carpeta /devel, lo cual nos costó entender y encontrar
