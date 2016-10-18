## Retour sur le cours 6
 * Fonction
    * Est un Fichier M.
    * Indentations, commentaires et en-tête comme un script.
    * La première ligne de commentaire après ```function``` est la ligne ```H1```. Elle contient un résumé d'une ligne.
    * Les lignes suivantes sont la description détaillé.
    * Nom de la fonction doit être le même que celui du fichier.
    * Ses variables sont locales.
    * Peut prendre des paramètres en entré.
    * L'ordre des paramètre est important. C'est la position qui détermine dans quel variable ils seront placés.
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
%   C = ADDME(A) additionne A a lui meme.
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
 * Une copie de ```n``` de ```messtats()``` est passé dans ```n``` de mamoyenne. Ce n'est pas la même variable. Changer ```n``` dans mamoyenne n'affecte pas ```n``` dans messtats.
 * Il est impossible d'utiliser les fonction ```min()``` et ```max()``` après la ligne ```[min, max] = minmax(x);```. Avant ça porterait à confusion.

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
  590.2361  % même si la variable s'appel psnr, c'est le résultat de mse étant donné la 2e position

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
