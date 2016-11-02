## Retour sur les fonctions
  * Est un Fichier M.
  * Indentations, commentaires et en-tête.
  * Commentaire ```H1``` est un résumé d'une ligne.
  * Le nom de la fonction doit être le même que celui du fichier.
  * Un fichier peut contenir plusieurs fonction, mais une seule est visible de l'extérieur.
  * Ses variables sont locales.
  * L'ordre des paramètres d'entré est important.
  * Peut retourner une ou plusieurs valeurs.
  * nargin / nargout
  * varargin, varargout
  * Une fonction sans param peut être appelé sans ```()``` (p.ex. help ou nargin)
  * Une fontion que prend ques des 'Strings' en paramètre peut aussi être appelé sans ```()```. (p.ex. ```format('short','g')``` vs ```format short g```)
    
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

#### fscanf une ligne à la fois
``` Matlab
fid = fopen('filetest.txt', 'r');
fscanf(fid, 'ligne %d\n',1)
fscanf(fid, 'ligne %d\n',1)
fscanf(fid, 'ligne %d\n',1)
fclose(fid);
```

#### fscanf d'un coup
``` Matlab
fid = fopen('filetest.txt', 'r');
fscanf(fid, 'ligne %d\n')
fclose(fid);
```

#### fscanf "avancé"
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


#### exemple sscanf variées
``` Matlab
s = '2.7183  3.1416';
A = sscanf(s,'%f')

s = 'val: 2.7183  3.1416';
A = sscanf(s,'%f')% A = sscanf(s,'val: %f %f')

s = 'abc def hij klm';
[A count] = sscanf(s, '%s')

s = 'abc 12 def 13';
[A count] = sscanf(s, '%s %d')

% from doc scanf
s = '78°F 72°F 64°F 66°F 49°F';
sscanf(s, ['%d' char(176) 'F'])

s = '99999999999999';
A = sscanf(s, '%i')
%int64(A) %intmax('int32')
B = sscanf(s, '%li')
```

#### fgetl
``` Matlab
fid = fopen('filetest.txt', 'r');
tline = fgetl(fid);

while ischar(tline)
    disp(['ligne="' tline '"'])
    tline = fgetl(fid);
end

% a ce point ci, tline est numerique
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


#### lecture d'une image PPM
``` Matlab
% P6 
% 1024 788 
% # A comment
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

% parceque le fichier est stoké en ordre raster..
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
