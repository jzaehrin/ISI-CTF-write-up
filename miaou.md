# Forensic - Miaou
En ouvrant le fichier fourni `"Shadow"`, nous pouvons voir divers hash de mots de passe systeme unix.

Le titre du challenge nous donne un indice quant à l'utilisation de `hashcat` pour casser ce mot de passe.

En regardant la ligne du fichier contenant le compte `admin`.

```
admin:$6$fwmjZupP$F5XO0St/E707vstLAxYUnzH2GdEhRBRYjT6rIqQvCGDizX3Z12tq0DeParRUYsSJPbFERuSgGk0e/
5GkMTJUm1:17689:0:99999:7:::
```

Nous pouvons voir après le premier `:` un `$6`, nous indiquant qu'il s'agit d'un hash UNIX sha512 salé.

Nous connaissons désormais l'algorithme à brute-forcer, maintenant il faut déterminer quoi brute-forcer.

Nous pouvons deviner que le mot de passe contient probablement la balise de flag `ISI18{...}`.

Avec cette connaissance, ainsi que le fait que ce challenge doit être faisable en une dizaine de minutes, nous pouvons deviner 4 types possibles de mots de passe : 

1. un mot de passe jusqu'à 2 caractères ASCII aléatoires
2. un mot de passe jusqu'à 3 caractères alphanumériques de casse quelconque
3. un mot de passe jusqu'à 4 caractères alphabétiques de même casse
4. un mot de passe jusqu'à 6 caractères numériques

En essayant ces 8 possibilités (avec ou sans balise), il est possible de trouver le flag en une dixaine de minutes sur une carte graphique décente, ou en une quarantaine de minutes du un CPU récent. 

La commande hashcat permettant de trouver le flag est :

```
hashcat -m 1800 -a 3 ./shadow -o ./solution.txt ISI18{?d?d?d?d?d}
```

( le `-m 1800` est l'algorithme des hash UNIX sha256 salés, et le `-a 3` est le mode d'attaque par force brute)