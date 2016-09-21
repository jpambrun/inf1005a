[3.25] Le professeur sait susciter l’intérêt des étudiants pour la matière du cours.

[3.68] Le professeur explique la matière du cours de façon claire et structurée.

[3.75] Le professeur enrichit le contenu du cours par sa culture scientifique, son expérience ou ses activités de recherche.

[3.87] Le professeur utilise des exemples qui favorisent une meilleure compréhension de la matière.

[3.87] Je suis satisfait des apprentissages réalisés dans ce cours.


#### Négatifs
[4] Plus d'exemples

[1] Plus participatif

[1] Intonation

[1] Meilleure utilisation du tableau

[1] Réponse pas claire à certaines questions

[1] Meilleure structure

#### Positif
[4] Maîtrise de la matière.

[3] Bonne utilisation du support didactique

#### Commentaires
- Micro? Ça serait mieux sans?


### Récapitulatif du cours 4

#### Fichier scriptes

 * a un nom (pas de mots clefs, pas de fonction qui existe déjà, commence par une lettre, etc.)
 * doit obligatoirement avoir un en-tête (nom, but, auteurs, date de création, date de modification)
 * le code doit être indenté
 * les commentaires commencent par %
 * les sections par %% (utile pour exécuter une seule section avec ctrl+enter)
 * F5 exécute le stript, F9 le code surligné
 * input() permet de saisir des données de l'utilisateur
 * disp, display, fprintf permettent d'afficher des résultats

#### Structures de programmation
 * opérateurs relationnels >, <, <=, >=, ==, ~=
 * all(), any()
 * indexation logique (p.ex. A =1:5;A(A<3)=A(A<3)*10 =>    10   20    3    4    5)
 * opérateurs logiques &, |, |, xor
 * || et && peuvent être coucircuité (p.ex.  (1 || fprintf('abc') == 3) n'affiche pas 'abc' )
 * pseudo-code
   * permet de structurer les idées sans avoir à se soucier du code
   * mots-clef comme Lire, Écrire, TANT QUE condition FAIRE, POUR ensemble_de_données FAIRE, SI condition ALORS --- SINON, etc.
   * doit être indenté aussi

## Structures de programmation

### if – elseif - else (chap.4 38-42)


Simple if:
``` Matlab
A = 12.5;
if mod(A,1) == 0
   disp('A est un entier')
end
```

if - else:
``` Matlab
if mod(A,1) == 0
   disp('A est un entier')
else
   disp('A n''est pas un entier')
end
```

if imbriqué:
``` Matlab
A = 12
if mod(A,1) ~= 0
   disp('A n''est pas un entier')
else
   if mod(A, 2) == 0
      disp('A est pair')
   end
end
```

if -elseif équivalent:
``` Matlab
A = 12
if mod(A,1) ~= 0
   disp('A n''est pas un entier')
elseif mod(A, 2) == 0
    disp('A est pair')
end
```

Exercice:
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

Solution:
``` Matlab
A = input('Entrer une année')
if mod(A,4) == 0
  fprintf('non ')
else
  if mod(A,4) == 0 & mod(A,400) ~= 0
    Écrire "non "
  end
end
fprintf('bissextile\n')
```



if - elseif en séquence
``` Matlab
%A = input('Écrire une couleur')   % 'bleu'
A = 'jaune'
if strcmp(A, 'rouge')
   rgb = [1 0 0]
elseif strcmp(A, 'vert')
   rgb = [0 1 0]
elseif strcmp(A, 'bleu')
   rgb = [0 0 1]
elseif strcmp(A, 'jaune')
   rgb = [1 1 0]
else
  disp('connais pas')
end
```

### switch-case (chap.4 43-46)

switch-case (chap.4 38-42)
``` Matlab
A = 'jaune'
switch A
  case 'rouge'                % {'rouge', 'red', 'R'} pourrait permettre plusieurs bonne réponses
     rgb = [1 0 0]
  case 'vert'
     rgb = [0 1 0]
  case 'bleu'
     rgb = [0 0 1]
  case 'jaune'
     rgb = [1 1 0]
  otherwise
    disp('connais pas')
end
```

## Boucle de répétitions

### While (chap.4 47-51)
Écrire l'alphabet:
``` Matlab
L = 'a'
while(L <= 'z')
   disp(L)
   L = char(L + 1);        % L = L + 1 marche pas, pourquoi?
end
```

### For (chap.4 52-54)
Écrire l'alphabet:
``` Matlab
for L = ['a':'z']         % marche dans octave..
   disp(L)
end
```

#### Ex.
coder eye()

``` Matlab
D= [5,4];
e = [];
for i = 1:D(1)
   for j = 1:D(2)
      %if i==j
      %    e(i,j) = 1;
      %else
      %    e(i,j) = 0;
      %end
      e(i,j) = i == j;
   end
end
disp(e)
```

### break et continue (chap.4 55)
Somme de seulement les nombre pairs entre 1 et 10

``` Matlab
S=0;
for i = 1:10
   if mod(i,2) ~= 0
       continue;
   end
   S = S + i;
end
disp(S)
```


``` Matlab
S=0;
i=1;
while(1)              % NE PAS FAIRE
   if mod(i,2) ~= 0
       i = i + 1;     % sinon, endless loop
       continue;
   end
   if i > 10
       break;
   end
   S = S + i;
   i = i + 1;
end
disp(S)
```

#### Ex.
sort:
``` Matlab
A = [6 3 2 4 5 2 3]
A = 'lkdjas jolrjdasflkj '
for i = 1:length(A)
   for j = i+1:length(A)
      if A(j) < A(i)
         temp = A(j);
         A(j) = A(i);
         A(i) = temp;
         disp(A)
      end
   end
end
disp(A)
```
