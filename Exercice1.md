# Théorie
## Question 1
*Le serveur SRVWIN01 a le rôle DHCP d'installé et correctement configuré et activé. Quelles peuvent être les raisons poour lesquelles le client ne reçoit pas de configuration IP du server ?* <br>
<br>

Voici plusieurs raisons possible à cela :
  * La machine serveur et cliente ne sont pas dans le même réseau.
  * La machine cliente a déjà une IP static de configuré.

## Question 2
*Sur le serveur on exécute la commande `ipconfig /all`. On a une adresse 172.16.10.10/24. Si on exécute la même commande sur le client, on a une adresse 172.16.100.50/24. Pourquoi un ping ne fonctionne pas entre ces 2 machines ?* <br>
<br>

La connexion ne se fait pas entre les deux machines car elles ne sont pas sur le même sous-réseau :
  * Sous-réseau serveur : 172.16.10
  * Sous-réseau client : 172.16.100

Il est possible de savoir le sous-réseau d'une machine grâce à son masque de sous-réseau qui ici vaut **24**.

## Question 3
*Si le client a une configuration IP en DHCP, pour quelle(s) raison(s) il ne prend pas la première adresse configurée sur la plage des adresses IP mais une autre adresse ?*<br>
<br>

Voici plusieurs raisons possible à cela :
  * L'adresse a été exclu du scope lors de la configuration du DHCP
  * L'adresse a été réservé à une autre adresse MAC lors de la configuration du DHCP
  * L'adresse est déjà utilisé par un autre client du sous-réseau

## Question 4
*Est-il possible de forcer un client à prendre une adresse IP spécifique en DHCP ? Si oui explique comment procéder sur le client et sur le serveur.*<br>
<br>

Il est possible de forcer un client à prendre une adresse IP spécifique en DHCP, pour cela nous aurons besoin de l'adresse MAC de la machine cliente.<br>
Une fois cela fait, il faut aller sur la machine server puis dans l'outils de gestion DHCP. Dans le panneau latéral gauche, déroulez le menu jusqu'à voir le dossier `Reservations`. <br>
Faites un clique droit dessus puis sélectionnez `New Reservation`, remplissez comme suit :
  * Reservation Name : Nom de la machine cliente
  * IP Address : Mettre une IP qui fasse partie du sous-réseau (pas forcément du scope)
  * MAC Address : Mettre l'adresse MAC de la machine cliente
  * Description : Mettre une description si vous le souhaitez
  * Supported types : Sélectionnez `DHCP`

Une fois cela fait, cliquez sur `Add`. Maintenant sur la machine cliente. <br>
Vous avez deux possibilités :
  * En redémarrant la machine
    * Une fois redémarrer, ouvrez un invité de commande puis faite la commande `ipconfig`, vous verrez votre nouvelle adresse.
  * Sans redémarrer la machine
    * Ouvrez un invité de commande, puis faite la commande `ipconfig /renew`
    * Puis faite la commande `ipconfig`, vous verrez votre nouvelle adresse.

## Question 5
*Le résultat de la commande ipconfig /all donne aussi, sur le client et sur le serveur, une adresse IPv6 qui commence par fe80... Quelle est cette adresse et à quoi sert-elle ?*<br>
<br>

Cette adresse IPv6 est l'adresse locale lien (Link local) et elle sert à joindre les voisins sur un même lien (sous-réseau).

## Question 6
*Quel autre type d'adresse IPv6 peut-on avoir sur une machine ? Précise le type, le préfixe, et la porté.*
Je ne sais pas.

## Question 7
*Est-il possible de configurer le service DHCPv6 sur le serveur SRVWIN01 avec des préfixes d'adresses Unicast Locales Uniques ? Dans ce cas, si le client a une configuration IP en DHCP, est-ce qu'il va avoir automatiquement une adresse IPv6 Unicast Locales Uniques ?*
Je ne sais pas.

## Question 8
*Entre 2 machines on exécute la commande ping avec le nom des machines au lieu de l'adresse IP. La commande s'exécute correctement. Quel protocole permet cela ?* <br>
<br>
C'est le protocole ICMP qui permet de ping deux machines entre elles et c'est le protocol DNS qui permet de ping avec le nom des machines (s'il est correctement configuré).

## Question 9
*Si l'IPv6 est activé, le retour de la commande ping avec le nom d'une machine est une adresse IPv6. Pourquoi ? Quelle option de la commande ping permet d'avoir une adresse IPv4 ?*<br>
<br>
Le retour de la commande ping avec le nom d'une machine est une adresse IPv6 parce que le DNS a été configuré avec les adresses IPv6. <br>

Pour pouvoir *forcer* le ping en IPv4, il faut faire la commande `ping -4`.

## Question 10
*À partir du serveur, je veux pouvoir faire un ping vers le client à partir de son nom, et également avec un alias de ce nom, par exemple CLIENT_TEST, comment procéder ?*
Je ne sais pas

# Mise en pratique
## Question 1
*Sans changer la configuration IPv4 des 2 machines, depuis le serveur montre le résultat d'un ping vers l'adresse IPv4 du client. Modifie la configuration IP statique sur le client pour que ce ping depuis le serveur soit fonctionnel. Montre le résultat de la commande `ipconfig /all` sur le client avec la nouvelle adresse IP. Montre le résultat d'un ping IPv4 du serveur vers le client.* <br>
<br>

Voici le résultat d'un ping vers l'adresse IPv4 du client : <br>
![pingfailed](https://github.com/Mirhazka/TSSR-Checkpoint-2/blob/main/Image/exercice1/pingfailed.png)

Voici le résultat de la commande `ipconfig /all` après modification de la nouvelle adresse IP sur le client : <br>
![ipconfigAll](https://github.com/Mirhazka/TSSR-Checkpoint-2/blob/main/Image/exercice1/ipconfigAll.png)

Voici le résultat d'un ping vers l'adresse IPv4 du client : <br>
![pingfailed](https://github.com/Mirhazka/TSSR-Checkpoint-2/blob/main/Image/exercice1/pingsuccess.png)

## Question 2
*Mets le client CLIENT1 en DHCP. Montre le résultat de la commande `ipconfig /all` et des commandes possibles sur le client qui permettent d'avoir une nouvelle configuration IP. Montre le résultat d'un ping IPv4 du serveur vers le client.* <br>
<br>

Voici le résultat de la commande `ipconfig /all` après l'ajout du CLIENT1 en DHCP : <br>
![ipconfigAll](https://github.com/Mirhazka/TSSR-Checkpoint-2/blob/main/Image/exercice1/ipconfigAllDHCP.png)

Voici le résultat des commandes possibles sur le client qui permettent d'avoir une nouvelle configuration IP : <br>
![ipconfigReleaseRenew](https://github.com/Mirhazka/TSSR-Checkpoint-2/blob/main/Image/exercice1/ipconfigReleaseRenew.png)

Voici le résultat d'un ping vers l'adresse IPv4 du client : <br>
![pingfailed](https://github.com/Mirhazka/TSSR-Checkpoint-2/blob/main/Image/exercice1/pingsuccessDHCP.png)

## Question 3
*Sur le serveur, modifie la configuration du service DHCP (sans supprimer la plage) pour que le client prenne une adresse IP entre 172.16.10.100 et 172.16.10.200. Montre les changements effectués sur le serveur. Montre le résultat de la commande `ipconfig /all` sur le client avec la nouvelle adresse IP.* <br>
<br>

Voici les changements effectués sur le serveur : <br>
![dhcpServer](https://github.com/Mirhazka/TSSR-Checkpoint-2/blob/main/Image/exercice1/dhcpServer.png)

Voici le résultat de la commande `ipconfig /all` après la modification du scope du DHCP : <br>
![ipconfigAll](https://github.com/Mirhazka/TSSR-Checkpoint-2/blob/main/Image/exercice1/ipconfigALLNewScope.png)