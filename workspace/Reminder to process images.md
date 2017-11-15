Vertical images : need to have an horizontal thumb

Gallery without text : OK. Caption field can be empty

##PHOTOFILTRE

Vérifier le meilleur rendu avec :
- recadrage
- niveaux automatiques
- contraste automatique


##GIMP

Taille full : 1600*1064  ou   1064*1600
Taille th : 600*400

Poids full : entre 100 et 250 ko
Poids miniatures th : entre 10 et 50 ko

Pour les miniatures horizontales :
- Echelle et taille de l'image : mettre 600 pour la largueur
- Export as... [...]-th.jpg avec une compression de 50%

Pour les full horizontales :
- Echelle et taille de l'image : mettre 1600 pour la largeur
- Export as... [...].jpg avec une compression de 50%

Pour les miniatures verticales :
- Echelle et taille de l'image : mettre 600 pour la largeur
- Taille du canevas : 600*400, cliquer sur centrer puis ajuster, puis sur redimmensionner
- Calque > Calque aux dimensions de l'image
- Export as... [...]-th.jpg avec une compression de 50%

Pour les full verticales :
- Echelle et taille de l'image : mettre 1600 pour la hauteur
- Export as... [...].jpg avec une compression de 50%





ALGO

Dans le repertoire en paramètre,
pour tous les fichiers en paramètres avec l'extension *.png ou *.jpg,
	
    Si image horizontal
    Alors

        Créer miniature horizontale :
        - Echelle et taille de l'image : mettre 600 pour la largueur
        - Export as... [...]-th.jpg avec une compression de 50%

        Créer full horizontales :
        - Echelle et taille de l'image : mettre 1600 pour la largeur
        - Export as... [...].jpg avec une compression de 50%

	Sinon

        Créer les miniatures verticales :
        Echelle et taille de l'image : mettre 600 pour la largeur
        Taille du canevas : 600*400, cliquer sur centrer puis ajuster, puis sur redimmensionner
        Calque > Calque aux dimensions de l'image
        Export as... [...]-th.jpg avec une compression de 50%

        Créer full verticales :
        - Echelle et taille de l'image : mettre 1600 pour la hauteur
        - Export as... [...].jpg avec une compression de 50%




WITH ImageMagick on UBUNTU

mkdir original
cp * ./original
mkdir full 
mkdir thumbs 
mkdir tmp1 
mkdir tmp2 
convert *.png ./tmp1/-.jpg 
convert ./tmp1/*.jpg -resize x1600 ./tmp2/-.jpg 
convert ./tmp2/*.jpg -quality 50 ./full/-.jpg 
rm -f ./tmp2/* 
convert ./tmp1/*.jpg -resize 600 ./tmp2/-.jpg 
convert -crop 600x400+0+600 ./tmp2/*.jpg ./thumbs/-.jpg 
rm -f ./tmp1/* 
rm -f ./tmp2/* 
