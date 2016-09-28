Note:
 * Les boucles ne devaient pas faire partie des premiers exercices du TD 2.
 * On a déjà vu les 15 premières heures en 12.

## Retour sur le cours 4
 * if – elseif - else
 * switch-case
 * while
 * for
 * break et continue

Faire l'exercice de classement.

## Résolution de problèmes
 1. La **définition** du problème
 2. L’**analyse** du problème
 3. La **conception** des algorithmes
 4. La mise au point (aka. l'**implémentation**) du programme MATLAB
 5. La **vérification** du programme

### 1.Définition
QUI? QUE? QUOI?

 - Identifier les entités à manipuler
 - Identifier les traitements à effectuer
 - Identifier les résultats attendus

### 2.Analyse
COMMENT?

 - Inventer et réfléchir à diverses solutions possibles.
 - Il faut s'attendre à envisager plusieurs possibilités avant de trouver la bonne.
    * En programmation, il n'y a pas de solution unique.


### 3.Conception

 - Écrire dans l’ordre les opérations déduites de l’analyse.
 - Faire ressortir la structure de base
   * les structures de décision
   * les structures de répétition
 - Utiliser adéquatement le pseudo-code schématique.

### 4. Mise au point (aka. **implémentation**)
 - Coder la solution
 - Faire en sorte que le programme fonctionne bien.

### 5. Vérification
 - s'assurer que son programme fonctionne bien
 - Vérifier le programme avec des données tests
   * Données usuelles;
   * Données de cas habituellement problématique: matrice vide, matrice ligne, matrice colonne, nombres très grands ou très petits, nombres positifs, nombres négatifs.
   * Données pour vérifier les conditions

 Certaines des techniques communes
 - Test unitaire (unit testting)
   * test chaque petite fonction selon et test comment elles se comportent avec des données invalides
 - Test de couverture (coverage testting)
   * s'assure que tout le code a été testé
 - développement piloté par les tests (test driven development)
   * code d'abord les tests avec même l'implémentation des fonctions

## Déboguage: calcul du temps

#### pause
``` Matlab
pause()
pause(1.5)
```

#### clock
``` Matlab
t1 = clock;
pause(1) % instructions
t2 = clock;

temps_ecoule = etime(t2,t1)
```

#### cputime
``` Matlab
t1 = cputime;
pause(1) % instructions
t2 = cputime;

t2-t1
```

#### tic -toc
``` Matlab
tic;
pause(1) % instructions
toc
```

## Exercices

#### E1 : Nombres premiers
Trouver les nombres premiers (nombres qui se divisent seulement par 1 et lui-même) entre 50 et 100.

#### E2 : Rognage (cropping) d'image
Créer une sous-image de ```256x256``` représentant le milieu d'une image de taille inconnue ```NxM```, ```N``` et ```M``` > 256.

#### E3 : Étalonnage des niveaux de gris
Réétaler les valeurs d'une matrice entre ```voi = [v1, v2]``` vers ```[0, 255]``` pour l'affichage. Convertir en uint8.

``` Matlab
info = dicominfo('IM-0001-0001.dcm')               % charge les métadonnées
I = double( dicomread(info) );                     % charge l'image en double
I = I * info.RescaleSlope + info.RescaleIntercept; % applique la transformation pour obtenir les HU

imshow(I,[])
imcontrast

%         -1000 (vacuum)                    0 (eau)                    1000
% DICOM      |------------------------------|--------------------------->
%
% display                                   |-----------|
%                                           0 (noir)   255 (blanc)

% VOI transform
% DICOM      |------------------------v1-----|-------------v2----------->
%                                      \                  /
% display                              0|----------------|255
```

#### E4 : Calcul d'histogramme
Calculer l'histogramme d'une image I.

``` Matlab
I = imread('cameraman.tif');
imshow(I)
imcontrast
```

#### E5 : Décodage HTML
Soit le code HTML suivant, écrire le code qui permet d'extraire le contenu des balises ```<h1>``` ou ```<p>```.

``` HTML
<html>
<body>
<h1>Un titre</h1>
<p>Un paragraphe</p>
</body>
</html>
```

``` Matlab
html = '<html><body><h1>Un titre</h1><p>Un paragraphe</p></body></html>';
tag = 'p'; % ou 'h1'
```


#### E6 : Création d'une matrice contenant un cercle
Créer une matrice ```MxM``` de 0 (noir) avec un cercle de rayon ```R``` dont les valeurs sont égales à 1 (blanc) au centre.

```
+--------------------+
|####################|
|########*  *########|
|#####*        *#####|
|####*     __R__*####|  M
|####*          *####|
|#####*        *#####|
|########*  *########|
|####################|
+--------------------+
           M
```

#### E7 : Décodage et exécution de commandes

Soit les commandes suivantes dans un tableau de cellules ```commandes```:

``` xml
<square> x y w <square>
<circle> x y r <circle>
<line> x1 y1 x2 y2 <line>
<oval> x y w h <oval>
```

Créer un programme qui appel les fonctions ```drawSquare(x,y,w)```, ```drawCircle(x,y,r)```, ```drawLine(x1,y1,x2,y2)``` ou ```drawOval(x,y,w,h)``` en fonction de la liste de commandes.

## Solutions

#### E1 - Solution 1
``` Matlab
nombre_premier = []
for n = 50:100

    n_est_premier = true;

    for i = 2:n-1
        if mod(n,i) == 0
            n_est_premier = false;
        end
    end

    if n_est_premier
        nombre_premier = [nombre_premier n];
    end

end
disp(nombre_premier)
```

#### E1 - Solution 2
``` Matlab
nombre_premier = []
for n = 50:100

    n_est_premier = true;

    for i = 2:n-1
        if mod(n,i) == 0
            n_est_premier = false;
            break;                   % pas la peine de continuer
        end
    end

    if n_est_premier
        nombre_premier = [nombre_premier n];
    end

end
disp(nombre_premier)
```

#### E1 - Solution 3
``` Matlab
nombre_premier = []
for n = 50:100

    n_est_premier = true;

    for i = 2:sqrt(n)                % pas la peine de tester après sqrt(n)
        if mod(n,i) == 0
            n_est_premier = false;
            break;                   % pas la peine de continuer
        end
    end

    if n_est_premier
        nombre_premier = [nombre_premier n];
    end

end
disp(nombre_premier)
```


#### E2
``` Matlab
I = imread('peppers.png');

[sx,sy,sz] = size(I);
Ic = I( sx/2-127:sx/2+128 , sy/2-127:sy/2+128, :);

disp(size(Ic))
imshow(Ic)

```

#### E3
``` Matlab
info = dicominfo('IM-0001-0001.dcm')               % charge les métadonnées
I = double( dicomread(info) );                     % charge l'image en double
I = I * info.RescaleSlope + info.RescaleIntercept; % applique la transformation pour obtenir les HU

voi = [-134 301];  % value of interest
I = uint8(  ( double(I) - voi(1) )/( voi(2) - voi(1) ) * 255 );
imshow(I)
```

#### E4 - Solution 1
``` Matlab
I = imread('cameraman.tif');
bins = zeros(256,1);

for i = 1:size(bins)
    bins(i) = sum( I(:) == i-1 );
end

plot(bins)
% tic toc = 0.065654
```
#### E4 - Solution 2
``` Matlab
I = imread('cameraman.tif');
bins = zeros(256,1);

for x = 1:size(I,1)
    for y = 1:size(I,2)
        bins( I(x,y)+1 ) = bins( I(x,y)+1 ) + 1;
    end
end

plot(bins)
```

#### E4 - Solution 3
``` Matlab
I = imread('cameraman.tif');
bins = zeros(256,1);

for val = I(:)'
    bins(val+1) = bins(val+1) + 1;
end

plot(bins)
```

#### E5
``` Matlab
html = '<html><body><h1>Un titre</h1><p>Un paragraphe</p></body></html>';
tag = 'p';

debut = strfind(html, [ '<'  tag '>' ]);
fin   = strfind(html, [ '</' tag '>' ]);
disp( html( debut:fin ) )

debut = strfind(html, [ '<'  tag '>' ]) + length(tag)+2;
fin   = strfind(html, [ '</' tag '>' ]) -1;
disp( html( debut:fin ) )
```


#### E6 -Solution 1
``` Matlab
M = 200;
R = 25;

I = zeros(M, M);

for i = 1:M
    for j = 1:M
        I(i,j) = sqrt( (M/2 - i).^2 + (M/2 - j).^2 ) < 25;
    end
end
imshow(I)
```

#### E6 -Solution 2
``` Matlab
x = repmat(1:M, [M,1]);
y = repmat((1:M)', [1,M]);

imshow([x y],[])
I = sqrt( (M/2 - x).^2 + (M/2 - y).^2) < 25;

imshow(I)
```

#### E7
``` Matlab
commandes = {'<square> 24 55 23 <square>' ...
             '<circle> 24 55 23 <circle>' ...
             '<line> 24 55 23 65 <line>' ...
             '<oval> 24 55 23 65 <oval>'};

for cmd = commandes

    cmd = strsplit(char(cmd));

    switch char(cmd(1))
        case '<square>'
            fprintf('call drawSquare(%d, %d, %d)\n',...
                str2num(char(cmd(2))),...
                str2num(char(cmd(3))),...
                str2num(char(cmd(4))) )
        case '<circle>'
            fprintf('call drawCircle(%d, %d, %d)\n',...
                str2num(char(cmd(2))),...
                str2num(char(cmd(3))),...
                str2num(char(cmd(4))))
        case '<line>'
            fprintf('call drawLine(%d, %d, %d, %d)\n',...
                str2num(char(cmd(2))),...
                str2num(char(cmd(3))),...
                str2num(char(cmd(4))),...
                str2num(char(cmd(5))) )
        case '<oval>'
            fprintf('call drawOval(%d, %d, %d, %d)\n',...
                str2num(char(cmd(2))),...
                str2num(char(cmd(3))),...
                str2num(char(cmd(4))),...
                str2num(char(cmd(5))) )
    end
end
```

