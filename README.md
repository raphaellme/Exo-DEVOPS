# Exo-DEVOPS


EXO DEV ops 

Exo 1

1.1<img width="945" height="297" alt="image" src="https://github.com/user-attachments/assets/b44a8cf9-096b-4b1a-9a1c-338cf8ffd805" />

 
1.2<img width="945" height="43" alt="image" src="https://github.com/user-attachments/assets/a0c8703d-417f-4a13-a394-0cbee65ffbfe" />


 
1.3<img width="945" height="124" alt="image" src="https://github.com/user-attachments/assets/c6839802-bfac-41ce-a153-222a82f1b901" />

Vérification que le conteneur est bien en cours d’exécution avec la commande docker ps.
Cette commande permet de lister uniquement les conteneurs actifs.
 
1.4<img width="945" height="397" alt="image" src="https://github.com/user-attachments/assets/1f1f231e-abc3-44b7-9baa-598c04613d7c" />

 
La page par défaut de Nginx s’affiche, ce qui confirme que le conteneur fonctionne correctement et que le port est bien exposé.
1.5<img width="945" height="546" alt="image" src="https://github.com/user-attachments/assets/ebdec368-2bc0-4da8-a25f-4d0ea9434c83" />

 
1.6<img width="945" height="187" alt="image" src="https://github.com/user-attachments/assets/b041b991-9b63-4ecf-a765-b4409c8776a6" />

 
La différence avec docker ps est que docker ps -a affiche aussi les conteneurs arrêtés.
1.7<img width="945" height="147" alt="image" src="https://github.com/user-attachments/assets/42427eff-0266-4d02-81c6-55ec0980ff07" />

 
1.8
Pour que le conteneur soit automatiquement supprimé à l’arrêt, il aurait fallu utiliser l’option --rm lors du lancement.
Commande correspondante : docker run --rm -d --name mon-nginx -p 8080:80 nginx:alpine






EXO 2
2.1
<img width="589" height="325" alt="image" src="https://github.com/user-attachments/assets/9cd727b7-efcb-4d14-86eb-b5e42fddb210" />

Création du fichier index.html avec une structure HTML minimale, contenant le titre “Ma première image Docker” et un titre principal <h 1> avec mon prénom.
 
2.2
<img width="945" height="60" alt="image" src="https://github.com/user-attachments/assets/ce171008-d3b1-4a45-a82e-7597359fced9" />

Création d’un Dockerfile basé sur l’image nginx:alpine.
Le fichier copie index.html dans /usr/share/nginx/html/index.html et expose le port 80.
 
2.3<img width="945" height="287" alt="image" src="https://github.com/user-attachments/assets/bb4652cf-166b-4cda-a6d7-8dc85ac48cdf" />

 
2.4
  <img width="945" height="49" alt="image" src="https://github.com/user-attachments/assets/501bbef7-48d9-4a72-8c01-94ae8513dbc9" />
  <img width="945" height="325" alt="image" src="https://github.com/user-attachments/assets/3d8b49c0-40f1-4cee-884c-7829299acb8b" />





2.5
<img width="945" height="128" alt="image" src="https://github.com/user-attachments/assets/508d99f8-a362-4f41-80b3-d1421f10049f" />

Affichage de la liste des images locales avec docker images.  
La taille de l’image mon-site:v1 est très proche de celle de nginx:alpine, car seule une petite page HTML a été ajoutée.

2.6
<img width="945" height="407" alt="image" src="https://github.com/user-attachments/assets/5d2bfd8d-1b24-4f32-b210-2059fdadab8a" />

  
On observe qu’une nouvelle couche a été ajoutée par rapport à l’image de base, correspondant à la copie du fichier index.html dans le dossier web de Nginx.
2.7
<img width="945" height="275" alt="image" src="https://github.com/user-attachments/assets/c23a88e4-855f-449a-b571-2b12f25719d3" />

Lors de la reconstruction de l’image mon-site:v2, l’image de base nginx:alpine a été récupérée depuis le cache. En revanche, l’étape de copie du fichier index.html a été rejouée car son contenu avait changé.
 
2.8
<img width="827" height="92" alt="image" src="https://github.com/user-attachments/assets/53e68f2b-0f3c-4639-bb08-d53c8044e0b8" />

 

Exo 3

3.1
<img width="945" height="329" alt="image" src="https://github.com/user-attachments/assets/49618f0c-c9c8-4a67-bff7-4491246d1f20" />

J’ai lancé un conteneur alpine en mode interactif avec l’option --rm. A l’intérieur, j’ai créé le fichier /data/test.txt avec le contenu bonjour. Après avoir quitté le conteneur puis relancé un nouveau conteneur alpine, le fichier n’existait plus. Cela montre que les données écrites directement dans le conteneur ne sont pas conservées après sa suppression 
3.2

J’ai créé un dossier exercice-3/html/ sur ma machine avec un fichier index.html. J’ai ensuite lancé un conteneur nginx:alpine . Après avoir modifié le fichier index.html sur ma machine, le changement est apparu directement dans le navigateur sans redémarrer le conteneur. J’en conclus que le conteneur utilise directement les fichiers présents sur l’hôte.

 <img width="841" height="377" alt="image" src="https://github.com/user-attachments/assets/6e5b0ce6-faba-4eda-95bb-db4c16688de3" />
<img width="503" height="252" alt="image" src="https://github.com/user-attachments/assets/b84d300f-b2a5-4af8-8fb8-ee909b9cb466" />

 

3.3
 <img width="945" height="63" alt="image" src="https://github.com/user-attachments/assets/52425b8a-e9c0-4355-b016-c3a2caf6fb32" />

3.4
 <img width="945" height="111" alt="image" src="https://github.com/user-attachments/assets/f59deeaf-9f1c-450b-9b1d-a7638b58fcd3" />

3.5
<img width="945" height="94" alt="image" src="https://github.com/user-attachments/assets/83598999-432b-480a-ac5f-83d8c8dff173" />

j’ai ensuite lancé un nouveau conteneur alpine en montant le même volume mes-donnees sur /data. Le fichier /data/persistant.txt était toujours présent. Cela démontre que les données stockées dans un volume nommé persistent même après la suppression du conteneur précédent.
 

3.6

<img width="945" height="89" alt="image" src="https://github.com/user-attachments/assets/fe28d54e-973a-44f3-9a78-10ef92051155" />
<img width="945" height="276" alt="image" src="https://github.com/user-attachments/assets/f230b026-1636-4acd-b987-40643160032b" />

J’ai listé les volumes Docker existants avec docker volume ls, puis j’ai inspecté le volume mes-donnees avec docker volume inspect mes-donnees. Cela m’a permis de voir que le volume est stocké physiquement par Docker sur la machine hôte, dans son espace de stockage interne
 
 





3.7
<img width="945" height="130" alt="image" src="https://github.com/user-attachments/assets/a772b1bc-0714-4c30-a4c5-2bc23e27dbf4" />

J’ai supprimé le volume mes-donnees avec la commande docker volume rm mes-donnees. Avant de supprimer un volume, il faut vérifier qu’il ne contient pas encore de données importantes, car cette suppression entraîne leur perte définitive.
 

Exo 4

4.1
<img width="689" height="284" alt="image" src="https://github.com/user-attachments/assets/71c09f25-d21f-4070-a912-ddb7a526aa2a" />

Les trois réseaux Docker créés par défaut sont bridge, host et none.
 
4.2
<img width="945" height="64" alt="image" src="https://github.com/user-attachments/assets/12c31583-15be-4644-82e3-d83a3a1339a8" />

 
4.3
 <img width="945" height="79" alt="image" src="https://github.com/user-attachments/assets/7a39ce37-3b4f-4677-a71d-e000ee9d985d" />

4.4
<img width="945" height="567" alt="image" src="https://github.com/user-attachments/assets/e04735fc-9897-4d02-8b07-e55954e93ad8" />

Depuis le conteneur client connecté au même réseau, j’ai récupéré la page par défaut de Nginx. Il est possible d’utiliser directement le nom serveur-web à la place d’une adresse IP, car Docker fournit une résolution DNS automatique entre les conteneurs connectés à un même réseau personnalisé.
 
4.5
<img width="945" height="295" alt="image" src="https://github.com/user-attachments/assets/3b50ad61-2061-4aaf-af0d-3d9332b6c3ea" />

Depuis le conteneur client-externe, qui n’était pas connecté au réseau mon-reseau, la communication avec serveur-web par son nom a échoué. Cela s’explique par le fait que ce conteneur n’était pas sur le même réseau et ne pouvait donc pas résoudre ce nom.

 
4.6
<img width="945" height="49" alt="image" src="https://github.com/user-attachments/assets/956781fe-5312-404d-a0b8-9bd8e0f2b369" />

Il est possible de connecter un conteneur déjà démarré à un réseau Docker après son lancement.
 
4.7
<img width="945" height="241" alt="image" src="https://github.com/user-attachments/assets/47a3d92a-bff5-4a0b-aa28-7446718dd1c7" />


 

Exo 5

5.1
<img width="884" height="497" alt="image" src="https://github.com/user-attachments/assets/63a13cb9-dbff-4b85-a22b-95cbf288e6af" />

 
5.2
J’ai créé le fichier requirements.txt avec Flask 3.0.3 comme unique dépendance.

5.3

Cet ordre est important car il permet à Docker de réutiliser le cache pour l’installation des dépendances tant que requirements.txt ne change pas. Si seul le code source change, Docker n’a pas besoin de réinstaller les dépendances..

5.4

<img width="945" height="479" alt="image" src="https://github.com/user-attachments/assets/68fb5095-fd5b-463b-a5df-4db327b0108b" />

 
5.5
 
 <img width="945" height="480" alt="image" src="https://github.com/user-attachments/assets/7a44b59e-3aa6-4a27-9ef0-77e524d35e5d" />

 <img width="945" height="481" alt="image" src="https://github.com/user-attachments/assets/0cca1f93-bab6-4f7e-86bb-f8bb09d546b7" />


 
5.6
<img width="945" height="442" alt="image" src="https://github.com/user-attachments/assets/aaa00ec2-1d92-4fe3-83e9-45d62f217480" />

 
En relançant le conteneur sans passer la variable APP_ENV, la valeur affichée est développement. Cette valeur provient de la valeur par défaut définie dans le code de l’application.


5.7
<img width="945" height="111" alt="image" src="https://github.com/user-attachments/assets/d91ded9c-99fc-4e58-9aea-8f864513796b" />

 
J’ai affiché la taille de l’image avec docker images. Pour réduire davantage la taille de l’image, il serait possible d’utiliser un multi-stage build et un fichier .dockerignore.

