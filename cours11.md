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
|single (32 bits)|x|xxxxxxxxxxx (11)|xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx (52)|
