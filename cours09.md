## Retour sur les fonctions
  * Est un Fichier M.
  * Indentations, commentaires et en-tête.
  * Commentaire ```H1``` est un résumé d'une ligne.
  * Le nom de la fonction doit être le même que celui du fichier.
  * Un fichier peut contenir plusieurs fonctions, mais une seule est visible de l'extérieur.
  * Ses variables sont locales.
  * L'ordre des paramètres d'entrée est important.
  * Peut retourner une ou plusieurs valeurs.
  * nargin / nargout
  * varargin, varargout
  * Une fonction sans param peut être appelé sans ```()``` (p.ex. help ou nargin)
  * Une fonction que prend que des 'Strings' en paramètre peut aussi être appelé sans ```()```. (p.ex. ```format('short','g')``` vs ```format short g```)
    
# Entrées/sorties (I/O)

### Fichiers (p. 3-13)
### Fichiers texte (p. 15-26)

#### Écriture simple
``` Matlab
fid = fopen('filetest.txt', 'wt'); % 'at'
fprintf(fid, 'ligne 1\n')
fprintf(fid, 'ligne 2\n')
fprintf(fid, 'ligne 3\n')
fclose(fid);
```

produit :
```
ans =
     8
ans =
     8
ans =
     8
```

et le fichier ```filetest.txt``` contient:

```
ligne 1
ligne 2
ligne 3

```

#### fscanf une ligne à la fois
``` Matlab
fid = fopen('filetest.txt', 'r');
fscanf(fid, 'ligne %d\n',1)
fscanf(fid, 'ligne %d\n',1)
fscanf(fid, 'ligne %d\n',1)
fclose(fid);
```

produit : 
```
ans =
     1
ans =
     2
ans =
     3
```

#### fscanf d'un coup
``` Matlab
fid = fopen('filetest.txt', 'r');
fscanf(fid, 'ligne %d\n')
fclose(fid);
```

produit :

```
ans =
     1
     2
     3
```

#### fscanf "avancé"
Avec le fichier commande:

```
<line> 24 55 23 65 <line>
<oval> 24 55 23 65 <oval>
<line> 56 23 74 77 <line>
```

``` Matlab
fid = fopen('commandes.txt', 'r');
i = 1;
while ~feof(fid)
    commandes(i).type = fscanf(fid, '%s\n',1);
    commandes(i).coords  = fscanf(fid, '%d\n',4);
    fscanf(fid, '%s\n',1);
    commandes(i)
    i = i+1;
end
fclose(fid);
```
produit :
```
ans = 
      type: '<line>'
    coords: [4x1 double]
ans = 
      type: '<oval>'
    coords: [4x1 double]
ans = 
      type: '<line>'
    coords: [4x1 double]
```


#### exemple sscanf variées
``` Matlab
s = '2.7183  3.1416';
A = sscanf(s,'%f')

s = 'val: 2.7183  3.1416';
B = sscanf(s,'%f')
B2 = sscanf(s,'val: %f %f')

s = 'abc def hij klm';
[C count] = sscanf(s, '%s')


s = 'abc 12 def 13';
[D count] = sscanf(s, '%s %d')

% from doc scanf
s = '78°F 72°F 64°F 66°F 49°F';
E = sscanf(s, ['%d' char(176) 'F'])

clc
s = '99999999999999';
F = sscanf(s, '%i') % int64(F)
G = sscanf(s, '%li')
intmax('int32')
```

produit:
```
A =
    2.7183
    3.1416
B =
     []
B2 =
    2.7183
    3.1416
C =
abcdefhijklm
count =
     4
D =
    97
    98
    99
    12
   100
   101
   102
    13
count =
     4
E =
    78
    72
    64
    66
    49
F =
   2.1475e+09    % 2147483647
G =
       99999999999999
ans =
  2147483647

```

#### fgetl
``` Matlab
fid = fopen('filetest.txt', 'r');
tline = fgetl(fid);

while ischar(tline)
    disp(['ligne="' tline '"'])
    tline = fgetl(fid);
end

% a ce point-ci, tline est numérique
tline
fclose(fid);
```

### Fichiers binaires (p. 28-39)

#### fwrite / fread
``` Matlab
A = eye(16) .* meshgrid(1:16)
fid = fopen('eye16.bin', 'w');
fwrite(fid, A, 'uint8')
fclose(fid);

fid = fopen('eye16.bin', 'r');
B = fread(fid,[16,16],'uint8')
fclose(fid);

isequal(A,B)
```

```hexdump -C eye16.bin``` produit :

```
00000000  01 00 00 00 00 00 00 00  00 00 00 00 00 00 00 00  |................|
00000010  00 02 00 00 00 00 00 00  00 00 00 00 00 00 00 00  |................|
00000020  00 00 03 00 00 00 00 00  00 00 00 00 00 00 00 00  |................|
00000030  00 00 00 04 00 00 00 00  00 00 00 00 00 00 00 00  |................|
00000040  00 00 00 00 05 00 00 00  00 00 00 00 00 00 00 00  |................|
00000050  00 00 00 00 00 06 00 00  00 00 00 00 00 00 00 00  |................|
00000060  00 00 00 00 00 00 07 00  00 00 00 00 00 00 00 00  |................|
00000070  00 00 00 00 00 00 00 08  00 00 00 00 00 00 00 00  |................|
00000080  00 00 00 00 00 00 00 00  09 00 00 00 00 00 00 00  |................|
00000090  00 00 00 00 00 00 00 00  00 0a 00 00 00 00 00 00  |................|
000000a0  00 00 00 00 00 00 00 00  00 00 0b 00 00 00 00 00  |................|
000000b0  00 00 00 00 00 00 00 00  00 00 00 0c 00 00 00 00  |................|
000000c0  00 00 00 00 00 00 00 00  00 00 00 00 0d 00 00 00  |................|
000000d0  00 00 00 00 00 00 00 00  00 00 00 00 00 0e 00 00  |................|
000000e0  00 00 00 00 00 00 00 00  00 00 00 00 00 00 0f 00  |................|
000000f0  00 00 00 00 00 00 00 00  00 00 00 00 00 00 00 10  |................|
00000100
```


#### lecture d'une image PPM
``` Matlab
I = imread('peppers.png');
imwrite(I, 'peppers.ppm')
```

```hexdump -C .bin``` produit :

```
00000000  50 36 20 35 31 32 20 33  38 34 20 32 35 35 0a 3e  |P6 512 384 255.>|
00000010  1d 40 3f 1f 40 3f 22 40  41 1e 3c 42 1b 3b 3f 1f  |.@?.@?"@A.<B.;?.|
00000020  3e 3d 1f 3e 3f 1e 3d 3f  1e 3b 40 1f 3a 40 1e 3d  |>=.>?.=?.;@.:@.=|
00000030  3d 1e 3a 41 1e 38 40 20  3b 3d 1f 3b 3e 1e 3c 3f  |=.:A.8@ ;=.;>.<?|
00000040  1e 3e 41 20 40 41 20 3d  40 1d 3a 3d 1d 39 40 1e  |.>A @A =@.:=.9@.|
00000050  38 41 1d 3a 40 1e 3d 42  1e 3d 47 1f 42 43 21 43  |8A.:@.=B.=G.BC!C|
00000060  41 21 3f 40 23 3e 3e 20  3e 44 1f 40 44 23 42 46  |A!?@#>> >D.@D#BF|
00000070  1f 41 46 1f 3f 47 21 41  46 22 44 44 21 43 4a 25  |.AF.?G!AF"DD!CJ%|
00000080  45 4a 25 45 46 24 45 46  24 46 47 25 43 47 24 43  |EJ%EF$EF$FG%CG$C|
00000090  48 22 45 4a 23 46 46 22  46 45 22 43 46 23 41 43  |H"EJ#FF"FE"CF#AC|
000000a0  22 3f 43 20 41 43 21 42  45 25 43 45 24 42 42 23  |"?C AC!BE%CE$BB#|
000000b0  3f 43 23 40 43 20 40 47  20 42 46 23 42 45 23 41  |?C#@C @G BF#BE#A|
000000c0  43 20 41 44 22 41 47 24  42 45 23 41 46 25 44 47  |C AD"AG$BE#AF%DG|
000000d0  24 45 47 22 43 47 24 42  46 26 44 43 25 44 44 20  |$EG"CG$BF&DC%DD |
000000e0  3f 43 1e 40 3c 1c 40 39  1c 3a 38 18 38 33 15 35  |?C.@<.@9.:8.83.5|
000000f0  2e 16 2f 2d 16 31 33 18  36 36 19 33 36 19 37 37  |../-.13.66.36.77|
00000100  1b 39 3a 1e 3b 36 20 38  36 1e 34 39 1d 33 3a 1d  |.9:.;6 86.49.3:.|
...
```

``` Matlab
% P6 
% 1024 788 
% 255

% RGBRGBRGB

clc

fid = fopen('peppers.ppm', 'r');

% Lire en-tete
i_magic = fscanf(fid, '%s ',1)
i_size  = fscanf(fid, '%d ',2)
i_max   = fscanf(fid, '%d ',1)


% Lire pixels (RGBRGB... en ordre raster (i.e. par ligne)
i_raw = fread(fid, 'uint8=>uint8');

R= i_raw(1:3:end);
G= i_raw(2:3:end);
B= i_raw(3:3:end);

I = [R,G,B];
I = reshape(I, [i_size(1), i_size(2),3]);

% parceque le fichier est stocké en ordre raster..
I = permute(I,[2 1 3]);

fclose(fid)

imshow(I,[0 255])
```


### Détection de la fin des fichiers (p. 41-42)
``` Matlab
fid = fopen('filetest.txt', 'r');
while ~feof(fid)
    tline = fgetl(fid);
    if ischar(tline)
       tline % doStuff(tline)
    end
end
tline
fclose(fid);
```

### Manipulation de fichiers et de répertoires (p. 44)
