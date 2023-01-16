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


|-|usr|usr|usr|grp|grp|grp|othr|othr|othr|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|valeur binaire|1|1|1|1|1|0|1|0|0|
|valeur décimale|4|2|1|4|2|0|1|0|0|
|resultat décimale|>|7|-|-|6|-|-|4|-|
|UMASK|0|0|0|0|0|0|0|0|0|
|complément|1|1|1|1|1|1|1|1|1|


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