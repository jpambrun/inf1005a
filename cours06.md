## Extra

Deep learning:
https://docs.google.com/presentation/d/1izN3aH9FoprZho0MEDAnjDPB0FaGyjI2KYv1-wM79Dc/edit?usp=sharing

## Retour sur le cours 5
 * Résolution de problèmes
   1. La **définition** du problème
   2. L’**analyse** du problème
   3. La **conception** des algorithmes
   4. La mise au point (aka. l'**implémentation**) du programme MATLAB
   5. La **vérification** du programme

## Aide au débogage (chap. 5 p.11-16)

### Calcul du temps (chap. 5 p.11-16)

#### pause

```pause()``` peut être utile pour stopper momentanément l'exécution dans une boucle.

``` Matlab
for i = 1:10
  % instructions
  pause()         % pause jusqu'à ce que l'usager touche le clavier
  pause(1.5)      % pause 1.5 seconde
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

% dans Matlab
> 126.0200
> 135.8700

% wat ?!
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

Par exemple, pour l'exercice coder ```eye()``` du cours 4

``` Matlab
D= [5,4];
e = [];
for i = 1:D(1)
   for j = 1:D(2)
      e(i,j) = i == j;
   end
end
disp(e)
```

On pourrait ajouter le test:

``` Matlab
if numel(D) ~= 2
    error('D dois avoir 2 éléments, pas %i.', numel(D))
end

if ~isnumeric(D)
    error('D dois contenir des valeurs numériques.')
end

if ~isreal(D)
    error('D ne dois pas avoir de composante imaginaire.')
end


if max(D) > 1000
    warning('Une taille supérieure à 1000, comme %i, est inefficace.',length(D))
end
```

lasterr & lastwarn:

```
>> lasterr

ans =

D dois contenir des valeurs numériques.

>> lastwarn

ans =

Une taille supérieure à 1000, comme 2, est inefficace.
```

### Déboguage (chap. 5 p.18-22)

Utilisons le débogueur pour comprendre ce qu'il se passe:

``` Matlab
I = imread('cameraman.tif'); % .tif dans matlab
I = imresize(I, .5);

A = zeros(size(I,1)*2, size(I,2)*4);
for i= 1:2
    for j = 1:4
        x1 = 1 + (i-1)*size(I,1);
        y1 = 1 + (j-1)*size(I,2);
        x2 = i*size(I,1);
        y2 = j*size(I,1);

        sel = false(size(A));
        sel(x1:x2,y1:y2) = true;
        A(sel) = imrotate(I,randsample(0:45:360,1),'crop'); % F9
    end
end
imshow(A,[])

```

à retenir
 * retirer les ; pour voir les résultats intermédiaires.
 * ajouter un breakpoint pour stopper le code
 * ajouter un breakpoint conditionnel pour stopper le code seulement lorsqu'une condition est vraie
 * une fois arrêté, on peut explorer les variables et même les modifier
 * F9 peut être utile pour voir l'effet de partie de ligne. Autrement , le débogueur procède ligne par ligne.
 * Step in entre dans une fonction
 * Step out sort d'une fonction

## Fonctions

Exemple :

``` Matlab
function [ e ] = moneye( D )
%MONEYE Identity matrix.
%   eye(N) is the N-by-N identity matrix.
%   eye(M,N) or eye([M,N]) is an M-by-N matrix with 1's on
%   the diagonal and zeros elsewhere.
    e = [];
    for i = 1:D(1)
       for j = 1:D(2)
          e(i,j) = i == j;
       end
    end
end
```


``` Matlab
function [ bissextile ] = isBissextile( an )
%ISBISSEX Retourne is l'année est bissextile
%   isBissextile( an ) retourne vrai si an est bissextile.

    bissextile = true;

    if mod(an,4) ~= 0
      bissextile = false;
    else
      if mod(an,100) == 0 && mod(an,400) ~= 0
        bissextile = false;
      end
    end
end
```

```
>> lookfor biss
isBissextile                   - ISBISSEX Retourne si l'année est bissextile.
>>

>> help isBissextile
 ISBISSEX Retourne si l'année est bissextile
    isBissextile( an ) retourne vrai si an est bissextile.
```

Un appel de fonction avec moins de paramètres est possible, mais cette option doit être prise en charge:

``` Matlab
function [ e ] = moneye( D )
%MONEYE Identity matrix.
%   eye(N) is the N-by-N identity matrix.
%   eye(M,N) or eye([M,N]) is an M-by-N matrix with 1's on
%   the diagonal and zeros elsewhere.

    if ~exist('D', 'var')
        D = [5,5];
    end

    e = [];
    for i = 1:D(1)
       for j = 1:D(2)
          e(i,j) = i == j;
       end
    end
end
```

Autrement:

```
Not enough input arguments.

Error in moneye (line 7)
    for i = 1:D(1)
```

Par contre, ce n'est pas possible d'omettre un paramètre au milieu (p. ex. ```fonc( ,12)``` de cette façon.
