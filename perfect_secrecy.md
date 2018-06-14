# Crypto - Perfect Secrecy

## Le but de ce challenge
Ce challenge à pour but de déchiffrer 2 cipher-texts.

cipher-text 1 : 

```
VSMMZ ZNNAV ZTMZS FVMDGC EXEVG FSOWZ MLMFO VRGIE CEIDT BALRH HVWVI GDSOG BADQG RRXYM ATORX TIBVG KHARB GUEFL LJKVM JBRTZ QBPWL PKYZX GKSHO VRTRJ CLGDI VEVFQ KAIQP RFDRW GCZID RVEFM NLOPY ASSAY SEPFZ AQHNT FTTOX DWPUU I
```

cipher-text 2 : 

```
ESGTW YHJXV FAUTS RWKCS FIYTN NUAGT XAQSW WARRC QFQHE GSHGL BVWKV PSTDN TWKQJ BUANN MPLIN GMBDR GWDCC MJRNS KJAXG IQGRO DRPUN TIHAE VMZBN JEBRW LYSHD RRKQZ GKMHC HLVCF FMRVY SWSYD RDMTC JHMMD SZXUU JFIJI YMBIN ZWLYV QGFLM KTSKE NXJWP NAALD FNTQV RYLWP TOMPA KFUES YRHSC XDGQE DJWZR RPNOY MTAEH XXYME JYJOM AULLS ISZIO UXMMA UOGUL MMPOZ QAHRF NTKFE FLBOZ OESKG FOAGQ NWJUO ATM
```

## Les informations à notre disposition

Le challenge est nommé `Perfect Secrecy`, donc nous pouvons assez facilement deviner qu'il s'agit de chiffrement de Vernam.

Nous pouvons confirmer cela avec un certain degré de confiance en passant un test d'[Indice de coïncidence](https://fr.wikipedia.org/wiki/Indice_de_co%C3%AFncidence), pour confirmer un contenu aléatoire sans grand biais, et donc n'utilisant pas un chiffrement de Vigenère avec clé raisonnable.

Un indice est présent dans la donnée :

```
HINT: Selon des rumeurs, il se pourrait que l'un des textes clairs contienne le nom de l'algorithme utilisé.
```

En visitant la page wikipedia de ["chiffre de Vernam"](https://fr.wikipedia.org/wiki/Masque_jetable), nous apprenons que celui-ci est également appelé "masque jetable"

Donc nous savons que probablement, le mot `vernam` ou le mot `masquejetable` se trouve dans l'un des textes

## Démarche de résolution
Il s'agit maintenant de trouver un moyen de tester la présence d'un des mots précités à chaque position des deux cipher-texts fournis.
Il existe de nombreux outils online offrant ce genre de services, mais ["ce site"](http://webpages.charter.net/nikkeenan/vigenere.html) à l'avantage de proposer la recherche simultané de plusieurs mots, la recherche par fragment de la clé, ou encore le déchiffrement final (à l'aide de la clé complète).

Après analyse méticuleuse des résultats, on s'apperçoit que le mot `masquejetable` en position 2 du deuxième cipher-text correspond à `uteinformatio`, qui pourrait être étendu à `toute information`. 
En plaçant cette fois-ci `touteinformation` en tant que fragment de clé, on peut lire `lemasquejetablee` en position 0.

Il peut être intéressant à présent de tester ce fragment de clé sur le cipher-text 1, au cas où la même clé aurrait été utilisée deux fois. 
Cela semble être le cas, car on trouve le fragment `cestvraimenttres`, que l'on comprend aisément.

Afin de poursuivre le décryptage de ces deux codes, il faut donc compléter tour à tour ces trois chaînes de caractère, et les entrer régulièrement dans l'outil précédemment cité afin de compléter les autres chaînes.
