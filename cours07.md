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

## Particularités d’une fonction en MATLAB
