# Crypto - Oracle

## Contexte
Ce challenge est composé :
+ D'un flux de chiffrement (accessible via `netcat` sur le port 9000 du serveur 10.10.40.200)
+ D'un fichier texte contenant le texte chiffré `e:grrlqtoocaympckcbqapqxclemipaihipzgxtuyzoahabtcokz sskujhkewo`

## Analyse
### Flux de chiffrement
1. Lorsque l'on envoie le même caractère au flux de chiffrement à plusieurs reprises, on peut constater que le *ciphertext* reçu en retour varie.
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

