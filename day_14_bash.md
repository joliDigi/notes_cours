# Linux - bash

- Gnome, KDE
- noyau Linux programmé en C

Info du noyau:

```sh
uname -a
```

manual of [command]

```sh
man uname
```

seul un admin (root) peut installer, en utilisant `sudo`

`apt` est le gestionnaire de package sur distribution Debian

`apk` est le gestionnaire de package sur distribution Alpine

Trouver une command

```sh
whereis wget
```

## les dossiers linux

`/bin` folder contenant les commandes

`/dev` communiquer avec les peripheriques (info materiels)

`sda` disk dur

`/mnt` ce qui est monté (périphérique en fonctionnement)

`/lib` les bibliothèques qui servent ... (python)

`/tmp` les files temp

`/proc` processus en cours d'execution

`/usr` disponible à tous

`/usr/bin` commandes pour l'utilisateur

`/home` le home de tous les utilisateurs

`/sbin` commandes de l'admin

`/usr/sbin` commandes de l'admin pour le user (pratiquement plus utilisé, vide)

`/usr/local` application accessibles à tous

`/etc/fstab` fichier point de montage

(`fsck` permet de vérifier les disk)

ext4 est que sous unix et très rapide

windows est plus lent car pas continu

Dans Linux tout est fichier

## Les commandes Unix

`cd` dans un container -> / dans unix -> /home/[current user]

`cat [fichier]` lire le fichier

`rm [fichier]` supprimer le fichier

`cp [path to fichier src] [path to fichier dest]` copier le fichier

`mkdir` create folder

`mv [fichier] [folder]` move file to folder

`rm -r [folder]` supprimer le folder et les files dedans -r recursive

`rmdir` delete empty folder ONLY

`echo bonjour`

`echo bonjour > bj.txt` ecrit dans un fichier

## Les droits

`ls -l` montre les droits

droit par defaut (user, group, others) :

- 755 pour les dossiers
- 644 pour les files

```sh
umask 0
mkdir [foldername]
```

umask change les droits par defaut (inverse de ce que l'on veut)
[foldername] se retrouve avec des droits 777 par defaut

```sh
umask 022
mkdir [foldername]
```

[foldername] se retrouve avec des droits 755 par defaut

|         -         | usr | usr | usr | grp | grp | grp | othr | othr | othr |
| :---------------: | :-: | :-: | :-: | :-: | :-: | :-: | :--: | :--: | :--: |
|  valeur binaire   |  1  |  1  |  1  |  1  |  1  |  0  |  1   |  0   |  0   |
|  valeur décimale  |  4  |  2  |  1  |  4  |  2  |  0  |  1   |  0   |  0   |
| resultat décimale |  >  |  7  |  -  |  -  |  6  |  -  |  -   |  4   |  -   |
|       UMASK       |  0  |  0  |  0  |  0  |  0  |  0  |  0   |  0   |  0   |
|    complément     |  1  |  1  |  1  |  1  |  1  |  1  |  1   |  1   |  1   |

## les scripts bash

```sh
nano firstscript.sh

#!/bin/bash
# commentaire
echo 'hello'
if true; then
    echo 'yes'
fi

chmod +x firstscript.sh
./firstscript.sh
```

## variables, conditions

`read A` attends une entrée pour assigner dans une variable A

`echo $A` lire la variable

`val=[string]` variable

`test -s [file] ` est-ce-que le fichier existe ?

`test -d [folder] ` est-ce-que le dossier existe ?

`test -z [variable avec read] ` est-ce-que la chaine est vide ?

`test [ $variableA = $variableB ]` est-ce-que les chaines sont égale ?

`test $nbA -eq $nbB` est-ce-que les nombres sont égaux ?

`test $nbA -ne $nbB` est-ce-que les nombres sont différents ?

`test $nbA -gt $nbB` est-ce-que A est > B ?

`test $nbA -lt $nbB` est-ce-que A est < B ?

`test $nbA -ge $nbB` est-ce-que A est >= B ?

`test $nbA -le $nbB` est-ce-que A est <= B ?

OR condensed

`if [ $nbA -eq $nbB ]`

### AND, OR

`test -d folder -a -x folder` repertoire exist ET en écriture

`test -d folder -o -x folder` repertoire exist OU en écriture

`if [ $nbA -eq 1 -a $nbB -eq 2 ]`

### case in condition

```sh
case $A in
    pattern1)
        echo 'hi'
        ;;
    pattern2)
        echo 'hello'
        ;;
    *)
        echo '...'
    ;;
esac
```

### for in loop

```sh
for i in 1 2 3
do
    echo $i
done
```

### while loop

```sh
while read val
do
    echo $val
done
```

```sh
val="1 2 3 4" # tableau en bash

for i in $val
do
    echo $i
done
```

### concat

```sh
a=1
b=2
c=$a$b
echo $c # 12

d=$a" plus "$b" égale pas 3 mais concat "$c
echo $d
```

```sh
var="hi"
bash # ouvre un nouveau terminal dans le terminal courant
echo $var # ne connais pas la variable
exit # retourne sur le terminal d'origine
export $var
bash
echo $var # connais la variable
exit
```

```sh
echo $HOME
echo $PATH
echo $PS1 # le shell courant le prompt primaire
echo $LOG1 # user courant
echo $PWD # working directory
printenv # affiche toute les variables d'environnement
env # toutes les variables positionnées
```

```sh
cd /tmp
wget -O google.txt google.com
mv /tmp/google.txt $PWD/google.html
rm google.txt
```

```sh
cd /tmp
wget https://wordpress.org/latest.zip
unzip latest.zip
mv wordpress $HOME
rm latest.zip
```

## Ajouter un script en tant que commande

```sh
nano commande

#! /bin/bash
echo toto

chmod +x commande

echo $PATH # peut pas lire notre commande
ls -l /usr/local/bin # besoin d'être root

sudo mv commande /usr/local/bin
commande # toto
sudo mv /usr/local/bin/commande ./

commande # command 'commande' not found

cat > ma_pro
ls /toto
ERR=$? # erreur de la dernière commande, numeric argument
# ERR=$$ # processus courant -> NOT SURE
if [ $ERR -ne 0 ]; then
    exit $ERR" ceci est une erreur"
else
    echo ok
fi

chmod +x ma_proc
./ma_proc # affiche l'erreur
```

```sh
$0 # nom de la procedure en cours
$1 # argument 1 paramètre positionel
$* # tous les paramètres
$# # nombre de paramètres

$$ # PID id number

# affiche les param
for i
    do echo $i
    done

mkdir toto

var=$(ls)
for i in $var
    do
        if [ $i = toto ]; then
            rm -r toto
        fi
    done
```

```sh
echo `ls` # print what cmd returns -> executes
```

```sh
A="Bob"
echo "hello there $A" # lis la variable entre double quote
```

## TP bash

Créer un script bash qui:

- vérifie qu'un répertoire documents existe
- si le répertoire existe : on affiche "le répertoire documents" existe
- sinon, on créé le répertoire

```sh
ls | sort # ordre abc

ls | grep g # g présent dans file ou folder name

ls | while read FICH; do
    echo $FICH
done

ls | while read FICH; do
    if [ -f $FICH ]; then
        rm $FICH
    fi
done

echo bonjour > texte.txt

# supprime tous les fichiers et dossiers
ls | while read FICH; do
    if [ -f $FICH ]; then
        if [ -x $FICH ]; then
            echo $FICH" executable non supprimable"
        fi
        rm $FICH
    fi
    if [ -d $FICH ]; then
        rm -r $FICH
    fi
done
```

```sh
ls | while read FICH; do
    if [ -f $FICH ]; then
        if [ -x $FICH ]; then
            echo $FICH" executable non supprimable"
        else
            echo "delete ? Y/n"
            confirm=$(bash read confirm)
            echo $confirm
        fi
        rm $FICH
    fi
    if [ -d $FICH ]; then
        rm -r $FICH
    fi
done
```

**/!\ YOU HAVE RIGHTS, TAKE BACK CONTROL /!\\**

```sh
sudo umount /mnt/c

sudo mount -t drvfs C: /mnt/c -o metadata,uid=1000,gid=1000,umask=22,fmask=133
```

## crontab

`sudo su` root definitivement, `exit` pour quitter

`var/spool/cron/crontabs` dossier pour fichier cron

`crontab -e` runs tasks, installs new cron tab named root

`nano root`

minute | hour | day_of_month | month | day_of_week | command_to_run

`0 5 * * 1 wget google.com` new task added

`crontab -l` view the contents of your crontab
