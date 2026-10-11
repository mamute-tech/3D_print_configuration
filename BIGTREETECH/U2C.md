# U2C

<img src=images/U2C/U2C_Title1.jpg width="600"/>

## **Présentation**

BIGTREETECH U2C est un module USB vers bus CAN bus, qui peut convertir un port USB d'un Raspberry Pi en bus CAN, et connecter une carte mère d'imprimante 3D, BIGTREETECH EBB35/36/42 CAN et d'autres produits au bus CAN. Il y a différents type d'interfaces CAN sur la carte, ce qui permet de la connecter à différents cartes.

Le bus CAN présente de nombreux avantages dans le domaine du contrôle industriel, c'est pourquoi BIGTREETECH a lancé ce module USB vers CAN. Le bus CAN permet une longue portée de transmission et peut accueillir un grand nombre de nœuds, ainsi la carte mère, l'EBB et d'autres cartes d'extension peuvent être connectées simultanément au même bus CAN.

**Lien produit:** https://biqu.equipment/products/bigtreetech-ebb-sb2209-can-v1-0?variant=40214284468322

## **Fonctionnalités**

- Prend en charge la connexion par bus CAN, la transmission de données sur longue distance, une forte immunité au bruit, d'excellentes performances en temps réel et une grande fiabilité.
- La surface du circuit imprimé utilise le procédé ENIG.
- Le port USB TYPE-C est doté d'une protection ESD pour empêcher l'électricité statique d'endommager le matériel.
- Prend en charge la mise à jour du firmware de la carte mère via SWD ou DFU.
- Bien plus sur l'interface CAN.

## **Dimensions**

<img src=images/U2C/U2C_Dimension.jpg width="600"/>

## **Connectique**

<img src=images/U2C/U2C_CAD.jpg width="600"/>

CAN_IN: USB vers CAN interface pour connecter le Raspberry Pi.

CAN_OUT*: utilisé pour connecter une interface sans transmission CAN mais avec la fonction CAN, comme le raccordement au port USB de la carte mère, où la broche reliant le port USB de la carte mère au contrôleur principal doit disposer de la fonction CAN. Par exemple : 

<img src=images/U2C/U2C_CAD1.jpg width="600"/>

CAN_OUT: Utilisé pour connecter une BIGTREETECH EBB CAN ou une autre carte avec transmission CAN.

Power: Alimentation.

## **Détail de la connectique**

<img src=images/U2C/U2C_Pinout.jpg width="600"/>

## **Présentation**

<img src=images/U2C/U2C_Display1.jpg width="600"/>

<img src=images/U2C/U2C_Display2.jpg width="600"/>

<img src=images/U2C/U2C_Display3.jpg width="600"/>

<img src=images/U2C/U2C_Display4.jpg width="600"/>

<img src=images/U2C/U2C_Display5.jpg width="600"/>

## **Configuration Matérielle**

### **Diagramme de cablage optionnel**

<img src=images/U2C/U2C_Wiring.jpg width="600"/>

## **Configuration Logicielle**

### **Code Source du Firmware**

V1.0/1.1: utiliser le firmware open source CandleLight du dépot suivant: 
https://github.com/candle-usb/candleLight_fw

MCU Model: STM32F072C8


V2.0/2.1: Le support du STM32G0 est ajouté au base du firmware  open source CandleLight dans le dépot suivant:
https://github.com/bigtreetech/candleLight_fw/tree/stm32g0_support 

MCU Model: STM32G0B1C8

### **Compilation du Firmware**

**connectez vous en ssh**

* U2C V1.0/1.1:
```
# installer les prérequis
sudo apt-get install cmake gcc-arm-none-eabi

cd ~
# clone git repo
git clone --depth=1 -b stm32g0_support https://github.com/candle-usb/candleLight_fw
cd ~/candleLight_fw

# créer la toolchain cmake
mkdir build
cd build
cmake .. -DCMAKE_TOOLCHAIN_FILE=../cmake/gcc-arm-none-eabi-8-2019-q3-update.cmake

# compiler firmware
make candlelight_fw
```

* U2C V2.0/2.1:
```
# installer les prérequis
sudo apt-get install cmake gcc-arm-none-eabi

cd ~
# clone git repo
git clone --depth=1 -b stm32g0_support https://github.com/bigtreetech/candleLight_fw
cd ~/candleLight_fw

# créer la toolchain cmake
mkdir build
cd build
cmake .. -DCMAKE_TOOLCHAIN_FILE=../cmake/gcc-arm-none-eabi-8-2019-q3-update.cmake

# compiler firmware
make candlelight_fw
```


### **Mise à jour du Firmware**

Après avoir débrancher le module, presser maintenir le bouton Boot, Brancher le cable Type-C pour allumer le module, entrer en mode DFU.

<img src=images/U2C/U2C_DFU.jpg width="600"/>

Avec `dfu-util -l`, vous pouvez vérifier si l'adaptateur a démarré en mode DFU. Le résultat devrait ressembler à ceci :

Si dfu-util parvient à détecter une carte en mode DFU, le résultat devrait alors ressembler à ceci :
<img src=images/U2C/dfu-util_-l.svg>
en cas d'erreur `dfu-util: Cannot open DFU device 0483:df11 found on devnum 26 (LIBUSB_ERROR_ACCESS)` 
exécutez `sudo dfu-util -l`

Si le BTT U2C a démarré en mode DFU, vous pouvez le flasher avec cette commande :

```
make flash-candlelight_fw
```
Cela devrait ressembler à ça:
<img src=images/U2C/flash_candlelight.svg>

**Débrancher et rebrancher l'USB TYPE-C pour redémarrer l'U2C**

### **Configuration de Klipper**

Référence de Configuration du Firmware: 
https://www.klipper3d.org/CANBUS.html

1. Entrer la commande dans un terminal ssh 

```
sudo nano /etc/network/interfaces.d/can0 
```

et complétez avec:

```
auto can0
iface can0 can static
bitrate 1000000
up ifconfig $IFACE txqueuelen 1024
```
Avec l'éditeur nano `ctrl+s` pour sauver le fichier et `ctrl+x` pour fermer l'éditeur.

<font  color="red">***Mettre la vitesse du CANBus à 1000000 (doit être la même vitesse que celle fixée dans le firmware (1000000) CAN bus speed), entrer "sudo reboot" pour redémarrer le Raspberry Pi.***</font>

2. Chaque appareil relié au CANBus génère un "canbus_uuid" basé sur le MCU's UID, pour trouver chaque microcontroller device ID, Assurez-vous que le matériel est sous tension et correctement câblé, puis exécutez :

```
~/klippy-env/bin/python ~/klipper/scripts/canbus_query.py can0
```

3. Si un appareil CAN non initialisé est détecté, La commande suivant affichera le canbus_uuid de l'appareil:

```
Found canbus_uuid=0e0d81e4210c
```

4. Si Klipper est déjà en cours d'exécution et connecté à cet appareil, le canbus_uuid ne sera pas affiché, ce qui est normal.

## **Precautions**

- les 12/24V et GND doivent être correctement connectés.
- Lors de l'utilisation de la communication CAN, vous devez identifier quel appareil CAN sert de terminaison. Sur chaque terminaison, vous devez placer le cavalier sur la position 120R.



## Lien d'achat produit
**Lien:**

https://biqu.equipment/products/bigtreetech-ebb-36-42-can-bus-for-connecting-klipper-expansion-device?variant=39762747949154

## Sources
**Documentation BIGTREETECH:**

https://github.com/bigtreetech/docs/blob/master/docs/U2C.md

https://github.com/bigtreetech/U2C

**Vidéo de Teaching Tech:**

https://www.youtube.com/watch?v=5pLjeQz9pEI

**Documentation Klipper de Metoyou:**

https://docs.meteyou.wtf/btt-u2c-v1.x/candlelight/

https://docs.meteyou.wtf/btt-u2c-v2.x/candlelight/

**Documentation CANBUS Klipper:**

https://www.klipper3d.org/CANBUS.html