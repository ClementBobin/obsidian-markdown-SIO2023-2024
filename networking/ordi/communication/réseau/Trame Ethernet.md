# Trame Ethernet et Datagramme IP

## Trame Ethernet

Une trame Ethernet est un format de paquet de données utilisé pour la communication dans un réseau local (LAN). Elle est composée de plusieurs champs, chacun jouant un rôle spécifique dans le processus de transmission des données.

![[trame ethernet.PNG]]
### Champs de la Trame Ethernet

1. **Preambule (7 octets):** Un motif de bits utilisé pour synchroniser le récepteur avec le signal.
	
2. SFD (1 octets) The term "SFD" in networking and data communication often stands for "Start Frame Delimiter."
    
3. **Adresse de Destination (6 octets):** L'adresse physique (MAC) de la destination.
    
4. **Adresse Source (6 octets):** L'adresse MAC de l'émetteur.
    
5. **Type (2 octets):** Indique le protocole encapsulé dans la trame (IPv4, ARP, etc.).
    
6. **Données (46-1500 octets):** Les données réelles à transmettre, allant de 46 à 1500 octets.
    
7. **FCS, CRC (4 octets):** Somme de contrôle de trame pour la détection d'erreurs.

### Table des EtherType (Type de Trame Ethernet)

|EtherType (Hex)|Protocole|
|---|---|
|0x0800|IPv4|
|0x0806|ARP|
|0x86DD|IPv6|
|0x8100|VLAN Tagging|
|0x0800|PPPoE Discovery|
|...|...|

## Datagramme IP

Un datagramme IP est un paquet de données utilisé dans les réseaux IP pour acheminer des informations d'un hôte à un autre.
![[datagramme ip.PNG]]
### Champs du Datagramme IP

1. **Version (4 bits):** Indique la version du protocole IP utilisé (IPv4 ou IPv6).
    
2. **IHL (4 bits):** Longueur de l'en-tête IP en mots de 32 bits. (nota: valeur minimale est 5)
    
3. **Type de Service (8 bits):** Indique la priorité de traitement et le type de service.
    
4. **Longueur Totale (16 bits):** Longueur totale du datagramme en octets.
    
5. **Identification (16 bits):** Identifie le datagramme lors de la fragmentation.
    
6. **Flags (3 bits):** Contrôle la fragmentation des datagrammes.
    
7. **Fragment Offset (13 bits):** Indique la position d'un fragment dans le datagramme original.
    
8. **Time to Live (8 bits):** Indique le nombre maximal de sauts avant expiration.
    
9. **Protocole (8 bits):** Indique le protocole encapsulé (TCP, UDP, ICMP, etc.).
    
10. **Checksum d'En-Tête (16 bits):** Somme de contrôle de l'en-tête IP.
    
11. **Adresse Source (32 bits):** Adresse IP de l'expéditeur.
    
12. **Adresse Destination (32 bits):** Adresse IP du destinataire.
    
13. **Options (0-320 bits):** Options facultatives pour des fonctionnalités spécifiques.
    
14. **Données:** Les données à transmettre dans le datagramme. (ici segment tcp)
    

Ces concepts de trame Ethernet et de datagramme IP sont essentiels pour comprendre le fonctionnement des réseaux informatiques et la manière dont les données sont transmises d'un hôte à un autre. Pour une communication réussie, il est crucial que les différents champs soient correctement configurés et interprétés.