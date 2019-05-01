## Practica 3: Balanceo de carga
# Introducción 
En esta práctica configuraremos una red entre varias máquinas de forma que tengamos un balanceador que reparta la carga entre varios servidores finales.
El problema a solucionar es la sobrecarga de los servidores. Se puede balancear cualquier protocolo, pero dado que esta asignatura se centra en las tecnologías web, balancearemos los servidores HTTP que tenemos configurados.
De esta forma conseguiremos una infraestructura redundante y de alta disponibilidad.

# Balanceo con Nginx
La primera herramienta que vamos a ultilizar para el balanceo de carga será Nginx. Debemos indicarle a Nginx que ips son los servidores que tiene que balancear
