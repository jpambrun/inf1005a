## Retour sur le cours 5
 * Résolution de problèmes
   1. La **définition** du problème
   2. L’**analyse** du problème
   3. La **conception** des algorithmes
   4. La mise au point (aka. l'**implémentation**) du programme MATLAB
   5. La **vérification** du programme

## Aide au déboguague (chap. 5 p.11-16)

### Calcul du temps (chap. 5 p.11-16)

#### pause

```pause()``` peut être utile pour stopper momentanément l'exécution dans une boucle.

``` Matlab
for i = 1:10
  % instructions
  pause()         % pause jusqu'à ce que l'usager touche le clavier
  pause(1.5)      % pause 1.5 secondes
end
```

#### clock
``` Matlab
t1 = clock;
pause(1)         % instructions longues
t2 = clock;

temps_ecoule = etime(t2,t1)
```

#### cputime
``` Matlab
disp(cputime);
pause(5);
disp(cputime);

% dans Octave
> 1.6967
> 1.7200
```

#### tic -toc
``` Matlab
tic;
pause(1)         % instructions
toc
pause(1)         % instructions
toc
```


### Messages d'erreurs (chap. 5 p.18-22)



### Déboguage (chap. 5 p.18-22)



## Fonctions
