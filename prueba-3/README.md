# Para dockerizar un nginx con el index.html default, seguiríamos los siguientes pasos:
---

- 1.Crear un directorio en nuestra máquina local con el nombre "nginx-docker" y dentro de él, crear un archivo llamado "index.html" con el contenido que queramos mostrar en nuestra página web, que en este caso va ser el index defaul de nginx.

2.Crear un archivo llamado "Dockerfile" en el mismo directorio, en el cual incluiremos las siguientes instrucciones:

```
FROM nginx:version
COPY index.html /usr/share/nginx/html/index.html
```

Estas instrucciones indican que se copiará el archivo "index.html" dentro del directorio predeterminado de nginx donde se buscan los archivos HTML.

3.En la línea de comandos, nos posicionamos en el directorio "nginx-docker" y ejecutamos el comando "docker build -t nginx-docker ." para construir la imagen con el nombre "nginx-docker" utilizando el Dockerfile que acabamos de crear.

4.Una vez construida la imagen, ejecutamos el comando `docker run -p 8080:80 nginx-docker` para iniciar un contenedor con la imagen recién creada y exponer el puerto 8080 para poder acceder a nuestra página web en localhost.

---

###para crear un pipeline en GitHub Actions que actualice la imagen ante cada cambio realizado en el index.html, podemos seguir estos pasos:
---

1.Crear un repositorio en GitHub donde almacenaremos nuestros archivos del proyecto, incluyendo el Dockerfile, index.html y docker-compose.

2.Crear un .github/workflows dentro del repositorio, 

3.En el pipeline de CI/CD actualizara la imagen en DockerHub cada vez que se realiza un cambio en el archivo index.html.

```
name: CI/CD
on:
  push:
    branches: [ master ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Build and push Docker image
      run: |
        docker build -t my-nginx-image .
        echo ${{ secrets.DOCKER_PASSWORD }} | docker login -u ${{ secrets.DOCKER_USERNAME }} --password-stdin
        docker push my-nginx-image
```

cada vez que se haga un push a la rama master, se construirá la imagen y se la publicará en tu cuenta de DockerHub.para loguear en Dockerhub debe de estar configurado las variables DOCKER_USERNAME y DOCKER_PASSWORD en tu repositorio.

- crear un archivo docker-compose.yml para poder desplegar tus cambios de manera automatizada cada vez que se actualize tu imagen en DockerHub


Con esto podrias ejecutar el comando docker-compose up para desplegar los cambios en tu entorno.
