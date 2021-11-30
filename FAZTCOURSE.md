# INSTALAR DOCKER UBUNTU

1. <https://docs.docker.com/engine/install/ubuntu/>
2. sudo apt-get update
3. sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
4. curl -fsSL <https://download.docker.com/linux/ubuntu/gpg> | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
5. echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] <https://download.docker.com/linux/ubuntu> \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
6. sudo apt-get update
7. sudo apt-get install docker-ce docker-ce-cli containerd.io
8. sudo docker run hello-world
9. sudo docker --version

## POST INSTALATION

1. sudo groupadd docker
2. sudo usermod -aG docker $USER
3. docker --version

# INSTALAR DOCKER WINDOWS

1. descargar .exe de docker desktop
2. <https://docs.docker.com/desktop/windows/install>
3. instalar WSL 2
4. instalar Hyper-V backend and Windows containers
5. Agregar usuario al grupo de docker:
**NOTA**

Para agregar usuario al grupo de docker en **windows** luego de desacargar docker desktop y hyper-V para windows

```cmd
net localgroup docker-users lramirez /add
```

## IMAGE

**Es una plantilla para crear un ambiente, contiene todos los elementos necesarios para un app(librerias, env, archivos de configuracion, software, code, etc) puede tener una vesion es inmutable pero puede ser clonado o compartido, estas imagenes son creadas usando Dockerfile.(Es como un instalador)**

# COMANDOS DOCKER

1. docker search [nombreImage] (para buscar una imagen de docker por consola)
2. docker pull [nombreImage] (para descargar una imagen de dockerHub)
3. docker images (para ver que imagenes tenemos descargadas)
4. docker run [imagen] (crea un contenedor usando una imagen) ejemplo: docker run -it ubuntu bash (ejecuta el bash de ubuntu)

## CONTAINER

**Es una instacia ejecutandose de una imagen, en una maquina puede haber multiples contenedores**

## SUBIR IMAGENES A DOCKERHUB

1. crear cuenta en dockerhub
2. generar imagen: docker build -t lexfer/website . **[nombre user de dockerhub/nombre imagen]**
3. docker login (colocar nombre de user y contrasena)
4. subir imagen: docker push lexfer/website

####  SUBIR IMAGEN EXISTENTE A DOCKERHUB

* docker login
* El siguiente paso es preparar la imagen para que tenga el formato correcto y sea aceptada dentro de este registro.==> nombre_de_usuario/nombre_del_repositorio:etiqueta
* docker tag [nombre-img-a-modificar] [user-dockerhub]/[nombre-img-a-modificar]:1.0
* docker push [user-dockerhub]/[nombre-img-a-modificar]:1.0