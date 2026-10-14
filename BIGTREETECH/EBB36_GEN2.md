# **EBB36 GEN2 V1.0**

<img src=images/EBB36_GEN2/EBB36_GEN2.jpg width="300"/>

- **Lien Produit**: [Buy Here](https://biqu.equipment/products/bigtreetech-ebb-36-42-can-bus-for-bigtreetech-ebb-36-42-can-bus-u2c-v2-1-for-connecting-klipper-expansion-device-support-pt1000connecting-klipper-expansion-device?variant=42238091821154)  

## **Introduction**

Un saut générationnel dans la conception des panneaux porte-outils.

Une protection complète pour réduire les risques de dommages, associée à du matériel d'amplification du signal garantissant des performances CAN et USB d'une fiabilité absolue.

Passage du mode CAN à l'USB à l'aide d'un simple cavalier.

#### **Fonctionnalités**

* Protection des circuits sur la quasi-totalité des entrées et sorties pour éviter tout dommage dû à des erreurs de connexion involontaires.

* Passage de la connectivité CAN à la connectivité USB à l'aide d'un seul cavalier, et le port de transfert s'ajuste automatiquement au nouveau réglage.

* Amplificateurs de signal pour garantir une connectivité USB d'une fiabilité absolue.

* Testé jusqu'à une température d'enceinte de 75 °C pour garantir des performances à long terme (l'utilisation d'un ventilateur est recommandée pour un fonctionnement au-delà de 60 °C).

* Ventilateur de tête d'impression à 3 broches avec signal tachymétrique pour la détection de panne.

* Sélection de tension (5 V / 24 V) disponible pour tous les ventilateurs.

* Port I²C pour la connexion à des capteurs environnementaux ou à courants de Foucault.

* Thermistance dédiée à la mesure de la température du pilote de moteur.

* Trois sorties pour ventilateurs pilotables par PWM, avec protection contre les courts-circuits et protection thermique.

* Boutons "reset" et "boot" repositionnés pour un accès pratique.

* Puce de contrôle principale : ARM Cortex-M0+ STM32G0B1CBT6, 64 MHz.

* Trous de montage reliés à la masse pour la dissipation des décharges électrostatiques (ESD).

### **Spécifications Techniques**

| Nom du Produit | BIGTREETECH EBB 36 GEN2 V1.0 |
|------|--------------|
| Puce Principale | ARM Cortex-M0+ STM32G0B1CBT6, 64MHz |
| Alimentation | DCIN=DC24V-DC28V |
| Tension Logique | DC3.3V |
| Alimentation Hotend | 120 W (24 V / 5 A) |
| Compatibilité de la Thermistance de la Hotend | PT1000 or NTC |
| Interfaces Ventillateurs | 2x 2-pin PWM (FAN0, FAN1)<br>1x 3-pin (FAN2) avec retour d'information tachymétrique. |
| Courant nominal de l'interface du ventilateur | Total: 1 A,  Courant de crête: 1.5 A<br>Protection intégrée contre les surintensités et les surchauffes. |
| Courant Maximum en 5V (Carte Mère) | Crête: 1.5 A |
| Extensions | Sondes (microsonde multiplexée, BLTouch, port de sonde 24 V), RGB, TH, moteurs, ports d'extension USB/CAN, et autres. |

### **Dimensions**

<img src=images/EBB36_GEN2/size.jpg width="500"/>

## **Interfaces périphériques**

### **Interface EBB36 GEN2 - Diagramme**

<img src=images/EBB36_GEN2/interface.jpg width="1000"/>

### **EBB adaptateur USB - Diagramme**

<img src=images/EBB36_GEN2/interface_adapter.jpg width="1000"/>

## **Descriptions de l'Interface**

### **Alimentation de l'Interface**

<img src=images/EBB36_GEN2/power_supply.jpg width="300"/>

* **Notes importantes au suje de l'adapatateur EBB USB**

    Afin d'intégrer un maximum de fonctionnalités sur la carte d'outils, certains composants de protection essentiels ont été transférés sur la carte adaptatrice. Par conséquent, l'alimentation électrique débute au niveau de la carte adaptatrice, et cette dernière ne doit pas être contournée lors de l'installation.

* **Méthode de Connection de l'Alimentation**

    Pour raccorder l'alimentation, il suffit d'utiliser les câbles fournis pour relier la carte adaptatrice à une source d'alimentation 24 V. Veillez à respecter scrupuleusement la polarité du raccordement, conformément au schéma des broches et au marquage sérigraphié sur le circuit imprimé (PCB). La carte adaptatrice est équipée d'un connecteur de sortie MX qui transmet à la fois l'alimentation et les signaux de communication. Pour les utilisateurs souhaitant employer un ancien type de faisceau avec des câbles séparés pour l'alimentation et le signal, nous avons également prévu un bornier à vis pour la sortie d'alimentation.

    > **À noter** Cela ne doit être utilisé que pour les connexions CAN, car les connexions USB nécessitent l'utilisation du câble fourni en raison du blindage.

    L'interface d'alimentation utilise un connecteur XT30, conçu pour une tension de 24 V. Si vous souhaitez faire passer le câble à travers un presse-étoupe, il peut être nécessaire de retirer le connecteur XT30 ; cette opération peut être effectuée à l'aide d'un outil tel que celui-ci : [Molex Microfit 3.0 Extractor](https://www.printables.com/model/394113-molex-microfit-30-extractor-using-staplers-din-246)

    Lors de la réinsertion des fils dans le connecteur MX, veillez à les insérer exactement dans le même ordre que celui dans lequel ils ont été retirés.

* **Protection à plusieurs niveaux**

    L'alimentation bénéficie d'un système de protection à plusieurs niveaux. Elle est protégée contre l'inversion de polarité en deux étapes : un premier étage basé sur un circuit MOSFET situé sur la carte adaptateur, et un second étage de secours utilisant une diode sur la carte outil. La protection contre les courts-circuits est assurée par un circuit à fusible qui se déclenche à 5 A. **À noter** : la protection par fusible s'applique aussi bien à la ligne positive qu'à la ligne de masse, garantissant ainsi que cette dernière est également protégée en cas d'inversion de tension lorsque le port USB est connecté. Une conception d'une robustesse exceptionnelle.

### **Branchement ventilateurs**

* FAN0, FAN2

    <img src=images/EBB36_GEN2/fan0.jpg width="500"/>

* FAN1

    <img src=images/EBB36_GEN2/fan1.jpg width="500"/>

Il existe trois interfaces pour ventilateurs : FAN0, FAN1 et FAN2 ; FAN0 et FAN1 sont des interfaces à 2 fils, tandis que FAN2 est une interface à 3 fils. La tension de sortie de ces trois interfaces (5 V ou 24 V) est configurée à l'aide de cavaliers.

L'interface FAN2 tire parti du fait que les ventilateurs de tête d'impression fonctionnent généralement avec un rapport cyclique PWM de 100 % pour mettre en œuvre un retour tachymétrique via une interface à 3 fils. Cela permet à votre micrologiciel de détecter si le ventilateur ne tourne pas alors qu'il le devrait, ce qui peut s'avérer critique dans le cas d'un ventilateur de tête d'impression.

> Note: Les connecteurs FAN0 et FAN2 disposent de cavaliers de sélection de tension adjacents, mais l'ordre des broches de sélection y est inversé. Ce choix de routage a été effectué délibérément afin de garantir une piste d'alimentation suffisamment large pour les deux ventilateurs. Veillez à sélectionner la tension appropriée pour votre ventilateur ; dans le cas contraire, vous risquez de le griller, et BIGTREETECH ne saurait être tenu pour responsable d'un tel dommage.

**Protection à Plusieurs Niveaux**<br>
Les sorties pour ventilateurs bénéficient d'une protection à plusieurs niveaux de qualité automobile. Premièrement, elles intègrent une protection contre les courants de retour (flyback) permettant de piloter des charges inductives sans risque de détérioration. Deuxièmement, elles utilisent un MOSFET de qualité automobile doté de protections intégrées contre les courts-circuits, les surtensions, les surchauffes, les surintensités et les décharges électrostatiques (ESD).

### **Interface de la Thermistance**

<img src=images/EBB36_GEN2/thermistor.jpg width="300"/>

L'interface pour thermistance externe est compatible avec les capteurs PT1000 et NTC. Elle intègre une résistance de tirage (pull-up) de 2,2 kΩ ainsi qu'un circuit de protection complet.

**Protection à Plusieurs Niveaux**
La protection du circuit est à plusieurs niveaux. Premièrement, l'entrée « côté haut » (high-side) de la thermistance est protégée contre un court-circuit direct au 24 V grâce à un circuit d'entrée à haute impédance qui dévie l'excès de courant vers le rail 3,3 V. Deuxièmement, le « côté bas » (low-side) est également protégé contre un court-circuit direct au 24 V par un fusible réarmable qui se déclenche en cas de court-circuit. Ces mesures garantissent que même des défaillances au niveau de la tête d'impression — où les fils de la thermistance et de l'élément chauffant cheminent souvent à proximité immédiate les uns des autres — ont peu de chances d'endommager votre carte d'outils (toolboard).

### **Interface RGB**

<img src=images/EBB36_GEN2/rgb.jpg width="300"/>

Une interface RGB à trois broches est prévue. Cette interface est mise en tampon via un convertisseur de niveau, de sorte que le signal de commande de sortie fonctionne avec une excursion complète de 5 V.

**Protection à Plusieurs Niveaux**
Cette interface bénéficie d'une protection à plusieurs niveaux : elle est protégée contre les décharges électrostatiques (ESD) grâce à une impédance élevée placée entre la puce tampon et la sortie, et contre les courts-circuits momentanés grâce à une diode Schottky qui renvoie le courant excédentaire vers le rail 5 V.

### **Interface de Communication**

La carte d'outils prend en charge les communications USB et CANBus. L'interface souhaitée peut être sélectionnée à l'aide d'un simple cavalier, en suivant les règles simples ci-dessous :

* **USB Mode** → Pas de cavalier

* **CAN Mode** → Installer un cavalier

Lorsqu'une interface est sélectionnée, le port d'entrée et le port de transfert (passthrough) s'adaptent tous deux pour prendre en charge cette interface. Cela signifie que vous disposerez, sur la carte d'outils (toolboard), d'un port d'extension CAN ou USB.

Si vous choisissez le CANBus, veuillez noter qu'une résistance de terminaison de 120 Ω est disponible en option sur la carte d'outils ; elle peut être utilisée si cet appareil constitue le dernier élément du réseau physique CANBus. Activez la résistance en insérant le cavalier approprié, comme indiqué sur l'image ci-dessous.

Les deux interfaces de communication nécessitent l'utilisation de la carte adaptatrice. Ne connectez jamais simultanément les interfaces CAN et USB, sous peine d'endommager votre appareil hôte. Pour l'interface USB, il suffit de se connecter au port USB-C ; pour l'interface CAN, utilisez le port JST-XH. Dans les deux cas, une alimentation 24 V est également requise.

**Protection à Plusieurs Niveaux**
Le bus de communication bénéficie d'une protection à plusieurs niveaux. Premièrement, les interfaces USB et CANBus sont toutes deux protégées contre les décharges électrostatiques (ESD). Deuxièmement, ces mêmes interfaces sont protégées contre les courts-circuits directs au 24 V sur leurs broches de communication. Nous déconseillons de provoquer intentionnellement ce type de défaut, car le circuit de protection utilisé pour l'USB n'est pas conçu pour supporter des commutations rapides en court-circuit.

<img src=images/EBB36_GEN2/communication.jpg width="500"/>

Pour la communication USB, la carte nécessite l'utilisation d'une carte adaptatrice.
Comme illustré ci-dessous, la carte adaptatrice se connecte à l'ordinateur hôte via une interface de type C et se relie à la carte EBB36 GEN2 V1.0 à l'aide du câble MX3.0 vers XT30.

> Note:
L'interface Type-C de la carte adaptatrice ne peut pas alimenter l'EBB36 GEN2 V1.0.
Une alimentation 24 V distincte doit être raccordée à la carte.

<img src=images/EBB36_GEN2/interface_adapter.jpg width="1000"/>

Le port de transfert est visible sur l'image ci-dessous.

<img src=images/EBB36_GEN2/passthrough-port.jpg width="500"/>

### **Interface - Probe**

<img src=images/EBB36_GEN2/probe.jpg width="300"/>

L'interface de sonde augmente la densité de fonctionnalités sur la carte d'outils en regroupant, par multiplexage sur un port unique, la prise en charge des types de sondes suivants :

-	BIQU MicroProbe
-	BLTouch
-	Sonde inductive 24V

Vous pouvez configurer la tension de fonctionnement à l'aide d'un cavalier. La sonde peut être réglée pour fonctionner à la tension d'entrée de la carte d'outils ou à 5 V.

> Note: Assurez-vous de sélectionner la tension appropriée avant de connecter votre sonde.

La sortie de la sonde est tirée vers la tension sélectionné par le cavalier.

**Protection à Plusieurs Niveaux**
Le port de sonde bénéficie d'une protection à plusieurs niveaux. Premièrement, la broche de la sonde est protégée contre les décharges électrostatiques (ESD). Deuxièmement, elle est protégée contre les surtensions grâce à un optocoupleur.

> Note: Par conception, la broche de servomoteur ne bénéficie d'aucune protection. Elle a été conservée comme unique broche reliée directement au microcontrôleur afin d'offrir une possibilité d'utilisation aux concepteurs si le besoin s'en faisait sentir. Par conséquent, une attention particulière doit être portée au raccordement de cette broche pour garantir des connexions correctes.

### **Interface de la Hotend**

<img src=images/EBB36_GEN2/heater.jpg width="300"/>

La sortie de l'élément chauffant utilise des borniers à vis avec plaque de serrage à descente. Veuillez ne pas utiliser de fils aux extrémités étamées pour ce raccordement, car cela pourrait entraîner une mauvaise connexion si la soudure venait à fluer avec le temps.
>Note: La tension de l'interface de l'élément chauffant est identique à la tension d'entrée. Si l'entrée est raccordée à une tension supérieure à 24 V, vous devez vérifier si l'élément chauffant supporte une telle tension.

La sortie de l'élément chauffant est dotée d'une protection contre les courants de retour (flyback), tandis que la protection contre les courts-circuits est assurée par les fusibles situés sur la carte adaptatrice.

### **Interface Moteur**

L'interface moteur utilise un pilote de moteur TMC2209 et dispose d'un connecteur JST-XH coudé, avec le brochage des bobines indiqué ci-dessous.

<img src=images/EBB36_GEN2/motor.jpg width="300"/>

L'interface moteur est protégée contre les surtensions de retour (flyback) et les décharges électrostatiques (ESD) au moyen de diodes TVS placées en série sur chaque sortie de bobine.

Une thermistance CTN est placée directement sous le pilote de moteur afin de fournir des mesures thermiques précises de ce dernier. Elle peut être configurée en suivant les indications fournies dans la section relative au micrologiciel.

### **Interface contacts**

<img src=images/EBB36_GEN2/switch.jpg width="300"/>

Deux interfaces de commutateur sont fournies pour répondre à vos besoins spécifiques de mise en œuvre. Elles sont étiquetées « Filament » et « Endstop ».

Les deux entrées sont rappelées au niveau haut (3,3 V) et bénéficient d'une protection à plusieurs niveaux. Elles sont tout d'abord protégées contre les décharges électrostatiques (ESD) et, par ailleurs, contre les courts-circuits momentanés grâce à une diode Zener et une résistance de limitation de courant.

### **Instructions de Mise à Masse du Moteur et des Trous de Montage**

La carte d'outils comporte des connexions au rail de masse via des résistances de 100 kΩ situées au niveau de chaque trou de fixation. Ces résistances sont essentielles pour garantir que toute charge statique accumulée dans le moteur soit dissipée avant de pouvoir provoquer une décharge électrostatique (ESD) susceptible d'entraîner une réinitialisation du microcontrôleur et de perturber l'impression.

Pour tirer pleinement parti de cette fonctionnalité, veillez à utiliser une fixation conductrice entre la carte d'outils et le châssis du moteur. Si vous ne disposez pas d'une telle fixation, envisagez de relier les trous de montage de la carte d'outils au châssis du moteur à l'aide d'un câble équipé de cosses à œillet serties à chaque extrémité.

### **Interface I²C**

<img src=images/EBB36_GEN2/i2c.jpg width="300"/>

L'interface I²C permet de connecter des dispositifs tels que des capteurs environnementaux et des sondes à courants de Foucault. Le port est doté de résistances de tirage (pull-up) intégrées reliées au 3,3 V.

**Protection à Plusieurs Niveaux**
Le port I²C bénéficie d'une protection à plusieurs niveaux. Il est protégé contre les courts-circuits momentanés ainsi que contre les décharges électrostatiques (ESD) grâce à un réseau composé d'une résistance à haute impédance et d'une diode Schottky.

## Klipper

### menuconfig

`[*] Enable extra low-level configuration options`

`    Micro-controller Architecture (STMicroelectronics STM32)  --->`

`    Processor model (STM32G0B1)  --->`


**Si vous n'utilisez pas katapult**

`    Bootloader offset (No bootloader)  --->`

**Si katapult est utilisé**

`    Bootloader offset (8KiBbootloader)  --->`


`    Clock Reference (8 MHz crystal)  --->`


**Pour la communication USB**

`    Communication interface (USB (on PA11/PA12))  --->`

**Pour la communication CAN bus**

`    Communication interface (CAN bus (on PB12/PB13))  --->`


`    USB ids  --->`

`[*] Optimize stepper code for 'step on both edges'`

`()  GPIO pins to set at micro-controller startup`


#### USB

<img src=images/EBB36_GEN2/usb.webp width="800"/>

#### CAN bus

<img src=images/EBB36_GEN2/canbus.webp width="800"/>

## **Notes**

- Lorsqu'elles sont alimentées en 24 V, chacune des trois interfaces de ventilateur peut fournir jusqu'à 1 A individuellement. Lorsqu'elles sont alimentées en 5 V, le courant total combiné des trois interfaces de ventilateur ne doit pas dépasser 1,5 A.

## Sources
- [Site Officiel BIQU](http://biqu3d.com)  
- [Site Officiel BIGTREETECH](http://bigtree-tech.com)  
- [Boutique en Ligne](https://biqu.equipment)  
- [Forum Communauté](https://community.biqu3d.com)  
- [Documentation BIGTREETECH](https://github.com/bigtreetech/docs)  
