# **Exercice 1. Adressage IP (rappels)**

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
