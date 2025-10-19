# BIND MOUNT
En un bind mount mapeamos (montar) un directorio o archivo específico del sistema de archivos del host con una parte del sistema de ficheros del contenedor.

```
docker run -d --name <nombre contenedor> -v <ruta carpeta host>:<ruta carpeta contenedor> <imagen> 
```
ó
```
docker run -d --name <nombre contenedor> --mount type=bind,source=<ruta carpeta host>,target=<ruta carpeta contenedor> <imagen>
```
- destination, dst, target: La ruta donde se monta el archivo o directorio en el contenedor.
- source, src: El origen del montaje.
  
### En tu computador crear una carpeta llamada nginx y dentro de esta carpeta crea otra llamada html. Como se aprecia en la figura.
![Volúmenes](directorio.PNG)

### Crear un contenedor con la imagen nginx:alpine, mapear todos por puertos, para la ruta carpeta host colocar el directorio en donde se encuentra la carpeta html en tu computador y para la ruta carpeta contenedor: /usr/share/nginx/html (esta ruta se obtiene al revisar la documentación de la imagen)
![Volúmenes](volumen-host.PNG)
# COMPLETAR CON EL COMANDO

```
docker run -d --name nginx-bind -p 80:80 -v C:/Users/User/Documents/CONSTRUCCION/nginx/html:/usr/share/nginx/html nginx:alpine
```

### ¿Qué sucede al ingresar al servidor de nginx?
Aparecerá una página de error 403 indicando que no se puede acceder al directorio, ya que no hay ningun index.html

### ¿Qué pasa con el archivo index.html del contenedor?
Es ocultado por el bind mount ya que al montar nuestra carpeta local vacía sobre ese directorio el contenido original queda inaccesible.

### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de tu computador en la carpeta html
### ¿Qué sucede al ingresar al servidor de nginx?
Carga el contenido del template

### Eliminar el contenedor

```
docker rm -f nginx-bind
```

### ¿Qué sucede al crear nuevamente un contenedor montado al directorio definidos anteriormente?
El template HTML sigue estando disponible y se visualiza correctamente al acceder al servidodr de nginx. Esto demuestra que los datos persisten en el sistema de archivos del host, independientemente del ciclo de vida del contenedor


