# Web - Matrix

Pour ce challenge, il est nécessaire de bien prendre en compte la description qui nous parles de cookie.

Dès lors, il est bien d'aller voir les cookies du site web, nous trouvons plusieurs champs.

* PHPSESSID
* session
* access

Deux d'entre eux sont utilisé pour la gestion de la Session, il n'est pas intéressant pour ce challenge.
Mais le champ `access` peut être intéressant, il semble être généré de manière aléatoire, si le cookie n'est pas présent.
Le titre `Matrix` nous donne un indice, il serait judicieux de vouloir tester l'accès `0`.

