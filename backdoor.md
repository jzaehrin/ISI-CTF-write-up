# Web - B4ckd00r

À l'aide de la description du challenge, il est evident qu'une backdoor est présente, et qu'elle est probablement présente dans la page web, mais cachée.

En conséquence, on regarde la source de la page web, pour voir si il y à quelque chose de particulier.

On remarque deux choses : 

1. un champ `secret_backdoor` caché dans la form.
2. une étrange chaine de code morse en bas de la page :

```
<!-- --- -.. ..-. ..- -... ... .-- .-. ..-. .... ...- .-- .-- ..- .-. ... ..- .-.. .--- .-. --- .-. -->
```

En passant cette chaine (sans les `<!--` et `-->`) sur un [traducteur de code morse](https://mattfedder.com/blog/ham/MorseTranslater), on obtiens ce texte :

```
ODFUBSWRFHVWWURSULJROR
```

On pourrais croire que cette chaine est la backdoor, mais en l'envoyant dans le champ `secret_backdoor` (avec tamperdata pour modifier la valeur du champ, ou en changeant le type du champ pour du text), rien ne se passe.

En regardant cette chaine de plus près, nous voyons qu'elle ne parait pas être complètement aléatoire, en effet il y à beaucoup de répétitions de lettres.
Donc en essayant de la passer sur un [système de décryptage de chiffrement césar](https://www.dcode.fr/caesar-cipher), avec un shift de 3, nous trouvons la chaine :

```
LACRYPTOCESTTROPRIGOLO
```

En la mettant en temps que `secret_backdoor`, (après avoir changé sa casse), la source de la page change et nous trouvons ce commentaire dans celle-ci : 

```
<--  username = admin, password = c3eUxw94aoMd !>
```

En se connectant avec ces données, le flag nous est donné.