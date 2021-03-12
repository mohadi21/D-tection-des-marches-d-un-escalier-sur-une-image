# D-tection-des-marches-d-un-escalier-sur-une-image

L'objectif de ce projet consiste à établir et mettre en oeuvre un algorithme permettant
l'extraction et le calcul du nombre de marches dans les images contenant un escalier.

L'étape de calcul du nombre d'étapes comporte deux phases principales. La première
consiste à prétraiter l'image pour détecter les bords des marches. La deuxième étape vise à localiser
et étudier les contours sur l'image résultant de la première étape à l'aide de critères géométriques
(proximité, parallélisme, ...) des différents éléments susceptibles d'être des marches.

Afin de préparer l’étape de calcule du nombre de marches, l’image couleur d’entrée est dans
un premier temps convertie en image en niveau de gris. Un rehaussement des contrastes peut
également être appliqué afin de renforcer la distinction entre les objets clairs et foncés.

Les marches possèdent diverses caractéristiques qui leur permettent d’être différenciés des
autres éléments présents dans l’image. L’une d’elles est la présence d’un fort contraste entre une
marche et contremarches. Dès lors, afin de mettre en évidence ces zones de fort contraste, un
filtrage moyenne et gaussien sont appliquées.
Un seuil global de l'image avec la fonction adaptiveThreshold de la bibliothèque OpenCV
est appliqué afin de binariser l'image, cette fonction détermine automatiquement le seuil pour un
pixel en fonction d'une petite région autour de lui. Nous obtenons donc des seuils différents pour
différentes régions d'une même image, ce qui donne de meilleurs résultats pour des images avec un
éclairage variable.

Calcule du nombre de marche
Le calcule de nombre de marches de l’image pré-traitée se déroulent en 2 étapes. Dans un premier
temps les lignes droites présentes dans l’image binaire sont calculées en utilisant la méthode de
Hough. Une première fonction de filtrage est appliquée sur les lignes. En effet, les marches
composantes un escalier sont perpendiculaires, et la marche qui est en bas à des dimensions plus
grand que celle en haut de plus si l’image est prise depuis le sol les marches seront horizontales.
Ainsi la fonction appliquée tient compte de la perpendicularité des lignes avec un seuil d’erreurs qui
représentait par un angle.

A l’issue de ce premier filtrage, un grand nombre de ligne ont pu être retirées, considérées comme
ne pouvant être une partie d’une marche.
Dès lors le premier filtrage est appliqué, une deuxième fonction de filtrage est appliquée sur les
composantes restantes. Plusieurs lignes horizontales peuvent représenter la même marche, cette
fonction permet donc de regrouper les lignes qui ont une distance inférieure à un seuil, comme les
lignes des marches qui sont aux plus hautes sont séparées par une distance court, donc ce seuil sera
réduit à chaque itération.

Enfin, une troisième fonction est appliquée sur les composantes restantes, deux lignes peuvent soit
correspondre à une marche ou à une contremarche, l’objectif de cette fonction est de calculer le
nombre de marche.
