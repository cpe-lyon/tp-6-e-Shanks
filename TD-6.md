# **Exercice 1. Adressage IP (rappels)**

Avec du VSLM:
On commence par le sous-réseau ayant le plus grand nombre de machines, soit le sous-réseau 3.
Pour 52 machines(+@réseau+@broadcast), on doit a besoin de 6 bits (car 2^6=64).
Ce qui donne 32-6=26 => /26.
Donc 172.16.0.0/26 comme adresse de sous-réseau pour le sous-réseau 7, avec une plage restante 172.16.0.64/26.
Ainsi de suite.
A l'exception du sous-réseau 7, pour lequel on a besoin de seulement 5 bits (car 2^5=32).

| sous-réseau  | @sous-réseau          | @broadcast | 1ère adresse | Dernière adresse |
| :--------------- |:---------------| :--------------- |:---------------|:--------------- |
| sous-réseau 3  | 172.16.0.0/26    |  172.16.0.63/26 |  172.16.0.1/26 | 172.16.0.62/26 |
| sous-réseau 1  | 172.16.0.64/26   |  172.16.0.127/26 |  172.16.0.65/26 | 172.16.0.126/26 |
| sous-réseau 6  | 172.16.0.128/26  |   172.16.0.191/26 |  172.16.0.129/26 | 172.16.0.190/26 |
| sous-réseau 4  | 172.16.0.192/26  |    172.16.0.255/26 |  172.16.0.193/26 | 172.16.0.254/26 |
| sous-réseau 5  | 172.16.1.0/26    |  172.16.1.63/26 |  172.16.1.1/26 | 172.16.1.62/26 |
| sous-réseau 2  | 172.16.1.64/26   |   172.16.1.127/26 |  172.16.1.65/26 | 172.16.1.126/26 |
| sous-réseau 7  | 172.16.1.128/27  |    172.16.1.159/27 |  172.16.1.129/27 | 172.16.1.158/27 |

# **Exercice 2. Préparation de l’environnement**

1 - Sur vsphere, on modifie les paramètres de la VM, on lui ajoute un nouvel adaptateur réseau: ICS_E14_2014. Sur la deuxième VM, on lui ajoute ce même adaptateur réseau. De ce fait, le serveur a accès à Internet et le client à accès à Internet via le serveur.

2 - Avec la commande **ip adrr** on peut vérifier que les interfaces réseaux sont bien présentes. L'interface lo permet de contacter la machine locale sans passer par une interface qui serait accessible de l'extérieur. En d'autres termes, elle permet à la machine de se connecter à elle même sans passer par le réseau. Elle représente la machine elle-même. On peut parler d'adresse de bouclage.

3 - Pour désinstaller le paquet cloud-init, on va utiliser la commande **sudo apt-get purge cloud-init**.

4 - **sudo hostnamectl set-hostname tpadmin.local** va permettre de renommer le serveur. Ensuite, **sudo nano /etc/hosts** pour remplacer l'occurence de l'ancien nom par le nouveau. Enfin, on reboot avec **sudo reboot** pour prendre en compte le changement.

# **Exercice 3. Installation du serveur DHCP**

1 - **isc-dhcp-server** puis **systemctl status isc-dhcp-server**. Cela va afficher Active: Failed ce qui veut dire que le serveur n'a pas réussi à démarrer, ce qui est normal (enfin je crois).

2 - Afin d'attribuer de manière permanente l'adresse IP 192.168.100.1 à l'interface réseau du réseau interne, il faut taper la commande **sudo nano /etc/netplan/50-cloud-init.yaml** et modifier le fichier de la sorte:
![img](img/TP-6_exo3.png)
Ensuite, on peut exécuter la commande **sudo netplan apply** pour prendre en compte ces changements.
![img](img/TP-6_exo3_2.png)
