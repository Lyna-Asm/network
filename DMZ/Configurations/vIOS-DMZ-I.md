Le rôle du switch dans le dmz:
Dans une DMZ (zone démilitarisée), le rôle d’un switch est crucial pour la sécurité et la connectivité.
Isolation des réseaux : La DMZ est une zone entre le réseau interne d’une organisation et Internet. Elle abrite des serveurs accessibles depuis l’extérieur, tels que des serveurs Web, des serveurs DNS ou des serveurs de messagerie. Le commutateur dans la DMZ permet de séparer physiquement ces serveurs du réseau interne, minimisant ainsi les risques de compromission.
Simplicité de conception : Un commutateur de couche 2 est souvent utilisé dans la DMZ. Contrairement à un commutateur de couche 3, qui a des capacités de routage, le commutateur de couche 2 se contente de transmettre les trames entre les appareils connectés. Cela simplifie la conception, car le firewall peut gérer les règles de filtrage et de sécurité sans avoir à se soucier du routage complexe.
Isolation maximale : Utiliser un commutateur de couche 2 garantit que la DMZ reste isolée autant que possible. Si un commutateur expose une interface de gestion dans la DMZ, les attaquants pourraient y accéder et s’échapper de la DMZ. 
Pourquoi un switch de couche 3?
Un switch de niveau 2 se limite aux adresses MAC et ne prend pas en compte les adresses IP ou d’autres éléments des couches supérieures. En revanche, un switch de niveau 3 peut effectuer toutes les tâches d’un switch de niveau 2 et gérer le routage statique et dynamique. Cela signifie qu’il dispose à la fois d’une table d’adresses MAC et d’une table de routage IP, permettant ainsi la communication intra-VLAN et le routage de paquets entre différents VLAN.
Sécurité et flexibilité : Les switchs de niveau 3 offrent une puissance et une sécurité supérieures. Ils sont capables de gérer des fonctions telles que le marquage du trafic VLAN en fonction des adresses IP, ce qui simplifie la configuration et améliore la flexibilité. De plus, ils sont adaptés aux environnements complexes tels que les centres de données et les réseaux d’entreprise.
S’échapper de la DMZ : Si l’attaquant peut compromettre le commutateur, il peut utiliser ce point d’accès pour accéder au réseau interne, contournant ainsi la sécurité mise en place.

Méthode de configuration:
<img width="453" alt="image" src="https://github.com/Lyna-Asm/network/assets/167743229/1ce3a01a-49b0-4921-8c5c-e4d5b90c4b31">

No ip http server:
-La commande “ip http server” active la fonctionnalité du serveur HTTP sur un périphérique Cisco.
-Lorsqu’elle est activée, le périphérique peut être configuré ou surveillé en toute sécurité depuis un navigateur web.
-Pour désactiver cette fonction, il faut utiliser la commande “no ip http server”.
-Une fois désactivée, elle permet d'améliorer la sécurité en empêchant l’accès non autorisé via HTTP, empêche l’accès via HTTPS (port 443).


No ip http secure-server :
-Désactive à la fois le serveur HTTPS et le serveur HTTP.
-Améliore la sécurité en empêchant l’accès non autorisé via HTTP et HTTPS.

<img width="431" alt="image" src="https://github.com/Lyna-Asm/network/assets/167743229/be11c994-adf3-4952-9f9d-38de9fd03604">

Authentication Console, Privileged Exec Mode et SSH:
-Creation d’un user:
<img width="398" alt="image" src="https://github.com/Lyna-Asm/network/assets/167743229/3d4618ff-d71f-4c2e-a7e5-05532c331cea">

vIOS-DMZ-I(config-line)# login local: Cette commande indique que l’authentification locale doit être utilisée pour accéder aux sessions VTY. Lorsqu’un utilisateur se connecte via SSH, le périphérique vérifie les informations d’identification stockées localement (par exemple, dans la base de données des utilisateurs locaux) pour autoriser ou refuser l’accès.

Configuration d’un nom de domain et génération de la clé RSA:

<img width="431" alt="image" src="https://github.com/Lyna-Asm/network/assets/167743229/94003429-6c97-42d4-aaa2-1b1765aff727">

La commande ip ssh version 2 configure le protocole Secure Shell (SSH) sur un périphérique Cisco pour utiliser la version 2 du protocole. 

<img width="341" alt="image" src="https://github.com/Lyna-Asm/network/assets/167743229/9341336f-19c2-4ff9-90d4-3834ce3fa807">

vIOS-DMZ-I(config-line)# transport input ssh:
 Cette commande restreint les types de connexion autorisés sur les lignes VTY à SSH uniquement. Cela renforce la sécurité en empêchant les connexions Telnet.
Ces commandes sécurisent l’accès aux sessions VTY en n’autorisant que les connexions SSH et en exigeant une authentification locale pour accéder au périphérique.
-Création d’une ACL “ssh-access”:
<img width="392" alt="image" src="https://github.com/Lyna-Asm/network/assets/167743229/079b1f62-e52f-4531-a310-eaefbbdd00d6">

Cette séquence de commandes crée une ACL qui autorise le trafic SSH depuis le réseau 195.1.1.0/25 (plage d’adresses de 195.1.1.0 à 195.1.1.127), tout en bloquant tout autre trafic. Cela renforce la sécurité en limitant l’accès au périphérique via SSH à une plage d’adresses IP spécifique.

<img width="331" alt="image" src="https://github.com/Lyna-Asm/network/assets/167743229/44e029ba-608e-46a0-8fc4-f77e85c5cae3">

Cette séquence de commandes configure les lignes VTY pour autoriser uniquement les connexions SSH depuis des adresses IP spécifiques, en utilisant l’ACL “ssh-access”. Cela renforce la sécurité en limitant l’accès aux sessions VTY sur le périphérique.
-NTP:
<img width="315" alt="image" src="https://github.com/Lyna-Asm/network/assets/167743229/c0df9b4b-abc2-47b5-b44e-d93f3b6fa6a2">

vIOS-DMZ-I(config)# ntp server 172.16.50.1 : Cette commande configure le serveur NTP (Network Time Protocol) sur le routeur vIOS-DMZ-I. L’adresse IP 172.16.50.1 est spécifiée comme serveur NTP. Le protocole NTP permet au routeur de synchroniser son horloge avec celle du serveur NTP, assurant ainsi une heure précise et cohérente dans le réseau. 
vIOS-DMZ-I(config)# ip domain lookup : Cette commande active la recherche de domaine sur le switch vIOS-DMZ-I. quand cette fonction est activée, le routeur tentera de résoudre les noms de domaine en adresses IP en utilisant le serveur DNS configuré précédemment. Cela permet au routeur de résoudre les noms de domaine en adresses IP, ce qui est essentiel pour accéder à des ressources externes telles que des sites Web.

- DNS Client:
<img width="460" alt="image" src="https://github.com/Lyna-Asm/network/assets/167743229/3cfe236e-967b-414c-aa09-6183a60347ad">
Ces deux commandes permettent au routeur vIOS-DMZ-I de résoudre les noms de domaine en adresses IP en utilisant le serveur DNS spécifié.Cela facilite la communication avec d’autres systèmes et services sur Internet ou dans le réseau local.

- Logging:
<img width="461" alt="image" src="https://github.com/Lyna-Asm/network/assets/167743229/f75a554e-cb2f-44be-9c2a-290ef68d2292">

vIOS-DMZ-I(config)# logging host 195.1.1.161 : Cette commande configure le switch vIOS-DMZ-I pour envoyer ses journaux (logs) au serveur à l’adresse IP 195.1.1.161. Le serveur collecte et stocke les messages de journalisation du routeur, ce qui est utile pour la surveillance, le dépannage et la sécurité du réseau.
vIOS-DMZ-I(config)# logging trap notifications : Cette commande définit le niveau de sévérité des messages à envoyer au serveur de syslog. En spécifiant “notifications”, le routeur enverra uniquement les messages de niveau de sévérité “notifications” (et plus graves) au serveur. Cela permet de contrôler la quantité de données de journalisation envoyées au serveur, en se concentrant sur les événements importants






