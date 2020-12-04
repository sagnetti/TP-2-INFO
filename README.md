# TP-2-INFO

Lien Github avec code :

•	Essai via filtres Gaussien (IN 2)
Via  Librairie skimage.filters.rank import mean, median  et cv2 import medianBlur on va insérer des filtres Gausien, uniform et impuls à notre image. Dans ce cas-ci aucune modification à l’œil humain est visible pour l’Impuls noise.

•	Essai via Contrast  (IN 3)
Via Librairie PIL import ImageEnhance (contrast) on améliore la qualité de l’image mais n’influence pas l’entièreté des couleurs.

•	Essai Gamma  (IN 4)
Via from PIL import ImageEnhance ImageFilter et définit par adjust_gamma(image, gamma=1) en jouant avec la table ( np.array ) on obtient une amélioration mais assez intense.
On doit donc simultanément jouer sur chaque pixels des RGB.
Retour sur image via le fonction cv2 LUT 

CONSTRUCTION DE L’IMAGE( IN 6 )

•	Étape 1 : Configuration des paramètres de l’image

Initialisation de 3 np array qui modelise les 3 channels de l’image RGB ainsi que taille de l’image.

Insertion/Definitions des paramètres permettant de « jouer » avec les gammas, saturation contrast luminosité et netteté de l’image en simultané aux étapes suivantes. 

•	Étape 2 : comptage des pixels sur chaque channel

L’image est parcourue en associant un triplet RGB à chaque point (i,j) de l’image.  (b, g, r) = img[i, j]   
Chaque pixel est stoké dans un channels via la variable par iteration de (i,j) ;  ‘count_b ; count_g ; count_r’ va permettre de comptabiliser le nombre de fois la valeur du pixel dans l’image où la fonction array les définit pour chaque channels. 

les variables ( count_b[index_b] = count_b[index_b] + 1. & count_b =  count_b / total  ) vont permettre le calcul des probabilités.
•	Étape 3 :  comptage cumulatif des probabilités

Somme cumulée de l’array jusquà la i-eme iteration  sur chaque channels en les stockant dans la variable sum 
“sum_b = sum_g = sum_r = float(0)” ( ‘sum_b += count_b[i]’)

•	Etape 4 :  construction de nouvelle Map
La variable ‘count_’ va reprendre la somme cumulée pour chaque  i et les placer dans une array de type uint16  mapl_b = np.uint16(255 * count_b) 

•	Etape 5 :  nouvelle tabelle array et construction de la nouvelle image 
Nouvelle Map composée des arrays obtenues et exprimée en channels  dst = np.zeros((height, width, 3), np.uint8)
Un triplet est attribué à chaque point de la Map où ces valeurs sont définies par b = mapl_b[b] ; g = mapl_g[g] ; r = mapl_r[r] pour chaque position. Chaque channels (RGB) remplit la nouvelle Map à chaque position ce qui donne la nouvelle image.

•	Supplément accentuation de couleurs

-	Effet dégradé de couleurs  en (0 ; 50)  
-	Effet de mise en évidence des couleurs (grayscaled, 256, cv2.ADAPTIVE_THRESH_GAUSSIAN_C, cv2.THRESH_BINARY, 115, 1)


Sources utilisées :

https://note.nkmk.me/en/python-pillow-putalpha/
https://f-legrand.fr/scidoc/srcdoc/image/extraction/regions/regions-pdf.pdf
https://www.programmersought.com/article/61683872029/ 
https://www.programmersought.com/article/61683872029/ 
http://datahacker.rs/opencv-pixel-intensity-change-and-watermark/



