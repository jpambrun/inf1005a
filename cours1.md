## Intro
#### Tour de Maltlab
 * REPL (Read, Eval, Print Loop)
 * help, doc, tab

Petit exemple:
``` MatLab
x = [0:0.1:2*pi];               % créer un vecteur ligne de 0 à 2pi par incrément de .1
y = sin(x);                     % le ';' supprime la sortie
plot(x,y);                      %
```

## Types (chap.2 3-9)
* Nom (Identificateur)
  * commence par une lettre
  * peut pas être un mot clef (break if)
* int, char, double, etc.
* whos

``` MatLab
A = 2
whos                            % A est un scalaire de type double
A = uint8(2)
whos                            % A est un scalaire de type uint8 (non-signé 8 bit)
```

## Matrice
#### Création (chap.2 10-15)

x`` MatLab
A = 3.1416
A = 1:9                         % 1   2   3   4   5   6   7   8   9
A = 1:3:9                       % 1   4   7
A = 9:-3:1                      % 9   6   3
A = 9:3:1                       % []
A = 9:1                         % []
A = ones(3), zeros(3), eye(3), randn(3)
A = [1,2]
A = [1 2]
A = [1;2]
A = [1 2; 3 4]
```

#### Indexation (chap.2 16-21)
``` MatLab
A = [1 2 3 4; 5 6 7 8; 9 10 11 12]
A(1,2)                          % 2
A(6)                            % 10
A(:)                            % sous forme de vecteur
A(2,:)                          % 2e ligne
A(:,2)                          % 2e colonne
A(2,1:2)                        % 5   6
```

``` MatLab
size(A)                         % 3  4
length(A)                       % 4
numel(A)                        % 12
```

#### Opérations (chap.2 22-34)

 * **Attention:** ```A \ B``` n'est pas strictement égal à ```inv(A) * B```. En fait, ```\``` est une pseudo inverse (!= inv()). 


``` MatLab
A= [1 2 3]; B=[4;5;6];C=5
A*C
A*A                             % error
A^2                             % error
A*B                             % 32
A.*A                            % produit élément par élément
A+A                             % somme élément par élément
A+B                             % octave ne produit pas d'erreur, mais Matlab ?
A+C                             % Additionne C à chaque éléments de A
A'+B
B*A
```


#### système d'équation (chap.2 35-37)
``` MatLab
A = [-1 1 -3;2 1 -1;3 -2 4]     % p.35
B = [4;8;12]
inv(A)*B
A\B                             % marcherait même si mal conditionné
```

## MOD vs. REM (chap.2 39-49)
1. MOD(x,0) =x , whereas REM(x,0)=NaN
2. MOD(x,y) has the sign of y, while REM(x,y) has the sign of x
3. MOD and REM are equal if x and y have the same sign.

## RECAP
``` MatLab
I = imread('cameraman.tif');
whos
imshow(I*3)
imshow(I/3)
imshow(I*I)
imshow(I.*I)
imshow(I-100)
imshow([I I])
imshow([I;I])
imshow(I')
imshow(I/64*64)
imshow(I(1:50,:))
imshow(I(100:200,100:200))
imshow(mod(I,1))
imshow(mod(I,255))
```

