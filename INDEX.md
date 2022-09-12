En français : [INDEX-fr.md](/INDEX-fr.md)

## Introduction

The data accessible via this GitHub repo was gathered using the process described in this Engineering at Meta blog post:



* [A new way to survey potential fiber routes — without access to paved roads](https://engineering.fb.com/2022/05/01/connectivity/fiber-routes/)

Included in this rich data set are the results of an Environmental Survey, a Construction Survey and a Geotechnical Survey (Gamma Spectrometer + Penetrometer) covering 5,898 km of potential fiber optic routes or other buried infrastructure.


## Prerequisites



* A PC with Windows, macOS or Linux
* Sufficient hard drive space (~200GB) to install QGIS software and store survey data
* Install the current version of QGIS Long term release (**avoid Latest release**)
    * [https://qgis.org/en/site/forusers/download.html](https://qgis.org/en/site/forusers/download.html)
        * Windows: 1.0GB zipped download / 2.3GB installed
        * macOS: 1.2GB zipped download / 3.2GB installed
* Familiarity with the use of QGIS; some excellent training resources:
    * [https://docs.qgis.org/3.22/en/docs/gentle_gis_introduction/index.html](https://docs.qgis.org/3.22/en/docs/gentle_gis_introduction/index.html)
    * [https://docs.qgis.org/3.22/en/docs/training_manual/index.html](https://docs.qgis.org/3.22/en/docs/training_manual/index.html)
    * [https://github.com/school-of-data/GIS-curriculum](https://github.com/school-of-data/GIS-curriculum)


## Survey Data Organization


### City Codes

Data is organized first by InterCity segment or Metro market:



* [FB_OTNx_CD_Consolidated_Project 20220712.png](https://github.com/facebookmicrosites/DRC_Infra_Survey_2020-21/blob/main/Reference/FB_OTNx_CD_Consolidated_Project%2020220712.png): overview map
* [FB_OTNx_DRC_Route_Survey_List_20210420-GitHub_Open_Source-End_Points.csv](https://github.com/facebookmicrosites/DRC_Infra_Survey_2020-21/blob/main/Reference/FB_OTNx_DRC_Route_Survey_List_20210420-GitHub_Open_Source-End_Points.csv): descriptions for 3-digit End Point locations used on the Route List tab and within Survey data files
* [FB_OTNx_DRC_Route_Survey_List_20210420-GitHub_Open_Source-Route_List.csv](https://github.com/facebookmicrosites/DRC_Infra_Survey_2020-21/blob/main/Reference/FB_OTNx_DRC_Route_Survey_List_20210420-GitHub_Open_Source-Route_List.csv): InterCity segment A-ends and Z-ends (or Metro names)


### Folder Structure

Survey data files are organized in folders as follows:



* _Env_survey:_ results of environmental survey activity
    * _1_Inhabited_area_crossing:_ hamlet, village, town, city
    * _2_Gardening_crossing:_ agricultural activity
    * _3_Forest_crossing:_ bushes, tree; more dense, less dense
    * _4_Sacred_area_crossing:_ temples, cemeteries, tombs, monuments
    * _5_Safety_risk_zones:_ landmines, landslide, militia areas (these risks are transient in nature, thus this data incomplete by its very nature)
    * _6_Other_obstacles_crossing:_ hill, mountain, 3rd party telecom networks
    * _7_Manual_trenching_area:_ narrow roads, roads impassable during rainy season
    * _8_Added_value_information:_ telecom sites, petrol stations, electrical poles and pylons
    * _9_Route_choice:_ recommended path based on environmental observations
    * _10_Env_survey_photos:_ layer linked to photos of Env_survey observations
* _Gap_observations:_ areas where one or more survey data types (Env_survey, Geotech_survey, Route_survey, etc.) could not be gathered
* _Geotech_survey:_ results of geotechnical survey activity; data is unavailable for Metro surveys
    * _Raw_data_
        * _Penetro_
            * _pda:_ Raw penetrometer data captured by Sol Solution [PANDA](https://www.sol-solution.com/en/our-materials/panda-en/) variable energy dynamic cone penetrometers
        * _Spectro_
            * _json:_ Raw gamma spectrometer data captured by Medusa Radiometrics [MS-2000](https://the.medusa.institute/pages/viewpage.action?pageId=3932225) radiation detection system
    * _Soil_type:_ Results of combining penetrometer and gamma spectrometer data to determine and estimated solid density; data organized into density bands described in: [FB_OTNx_DRC_Route_Survey_Soil_Types_20210420-GitHub_Open_Source.csv](https://github.com/facebookmicrosites/DRC_Infra_Survey_2020-21/blob/main/Reference/FB_OTNx_DRC_Route_Survey_Soil_Types_20210420-GitHub_Open_Source.csv)
* _Initial_design:_ original desktop route design
* _Route_survey:_ results of construction survey activity
    * _1_Route_obstacles_crossing:_ various construction obstacles which need to be crossed such as: bridge, erosion, gutter, railway, river, road, swamp or another type of obstruction
    * _2_Telecom_sites:_ mobile network tower sites observed during survey
    * _3_Physical_FO_route:_ recommended path based on Route_survey observations
    * _4_Route_waypoints:_ survey running line waypoints (heading changes)
    * _5_Route_survey_photos:_ layer linked to photos of Route_survey observations
* _.qgs file:_ a QGIS project file for that route segment linked to the data in the folder structure

A more detailed breakdown of Env_survey and Route_survey content can be found in this file:



* [FB_OTNx_CD_Layers_SIG_with_Color_Charter_V4_20201003-No_Colors.xlsx](https://github.com/facebookmicrosites/DRC_Infra_Survey_2020-21/blob/main/Reference/FB_OTNx_CD_Layers_SIG_with_Color_Charter_V4_20201003-No_Colors.xlsx) (download file from GitHub to view)


### Instructions

After downloading the .zip file for an InterCity segment or Metro market, decompress (unzip) the file to reveal a folder with subfolders containing survey data files. The QGIS project (.qgs file) will be at the root of that folder. Simply click on the .qgs file and it will open in QGIS. Depending on the amount of data for the InterCity segment or Metro market, the file could take 5-10 seconds to open.

**QGIS does not embed GIS data in the .qgs file.** Instead, the .qgs file stores the path to GIS data files, thus data must remain in the same location relative to the .qgs project. The entire InterCity segment or Metro market folder can be moved to another location on your hard drive, but be mindful of the following:



* Do NOT move a .qgs file out of its folder or you will break the .qgs file.
* Do NOT rearrange subfolders or files within a main InterCity segment or Metro market folder or you will break the .qgs file.
* Do NOT rename subfolders or files or you will break the .qgs file.


## Using QGIS to View Survey Data

After opening a .qgs file, chances are you will not see anything which looks like a route design. To re-center the QGIS map on the data:



* Locate the InterCity segment or Metro market name in the Layers panel (by default, this panel is located on the left side of the QGIS screen).
* Right click on that name and select “Zoom to Group”.

What looks like an InterCity segment or Metro market name is actually a Group (similar to a folder) containing links to the data for that InterCity segment or Metro market. Clicking a carat (>, v) to the left of items labeled in the Layers panel will reveal or hide items in that Group. Note there are groups for _Env_survey_, _Route_survey_, etc. Data in the .qgs file is organized similar to how it’s organized within its decompressed .zip file (see **[Folder Structure](#folder-structure)** section above).

To view _10_Env_survey_photos_ or _5_Route_survey_photos_:



* Be sure the “Show Map Tips” button is clicked on. You will find this control in the toolbar along the top of the QGIS screen (its a yellow icon which looks like a chat bubble with a green dot at its base).
* Click on one of the photo layers, then on the main map view, hover your mouse over a red (_10_Env_survey_photos_) or brown (_5_Route_survey_photos_) icon to reveal the associated photo.


## Survey Data Downloads

The survey data is organized into three (3) phases totalling 188.4GB. The majority of file count and storage requirement is associated with 77,640 geo-tagged .jpg images:



* Phase 1: 15,279 .jpg images
* Phase 2: 54,229 .jpg images
* Phase 3: 8,132 .jpg images

For this reason, data is organized into segment-specific folders: download as many segments as desired.


### Summary (15MB)

A lightweight QGIS project with just the surveyed routes and soil types:



* [Consolidated-GIS.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Consolidated-GIS.zip) (15MB)
* Does not include:
    * Detailed environmental or construction survey layers
    * .jpg images
    * Detailed geotechnical data


### Phase 1 (40.4GB)

InterCity



* [FB_OTNx_CD_MSK-SMB_20201205.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_MSK-SMB_20201205.zip) (1.2GB)
* [FB_OTNx_CD_SMB-KSG_20201124.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_SMB-KSG_20201124.zip) (0.8GB)
* [FB_OTNx_CD_KSG-WMZ_20201119.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_KSG-WMZ_20201119.zip) (1.0GB)
* [FB_OTNx_CD_WMZ-KIZ_20201208.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_WMZ-KIZ_20201208.zip) (3.9GB)
* [FB_OTNx_CD_SMB-KIM_20201124.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_SMB-KIM_20201124.zip) (1.4GB)
* [FB_OTNx_CD_KIM-KND_20201118.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_KIM-KND_20201118.zip) (1.6GB)
* [FB_OTNx_CD_KSG-KAY_20201124.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_KSG-KAY_20201124.zip) (1.9GB)
* [FB_OTNx_CD_KAY-KMA_20201121.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_KAY-KMA_20201121.zip) (2.6GB)
* [FB_OTNx_CD_UVI-BKY_20201127.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_UVI-BKY_20201127.zip) (6.7GB)

Metro



* [FB_OTNx_CD_BKY_metro_20201125.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_BKY_metro_20201125.zip) (4.9GB)
* [FB_OTNx_CD_GOM_metro_20201121.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_GOM_metro_20201121.zip) (3.8GB)
* [FB_OTNx_CD_KGA_metro_20201211.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_KGA_metro_20201211.zip) (3.8GB)
* [FB_OTNx_CD_KND_metro_20201125.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_KND_metro_20201125.zip) (1.8GB)
* [FB_OTNx_CD_MJM_metro_20201212.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_1/FB_OTNx_CD_MJM_metro_20201212.zip) (5.8GB)


### Phase 2 (130.4GB)

InterCity



* [FB_OTNx_CD_KGA-DEM_20210428.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_KGA-DEM_20210428.zip) (1.3GB)
* [FB_OTNx_CD_MTB-KGA_20210504.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_MTB-KGA_20210504.zip) (0.4GB)
* [FB_OTNx_CD_TSL-DIM_20210430.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_TSL-DIM_20210430.zip) (0.6GB)
* [FB_OTNx_CD_BYM-BKD-MJM_20210401.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_BYM-BKD-MJM_20210401.zip) (1.5GB)
* [FB_OTNx_CD_FKI-BAG_20210322.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_FKI-BAG_20210322.zip) (5.4GB)
* [FB_OTNx_CD_BAG-BAF_20210327.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_BAG-BAF_20210327.zip) (4.7GB)
* [FB_OTNx_CD_BAF-NIA_20210325.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_BAF-NIA_20210325.zip) (3.2GB)
* [FB_OTNx_CD_NIA-EPU_20210406.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_NIA-EPU_20210406.zip) (5.7GB)
* [FB_OTNx_CD_EPU-MBS_20210407.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_EPU-MBS_20210407.zip) (4.1GB)
* [FB_OTNx_CD_MDT-KMJ_20210409.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_MDT-KMJ_20210409.zip) (2.9GB)
* [FB_OTNx_CD_MDT-BMG_20210424.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_MDT-BMG_20210424.zip) (2.6GB)
* [FB_OTNx_CD_MDT-LUP_20210428.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_MDT-LUP_20210428.zip) (1.2GB)
* [FB_OTNx_CD_LUK-LUP_20210417.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_LUK-LUP_20210417.zip) (0.9GB)
* [FB_OTNx_CD_LUP-BMS_20210510.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_LUP-BMS_20210510.zip) (2.5GB)
* [FB_OTNx_CD_TSH-TSK_20210512.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_TSH-TSK_20210512.zip) (3.7GB)
* [FB_OTNx_CD_SBZ-TSH_20210507.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_SBZ-TSH_20210507.zip) (3.1GB)
* [FB_OTNx_CD_TSH-MDA_20210410.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_TSH-MDA_20210410.zip) (0.9GB)
* [FB_OTNx_CD_KYL-CYU_20210512.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_KYL-CYU_20210512.zip) (2.4GB)
* [FB_OTNx_CD_KMA-KBA_20210419.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_KMA-KBA_20210419.zip) (1.6GB)
* [FB_OTNx_CD_KBA-PUN_20210414.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_KBA-PUN_20210414.zip) (2.6GB)
* [FB_OTNx_CD_PUN-LTU_20210410.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_PUN-LTU_20210410.zip) (2.3GB)
* [FB_OTNx_CD_FKI-PTG_20210322.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_FKI-PTG_20210322.zip) (1.1GB)
* [FB_OTNx_CD_PTG-LTU_20210326.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_PTG-LTU_20210326.zip) (1.9GB)
* [FB_OTNx_CD_LTU-MAF_20210331.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_LTU-MAF_20210331.zip) (2.1GB)
* [FB_OTNx_CD_MAF-MUF_20210406.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_MAF-MUF_20210406.zip) (2.4GB)
* [FB_OTNx_CD_MUF-TDA_20210427.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_MUF-TDA_20210427.zip) (2.4GB)
* [FB_OTNx_CD_WMZ-PEN_20210504.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_WMZ-PEN_20210504.zip) (4.6GB)
* [FB_OTNx_CD_LMB-PEN_20210428.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_LMB-PEN_20210428.zip) (1.9GB)
* [FB_OTNx_CD_LMB-AKY_20210424.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_LMB-AKY_20210424.zip) (0.8GB)
* [FB_OTNx_CD_FMI-LKG_20210416.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_FMI-LKG_20210416.zip) (0.7GB)
* [FB_OTNx_CD_LKG-LMB_20210426.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_LKG-LMB_20210426.zip) (3.9GB)
* [FB_OTNx_CD_MIS-LMB_20210423.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_MIS-LMB_20210423.zip) (1.2GB)
* [FB_OTNx_CD_MBS-KOM_20210416.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_MBS-KOM_20210416.zip) (4.3GB)
* [FB_OTNx_CD_MDA-MTB_20210417.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_MDA-MTB_20210417.zip) (3.8GB)

Metro



* [FB_OTNx_CD_FIH_metro_zone_1_20210227.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_FIH_metro_zone_1_20210227.zip) (4.2GB)
* [FB_OTNx_CD_FIH_metro_zone_2_20210227.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_FIH_metro_zone_2_20210227.zip) (9.2GB)
* [FB_OTNx_CD_FIH_metro_zone_3_20210305.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_FIH_metro_zone_3_20210305.zip) (7.2GB)
* [FB_OTNx_CD_FIH_metro_zone_4_20210226.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_FIH_metro_zone_4_20210226.zip) (3.2GB)
* [FB_OTNx_CD_FIH_metro_zone_5_20210309.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_FIH_metro_zone_5_20210309.zip) (3.7GB)
* [FB_OTNx_CD_FIH_metro_zone_6_20210311.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_FIH_metro_zone_6_20210311.zip) (3.4GB)
* [FB_OTNx_CD_FIH_metro_zone_7_20210302.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_FIH_metro_zone_7_20210302.zip) (9.1GB)
* [FB_OTNx_CD_FKI_metro_20210312.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_FKI_metro_20210312.zip) (3.0GB)
* [FB_OTNx_CD_FMI_metro_20210412.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_2/FB_OTNx_CD_FMI_metro_20210412.zip) (3.2GB)


### Phase 3 (17.6GB)

InterCity



* [FB_OTNx_CD_MNB-MEA_20210716.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_3/FB_OTNx_CD_MNB-MEA_20210716.zip) (2.4GB)
* [FB_OTNx_CD_MEA-KVA_20210710.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_3/FB_OTNx_CD_MEA-KVA_20210710.zip) (0.4GB)
* [FB_OTNx_CD_KVA-NBI_20210717.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_3/FB_OTNx_CD_KVA-NBI_20210717.zip) (3.1GB)
* [FB_OTNx_CD_NBI-NLO_20210707.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_3/FB_OTNx_CD_NBI-NLO_20210707.zip) (2.7GB)
* [FB_OTNx_CD_NLO-BZV_20210712.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_3/FB_OTNx_CD_NLO-BZV_20210712.zip) (3.1GB)
* [FB_OTNx_CD_KNZ-KVA_20210708.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_3/FB_OTNx_CD_KNZ-KVA_20210708.zip) (2.2GB)
* [FB_OTNx_CD_IGA-NBI_20210705.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_3/FB_OTNx_CD_IGA-NBI_20210705.zip) (2.6GB)
* [FB_OTNx_CD_MTE-MEA_20210714.zip](https://dataforgood-meta-otnx.s3.amazonaws.com/DRC_Infra_Survey_2020-21/Phase_3/FB_OTNx_CD_MTE-MEA_20210714.zip) (1.1GB)
