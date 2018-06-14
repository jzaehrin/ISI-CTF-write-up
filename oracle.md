# Crypto - Oracle

## Contexte
Ce challenge est composé :
+ D'un fichier texte contenant le texte chiffré `e:grrlqtoocaympckcbqapqxclemipaihipzgxtuyzoahabtcokz sskujhkewo`
+ D'un flux de chiffrement (accessible via `netcat` sur le port 9000 du serveur 10.10.40.200)

## Analyse
### Texte chiffré fourni
1. Le texte chiffré fourni débute par un caractère alphabetique suivi de **:** , ainsi que d'une suite de caractères alphabétiques et d'espaces.
On peut penser que le premier caractère et les deux points qui suivent sont des paramètres, et n'appartiennent donc pas au texte clair.

2. D'après l'hypothèse du premier point, l'alphabet probablement être [a-z,' '].

### Flux de chiffrement
1. Lorsque l'on envoie le même caractère au flux de chiffrement à plusieurs reprises, on peut constater que le *ciphertext* reçu en retour varie :
```
Plaintext: a
Ciphertext: m:j

Plaintext: y
Ciphertext: e:z

Plaintext: a
Ciphertext: r:o

Plaintext: a
Ciphertext: g:d
```
La lettre chiffré semble donc dépendre de la lettre précédant **:**.
2. Lorsque l'on envoie la lettre **b**, on obtient systématiquement la même lettre à double :
```
Plaintext: d
Ciphertext: q:q

Plaintext: d
Ciphertext: g:g

Plaintext: d
Ciphertext: v:v

Plaintext: d
Ciphertext: e:e
```
Une clé incunnu doit également intervenir dans le chiffrement, et il semble que son premier caractère aie un lien avec la lettre **d**.


