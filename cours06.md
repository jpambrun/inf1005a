## Retour sur le cours 5
 * Résolution de problèmes
   1. La **définition** du problème
   2. L’**analyse** du problème
   3. La **conception** des algorithmes
   4. La mise au point (aka. l'**implémentation**) du programme MATLAB
   5. La **vérification** du programme

## Déboguage: calcul du temps

#### pause
``` Matlab
pause()
pause(1.5)
```

#### clock
``` Matlab
t1 = clock;
pause(1) % instructions
t2 = clock;

temps_ecoule = etime(t2,t1)
```

#### cputime
``` Matlab
t1 = cputime;
pause(1) % instructions
t2 = cputime;

t2-t1
```

#### tic -toc
``` Matlab
tic;
pause(1) % instructions
toc
```
