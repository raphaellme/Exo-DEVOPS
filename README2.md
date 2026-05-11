Exo 1 


Exo 2
1) J’ai supprimé l’ancien conteneur Prometheus afin de le relancer avec une configuration personnalisée. 
2)  J’ai créé un fichier prometheus.yml contenant un intervalle de scrape global de 10 secondes ainsi qu’un label externe environment=lab. 
3) Le fichier a été monté dans le conteneur à l’emplacement /etc/prometheus/prometheus.yml. 
J’ai également activé l’option --web.enable-lifecycle afin de pouvoir recharger la configuration sans redémarrer Prometheus. 
4)  Après avoir exécuté la commande curl -X POST http://localhost:9090/-/reload, la configuration a bien été prise en compte et visible dans Status > Configuration.


<img width="976" height="277" alt="image" src="https://github.com/user-attachments/assets/96772aba-3739-486a-b10b-08c0ef74ffba" />

 


Exo 3 
1) J’ai lancé un conteneur node_exporter sur le port 9100 afin d’exposer des métriques système au format Prometheus. 

2) J’ai ensuite ajouté un nouveau job nommé node dans le fichier prometheus.yml, avec comme cible host.docker.internal:9100. 
3) Après avoir rechargé la configuration Prometheus avec l’endpoint /-/reload, la cible node est apparue en état UP dans Status > Targets. 
4) Enfin, la requête node_cpu_seconds_total a bien retourné des données dans l’expression browser de Prometheus.
 

 <img width="945" height="332" alt="image" src="https://github.com/user-attachments/assets/fbdf56ad-1ad2-49f0-a37c-fa0ecf2334e2" />


<img width="945" height="424" alt="image" src="https://github.com/user-attachments/assets/b3b48518-93c5-4d35-8a38-5670a8398ca1" />

 <img width="945" height="129" alt="image" src="https://github.com/user-attachments/assets/4cc7b399-74a4-425d-a2e7-b79f7269eae2" />



Exo 4 


1)J’ai remplacé la configuration statique des cibles Prometheus par une découverte de service basée sur un fichier. 
2)Pour cela, j’ai créé un fichier targets.json contenant deux endpoints : Prometheus sur localhost:9090 et node_exporter sur host.docker.internal:9100. 
3) J’ai ensuite modifié prometheus.yml afin d’utiliser file_sd_configs avec un refresh_interval de 5 secondes. 
4) Après avoir monté le dossier sd dans le conteneur Prometheus, les cibles sont apparues dans Status > Targets. 
5)Enfin, en ajoutant ou supprimant une cible dans le fichier targets.json, Prometheus a automatiquement mis à jour ses targets sans redémarrage ni rechargement manuel.


 
<img width="945" height="129" alt="image" src="https://github.com/user-attachments/assets/389ca1e7-a527-438b-b203-34796c295a7d" />

<img width="945" height="141" alt="image" src="https://github.com/user-attachments/assets/3752522e-b847-4c09-8fc5-e758a22a22cb" />

 
<img width="400" height="346" alt="image" src="https://github.com/user-attachments/assets/dc69200d-c7f9-4cda-bd33-42bebb6b9352" />

 
 <img width="945" height="142" alt="image" src="https://github.com/user-attachments/assets/4067914c-d2d0-4f0b-bdbd-6368559ad9c6" />


Exo 5 
J’ai créé un fichier de règles Prometheus nommé api_rules.yml dans un dossier rules. 
Ce fichier contient un groupe de règles évalué toutes les 30 secondes. 
La règle d’enregistrement job:http_requests:rate5m permet de pré-calculer le taux de requêtes HTTP de demo-api sur les cinq dernières minutes. 
J’ai ensuite ajouté le dossier rules dans la configuration Prometheus avec rule_files, puis monté ce dossier dans le conteneur. 
Après le redémarrage de Prometheus, la règle apparaît bien dans Status > Rules. 
La métrique job:http_requests:rate5m peut ensuite être interrogée depuis l’expression browser de Prometheus.
 
 <img width="945" height="158" alt="image" src="https://github.com/user-attachments/assets/d2fae9c9-2cea-4dfc-a6b0-8e6cead0abf7" />

<img width="945" height="210" alt="image" src="https://github.com/user-attachments/assets/ec2d4e32-63ce-4d1f-8cd6-802c738bac25" />


Exo 6
J’ai lancé un conteneur Alertmanager sur le port 9093 avec une configuration minimale contenant un receiver nommé default. 
J’ai ensuite créé un fichier api_alerts.yml contenant une règle d’alerte HighErrorRate. 
Cette alerte se déclenche lorsque le ratio d’erreurs HTTP 5xx de demo-api dépasse 5 % pendant 2 minutes. 
Dans prometheus.yml, j’ai ajouté le fichier d’alerte dans rule_files et configuré la section alerting afin d’envoyer les alertes vers alertmanager:9093. 
Après le redémarrage de Prometheus, l’alerte apparaît dans l’onglet Alerts de Prometheus et peut être transmise à Alertmanager.

<img width="945" height="477" alt="image" src="https://github.com/user-attachments/assets/5ccefb70-0268-4801-86e0-4b2c1d00399b" />

 <img width="945" height="104" alt="image" src="https://github.com/user-attachments/assets/d1b9b557-a486-4c86-8d89-b7aae76627a1" />
<img width="945" height="326" alt="image" src="https://github.com/user-attachments/assets/b8f17c10-bb30-4b3d-972e-388d61fa1e60" />

 

 

