---
layout: post
published: false
title: 'Title: Lidar est là : profitons-en. Tutoriel QGIS pour lidar HD.'
---

Attendues depuis très longtemps, les données lidar pour le territoire métropolitain français sont enfin disponibles. Chaque élément du terrain ou presque est enregistré en 3D : bâtiments, relief, trait de côte, etc. Le suivi du projet - une moitié du territoire est couverte au moment de rédaction - et le téléchargement des données peuvent être trouvées sur *geoservices.ign.fr* [1][1].

Mais, que sont en réalité ses fameuses données lidar ? Un peu de théorie s'impose en amont du tutoriel pas à pas. L'appareil lidar utilise les faisceaux laser pour obtenir des mesures de distance. Ainsi, des millions de faisceaux sont envoyés depuis un avion, un hélicoptère ou un drone pour restituer finement la topographie ("HD" signifie haute définition). Or, les faisceaux peuvent rebondir de tout type d'obstacle autre que la surface du sol: bâtiments, végétation ou même des oiseaux en vol. S'impose donc la tâche très technique de classification, c'est à dire d'interprétation des signaux de retour en fonction de la nature de cible atteinte. Voici les codes standardisés de classification utilisés pour le format de données .las/.laz :

| Code | Catégorie (classe) |
| 0  | Jamais classé      |
| 1  | Non attribué       |
| 2  | Sol                |
| 3  |  Végétation basse  |
| 4  | Moyenne végétation |
| 5  | Haute végétation   |
| 6  | Bâtiment           |
| 7  | Point bas          |
| 8  | Réservé            |
| 9  | Eau                |
| 10 | Ferroviaire        |
| 11 | Surface routière   |
| etc. |


Il arrive, souvent même, des erreurs de classification ; une haie bizarrement taillée peut être prise pour un bâtiment, un buisson pour un rocher, par exemple. Ceci-dit, je trouve que les classifications fournies avec le lidar HD sont plutôt fiables - à étudier par chacun pour son usage particulier [2][2]. Nous n'allons pas aborder la classification ici - problématique très ardue - il s'agit tout simplement de comprendre que nous avons besoin des **données classifiées** par le prestataire, à la différence des données brutes. Nous comprenons également le besoin de jongler avec plusieurs classes pour récupérer des éléments d’intérêt, ou encore de vérifier les erreurs de classification (éléments omis ou faux positifs, tels les bâtiments fantômes).

## Tutoriel

Le tutoriel suivant présentera la procédure pour le traitement du nuage des points classés, en format .las/.laz dans QGIS. Les données lidar étant extrêmement volumineuses, toute la problématique relève en réalité de la gestion du gros volume (partant des données classifiées). Il faut d'abord choisir les dalles à télécharger. Pour ce faire, nous disposons d'un tableau d'assemblage régulièrement mis au jour.


![2023_lidarhd_1.jpg]({{site.baseurl}}/figures/2023_lidarhd_1.jpg)
Tableau d'assemblage.

Une fois chargé dans QGIS, le tableau d'assemblage permet de récupérer les liens de téléchargement pour les dalles souhaitées. Il suffit de copier ces liens ... que je ne saurais pas faire directement dans QGIS, donc je passe par Excel. Je copie-colle la sélection dans Excel, pour ensuite sélectionner et copier les liens. ATTENTION : Les données lidar sont volumineuses, d'ordre de 5 à 10 Giga-octets par commune, soyez parcimonieux !


![2023_lidarhd_1.jpg]({{site.baseurl}}/figures/2023_lidarhd_2.jpg)
Tableau d'assemblage dans QGIS.

Ensuite, nous allons télécharger les dalles en vrac. De nombreuses solutions existent pour ce faire, je utilise *Simple mass downloader* pour Chrome [3]. Il suffit de coller les liens de téléchargement (*uniquement les liens*), et le tour est joué.



![2023_lidarhd_1.jpg]({{site.baseurl}}/figures/2023_lidarhd_3.jpg)
Simple mass downloader.

Le nuage de points n'est pas très utile pour les traitements SIG, hormis quelques visualisations que certains semblent trouver épatantes. Nous allons donc créer un MNT en format raster. L'algorithme est disponible en QGIS depuis la **version 3.32**.


![2023_lidarhd_1.jpg]({{site.baseurl}}/figures/2023_lidarhd_3b.jpg)
Conversion du nuage de points en raster.

L'outil nous demande, entre autres, la résolution souhaitée et la sélection de classes à prendre en compte. Concernant la résolution, un demi-mètre et à mon sens le maximum de précision justifiable, et un mètre peut-être un bon compromis entre la précision et la maniabilité (à étudier). L'attribut se réfère à la valeur enregistrée ; pour notre cas ce sera l'altitude en z. Autres attributs peuvent être intéressants pour une étude technique de l'acquisition lidar (temps d'acquisition, intensité du faisceau, nombre de reflets, etc.).

L'utilisation d'un filtre est primordiale, nous permettant de choisir la ou les classes d'intérêt : sol, architecture, végétation, etc. Éventuellement, nous pouvons faire des modèles multiples pour comparer l'apport de différentes classes. A ce stade **ne chargez pas les dalles dans QGIS**. Le logiciel doit les traiter une par une  pour la visualisation, ce qui est excessivement long (10 - 15 minutes pour un lot de taille moyenne). Je propose un script en Python pour le traitement direct, en appelant l'outil d'exportation en raster. Le script est téléchargeable à partir du lien [ci-dessus][Téléchargement], pour être chargé dans QGIS via la boite à outils de traitement.


![2023_lidarhd_1.jpg]({{site.baseurl}}/figures/2023_lidarhd_4.jpg)
Chargement d'un script dans le Traitement.

Le plugin est rangé parmi les *Scripts*, section *LandscapeArchaeology*. L’interface est très simple et reprend les paramètres de l’outil QGIS expliqués ci-dessus. Enfin, veuillez prendre en compte le temps nécessaire pour traiter des gros lots, d’ordre de plusieurs heures pour une commune (une minute par dalle +/-).

Une fois la conversion en raster faite, il nous reste à traiter les dalles crées. Pour les jeux de données de taille raisonnable, disons jusqu’à 2 ou 3 giga-octets, il est commode de fusionner les dalles en une seule surface. Sinon, pour les jeux de données plus conséquents, ou bien pour les ordinateurs moins puissants, il nous reste l’option du raster virtuel [4][4].


![2023_lidarhd_1.jpg]({{site.baseurl}}/figures/2023_lidarhd_5.jpg)
Fusion des dalles

ATTENTION : veuillez à renseigner la valeur -9999 comme *NoData*, c’est-à-dire le vide. Nous avons en effet écarté plusieurs catégories (classes) de points – sinon, c’est pas bien fait –, ce qui laissera des vides à l’emplacement, par exemple, de la végétation. L’algorithme QGIS (ou PDAL en réalité) utilise par défaut la valeur -9999 pour marquer les vides.


![2023_lidarhd_1.jpg]({{site.baseurl}}/figures/2023_lidarhd_6.jpg)
Bien renseigner la valeur des vides (NoData).

Alors les trous, il va falloir les combler. L’outil GDAL *Fill nodata* est parfait pour la tâche (à trouver sous le menu raster, ou dans le outils du Traitement). Le MNT est prêt !


![2023_lidarhd_1.jpg]({{site.baseurl}}/figures/2023_lidarhd_7.jpg)

Enfin, nous allons pouvoir nous amuser avec le MNT lidar (Puy-en-Velay) :

![2023_lidarhd_1.jpg]({{site.baseurl}}/figures/2023_lidarhd_8.jpg)

... ou en 3D : 

![2023_lidarhd_1.jpg]({{site.baseurl}}/figures/2023_lidarhd_9.jpg)


Les visualisations ont été faites à l'aide du plugin *Terrain shading* [5][5]. J'aborderai le traitement du MNT dans un post ultérieur (à suivre...).

Bonne continuation !

## Téléchargement 

https://github.com/zoran-cuckovic/QGIS-scripts/ (le dépôt GitHub n'est pas très érgonomique : il faut télécharger l'ensemble du dépôt, ou bien chercher le code brut [*raw*] et enregistrer comme un fichier .py)

## Liens
[1]: https://geoservices.ign.fr/lidarhd
[2]: https://geoservices.ign.fr/documentation/donnees/alti/lidarhd
[3]: https://chromewebstore.google.com/detail/simple-mass-downloader/abdkkegmcbiomijcbdaodaflgehfffed
[4]: https://docs.qgis.org/3.28/fr/docs/training_manual/rasters/data_manipulation.html#basic-fa-create-a-virtual-raster 
[5]: https://landscapearchaeology.org/qgis-terrain-shading/ 