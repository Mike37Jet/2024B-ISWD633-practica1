# Contenedores

### Crear un contenedor
Para crear un nuevo contenedor Docker a partir de una imagen específica, pero sin iniciarlo automáticamente. 

```
docker create --name <nombre contenedor> <nombre imagen>:<tag>
```
Crear el contenedor  **srv-web** usando la imagen nginx version alpine

```
docker create --name srv-web nginx:alpine
```

Si creas un contenedor en Docker sin asignarle un nombre específico utilizando la opción --name, Docker asignará automáticamente un nombre aleatorio al contenedor. Este nombre suele consistir en una combinación de palabras y números.  

Crear el contenedor usando la imagen hello-world

```
docker create hello-world:latest
```

### Listar los contenedores ejecutándose o no

```
docker ps -a
```

### Para iniciar un contenedor

```
docker start <nombre contenedor o identificador>
```
Iniciar el contenedor srv-web 

```
docker start srv-web
```

### Listar los contenedores ejecutándose
```
docker ps 
docker ps | grep <nombre contenedor>
```

### Para detener un contenedor

```
docker stop <nombre contenedor>
```

### Para crear un contenedor y ejecutarlo inmediatamente

```
docker run --name <nombre contenedor> <nombre imagen>:<tag>
```
![Ecosistema de Docker](img/dockerRun.PNG)

Crear y ejecutar inmediatamente el contenedor **srv-web2** usando la imagen nginx:alpine

```
docker run --name srv-web2 nginx:alpine
```

**¿Qué sucede luego de la ejecución del comando?**

```
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh       
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2024/10/15 13:07:40 [notice] 1#1: using the "epoll" event method
2024/10/15 13:07:40 [notice] 1#1: nginx/1.27.2
2024/10/15 13:07:40 [notice] 1#1: built by gcc 13.2.1 20240309 (Alpine 13.2.1_git20240309)  
2024/10/15 13:07:40 [notice] 1#1: OS: Linux 5.15.153.1-microsoft-standard-WSL2
2024/10/15 13:07:40 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2024/10/15 13:07:40 [notice] 1#1: start worker processes
2024/10/15 13:07:40 [notice] 1#1: start worker process 30
2024/10/15 13:07:40 [notice] 1#1: start worker process 31
2024/10/15 13:07:40 [notice] 1#1: start worker process 32
2024/10/15 13:07:40 [notice] 1#1: start worker process 33
2024/10/15 13:07:40 [notice] 1#1: start worker process 34
2024/10/15 13:07:40 [notice] 1#1: start worker process 35
2024/10/15 13:07:40 [notice] 1#1: start worker process 36
2024/10/15 13:07:40 [notice] 1#1: start worker process 37
2024/10/15 13:07:40 [notice] 1#1: start worker process 38
2024/10/15 13:07:40 [notice] 1#1: start worker process 39
2024/10/15 13:07:40 [notice] 1#1: start worker process 40
2024/10/15 13:07:40 [notice] 1#1: start worker process 41
```

Cuando ejecutas un contenedor en primer plano sin la opción -d (modo detach), el contenedor captura la entrada estándar (stdin) del terminal, lo que significa que el terminal queda "atrapado" y no puedes introducir más comandos hasta que detengas el contenedor.

### Para crear un contenedor y ejecutarlo inmediatamente sin estar vinculados al mismo
-d: Es la opción que indica a Docker que ejecute el contenedor en segundo plano (en modo "detach").
Cuando un contenedor se ejecuta en segundo plano, Docker devuelve el control al terminal inmediatamente después de iniciar el contenedor, lo que permite al usuario seguir ejecutando otros comandos en el mismo terminal sin que el contenedor detenga la interacción.

```
docker run -d --name <nombre contenedor> <nombre imagen>:tag
```
Crear y ejecutar inmediatamente el contenedor **srv-web3** en modo detach usando la imagen nginx:alpine

```
docker run -d --name srv-web3 nginx:alpine
```

### Para eliminar un contenedor

```
docker rm <nombre contenedor>
```
Eliminar el contenedor que se creó a partir de la imagen hello-world 

```
docker rm intelligent_wing
```

Verificar que el contenedor que se eliminó

```
PS C:\Users\migue> docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS           
          PORTS     NAMES
6746d386b8e4   nginx:alpine   "/docker-entrypoint.…"   3 minutes ago    Up 3 minutes               80/tcp    srv-web3
e18d6e7dabaa   nginx:alpine   "/docker-entrypoint.…"   9 minutes ago    Exited (0) 4 minutes ago             srv-web2
52303cc0da5a   nginx:alpine   "/docker-entrypoint.…"   23 minutes ago   Up 12 minutes              80/tcp    srv-web
```

### Para eliminar un contenedor que esté ejecutándose

```
docker rm -f <nombre contenedor>
```
Eliminar el contenedor **srv-web3** 

```
docker rm -f srv-web3
```

Verificar que el contenedor que se eliminó

```
PS C:\Users\migue> docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS           
          PORTS     NAMES
e18d6e7dabaa   nginx:alpine   "/docker-entrypoint.…"   11 minutes ago   Exited (0) 6 minutes ago             srv-web2
52303cc0da5a   nginx:alpine   "/docker-entrypoint.…"   24 minutes ago   Up 14 minutes              80/tcp    srv-web
```

### Para inspecionar un contenedor 

Inspeccionar el contenedor **srv-web** 

```
docker inspect srv-web
```
