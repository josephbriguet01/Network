Copyright © JasonPercus Systems, Inc - All Rights Reserved
# **Introduction**

Cette librairie apporte une multitude de fonctions utiles permettant de manipuler les adresses IP. À savoir qu'elle possède un dépendance vers le projet :

- [Util-1.15.0](https://github.com/josephbriguet01/Util) (attention ce projet possède lui aussi des dépendances)

# **Network**
Ce projet permet de récupérer le nom des cartes réseaux, le nom des interfaces, l'adresse MAC, les IP...

### Explications sur les classes et interfaces
##### CharHexadecimal
La classe `CharHexadecimal.java` permet de créer un caractère hexadécimal.
On peut lui donner sa version en caractère hexadécimal et également en valeur décimal. 
Voici les correspondances des valeurs décimales et hexadécimales:
`0` *(décimal)* -> `0` *(hexadécimal)*, 
`1` *(décimal)* -> `1` *(hexadécimal)*, 
`2` *(décimal)* -> `2` *(hexadécimal)*, 
`3` *(décimal)* -> `3` *(hexadécimal)*, 
`4` *(décimal)* -> `4` *(hexadécimal)*, 
`5` *(décimal)* -> `5` *(hexadécimal)*, 
`6` *(décimal)* -> `6` *(hexadécimal)*, 
`7` *(décimal)* -> `7` *(hexadécimal)*, 
`8` *(décimal)* -> `8` *(hexadécimal)*, 
`9` *(décimal)* -> `9` *(hexadécimal)*, 
`10` *(décimal)* -> `A` *(hexadécimal)*, 
`11` *(décimal)* -> `B` *(hexadécimal)*, 
`12` *(décimal)* -> `C` *(hexadécimal)*, 
`13` *(décimal)* -> `D` *(hexadécimal)*, 
`14` *(décimal)* -> `E` *(hexadécimal)*, 
`15` *(décimal)* -> `F` *(hexadécimal)*
Voici comment on crée un objet `CharHexadecimal`:
```java
// Création d'un objet CharHexadecimal à partir d'une valeur décimale
CharHexadecimal hex1 = new CharHexadecimal(12);

// Création d'un objet CharHexadecimal à partir d'un caractère hexadécimal
CharHexadecimal hex2 = new CharHexadecimal('c');

// On teste que ces deux objets sont identiques
System.out.println("Test [" + hex1 + " = " + hex2 + " ?] -> "+hex1.equals(hex2));
```
Ceci nous affiche comme résultat
```
Test [c = c ?] -> true
```
>Si on entre dans le constructeur une valeure inférieure à `0` et supérieure à `15`, l'exception `InvalidNumberException` est levée.
>Si on entre dans le constructeur le caractère `'g'`, l'exception `InvalidCharacterException` est levée.

##### ChainHexadecimal
La classe `ChainHexadecimal.java` permet de créer des chaînes hexadécimales de caractères.
On peut créer un objet de ce type à partir d'une chaîne String contenant que des caractères hexadécimaux: exemple `47ab53fc`. Ou à partir d'une liste de `CharHexadecimal`: exemple `List<CharHexadecimal> lch = ...`

Voici comment on crée un objet `ChainHexadecimal`:
```java
// Création d'un objet ChainHexadecimal à partir d'une chaîne String.
ChainHexadecimal sHex1 = new ChainHexadecimal("47ab53fc");

// Création d'une liste de CharHexadecimal
List<CharHexadecimal> lHex = new ArrayList<>();
lHex.add(new CharHexadecimal('8'));
lHex.add(new CharHexadecimal('7'));
lHex.add(new CharHexadecimal('a'));
lHex.add(new CharHexadecimal('b'));
lHex.add(new CharHexadecimal('5'));
lHex.add(new CharHexadecimal('3'));
lHex.add(new CharHexadecimal('f'));
lHex.add(new CharHexadecimal('c'));

// Création d'un objet ChainHexadecimal à partir d'une liste de CharHexadecimal
ChainHexadecimal sHex2 = new ChainHexadecimal(lHex);

// On teste que ces deux objets sont identiques
System.out.println("Test [" + sHex1 + " = " + sHex2 + " ?] -> "+sHex1.equals(sHex2));
```
Ceci nous affiche comme résultat
```
Test [47ab53fc = 87ab53fc ?] -> false
```
> Les mêmes exceptions que pour `CharHexadecimal` sont levées si la chaîne est incorrecte...

> Remarque: `ChainHexadecimal` implémente `CharSequence`

##### IPv4
La classe `IPv4.java` permet de créer des adresses IP de type 4.
On peut créer un objet de ce type à partir d'une chaîne String: exemple `"192.168.1.1"`. Ou à partir d'un tableau de bytes: exemple `{-64, -88, 1, 1}`.

Voici comment on crée un objet IPv4:
```java
// Création d'un objet IPv4 par défaut.
IPv4 ip0 = new IPv4();

// Création d'un objet IPv4 à partir d'une chaîne String.
IPv4 ip1 = new IPv4("192.168.1.1");

// Création d'un tableau de bytes
byte[] array = {-64, -88, 1, 1};

// Création d'un objet IPv4 à partir d'un tableau de bytes
IPv4 ip2 = new IPv4(array);

// On teste que deux adresses IP sont identiques
System.out.println("Test [" + ip0 + " = " + ip1 + " ?] -> "+ip0.equals(ip1));

// On teste que ces deux adresses IP sont identiques
System.out.println("Test [" + ip1 + " = " + ip2 + " ?] -> "+ip1.equals(ip2));

// On récupère et on affiche l'ip publique du réseau local
System.out.println("IP Publique: "+IPv4.getPublicIP());
```
Ceci nous affiche comme résultat
```
Test [0.0.0.0 = 192.168.1.1 ?] -> false
Test [192.168.1.1 = 192.168.1.1 ?] -> true
IP Publique: 87.198.63.149
```
> On peut également récupérer l'adresse IPv4 principale de l'équipement qui exécute la méthode `IPv4.getMainLocalIPv4()`. Cette méthode est pratique lorsque l'on possède plusieurs IP statiques et que l'on veut connaître la principale.

##### MaskIPv4
La classe `MaskIPv4.java` permet de créer des masques IP de type 4. Cette classe hérite de `IPv4.java`. Elle possède donc des méthodes supplémentaires:
 - public static String getSimplifiedNorm(MaskIPv4 ipv4): Permet de transformer un masque de ce type `255.255.0.0` au type `/16`.
 - public static MaskIPv4 getFullNorm(String simplifiedNorm): Permet de transformer un masque de ce type `/16` au type `255.255.0.0`.

> Attention: A la création d'un masque une vérification supplémentaire est réalisée. En effet certains masques sont impossibles à créer. Exemple: `255.255.192.128`. cette création lèvera l'exception `InvalidAddressException`.

> On peut également récupérer le masque principale de l'équipement qui exécute la méthode `IPv4.getMainLocalMask()`. Cette méthode est pratique lorsque l'on possède plusieurs IP statiques et que l'on veut connaître le masque principal.

##### MACAddress
La classe `MACAddress.java` permet de créer et gérer des adresses MAC.
On peut créer un objet de ce type à partir d’une chaîne String: exemple "88-51-FC-55-30-A4". Ou à partir d’un tableau de bytes: exemple {-120, 81, -4, 85, 48, -92}.

Voici comment on crée un objet MACAddress:
```java
// Création d'un objet MACAddress par défaut.
MACAddress mac0 = new MACAddress();

// Création d'un objet MACAddress à partir d'une chaîne String.
MACAddress mac1 = new MACAddress("88-51-FC-55-30-A4");

// Création d'un tableau de bytes
byte[] array = {-120, 81, -4, 85, 48, -92};

// Création d'un objet MACAddress à partir d'un tableau de bytes
MACAddress mac2 = new MACAddress(array);

// On teste que deux adresses MAC sont identiques
System.out.println("Test [" + mac0 + " = " + mac1 + " ?] -> "+mac0.equals(mac1));

// On teste que ces deux adresses MAC sont identiques
System.out.println("Test [" + mac1 + " = " + mac2 + " ?] -> "+mac1.equals(mac2));
```
Ceci nous affiche comme résultat
```
Test [00-00-00-00-00-00 = 88-51-FC-55-30-A4 ?] -> false
Test [88-51-FC-55-30-A4 = 88-51-FC-55-30-A4 ?] -> true
```

> Une mauvaise création d'adresse MAC entraine la levée de l'exception `InvalidAddressException`.

> On peut également récupérer l'adresse MAC principale de l'équipement qui exécute la méthode `IPv4.getMainLocalMACAddress()`. Cette méthode est pratique lorsque l'on possède plusieurs IP statiques et que l'on veut connaître l'adresse MAC principale de l'équipement.

##### IPCard
La classe `IPCard.java` permet d'associer une adresse IP avec un masque et une adresse de broadcast.

Voici comment on crée un objet IPCard:
```java
// Création d'une adresse IP
IPv4 ip = new IPv4("192.168.1.1");

// Création d'un masque
MaskIPv4 mask = MaskIPv4.getFullNorm("/24");

// Création d'une adresse de broadcast
BroadcastIPv4 broadcast = new BroadcastIPv4("192.168.1.255");

// Création d'un objet IPCard.
IPCard ipCard = new IPCard(ip, mask, broadcast);

// Affichage de l'objet IPCard
System.out.println(ipCard);
```
Ceci nous affiche comme résultat
```
IPCard(ip: 192.168.1.1, mask: 255.255.255.0, broadcast: 192.168.1.255)
```

##### NetworkCard
La classe `NetworkCard.java` permet de lier une adresse MAC avec le nom de la carte réseau, le nom de l'interface réseau, le numéro de la carte et les `IPCards` de la carte réseau.

Voici comment on crée un objet NetworkCard:
```java
// Création d'un objet MACAddress à partir d'une chaîne String.
MACAddress mac = new MACAddress("88-51-FC-55-30-A4");

// Création d'une IPCard
IPCard ipc1 = new IPCard(new IPv4("192.168.1.1"), MaskIPv4.getFullNorm("/24"), new BroadcastIPv4("192.168.1.255"));

// Création d'une autre IPCard
IPCard ipc2 = new IPCard(new IPv4("192.168.0.36"), MaskIPv4.getFullNorm("/24"), new BroadcastIPv4("192.168.0.255"));

// Création d'une liste d'IPCard
List<IPCard> lipc = new ArrayList<>();
lipc.add(ipc1);
lipc.add(ipc2);

// Création d'un objet NetworkCard
NetworkCard nc = new NetworkCard(mac, "Realtek PCIe GBE Family Controller", "eth1", 1, lipc);

// Affichage de l'objet NetworkCard
System.out.println(nc);
```
Ceci nous affiche comme résultat
```
NetworkCard(@MAC: 88-51-fc-55-30-a4, name: Realtek PCIe GBE Family Controller, nameEth: eth1, index: 1, ipCards: [IPCard(ip: 192.168.1.1, mask: 255.255.255.0, broadcast: 192.168.1.255), IPCard(ip: 192.168.0.36, mask: 255.255.255.0, broadcast: 192.168.0.255)])
```

##### Network
La classe `Network.java` permet de récupérer la liste des cartes réseaux d'un système d'exploitation...
Elle ne contient qu'un seul constructeur: `public Network(){}`.

Voici comment on crée un objet Network:
```java
// Création d'un objet Network par défaut.
Network net = new Network();

// Récupère une liste de NetworkCard
java.util.List<NetworkCard> list = net.getHardwareList();

// Affiche chaque NetworkCard
for(NetworkCard nc : list)
    System.out.println(nc);

// On crée un masque de réseau
MaskIPv4 mask = Mask.getFullNorm("/24");

// On récupère l'adresse IP d'un réseau avec l'adresse IP d'un équipement ainsi que le masque de réseau
IPv4 ipNetwork = Network.getIPNetwork(new IPv4("192.168.0.35"), mask);

// On récupère l'adresse de broadcast d'un réseau avec l'adresse IP d'un réseau aunsi que son masque
BroadcastIPv4 ipBroadcast = Network.getIPBroadcast(ipNetwork, mask);

// On récupère un pool d'adresse utilisable comprise dans le réseau 192.168.0.0
PoolIPv4 pool = Network.getPoolIpv4(ipNetwork, mask);

// On récupère le nombre d'adresses utilisables (sans l'adresse du réseau et de broadcast)
long count = pool.count();

// On affiche toute les adresses IP utilisable sur le réseau 192.168.0.0/24
for(long l=0; l<count; l++)
    System.out.println(pool.next());
```
Ceci nous affiche comme résultat
```
NetworkCard(@MAC: null, name: WAN Miniport (SSTP), nameEth: net0, index: 2, ipCards: [])
NetworkCard(@MAC: null, name: WAN Miniport (L2TP), nameEth: net1, index: 3, ipCards: [])
NetworkCard(@MAC: null, name: WAN Miniport (PPTP), nameEth: net2, index: 4, ipCards: [])
NetworkCard(@MAC: null, name: WAN Miniport (PPPOE), nameEth: ppp0, index: 5, ipCards: [])
NetworkCard(@MAC: null, name: WAN Miniport (IPv6), nameEth: eth0, index: 6, ipCards: [])
NetworkCard(@MAC: null, name: WAN Miniport (Network Monitor), nameEth: eth1, index: 7, ipCards: [])
NetworkCard(@MAC: null, name: WAN Miniport (IP), nameEth: eth2, index: 8, ipCards: [])
NetworkCard(@MAC: null, name: RAS Async Adapter, nameEth: ppp1, index: 9, ipCards: [])
NetworkCard(@MAC: null, name: WAN Miniport (IKEv2), nameEth: net3, index: 10, ipCards: [])
NetworkCard(@MAC: 88-51-fb-55-30-a4, name: Realtek PCIe GBE Family Controller, nameEth: eth3, index: 11, ipCards: [IPCard(ip: 192.168.201.35, mask: 255.255.255.0, broadcast: 192.168.201.255), IPCard(ip: 192.168.31.48, mask: 255.255.255.0, broadcast: 192.168.31.255), IPCard(ip: 192.168.0.36, mask: 255.255.255.0, broadcast: 192.168.0.255)])
...
192.168.0.1
192.168.0.2
192.168.0.3
192.168.0.4
192.168.0.5
...
192.168.0.251
192.168.0.252
192.168.0.253
192.168.0.254
```
Il est possible de parcourir un pool dans le sens inverse pour cela il faut placer le curseur à la fin du pool avec la méthode `setCursorEnd()` *(l'inverse c'est: `setCursorBeginning()`)* puis d'utiliser la méthode `previous()` au lieu de `next()`.
##### Scanner
La classe `Scanner.java` permet de récupérer la liste des équipements réseaux d'un réseau LAN.
```java
// Crée un objet scanner
Scanner scanner = new Scanner();

// On vérifie que le port 80 d'un PC est ouvert
boolean open = scanner.portIsOpen(new IPv4("192.168.0.1"), 80);

// On scanne toutes les ip du réseau LAN
ResultScan rs = scanner.listLanHardware(new IPv4("192.168.0.0"));

// On scanne toutes les ip inactives du réseau LAN
rs = scanner.listLanHardware(new IPv4("192.168.0.0"), "/n");

// On scanne toutes les ip actives du réseau LAN
rs = scanner.listLanHardware(new IPv4("192.168.0.0"), "/a");

// On scanne toutes les ports de 0 à 1024 d'un équipement
ResultScan rsp = scanner.listPort(new IPv4("192.168.0.0"));

// On scanne toutes les ports de 100 à 512 d'un équipement
rsp = scanner.listPort(new IPv4("192.168.0.1"), "/m 100", "/M 512");

// On scanne toutes les ports inactifs de 100 à 512 d'un équipement
rsp = scanner.listPort(new IPv4("192.168.0.1"), "/m 100", "/M 512", "/n");

// On scanne toutes les ports actifs de 100 à 512 d'un équipement
rsp = scanner.listPort(new IPv4("192.168.0.1"), "/m 100", "/M 512", "/a");

// On scanne toutes les ports TCP actifs de 100 à 512 d'un équipement
rsp = scanner.listPort(new IPv4("192.168.0.1"), "/m 100", "/M 512", "/a", "/tcp");

// On scanne toutes les ports UDP inactifs de 100 à 512 d'un équipement
rsp = scanner.listPort(new IPv4("192.168.0.1"), "/m 100", "/M 512", "/n", "/udp");

// Affiche tous les équipements réseaux du LAN
for(int i=0;i<rs.getEquipments().length;i++)
    System.out.println(rs.getEquipments()[i]);

// Affiche tous les ports d'un équipement réseau ainsi que leurs noms
for(int i=0;i<rsp.getEquipmentPorts().length;i++)
    System.out.println(rsp.getEquipmentPorts()[i] + " - nom: " + rsp.getEquipmentPorts()[i].getName());
    
// Affiche un port TCP non utilisé
System.out.println(scanner.getFreePortTCP());

// Affiche un port UDP non utilisé
System.out.println(scanner.getFreePortUDP());
```

##### Ping
La classe `Ping.java` permet de créer des pings vers des équipements ou des urls.

###### Exemples:
Créons un Ping infini vers une destination présente sur le réseau
```java
Ping ping = new Ping("192.168.1.1");
ping.addPingListener(new PingListener() {
    @Override
    public void newPingResult(String hostOrIp, ResultPing result) {
        System.out.println(hostOrIp+" - "+result);
    }
});
ping.execute();
```
Ce qui nous donne comme résultat:
```
192.168.1.1 - SuccessPing{from=192.168.1.1, bytes=32, time=1, ttl=64}
192.168.1.1 - SuccessPing{from=192.168.1.1, bytes=32, time=1, ttl=64}
192.168.1.1 - SuccessPing{from=192.168.1.1, bytes=32, time=2, ttl=64}
192.168.1.1 - SuccessPing{from=192.168.1.1, bytes=32, time=6, ttl=64}
...
```
> Comme on le constate on reçoit un objet ```SuccessPing```. En réalité il s'agit bien d'un ```ResultPing```. Car il y a héritage.

Créons un Ping fini (disons 4 pings) vers une destination non présente sur le réseau
```java
Ping ping = new Ping("192.168.1.200", 4);
ping.addPingListener(new PingListener() {
    @Override
    public void newPingResult(String hostOrIp, ResultPing result) {
        System.out.println(hostOrIp+" - "+result);
    }
});
ping.execute();
```
Ce qui nous donne comme résultat:
```
192.168.1.200 - FailedPing{from=192.168.1.200}
192.168.1.200 - FailedPing{from=192.168.1.200}
192.168.1.200 - FailedPing{from=192.168.1.200}
192.168.1.200 - FailedPing{from=192.168.1.200}
```
> Comme on le constate on reçoit un objet ```FailedPing```. En réalité il s'agit bien d'un ```ResultPing```. Car il y a héritage.

Il est possible d'envoyer un seul ping avec une méthode static. Ce qui peut être assez pratique.
```java
ResultPing result = Ping.execute(new IPv4("192.168.1.1"));
System.out.println(result);
```
Ce qui nous donne comme résultat:
```
SuccessPing{from=192.168.1.1, bytes=32, time=1, ttl=64}
```
Lorsqu'un ping est en cours, il est possible de le killer de force avec la méthode ```kill()```.
Il est également possible de savoir si un ping est en cours avec la méthode ```isRunning()```.

# **Licence**
Le projet est sous licence "GNU General Public License v3.0"

## Accès au projet GitHub => [ici](https://github.com/josephbriguet01/Network "Accès au projet Git Network")