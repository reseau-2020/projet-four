## 5 Etherchannel

Pour la communication entre la couche Access et la couche Distribution appelé "switch block" nous avons utilisé la technologie Etherchannel (ou Portchannel) propriétaire cisco 
qui existe aussi en version ouverte avec le standard IEEE 802.3ad
Etherchannel permet d'assembler plusieurs liens physiques en un seul lien logique (agrégation de liens) dans le but d'augmenter la vitesse mais aussi la tolérance aux pannes.
Cela permettra d'augmenter la bande passante dans le "switch block".

### 5.1 Configuration

Dans notre topologie nous avons configuré 5 ports Etherchannel :

Ports channel | Ports physique | Commutateurs
|-------------|----------------|-------------
po1  | g0/0, g1/0 | AS1-DS1
po2  | g0/1, g1/1 | AS1-DS2
po3  | g0/2, g1/2 | DS1-DS2
po4  | g0/0, g1/0 | AS2-DS2
po5  | g0/1, g1/1 | AS2-DS1

Le maillage entre liaisons Etherchannels entre les switch Access (AS1&2) et les switch distribution (DS1&2) permettent d'assurer une redondance de liens.
Pour configurer un lien Etherchannel on assigne 2 interfaces au même channel-group et on active le mode `desirable` pour avoir une configuration dynamique d'Etherchannel avec le périphérique relié au même lien physique.

__Exemple configuration sur DS1:__

    interface range g0/0,g1/0
     shutdown
     channel-group 1 mode desirable   ! --> Chaque lien etherchannel correspond a un numéro de groupe différent
     no shutdown
     ...
   
Le trunking doit aussi être activé sur les liens Etherchannels.

### 5.2 Diagnostiques

Les commandes suivantes permettent de diagnostiquer des erreurs sur Etherchannel:
- `show interface etherchannel`                                                --> Voir les interfaces configurées en Etherchannel
- `show etherchannel [summary | port | load-balance | port-channel | detail]`  --> Voir le détailde la configuration Etherchannel
- `show [pagp | lacp ] neighbors`                                              --> En config dynamique voir le voisinage Etherchannel
   
   
