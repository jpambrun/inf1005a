## Retour sur l'examen

 * Constat:
    - Notre moyenne est la pire avec 8.0
    - Les autres moyennes (3/5) se situent entre 8.5 et 9.5.
    - un groupe a une moyenne de 11.5.
 * On a eu une rencontre à 6 jeudi (5 chargés + la coordonnatrice) et on a dégagé deux consensus:
   1. Cette disparité des notes est statistiquement improbable (je dirais impossible) et inéquitable.
   2. La solution consensuelle était de normaliser les notes à 10 (c.-à-d. ajouter 2 points à tout le monde dans notre groupe) et recorriger toutes les copies du groupe à 11.5.
 * Le groupe de 11.5 a été recorrigé et la moyenne est maintenant de 11.0.
 * Or, lundi, on **la coordonnatrice nous a informés qu'il n'y aurait pas de normalisation**, et ce, sans explication.
 * Cette position me semble absolument injustifiable. Le groupe à 11.5 va manifestement s'accaparer presque la totalité de A et notre groupe sera condamné au B et au C. En plus, les étudiants de notre groupe sont maintenant disproportionnèrent à risque d'échec, surtout avec la règle du 8/20.
 * Qu'est-ce qui peut expliquer cette différence? 
  1. Ce groupe contient les meilleurs étudiants.
  2. Cet enseignant, qui en est à sa première charge, est significativement meilleur que les autres.
  3. Cet enseignant a laissé transparaître un peu trop les questions lors de la préparation à l'examen.
 * On voudrait nous faire croire que l'explication la plus probable est l'option 1, mais avec un n=80 et une différence d'un (1) écart type est nous et eux, c'est extrêmement improbable. Personnellement, l'option 3 me semble la plus probable.
 * Si j'étais vous, j'utiliserais tous les moyens à ma disposition pour faire changer cette décision.



## Représentation des nombres

``` Matlab
>> 1-0.2-0.2-0.2-0.2-0.2
ans =
   5.5511e-17

>> eps(1)
ans =
   2.2204e-16
>> 1+eps(1)/2
ans =
     1


format long e
a=0.123456789012345*10^(-4)
b=0.543210987654321*10^2
c=-0.543210987650001*10^2 
>> (a+b+c) - (a+b+c)
ans =
     0
>> (a+b+c) - (c+b+a)
ans =
     2.834290826125505e-15
>> (a+(b+c)) - ((a+b)+c)
ans =
    -2.834290826125505e-15
>> (a*(b+c)) - ((a*b)+(a*c))
ans =
     6.990847167906112e-20
```


### Complément à deux

| Binaire| Non Signé | Complément à deux |
|---|---|---|
| 0111 1111 |127|127|
| 0111 1110	|126|126|
| 0000 0010	|2|2|
| 0000 0001	|1|1|
| 0000 0000	|0|0|
| 1111 1111	|255|−1|
| 1111 1110	|254|−2|
| 1000 0010	|130|−126|
| 1000 0001	|129|−127|
| 1000 0000	|128|−128|


#### Addition
```
11111 111   (carry)
   0000 1111  (15)
 + 1111 1011  (−5)
 ==================
   0000 1010  (10)
```


```
  0111   (carry)
   0111  (7)
 + 0011  (3)
 =============
   1010  (−6)  invalid!
```


#### Soustraction

```
11110 000   (borrow)
   0000 1111  (15)
 − 1111 1011  (−5)
 ===========
   0001 0100  (20)
```

```
  11100 000   (borrow)
   0000 1111  (15)
 − 0010 0011  (35)
 ===========
   1110 1100  (−20)
```


### IEEE 754


#### Préface - Nombre à point fixe

##### Décimal
|10^3|10^2|10^1|10^0|10^-1|10^-2|10^-3|10^-4|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|4|2|4|5|6|7|2|3|

```(4*10^3) + (2*10^2) + (4*10^1) + (5*10^0) . (6*10^-1) + (7*10^-2) + (2*10^-3) + (3*10^-4) = 4245.6723```


##### Binaire

|2^3|2^2|2^1|2^0|2^-1|2^-2|2^-3|2^-4|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|1|0|1|1|1|0|0|1|

``` (1*2^3) + (0*2^2) + (1*2^1) + (1*2^0) + (1*2^-1) + (0*2^-2) + (0*2^-3) + (1*2^-4) = 11.5625 ```


Peu flexible, on veut un point flottant et signé. La solution : IEEE 754.

``` A = (-1)^s * (1+frac) * 2^e ```


|| signe (s)| exposant (e)| mantisse (frac) |
|---:|:---:|:---:|:---:|
|single (32 bits)|x|xxxxxxxx (8) |xxxxxxxxxxxxxxxxxxxxxxx (23)|
|double (64 bits)|x|xxxxxxxxxxx (11)|xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx (52)|

##### Conversion
Ex: 0.1


```0.1 = (-1)^s * (1+frac) * 2^e```

Comme 0.1 est positif, on déduit que **s=0**.

```0.1/2^e = (1+frac) ```

Je cherche le e qui me donne la forme (1+frac):
```
>> 0.1/2^-1
ans =
    0.2000
>> 0.1/2^-2
ans =
    0.4000
>> 0.1/2^-3
ans =
    0.8000
>> 0.1/2^-4
ans =
    1.6000
```

Donc **e=-4**.

Maintenant, on pourrait déterminer quelle séquence de ```(X*2^-1) + (X*2^-2) + (X*2^-3) + ... + (X*2^-23) = 0.6```, mais il y a un truc.

On multiplie successivement par 2 et on note le chiffre avant le '.', il ne peut être que '0' ou '1'. On recommence avec le chiffre après le '.' jusqu'au nombre de bits requis ou jusqu'à ce que le nombre après le point soit zéro.

|position|après le '.'|avant le '.'| notes |
|:--:|:--:|:--:|:--|
|1|.6|1| ```0.6``` est la valeur de départ. ```0.6*2 = 1.2```, on met le ```1``` de ```1.2``` dans la troisième colonne|
|2|.2|0|le ```.2``` est la suite du ```1.2```. ```.2*2=0.4```. Le 0 de 0.4 est rapporté dans le troisième colonne|
|3|.4|0||
|4|.8|1||
|5|.6|1||
|6|.2|0||
|7|.4|0||
|8|.8|1||
|9|.6|1||
|10|.2|0||
|11|.4|0||
|12|.8|1||
|13|.6|1||
|14|.2|0||
|15|.4|0||
|16|.8|1||
|17|.6|1||
|18|.2|0||
|19|.4|0||
|20|.8|1||
|21|.6|1||
|22|.2|0||
|23|.4|0|C'est le dernier bit de la mantisse (frac)|
|24|.8|1|On doit en calculer un autre pour tenir compte de l'arrondissement|

Pour combiner le tout:


###### Pour s:
s est inséré comme tel sans modification. Ici, s= ```0```


###### Pour e:
e contient un biais de 127 qu'il faut ajouter. Ceci permet les valeurs négatives.
Ici, ```127+(-4) = 123```, en binaire ```0111 1011```.


###### Pour frac:
Il faut ajouter le 24e (en single) bit pour arrondir.
```
1001 1001 1001 1001 1001 100
                         + 1
============================
1001 1001 1001 1001 1001 101
```


|| signe (s)| exposant (e)| mantisse (frac) |
|---:|:---:|:---:|:---:|
|single (32 bits)|0|0111 1011|1001 1001 1001 1001 1001 101 |

Pour valider, voir https://www.h-schmidt.net/FloatConverter/IEEE754.html



### Exercice

Convertir 11.5625 en IEEE 754

```s = 0```

``` 11.5625/2^e = (1+frac) ```

``` 11.5625/2^3 = (1+.445312500000000) ```

Attention à la précision de vos calculs!

```e = 3+127 = 1000 0010```

|position|après le '.'|avant le '.'|
|:--:|:--:|:--:|:--|
|1|.445312500000000|0|
|2|.890625000000000|1|
|3|.781250000000000|1|
|4|.562500000000000|1|
|5|.125000000000000|0|
|6|.250000000000000|0|
|7|.500000000000000|1|
|8|0|0|
|9|0|0|
|10|0|0|
|11|0|0|
|12|0|0|
|13|0|0|
|14|0|0|
|15|0|0|
|16|0|0|
|17|0|0|
|18|0|0|
|19|0|0|
|20|0|0|
|21|0|0|
|22|0|0|
|23|0|0|
|24|0|0|

Pas besoin d'arrondir. ``` frac = 0111 0010 0000 0000 0000 000 ```


Rép : 11.5625 == 0    1000 0010    0111 0010 0000 0000 0000 000
