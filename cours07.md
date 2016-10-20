## Retour sur le cours 6
 * Fonction
    * Est un Fichier M.
    * Indentations, commentaires et en-tête comme un script.
    * La première ligne de commentaire après ```function``` est la ligne ```H1```. Elle contient un résumé d'une ligne.
    * Les lignes suivantes sont la description détaillée.
    * Le nom de la fonction doit être le même que celui du fichier.
    * Ses variables sont locales.
    * Peut prendre des paramètres en entrée.
    * L'ordre des paramètres est important. C'est la position qui détermine dans quelle variable ils seront placés.
    * Peut retourner une ou plusieurs valeurs.

#### Bon exemple:

``` Matlab
%***************************************
% Nom du fichier: addme.m
% Description: Exemple de fonction
% Auteur: JF Pambrun (inspiré de 'doc nargin')
% Date: 18 oct. 2016
%***************************************

function [c] = addme (a, b)
% ADD  Additionne deux valeurs.
%   C = ADDME(A) additionne A à lui-même.
%   C = ADDME(A,B) additionne A et B ensemble.
%
%   See also SUM, PLUS.
  c = a + b;
end
```

#### Exemple de plusieurs fonctions dans un fichier M:

``` Matlab
function [moyenne, min, max] = messtats (x)
  n = length(x);
  moyenne    = mamoyenne(x,n);
  [min, max] = minmax(x);
end

function a = mamoyenne(v,n)
  a = sum(v)/n;
end

function [min, max] = minmax(v)
  min = min(v);
  max = max(v);
end
```
Notes:
 * Supporant que le fichier M s'appel ```messtats.m```, seul la fonction ```messtats()``` sera accessible de l'extérieur.
 * C.-à-d. que seule ```messtats()``` peut utiliser ```mamoyenne(v,n)``` et ```minmax(v)```.
 * La variable ```n``` est local à ```messtats()```, elle n'est pas accessible dans le script/fonction qui l'appel ou les fonctions qu'elle appel (```mamoyenne()``` et ```minmax()```).
 * Une copie de ```n``` de ```messtats()``` est passé dans ```n``` de mamoyenne. Ce n'est pas la même variable. Changer ```n``` dans mamoyenne n'affecte pas ```n``` dans messtats.
 * Il est impossible d'utiliser les fonction ```min()``` et ```max()``` après la ligne ```[min, max] = minmax(x);```. Avant ça porterait à confusion.
 * Les fonctions d'un même fichier ont priorité dans l'ordre d'appel sur les fonctions définies ailleurs.
    * Peut être utile pour le débogage. On remplace une fonction par un 'stub' qui retourne toujours la même valeur connue.
p.ex. :

``` Matlab
function [cmd] = getAndDecodeCommand (ip, port)
  rep = getNextCommand(ip, port)

  % decode rep...
  % cmd = ...

end


function [rep] = getNextCommand (ip, port)
  rep = '<square> 12 34 5 <square>';
end
```


## nargin() / nargout ()

 * **N**umber of function **in**put **arg**uments
 * **N**umber of function **out**put **arg**uments


``` Matlab
% tiré de: doc nargin

function c = addme(a,b)

switch nargin
    case 2
        c = a + b;
    case 1
        c = a + a;
    otherwise
        c = 0;
end
```

Au cours 6, j'avais proposé:

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

Mais ```nargin()``` est plus élégant et lisible:

``` Matlab
    if nargin() < 1
        D = [5,5];
    end
```


## Nombre indéfini de paramètres / valeurs de retour

``` Matlab
function [ varargout ] = numels( varargin )
%NUMELS Number of elements in multiple arrays
%   [N1, N2, ...] = numel(A, B, ...) returns the number of elements, N1,
%   N2, ..., in array A,B, ...

    for i=1:length(varargin)
        varargout{i} = numel(varargin{i});
    end
end
```
```
>> numels(eye(3))
ans =
     9
>> numels(eye(3), eye(5))
ans =
     9
>> [N1,N2] = numels(eye(3), eye(5))

N1 =
     9

N2 =
    25
```



``` Matlab
function [ mad, mse, psnr ] = immetric( I, Id )
%IMMETRIC Compute image metrics
%   [ mad, mse, psnr ] = immetric( I, Id ) ...
    I = double(I);
    Id = double(Id);

    fprintf('calc mad')
    Idiff = I-Id;
    mad = max(abs(Idiff(:)));

    if nargout > 1
        fprintf(', mse');
        mse = mean(Idiff(:).^2);
    end

    if nargout > 2
        fprintf(', psnr\n');
        psnr = 20*log10(max(I(:))/sqrt(mse));
    end
end
```

```
>> immetric(I, Id)
calc mad
ans =

   109

>> [mad, psnr] = immetric(I, Id)
calc mad, mse
mad =
   109

psnr =
  590.2361  % même si la variable s'appelle psnr, c'est le résultat de mse étant donné la 2e position

>> [mad, mse, psnr] = immetric(I, Id)
calc mad, mse, psnr

mad =
   109

mse =
  590.2361


psnr =
   20.3522

>> if immetric(I, Id) > 10
        %
   end
calc mad
>>
```


## Particularités d’une fonction en MATLAB


## Exercice

### Intra passé
* intra1005AIntraSolH16.pdf : Q2

### Tiré de 'Chapitre 4 - Exercices matlab' (Guillaume-Alexandre Bilodeau)
#### Exercice #19: Calcul de pi
Écrire un programme qui calcule la valeur de π à partir de la série infinie

pi = 4 - 4/3 + 3/5 - 4/7 + 4/9 - 4/11 ...

Le programme affiche les valeurs de pi, selon le nombre de termes choisis par l'utilisateur.
Finalement le programme détermine et affiche le nombre de termes nécessaires de cette
série avant d'obtenir une erreur de 0.00001.

#### Exercice #21:
Une personne à la retraite dépose 300 000$ dans un compte qui paye 5% d'intérêt par
année. La personne planifie de retirer l'argent du compte une fois par année. Il commence
par retirer 25 000$ la première année, et ensuite pour les années futures, il majore le
montant retiré par le taux d'inflation. Par exemple, si le taux d'inflation est de 3%, il retire
25 750% la deuxième année. Calculer le nombre d'années nécessaires avant que le
compte contienne 0$ pour un taux d'inflation spécifié par l'utilisateur. Afficher le résultat
avec fprintf().

#### Exercice #28 Distance la plus courte entre des domiciles
Soit l'École Polytechnique aux coordonnées (0,0) d'un plan. L'axe des Y pointe vers le
nord de l'île de Montréal et l'axe des X pointe vers l'est de l'île. On peut alors exprimer la
position du domicile d'une personne dans ce référentiel.
Écrire un programme qui demande des noms de personnes et les coordonnées (x,y) de
leurs résidences dans le référentiel décrit précédemment et affiche les noms des deux
personnes habitant le plus près l'une de l'autre.


### Solutions

#### #19

``` Matlab
tol = 0.00001;
pi = 0;

for i = 0:1000000
    denom = 1+(i*2);

    if( mod(i,2) == 0 )
        sign = 1;
    else
        sign = -1;
    end

    pi_suiv = pi + sign * 4/denom;

    delta = abs(pi_suiv - pi);

    if (delta < tol)
        break;
    else
        pi = pi_suiv;
    end
end

fprintf('pi=%f\n', pi)
```


#### #21

``` Matlab
% t_inf = input..
t_inf   = 0.03;
t_int   = 0.05;
solde   = 300000;
retrait = 25000;

an      = 0;

while (solde > 0)
    an = an + 1
    solde = solde * (1+t_int)
    solde = solde - retrait
    retrait = retrait * (1+t_inf)
end

```

#### #29

``` Matlab
% for i=1:100 % meh..
%     nom = input('Entrer un nom (rien pour terminer): ','s');
%     if strcmp(nom, '')
%         break;
%     end
%
%     residence(i).nom = nom;
%     x = input('Entrer une coord x: ');
%     y = input('Entrer une coord y: ');
%     if ~isreal(x) || ~isnumeric(x) || ~isreal(y) || ~isnumeric(y)
%         error('doit etre un nombre réel')
%     end
%     residence(i).x = x;
%     residence(i).y = y;
% end

residence(1).nom = 'r1';
residence(1).x = 12;
residence(1).y = -11;

residence(2).nom = 'asldkfj lkj';
residence(2).x = 123;
residence(2).y = 412;

residence(3).nom = 'r2';
residence(3).x = 12;
residence(3).y = -12;

residence(4).nom = 'asldkfj lkj';
residence(4).x = 124;
residence(4).y = -121;

pluspetitedistance = inf;
nom1 = '';
nom2 = '';

for i = 1:length(residence)-1
    for j = i+1:length(residence)
        distance = sqrt((residence(i).x-residence(j).x).^2 + (residence(i).y-residence(j).y).^2)
        if distance < pluspetitedistance
            pluspetitedistance = distance;
            nom1 = residence(i).nom;
            nom2 = residence(j).nom;
        end
    end
end

pluspetitedistance
nom1
nom2
```
