Le mouvement DevOps et les pratiques d'automatisation du déploiement par Olivier ANDRADE 

DevOps = development + operations (exploitation) 

 

Ops : mise en prod + monitoring du logiciel (espace disk sur server, surveillance faille et attacks, ) 

 

 

La pre prod : permet de tester/simuler les pbs potentiels de mise en prod 

 

App.1.0.2.SNAPSHOT : la version en construction de la version 1.0.2 livré après un sprint review 

 

DevOps : sécurité, intrusion possible. Un port SSH ouvert se retrouvera attaqué. 

Monitoré la latence réseau (ping),  

 

 

ITIL (The Information Technology Infrastructure Library) : stablisé la mise en prod elle-même. (stable duplicate) Bien documenté le processus pour permettre de le répéter. 

 

 

BDD a testé plus rapide : moins de données + BDD sur RAM et non sur disk (in-memory testing) (forcément pas de mémorisation long terme) 

 

 

 

docker on windows ne fonctionne pas aussi bien que docker on WSL2 Ubuntu car il y a une cassure dans le schéma de la conteneurisation 