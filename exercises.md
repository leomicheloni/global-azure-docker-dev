# Basic

### Test docker installation

```powershell
docker run hello-world
```

### list images
```powershell
docker images

docker image ls
```
### list containers
```powershell
docker ps

### include running containers
docker ps -a
```
```powershell
docker run hello-world

docker ps -a

docker images
```
# Ports

### run tomcat locally

```powershell
docker run tomcat:latest

docker ps

docker stop [container id]
```

open port 8888 and map to por 8080 into the container using -p

```powershell
docker run -p 8888:8080 tomcat:latest

docker ps

docker stop id

docker ps 
```

> Once the container is created you cannot change ports mappings

``` powershell
docker create --name minginx -p 8080:80 nginx
``` 

execute temporaty container with --rm


```powershell
docker run --rm -p 8888:80 httpd

docker ps

docker images
```

run detached with -d
```powershell
docker run --rm -p 8888:80 -d httpd

docker ps
```

show object logs
```powershell
docker logs id

docker logs id -f

docker stop id

docker ps -a

docker rmi id
```powershell

### Identity
Every object has a unique Id

```powershell
docker run --rm -p 8888:80 httpd
docker run --rm -p 8889:80 httpd
docker run --rm -p 8890:80 httpd
```

```powershell
docker stop id1
```

#### set container name
We can set a name and reference a container by its name with --name option

```powershell
docker run --rm --name miapache -p 8888:80 httpd

docker stop miapache

docker ps -a
```
### other commands

> $(docker [list command] -q) return elements id as an array

```powershell
## stop containers
docker stop $(docker ps -q)
## remove
docker rm $(docker ps -a -q)
## remove images
docker rmi $(docker images -q)
```

```powershell
## pull an imange
docker pull nginx
```

```powershell
## create a container
docker create nginx
```
```powershell
## start an existing container
docker start minginx

docker start [container id]
```

### get object information

``` powershell
docker inspect [object id]
```


### run commands against a running container

``` powershell
docker run --name mynginx nginx

docker ps

docker exec mynginx nginx -h

docker exec mynginx nginx -v
```
``` powershell
## bash or sh depending on Linux version
docker exec -it mynginx bash

cd etc/nginx

cat nginx.conf
```

## volumenes

``` powershell
docker volume --help

docker volume ls

docker volume create --name vol1

docker volume ls

docker volume inspect vol1
```
``` powershell
docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=P@ssw0rd' -p 1433:1433 -d mcr.microsoft.com/mssql/server

docker stop id

docker rm id1
```
``` powershell
docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=P@ssw0rd' -v vol1:/var/opt/mssql/data -p 1433:1433 -d mcr.microsoft.com/mssql/server

docker stop id

docker rm id1

docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=P@ssw0rd' -v vol1:/var/opt/mssql/data -p 1433:1433 -d mcr.microsoft.com/mssql/server
```

#### directory mapping

``` powershell
docker run -p 8888:80 -d nginx

docker exec -it id bash

cd /usr/share/nginx/html

cat index.html

docker run -v c:/html:/usr/share/nginx/html -p 8888:80 -d nginx
```



## Docker Compose

docker.host.local

```yaml
version: '3.5'
services:
    image: nginx
    ports:
        - 8088:80
```

``` powershell
docker-compose up -d

docker ps

docker-compose ps

docker-compose down

docker ps

docker-compose up -d

docker-compose stop

docker ps
```

``` powershell
docker-compose start

docker-compose stop

docker-compose rm

docker-compose create

docker-compose up --no-start

docker-compose start

docker-compose stop

docker-compose rm
``` 

##### compose + volumes

``` yaml
version: '3.5'
services:
  nginx:
    image: nginx
    ports:
        - 8088:80
    volumes:
        - html:/usr/share/nginx/html
volumes:
  html:
```

``` powershell
docker-compose -f nginxv.yaml up -d
```
``` powershell
docker exec -it docker_nginx_1 bash

apt-get update
apt-get install vim
vim index.html

docker-compose -f nginxv.yaml down

docker-compose -f nginxv.yaml up -d
```


#### "Real sample"

``` yaml
version: '3.1'

services:

  wordpress:
    image: wordpress
    restart: always
    ports:
      - 8080:80
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: exampleuser
      WORDPRESS_DB_PASSWORD: examplepass
      WORDPRESS_DB_NAME: exampledb
    volumes:
      - wordpress:/var/www/html

  db:
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_DATABASE: exampledb
      MYSQL_USER: exampleuser
      MYSQL_PASSWORD: examplepass
      MYSQL_RANDOM_ROOT_PASSWORD: '1'
    volumes:
      - db:/var/lib/mysql

volumes:
  wordpress:
  db:
```


### Create images

``` powershell
code Dockerfile
```
``` dockerfile
FROM alpine
CMD ["ping","www.yahoo.com"]
```
``` powershell
## docker build creates an image from Dockerfile, the final dot (.) is the context or relative path
docker build .

docker images
```
``` powershell
## add tag or repository+tag
docker build -t yahoo .

docker images

docker run yahoo

docker logs [container id] -f

docker builf -f Dockerfilea -t imagen2 .
```

## Tags
``` powershell
docker pull alpine

docker images

docker pull alpine:3.7

docker images

docker pull alpine:3.10

docker images

Dockerfile => from alpine:3.7

docker build -t yahoo:1 .

## latest can target a newer version backguard incompatible, avoid using latest
```

> can add tags to existing images
``` powershell
docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
```

#### Create own images
``` powershell
dotnet new mvc --name myapp
## open browser
```
``` powershell
dotnet publish -o output

dotnet dll
## browse

```
> most of the time will put the publish output in our containers
``` dockerfile
mcr.microsoft.com/dotnet/aspnet:5.0
COPY output/. .
ENTRYPOINT [ "dotnet", "myapp.dll" ]
```
``` powershell
docker build -t myapp:1.0 .
```

``` powershell

docker run -p 8081:80 -e 'ASPNETCORE_URLS=http://+:81' --name myappcontainer myapp:1.0

inspect myappcontainer
```

> labels are useful for future information

``` dockerfile
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
LABEL author leomicheloni
ENV ASPNETCORE_URLS=http://+:81
EXPOSE 81
WORKDIR /app
COPY publish/. .
ENTRYPOINT [ "dotnet", "samples.dll" ]
```

#### create out compose that builds using Dockerfile

``` yaml
version: '3.5'
services:
  app:
    build:
      dockerfile: Dockerfile
      context: .
    environment:
      ASPNETCORE_URLS: http://+:5000
  proxy:
    build:
      context: .
      dockerfile: Dockerfile-nginx
    ports:
      - 88:80
```

### upload image to Azure

``` powershell
docker login lmicheloni.azurecr.io
docker tag myapp:1.0 lmicheloni.azurecr.io/myapp2:1.0
docker push lmicheloni.azurecr.io/myapp2:1.0
```






























