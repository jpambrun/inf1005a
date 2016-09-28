Note:
 * Les boucles ne devait pas faire partie des permiers exercices du TD 2.
 * On a déjà vu les 15 primières heures en 12.

## Retour sur le cours 4
 * Todo

## Déboguage: calcul du temps

``` Matlab
t1 = clock
%something slow
t2 = clock

temps_ecoule = etime(t2,t1)
```

``` Matlab
temps = cputime
```

``` Matlab
tic;
% instructions      
toc
```

tic toc == wall time ou cpu time?

``` Matlab
pause()
pause(1.5)
```

## Exercices

#### Nombres premiers
Trouver les nombre premier (nombre qui se divise seulement par 1 et lui-même) entre 50 et 100.

#### Rognage (cropping) d'image
Créer une sous-image de 256x256 représentant le millieu d'une image de taille inconue NxM, N et M > 256.

#### Étalonnage des niveaux de gris
Réétaler les valeurs d'une matrice entre clim = [new_min, new_max] vers [0,255] pour l'affichage. Convertir en uint8.

#### Calcul d'histogramme
Calculer l'histogramme d'une image.

#### Décodage HTML
Soit le code HTML suivant:
``` HTML
<html>
<body>
<h1>Un titre</h1>
<p>Un paragraphe</p>
</body>
</html>
```
Écrire le code qui permet d'extraire le contenu des balises ```<h1>``` ou ```<p>```.

#### Création d'une matrice contenant un cercle
Créer une matrice MxM de zéros avec un cercle de rayon R dont la valeur égal 1 en son centre.

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

#### Décodage et éxécution de comandes




