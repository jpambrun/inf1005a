
## Recap cours 1

```
% création
A = 12                  % scalaire
A = [1:10]              % ligne
A = [1:10]'             % colonne
A = zeros(3)            % matrice
A = [1 2 3; 4 5 6]      % matrice
whos                    % default to double
```

```
% indéxation
A(1)                    % 1er item
A(5) ?                  % index par colonne
A(:)                    % créer une colonne
A(2,2)                  % (ligne, colonne)
A(2,:)                  % 2e ligne, pour toute les colonnes
A(2,2:end)              % 2e ligne, de la 2e colonnes jusqu'à la fin    
A(2,1:2:end)   ?        % 2e ligne, de la 1e colonnes jusqu'à la fin par bon de 2
size(A)                 % size de A
Li = size(A,1)          % nb de ligne de A
Col = size(A,2)         % nb de colonne de A
[Li Col] = size(A)      % les deux
```

```
% opération
A+A                     % élément par élément
A*A                     % marche pas
A.*A                    % élément par élément
A*A(1) ?                % A(1) est un scalaire, élément par élément
A*2                     % 2 est un scalaire, élément par élément
A*A' ?                  % dimenssion agree 
A/A                     % marche, mais /inv(A)
A./A                    % élément par élément
```

```
mod(3,0)          
rem(3,0)                % difference avec octave, donne pas un NaN
```

REM(x,y) | MOD(x,y) |
--- | --- |
fix(x/y) | floor(x/y) |
prend le signe de x | prend le signe de y |
y=0 => NaN|y=0 => x|
y=x & x~=0 => 0 |y=x => 0|


## Autre types (chap.2 41-45)
### Chaine de caractère
vim c2.txt
```
Par exemple..
ABCD
abcd
AaBb
012345
_%&^
```

```
hexdump -C c2.txt
hexdump -e'"%07.8_ad  " 1/1 "%03d  "' -e'1/1 "%02x   "' -e'1/1 "%03o   "'  -e'1/1  "%_u"  "\n"' c2.txt
```

dans matlab
```
a = 'abcd'          
whos                    % type
a(2)                    % on peut l'indexer 
a = '2'                 % un char 
a == 2                  % faux?, doit convertir a en int ou vice-versa
uint8(a)                % a = '' en ASCII
char(2)  ?              % rien? voir ASCII
2 + '2'  ?              % casté en int 
'2' + '2'  ?            % 100, pour la même raison 
a = [89 111 108 111]    % on peut écrire les vals numérique
char(a)                 % yup..

a = ['abs' ' ' '123']  % concat
a = ['abs', ' ', '123']     % les ',' aide la lisibilit.é 
a = ['abc'; '123']     % vertical concat
a = ['abc'; '1234']    % diff dans octave (utilise toujours strvcat)
a = strvcat('abc', '1234')
```


### operations string (chap.2 41-45)

```                
strcmp('abc', 'abc')                    % 1
strcmp('abc', 'Abc')                    % 0, case
tolower('AbC')
strcmp(tolower('abc'), tolower('Abc'))  % 
strcmpi('abc', 'Abc')                   % 

deblank('abs   ')                       % enlève les espace à la fin
strcmp(deblank('abc'), deblank('abc ')) 
strcmpi(deblank('abc'), deblank('AbC ')) % couvre pas mal

whos
length()  ?
```



### string conversion (chap.2 46-52)

```
char(99)
uint8('c')
a = int2str(99)
uint8(a)

a = int2str(3.1416)    % what
a = num2str(3.1416)
uint8(a)


a = num2str([1 2] * 3.1416)
uint8(a)

mat2str([1 3.1416])    % produit une string


str2num('[1 2]')
whos

str2num('1 2 3.5')
whos
```

### test et affichage formaté (chap.2 53-54)

```
isspace(' ')
isspace('a')
isspace("\t\n")


a = sprintf('Reponse = %i', 12)
fprintf('Reponse = %i', 12)
fprintf('Reponse = %i\n', 12)
fprintf('Reponse = %02X\n', 12)
fprintf('Reponse = %5.2f\n', 12)    % compte le '.'
fprintf('Reponse = %06.2f\n', 12)   % zero padding

sscanf('3.1415', '%f')

a = input('Donnez un vecteur')  % Attention: ca avalue l'entre
  >> [1 2 3]

a = input('Donnez un vecteur')
  >> delete 'toto.m'
  >> [une var qui existe]

a = str2num(input('Donnez un vecteur', ''))
  >> [1 2 3]

bin2dec('0101')
```

### cellules (chap.2 55-57)
```
A = {}                  % créer un cell array
A{1,1} = 'abc'
A{1,2} = pi
A{2,1} = 1:10
A{2,2} = {'abc'}        % cell array imbriqué

A{:}                    % vecteur colonne
A{3}                    % 3e item
A{2,1}
A{2,1}(3)
A{4}{1}
A{4}{1}(1)

% delete
A(4) = []               % attention paranthese!
```

### structures (a.k.a. enregistrements) (chap.2 57-63)
```
user.name = 'JF pambrun'
user.email = 'a@bc.com'
user.id = 1

user(2).name = 'Paul Tr'
user(2).email = 'b@bc.com'
user(2).id = 2

whos

user
user(1)
user(1).name
```

### nombre à point flottant (chap.2 64)
```
A = zeros(3);A(1,1)=1;
B = sparse(A)
whos

A = ones(3);A(1,1)=0;
B = sparse(A)
whos

realmin
realmax

realmin('single')
realmax('single')

eps(1)
eps(0)

eps(single(1))
eps(single(0))
```