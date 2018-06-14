# PWN - Debordement
## Contexte
Il suffit d'exploiter le code c fournit afin d'ouvrir un *shell* sur le serveur cible, ce qui doit ensuite permettre de récupérer le flag.
## Analyse
Voici le code c fournit :
```c
int main(int argc, char **argv) {
    int value_to_overwrite = 0x12345678;
    char buffer[B_SIZE];
    setvbuf(stdout, NULL, _IONBF, 0);

    printf("Valeur de l'adresse: 0x%x\n", value_to_overwrite);
    printf("Input : ");
    scanf("%s", buffer);

    printf("Valeur de l'adresse: 0x%x\n", value_to_overwrite);
    if (value_to_overwrite == 0xdeadbeef){
        printf("Bravo! Trouve le flag maintenant!\n");
        system("/bin/bash");
    }else if(value_to_overwrite != 0x12345678){
        printf("Presque... Essaie encore!\n");
    }

    return 0;
}
```
On doit donc évidemment effectuer une attaque par débordement sur `buffer` afin de modifier la valeure stockée dans `value_to_overwrite`.

## Démarche de résolution
Pour résoudre ce challenge, il faut :
1. Trouver la taille de `buffer`.
    
   Conseil : entrer un certain nombre de 'a', suivi de trois 'b', puis augmenter le nombre de 'a' jusqu'à voir 0x626262 exactement dans `value_to_overwrite`.
2. Écrire convenablement `0xdeadbeef` afin de l'insérer (par débordement) dans `value_to_overwrite`.
   
   Conseil : les valeurs seront insérer à l'envers dans la stack, soit en *little-endian*.
3. Parvenir à transmettre *l'exploit* ainsi construit afin de pouvoir envoyer des commandes au *shell*.
   
   Conseil : pour éviter le copier-coller qui pourrait poser problème avec certains caractère spéciaux correspondant aux valeurs de `0xdeadbeef`, il est impératif de `pipe` directement *l'exploit* à la commande netcat.
   Mais cela empêche ensuite la communication avec le *shell*. 
   Essayez donc de grouper la commande `echo` avec une commande sans incidence (tel que `cat`, sans paramètre).

