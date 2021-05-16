# domoticz-embsys
Projet système embarqué - ENSTA Bretagne



## MISE EN PLACE DU SYSTÈME EMBARQUÉ :

Pour autoriser l’accès de root vers user pour un dossier : 
'''python
$ ls -lsa (visualiser l’appartenance des dossiers à root ou user)
$ chown -R user drivers
$ su user (changement d’utilisateur vers user)
'''


## Principe de cross-compilation :

- écrire ses programmes sur IDE
- passer les script sur docker
- créer un binaire depuis docker
- le refaire passer sur la machine locale
- transférer le binaire sur la rasp



Revenir sur docker existant :

docker ps -a
docker start ID_number
docker exec -it  ID_number /bin/bash

## Comment utiliser cp ? 

le cp commande peut être utilisée pour copier des fichiers.
Un fichier spécifique peut être copié dans le conteneur comme:

docker cp linux_userspace.c mycontainer:/ linux_userspace.c

Un fichier spécifique peut être copié DU conteneur comme:

docker cp mycontainer:/ linux_userspace.c  linux_userspace.c

Plusieurs fichiers contenus dans le dossier srcpeuvent être copiés dans le targetdossier en utilisant:

docker cp src/. mycontainer:/target
docker cp mycontainer:/src/. Target

Copier un dossier local vers un ssh :

scp -r BME280_driver/ user@172.20.11.253:/home/user/drivers


Créer le binaire à partir des fichiers .c sur docker :

./output/host/usr/bin/arm-linux-gcc /root/*.c -o linux_userspace



## FONCTIONNEMENT DU SYSTÈME EMBARQUÉ :

1) Brancher les capteurs en respectant la norme des GPIO
2) Brancher la raspberry en éthernet
3) Mettre sous tension la raspberry
4) Depuis un pc distant, executer le fichier binaire issu de la cross compilation via ssh
5) Les messages informant des données relevées par les capteurs sont affichés
   &
   La led verte clignote
   &
   La led rouge s'allume si l'humidité dépasse 40.6%
   






