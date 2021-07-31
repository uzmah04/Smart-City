# Smart-City
Projet Smart City : Code pour la partie Control d'Acces (ROS)

Ce projet consiste à donner l'état de deux barrières dans un objet JSON à l'interface Web developper en utilisant le Rosbridge.
Ce repository contient les fichiers d'un package. Il y a :
- CMakeLists.txt
- package.xml
- src -- qui contient le fichier qui va afficher l'état des barrières
- srv -- qui contient le fichier service qui va préciser le type de données comme request et response

Pour utiliser ce programme, il faut avoir les outils ROS et un workspace avec les dossiers build, devel, logs et src.
Exemple : nom de mon workspace -> catkin_ws
```sh
        $ cd ~/catkin_ws/src
```
Dans le dossier src du workspace, il faut cloner ce repository.
```sh
        $ git clone https://github.com/uzmah04/Smart-City
```
Il faut ensuite faire:
```sh
        $ catkin build
```
Dans le dossier catkin_ws/src, il faut faire:
```sh
        $ source ../devel/setup.bash
```

## Pour lancer le programme
> Ouvrir un terminal et executer la commande roscore
```sh
        $ roscore
```
> Ouvrir un autre terminal sans fermer le precedent et lancer le programme dans src
> ### Le nom du package est udm_service.
```sh
        $ source ~/catkin_ws/devel/setup.bash
        $ rosrun udm_service udm_service_server.py
```
> Garder les deux terminals ouverts et ouvrez un autre pour voir les données en JSON affichés
```sh
        $ rostopic echo /access_state
```

Ainsi le programme est lancé.

## Pour changer l'état des barrières
Dans ce projet, il y a que deux barrières qui ont access_id 1 et 2.
Chaque barrière a deux états, 1 pour dire que la barrière est ouverte et 2 quand la barrière est fermer.
Pour changer les états des barrières, il faut s'en servir du service.
> Garder les trois autres terminals ouverts et ouvrir un autre pour faire appel au service
```sh
        $ rosservice call /udm_service_server 
```
> Et presser sur la touche Tab
> On va obtenir:
```sh
        $ rosservice call /udm_service_server "access_id:
          data: 0
        state:
          data: 0"
```
> Il faut changer les '0' en 1 ou 2. Par exemple, pour dire que la première barrière est ouverte, il faut changer comme suite.
```sh
        $ rosservice call /udm_service_server "access_id:
          data: 1
        state:
          data: 1"
```
> Ainsi, la valeur va changer das le terminal ou la commande 'rostopic echo /access_state' avait été éxecutée.
