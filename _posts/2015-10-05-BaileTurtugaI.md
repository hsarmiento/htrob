---
layout: post
title:  "Baile Turtuga I"
date:   2015-10-10 17:00:00
author: Teófilo - Hernán
categories: finished
---

# Baile Turtuga I

## Tareas realizadas
Durante esta semana de trabajo se implementó el baile de "moonwalk" para el turtlebot. Primero, se elaboraron los pasos para que funcionará de manera correcta en el simulador de Gazebo y luego en el TurtleBot como tal.

![Viernes 09 de octubre]({{site.baseurl}}/assets/week-progress/turtledance.png) 

### Obstáculos encontrados
En un comienzo, los movimientos del robot iban a ser realizados utilizando solo Twist una cantidad X de tiempo para cada iteración. En la teoría (simulación) esto funcionaba bien pero al probarlo en el TurtleBot, el robot no efectuaba la misma coordinación de los pasos y movimientos debido a la interpretación del tiempo en ambos entorno.

Tras ello, cambiamos la forma de calcular la distancia/tiempo que debía moverse el robot, por lo que utilizamos JointStates para obtener sincronización respecto a las ruedas del robot. Nuevamente, en la simulación logramos realizar los movimientos del baile pero al probar en el TurtleBot este no recibía ningún tipo de dato para ser utilizados por el programa elaborado. Nos dimos cuenta que los valores del JointStates no eran recibidos por nuestra máquina y que incluso no tenían el mismo formato.

Por último, recurrimos a la utilización del Odometry, de forma de saber la posición y ángulo relativo del robot en todo momento. Mediante una serie de transformaciones de ambos datos logramos descifrar en "lenguaje humano" la distancia que se movía el robot y el ángulo en grados de este. Nuevamente, en simulación realizamos las tareas correspondientes pero al hacerlo en el TurtleBot al parecer se perdía conexión o paquetes por lo que a veces funcionaba bien pero en otras no tanto.

###Resultados

Codigo <a href="https://github.com/tchambil/htrob/blob/master/turtledance1.py">github</a>
 

### Críticas
Para obtener el resultado esperado, la programación del baile se realizó de prueba y error para asi hacer calzar los movimientos esperados. Para ello se tenia que inicializar en cada momento el gazebo lo que realmente era molesto y se perdia un tiempo considerable.
Por otro lado,la aceleración no se podria controlar, ya que se establecia un parametro esperando que se paralice en ello, lo que tambien nos demoró en la programacion. 
