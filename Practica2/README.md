# Clonar información de un sitio web
## Primeros pasos
Para empezar debemos ver si tenemos instalado rsync, para ello es tan facil como ejecutar en la terminal el comando `sudo apt-get install rsync`. Tras esto tenemos dos opciones: 
1 - Esta instalado y lo unico que hace ubuntu es decirnos que se han actualizado 0 paquetes
2 - No esta instalado y lo instala preguntandonos si queremos que se haga uso de X MB en disco

El siguiente paso es crear en la carpeta **/var/www/html/** uno o varios archivos en la maquina que actua de servidor en producción y decirle a la carpeta que su dueño es el usuario del servidor con `chown mamb:mamb /var/www/html/ `

## clonando archivos con rsync
Vamos a clonar archivos de la maquina en producción a la maquina que tenemos de backup. Para ello utilizaremos el comando `rsync -avz -e ssh ip_servidor_producción:/var/www/ /var/www/`
![img](https://github.com/MenaBarrera/SWAP/blob/master/Practica2/img/img1.png)
Tal y como podemos ver en la imagen se reciben los archivos index.php e index.html. Archivos que solo existian en la maquina en producción.

## Acceso sin contraseña por ssh
Para el acceso sin contraseña haremos uso del comando `ssh-keygen`. Se basa en la filosofia de llave publica-privada. Generas un par de llaves, subes al servidor en producción la correspondiente, y con eso ya es suficiente para poder autenticarte sin tener que introducir ninguna password. A continuación podemos ver en las capturas de pantalla como se ha generado la clave (captura 1) y como se ha subido al servidor en produccion (captura 2)

![img](https://github.com/MenaBarrera/SWAP/blob/master/Practica2/img/key.png)
![img](https://github.com/MenaBarrera/SWAP/blob/master/Practica2/img/copykey.png)

Ahora vamos a comprobar si podemos acceder por ssh a la maquina en producción sin tener que introducir nada.

![img](https://github.com/MenaBarrera/SWAP/blob/master/Practica2/img/ssh.png)

## Archivo contrab
Como es interesante que se haga este clonado de archivos de forma automática, añadiremos al archivo crontab una linea para que se ejecute rsync cada hora. Para ello bastaria con añadir la ultima linea del archivo que se muestra en la siguiente imagen 

![img](https://github.com/MenaBarrera/SWAP/blob/master/Practica2/img/crontabs.png)
