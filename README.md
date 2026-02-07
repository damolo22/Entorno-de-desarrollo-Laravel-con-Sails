# Practica Realizada por :
DAVID MORENO LÓPEZ

# Practica: Entorno de desarrollo Laravel con Sails #
Para esta tarea vamos a necesitar los siguientes requisitos:

Docker Desktop (en ejecución).
WSL 2 (si utilizas Windows).
Terminal o consola de comandos.


Con todo esto empezamos ejecutando el comando de instalación : curl -s "https://laravel.build/ProyectoSails" | bash


![Imagen status nginx](img/CAP1.png)



Una vez creado entramos y lanzamos por primera vez los contenedores:

./vendor/bin/sail up -d

![Imagen status nginx](img/CAP2.png)

Ahora ejecutamos las migraciones :

./vendor/bin/sail artisan migrate

Entrando en http://localhost vemos: 

![Imagen status nginx](img/CAP3.png)






## 3. ¡Ahora con más clúster! ##
Ahora detenemos el servidor que hemos dejado ejecutándose, y ahora creamos un archivo con-cluster.js, con el contenido del PDF y lo lanzamos:
```
node con-cluster.js
```
![Imagen status nginx](img/cap4.png)

Después podemos ver en el rendimiento que al hacer loadtest nos da que los rps y la Mean latency han cambiado,  (aunque son valores más bajos, esto pasa porque mi máquina virtual solo tiene 1 núcleo asignado):
![Imagen status nginx](img/cap5.png)


## 4. Uso de PM2 para administrar un clúster de Node.js  ##
A continuación vamos a utilizar PM2, lo instalamos en la terminal que no está ejecutando nada, tras instalarlo lo ejecutamos en el sin-cluster.js :
![Imagen status nginx](img/cap6.png)

Con PM2 instalado ejecutamos y podemos ver que su rendimiento es estable y similar al modo cluster manual:
![Imagen status nginx](img/cap7.png)

Tras esto vamos a crear un archivo de configuración, primero borramos el pm2, instalamos su ecosystem y editamos el archivo de configuración:
```
pm2 delete all
pm2 ecosystem
nano ecosystem.config.js
```

Lo ejecutamos y vemos que está correcto:
```
pm2 start ecosystem.config.js
```
![Imagen status nginx](img/cap8.png)


## TAREA  ##
Comando: pm2 ls: Te muestra una lista de todas las aplicaciones que PM2 está controlando, su estado, cuánto llevan encendidas y cuánta memoria ocupan.
![Imagen status nginx](img/cap9.png)

Comando: pm2 logs: Es el comando base. Son los registros (logs) de salida. 
![Imagen status nginx](img/cap10.png)

Comando: pm2 monit : Abre un panel de monitoreo en tiempo real para  ver cuánto uso de CPU y RAM consume cada proceso al instante.
![Imagen status nginx](img/cap11.png)

## 5. Cuestiones  ##
La aplicación sin clúster funciona mejor en este caso por dos motivos principales:
- Gasto extra de gestión: Al activar el clúster, el ordenador tiene que gastar recursos (CPU y memoria) para coordinar a los procesos trabajadores. La versión simple no tiene ese "gasto extra".
- Solo hay un núcleo: Como la máquina de pruebas solo tiene un núcleo, no puede hacer varias cosas a la vez de verdad. El sistema pierde tiempo parando y arrancando los diferentes procesos para que se turnen, lo que acaba siendo más lento que dejar a un solo proceso trabajar sin interrupciones.
