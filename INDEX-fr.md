In English: [INDEX.md](/INDEX.md)

## Introduction

Les données accessibles via ce référentiel GitHub ont été collectées à l'aide du processus décrit dans cet article de blog Engineering at Meta :



* [A new way to survey potential fiber routes — without access to paved roads](https://engineering.fb.com/2022/05/01/connectivity/fiber-routes/)

Ce riche ensemble de données comprend les résultats d'une étude environnementale, d'une étude de construction et d'une étude géotechnique (spectromètre gamma + pénétromètre) couvrant 5 898 km de routes de fibre optique potentielles ou d'autres infrastructures enterrées.


## Conditions préalables



* Un PC avec Windows, macOS ou Linux
* Espace disque suffisant (~ 200 Go) pour installer le logiciel QGIS et stocker les données d'enquête
* Installez la version actuelle de la version à long terme de QGIS (**évitez la dernière version**)
    * [https://qgis.org/fr/site/forusers/download.html](https://qgis.org/fr/site/forusers/download.html)
        * Windows : 1,0 Go de téléchargement compressé / 2,3 Go installés
        * macOS : 1,2 Go de téléchargement compressé / 3,2 Go installés
* Familiarité avec l'utilisation de QGIS; d'excellentes ressources de formation :
    * [https://docs.qgis.org/3.22/fr/docs/gentle_gis_introduction/index.html](https://docs.qgis.org/3.22/fr/docs/gentle_gis_introduction/index.html)
    * [https://docs.qgis.org/3.22/fr/docs/training_manual/index.html](https://docs.qgis.org/3.22/fr/docs/training_manual/index.html)
    * [https://github.com/school-of-data/GIS-curriculum](https://github.com/school-of-data/GIS-curriculum)


## Organisation des données d'enquête


### Indicatifs de ville

Les données sont d'abord organisées par segment InterCity ou marché Metro :



* [FB_OTNx_CD_Consolidated_Project 20220712.png](https://github.com/facebookmicrosites/DRC_Infra_Survey_2020-21/blob/main/Reference/FB_OTNx_CD_Consolidated_Project%2020220712.png) : carte d'ensemble
* [FB_OTNx_DRC_Route_Survey_List_20210420-GitHub_Open_Source-End_Points.csv](https://github.com/facebookmicrosites/DRC_Infra_Survey_2020-21/blob/main/Reference/FB_OTNx_DRC_Route_Survey_List_20210420-GitHub_Open_Source-End_Points.csv) : descriptions des emplacements des points finaux à 3 chiffres utilisés dans l'onglet Liste des routes et dans les fichiers de données de topographie
* [FB_OTNx_DRC_Route_Survey_List_20210420-GitHub_Open_Source-Route_List.csv](https://github.com/facebookmicrosites/DRC_Infra_Survey_2020-21/blob/main/Reference/FB_OTNx_DRC_Route_Survey_List_20210420-GitHub_Open_Source-Route_List.csv) : InterCity segment A-ends et Z-ends (ou noms de Métro)


### Structure des dossiers

Les fichiers de données topographiques sont organisés en dossiers comme suit :



* _Env_survey:_ rrésultats de l'activité d'enquête environnementale
    * _1_Inhabited_area_crossing:_ hameau, village, ville, ville
    * _2_Gardening_crossing:_ activité agricole
    * _3_Forest_crossing:_ buissons, arbre; plus dense, moins dense
    * _4_Sacred_area_crossing:_ emples, cimetières, tombeaux, monuments
    * _5_Safety_risk_zones:_ mine dans la sous sol, eboulement, zones de milices (ces risques sont de nature transitoire, donc ces données sont incomplètes par leur nature même)
    * _6_Other_obstacles_crossing:_ montagne, coline, réseau de télécommunication tiers
    * _7_Manual_trenching_area:_ routes étroites, routes impraticables pendant la saison des pluies
    * _8_Added_value_information:_ sites télécoms, stations-service, poteaux et pylônes électriques
    * _9_Route_choice:_ chemin recommandé basé sur les observations environnementales
    * _10_Env_survey_photos:_ couche liée aux photos des observations Env_survey
* _Gap_observations:_ zones où un ou plusieurs types de données topographiques (Env_survey, Geotech_survey, Route_survey, etc.) n'ont pas pu être collectés
* _Geotech_survey:_ les résultats de l'activité d'étude géotechnique ; les données ne sont pas disponibles pour les enquêtes Metro
    * _Raw_data_
        * _Penetro_
            * _pda:_ Données brutes du pénétromètre capturées par Sol Solution [PANDA](https://www.sol-solution.com/en/our-materials/panda-en/) pénétromètres à cône dynamique à énergie variable
        * _Spectro_
            * _json:_ Données brutes du spectromètre gamma capturées par le système de détection de rayonnement Medusa Radiometrics [MS-2000](https://the.medusa.institute/pages/viewpage.action?pageId=3932225)
    * _Soil_type:_ Résultats de la combinaison des données du pénétromètre et du spectromètre gamma pour déterminer et estimer la densité des solides ; données organisées en bandes de densité décrites dans : [FB_OTNx_DRC_Route_Survey_Soil_Types_20210420-GitHub_Open_Source.csv](https://github.com/facebookmicrosites/DRC_Infra_Survey_2020-21/blob/main/Reference/FB_OTNx_DRC_Route_Survey_Soil_Types_20210420-GitHub_Open_Source.csv)
* _Initial_design:_ conception d'itinéraire de bureau originale
* _Route_survey:_ résultats de l'activité d'enquête sur la construction
    * _1_Route_obstacles_crossing:_ divers obstacles de construction qui doivent être franchis tels que : pont, érosion, gouttière, voie ferrée, rivière, route, marécage ou autre type d'obstacle
    * _2_Telecom_sites:_ sites de pylônes de réseau mobile observés lors de l'enquête
    * _3_Physical_FO_route:_ chemin recommandé basé sur les observations Route_survey
    * _4_Route_waypoints:_ enquêter sur les waypoints de la ligne de course (changements de cap)
    * _5_Route_survey_photos:_ couche liée aux photos des observations Route_survey
* _.qgs file:_ un fichier de projet QGIS pour ce segment de route lié aux données dans la structure de dossiers

Une ventilation plus détaillée du contenu Env_survey et Route_survey peut être trouvée dans ce fichier :



* [FB_OTNx_CD_Layers_SIG_with_Color_Charter_V4_20201003-No_Colors.xlsx](https://github.com/facebookmicrosites/DRC_Infra_Survey_2020-21/blob/main/Reference/FB_OTNx_CD_Layers_SIG_with_Color_Charter_V4_20201003-No_Colors.xlsx) (télécharger le fichier depuis GitHub pour voir)


### Instructions

Après avoir téléchargé le fichier .zip pour un segment InterCity ou un marché Metro, décompressez (décompressez) le fichier pour révéler un dossier avec des sous-dossiers contenant des fichiers de données d'enquête. Le projet QGIS (fichier .qgs) sera à la racine de ce dossier. Cliquez simplement sur le fichier .qgs et il s'ouvrira dans QGIS. Selon la quantité de données pour le segment InterCity ou le marché Metro, le fichier peut prendre 5 à 10 secondes pour s'ouvrir.

**QGIS n'intègre pas les données SIG dans le fichier .qgs.** Au lieu de cela, le fichier .qgs stocke le chemin vers les fichiers de données SIG, ainsi les données doivent rester au même emplacement par rapport au projet .qgs. L'intégralité du segment InterCity ou du dossier Metro market peut être déplacé vers un autre emplacement sur votre disque dur, mais gardez à l'esprit ce qui suit :



* Ne déplacez PAS un fichier .qgs hors de son dossier ou vous casserez le fichier .qgs.
* Ne réorganisez PAS les sous-dossiers ou les fichiers d'un segment principal InterCity ou d'un dossier de marché Metro ou vous casserez le fichier .qgs.
* Ne renommez PAS les sous-dossiers ou les fichiers ou vous casserez le fichier .qgs.


## Utilisation de QGIS pour afficher les données d'enquête

Après avoir ouvert un fichier .qgs, il y a de fortes chances que vous ne voyiez rien qui ressemble à une conception d'itinéraire. Pour recentrer la carte QGIS sur les données :



* Localisez le segment InterCity ou le nom du marché Metro dans le panneau Calques (par défaut, ce panneau est situé sur le côté gauche de l'écran QGIS).
* Faites un clic droit sur ce nom et sélectionnez "Zoom sur le groupe".

Ce qui ressemble à un segment InterCity ou à un nom de marché Metro est en fait un groupe (semblable à un dossier) contenant des liens vers les données de ce segment InterCity ou de ce marché Metro. Cliquer sur un carat (>, v) à gauche des éléments étiquetés dans le panneau Calques révélera ou masquera les éléments de ce groupe. Notez qu'il existe des groupes pour _Env_survey_, _Route_survey_, etc. Les données du fichier .qgs sont organisées de la même manière que dans son fichier .zip décompressé (voir la section **[Folder Structure](#folder-structure)** ci-dessus).

Pour afficher _10_Env_survey_photos_ ou _5_Route_survey_photos_ :



* Assurez-vous que le bouton "Afficher les conseils sur la carte" est cliqué. Vous trouverez ce contrôle dans la barre d'outils en haut de l'écran QGIS (c'est une icône jaune qui ressemble à une bulle de discussion avec un point vert à sa base).
* Cliquez sur l'une des couches de photos, puis sur la vue principale de la carte, passez votre souris sur une icône rouge (_10_Env_survey_photos_) ou marron (_5_Route_survey_photos_) pour faire apparaître la photo associée.


## Téléchargements de données d'enquête

Les données de l'enquête sont organisées en trois (3) phases totalisant 188,4GB. La majorité du nombre de fichiers et des exigences de stockage est associée à 77 640 images .jpg géomarquées :



* Phase 1 : 15 279 images .jpg
* Phase 2 : 54 229 images .jpg
* Phase 3 : 8 132 images .jpg

Pour cette raison, les données sont organisées dans des dossiers spécifiques aux segments : téléchargez autant de segments que vous le souhaitez.


### Résumé (15MB)

Un projet QGIS léger avec uniquement les routes et les types de sol étudiés :



* [Consolidated-GIS.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Consolidated-GIS.zip) (15MB)
* N'inclus pas:
    * Couches détaillées d'enquête environnementale ou de construction
    * Images .jpg
    * Données géotechniques détaillées


### La phase 1 (40,4GB)

InterCity



* [FB_OTNx_CD_MSK-SMB_20201205.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_MSK-SMB_20201205.zip) (1,2GB)
* [FB_OTNx_CD_SMB-KSG_20201124.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_SMB-KSG_20201124.zip) (0,8GB)
* [FB_OTNx_CD_KSG-WMZ_20201119.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_KSG-WMZ_20201119.zip) (1,0GB)
* [FB_OTNx_CD_WMZ-KIZ_20201208.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_WMZ-KIZ_20201208.zip) (3,9GB)
* [FB_OTNx_CD_SMB-KIM_20201124.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_SMB-KIM_20201124.zip) (1,4GB)
* [FB_OTNx_CD_KIM-KND_20201118.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_KIM-KND_20201118.zip) (1,6GB)
* [FB_OTNx_CD_KSG-KAY_20201124.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_KSG-KAY_20201124.zip) (1,9GB)
* [FB_OTNx_CD_KAY-KMA_20201121.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_KAY-KMA_20201121.zip) (2,6GB)
* [FB_OTNx_CD_UVI-BKY_20201127.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_UVI-BKY_20201127.zip) (6,7GB)

Metro



* [FB_OTNx_CD_BKY_metro_20201125.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_BKY_metro_20201125.zip) (4,9GB)
* [FB_OTNx_CD_GOM_metro_20201121.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_GOM_metro_20201121.zip) (3,8GB)
* [FB_OTNx_CD_KGA_metro_20201211.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_KGA_metro_20201211.zip) (3,8GB)
* [FB_OTNx_CD_KND_metro_20201125.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_KND_metro_20201125.zip) (1,8GB)
* [FB_OTNx_CD_MJM_metro_20201212.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_MJM_metro_20201212.zip) (5,8GB)


### La phase 2 (130,4GB)

InterCity



* [FB_OTNx_CD_KGA-DEM_20210428.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_KGA-DEM_20210428.zip) (1,3GB)
* [FB_OTNx_CD_MTB-KGA_20210504.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_MTB-KGA_20210504.zip) (0,4GB)
* [FB_OTNx_CD_TSL-DIM_20210430.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_TSL-DIM_20210430.zip) (0.6GB)
* [FB_OTNx_CD_BYM-BKD-MJM_20210401.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_BYM-BKD-MJM_20210401.zip) (1,5GB)
* [FB_OTNx_CD_FKI-BAG_20210322.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_FKI-BAG_20210322.zip) (5,4GB)
* [FB_OTNx_CD_BAG-BAF_20210327.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_BAG-BAF_20210327.zip) (4,7GB)
* [FB_OTNx_CD_BAF-NIA_20210325.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_BAF-NIA_20210325.zip) (3,2GB)
* [FB_OTNx_CD_NIA-EPU_20210406.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_NIA-EPU_20210406.zip) (5,7GB)
* [FB_OTNx_CD_EPU-MBS_20210407.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_EPU-MBS_20210407.zip) (4,1GB)
* [FB_OTNx_CD_MDT-KMJ_20210409.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_MDT-KMJ_20210409.zip) (2,9GB)
* [FB_OTNx_CD_MDT-BMG_20210424.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_MDT-BMG_20210424.zip) (2,6GB)
* [FB_OTNx_CD_MDT-LUP_20210428.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_MDT-LUP_20210428.zip) (1,2GB)
* [FB_OTNx_CD_LUK-LUP_20210417.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_LUK-LUP_20210417.zip) (0,9GB)
* [FB_OTNx_CD_LUP-BMS_20210510.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_LUP-BMS_20210510.zip) (2,5GB)
* [FB_OTNx_CD_TSH-TSK_20210512.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_TSH-TSK_20210512.zip) (3,7GB)
* [FB_OTNx_CD_SBZ-TSH_20210507.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_SBZ-TSH_20210507.zip) (3,1GB)
* [FB_OTNx_CD_TSH-MDA_20210410.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_TSH-MDA_20210410.zip) (0,9GB)
* [FB_OTNx_CD_KYL-CYU_20210512.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_KYL-CYU_20210512.zip) (2,4GB)
* [FB_OTNx_CD_KMA-KBA_20210419.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_KMA-KBA_20210419.zip) (1,6GB)
* [FB_OTNx_CD_KBA-PUN_20210414.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_KBA-PUN_20210414.zip) (2,6GB)
* [FB_OTNx_CD_PUN-LTU_20210410.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_PUN-LTU_20210410.zip) (2,3GB)
* [FB_OTNx_CD_FKI-PTG_20210322.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_FKI-PTG_20210322.zip) (1,1GB)
* [FB_OTNx_CD_PTG-LTU_20210326.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_PTG-LTU_20210326.zip) (1,9GB)
* [FB_OTNx_CD_LTU-MAF_20210331.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_LTU-MAF_20210331.zip) (2,1GB)
* [FB_OTNx_CD_MAF-MUF_20210406.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_MAF-MUF_20210406.zip) (2,4GB)
* [FB_OTNx_CD_MUF-TDA_20210427.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_MUF-TDA_20210427.zip) (2,4GB)
* [FB_OTNx_CD_WMZ-PEN_20210504.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_WMZ-PEN_20210504.zip) (4,6GB)
* [FB_OTNx_CD_LMB-PEN_20210428.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_LMB-PEN_20210428.zip) (1,9GB)
* [FB_OTNx_CD_LMB-AKY_20210424.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_LMB-AKY_20210424.zip) (0,8GB)
* [FB_OTNx_CD_FMI-LKG_20210416.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_FMI-LKG_20210416.zip) (0,7GB)
* [FB_OTNx_CD_LKG-LMB_20210426.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_LKG-LMB_20210426.zip) (3,9GB)
* [FB_OTNx_CD_MIS-LMB_20210423.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_MIS-LMB_20210423.zip) (1,2GB)
* [FB_OTNx_CD_MBS-KOM_20210416.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_MBS-KOM_20210416.zip) (4,3GB)
* [FB_OTNx_CD_MDA-MTB_20210417.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_MDA-MTB_20210417.zip) (3,8GB)

Metro



* [FB_OTNx_CD_FIH_metro_zone_1_20210227.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_FIH_metro_zone_1_20210227.zip) (4,2GB)
* [FB_OTNx_CD_FIH_metro_zone_2_20210227.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_FIH_metro_zone_2_20210227.zip) (9,2GB)
* [FB_OTNx_CD_FIH_metro_zone_3_20210305.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_FIH_metro_zone_3_20210305.zip) (7,2GB)
* [FB_OTNx_CD_FIH_metro_zone_4_20210226.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_FIH_metro_zone_4_20210226.zip) (3,2GB)
* [FB_OTNx_CD_FIH_metro_zone_5_20210309.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_FIH_metro_zone_5_20210309.zip) (3,7GB)
* [FB_OTNx_CD_FIH_metro_zone_6_20210311.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_FIH_metro_zone_6_20210311.zip) (3,4GB)
* [FB_OTNx_CD_FIH_metro_zone_7_20210302.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_FIH_metro_zone_7_20210302.zip) (9,1GB)
* [FB_OTNx_CD_FKI_metro_20210312.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_FKI_metro_20210312.zip) (3,0GB)
* [FB_OTNx_CD_FMI_metro_20210412.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_FMI_metro_20210412.zip) (3,2GB)


### La phase 3 (17,6GB)

InterCity



* [FB_OTNx_CD_MNB-MEA_20210716.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_3/FB_OTNx_CD_MNB-MEA_20210716.zip) (2,4GB)
* [FB_OTNx_CD_MEA-KVA_20210710.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_3/FB_OTNx_CD_MEA-KVA_20210710.zip) (0,4GB)
* [FB_OTNx_CD_KVA-NBI_20210717.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_3/FB_OTNx_CD_KVA-NBI_20210717.zip) (3,1GB)
* [FB_OTNx_CD_NBI-NLO_20210707.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_3/FB_OTNx_CD_NBI-NLO_20210707.zip) (2,7GB)
* [FB_OTNx_CD_NLO-BZV_20210712.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_3/FB_OTNx_CD_NLO-BZV_20210712.zip) (3,1GB)
* [FB_OTNx_CD_KNZ-KVA_20210708.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_3/FB_OTNx_CD_KNZ-KVA_20210708.zip) (2,2GB)
* [FB_OTNx_CD_IGA-NBI_20210705.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_3/FB_OTNx_CD_IGA-NBI_20210705.zip) (2,6GB)
* [FB_OTNx_CD_MTE-MEA_20210714.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_3/FB_OTNx_CD_MTE-MEA_20210714.zip) (1,1GB)
