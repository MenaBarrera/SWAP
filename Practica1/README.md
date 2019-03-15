# Practica 1: Preparacion de herramientas
## Instalacion de Ubuntu
Para la instalación de Ubuntu Server 16.04 se han seguido los pasos que se esperan 'estandar'. Es decir se ha seguido una instalacion limpia sin montar volúmenes con VLM. Al llegar al apartado de software adicional, se instaló **OpenSSH** y la pila software **LAMP**.

Una vez instalado el sistema, comprobamos si los servicios se han levantado comprobando si estan en el álbol de procesos que se están ejecutando. Lo haremos con ```ps -aux | grep apache```.

## Configuración de la interfaz
Una vez instalado el sistema operativo clonamos la maquina. Ahora hay que configurar una red local entre ambas maquinas virtuales. Para ello con las maquinas apagadas accedemos a su configuración y en el apartado de red, creamos un nuevo adaptador de red de tipo red interna.
![img](https://github.com/MenaBarrera/SWAP/blob/master/Practica1/red1.png)

 Ahora en cada maquina modificamos el archivo */etc/network/interfaces* de la siguiente manera
 ![img](https://github.com/MenaBarrera/SWAP/blob/master/Practica1/INTERFAZ.png) 
 En la otra maquina lo haremos de la misma manera el único detalle es que tendremos que cambiar la ip (por ejemplo poner 192.168.1.101)

 ##Prueba Curl
Probamos con Curl que efectivamente el servidor hhtp esta funcionando en una de las maquinas. Al ser clonada podemos deducir que funciona en ambas.
![img](https://github.com/MenaBarrera/SWAP/blob/master/Practica1/curl.png)
 