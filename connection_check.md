# Misc - Connection Check

Le challenge est simplement là pour s'assurer que le système de CTF fonctionne pour toutes les équipes.

En ouvrant le fichier fourni, on est accueilli par cette chaine : 

```
TGUgZmxhZyBlc3QgSVNJMTh7QmFzZTY0TmVzdFBhc0RlTGFDcnlwdG99
```

En connaissant le format, ainsi que le fait que il y à des caractères alphanumériques de casse mixte, on peut se douter qu'il s'agit d'un encodage base 64.

En passant la chaine sur un [décodeur base 64](https://base64decode.org), nous obtenons :

```
Le flag est ISI18{Base64NestPasDeLaCrypto}
```
