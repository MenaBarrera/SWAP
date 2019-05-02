## Practica 3: Balanceo de carga
# Introducción 
En esta práctica configuraremos una red entre varias máquinas de forma que tengamos un balanceador que reparta la carga entre varios servidores finales.
El problema a solucionar es la sobrecarga de los servidores. Se puede balancear cualquier protocolo, pero dado que esta asignatura se centra en las tecnologías web, balancearemos los servidores HTTP que tenemos configurados.
De esta forma conseguiremos una infraestructura redundante y de alta disponibilidad.

# Balanceo con Nginx
La primera herramienta que vamos a ultilizar para el balanceo de carga será Nginx. Debemos indicarle a Nginx que ips son los servidores que tiene que balancear

![img](https://github.com/MenaBarrera/SWAP/blob/master/Practica3/img/4.png)

Con esta configuración hemos balanceado mediante Round-Robin ya que le hemos dado el mismo peso a ambas maquinas.
Para comprobar el funcionamiento vamos a lanzar peticiones al balanceador.

![img](https://github.com/MenaBarrera/SWAP/blob/master/Practica3/img/2.png)

Como se puede ver cada vez responde una maquina distinta, para hacerlo mas grafico lo vamos a comprobar con la herramienta htop.

![img](https://github.com/MenaBarrera/SWAP/blob/master/Practica3/img/3.png)

Como podemos ver el % de cpu de las maquinas 1 y 2 son relativamente parecidos (y bajos cosa que al hacer la practica no ocurría :/ )

# Balanceo con Haproxy
Para configurar Haproxy como balanceador tenemos que modificar algunos parametros de configuracion de Haproxy. Para ello modificamos el archivo ` /etc/haproxy/haproxy.cfg ` Usando como configuración la siguiente.

![img](https://github.com/MenaBarrera/SWAP/blob/master/Practica3/img/5.png)

Ahora vamos a comprobar como antes con htop que se realiza balanceo tal y como lo hicimos anteriormente. Con la herramienta htop


![img](https://github.com/MenaBarrera/SWAP/blob/master/Practica3/img/6.png)
