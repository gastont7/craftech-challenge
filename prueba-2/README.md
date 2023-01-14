#  Documentacion para levantar proyecto en local 
---
## como levantar proyecto DJANGO en local con SO ubuntu:

Para levantar un proyecto de Django en Ubuntu, primero debes asegurarte de tener las herramientas necesarias instaladas en tu sistema. Necesitarás tener instalado Python, así como pip, el administrador de paquetes de Python. También es recomendable tener instalado virtualenv, que te permite crear entornos de desarrollo aislados.
Para instalar Python, pip y virtualenv en Ubuntu, puedes ejecutar los siguientes comandos en la terminal:

```
sudo apt-get update
sudo apt-get install python3
sudo apt-get install python3-pip
sudo apt-get install -y python3-venv
pip3 install virtualenv
```

- en la directorio backend(donde se encuentra el proyecto) crear el entorno virtual

`python3 -m venv “name venv”`

- luego activar el virtual enviroment (venv)

`source “name venv”/bin/activate`  (para desactivarlo, deactivate)

- ya dentro del entorno virtual instalar las dependencias necesarias indicadas en el requirements.txt

`pip install -r requirements.txt`

- declarar la variable SECRET_KEY como variable de entorno(depende del SO) en Ubuntu seria:

`export SECRET_KEY=”pass”`

- finalmente levantar el servicio

`pyhton manage.py runserver 0.0.0.0:8000`

### Ahora tu proyecto estará corriendo en el localhost:8000, Puedes abrirlo en un navegador.
--- 

## como levantar projecto react.js en ubuntu:

Para levantar un proyecto React en Ubuntu, primero necesitas tener instalado Node.js y npm (gestor de paquetes de Node.js) en tu sistema. Puedes verificar si ya tienes estas herramientas instaladas ejecutando los siguientes comandos en la terminal:

```
node -v
npm -v
```

- Si no tienes Node.js y npm instalados, puedes instalarlos mediante el siguiente comando:

```
apt-get install nodejs npm
o
curl -fsSL https://deb.nodesource.com/setup_1x.x | sudo -E bash –
apt-get install nodejs -y
```

- tambien puedes instalar `nvm` para instalar la versión requerida de nodejs

`curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash`

- comprobar instalacion en otra terminal 

`nvm –versión`

- instalar la versión deseada

`nvm install 1.x`     

- Una vez que tengas Node.js y npm instalados, 
Para iniciar el servidor de desarrollo y ver tu aplicación React en el navegador, ejecuta el siguiente comando dentro de la carpeta del proyecto:

`npm start`

 Ahora tu proyecto estará corriendo en el localhost:3000, Puedes abrirlo en un navegador.

### Nota: Tambien es posible usar yarn, que es otro administrador de paquetes, en lugar de npm, como sigue a continuacion:


- Para crear un proyecto de React en Ubuntu con Yarn, primero debes asegurarte de tener instalado Node.js y Yarn en tu sistema. Puedes verificar si los tienes instalados ejecutando los siguientes comandos en la terminal:
```
node -v
yarn -v
```
- Si no tienes Node.js o Yarn instalados, puedes instalarlos siguiendo las instrucciones en los sitios web oficiales:

(see [docs for `Node.js`](https://nodejs.org/en/download/package-manager/))

(see [docs for `Yarn`](https://classic.yarnpkg.com/en/docs/install))

https://phoenixnap.com/kb/how-to-install-yarn-ubuntu

- Una vez que tengas Node.js y Yarn instalados, Ubicarse en el proyecto frontend:

```
Cd /path to directory/
yarn install 
```

Después de ejecutar el comando anterior, Yarn descargará e instalará todas las dependencias necesarias para el proyecto, y creará una estructura de directorios básica para el proyecto.
Una vez que el proceso de instalación haya terminado ejecutar el comando

`yarn start`

para iniciar un servidor de desarrollo y ver tu aplicación en ejecución en el navegador en la url http://localhost:3000/.


## levantar los servicios con docker desde los dockerfile:

Para poder realizar el despliegue de la aplicación Django (backend) con un frontend en React.js, es necesario seguir los siguientes pasos:

Crear una imagen Docker para el backend:

a. se creo un archivo "Dockerfile" en la raíz del proyecto Django.
b. se utilizo como imagen base "python:3.8-slim-buster" y se crea el directorio de trabajo.
c. Copiar el archivo "requirements.txt" del proyecto al contenedor para instalar las dependencias necesarias.
d. Copiar el resto de los archivos del proyecto al contenedor.
e. Exponer el puerto 8000 (o el que se esté utilizando) para que pueda ser accesible desde el exterior.
f. Ejecutar los comandos necesarios para iniciar el servidor de Django,"python manage.py runserver 0.0.0.0:8000"
g. construimos la imagen a partir del Dockerfile

docker build -t craftech/docker-django .

h. a partir de la imagen creada, vamos a construir el container

docker run “id imagen o name”
docker run -p 8008:8000 “id imagen o name”


Nota: se actualiza librerias y comentan algunas, en requirements.txt. se trobleshootean varios errores. 


Crear una imagen Docker para el frontend:

a. Crear un archivo "Dockerfile" en la raíz del proyecto React.js.
b. se utilizo como imagen base "node:18-buster-slim" y se crea el directorio de trabajo.
c. Copiar el archivo "package.json" del proyecto al contenedor y ejecutar "npm install" para instalar las dependencias necesarias.
d. Copiar el resto de los archivos del proyecto al contenedor.
e. Exponer el puerto 3000 (o el que se esté utilizando) para que pueda ser accesible desde el exterior.
f. Ejecutar el comando necesario para iniciar la aplicación, por ejemplo "npm start" o "yarn start"
g. construimos la imagen a partir del Dockerfile

docker build -t craftech/docker-react .

h. a partir de la imagen creada, vamos a construir el container

docker run “id o name imagen”
docker run -p 8008:8000 “id o name imagen”


---
# Documentacion para levantar proyecto en AWS
---


