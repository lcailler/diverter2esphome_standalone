# Controler un **Diverter** avec son navigateur internet préféré
Vous trouverez ici une configuration yaml esphome pour le module **wifi** de votre choix. Elle vous permettra, en plus des fonctions natives du **diverter**, d'ajouter son contrôle à distance directement depuis votre navigateur **web** préféré, pc ou smartphone.

- [Introduction](#Introduction)
- [Fonctionnalités](#Fonctionnalités)
- [Prérequis](#Prérequis)
- [Instructions d'installation](#Instructions-installation)
- [Pour aller plus loin](#Pour-aller-plus-loin)

---

## Introduction
**Autonome** par défaut

Le module wifi en toute **autonomie** met à disposition un "contrôleur" sous la forme d'une page web. cf copie d'écran ci-dessous. Cette solution n'a pas besoin **d'Home Assistant**, un simple navigateur web permet de prendre le contrôle.<br />Par contre, si vous préférez, rien n'interdit utiliser **Home Assistant**. Avec cette approche composant **ESPHome**, l'ajout du composant dans home assistant sera automatique et sans effort.

Pour plus d'informations sur le **diverter**, veuillez suivre ce lien : [http://wikinid.free.fr/wiki/Main/DiverterModule](http://wikinid.free.fr/wiki/Main/DiverterModule)

---

## Fonctionnalités
**Remontée** d'infos, mode **AUTO** par programmation d'une **plage horaire** de marche forcée, mode **MANUEL** pour un contrôle manuel.

Vous pouvez contrôler votre **diverter** depuis l'interface **Web**. Elle permet de rendre visible des grandeurs invisbles, elle affiche les informations de puissances produite, consommée ou injectée. En plus de sa fonction de "diverter", cette solution permet de prendre le **contrôle** de la marche forcée dans deux modes distincts : AUTO ou MANUEL.<br/>
+ Le mode AUTO est un automatisme activable en programmant la plage horaire de votre choix. Sa durée devra être supérieure ou égale à 1 heure de mise en marche forcée.<br/>
+ Le mode MANUEL permet de positionner manuellement à on/off la marche forcée.

L'activation du mode MANUEL sera effectif dés que la plage horaire sera réglée pour durer 0 heure, H0=H1. Le mode AUTO sera ainsi désactivé, et le mode MANUEL prendra le relais.<br/>
Inversement, l'activation du mode AUTO sera effectif dés que la plage horaire sera réglée pour une durée différente de 0 heure, H0<>H1.

## Aperçu de l'interface web produite par le module wifi

<p align="center">
<img src="https://raw.githubusercontent.com/lcailler/diverter2esphome/refs/heads/main/screenshot00.png" width="600">
</p>

---

## Prérequis
**Sonoff** ou tout autre module wifi compatible **ESPHome**

La configuration disponible ici est adaptée à un [Sonoff Basic R2](https://devices.esphome.io/devices/Sonoff-BASIC-R2-v1.4).
Avec quelques adaptations **mineures**, vous pourrez adapter cette configuration a d'autres modules wifi. Vous trouverez la liste exhautive de plus de 200 modules wifi supportés en suivant ce lien : https://devices.esphome.io/standards/global.

<p align="center">
<img src="https://devices.esphome.io/assets/images/Sonoff-BASIC-R2-v1.4_pcb-91413dd2dfff7c370d2c18685c91cac2.jpg" width="500">
</p>

---

## Instructions installation

### installation esphome

Plusieurs façons pour installer esphome sur votre carte esp8266 ou autre. Cela peut être via home assistant mais aussi directement depuis votre pc.

Concrètement, sous home assistant, ajouter le composant "ESPHome Device Builder", puis ouvrir "l'interface utilisateur web". Voici un guide : https://www.hacf.fr/esphome-introduction/

Sur votre pc, vous trouverez un guide complet en suivant ce lien : https://peyanski.com/complete-esphome-installation-guide/

### flash du firmware

Avec ESPHome flasher le firmware basé sur les fichiers yaml suivants : sonoff-esp-diverter.yaml & secrets.yaml

### câblage croisé

Il vous faudra câbler ici les signaux tx, rx, gnd du module wifi sur le diverter. Il vous faudra relier les signaux gnd entre eux, le signal tx sur le rx et inversement. Le tx du module wifi au rx du diverter, le rx du module wifi sur le tx du diverter. On parle dans ce cas de câblage croisé.

Attention a ne pas utiliser le signal 3.3v pour alimenter un module wifi. La quantité de courant sur ce signal ne permet pas d'alimenter un module wifi trop gourmand en courant. Si jamais vous connectez l'alimention d'un module sur le signal 3.3v, vous vous exposez à mettre le diverter dans un état de reset continue, sans fin. Le diverter ne sera alors plus fonctionnel.

Autre détail technique, les signaux tx/rx du diverter sont compatibles signaux ttl 3.3v.

<p align="center">
<img src="http://lionel.wiki.free.fr/download/projets/diverterV1_7_20190705/connect_diverter_03.png" width="400">
</p>

### première mise sous tension :

Pas d'obligation de renseigner vos paramètres Wi-Fi dans la configuration yaml.
Une fois flashée, si votre configuration Wi-Fi n'est pas faite, un hotspot Wi-Fi est activé. Connectez-vous sur ce hotspot et configurez votre Wi-Fi local, ssid et password. Si la led se met à clignoter régulièrement, cela indique que vous avez réussi à configurer correctement les paramètres wifi. Par contre, si la led reste alumée fixe sans clignoter, il vous faudra reprendre la configuration wifi. Attention, si le module wifi reste déconnecté du réseau wifi pendant plus de 2 minutes, le module se réinitialise en effecftuant un reset.


## Pour aller plus loin

Voici quelques raisons pour lesquels vous pourriez faire évoluer le yaml partagé ici :
+ si vous voulez ajouter un automatisme, esphome rend trés accessible ce type de chose.
+ supporter d'autres cartes compatibles ESPHome.
+ prendre le contrôle du relais présent sur le module wifi sonfoff basic.
+ automatiser la mise à on/off du relais sur des seuils de production solaire, ou sur des plages horaires etc ....
+ ....

https://esphome.io
