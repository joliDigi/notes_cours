# Day 2 docker volume

## Volume anonyme

**busybox** est le noyau le plus léger avec seulement les commandes de bases

`docker run --name=[nom de conteneur] -v [nom de dossier] busybox true` (volume anonyme créé automatiquement, nom de dossier qui sera ajouté au conteneur d'accès ci-dessous, busybox a besoin de la command true)

`docker run -ti --name=[nom de conteneur] --volumes-from=[nom du conteneur busybox] [nom de l'image]` (lier un conteneur au volume anonyme (sous le nom de son conteneur backup))

_Example :_

`docker run --name=backup -v /datas busybox true` (volume anonyme créé automatiquement)

`docker run -ti --name=alpine_bb --volumes-from=backup alpine` (lier un conteneur au volume anonyme (sous le nom de son conteneur backup))

`docker ps -a`

|CONTAINER ID|IMAGE|COMMAND|CREATED|STATUS|PORTS|NAMES|
|-|-|-|-|-|-|-|
39893448cf27|busybox|"true"|16 minutes ago|Exited (0) 16 minutes ago||backup|

`docker volume ls`

|DRIVER|VOLUME NAME|
|-|-|
|local|0d3d4b64d59649cae9367ee2f9b3a62a9e0c6c5b09a8270d1b073c581b11994d|


## Volume dans dockerfile

```dockerfile
FROM alpine
RUN mkdir /datas
RUN echo "hello" > /datas/msg.txt
VOLUME /datas
```

`docker build -t message:1.0 .`

Avec dockerfile les volumes ne sont QUE anonymes !

**_Aparte :_** `df -h`


## La mise en réseau

`docker network ls`

_Example :_

```bash
docker run -dti --name=alpo0 alpine
docker run -dti --name=alpo1 alpine
docker attach alpo0

ifconfig
ping [addr]

(ctrl+P+Q)

docker attach alpo1
ifconfig
ping [addr]
```

`docker network inspect [ID du network]`

dans un conteneur on peut accéder à un résea à l'exterieur

par defaut, les conteneurs sont sur le même réseau

On peut créer un réseau bridge indépendent

```bash
docker network create --driver=bridge [nom du reseau]
docker network inspect [nom du reseau]

docker run -dti --net [nom du reseau] --name=[nom du conteneur] alpine (first container same network)
docker run -dti --net [nom du reseau] --name=[nom du conteneur] alpine (snd container same network)

ping [nom du reseau] (first) (il sont pas sur le même reseau et fournit la résolution de nom)

docker network ls
docker network inspect [nom du reseau]
```

Ajouter un conteneur déjà créé à un réseau
```bash
docker network connect [nom du reseau] [nom du conteneur] (third container same network)

docker network disconnect [nom du reseau] [nom du conteneur]
```

**_Aparte :_**
```
arp -a
traceroute google.com
```

## PORT

PAT : Port Address Translation
[port de l'hôte]:[port du conteneur]

```bash
docker network create web
docker run -dti --net web --name=commanche -p 8181:80 httpd
docker run -ti --net web --name=huron alpine

docker run -dti --net web --name=apache -p 8080:80 -v [some_directory]:/usr/local/apache2/htdocs httpd
```

```bash
docker run -d --net web --name=maria_db --env MARIADB_USER=jolidigi --env MARIADB_PASSWORD=mariapassdb
 --env MARIADB_ROOT_PASSWORD=mariapassroot mariadb:latest


 docker attach []
 apk add mariadb-client
```

```mysql
mysql -u root -h maria_db -p
******(password)
```

