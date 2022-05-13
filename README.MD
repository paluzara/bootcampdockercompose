Lo primero que habría que hacer seria generar los dititos dockerfiles de cada uno de los servicios.
En los dockerfiles simplemente ponemos en caso de un MS java ponemos la imagen del java 11(o el correspondiente al micro) y en caso
de la bbdd pues la imagen del mysql correspondiente.  Añadimos las variables de entorno de java y el puerto en el que queramos arrancar la aplicaciones
Y por ultimo ejecutamos con CMD el java -jar de las apps pasandole el puerto las java opts y demas configuraciones. Con esto a tendriamos listos los DockerFIles

Una vez generados los dockerfiles de cada uo de los servicios y teniendo ya las aplicaciones compiladas en sus jars, generamos las imagenes con el Docker build.
Cuando ya tenemos las imagenes custom creadas pasamos a generar el docker compose.
En el docker compose lo primero es bajarnos la imagen de la base de datos de prize y productservice junto con su volumen.
Para levantar nuestras imagenes custom en la propiedad  services.nombredelservicio.image : añadimos el nombre de nuestra imagen custom
													    services.nombredelservicio.depends_on: añadimos con que otras imagenes tiene dependencias (La bbdd por ejemplo)
														services.nombredelservicio.ports: para hacer el mapeo de puertos del host
Una vez terminado el docker-compose solo nos quedaría ejecutar el comando docker-compose up y ya arrancarian todos 
nuestros contenedores en el orden correcto con sus volumenes y sus dependencias.
Para parar todos los servicios a lavez simplemente ejecutar docker-compose down
