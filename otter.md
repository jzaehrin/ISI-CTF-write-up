# Web - Otter

Dans ce challenge, nous sommes confrontés à une page web de mauvais goût en PHP.

Nous pouvons voir qu'il y à un champ rôle dans les paramètres de l'`URL`.
Une idée vient de vouloir monter en privilège en changeant de rôle pour `admin`.
Malheureusement, l'envoi d'"admin" dans le rôle ne change rien, il est possible que le php test si le paramètre vaut admin pour éviter cette faille.

Par exemple
```php
    if($_GET["role"] == "admin") 
```

Dans ce cas, si l'on envoie des caractères spéciaux, les caractères seront mal interprétés par PHP.
Il est possible d'envoyer des caractères spécifiques aux URL qui sont préfixées par `%`.

Vous pouvez les trouver [__ici__](https://www.w3schools.com/Tags/ref_urlencode.asp)

On est maintenant capable d'écrire "admin" avec ces symboles.

Voilà, nous nous trouvons sur une magnifique page remplie de Licornes !
