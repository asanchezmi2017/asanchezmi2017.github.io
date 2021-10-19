
Hola, mi nombre es Antonio Sánchez Mranda y este es el repositorio donde actualizaré mis avances de mi [Turtlebot 3](https://github.com/asanchezmi2017/hello-world) te invito a visitarlo y a colaborar. (Prueba Visual)

A continuación les muestro una imagen de mi espacio de trabajo: ![ESpacio de Trabajo](https://github.com/asanchezmi2017/asanchezmi2017.github.io/blob/main/IMG_3592.jpg)


## Writing a Publisher and subscriber 

Vamos a empezar poniendo el código que necesitamos para publicar y suscribirnos a un topic

### Publisher
En este caso vamos a publicar en el topic /cmd_vel con el fin de que nuestro Turtlebot 3 se mueva en línea recta:
```
#! /usr/bin/env python3   
#esto tenemos que ponerlo siempre  para asegurarnos de que se ejecuta como una secuencia de comandos Python

import time
import rospy
from geometry_msgs.msg import Twist  #Estamos importando Rospy y el tipo de mensaje que vamos a utilizar, esta información la podemos sacar del nodo en el que queremos publicar


rospy.init_node('move_robot_node')  #Aquí ponemos el nombre del nodo que queremos ejecutar
pub = rospy.Publisher('/cmd_vel', Twist, queue_size=1) #(nodo donde queremos pubicar, tipo de mensaje que vamos a publicar, queue_size limita los mensajes en cola si algún suscriprtos no los recibe)
rate = rospy.Rate(10)  #Son las veces que  publica por segundo 
move = Twist()
move.linear.x = 0.1

while not rospy.is_shutdown():  #Ocurren las siguientes condiciones mientras no pulsemos CTRL-C
  pub.publish(move) 
  rate.sleep()
  rospy.loginfo(move)	#Obtenemos por pantalla lo que estamos publicando en el nodo
```

### Subsriber
En este caso nos queremos subscribir al topic /scan para poder escucha la información que está leyendo el LIDAR de nuestro Turtlebot 3
```
#!/usr/bin/env python3

import rospy 
from sensor_msgs.msg import LaserScan


def callback(msg):
  rospy.loginfo(msg.ranges) #Obtenemos por pantalla una tupla de 360 valores con las distancias en metros

def get_info_laser():
	rospy.init_node ('info_laser', anonymous = True)
	rospy.Subscriber("/scan", LaserScan, callback)
	rospy.spin()
	

if __name__ == '__main__':
    get_info_laser()	
    
```



## Contacto
Pueden contactar conmigo si tienen cualquier duda a través de mi correo a.sanchezmi.2017@alumnos.urjc.es

