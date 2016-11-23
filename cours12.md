## Opération binaire en complément à deux

15 + -5

```
  11111 111   (carry)
   0000 1111  (15)
 + 1111 1011  (−5)
 ==================
   0000 1010  (10)
```

7+3 sur 4

```
  0111   (carry)
   0111  (7)
 + 0011  (3)
 =============
   1010  (−6)  invalid!
```


#### Soustraction binaire

15 - -5

```
  11110 000   (borrow)
   0000 1111  (15)
 − 1111 1011  (−5)
 ===========
   0001 0100  (20)
```

15 - 35

```
  11100 000   (borrow)
   0000 1111  (15)
 − 0010 0011  (35)
 ===========
   1110 1100  (−20)
```

## Final AUT 2015

q1.2 : -65.5
q1.3c : en binaire, les chances de pas avoir de retenue sont limitées..
q1.4a : cpu time compte le temps d'usage cpu. Celui-ci peut même être plus élevé que 1 pour une seconde de "wall time" si plusieurs cœurs sont utilisé en même temps. Il peut être de zéro si le cpu n'est pas utilisé.
q1.4b non, toc retourne déjà le temp entre le tic et le toc.
q1.4d : Error using toc You must call TIC without an output argument before calling TOC without an input argument.
q.15c : plot(x1, [y1;y2])
