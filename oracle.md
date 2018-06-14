# Crypto - Oracle

## Contexte
Ce challenge est composé :
+ D'un fichier texte contenant le texte chiffré `e:grrlqtoocaympckcbqapqxclemipaihipzgxtuyzoahabtcokz sskujhkewo`
+ D'un flux de chiffrement (accessible via `netcat` sur le port 9000 du serveur 10.10.40.200)

## Analyse
### Texte chiffré fourni
1. Le texte chiffré fourni débute par un caractère alphabetique suivi de **:** , ainsi que d'une suite de caractères alphabétiques et d'espaces.
On peut penser que le premier caractère et les deux points qui suivent sont des paramètres, et n'appartiennent donc pas au texte clair.

2. D'après l'hypothèse du premier point, l'alphabet est probablement [a-z,' '].

### Flux de chiffrement
1. Lorsque l'on envoie le même caractère au flux de chiffrement à plusieurs reprises, on peut constater que le *ciphertext* reçu en retour varie :
```
Plaintext: a
Ciphertext: m:j

Plaintext: y
Ciphertext: e:z
```
La lettre chiffré semble donc dépendre de la lettre précédant **:**.

2. Lorsque l'on envoie la lettre **b**, on obtient systématiquement la même lettre à double :
```
Plaintext: d
Ciphertext: q:q

Plaintext: d
Ciphertext: g:g
```
Une clé incunnu doit également intervenir dans le chiffrement, et il semble que son premier caractère aie un lien avec la lettre **d**.

3. Lorsque l'on envoie les mêmes deux lettres plusieurs fois, la deuxième lettre chiffrée est toujours la même :
```
Plaintext: aa
Ciphertext: d:ai

Plaintext: aa
Ciphertext: h:ei
```
On est sûr à présent que le chiffrement de chaque lettre dépend de la lettre précédente (la lettre avant '**:**' pour la première), et de la clé.
### Démarche de résolution
#### Trouver la clé
Afin de trouver *la clé*, il peut être intéressant de trouver tout d'abord la lettre qui, une fois chiffrée, vaut la lettre précédente à chaque étape.



