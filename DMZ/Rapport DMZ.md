# Rapport sur la configuration de la zone demilitarisée 
## Introduction 
La DMZ est un segment de réseau qui se situe entre le réseau interne de confiance et l'internet non fiable. 
Elle héberge généralement des serveurs accessibles au public, tels que des serveurs Web ou des serveurs de messagerie, tout en les isolant du réseau interne.
## Generalités sur la DMZ : 
### Fonctions principales d'une DZM :

Filtrage du trafic: La DZM permet de filtrer le trafic entrant et sortant du réseau interne, en ne laissant passer que les communications autorisées. Cela permet de protéger le réseau interne contre les attaques et les intrusions.

Contrôle d'accès: La DZM peut être configurée pour autoriser ou refuser l'accès à des services spécifiques en fonction de l'adresse IP ou d'autres critères. Cela permet de limiter l'accès aux ressources sensibles du réseau interne.

Sécurité des applications: La DZM peut être utilisée pour héberger des applications qui ne sont pas nécessairement sûres, mais qui doivent être accessibles depuis le réseau interne. Cela permet de limiter les risques pour le réseau interne en cas de compromission de l'application.

Logistique et surveillance: La DZM peut être utilisée pour collecter des journaux et des informations de sécurité sur les communications qui transitent par la zone. Cela permet de surveiller l'activité et de détecter les menaces potentielles.


### Types de DZM :  
Il existe plusieurs types de DZM, dont les plus courants sont :

DZM à base de pare-feu: Ce type de DZM utilise un pare-feu pour filtrer le trafic entre les réseaux interne et externe.
DZM à base de routeur: Ce type de DZM utilise un routeur pour séparer les réseaux interne et externe.
DZM virtuelle: Ce type de DZM utilise des technologies de virtualisation pour créer une zone réseau distincte sur un même serveur physique.

### Avantages d'une DZM :

Amélioration de la sécurité: La DZM permet de réduire les risques d'attaque et d'intrusion sur le réseau interne.
Meilleure gestion des accès: La DZM permet de contrôler plus précisément qui a accès aux ressources du réseau interne.
Flexibilité accrue: La DZM peut être adaptée aux besoins spécifiques de chaque organisation.


### Inconvénients d'une DZM :

Coût: La mise en place et la maintenance d'une DZM peuvent être coûteuses.
Complexité: La configuration et la gestion d'une DZM peuvent être complexes.
Performances: La DZM peut avoir un impact sur les performances du réseau.

  
## vue d'ensemble sur la configuration 
Dans notre conception on a les equipements suivants : 

### ASAv-DMZ-I : 
Ce pare-feu ASA contrôle le trafic entrant et sortant vers et depuis la DMZ. Il dispose de deux interfaces :
Gi0/0 : Cette interface est connectée à un routeur ou un commutateur menant à Internet.
Gi0/2 : Cette interface se connecte au commutateur multi-couche (vIOS-DMZ-I) au sein de la DMZ.

### vIOS-DMZ-I : 
Ce commutateur Cisco vIOS-L2 est responsable de la commutation de couche 2 au sein de la DMZ. Il dispose de trois interfaces :
Gi0/1 : Cette interface est connectée au pare-feu ASA (ASAv-DMZ-I).
e0 : Cette interface est connecté à Serv-DMZ-I (serveur Linux).
VLAN10 : Cette interface VLAN peut être utilisée pour connecter d'autres appareils au sein de la DMZ.



### Serv-DMZ-I : 
Ce serveur Linux exécute Ubuntu 16.04.3 LTS. Il fournit probablement ces services :
DNS (Domain Name System) : Convertit les noms de domaine en adresses IP pour les appareils de la DMZ.
NTP (Network Time Protocol) : Synchronise l'heure sur les appareils de la DMZ.
Syslog : Fournit un service de journalisation des événements provenant des appareils de la DMZ.
Serveur Web : Ce serveur semble également héberger un service Web public accessible depuis Internet.

## Le Serveur de la DMZ 

### choix du serveur 
Windows Server est largement utilisé et compatible avec un large éventail de logiciels. ce pour il est  une cible privilégiée pour les pirates informatiques en raison de sa popularité.
On a donc choisit l'utilisateur d'Ubuntu car celui ci est plus sécurisé pour une DMZ en raison de:
Sa base de code plus petite et moins complexe, ce qui réduit la surface d'attaque.
Sa communauté active qui développe et publie rapidement des correctifs de sécurité.
Son architecture open source qui permet une inspection et une modification transparentes du code.

## Le firewall de la DMZ 

Le pare-feu Cisco ASAv 9.8.1 est une solution de sécurité réseau virtuelle de nouvelle génération,  puissante et flexible qui offre de nombreux avantages pour la protection de notre DMZ. 


### Avantages :

Sécurité avancée : Offre une protection complète contre les menaces réseau et les attaques sophistiquées grâce à des fonctionnalités telles que le filtrage de paquets, l'inspection approfondie des paquets (DPI), le contrôle des applications et la prévention des intrusions (IPS).
Flexibilité et évolutivité : Disponible en plusieurs versions pour répondre aux besoins de différents types de réseaux, des petites entreprises aux grandes organisations. Il peut également être déployé sur site ou dans le cloud.

Gestion simplifiée : Offre une interface graphique intuitive (ASDM) pour une configuration et une gestion faciles, ainsi qu'une prise en charge de la ligne de commande (CLI) pour un contrôle plus granulaire.

Performances élevées : Offre un débit et une latence optimisés pour garantir un impact minimal sur les performances du réseau.

Fonctionnalités VPN : Prend en charge les connexions VPN IPsec et SSL pour un accès sécurisé à distance à la DMZ.

Intégration avec d'autres solutions Cisco : Fonctionne de manière transparente avec d'autres produits de sécurité Cisco pour une protection complète du réseau.


### Forces :

Meilleure protection contre les menaces: L'ASAv 9.8.1 offre une protection avancée contre les dernières menaces, y compris les ransomwares, les malwares et les attaques zero-day.
Visibilité et contrôle accrus: Le pare-feu offre une visibilité complète sur le trafic réseau et permet un contrôle granulaire sur les accès aux ressources de la DMZ.
Facilité de gestion: L'ASDM facilite la configuration et la gestion du pare-feu, même pour les utilisateurs non techniques.
Coût total de possession (TCO) réduit: L'ASAv 9.8.1 est une solution de sécurité rentable qui offre un excellent rapport qualité-prix.

Stateful inspection: Permet d'autoriser ou de refuser le trafic en fonction de l'état de la connexion, ce qui améliore la sécurité et les performances.

High availability: Prend en charge la mise en cluster actif/passif pour garantir une disponibilité continue du pare-feu.
Reporting and logging: Fournit des rapports et des journaux détaillés pour une analyse et une détection des menaces plus efficaces.



## Configuration du switch 