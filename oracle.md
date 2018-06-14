# Crypto - Oracle

## Contexte
Ce challenge est composé :
+ D'un fichier texte contenant le texte chiffré `k:mrrlqtoocaympckcbqapqxclemipaihipzgxtuyzoahabtcokz sskujhkewo`
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

Ciphertext: s:p
Ciphertext: x:u
```
La lettre chiffré semble donc dépendre de la lettre précédant **:**.

2. Lorsque l'on envoie la lettre **d**, on obtient systématiquement la même lettre à double :
```
Plaintext: d

Ciphertext: q:q
Ciphertext: g:g
```
Une clé incunnu doit également intervenir dans le chiffrement, et il semble que son premier caractère aie un lien avec la lettre **d**.

3. Lorsque l'on envoie les mêmes deux lettres plusieurs fois, la deuxième lettre chiffrée est toujours la même :
```
Plaintext: aa

Ciphertext: d:ai
Ciphertext: h:ei
```
On est sûr à présent que le chiffrement de chaque lettre dépend de la lettre précédente (la lettre avant '**:**' pour la première), et de la clé.
### Démarche de résolution
#### Comprendre le chiffrement
Essayons de comprendre le fonctionnement du chiffrement à l'aide des échanges suivants :
```
Plaintext: a     (0)

Ciphertext: c:   ( 2:26)
Ciphertext: s:p  (18:15)
Ciphertext: x:u  (23:20)
```
Les indications entre parenthèses correspondent à l'index des lettres dans l'alphabet [a-b, ' '].

Sachant que la lettre **d** (3) intervient dans le chiffrement, on peut émettre l'hypothèse que le calcule effectuer est :
```
(lettre chiffrée) = (lettre claire) + (lettre précédente) - (clé[0]) mod(taille alphabet)
```
Vérification :
```
26 = 0 +  2 - 3 mod(27) = -1 mod(27) ✓
15 = 0 + 18 - 3 mod(27) = 15 mod(27) ✓
20 = 0 + 23 - 3 mod(27) = 20 mod(27) ✓
```

#### Trouver la clé
Afin de trouver *la clé*, il suffit donc trouver tout d'abord la lettre qui, une fois chiffrée, vaut la lettre précédente à chaque étape.

#### Décrypter le texte chiffré fourni
Avec la clé, on peut décrypter un caractère en inversant l'opération de l'hypothèse précédente (généralisée) :
```
(lettre chiffrée) = (lettre claire) + (lettre précédente) - (clé[position]) mod(taille alphabet)
(lettre claire) = (lettre chiffrée) - (lettre précédente) + (clé[position]) mod(taille alphabet)
```



