# Exo-DEVOPS


EXO DEV ops 

Exo 1

1.1
 
1.2<img width="945" height="130" alt="image" src="https://github.com/user-attachments/assets/bdac9811-c888-4267-b506-a19a2cf870cc" />

 
1.3
Vérification que le conteneur est bien en cours d’exécution avec la commande docker ps.
Cette commande permet de lister uniquement les conteneurs actifs.
 
1.4
 
La page par défaut de Nginx s’affiche, ce qui confirme que le conteneur fonctionne correctement et que le port est bien exposé.
1.5
 
1.6
 
La différence avec docker ps est que docker ps -a affiche aussi les conteneurs arrêtés.
1.7
 
1.8
Pour que le conteneur soit automatiquement supprimé à l’arrêt, il aurait fallu utiliser l’option --rm lors du lancement.
Commande correspondante : docker run --rm -d --name mon-nginx -p 8080:80 nginx:alpine






EXO 2
2.1
Création du fichier index.html avec une structure HTML minimale, contenant le titre “Ma première image Docker” et un titre principal <h1> avec mon prénom.
 
2.2
Création d’un Dockerfile basé sur l’image nginx:alpine.
Le fichier copie index.html dans /usr/share/nginx/html/index.html et expose le port 80.
 
2.3
 
2.4
  



2.5
Affichage de la liste des images locales avec docker images.  
La taille de l’image mon-site:v1 est très proche de celle de nginx:alpine, car seule une petite page HTML a été ajoutée.

2.6
  
On observe qu’une nouvelle couche a été ajoutée par rapport à l’image de base, correspondant à la copie du fichier index.html dans le dossier web de Nginx.
2.7
Lors de la reconstruction de l’image mon-site:v2, l’image de base nginx:alpine a été récupérée depuis le cache. En revanche, l’étape de copie du fichier index.html a été rejouée car son contenu avait changé.
 
2.8
 

Exo 3

3.1
J’ai lancé un conteneur alpine en mode interactif avec l’option --rm. A l’intérieur, j’ai créé le fichier /data/test.txt avec le contenu bonjour. Après avoir quitté le conteneur puis relancé un nouveau conteneur alpine, le fichier n’existait plus. Cela montre que les données écrites directement dans le conteneur ne sont pas conservées après sa suppression 
3.2

J’ai créé un dossier exercice-3/html/ sur ma machine avec un fichier index.html. J’ai ensuite lancé un conteneur nginx:alpine . Après avoir modifié le fichier index.html sur ma machine, le changement est apparu directement dans le navigateur sans redémarrer le conteneur. J’en conclus que le conteneur utilise directement les fichiers présents sur l’hôte.

 
 

3.3
 
3.4
 
3.5
j’ai ensuite lancé un nouveau conteneur alpine en montant le même volume mes-donnees sur /data. Le fichier /data/persistant.txt était toujours présent. Cela démontre que les données stockées dans un volume nommé persistent même après la suppression du conteneur précédent.
 

3.6
J’ai listé les volumes Docker existants avec docker volume ls, puis j’ai inspecté le volume mes-donnees avec docker volume inspect mes-donnees. Cela m’a permis de voir que le volume est stocké physiquement par Docker sur la machine hôte, dans son espace de stockage interne
 
 





3.7
J’ai supprimé le volume mes-donnees avec la commande docker volume rm mes-donnees. Avant de supprimer un volume, il faut vérifier qu’il ne contient pas encore de données importantes, car cette suppression entraîne leur perte définitive.
 

Exo 4
