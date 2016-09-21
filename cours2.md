
## Recap du cours 1

### Création
``` MatLab
A = 12                 % scalaire
A = [1:10]             % ligne
A = [1:10]'            % transposé
A = zeros(3)           % matrice de zéros 3x3
A = [1 2 3; 4 5 6]     % matrice
whos                   % par défaut ce sont des doubles
```

### Indexation
``` MatLab
A(1)                   % 1er item
A(5)                   % matlab index par colonne avec ()
A(:)                   % créer un vecteur colonne avec la matrice
A(2,2)                 % (ligne, colonne)
A(2,:)                 % 2e ligne, pour toutes les colonnes
A(2,2:end)             % 2e ligne, de la 2e colonne jusqu'à la fin
A(2,1:2:end)   ?       % 2e ligne, de la 1e colonne jusqu'à la fin par bons de 2
size(A)                % size de A
Li = size(A,1)         % nb de ligne de A
Col = size(A,2)        % nb de colonne de A
[Li Col] = size(A)     % les deux
```

### Opération
``` MatLab
A = [1 2 3; 4 5 6]
A+A                    % élément par élément
A*A                    % marche pas
A.*A                   % élément par élément
A*A(1) ?               % A(1) est un scalaire, élément par élément
A*2                    % 2 est un scalaire, élément par élément
A*A' ?                 % dimenssion agree
A/A                    % marche, mais /inv(A)
A./A                   % élément par élément
```

### Modulo
``` MatLab
mod(3,0)
rem(3,0)               % différence avec octave, donne 3 au lieu de NaN
```

REM(x,y)             | MOD(x,y)             |
---------------------| ---------------------|
fix(x/y)             | floor(x/y)           |
prends le signe de x | prends le signe de y |
y=0 => NaN           | y=0 => x             |
y=x & x~=0 => 0      | y=x => 0             |


## Autres types (chap.2 41-45)
### Chaine de caractère
Par exemple un fichier texte:
```
Par exemple.
ABCD
abcd
AaBb
012345
_% &^
```

La commande ```hexdump -C fichier.txt```  produit:
```
00000000  50 61 72 20 65 78 65 6d  70 6c 65 2e 0a 41 42 43  |Par exemple..ABC|
00000010  44 0a 61 62 63 64 0a 41  61 42 62 0a 30 31 32 33  |D.abcd.AaBb.0123|
00000020  34 35 0a 5f 25 26 5e 0a                           |45._%&^.|
00000028
```

Ce résultat est le contenu binaire du fichier. La première section est l'adresse, la seconde les valeurs hexadécimales telles qu'elles sont écrites dans le fichier ou en mémoire et la dernière, le contenu textuel une fois décodé avec la table ASCII.

La commande ```hexdump -e'"%07.8_ad  " 1/1 "%03d  "' -e'1/1 "%02x   "' -e'1/1 "%03o   "'  -e'1/1  "%_u"  "\n"' fichier.txt```:

```
00000000 080 50 120 P
00000001 097 61 141 a
00000002 114 72 162 r
00000003 032 20 040
00000004 101 65 145 e
00000005 120 78 170 x
00000006 101 65 145 e
00000007 109 6d 155 m
00000008 112 70 160 p
00000009 108 6c 154 l
00000010 101 65 145 e
00000011 046 2e 056 .
00000012 010 0a 012 lf
00000013 065 41 101 A
00000014 066 42 102 B
00000015 067 43 103 C
00000016 068 44 104 D
00000017 010 0a 012 lf
00000018 097 61 141 a
00000019 098 62 142 b
00000020 099 63 143 c
00000021 100 64 144 d
00000022 010 0a 012 lf
00000023 065 41 101 A
00000024 097 61 141 a
00000025 066 42 102 B
00000026 098 62 142 b
00000027 010 0a 012 lf
00000028 048 30 060 0
00000029 049 31 061 1
00000030 050 32 062 2
00000031 051 33 063 3
00000032 052 34 064 4
00000033 053 35 065 5
00000034 010 0a 012 lf
00000035 095 5f 137 _
00000036 037 25 045 %
00000037 038 26 046 &
00000038 094 5e 136 ^
00000039 010 0a 012 lf
```

Cette commande présente le même résultat affiché différemment. Les colonnes sont adresse, valeur décimale, valeur hexadécimale, valeur octale, caractère ASCII.

#### Céation
``` MatLab
a = 'abcd'
whos                                         % type "char" pour character
a(2)                                         % on peut l'indexer
a = '2'                                      % un seul char
a == 2                                       % faux? doit convertir a en entier ou vice-versa
uint8(a)                                     % a = 97 != 2
char(2)  ?                                   % rien? Voir ASCII, c'est un caractère inaffichable
2 + '2'  ?                                   % 52, les deux sont convertis en entier
'2' + '2'  ?                                 % 100, pour la même raison
a = [89 111 108 111]                         % on peut écrire les vals numériques
char(a)                                      % yup.. 'Yolo'

a = ['abs' ' ' '123']                        % concaténation
a = ['abs', ' ', '123']                      % les ',' aide la lisibilité
a = ['abc'; '123']                           % concaténation verticale
a = ['abc'; '1234']                          % erreur, dans octave il utilise toujours strvcat
a = strvcat('abc', '1234')                   % concaténation verticale en ajoutant des ' ' si nécessaire
```


#### opérations string (chap.2 41-45)

``` MatLab
strcmp('abc', 'abc')                         % 1
strcmp('abc', 'Abc')                         % 0, A != a
lower('AbC')                                 % abc
strcmp(lower('abc'), lower('Abc'))           % abc == abc => 1
strcmpi('abc', 'Abc')                        % strcmpi est insensible aux majuscules

deblank('abs   ')                            % enlève les espace à la fin
strcmp(deblank('abc'), deblank('abc '))
strcmpi(deblank('abc'), deblank('AbC '))     % couvre pas mal d'erreur de saisie
```



#### string conversion (chap.2 46-52)

``` MatLab
char(99)                                     % c
uint8('c')                                   % 99
a = int2str(99)                              % '99'
uint8(a)                                     % 57   57

a = int2str(3.1416)                          % '3'
a = num2str(3.1416)                          % '3.1416'
uint8(a)                                     %   51  46  49  52  49  54

a = num2str([1 2] * 3.1416)                  % '3.1416      6.2832'
uint8(a)                                     %   51  46  49  52  49  54  32  32  32  32  32  32  54  46  50  56  51  50

mat2str([1 3.1416])                          % '[1 3.1416]'

str2num('[1 2]')                             % 1   2
str2num('1 2 3.5')                           % 1.0000   2.0000   3.5000
```

#### test et affichage formaté (chap.2 53-54)

``` MatLab
isspace(' ')                                 % 1
isspace('a')                                 % 0

a = sprintf('Reponse =% i', 12)              % a = 'Reponse = 12'
fprintf('Reponse =%i', 12)                   % Reponse =12>>
fprintf('Reponse =%i\n', 12)                 % Reponse =12 (ajoute un <ENTER> après 12)
fprintf('Reponse =%02X\n', 12)               % Reponse =0C
fprintf('Reponse =%5.2f\n', 12)              % Reponse =12.00
fprintf('Reponse =%06.2f\n', 12)             % Reponse =012.00

sscanf('3.1415', '%f')                       % ans =  3.1415

a = input('Donnez un vecteur')               % a =    1   2   3
  >> [1 2 3]

a = str2num(input('Donnez un vecteur', 's'))
  >> [1 2 3]

bin2dec('0101')                              % 5, conversion binaire vers décimal
```

### cellules (chap.2 55-57)
``` MatLab
A = {}                                       % créer un cell array
A{1,1} = 'abc'                               % un champ string
A{1,2} = pi                                  % un champ double
A{2,1} = 1:10                                % un champ vecteur
A{2,2} = {'abc'}                             % un champ cell array imbriqué

A{:}                                         % vecteur colonne
A{3}                                         % 3.1416
A{2,1}                                       %  1    2    3    4    5    6    7    8    9   10
A{2,1}(3)                                    % 3
A{4}{1}                                      % 'abc'
A{4}{1}(1)                                   % 'a'

A(4) = []                                    % supprime un champ
```

### structures (a.k.a. enregistrement) (chap.2 57-63)
``` MatLab
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

produit:

```
>> whos
Variables in the current scope:

   Attr Name        Size                     Bytes  Class
   ==== ====        ====                     =====  =====
        user        1x2                         49  struct

>> user
user =

  1x2 struct array containing the fields:

    name
    email
    id

>> user(1)
ans =

  scalar structure containing the fields:

    name = JF pambrun
    email = a@bc.com
    id =  1

>> user(1).name
ans = JF pambrun

```


### nombre à point flottant (chap.2 64)
``` MatLab
A = zeros(3);A(1,1)=1;
B = sparse(A)
whos                                    % A= 72 Bytes, B= 28 Bytes

A = ones(3);A(1,1)=0;
B = sparse(A)
whos                                    % A= 72 Bytes, B= 112 Bytes

realmin                                 % 2.2251e-308
realmax                                 % 1.7977e+308

realmin('single')                       % 1.1755e-38
realmax('single')                       % 3.4028e+38

eps(1)                                  % 2.2204e-16
eps(0)                                  % 4.9407e-324

eps(single(1))                          % 1.1921e-07
eps(single(0))                          % 1.4013e-45
```
