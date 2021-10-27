---
layout: post
title: Analyse thermique en archéologie
published: true
tags:
  - télédétection
---

Ce résumé a été produit pour un projet d’acquisition thermique par drone, mené par l’équipe d’[IntelEspace](http://www.msh-clermont.fr/panel-intelespace) de la Maison des Sciences de l’Homme, Université Clermont Auvergne. Ce petit rapport interne pourrait être utile aux archéologues – et plus largement à tous ceux qu’on a fait croire que la caméra thermique mesure la température du sol. 

## Introduction

A l’instar d’autres méthodes en télédétection et géophysique, l’analyse thermique cherche à relever le contraste entre diverses structures archéologiques et le sédiment géologique. En théorie, ce contraste dépend de deux propriétés thermodynamiques fondamentales : 
1.	Conductivité, qui se rapporte à la propagation de la chaleur dans un matériau et qui mesure la quantité de l’énergie transmise (dans un espace et temps donnés).
2.	Capacité thermique, qui décrit la quantité d’énergie thermique qui peut être emmagasinée dans un matériau, plus précisément la quantité d’énergie requise pour changer sa température. 

… ainsi que de deux propriétés dérivées:
3.	Inertie thermique, ou la résistance de matériau au changement de température.
4.	Diffusivité, ou la vitesse de transmission de la chaleur au sien d’un matériau. 

*Adapté d’après Cool 2018, voir aussi Gaussourgues 1994.*


En pratique, il y a un très grand nombre de facteurs supplémentaires qui nous concernent en archéologie/géophysique. En premier lieu c’est l’humidité du sol (cf. Casana 2017 ; Walker 2020). L’eau a une très forte capacité thermique, et de ce fait emmagasine aussi bien la chaleur que la fraicheur. Or, dans une matrice sédimentologie ces caractéristiques sont très fortement liés à la structure et la taille des alvéoles remplies d’eau : gravier, sable, argile etc. S’ajoute l’effet d’évaporation de l’eau qui tend à rafraichir la température en surface. Ensuite, les capacités thermiques varient selon les roches, ce qui n’est pas seulement liée à la structure moléculaire et cristalline, mais aussi la morphologie (taille, forme, etc. ; voir aussi Cassinis et al. 1984). 

On rencontre couramment un malentendu concernant l’analyse thermique, du moins dans la littérature archéologique, qui provient de la confusion entre la température de surface et l’émission thermique. La méthode thermique à distance, sans contact avec le matériau, ne mesure pas directement la température, mais seulement l’émission thermique (Gaussorgues 1994). Et ça change tout !

![](/figures/2021-10-image1.gif) ![](/figures/2021-10-image2.png)
*Figure 1. La loi de Lambert : l’émission varie selon l’angle d’observation. Plus exactement, la quantité émise égale la superficie des coins colorés, pour une surface plane dA.*

La radiation thermique est, ainsi, affectée par l’inclinaison de la superficie mesurée, donc par la microtopographie. Une plaque chauffante, par exemple, émet bien plus de chaleur dans le sens perpendiculaire, directement en face, que sur le côté – ce rapport entre l’inclinaison et la quantité émise est décrit par la loi de Lambert. [Il s’agit d’un principe général, en réalité la loi de Lambert ne s’applique pas de même manière à tous les matériaux ou surfaces : Gaussorgues 1994, 45.] Ainsi, pour une température homogène d’une surface irrégulière, nous obtiendrons des mesures différentes en fonction des orientations de ses facettes. Remarquons que la réflexion de la radiation solaire est affectée de même manière par l’inclinaison de la surface, elle est la plus forte dans le sens perpendiculaire de la surface. Ce principe n’est pas valable seulement pour les matériaux très réfléchissants, telle l’eau ou la glace. 


![](/figures/2021-10-image3.gif) 
*Figure 2. Emission des ondes thermiques : noter la contribution des couches profondes (Xiao et al. 2020).*

La question particulièrement intéressante concerne la profondeur depuis laquelle provient le signal thermique. L’émission thermique ne doit pas être pensée comme un échange ayant lieu à la surface d’un matériau, mais comme une contribution simultanée des émissions provenant de toutes ses strates. Ceci dit, en traversant le matériau, la plupart de ces émissions de profondeur seront immédiatement réabsorbées, seule une toute petite quantité s’échappera des couches les moins profondes. Sachant que chaque matériau à une tendance spécifique d’absorption et d’émission thermique, l’émission venant de la profondeur aura une signature thermique bien différente par rapport à celle de la surface (en principe, les longueurs d’onde bien élargies : Fig. 2). Quant à l’émission thermique du sol, il se peut que ce phénomène ne concerne qu’une dizaine de centimètres en épaisseur – je n’ai pas trouvé de discussions dans ce sens.  

La question du caractère ondulatoire des signaux thermiques invite ainsi à repenser certaines conceptions fondamentales de l’acquisition thermique. La matrice sédimentologie est presque invariablement représentée dans les travaux scientifiques comme un matériau avec les propriétés thermiques homogènes (Tabaggh 1977 ; Pérriset & Tabbagh 1981). Cela peut paraître acceptable d’une première vue, en prenant en compte la variabilité de ces propriétés selon le taux d’humidité. Or, il s’agit d’une importante simplification puisque ce type de matrice est en réalité composé d’une multitude d’émetteurs : à côté de la transmission de chaleur à l’intérieur du matériau, nous avons également l’émission des ondes thermiques vers l’extérieur. Chaque structure cristalline et moléculaire sera donc caractérisée par son propre spectre thermique. Qui plus est, la morphologie des composantes sédimentologies, ou même leur organisation (inclinées, alignées, désordonnées) peuvent (devraient ?) influencer le résultat. Il est ainsi très difficile à modéliser la combinaison de ces effets au sein d’un sédiment hétérogène. Je n’ai pas vu de discussions dans ce sens dans la littérature archéologique. 

L’incompréhension de la radiation thermique a une incidence particulière sur la pratique d’acquisition thermique en archéologie. Puisque l’on part du principe que la radiation est émise par la superficie du sol, c’est-à-dire en prenant en compte seule la transmission thermique entre le sol et l’air, les archéologues tendent à favoriser les acquisitions nocturnes, pour diminuer l’influence du réchauffement de la surface (Casana et al. 2017 ; infra). Or, rappelons que la réflexion thermique solaire suit les mêmes principes que l’émission thermique du sol même – en théorie du moins ! – , elle n’est donc pas nécessairement destinée à brouiller le signal provenant du sol. Qui plus est, des différences intéressantes entre les spectres thermiques de l’énergie reflétée de la superficie et celle émise de la profondeur peuvent se manifester durant la journée : le sujet reste à explorer pour l’archéologie (mais voir Cremona et al. 2020 : infra).   

## Approches archéologiques

L’analyse thermique en archéologie est une approche déployée essentiellement ad hoc et de manière expérimentale, le plus souvent en parallèle avec d’autres méthodes. La mise en place de la méthode est conditionnée par la technologie disponible plutôt que par des questions scientifiques. Ainsi, on ne cherche pas de généraliser les solutions méthodologiques et on ne développe pas des discussions au-delà questions techniques. Néanmoins, ce pragmatisme peut être justifié par des résultats assez modestes jusqu’au présent – les archéologues sont toujours en quête d’une approche par l’acquisition thermique qui mériterait un investissement plus conséquent. 

Les premiers travaux sur la télédétection des vestiges archéologiques par la méthode thermique aéroportée ont été publiés par A. Tabagh dans les années 70 et 80. Très techniques et assez difficiles à comprendre sans un bon niveau en mathématiques, ses articles sont aujourd’hui une référence obligatoire (sans qu’ils soient effectivement lus).

Après les premiers travaux de Tabbagh, la méthode thermique aéroportée a été peu utilisée jusqu’aux années 1990 – 2000, époque qui a vu le développement de la gamme des capteurs Daedalus. Parmi eux, Daedalus Thematic Mapper propose 11 bandes, dont plusieurs bandes en infrarouge et une thermique. Pour l’acquisition dans les Hébrides écossais, publiée par Winterbottom & Dawson (2005), l’altitude du vol mesurait 750 m et la méthode thermique était utilisée en complément d’acquisition dans les bandes visibles. Le résultat était plutôt moyen, sans un apport dramatique d’information dans la bande thermique. Un meilleur résultat par la même approche a été obtenu par Challis et al. (2009). Or, leur intérêt portait sur la géologie des vallées alluviales plutôt qu’à l’archéologie. Les divers sédiments alluviaux produisent un très bon contraste en thermique, aussi bien que dans les bandes visibles. 

Une approche inhabituelle a été expérimentée par Kwamme et al. (2008) sur un site dans la prairie américaine. Son équipe a embraqué une caméra thermique (Raytheon) sur un parapente. Avec une altitude du vol de 300 – 500 m ils ont obtenu un résultat de très bonne qualité. Cependant, il faut savoir que les sites de prairie sont souvent visibles en microtopographie, et c’est effectivement le cas ici. En plus, les dépressions à l’emplacement des structures archéologiques captent bien l’humidité et donc se distinguent bien sur les images thermiques.   

Une nouvelle ère dans l’application de la méthode thermique a été inaugurée avec la gamme des capteurs FLIR, fabriqués pour les drones à partir des années 2010. Grace à la compétitivité accrue des publications scientifique de nos jours, toute expérience avec le FLIR semble digne d’une publication internationale (cf. l’Annexe). 

Encore une fois, les meilleurs résultats ont été obtenus pour la prairie américaine (McLeester et al. 2018). Le site étudié par ces chercheures est dépourvu d’anomalies topographiques, mais le faible enfouillassent des vestiges (absence d’agriculture mécanisé), le sédiment très fin et homogène et, vraisemblablement, un captage d’eau dans les structures archéologiques, sont autant de facteurs qui ont dû contribuer au bon résultat.

Un de très rares archéologues spécialisés en thermique est Jesse Casana (2017). Or, ses acquisitions dans le milieu rocailleux du sud des Etats Unis n’ont pas livré des résultats spectaculaires, malgré une attention particulière aux paramètres du vol (multiples acquisitions dans la journée : Casana et al. 2014). La sècheresse et l’hétérogénéité de la matrice (roches, cailloutis) n’ont certainement pas aidé. Cassana obtient des meilleurs résultats pour les acquisitions matinales, juste avant le lever du soleil, et préconise de fait les vols nocturnes/matinaux.  

Un milieu encore plus rocailleux, mais aussi très humide, a été exploré par Walker et al. (2020) pour l’Arctique canadien. Ils s’intéressent aux sites inuits qui demeurent visibles en surface, mais l’imagerie produite est difficile à interpréter à cause de la disposition erratique des blocs granitiques. Le résultat est visiblement corrélé avec l’humidité capté dans les structures archéologiques. Les grand blocs granitiques (0,5 à 2 m) apparaissent également assez clairement dans la thermographie, à condition d’être faiblement enfouis. L’horaire optimal pour l’acquisition se situait juste après le coucher du soleil. 

Plus récemment, Calastrenc et al. (2020) ont publié une étude thermographique des sites pastoraux dans le Pyrénées. Bien visibles en microrelief, sous forme de tas de déblais caillouteux, ces sites le sont aussi dans les images thermiques (rappelons la corrélation entre l’inclinaison de surface et le taux de radiation thermique : supra).

Le choix de **l’horaire d’acquisition** est sans doute particulièrement important pour l’analyse thermique. Pour éviter le reflet de la radiation solaire, on préconise le plus souvent l’acquisition nocturne (Casana et al. 2017 ; Cool 2018). Dans le sud des Etats-Unis, le résultat optimal est ainsi obtenu au petit matin (Casana et al. 2014), et dans l’arctique plutôt au coucher du soleil (Walker 2020). Or, comme je l’ai relevé plus haut, l’enjeu specifique de la méthode thermique consiste en enregistrement du signal provenant depuis la profondeur – les contrastes intéressants peuvent ainsi se révéler à divers horaires. En effet, pour Carmona et al. (2020), les meilleurs résultats ont été obtenus pour l’acquisition du midi. Cette dernière recherche, faite en Espagne au mois du mai, a bien ressorti une structure quadrilatérale, ainsi que des supposés murs du rempart protohistorique (Figure en bas). La clé du succès de leur approche est dans le timing : ils ont ciblé le jour après une pluie printanière. Ceci dit, les acquisitions matinale et vespérale fournissent des informations complémentaires : les contraste évolue au fil du temps (Fig. en bas).

![](/figures/2021-10-image4.png) 
*Figure 3. Carmona et al. 2020 : bon résultat pour l’acquisition de midi.*

Le **traitement des images thermiques** reste pour l’essentiel basique : calibration, rectification et l’examen à l’œil. Certains, cependant, sont allés plus loin. Calastrenc et al. (2020) ont cherché à extraire des « profils thermiques » qui affichent la variation des valeurs enregistrées le long d’un axe choisi. Voir aussi Cassinis et al. 1984 pour la même solution. Casana et al. (2017) se sont attaqués à une question très importante : le filtrage de végétation dans les images thermiques. Pour ce faire, ils se sont appuyés à un appareil photo modifié pour l’enregistrement dans la fréquence IR (un Canon DSLR), et au NDVI ressorti de ces images. Ensuite, ils ont soustrait les valeurs NDVI des valeurs thermiques, partant du principe que le NDVI représente la composante biologique du signal thermique. D’autres chercheurs, travaillant sur les données multispectrales se sont naturellement tournées vers l’analyse PCA (Challis et al. 2009 ; Carmona et al. 2020). Une approche intéressante en analyse thermique a été publié par Danese et al. (2009). Travaillant sur l’analyse architecturale, avec une camera fixe, ils ont combiné des multiples acquisitions dans un jeux de données multi-temporel et ensuite utilisé les réseaux de neurones pour l’analyser (« SOM neural networks »). 

L’utilisation des **capteurs thermiques** au sol est très rare en archéologie et je n’ai pas trouvé d’exemples pour un couplage avec l’acquisition aéroportée. Perriset et Tabbagh (1981) mentionnent des prospections thermiques qui semblent avoir été faites en utilisant la caméra thermique en marchant, mais ce n’est pas clair dans le texte (idem, Fig. 8). Des expériences avec des capteurs sous-sol ont été conduites dans les années 80 par Bellerby et al. (1990)  . La profondeur choisie était de 20 cm, mais leur idée de cartographier un site à l’aide des mesures thermiques disposées dans un carroyage était trop fastidieuse pour pouvoir donner de résultats suffisamment précis. Mori et al. (1990) ont testé des probes thermiques insérées à 50 cm de profondeur pour l’étude des grandes tombes princières au Japon. Avec seulement quatre probes, ils n’ont pas pu détecter grande chose, mais les variations du gradient thermique se sont quand même montrées très intéressantes. La température a été enregistré toutes les 10 minutes pendent 38 heures, nous fournissant ainsi un aperçu de ce qui se passe en sous-sol. En effet la sonde 3, positionnée au-dessus la tombe présumée (détectée par d’autres approches) affiche une nette anomalie du gradient (une inertie, je dirais : Figure en bas).

![](/figures/2021-10-image5.png) 
*Figure 4. Evolution des températures à 50cm de profondeur, sur un site funéraire japonais. Les courbes représentent quatre sondes thermiques et la température atmosphérique (Mori et al. 1999).*


## Bibliographie

Bellerby T.J. and M. Noel 1990 : A Thermal Method for Archaeological Prospection: Preliminary Investigations. Archaeometry 32, 2 (1990). 191-203.

Benner & Brodkey 1984: Underground Detection Using Differential Heat Analysis. Archaeometry 26, 1 (1984), 21 -36.

Calastrenc F. Baleux, N. Poirier et C. Rendu 2020 : Thermographie aéroportée par drone. Nouvelle procédure pour la détection archéologique en haute montagne. ArcheoSciences 44(1).

Carmona et al. 2020 : Assessing the potential of multispectral and thermal UAV imagery from archaeological sites. A case study from the Iron Age hillfort of Villasviejas del Tamuja (Cáceres, Spain). Journal of Archaeological Science: Reports 31

Casana et al. 2014 : Archaeological aerial thermography: a case study at the Chaco-era Blue J community, New Mexico. Journal of Archaeological Science 45

Casana, J., A. Wiewel, A. Cool, A. C. Hill, K. D. Fisher, E. J. Laugier 2017 : Archaeological Aerial Thermography in Theory and Practice. Advances in Archaeological Practice 5(4).

Cassinis, R., N. Tosi , G. M. Lechi , P. A. Brivio , E. Zilioli & A. Marini 1984: Thermal inertia of rocks—an HCMM experiment on Sardinia, Italy. International Journal of Remote Sensing, 5(1), 79-94.

Challis, K., M. Kincey, A.J. Howard 2009 : Airborne Remote Sensing of Valley Floor Geoarchaeology using Daedalus ATM and CASI. Archaeol. Prospect. 16, 17–33

Cool, A. 2018 : Thermography. The Encyclopedia of Archaeological Sciences (S. L. López Varela ed.)

Danese, M., U. Demšar, N. Masini and M. Charlton 2010: Investigating Material Decay of Historic Buildings Using Visual Analytics with Multi‐Temporal Infrared Thermographic Data. Archaeometry 52 (3).

Gaussorgues, G. 1994 : Infrared Thermograph. Springer. [Original: La thermographie infrarouge : principes, technologies, applications, 1989 : Lavoisier]

James,j K., C. J. Nichol, T. Wade, D. Cowley, S. Gibson Poole, A. Gray and J. Gillespie 2020 : Thermal and Multispectral Remote Sensing for the Detection and Analysis of Archaeologically Induced Crop Stress at a UK Site. Drones 4.

Kvamme, K. 2008 : Archaeological Prospecting at the Double Ditch State Historic Site, North Dakota, USA. Archaeol. Prospect. 15, 62–79

McLeester M., J. Casana, M. R. Schurra, A. Ch. Hill, J. H. Wheeler III 2018 : Detecting prehistoric landscape features using thermal, multispectral, and historical imagery analysis at Midewin National Tallgrass Prairie, Illinois. Journal of Archaeological Science: Reports, 21

Mori, M., H. Kamei, M. Nakai and H. Kudo 1999: High-density Resistivity Survey and Experimental Measurement of subsurface Temperatures on Hirui-Otsuka Mounded Tomb in Ogaki, Japan. Archaeol. Prospect. 6. 

Pérriset M. C. and A. Tabbagh 1981 : Interpretation of thermal prospection on bare soils. Archaeometry 23 (2), 169-187.

Tabbagh, A. 1977 : Sur la determination du moment de mesure favorable et l'intérprétation des résultats en prospection thermique archéologique. Annales de Géophysique 33. 

Thomas, H. 2017 : Some like it hot: The impact of next generation FLIR Systems thermal cameras on archaeological thermography. Archaeological Prospection. 2017; 1–7. 

Winterbottom, S. J. and T. Dawson 2005: Airborne Multi-spectral Prospection for Buried Archaeology in Mobile Sand Dominated Systems. Archaeol. Prospect. 12, 205–219.

Walker, S. 2020 : Low-altitude aerial thermography for the archaeological investigation of arctic landscapes. Journal of Archaeological Science 117.

Xiao, Y.,  C. Wan, A. Shahsafi, J. Salman and M. A. Kats, 2020: Depth Thermography: Noninvasive 3D Temperature Profiling Using Infrared Thermal Emission. ACS Photonics 2020, 7, 853−860

## Annexe

| Article                    | Engin & hauteur                         | Capteur                                                 | Milieu                                                | Archéologie                                            | Temps                                     | Traitement                                                           | Commentaire                                                                                                                                                                                         |
| -------------------------- | ------------------------------------------ | ------------------------------------------------------- | ----------------------------------------------------- | ------------------------------------------------------ | ----------------------------------------- | -------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Tabbagh années 70          | \> 300 m ( ?)                              | Très ancien                                             | FR, Bassin parisien : marno-calcaire, gravier         | Sous la terre arable, remplissages des fossés          | Mars, decembre 9-11h                      | ( ?)                                                                 |                                                                                                                                                                                                     |
| Winterbottom & Dawson 2005 | Avion, 750 m                               | Daedalus Thematic Mapper (MS, 11 bands)                 | Ecosse : sableux, avec des cailloux                   | En partie sous-sol, structures en relief (cairns etc.) | Avril, midi, lever du soleil              | Aucun                                                                | Resultat : moyen, combinaison thermal – MS                                                                                                                                                          |
| Kvamme 2008                | Parapente, 300-500 m                       | caméra manuelle Raytheon                                | USA, prairie (sédiment fin ?)                         | Enfouillée & affleurante (dépressions en surface)      | « le soir »                               | ?                                                                    | Résultat : excellent, mais seulement pour les structures peu profondes/affleurantes                                                                                                                 |
| Casana et al. 2014         | Drone Cinestar 8, 70 m (lentille 19 mm)    | FLIR Tau II LWIR (sans refroidissement)                 | USA, N. Mexico : colluvion/alluvion, très caillouteux | Affleurante, structures en pierre                      | Juin, 5 – 10h (5 vols)                    | Aucun (mosaïque)                                                     | Résultat : moyen Optimum : 5h20 de matin                                                                                                                                                            |
| Casana et al. 2017 a)      | Drone, sans précisions                     | ?                                                       | USA Arkansas, prairie                                 | Affleurante ( ??)                                      | Mars, 6h45 (avant l’aube)                 | Usage de NIR (Canon reflex) pour NDVI et l’élimination de végétation | Résultat : moyen. Usage du NDVI est novateur.                                                                                                                                                       |
| Walker 2020                | Drone Phantom 4 pro, 20 m (sic)            | FLIR Vue Pro                                            | Arctique, très caillouteux, sol peu formé             | Affleurante, structures bien visibles en surface       | Juillet – Aout, multiples vols & horaires | Aucun (mosaïque)                                                     | Résultat : plutôt bien. Optimum : juste après le coucher du sol. Le meilleur contraste avec le ciel couvert (pas de réfraction). Humidité – cruciale. |
| McLeester et al. 2018 | Drone Phantom 3, 50 m | FLIR Vue Pro | USA, prairie (sédiment très fin, j&#39;imagine ) | Enfouillée, mais à faible profondeur | Septembre, 12h, 14h40, 17h | Aucun (mosaïque)Comparaison visuelle | Résultat : plutôt bien |
| Thomas 2017 | Phantom 2 | FLIR Vue Pro | Grèce, caillouteux | Enfouillée &amp; affleurante | Août-septembre, 11h – 19h | N/A | Résultat : moyenDétection des grandes cavités |
| James 2020 | Vulcan optocopter, DJI Matrice 100,60 m | FLIR Vue Pro-R + Micasense Red-edge MS + Parrot Sequoia | Ecosse, terre labourée | sous la terre arable, remplissages des fossés | May/Juin, non rens. | Pix4D radiometric calibration of MS | Résultat: nul (soucies d&#39;analyse !) |
| Carmona et al. 2020 | eBee by SenseFly, 75 m (thermique) | Parrot Sequoia, ThermoMAP (thermique) | Espagne : caillouteux | enfouillée | Mai : matin, midi, soir | Traitement d&#39;image pour le MS (NDVI et compagnie…) | Ils ont ciblé des jours après la pluie !Thermique : excellent , « clarity of the anomalies captured in the noon&quot; |
| Challis et al. 2009 | Avion, altitude pas specifiée | Daedalus MS (11 bands)CASI (hyperspectral) | Angleterre, alluvium | Géologie, pas d&#39;archéo | PCA du MS + analyse standard | 95% d&#39;info dans le « middle infrared » : pour la géole, mais aussi pour l&#39;archéo.|
| Calastrenc et al. 2020 | Drone , 30 m | Flir T620 | Pyrénées, rocheux | Affleurante, très faiblement enfouille | Septembre-Octobre, midi-15h30 | Traitement MNT (profils, discrétisation) | Resultat : bon, mais l&#39;archéo est en surface ( !)Position du capteur oblique – meilleur résultat |
