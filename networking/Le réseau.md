# Définition :

> Un réseau (en Anglais « #Network ») est un ensemble d’équipements reliés entre eux pour échanger des informations.

Outre des `moyens informatiques`, la mise en œuvre d’un réseau suppose des `infrastructures` telles que des liaisons physiques (câbles, ondes hertziennes…) et des `équipements de transmission` et d’interconnexion (carte réseau, routeur, switch…). Un réseau informatique nécessite également la mise en œuvre de `protocoles` de communication permettant de définir de façon standardisée la manière dont les informations sont échangées entre les équipements du réseau.

# Les types de réseaux
## Les LAN :

> LAN signifie Local Area Network (en français Réseau Local). Il s'agit d'un ensemble d'ordinateurs appartenant à une même organisation et reliés entre eux dans une petite aire géographique par un réseau

C’est un réseau domestique ou d’entreprise. La taille d'un réseau local peut atteindre jusqu'à 100 voire 1000 utilisateurs.

## Les MAN :

> Les MAN (Metropolitan Area Network) interconnectent plusieurs LAN géographiquement proches (au maximum quelques dizaines de km) à des débits importants. Ainsi un MAN permet à deux nœuds distants de communiquer comme s’ils faisaient partie d'un même réseau local.

Un MAN est formé de commutateurs ou de routeurs interconnectés par des liens hauts débits (en général en fibre optique).

## Les WAN :

> Un WAN (Wide Area Network ou réseau étendu) interconnecte plusieurs LAN à travers de grandes distances géographiques.

Les WAN fonctionnent grâce à des routeurs qui permettent de "choisir" le trajet le plus approprié pour atteindre un nœud du réseau.

Le plus connu des WAN est Internet.

![[asset/types de réseaux.png]]

# Les méthodes d’accès à Internet

Actuellement, les 3 méthodes d’accès à Internet les plus utilisées sont l’ADSL, la fibre optique et les ondes radioélectriques (2G, 3G, 4G, etc).

## L’ADSL :

> L’ADSL (Asymmetric Digital Subscriber Line) est une technique de
communication numérique. Elle permet d'utiliser une ligne téléphonique
pour transmettre et recevoir des données numériques de manière
indépendante du service téléphonique conventionnel (c'est-à-dire
analogique).

## La fibre optique :

> Une fibre optique est un fil en verre ou en plastique très fin qui a la
propriété d'être un conducteur de lumière et sert dans la transmission
de données par la lumière.

### Le FTTH :

--- Fiber To The Home : Le réseau de fibre optique va jusqu’au domicile.

### Le FTTB :

--- Fiber To The Building : Le réseau de fibre optique va jusqu’au bâtiment. Le reste de la connexion se fait grâce à des câbles existants dans le bâtiment (téléphonique, ADSL). Le débit est donc fortement diminué.

## Les ondes radioélectriques :

>Une onde radioélectrique est une onde électromagnétique dont la fréquence est inférieure à 300 GHz. La transmission des données se fait donc dans l’air grâce à des antennes relais.

Les antennes-relais sont indispensables pour qu’un téléphone mobile fonctionne. A la réception d'un appel, l'antenne-relais transforme les ondes électromagnétiques qui transitent dans l’air en signal électrique. Le signal circule alors dans des câbles sous forme de données numériques. Le phénomène a lieu dans le sens
inverse lorsque l'antenne-relais émet le signal.

Dès que le mobile est allumé, un dialogue s’établit entre le terminal et l’antenne la plus proche pour permettre une émission ou une réception d’appel. Entre le téléphone mobile et l'antenne-relais, l’appel est acheminé à travers les airs. Le même phénomène se produit pour accéder à l’Internet mobile.

| Standard | Génération | Bande de fréquence | Débit | |
| :----------------- | :---- | :----------------- | :---- | :-- |
| GSM | 2G | Transfert voix ou données numériques de faible volume. | 9,6 kbps | 9,6 kbps |
| GPRS | 2.5G | Transfert voix ou données numériques de volume modéré. | 21-171 kbps | 48 kbps |
| EDGE | 2.75G | Transfert simultané voix et données numériques. | 43-345 kbps | 171 kbps |
| UMTS | 3G | Transfert simultané voix et données numériques à haut débit. | 0,1-2 Mbps | 384 Kbps |
| LTE | 4G | Transfert simultanés voix et données numériques à haut débit. | 10-300 Mbps | 5-75 Mbps |

# Matériels au sein d’un LAN

![[Matériels LAN.png]]

## Le HUB :
> Un HUB (appelé aussi concentrateur) est un élément matériel permettant de concentrer le trafic réseau provenant de plusieurs hôtes, et de régénérer le signal. Son unique but est de récupérer les données binaires parvenant sur un port et de les diffuser sur l'ensemble des ports.

## Le switch :
> Le switch est un matériel d’interconnexion. Appelé aussi commutateur, il analyse les trames arrivant sur ses ports d'entrées et filtre les données afin de les aiguiller uniquement sur les ports adéquats (on parle de commutation ou de réseaux commutés).

## Le routeur :
>Un routeur est un élément intermédiaire dans un réseau informatique assurant le routage des paquets. Son rôle est de faire transiter des paquets d'une interface réseau vers une autre, au mieux, selon un ensemble de règles.

Le routeur permet par exemple de relier un réseau domestique (LAN) à Internet (WAN).

# Adressage

La communication entre deux ordinateurs peut être comparée à l’envoi d’un courrier postal entre un expéditeur (toto) et un destinataire (titi).

Si Toto veut envoyer un courrier à Titi il a besoin d’une `adresse postale`

Le réseau postal Français est composé de sous-réseaux : `les régions`.
Les régions sont, elles-mêmes, composées de sous-réseaux : l`es villes`.
Les villes sont, elles-mêmes, composées de sous-réseaux : `les rues`.
Les rues forment un réseau de maisons repérées par un `N°`.

![[Adressage.png]]

Si PC1 veut envoyer un message à PC2 il a besoin d’une `adresse réseau (adresse IP)`

> L’adresse IP fonctionne selon le même principe que l’adresse postale, elle permet de localiser la machine sur un réseau d’ordinateurs, celui-ci pouvant être composé de sous-réseaux. L’adresse IP de la machine contient l’ensemble de ces informations.

## Adresse IP / MAC :

L’adresse IP (comme Internet Protocol) est une adresse « `logique` » affectée à une machine manuellement par l’administrateur réseau ou automatiquement par un serveur DHCP (Dynamic Host Configuration Protocol). Cette adresse permet de communiquer au sein d’un réseau. Elle est modifiable.

Chaque interface réseau (carte réseau, interface Wi-fi, Bluetooth, …) possède également une `adresse physique` non modifiable et « inscrite en dur » par le constructeur. Il s’agit de l’adresse `MAC` (Media Acces Control). Cette adresse permet d’identifier de façon unique la `carte` dans tous les réseaux.
Une adresse MAC est un nombre de 48 bits représenté en hexadécimal par 6 octets.
Exemple d’adresse MAC : `F4-6D-04-AF-64-62`

Sous Windows pour obtenir les adresses physiques (MAC) et logique (IP) des interfaces réseaux de votre PC vous pouvez taper la commande : `ipconfig /all`

Sous Windows, c’est le protocole ARP (Address Resolution Protocol) qui établit la correspondance entre adresse physique et adresse IP.
Pour afficher les entrées de la table ARP saisissez : `arp –a`.

## Adresse #IP :
### Adresse publique / privé :

Les adresses `publiques` sont celles qu’il est possible d’utiliser pour une connexion à l’Internet. Elles sont attribuées par l’IANA (Internet Assigned Numbers Authority) auprès de qui il faut s’enregistrer en passant par un FAI (Fournisseur d’Accès à Internet).

A moins de disposer d’un #proxy (serveur Mandataire) ou d’un service #NAT (Network Adress Traduction), tout ordinateur d’un réseau local voulant se connecter à Internet doit disposer de sa propre adresse IP.

Grâce au service #NAT, une seule adresse #IP publique est nécessaire (elle est attribuée au routeur permettant l’accès du réseau à local à l’internet). Les ordinateurs du réseau doivent alors disposer de leurs propres
adresses #IP privées pour communiquer entre eux et avec le serveur #NAT.

### Format :
> Il existe des adresses #IP de version 4 (sur 32 bits, soit 4 octets) et de version 6 (sur 128 bits, soit 16 octets).

La version 4 est actuellement la plus utilisée : elle est généralement représentée en notation décimale avec quatre nombres compris entre 0 et 255, séparés par des points, ce qui donne par exemple : 172.16.254.1
(l'adresse qui figure sur l'image ci-dessous).

![[example ip.png]]

Le nombre d'adresses #IP Version 4 publiques est arrivé officiellement à saturation le 3 février 2011. La transition d'IPv4 vers IPv6 est en cours.

### Classe :
>Dans le système de définition des réseau #IP version 4 ( #IPv4), les adresses #IP étaient réparties en classes, selon le nombre d'octets qui représentent le réseau, lui-même déterminé par les premiers bits de l'adresse #IP.

A cause de la migration vers l’ #IPv6, cette notion de classe est maintenant obsolète.

L’adresse #IP d’un équipement contient à la fois un identifiant réseau (NetID) et un identifiant équipement (HostID)

![[separation ip.png]]

En fonction du nombre d’équipements pouvant être connectés à un réseau, les adresses #IP appartiennent à la classe A, B ou C. Le format d’une adresse #IP selon sa classe est le suivant :

![[class ip.png]]

L’adresse #IP du réseau est une adresse #IP avec tous les bits de la partie « ID Hôte » à 0. C’est donc une adresse réservée et non attribuable à un équipement.

Une autre combinaison est réservée. C’est celle où tous les bits de la partie « ID Hôte » sont à 1. Cette adresse est l’adresse de diffusion ( #broadcast) et sert à désigner tous les hôtes du réseau.

![[global rule adresse.png]]
`classe B`

| id réseaux | id hôte | adresse réseaux |  adresse diffusion |
| :--------- | :------ | :-------------- | :----------------- |
| 172.16 | 25.105 | 172.16.0.0 | 172.16.255.255 |

### Masque de sous-réseau :
>Une adresse #IP est toujours associée à un « masque de sous-réseau », c’est grâce à celui-ci que l’on peut extraire de l’adresse #IP, le N° de la machine et le réseau / sous réseau auquel il appartient.

Par défaut, lorsqu’il n’y a pas de sous réseaux, les masques sont :
- En classe A : `255.0.0.0`
-  En classe B : `255.255.0.0`
-  En classe C : `255.255.255.0`

Pour déterminer l’adresse réseau à partir d’une adresse #IP, on effectue l’opération logique suivante :
Adresse réseau = (Adresse #IP) ET (masque)

Adresse #IP = 10.121.58.12
ET
masque = 255.0.0.0
Equal
Adresse réseau = 10.0.0.0

Pour résumer :

![[Classe ip.png]]

# Les architectures de réseau
## Architecture client-serveur :
>Dans cet environnement les ordinateurs "clients" contactent un ordinateur "serveur" pour utiliser un service d’application, une base de données, une connexion à un autre réseau, etc... La machine « serveur » est en
général très puissante.

#### Un système client/serveur fonctionne selon le schéma suivant :

- Le client émet une requête vers le serveur grâce à son adresse IP et le port, qui désigne un service particulier du serveur.
- Le serveur reçoit la demande et répond à l'aide de l'adresse de la machine cliente et son port.

![[architecture client serveur schema.png]]

#### Avantages :

- `Des ressources centralisées` : étant donné que le serveur est au centre du réseau, il peut gérer des ressources communes à tous les utilisateurs, comme par exemple une base de données centralisée, afin d'éviter les problèmes de redondance et de contradiction.
- `Une meilleure sécurité` : car le nombre de points d'entrée permettant l'accès aux données est moins important.
- `Une administration au niveau serveur` : les clients ayant peu d'importance dans ce modèle, ils ont moins besoin d'être administrés.
- `Un réseau évolutif` : grâce à cette architecture il est possible de supprimer ou rajouter des clients sans perturber le fonctionnement du réseau et sans modification majeure.

![[architecture client server.png]]
#### Inconvénients :

- `Un coût élevé` dû à la technicité du serveur.
- `Un maillon faible` : le serveur est le seul maillon faible du réseau client/serveur, étant donné que tout le réseau est architecturé autour de lui.

### Architecture égal à égal (groupe de travail, « workgroup ») :

>Dans cette architecture, il n'y a pas de serveur dédié. Ainsi, chaque ordinateur est un peu serveur et un peu client. Cela signifie que chacun des ordinateurs du réseau est libre de partager ses ressources. Ces ressources ne sont alors pas centralisées.

#### Avantages :

- Coût réduit dû à l'absence de serveur.
- Extrême simplicité.

![[architecture égal à égal.png]]
#### Inconvénients :

- Administration plus difficile à cause de l'absence de centralisation.
- Sécurité plus difficile à assurer.

# Topologie physique d’un réseau
Un réseau informatique est constitué d'ordinateurs reliés entre eux grâce à des lignes de communication (câbles réseaux, etc.) et des éléments matériels (cartes réseau, ainsi que d'autres équipements permettant d'assurer la bonne circulation des données). L'arrangement physique, c'est-à-dire la configuration spatiale du réseau est appelé `topologie physique`. On distingue généralement les topologies suivantes :

- Topologie en bus
- Topologie en étoile
- Topologie maillée
- Topologie en anneau
- Topologie en arbre

## Topologie en bus :
>Dans une topologie en bus tous les ordinateurs sont reliés à une même ligne de transmission par l'intermédiaire de câble. Le mot « bus » désigne la ligne physique qui relie les machines du réseau.

Cette topologie est extrêmement vulnérable étant donné que si l'une des connexions est défectueuse, l'ensemble du réseau en est affecté. ![[topologie bus.png]]

## Topologie en étoile :
>Dans une topologie en étoile, les ordinateurs du réseau sont reliés à un système matériel central : soit un concentrateur (hub) soit à un commutateur (switch).

Si une liaison est en défaut, le réseau peut tout de même fonctionner.
On rencontre ce genre de topologie dans les lycées par exemples.
![[topologie en étoile.png]]
## Topologie maillée :
>Une topologie maillée correspond à plusieurs liaisons point à point (ex : les WAN
comme Internet). L'information peut parcourir le réseau suivant des itinéraires divers.

![[topologie mailée.png]]

# La communication
La communication entre deux ordinateurs peut être comparée à l’envoi d’un courrier postal entre un expéditeur et un destinataire.

### Adresse IP

1. Pour que l’ordinateur A puisse envoyer un message à l’ordinateur B, il doit connaître son adresse. Les deux ordinateurs ont une adresse unique sur le réseau qui permet de les identifier. Il s’agit de leur adresse IP. ![[electronic 1.png]]

2. Par analogie, lorsqu’une entreprise A veut envoyer un courrier à une autre entreprise B elle doit connaitre son adresse postale. ![[traditional 1.png]]

### Notion de port

1. Il peut y avoir plusieurs programmes qui fonctionnent en même temps sur le même ordinateur :
- un navigateur
- un logiciel d'email
- un logiciel de consultation de notes
- …. 
![[electronic 2.png]]

2. Dans l’entreprise B le courrier est adressé à un service particulier :
- service comptabilité
- service clients
- direction
- ….
![[traditional 2.png]]

A chaque logiciel correspond un numéro unique appelé port. Ce numéro est transmis en même temps que l’adresse IP. Les données reçues sont alors dirigées vers le « bon » destinataire. Un ordinateur possède 65535 ports. Les 1023 premiers sont réservés (http :80, ftp : 21, etc)On écrit donc sur la lettre l’adresse de l’entreprise
mais également le service destinataire.

### Notion de protocole
1. Les deux ordinateurs peuvent également échanger des données parce qu’ils utilisent les mêmes protocoles de communication. Cela permet par exemple :
- L’envoi d’un message avec OUTLOOK et sa lecture avec GMAIL car le codage du message est reconnu par les deux logiciels.
- L’envoi des données d’un ordinateur à un autre
- …
![[electronic 3.png]]

2. Le courrier transmis par l’entreprise (A) arrive bien à l’entreprise (B) par ce que :
- Le format de l’enveloppe respecte la norme
- Les éléments de l’adresse respectent les règles fixées par les sociétés d’acheminement du courrier (N° de rue, Code postal, …)
![[traditional 3.png]]

On respecte là aussi des PROTOCOLES de communication.

# Le modèle TCP / IP

Le sigle TCP/IP signifie « Transmission Control Protocol/Internet Protocol ».

>TCP/IP représente d'une certaine façon l'ensemble des règles de communication sur internet et se base sur la notion adressage IP, c'est-à-dire le fait de fournir une adresse IP à chaque machine du réseau afin de pouvoir acheminer des paquets de données.

Le système de protocoles TCP/IP a été décomposé en 4 modules effectuant les uns après les autres une tâche précise. On a donc un système stratifié, c’est la raison pour laquelle on parle de `modèle en couches`.

Chaque couche à une tâche précise. Une fois cette tâche réalisée elle transmet l’information à la couche voisine :

Au-dessus lors d’une réception

Au-dessous lors d’une émission

>Le protocole de transport TCP (Transmission Control Protocol) s’occupe
de découper l’information en segments.
Le protocole réseau IP (Internet Protocol) s’occupe d’identifier les paquets
avec des adresses IP.

![[modèle TCP ip.png]]
![[modele tcp ip example.png]]
![[modele tcp ip example 2.png]]

# Encapsulation des données
>A l’émission, les informations d’une couche sont « insérées » dans la couche voisine, en tant que « Données ». Ce phénomène se répète de couche en couche comme l’illustre le schéma ci-contre. Ce processus est appelé : ENCAPSULATION

![[encapsulation.png]]

# Le modèle OSI
Il existe d’autres modèles décrivant la transmission de l’information. Parmi ceux-ci, il en existe un, concurrent du modèle TCP/IP et plus détaillé : c’est le modèle OSI.

Le principe de fonctionnement est exactement le même que celui observé précédemment
Le `modèle OSI` (Open Systems Interconnect) est décomposé en `7 couches`.

`Comment se passe la communication entre machines ? Analogie Homme / Machine`

![[modèle iso.png]]

# Les protocoles de communication
### Couche physique :
>Cette couche est chargée de la transmission et de la conversion entre bits et signaux électriques ou optiques.

### Bluetooth :
Le `Bluetooth` est une technologie de réseau personnel sans fils (noté `WPAN` pour Wireless Personal Area Network), c’est-à-dire une technologie de réseaux sans fils d’une faible portée permettant de relier des appareils entre eux sans liaison filaire. Contrairement à la technologie `IrDa` (liaison infrarouge), les appareils Bluetooth ne nécessitent pas d’une ligne de vue directe pour communiquer, ce qui rend plus souple son utilisation et permet notamment une communication d’une autre pièce à une autre, sur de petits espaces.

### USB :
Le `bus USB` (Universal Serial Bus, en français Bus série universel) est, comme son nom l'indique, basé sur une architecture de type série. Il s'agit toutefois d'une interface entrée-sortie beaucoup plus rapide que les ports série standards.

Le standard `USB 1.0` propose deux modes de communication :
- 12 Mb/s en mode haute vitesse,
- 1.5 Mb/s à basse vitesse.
La norme `USB 2.0` permet d'obtenir des débits pouvant atteindre 480 Mbit/s.
La norme `USB 3.0` permet d'obtenir des débits pouvant atteindre à 4,8 Gbit/s.

## Couche liaison :
>La couche de liaison de données s'occupe de la livraison locale de trames entre dispositifs présents sur un même LAN.

### Ethernet :
Deux principaux types de câblage RJ45 :

- `Câblage droit : Il permet la communication entre une machine et un appareil réseau (switch, routeur, etc).`
- `Câblage croisé : Il permet la communication entre une machine et une autre machine.`

### WIFI :
Le Wi-Fi (Wireless Fidelity) est un ensemble de protocoles de communication sans fil.

>Un réseau Wi-Fi permet de relier par ondes radio plusieurs appareils informatiques (ordinateur, routeur, smartphone, décodeur Internet, etc.) au sein d'un réseau informatique afin de permettre la transmission de données entre eux.

### CPL :
La communication par `courants porteurs en ligne` (ou CPL) permet de construire un réseau informatique sur le réseau électrique d'une habitation ou d'un bureau, voire d'un quartier ou groupe de bureaux.

### Le bus I²C :
Conçu par Philips pour les applications de domotique et d’électronique domestique, le bus I²C permet de relierfacilement un microprocesseur et différents circuits.

### Le bus CAN :
Le bus CAN (Controller Area Network) est un bus système série très répandu dans beaucoup d'industries, notamment l'automobile. Il met en application une approche connue sous le nom de multiplexage, et qui consiste à raccorder à un même câble (un bus) un grand nombre de calculateurs qui communiqueront donc à tour de rôle.

## Couche réseau :
>La couche réseau construit une voie de communication de bout à bout à partir de voies de communication avec ses voisins directs.

Ses apports fonctionnels principaux sont donc :
- Le routage :
Détermination d'un chemin permettant de relier les 2 machines distantes.
- Le relayage :
Retransmission d'un PDU (Protocol Data Unit ou Unité de données de protocole) dont la destination n'est pas locale pour le rapprocher de sa destination finale.
• Le contrôle des flux :
Contrôle de congestion dans un réseau.

### IP :
Voir chapitre sur l’adressage IP.

#### IPv4 : IPv4 (Internet Protocol version 4) est la première version d'Internet Protocol (IP) à avoir été largement déployée, et qui forme encore en 2016 la base de la majorité des communications sur Internet.

#### IPv6 : Grâce à des adresses de 128 bits au lieu de 32 bits, IPv6 dispose d'un espace d'adressage bien plus important qu'IPv4. Cette quantité d'adresses considérable permet une plus grande flexibilité dans l'attribution des adresses et une meilleure agrégation des routes dans la table de routage d'Internet. La traduction d'adresse (NAT), qui a été rendue populaire par le manque d'adresses IPv4, n'est plus nécessaire.

### ARP :
> L’Address Resolution Protocol (ARP, protocole de résolution d’adresse) est un protocole effectuant la traduction d’une adresse de protocole de couche réseau (typiquement une adresse IPv4) en une adresse MAC (typiquement une adresse Éthernet), ou même de tout matériel de couche de liaison.

## Couche transport :
>La couche transport gère les communications de bout en bout entre processus.

### UDP :
Le User Datagram Protocol (UDP, en français protocole de datagramme utilisateur) est un des principaux protocoles de télécommunication utilisés par Internet.
UDP ne garantit pas la bonne livraison des datagrammes à destination, ni leur ordre d'arrivée. Il est également possible que des datagrammes soient reçus en plusieurs exemplaires.

### TCP :
Transmission Control Protocol (littéralement, « protocole de contrôle de transmissions »), abrégé TCP, est un protocole de transport fiable.
TCP et UDP utilise un numéro de port pour identifier les applications. À chaque extrémité (client/serveur) de la connexion TCP ou UDP est associé un numéro de port sur 16 bits (de 1 à 65535) assigné à l'application
émettrice ou réceptrice.

## Couche session :
Elle assure :
- Établissement, maintien et libération de la session : permet à deux processus applicatifs sur des ordinateurs différents d'établir, d'utiliser et de mettre fin à une connexion, appelée session.
- Prise en charge de session : exécute les fonctions qui permettent à ces processus de communiquer sur le réseau, de mettre en œuvre les procédures de sécurité, la reconnaissance du nom, l'enregistrement et ainsi de suite.

Protocole session principal pour Microsoft : NetBios
Protocole session principal pour Apple : AppleTalk

## Couche présentation :
>La couche présentation est chargée du codage des données applicatives.

Les couches 1 à 5 transportent des octets bruts sans se préoccuper de leur signification. Mais ce qui doit être transporté en pratique, c'est du texte, des nombres et parfois des structures de données arbitrairement complexes. Un protocole de routage par exemple doit transporter un graphe représentant au moins
partiellement la topologie du réseau. Le rôle de la couche présentation est donc de convertir les données applicatives manipulées par les programmes en chaînes d'octets.

### ASCII :
L'American Standard Code for Information Interchange (Code américain normalisé pour l'échange d'information), plus connu sous l'acronyme ASCII ([askiː]), est une norme informatique de codage de caractères apparue dans les années 1960. C'est la norme de codage de caractères la plus influente à ce jour. ASCII définit 128 codes à 7 bits, comprenant 95 caractères imprimables : les chiffres arabes de 0 à 9, les
lettres minuscules et capitales de A à Z, et des symboles mathématiques et de ponctuation.

*Voir cours codage de l’information.*

### Unicode :
Le standard Unicode est constitué d'un répertoire de 128 172 caractères. Il reprend la base du codage ASCII.

## Couche application :
>La couche d'application sert de fenêtre pour que les utilisateurs et les processus d'application aient accès aux services réseau.

Cette couche contient de nombreuses fonctions souvent nécessaires :
- Redirection des appareils et du partage des ressources
- Accès aux fichiers à distance
- Accès à l'imprimante distante
- Communication entre les processus
- Gestion de réseau
- Services d'annuaire
- Messagerie électronique (par exemple, courrier électronique)
- Terminaux virtuels de réseau

### DHCP :
> Dynamic Host Configuration Protocol (DHCP, protocole de configuration dynamique des hôtes) est un protocole dont le rôle est d’assurer la configuration automatique des paramètres IP d’une station, notamment en lui affectant automatiquement une adresse IP et un masque de sous-réseau.

### DNS :
>Le Domain Name System (ou DNS, système de noms de domaine) est un service permettant de traduire un nom de domaine en informations de plusieurs types qui y sont associées, notamment en adresses IP de la machine portant ce nom.

### SMTP :
>Simple Mail Transfer Protocol (SMTP, littéralement « protocole simple de transfert de courrier ») est un protocole utilisé pour transférer le courrier électronique (courriel) vers les serveurs de messagerie électronique.

### HTTP :
>L'HyperText Transfer Protocol, plus connu sous l'abréviation HTTP — littéralement « protocole de transfert hypertexte » — est un protocole de communication client-serveur développé pour le World Wide Web.

HTTPS (avec S pour secured, soit « sécurisé ») est la variante du HTTP sécurisée par l'usage des protocoles SSL ou TLS.

Les clients HTTP les plus connus sont les navigateurs Web permettant à un utilisateur d'accéder à un serveur contenant les données.

### FTP :
>File Transfer Protocol (protocole de transfert de fichier), ou FTP, est un protocole de communication destiné au partage de fichiers. Il permet, depuis un ordinateur, de copier des fichiers vers un autre ordinateur du réseau, ou encore de supprimer ou de modifier des fichiers sur cet ordinateur.