## Opérateurs relationnels (chap.4 3-5)

 * >
 * <
 * >=
 * <=
 * ==
 * ~=

Exemples:
``` Matlab
A = 1:5              % 1   2   3   4   5
A < 3                % 1   1   0   0   0
A > 3                % 0   0   0   1   1
A <= 3               % 1   1   1   0   0
A >= 3               % 0   0   1   1   1
A == 3               % 0   0   1   0   0
A ~= 3               % 1   1   0   1   1

A = 'abracadabra'
A == 'a'             % 1   0   0   1   0   1   0   1   0   0   1
A > 'b'              % 0   0   1   0   1   0   1   0   0   1   0
A > 98               % 0   0   1   0   1   0   1   0   0   1   0
A == 'ab'            % erreur de dimenssion
strfind(A, 'ab')     % 1   8

A = 1:5              % 1   2   3   4   5
B =  5:-1:1          % 5   4   3   2   1
A<B                  % 1   1   0   0   0
A>B                  % 0   0   0   1   1
A == B               % 0   0   1   0   0
A == A               % 1   1   1   1   1
isequal(A,A)         % 1
```

## all() et any() (chap.4 7-9)

``` Matlab
all([1 2 3 4]) % 1
all([1 2 3 0]) % 0

any([0 0 0 4]) % 1
any([0 0 0 0]) % 0
```

Exercice: comment coder isequal() avec any() ?

Solution:

``` Matlab
A=[1 2 3 4]
B=[1 2 3 3]
~any(A-B)         % 0
~any(A-A)         % 1

% alternative avec sum
~sum(abs(A-B))    % 0
```


Pour un vecteur any() considère tous les éléments alors que pour une matrice c'est colonne par colonne.

``` Matlab
A = [1 0 1 1 0;1 1 1 1 0; 1 1 1 1 0]
any(A)            %   1   1   1   1   0
all(A)            %   1   0   1   1   0
```

C'est vrai pour plusieurs autres fonctions sont sum().

``` Matlab
A = [1 0 1 1 0;1 1 1 1 0; 1 1 1 1 0]
sum(A)           %    3   2   3   3   0
sum(sum(A))      % 11 ()
sum(A(:))        % 11
```

## Indexation conditionnel (ou logique) (chap.4 10-11)
``` Matlab
A = 1:5                % 1   2   3   4   5
sel = A > 3            % 0   0   0   1   1
A(sel)                 % 4   5
A(A>3)                 % 4   5

A(A>3) = A(A>3)+10     % 1    2    3   14   15

A = A(A>10) .* 2       % 28   30
```

## Expression booléenne (ou logique) (chap.4 12-17)
 * &
 * |
 * ~
 * xor

Note impostante:
 * FAUX si =  0
 * VRAI si ~= 0 (p.ex. 3.1416 ou -12)

``` Matlab
~12     % 0 (type logical)
~0      % 1 (type logical)

2 | 0   % 1 (type logical)
2 & -2  % 1 (type logical)
```


## Structures de programmation & décision (chap.4 18-37)

### pseudo-code
Exercice: trouver la plus grande valeur d'un vecteur
Solution:
```
lePlusGros = -inf
POUR x FAIRE
  SI x > lePlusGros ALORS
    lePlusGros = x
```

Exercice: Déterminer si l'année est bissextile
 1. si l'année est divisible par 4 et non divisible par 100, ou
 2. si l'année est divisible par 400.

```
Écrire "Entrer une année"
A = Lire l'année
Si A ~/4 ALORS                    % ici '/n' voudra dire 'divisible par n'
  Écrire "non bissextile"
SINON                             % /4
  SI A ~/100 ALORS
    Écrire "bissextile"           % /4 ~/100 (implique ~/400)
  SINON                           % /100
    SI A /400 ALORS
      Écrire "bissextile"         % /4 /100 /400
    SINON
      Écrire "non bissextile"     % /4 /100 ~/400
```

```
Écrire "Entrer une année"
A = Lire l'année
Si A ~/4 ALORS                    % ici '/n' voudra dire 'divisible par n'
  Écrire "non "
SINON
  SI A /100 & ~/400 ALORS
    Écrire "non "                 % /4 & (/100 ~/400)

Écrire "bissextile"
```

```
Écrire "Entrer une année"
Lire l'année
SI /400 | (/4 & ~/100) ALORS      % ici '/n' voudra dire 'divisible par n'
  Écrire "bissextile"
SINON
  Écrire "non bissextile"
```
