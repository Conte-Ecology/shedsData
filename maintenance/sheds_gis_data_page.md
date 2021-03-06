---
title: "SHEDS Data GH Page"
author: "Kyle O'Neil"
date: "March 30, 2016"
output: 
  html_document
  keep_md: yes
---





# SHEDS GIS Data
----------------
  
This project documents the steps used to generate the supporting data used on 
the Spatial Hydro-Ecological Decision System (SHEDS). It includes descriptions 
of products and processing related to:
* The high resolution catchment delineation
* Basin characteristics used in models and visualization
* Daily climate records used to drive models
* A spatial layer representing water bodies experiencing tidal influence
* A spatial layer representing river segments potentially influenced by upstream 
impoundments

The high resolution delineation spatial layers, basin characteristics, and 
documentation files have been made available on the SHEDS GIS Data 
[download page](http://ecosheds.org/assets/nhdhrd/v2/). The specific layers made 
avilable are described in the respective sections below.

Further details about the data sources related to each product can be found 
directly in the product repositories.
<br><br>

  
## The National Hydrography Dataset High Resolution Delineation Version 2 (NHDHRDV2)

Repository: [NHDHRDV2](https://github.com/Conte-Ecology/shedsData/tree/master/NHDHRDV2)
<br>
Product Download: [SHEDS GIS Data download page](http://ecosheds.org/assets/nhdhrd/v2/)

### Description
The NHDHRDV2 is a series of GIS layers representing hydrologic catchments and 
flowlines spanning the Northeast region of the United States. The catchments 
are similar to existing products such as the well-known NHD Plus dataset. 
Based on the National Hydrography Dataset (NHD), catchment layers contain 
fields to indicate routing paths which can be used to establish the network 
structure. Some basic information about the layers is also included in the 
attribute tables. Layers representing riparian buffer zones in each catchment 
also exist.

The NHDHRDV2 seeks to address specific aspects of existing hydrography products 
that have proven to restrict their usefulness. Specifically, improved spatial 
resolution and consistency are the focus of the development of these products. 
Catchment delineation is based on the high resolution NHD flowlines. Currently, 
there are no known large scale catchment products derived from this more detailed 
layer. One primary focus of this product is to capture small headwater streams 
omitted by existing products such as the medium resolution catchments in NHDPlus 
Version 2. Representing these streams can be critical to understanding key ecological 
interests. Figure 1 shows the added catchment detail from the high resolution 
streams in the Westbrook stream in Whately, MA.

![Figure 1](https://cloud.githubusercontent.com/assets/6216239/13364134/22316bc8-dc9b-11e5-93f9-3d1d0db73fb0.png)

Figure 1: Catchment resolution compariston in the Westbrook, Whately, MA 
<br><br>
  
Resolution consistency is addressed in the creation of the high resolution 
catchments. The NHD Plus Version 2 catchments, derived from the medium resolution 
NHD flowlines, are unnaturally inconsistent in area. The inconsistency is evidenced 
in Figure 2, which shows a regional view of the catchments. The unnatural catchment 
area differential shows up as straight lines between lighter and darker shades, 
indicating lesser and greater density of catchments respectively. These inconsistencies 
permeate the entire dataset and are a result of the varying resolution of existing 
hydrography data in the region. The areal inconsistency presents a problem for models 
relying on drainage area as a driver as well as for visual representation of data layers. 

![Figure 2](https://cloud.githubusercontent.com/assets/6216239/13364586/9ddedc0e-dc9d-11e5-8f8c-7b7126654b8a.png)

Figure 2: NHDPlus Version 2 medium resolution catchments in the Northeast
<br><br>
  
The issue shown above in the medium resolution layers also exists in the high 
resolution flowlines. It is evident from examining the flowline layers that the 
dataset has been processed in a gridded format at differing resolutions. The 
catchments are developed using a methodology for improving areal consistency. 
The hydrography layers created by this method are derived from a 30m resolution 
digital elevation model and the NHD high resolution flowlines. The high resolution 
flowlines edited by the Designing Sustainable Landscapes (DSL) Project to eliminate 
network gaps, correct flow direction, and remove coastline from the majority of 
the flowline layer used. Raw NHD flowlines were edited in general accordance with 
the DSL Project methodolgoy to produce whole watersheds that are not artificially 
split along poltical boundaries. Figure 3 shows the expansion added in the 
delineation effort.

![Range Expansion](https://cloud.githubusercontent.com/assets/6216239/13403225/05fdcaa2-dee2-11e5-9368-0a92ad782b38.png)

Figure 3: Range comparison between DSL Project boundary and NHDHRDV2 layers
<br><br>
  
The final products adhere to an established areal consistency while managing to 
include higher resolution streams than the medium resolution products. The high 
resolution catchments, network, and flowlines form the foundation of the other 
data in this project that go into SHEDS. The layers are divided by hydrologic 
region as shown in Figure 4. Comprehensive documentation and citations for source 
data can be found in the 
[NHDHRDV2 Documentation file](http://ecosheds.org/assets/nhdhrd/v2/NHDHRDV2_Documentation.docx).

![Hydrologic Regions](https://cloud.githubusercontent.com/assets/6216239/13403701/55a1428a-dee4-11e5-952d-eded1daa6e83.png)

Figure 4: Hydrologic region map
<br><br>

In addition to the existing hydrography layers, it is possible to utilize the 
processing effort for delineating user-specified locations. The 
[MassDOT Deerfield Culvert Delineation](http://conte-ecology.github.io/culvertDelineation_MassDOT/) 
exemplifies this process for a separate project. Watersheds are delineated from 
a culvert location layer and landscape attributes within the watersheds are 
assigned to each culvert location. 
<br><br>


### Products
The spatial hydrography products described in this section are currently 
available on the download page. Each of the 4 layers described below are grouped 
into the "spatial_XX.zip" files for each of the 6 hydrologic regions in Figure 4.

#### Catchments
The catchments layer consists of polygons representing the drainage area 
contributing to individual stream segments in the "truncated flowlines" network 
described below. One catchment polygon exists per stream segment. A segment is 
defined as the reach in between confluences. The table below describes the 
fields in the shapefile attributes table.

|   Field    | Description                                                                                                                                               |   Type   |
|:----------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------|:--------:|
|    FID     | A unqiue identifier specific to the spatial layer (required field)                                                                                        | Integer  |
|   Shape    | The spatial geometry type of the layer such as "Point" or "Polygon"                                                                                       | Geometry |
|   Source   | The process by which the catchment was defined. Categories are "Delineation", "Coastal", or "Coastal Fill" and are described in the product documentation |   Text   |
| FEATUREID  | The unique ID that links catchments to their respective flowlines or riparian buffers                                                                     |  Double  |
| NextDownID | The FEATUREID of the catchment located immediately downstream in the network                                                                              |  Double  |
| Shape_Leng | The length of the feature in meters (required field)                                                                                                      |  Double  |
| Shape_Area | The area of the feature in meters (required field)                                                                                                        |  Double  |
|  AreaSqKM  | The area of the feature in square kilometers                                                                                                              |  Double  |
<br>

#### Truncated Flowlines
The truncated flowlines layer consits of polylines representing the delineation 
flowlines used to define the catchments. These flowlines are an adjusted version 
of the high resolution flowlines. In this layer streams are only initiated if 
they meet the minimum 0.75 square kilometer drainage area threshold. The table 
below describes the fields in the shapefile attributes table.

|   Field    | Description                                                                                                                                               |   Type   |
|:----------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------|:--------:|
|    FID     | A unqiue identifier specific to the spatial layer (required field)                                                                                        | Integer  |
|   Shape    | The spatial geometry type of the layer such as "Point" or "Polygon"                                                                                       | Geometry |
|   Source   | The process by which the catchment was defined. Categories are "Delineation", "Coastal", or "Coastal Fill" and are described in the product documentation |   Text   |
| FEATUREID  | The unique ID that links catchments to their respective flowlines or riparian buffers                                                                     |  Double  |
| NextDownID | The FEATUREID of the catchment located immediately downstream in the network                                                                              |  Double  |
| Shape_Leng | The length of the feature in meters (required field)                                                                                                      |  Double  |
|  LengthKM  | The length of the feature in kilometers                                                                                                                   |  Double  |
<br>

#### Detailed Flowlines
The detailed flowlines layer is a polyline representation of the high resolution 
flowlines mapped to the catchments. Multiple stream segments may exist for a 
single catchment with no intra-catchment network identifiers present in the 
layer. The table below describes the fields in the shapefile attributes table.

|   Field    | Description                                                                           |   Type   |
|:----------:|:--------------------------------------------------------------------------------------|:--------:|
|    FID     | A unqiue identifier specific to the spatial layer (required field)                    | Integer  |
|   Shape    | The spatial geometry type of the layer such as "Point" or "Polygon"                   | Geometry |
| FEATUREID  | The unique ID that links catchments to their respective flowlines or riparian buffers |  Double  |
| Shape_Leng | The length of the feature in meters (required field)                                  |  Double  |
|  LengthKM  | The length of the feature in kilometers                                               |  Double  |
<br>

#### Region Boundary
The region boundary layer is simply the outline of the catchments layer for the 
hydrologic region. The table below describes the fields in the shapefile 
attributes table.

|   Field    | Description                                                         |   Type   |
|:----------:|:--------------------------------------------------------------------|:--------:|
|    FID     | A unqiue identifier specific to the spatial layer (required field)  | Integer  |
|   Shape    | The spatial geometry type of the layer such as "Point" or "Polygon" | Geometry |
| Shape_Leng | The length of the feature in meters (required field)                |  Double  |
| Shape_Area | The area of the feature in square meters (required field)           |  Double  |
<br><br>


## Basin Characteristics
  
Repository: [basinCharacteristics](https://github.com/Conte-Ecology/shedsData/tree/master/basinCharacteristics)
<br>
Product Download: [SHEDS GIS Data download page](http://ecosheds.org/assets/nhdhrd/v2/)

### Description
This section assigns a variety of attributes from different sources to the 
hydrologic catchments in the NHDHRDV2. The basin characteristics are spatially 
attributed to the zonal catchment layers through a series of ArcPy and R scripts. 
Varying source data structures are processed to create uniformly structured 
value raster layers that are attributed to the individual catchments and 
aggregated to larger basins based on the network structure of the delineation
product. The repository provides an in depth description of the processing steps 
and the different characteristics assigned. For a full list of variables refer 
to the [NHDHRDV2 Covariate Documentation spreadsheet](http://ecosheds.org/assets/nhdhrd/v2/NHDHRDV2_Covariate_Documentation.xlsx).
<br><br>
  
### Products
The basin characteristics for the delineation products are made available on 
the download page. Spatial averages for the full list of variables exist over 
4 zones: the catchment area plus 3 riparian buffer zones (50, 100, and 200ft). 
Each of the 4 zones are grouped into the "covariates_XX.zip" files for each of 
the 6 hydrologic regions in Figure 4. The table below describes the fields in 
the covariate CSV files.

|        Field         | Description                                                                                                                                                |  Type   |
|:--------------------:|:-----------------------------------------------------------------------------------------------------------------------------------------------------------|:-------:|
|      featureid       | The unique ID that links catchments to their respective flowlines or riparian buffers                                                                      | Integer |
|       variable       | The variable name corresponding to the "Name" column of the NHDHRDV2 Covariate Documentation spreadsheet                                                   |  Text   |
|        value         | The spatial average of the variable within the zone                                                                                                        | Double  |
|         zone         | The area over which the values were spatially averaged. Options are either "local" for current zone or "upstream" for the entire contributing network zone |  Text   |
| riparian_distance_ft | The distance of the riparian buffer, in feet. The value for catchments in this field is "NA"                                                               | Integer |



## Daymet Climate Record
  
Repository: [daymet](https://github.com/Conte-Ecology/shedsData/tree/master/daymet)

This section takes advantage of the gridded daily surface weather and 
climatological summaries known as [Daymet](https://daymet.ornl.gov/). 
A daily timeseries is assigned to all catchments in the NHDHRDV2 for 
all available climate variables over the entire record (1980-2014). The 
repository README documents the process for assigning the climate records 
to each hydrologic catchment in the NHDHRDV2. 
<br><br>
  
  
## Tidal Influence Layer
  
Repository: [tidalLayer](https://github.com/Conte-Ecology/shedsData/tree/master/tidalLayer). 

The tidal influence layer represents all water bodies within the SHEDS spatial 
range that experience some form of tidal effect. Spatial layers from the 
[U.S. Fish & Wildlife Service - National Wetlands Inventory](http://www.fws.gov/wetlands/Data/Mapper.html) 
are processed to generate a spatial polygon layer of all of the tidal zones. 
The processing documentation exists in the repository README. This layer is 
primarily used to flag observed stream temperature sites that may be influenced 
by tides.
<br><br>
  
  
## Impoundment Influence Layer
  
Repository: [impoundments](https://github.com/Conte-Ecology/shedsData/tree/master/impoundments)

The impoundment influence layer is developed to represent the stream sections 
within the SHEDS hydrologic network that are impacted by impoundments. The product 
is a polyline layer representing the stream segments of a user-specified distance 
downstream from each impoundments location. The impoundments dataset comes 
from the DSL Project where the locations from The Nature Conservancy's dam inventory 
were snapped to the NHD high resolution flowlines. This source layer is not public 
and the resulting layer is only used within the SHEDS group. The processing 
documentation exists in the repository README. 
<br><br>


## Contact Info 

Kyle O'Neil <br>
koneil@usgs.gov

Benjamin Letcher <br>
bletcher@usgs.gov 
