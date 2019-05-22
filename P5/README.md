## Práctica 5. Replicación de bases de datos MySQL
# Crear una BD e insertar datos

Lo primero que vamos a hacer es crear una BD e insertar algunos datos en la tabla datos. Para ello tendremos que que entrar en mysql
`mysql -uroot -p` una vez dentro ejecutaremos los siguientes comandos para crear e insertar datos.

![img](https://github.com/MenaBarrera/SWAP/blob/master/P5/capturas%20p5/1.png)

Ahora insertamos una fila en la tabla

![img](https://github.com/MenaBarrera/SWAP/blob/master/P5/capturas%20p5/2.png)

# Copiar de una maquina a otra la base de datos
Para ellos vamos a utilizar mysqldump
![img](https://github.com/MenaBarrera/SWAP/blob/master/P5/capturas%20p5/4.png)
Ahora lo copiamos con scp en la maquina 2 y lo ejecutamos para copiar la estructura de la BD
![img](https://github.com/MenaBarrera/SWAP/blob/master/P5/capturas%20p5/scp.png)
Y como teniamos las tablas bloqueadas, las desbloqueamos ejecutando la orden de la imagen
![img](https://github.com/MenaBarrera/SWAP/blob/master/P5/capturas%20p5/5.png)

# Replicación de BD mediante una configuración maestro-esclavo
La opción anterior funciona perfectamente, pero es algo que realiza un operador a mano. Sin embargo, MySQL tiene la opción de configurar el demonio para hacer replicación de las BD sobre un esclavo a partir de los datos que almacena el maestro.
Se trata de un proceso automático que resulta muy adecuado en un entorno de producción real. Implica realizar algunas configuraciones, tanto en el servidor principal como en el secundario.

Lo primero es editar el archivo de configuracion /etc/mysql/mysql.conf.d/mysqld.cnf y comentar la linea *#bind-address 127.0.0.1*
cambiar los logs a *log_error = /var/log/mysql/error.log*
establecer el server id a 1 *server-id = 1*. Guardamos el documento y reiniciamos el servicio:
/etc/init.d/mysql restart

![img](https://github.com/MenaBarrera/SWAP/blob/master/P5/capturas%20p5/restart.png)

Ahora repetimos lo mismo en la maquina 2 pero cambiando el server-id=1 por server-id=2. Y reiniciamos el servicio mysql.
Entramos en mysql y ejecutamos las siguientes ordenes
__mysql> CREATE USER esclavo IDENTIFIED BY 'esclavo';
mysql> GRANT REPLICATION SLAVE ON *.* TO 'esclavo'@'%' IDENTIFIED BY 'esclavo';
mysql> FLUSH PRIVILEGES;
mysql> FLUSH TABLES;
mysql> FLUSH TABLES WITH READ LOCK;__
Para finalizar con la configuración en el maestro, obtenemos los datos de la BD que vamos a replicar para posteriormente usarlos en la configuración del esclavo:
__mysql> SHOW MASTER STATUS;__
![img](https://github.com/MenaBarrera/SWAP/blob/master/P5/capturas%20p5/master%20status.png)

Volvemos a la máquina esclava, entramos en mysql y le damos los datos del maestro. Como indicábamos antes, sólo si trabajamos con versiones inferiores a mysql 5.5 estos datos se pueden introducir directamente en el archivo de configuración. Como lo más seguro es que estemos trabajando con una versión de mysql superior a la 5.5, entraremos en el entorno de mysql y ejecutamos la siguiente sentencia (ojo con la IP,
con el valor de "master_log_file" y del "master_log_pos" del maestro):
__mysql> CHANGE MASTER TO MASTER_HOST='10.211.55.10', MASTER_USER='esclavo', MASTER_PASSWORD='esclavo', MASTER_LOG_FILE='mysql-bin.000002', MASTER_LOG_POS=980, MASTER_PORT=3306;__
Por último, arrancamos el esclavo
__mysql> START SLAVE;__
Ahora, si queremos asegurarnos de que todo funciona perfectamente y que el esclavo no tiene ningún problema para replicar la información, nos vamos al esclavo y con la siguiente orden:
__mysql> SHOW SLAVE STATUS\G__
revisamos si el valor de la variable “Seconds_Behind_Master” es distinto de “null”. En ese caso, todo estará funcionando perfectamente. 
![img](https://github.com/MenaBarrera/SWAP/blob/master/P5/capturas%20p5/Captura%20de%20pantalla%202019-05-22%20a%20las%2016.34.19.png)

Insertamos un dato en la maquina 1 y vemos como se repica en la segunda
![img](https://github.com/MenaBarrera/SWAP/blob/master/P5/capturas%20p5/Captura%20de%20pantalla%202019-05-22%20a%20las%2016.37.13.png)


