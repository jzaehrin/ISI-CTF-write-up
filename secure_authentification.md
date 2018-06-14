# Web - Secure Authentification

Nous sommes confronté à une page de login d'un site.

Dans les sources de la page se trouve un fichier javascript.
On y voit des fonctions que test l'authentification, elles sont malheureusement obfusqués.

Nous pouvons voir que la fonction d'authentification test la condition suivante :

```javascript
    if(n==bb(p) && m==o)
```

Dans cette fonction, `n` est notre identifiant et `p` est une valeur static.
Si nous executons `bb(p)`, p étant la valeur static, dans la console, le résultat est "admin".

Le second test prend `m` étant le mot de passe entrée et `o` une fonction calculé avant l'appel.
Cette fonction `ba` prends 4 paramètre mais seulement les deux premiers sont utilisés.
Ces deux parametres proviennet du formulaire qui sont caché à l'utilisateur qui sont '10' et '1'.
Il suffit d'appeler `ba(x,y,'','')`, x et y étant les parametres cachés dans le formulaire, dans la console pour trouver le mot de passe.
