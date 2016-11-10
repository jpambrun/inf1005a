##Retour sur les E/S
 * fid = fopen(filename, type): ouvre filename avec le type:
   * r : lecture
   * w : écriture
   * a : ajout
   * rt, wt, at : pour du texte
 * fclose(fid) : ferme le fichier (important!)
 * fprintf(fid,...): écrit du texte dans un fichier
 * on doit vérifier le retour de fopen, fclose et fprintf pour s'assurer que ça fonctionne (i.e. manque d'espace, mauvais nom de fichier)
 * frwite(fid, ...): écrit en binaire 
 * fscanf(fid, ...): lit une chaîne formatée
  * attention aux très grands chiffres (requiert %li pour long)
 * fread(fid, ...): lit en binaire
   * 'uint8=>uint8' pour le type permet de lire des uint8 et les convertir en uint8 (sinon Matlab les stocke en double)
 * fgetl(fid) : récupère une ligne et saute les \n\r
 * en lecture, on doit vérifier la fin du fichier (avec feof, ischar, etc.)
 



TODO:

* p.18 : est-ce qu'on peut vraiment utiliser le no de figure? la doc semble indique qu'il faut utiliser un handle.





``` Matlab
x = 0:.1:2*pi;
y1 = sin(x);
y2 = sawtooth(x*3);
y3 = tan(x);

%%
close all;
plot(x, y1) %y2

%% deux figures-ish
close all;
plot(x, y1)
plot(x, y2) % remplace plot(x, y1) dans la figure


%% deux figures
close all;
figure;plot(x, y1)
figure;plot(x, y2)

%% subplot horizontal
close all;
subplot(2,1,1);plot(x, y1)
subplot(2,1,2);plot(x, y2)


%% subplot vertical
close all;
subplot(1,2,1);plot(x, y1)
subplot(1,2,2);plot(x, y2)

%% subplot span
close all;
subplot(2,2,1);plot(x, y1)
subplot(2,2,2);plot(x, y2)
subplot(2,2,[3 4]);plot(x, y3)

%% plot (x1,y1,x2,y2)
close all;
plot(x, y1, x, y2)


%% plot (x1,y1,x2,y2) + style
close all;
plot(x, y1,':', x, y2,'-.', 'linewidth', 1.5)


%% plot (x1,y1,x2,y2) + couleur
close all;
plot(x, y1,':m', x, y2,'-.k', 'linewidth', 1.5)

%% plot (x1,y1,x2,y2) + marqueur
close all;
plot(x, y1,'-*', x, y2,'-s', 'linewidth', 1.5)


%% plot matrice
close all;
plot(x, [y1;y2])
% plot([y1;y2]')


%% get - set
close all;
h = plot(x,y1);
get(h)
set(h, 'LineWidth', 2)


%% get - set imbriqué (probablement pas à l'examen..)
close all;
h = figure;
plot(x, y1, x, y2)

% get(h)
% get(h.CurrentAxes)
% get(h.CurrentAxes.Children(1))

set(h.CurrentAxes, 'Xgrid', 'on');
set(h.CurrentAxes.Children(1), 'LineWidth', 2)

%% axis
close all;
plot(x,y1);
axis([0 2*pi -10 10])
% axis([0 2*pi -inf 10])


%% titres & labels
close all;
plot(x,y1);
title('mon titre')
xlabel('les X')
ylabel('les Y')
% text(pi, 0, '\leftarrow passage par zéro')
% text(pi, 0, '\leftarrow passage par zéro','Color','red','FontSize',14)
% text(pi, 0, '\leftarrow passage par zéro','Color','red','FontSize',14)
% text(pi, 0, 'passage par zéro \rightarrow','Color','red','FontSize',14, 'HorizontalAlignment', 'right')

%% légende
close all;
plot(x, y1, x, y2)
legend('sin(x)', 'sawtooth(x)')
% legend('sin(x)', 'cos(x)','Location','northwest')


%% hold
close all;
figure;
hold on
plot(x, y1)
plot(x, y2)


%% colormap
close all;
h = 160*membrane(1,100);
imshow(h,[])
% colormap(jet)
% colormap(bone)
% colormap(parula)

%% print
close all;
h = 160*membrane(1,10);
surf(h)
% print -djpeg toto.jpg % raster
% print -dpdf toto.pdf  % vectoriel

%% plot3
% from doc
t = 0:pi/50:10*pi;
st = sin(t);
ct = cos(t);

figure
plot3(st,ct,t)
% grid on

%% plotyy
close all
figure;plot(x, y1, x, y3)
figure;plotyy(x, y1, x, y3)
```
