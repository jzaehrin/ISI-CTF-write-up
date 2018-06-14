# Crypto - Oracle

## Contexte
Ce challenge est composé :
+ D'un flux de chiffrement (accessible via `netcat` sur le port 9000 du serveur 10.10.40.200)
+ D'un fichier texte contenant le texte chiffré `e:grrlqtoocaympckcbqapqxclemipaihipzgxtuyzoahabtcokz sskujhkewo`

## Analyse
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
... La lettre chiffré semble donc dépendre de la lettre précédant **:**.
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
... Une clé incunnu doit également intervenir dans le chiffrement, et il semble probable que son premier caractère aie un lien avec la lettre **d**.

