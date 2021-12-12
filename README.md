## INSTALACION DE DOCKER

1. linux y Mac
   * Ir a ==> docker.com
   * seleccionar "get started"
   * En "docker Desktop" seleccionar descargar en el sistema operativo(linux/mac)
   * paso a paso instalacion de ubuntu en ubuntu 20.04:
     * <https://docs.docker.com/engine/install/ubuntu/>
     * <https://docs.docker.com/engine/install/linux-postinstall/>
  
## COMANDOS DOCKER

* docker build -t express-app .  **(Permite generar un imagen y con el flag -t se le asigna un nombre a la imagen)**
* docker build -t express-app:v2 .  **(Permite generar un imagen y con el flag -t se le asigna un nombre a la imagen y version usando :v2 despues del nombre)**
* docker images -aq( el flag -aq permite listar solo los IDs de las imagens) **(Lista las imagenes activas)**
* docker image rm express-app:v2 / docker rmi [nombre-imagen] **(Permite eliminar una imagen indicando la version con el tag)**
* docker run [nombre-image] **(ejecuta una imagen y crea un contenedor)**
* docker run -d --name [nombre-contenedor] [nombre-image] **(ejecuta una imagen en 2do plano usanod el flag -d(detach))**
* docker ps **(permite verificar los contenedores que estan corriendo)**
* docker ps -a **(permite verificar los contenedores que estan activos e inactivos)**
* docker ps -aq **(permite verificar los contenedores que estan activos e inactivos SOLO IDs)**
* docker rm [CONTAINER ID]/[IMAGE NAME] **(eliminar un contenedor)**
* docker rm $(docker ps -aq) -f **elimina todos los contenedores** **-f es para forzar la eliminacion incluso si esta corriendo el container**
* docker stop/kill [CONTAINER ID]/[IMAGE NAME] **(detener un contenedor)**
* docker start [CONTAINER ID]/[IMAGE NAME] **(ejecutar un contenedor)**
* docker run -d/-it(solo para react) --name [name container] -p 3333:3333 [image name] **(el flag -p permite mapear los puertos, que es el proceso de redireccionar el puerto 3333 del pc al puerto 3333 del contenedor, de esta forma cada vez que se llame al puerto 3333 del pc se estara llamando al 3333 del contenedor)**
* docker run -d/-it(solo para react) -e ENV=development --name [name container] -p 3333:3333 [image name] **-e ENV=development es la forma en la que se  pasa variables de entorno**
* docker ps --format="ID\t{{.ID}}\nNombre:\t{{.Names}}" **para imprimir con un formato**
* docker rm $(docker ps -a -f status=exited -q) ==> Elimina todos los contenedores
* docker rmi $(docker images -q) ==> Eliminar todas las imágenes de docker
* docker rm $(docker ps -a -q) ==> Eliminar todos los contenedores de docker
* docker logs [id]/ docker logs -f [id] ==> ver logs de un contenedor
* docker ps -a | grep [npmbre-images] ==> lista detalle de una imagen especifica

---

## WORKING WITH VOLUMENS

Si generamos una imagen de una app y luego realizamos un cambio a dicha app no lo vamos a ver reflejado en el contenedor que se esta ejecutando con la imagen generada, para ver los ultimos cambios debemos generar una nueva imagen.
Para solventar este problema debemos mapear el working directory de nuestra app local al working directory del contenedor, de esta manera si hacemos un cambio en el proyecto local veremos los cambios reflejados en la app del contenedor **(esto se logra mediante los volumes con el flag -v)**

> **-v [absolutePathProject]:[workingDirectoryContainer]**

#### En Mac o linux: 

**-v $(pwd):[workingDirectoryContainer]** (pwd permite obtener la rute absoluta del directorio actual)

 **-v /usr/app/node_modules** (Permite que no se borre las dependencias de node_modules cuando se realiza la copia de archivos de nuestros archivos locales a la imagen)

 ##### EJEMPLO EJECUTANDO CON VOLUMES

 * docker run -v $(pwd):/app -d --name [ container name] -p 3333:3333 [image name]
 * docker run -v $(pwd):/app -v /app/node_modules -d --name react-app -p 3000:3000 react-app
 * docker run -d -p 80:80 --name website -v $(pwd):/usr/share/nginx/html nginx:ro (usa la imagen de nginx y copia el proyecto de la ruta actual con pwd a la carpeta de nginx para desplegarla con este servidor PUEDE SER USADO PARA DESPLEGAR LA CARPETA BUILD DE UN PROYECTO DE REACTJS)


### STEPS TO CONTENARIZED AN APLICATION

1. Create dockerfile
2. docker build -t <image_name>
3. docker run -v $(pwd):/app -d --name [ container name] -p 3333:3333 [image name]

# Instalar Docker Compose

1. sudo curl -L "https://github.com/docker/compose/releases/download/1.26.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
2. sudo chmod +x /usr/local/bin/docker-compose
3. docker-compose --version

# EJECUTAR DOCKER-COMPOSE

1. docker-compose up
2. docker-compose down

# Verificar todos los puerto que estan siendo usados en tu pc: **sudo lsof -nP | grep LISTEN**
# Detener servicio que esta ocupando cierto puerto: **sudo systemctl stop apache2[<== este es el nombre del servicio "apache2"]**


