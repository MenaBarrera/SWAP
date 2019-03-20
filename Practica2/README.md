# Clonar información de un sitio web
## Primeros pasos
Para empezar debemos ver si tenemos instalado rsync, para ello es tan facil como ejecutar en la terminal el comando `sudo apt-get install rsync`. Tras esto tenemos dos opciones: 
1 - Esta instalado y lo unico que hace ubuntu es decirnos que se han actualizado 0 paquetes
2 - No esta instalado y lo instala preguntandonos si queremos que se haga uso de X MB en disco

El siguiente paso es crear en la carpeta **/var/www/html/** uno o varios archivos en la maquina que actua de servidor en producción y decirle a la carpeta que su dueño es el usuario del servidor con `chown mamb:mamb /var/www/html/ `

## clonando archivos con rsync
Vamos a clonar archivos de la maquina en producción a la maquina que tenemos de backup. Para ello utilizaremos el comando `rsync -avz -e ssh ip_servidor_producción:/var/www/ /var/www/`

