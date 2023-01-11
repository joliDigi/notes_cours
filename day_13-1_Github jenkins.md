# Github jenkins 

## LINUX 

/bin les commandes unix 

/dev les montages (CPU en tant que fichier, disk dur, ram, tty = terminal, ...) 

/home dossier user 

/root c'est l'admin = le super admin 

/mnt montage du disk C, ... 

/etc les configurations des prog (fstab: point de montage au boot de linux; hosts; init.d  pour démarrer les ..) 

Cmd `ifconfig` SAME AS `ipconfig` ON WINDOWS 

`ls –la` dossier caché également 

`dist upgrade` (upgrades distribution) 

`uname –a` (info linux) 

`docker inspect [container name] > [filename or path to filename]` 

## DOCKER 

Kubernetes gère des copy de conteneur 

Google, Amazon, Microsoft sont les 3 fournisseurs de VM 

Image est le "fichier docker" sans conteneur ça ne sert à rien 

Conteneur est l'espace d'execution 

### Commands : 

`docker images` (images on disk dur) 

`docker search [nom de l'image]` (docker hub sur terminal) 

`docker pull [nom de l'image]:[version]` (stock l'image sur disk dur) 

`docker rmi [nom de l'image]` (remove image + tous les conteneurs les utilisant (seulement si pas executé)) 

`docker run –ti –name=alps alpine` (si pas de tag sera latest donc ne pas oublier au cas si utilisé -ti terminal interactif –d dettached) 

`docker commit [nom du conteneur] [nom image que je donne]` (permet de faire évoluer une image de base avec nos propres install en plus) 

`docker ps` (conteneur en cours d'execution) 

`docker ps –a` (tous les conteneurs même ceux qui ne sont pas en cours d'execution) 

`docker start` (démaré un conteneur) 

`docker stop` (arrêté un conteneur) 

`docker attach [nom du conteneur]` (besoin d'être start) 

`docker inspect [nom du conteneur]` 

`docker rm [nom du conteneur]` 

`docker rm $(docker ps -aq --filtered status=exited)` (deletes everything that doesn't run) 

`docker ps -aq --filtered status=exited` (returns everything that doesn't run –aq q == container id, ) 

`docker ps -a --filtered name=alpine*` 

**VOIR LA DOC** https://docs.docker.com/engine/reference/commandline/docker/ 

### VOLUMES NOMMES

`docker volume create --name=[nom du volume]` (par defaut sur /var/lib/docker/volumes) 

`docker volume ls` 

`docker volume inspect [nom du volume]` 

`docker run –ti –v [nom du volume]:[path to volume] [nom de l'image]` 

`docker volume rm [nom du volume]` 

(On peut lier le volume à un conteneur, attach container, add files and stuff, rm container, create a new container linked to that volume, and still have access to the files) 

Example : 
```bash
docker volume create --name=/my_vol 
docker run –ti –name=myfirst –v my_vol:/someFolder alpine 
Echo "some stuff" > /someFolder/data.txt 
docker rm myfirst 
docker run –ti –name=mysnd –v my_vol:/home/otherDirectory alpine 
Cat /home/otherDirectory/data.txt 
username@laptop:/$ (returns some stuff) 
docker rm mysnd
```

### VOLUMES D'HOTES
(lie (autorise docker de considérer un dossier sur mon disk dur en tant que volume) le dossier (e.g. C:\User\...) à un volume) 

`docker run -ti -v [volume d'hôte]:[point de montage] --name=[nom]` 

`docker run -ti -v /mnt/c/Users/FORMATION/Desktop/joli_digi/datas:/datas --name=alpa alpine`

#### CREATION D'IMAGE 
#### DANS UN DOSSIER docker 

`mkdir docker`
`cd docker` 

SUR dockerfile
 
```docker
FROM alpine 
RUN apk update && apk add --no-cache \ 
Shadow bash
```

 

`docker build -t [nom image chemin dossier] .` (jolidigi/alpine:1.0 + ne pas oublier le dossier dans lequel se trouve le dockerfile) 

 

 

## ALPINE 

`apk add bash`

`apk add wget`

 

`CTR + P + Q` (Read escape sequence exit without stopping container == detached mode) 


## Droits 

 

Propiétaire  | groupe | autre | 
------------ | -----  | ----- |
w r x        | w r x  | w r x |


Lecture W | ecriture R  | execution X ||
-----     | -----       | -----       |-|
Bit 3     | Bit 2       | Bit 1       ||
4         | 2           | 1           ||
1         | 1           | 1           | 7 |
1         | 1           | 0           | 6 |
1         | 0           | 0           | 4 |

