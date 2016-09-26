Note:
 * Les boucles ne devait pas faire partie des permiers exercices du TD 2.
 * On a déjà vu les 15 primières heures en 12.

## Retour sur le cours 4
 * Todo

## Déboguage: calcul du temps


``` Matlab
t1 = clock
%something slow
t2 = clock

temps_ecoule = etime(t2,t1)
```

``` Matlab
temps = cputime
```

``` Matlab
tic;
% instructions      
toc
```

tic toc == wall time ou cpu time?

``` Matlab
pause()
pause(1.5)
```

## Exercices
