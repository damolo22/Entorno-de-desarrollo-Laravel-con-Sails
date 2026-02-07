# Practica Realizada por :
DAVID MORENO LÓPEZ

# Practica: Entorno de desarrollo Laravel con Sails #
Para esta tarea vamos a necesitar los siguientes requisitos:

Docker Desktop (en ejecución).
WSL 2 (si utilizas Windows).
Terminal o consola de comandos.


Con todo esto empezamos ejecutando el comando de instalación : curl -s "https://laravel.build/ProyectoSails" | bash


![foto 1](img/CAP1.png)



Una vez creado entramos y lanzamos por primera vez los contenedores:

./vendor/bin/sail up -d

![foto 2](img/CAP2.png)

Ahora ejecutamos las migraciones :

./vendor/bin/sail artisan migrate

Entrando en http://localhost vemos: 

![foto 3](img/CAP3.png)


