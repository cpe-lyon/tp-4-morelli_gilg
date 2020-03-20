# Compte Rendu  - TP 4 - Binôme 22

13/03/2020
Thibault GILG
Clément MORELLI

## Exercice 1 : Gestion des utilisateurs et des groupes

1. Pour créer deux groupes ```groupe1``` et ```groupe2```, on exécute la commande ``` sudo addgroup groupe1``` et ``` sudo addgroup groupe2```. ``` sudo``` permet de passer en super-utilisateur et ```addgroup``` permet d'ajouter un groupe (ici groupe1 ou groupe2) au système.

2. Il faut créer 4 utilisateurs u1,u2,u3,u4 avec leurs dossiers personnels et avec bash pour shell. Pour cela, on utilise la ligne de commande ```sudo useradd ui --create-home --shell /bin/bash```  avec i = 1 ou 2 ou 3 ou 4. ```sudo``` permet de passer en super-utilisateur, ```useradd``` permet d'ajouter un utilisateur à la liste des utilisateurs, ``` --create-home``` est une option qui nous permet de créer le dossier personnel de l'utilisateur et ```--shell /bin/bash``` sélectionne le shell à utiliser pour exécuter les commandes du terminal avec le chemin que l'on passe en paramètre (ici bash).

3. Pour ajoutez les utilisateurs dans les groupes créés : 
	- u1, u2, u4 dans groupe1  
    - u2, u3, u4 dans groupe2

On utilise la commande ``` sudo usermod -a -G groupei uy  ``` avec i le numéro du groupe et y le numéro de l'utilisateur. ```sudo``` permet de passer en super-utilisateur, ``` usermod ```  modifie les fichiers d'administration des comptes du système selon les modifications qui ont été indiquées sur la ligne de commande. Dans notre cas, on ajoute les options```-a et -G```. ```-a``` permet d'ajouter l'utilisateur à la liste actuelle des groupes supplémentaires et ```-G``` est la liste de groupes supplémentaires auxquels appartient également l'utilisateur. On peut aussi utiliser ```sudo adduser uy groupei```.

4. Pour afficher les membres d'un groupe, il y plusieurs moyens. On commence par installer le paquet ```members``` avec ``` sudo apt install members```. Ainsi, on peut utiliser la commande ``` members groupe2```. De plus, on peut utiliser la commande ```cat /etc/group | grep "groupe2" ```. Ainsi, on affiche uniquement le groupe2 en recherchant groupe2 dans le contenue des /etc/group.

5. Pour faire de groupe1 le groupe propriétaire de /home/u1 et /home/u2 et de groupe2 le groupe propriétaire de /home/u3 et /home/u4, on utilise la commande ``` sudo chown :groupei /home/uy```. On peut ajouter ```-R``` pour le faire de façon récursive.

6. Pour remplacer le groupe primaire des utilisateurs : 
	- groupe1 pour u1 et u2  
    - groupe2 pour u3 et u4

On exécute la commande ``` sudo usermod -g groupei uy ```.``` sudo``` permet de passer en super-utilisateur, ``` usermod ```  modifie les fichiers d'administration des comptes du système selon les modifications qui ont été indiquées sur la ligne de commande. Dans notre cas, on utilise ```-g``` pour le groupe propriétaire.

7. Pour créer deux répertoires /home/groupe1 et /home/groupe2 pour le contenu commun aux groupes, et mettre en place les permissions permettant aux membres de chaque groupe d’écrire dans le dossier associé. On utilise la commande ``` mkdir /home/groupe1 && mkdir /home/groupe2  ``` pour créer les deux dossiers. Puis, ```chown :groupe1 groupe1 && chown :groupe2 groupe2``` pour donner accès au groupe au fichier. Et enfin, ```sudo chmod g+w groupe2 ``` de même pour groupe 1. Ainsi, on ajoute au groupe la possibilité d'écrire dedans en plus de la possibilité de lecture.

8. Pour que, dans ces dossiers, seul le propriétaire d’un fichier ait le droit de renommer  ou supprimer ce fichier, on fait la commande :
```chmod +t /home/groupe1/ && chmod +t /home/groupe2/```
Le ```+t``` correspond au "sticky bit", c'est-à-dire qu'il permet seulement au propriétaire du fichier, au propriétaire du dossier ou root de renommer ou supprimer des fichiers dans ce dossier.

9. On ne peut pas se connecter sur u1 car tout compte créé sans mot de passe est inactif, jusqu’à l’attribution d’un mot de passe.

10. Pour activer le compte de l’utilisateur u1 et se connecter, on doit créer un mot de passe. Donc, on utilise la commande. ``` sudo passwd u1 #entrer mdp``` pour crée le mot de passe. Ainsi, on peut se connecter avec ```su u1```.

11. Pour connaitre quels sont l’uid et le gid de u1, on fait ```id u1```. Cela nous donne ```uid=1001(u1) gid=1001(groupe1) groups=1001(groupe1)```.

12. On trouve que l'uid1003 appartient à u3.

13. Pour connaitre quel est l’id du groupe groupe1 on fait ```cat /etc/groupe | grep groupe1```, on obtient 1001.

14. C'est le groupe2 qui a pour guid 1002.

15. Avec ``` sudo gpasswd -d u3 groupe2  ``` on supprime l'utilisateurs u3 du groupe2 donc il ne peut plus accéder à /home/groupe2 ce qui est logique car il ne fait plus partie du groupe 2.

16. Voici les commandes pour effectuer les changements suivants :  
— il expire au 1er juin 2020 : ```usermod --expiredate 06/01/2019 u4  ```
— il faut changer de mot de passe avant 90 jours : ```sudo chage -M 90 u4  ```
— il faut attendre 5 jours pour modifier un mot de passe :```sudo chage -m 5 u4  ```
— l’utilisateur est averti 14 jours avant l’expiration de son mot de passe : ```sudo chage -W 14 u4  ```
— le compte sera bloqué 30 jours après expiration du mot de passe : ```sudo chage -I 30 u4```.

17. On utilise la commande ``` echo $SHELL``` on trouve /bin/bash donc c'est le bash.

18. Nobody est un utilisateur à qui aucun fichier n'appartient, qui n'est dans aucun groupe qui a n'a pas de privilèges et dont les seules possibilités sont celles que tous les autres utilisateurs ont.

19. Par défaut, le mot de passe est gardé en mémoire pendant 15 minutes. Pour forcer l'oubli on tape la commande commande ```sudo -k```.

## Exercice 2

1. Pour effectuer ces opérations, nous avons du taper les commandes suivantes :
```
cd $HOME
mkdir test
cd test
nano fichier
```
Ensuite, pour connaître les droits sur des éléments (fichier ou dossier), on utilise la commande : ``` ls -l ```. 

Cette dernière nous renvoie la ligne suivante pour ```fichier``` :
```
-rw-r--r-- 1 thibault thibault 76 mars  13 14:25 fichier
```
Ainsi, cela veut dire que pour ```fichier```, l'utilisateur propriétaire a les droits de lecture et d'écriture, et que le groupe et les autres utilisateurs ont les droits de lecture.

La commande nous renvoie la ligne suivante pour ```test``` : 
```
drwxr-xr-x  2 thibault thibault 4096 mars  13 14:25  test
```
Ainsi, cela veut dire que pour ```test```, l'utilisateur propriétaire et le groupe ont les droits de lecture, d'écriture et d'accès, et que les autres utilisateurs ont les droits de lecture et d'accès.

2. D'abord, on retire tous les droits avec la commande ```chmod 000 fichier ```. Ensuite, pour passer en utilisateur ```root```, il faut exécuter la commande ```su```, entrer le mot de passe s'il y en a un. Ainsi, pour afficher son contenu, on exécute la commande ```cat fichier``` et on le modifie avec ```nano```. Les deux opérations fonctionnent avec l'utilisateur ```root```. C'est normal car le ```root``` est un super-utilisateur : il possède toutes les permissions d’administration
du système.

3. Pour redonner les droits en écriture et exécution à l'utilisateur  sur fichier```fichier```, on exécute la commande ```chmod u+wx fichier```. La commande suivante ```echo "Hello" > fichier``` remplace le contenu du fichier par "Hello". On voit que l'utilisateur a bien récupéré son droit d'écriture.

4. Lorsqu'on essaye d'exécuter le fichier avec la commande ```./fichier```, la console nous renvoie ```bash: ./fichier: Permission non accordée``` car l'utilisateur ne dispose pas du droit d'exécution sur le fichier. On ne peut pas l'exécuter en tant qu'utilisateur simple. Autrement, on aurait ```x``` dans les droits du fichier.
Lorsqu'on tente d'exécuter le fichier en tant que super-utilisateur avec la commande ```sudo ./fichier```, la console nous renvoie : ```sudo: ./fichier : commande introuvable```. Cela ne fonctionne pas car l'exécution est la seule opération qui n'est pas possible pour un utilisateur si elle n'est pas autorisée dans les droits du fichier.

5. On retire le droit d'écriture du dossier ```test```, ainsi avec la commande ```ls```, il est impossible d'afficher le contenu du dossier. La console renvoie ```ls: impossible d'ouvrir le répertoire '.': Permission non accordée```. Si le fichier a le droit d'exécution et de lecture, alors il est possible de l'exécuter et d'en afficher le contenu. Les droits du fichier restent inchangés malgré tout.

6. Après avoir retiré les droits d'écriture du répertoire ```test``` et du fichier ```nouveau```  avec la commande ```chmod u-w``` qu'il contient, avec la commande ```chmod ugo-w```, il est impossible de modifier ce fichier car nous n'avons pas la permission. Une fois de plus, même après avoir rétabli les droits d'écriture au répertoire, on ne peut modifier ou supprimer le fichier ```nouveau``` car on n'a pas le droit d'écriture. On en conclut qu'un fichier est indépendant en écriture des droits de son répertoire.

7. On retire le droit en exécution du répertoire ```test``` avec la commande ```chmod u-x test```. Les opérations de manipulation des fichiers au sein du répertoire sans droit d'exécution, ainsi que l'accès à ce répertoire sont impossibles. En revanche, il est possible de lister le contenu du répertoire. Le droit en exécution pour les répertoires correspond à l'accès au répertoire et à tout ce qu'il contient.

8. On rétabli le droit en exécution du répertoire ```test``` avec la commande ```chmod u+x test```. Pour modifier les permissions du dossier, alors qu'on se trouve dedans avec  le terminal, il n'est pas possible, donc nous avons modifié les paramètres avec l'interface graphique *Fichier*. Une fois les droits d'exécution supprimés, il est impossible de lister le contenu du répertoire, de modifier, créer, supprimer un fichier ou répertoire mais également de se déplacer dans le répertoire ```sstest``` et de lister son contenu. Cependant, il est possible de retourner au répertoire précédent qui est le répertoire courant avec la commande ```cd ..```.

9. On rétabli le droit en exécution du répertoire ```test``` avec la commande ```chmod u+x test```. Si l'on souhaite que les autres personnes du groupe aient les droits de lecture mais pas d'écriture (ni d'exécution), il faut rentrer la commande ```chmod 740 fichier```. Ceux qui ne font pas partie du groupe n'auront aucun droit sur le fichier.

10. Pour définir un umask très restrictif qui interdit à quiconque à part le propriétaire l’accès en lecture et en écriture et la traversée de nos répertoires, il faut exécuter la commande ```umask 077```. Si l'on exécute la commande ```umask -S```, on aura bien ```u=rwx,g=,o=``` Ainsi, cela modifie l'umask avec tous les droit au propriétaire et aucun aux autres pour la création de nouveaux répertoires et fichiers. 

On peut le voir si on crée un nouveau fichier. En effet, le masque est appliqué par une fonction AND NOT sur la valeur 666 pour un fichier. Ainsi, le droit d'exécution n'est pas présent pour un fichier.
```
thibault@thibault-gilg:~/test$ touch nouveau_fichier
thibault@thibault-gilg:~/test$ ll nouveau_fichier 
-rw------- 1 thibault thibault 0 Mar 17 16:27 nouveau_fichier
```
On peut le voir si on crée un nouveau répertoire. En effet, le masque est appliqué par une fonction AND NOT sur la valeur 777 pour un répertoire. Ainsi, le propriétaire possède le droit d'accès sur les nouveaux répertoires. La dernière ligne correspond aux droits du répertoire parent qui restent inchangés comme il a été créé précédemment.
```
thibault@thibault-gilg:~/test$ mkdir nouveau_répertoire
thibault@thibault-gilg:~/test$ ll nouveau_répertoire/
total 8
drwx------ 2 thibault thibault 4096 Mar 17 16:33 ./
drwxr-xr-x 4 thibault thibault 4096 Mar 17 16:33 ../
```

11. Pour définir un umask très permissif qui autorise tout le monde à lire nos fichiers et traverser nos répertoires, mais n’autorise que le propriétaire à écrire, on exécute la commande ```umask 022``` et ensuite on vérifie que l'on ait bien choisi le masque adéquat : 
```
thibault@thibault-gilg:~$ umask -S
u=rwx,g=rx,o=rx
```
On peut le voir si on crée un nouveau fichier. En effet, le masque est appliqué par une fonction AND NOT sur la valeur 666 pour un fichier. Ainsi, le droit d'exécution n'est pas présent pour un fichier.
```
thibault@thibault-gilg:~/test$ touch nouveau_fichier
thibault@thibault-gilg:~/test$ ll nouveau_fichier 
-rw-r--r--1 thibault thibault 0 Mar 17 16:36 nouveau_fichier
```
On peut le voir si on crée un nouveau répertoire. En effet, le masque est appliqué par une fonction AND NOT sur la valeur 777 pour un répertoire. Ainsi, le propriétaire possède le droit d'accès sur les nouveaux répertoires. La dernière ligne correspond aux droits du répertoire parent qui restent inchangés comme il a été créé précédemment.
```
thibault@thibault-gilg:~/test$ mkdir nouveau_répertoire
thibault@thibault-gilg:~/test$ ll nouveau_répertoire/
total 8
drwxr-xr-x 2 thibault thibault 4096 Mar 17 16:39 ./
drwxr-xr-x 5 thibault thibault 4096 Mar 17 16:39 ../
```

12. Pour définir, un umask équilibré qui autorise un accès complet au propriétaire et autorise un accès en lecture aux
membres du groupe, on exécute la commande ```umask 037``` et ensuite on vérifie que l'on ait bien choisi le bon masque adéquat : 
```
thibault@thibault-gilg:~/test$ umask -S
u=rwx,g=r,o=
```
On peut le voir si on crée un nouveau fichier. En effet, le masque est appliqué par une fonction AND NOT sur la valeur 666 pour un fichier. Ainsi, le droit d'exécution n'est pas présent pour un fichier.
```
thibault@thibault-gilg:~/test$ touch nouveau_fichier
thibault@thibault-gilg:~/test$ ll nouveau_fichier 
-rw-r----- thibault thibault 0 Mar 17 16:45 nouveau_fichier
```
On peut le voir si on crée un nouveau répertoire. En effet, le masque est appliqué par une fonction AND NOT sur la valeur 777 pour un répertoire. Ainsi, le propriétaire possède le droit d'accès sur les nouveaux répertoires. La dernière ligne correspond aux droits du répertoire parent qui restent inchangés comme il a été créé précédemment.
```
thibault@thibault-gilg:~/test$ mkdir nouveau_répertoire
thibault@thibault-gilg:~/test$ ll nouveau_répertoire/
total 8
drwxr-xr-x 2 thibault thibault 4096 Mar 17 16:39 ./
drwxr-xr-x 6 thibault thibault 4096 Mar 17 16:39 ../
```

13. 
* La notation octale correspondante est ```chmod 534 fic```. Lorsqu'on vérifie avec la commande ```stat fic```, qui affiche les caractéristiques système de ```fic```, on obtient :
```
  Fichier : fic
   Taille : 0         	Blocs : 0          Blocs d'E/S : 4096   fichier vide
Périphérique : 808h/2056d	Inœud : 1073530     Liens : 1
Accès : (0534/-r-x-wxr--)  UID : ( 1000/thibault)   GID : ( 1000/thibault)
Accès : 2020-03-17 17:13:52.328313330 +0400
Modif. : 2020-03-17 17:13:52.328313330 +0400
Changt : 2020-03-17 17:15:09.949588676 +0400
  Créé : -
```
La ligne ```Accès : (0534/-r-x-wxr--)``` met en évidence que la conversion octale est bonne.

* La commande ```chmod uo+w,g-rx``` correspond à ajouter le droit d'écriture à l'utilisateur et à l'autre, et à supprimer les droits d'écriture et d'exécution aux personnes du groupe. Sachant que les droits initiaux de fic sont ```r--r-x---```, cela doit devenir ```rw-----w-```. En octal, cela donne ```chmod 602 fic```. On vérifie et on obtient bien ```Accès : (0602/-rw-----w-)```.

* La commande ```chmod 653 fic``` correspond à attribuer les droits d'écriture et de lecture à l'utilisateur, les droits de lecture et d'exécution au groupe et les droits d'écriture et d'exécution à l'autre. Sachant que les droits initiaux de fic sont ```711```, avec la notation classique, on doit exécuter la commande ```chmod u-x,g+r,o+w fic```. On vérifie et on obtient bien ```Accès : (0653/-rw-r-x-wx)```.

* La commande ```chmod u+x,g=w,o-r fic``` correspond à ajouter le droit d'exécution à l'utilisateur, à définir uniquement un droit d'utilisation au groupe et à supprimer le droit de lecture à l'autre. Sachant que les droits initiaux de fic sont ```r--r-x---```, cela doit devenir ```r-x-w----```. En octal, cela donne ```chmod 520 fic```. On vérifie et on obtient bien ```Accès : (0520/-r-x-w----)```.

14. On affiche les droits du fichier ```passwd``` avec la commande ```stat /etc/passwd```, avec le chemin complet. On obtient : ```Accès : (0644/-rw-r--r--)```. Ainsi, le sticky bit est désactivé, c'est-à-dire qu'il n' y a pas que le propriétaire d’un fichier, le propriétaire du dossier ou root qui ont le droit de
renommer ou supprimer ce fichier.  De plus, pour le fichier ```passwd```, le propriétaire dispose des droits d'écriture et de lecture, le groupe et l'autre du droit de lecture.

