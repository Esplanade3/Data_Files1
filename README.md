**Examining Local Relationships between Age and Underlying Conditions on COVID-19 Incidence**

Data and Computational Steps


Prepared by: Naomi W. Lazarus, PhD

August 20th, 2021

**A. Introduction**

A county-level assessment of COVID-19 in relation to age demographics and comorbidities is carried out to provide context to the emerging hotspots of the virus during the early stages of the pandemic.  The two peak periods under investigation were 03/01/20 - 04/30/20 and 06/01/20 - 07/31/20.  The spatial relationships between coronavirus, age, and comorbidities is examined using geographically weighted regression (GWR).  COVID-19 incidence rate and death-case ratio function as the dependent variables. The independent variables include percent population in age cohorts 50 – 74 and above 75, heart disease mortality, diabetes, and obesity.  Data and methodological challenges in defining the GWR model had to be addressed in the interests of reproducibility and transparency.

**B.  Data Sources**

Variable Definition	Source
COVID-19 case and death counts	USAFacts.org
https://usafacts.org/visualizations/coronavirus-covid-19-spread-map/ 

Percent population aged 50 - 74	American Community Survey 2018 5-year estimates
data.census.gov

Percent population aged 75 and above	--do--
Percent population diagnosed with diabetes	Centers for Disease Control and Prevention
https://gis.cdc.gov/grasp/diabetes/DiabetesAtlas.html#

Mortality rate – number of deaths per 100,000 of population	Centers for Disease Control and Prevention
https://wonder.cdc.gov/

Percent adult population with diagnosed obesity	Centers for Disease Control and Prevention
https://gis.cdc.gov/grasp/diabetes/DiabetesAtlas.html#


**C.  Dependent Variables**

Incidence Rates during peak period 1  (03/01/20 to 04/30/20)

Incidence Rates during peak period 2  (06/01/20 to 07/31/20)

Calculation of Incidence rates:

New covid cases during the first peak – 03/01/20 to 04/30/20 was obtained by subtracting value in 03/01/20 from 04/30/20.  Use incidence rate formula to calculate the rate. 

New covid cases during the second peak – 06/01/20 to 07/31/20 was obtained by subtracting value in 06/01/20 from 07/31/20. Use incidence rate formula to calculate the rate. 

Incidence Rate = (Number of New Cases during a specified time period)/(Total County Population)  x 100,000

Log Transformation:

Dependent variables were transformed (Log10) to address skewness.  Can be done on Excel or SPSS.

**D.  Datasets**

Counties with no recorded coronavirus cases or deaths during the peak periods were removed. 
Counties with death counts below 10 due to heart disease were removed. 
Counties that recorded zero or unreliable numbers related to the other independent variables were removed.  
Four datasets were compiled.  All datasets contained the same independent variables.  Dependent variable was unique to each dataset.  Size of dataset varied after data clean-up was completed. 


Peak Period					Dependent Variable			Number of Observations

Peak 1: 03/01/20 - 04/30/20			Incidence Rate				N = 2,807

Peak 2: 06/01/20 - 07/31/20			Incidence Rate				N = 3,061

**E.  File Descriptions**

Layer_IR1_1.shp: modified county-level shapefile of contiguous US - contains data for Incidence rate for Peak 1 (03/01/20 - 04/30/20) and all age cohort and comorbidity variables.  Number of observations (counties): 2807

Layer_IR2_1.shp: modified county-level shapefile of contiguous US - contains data for Incidence Rate for Peak 2 (06/01/20 - 07/31/20) and all age cohort and comorbidity variables.  Number of observations (counties): 3061

IR1_table.csv: CSV table containing Dependent Variable - Incidence rate for Peak 1 (03/01/20 - 04/30/20) and all age cohort and comorbidity variables.  Number of observations (counties): 2807

IR2_table.csv: CSV table containing Dependent Variable - Incidence Rate for Peak 2 (06/01/20 - 07/31/20) and all age cohort and comorbidity variables.  Number of observations (counties): 3061

**F.  Variable Descriptions**

Dependent Variables: 
       
       IR1_log  -  Log transformed covid-19 incidence rates for peak period 1 (03/01/20 - 04/30/20)
       IR2_log  -  Log transformed covid-19 incidence rates for peak period 2 (06/01/20 - 07/31/20)
	
Predictors:
        
	PCT_50to74  - Percent population aged 50 - 74
        PCT_over75  - Percent population aged 75 and above
        DIAB_PCT  - Percent population diagnosed with diabetes
        CARDIO_MR  - Heart disease mortality rate – number of deaths per 100,000 of population
        OBESE_PCT  - Percent adult population with diagnosed obesity

Geography/Geometry:
        
	X  -  X coordinate of geographic centroid of spatial feature (county) in meters
        Y  -  Y coordinate of geographic centroid of spatial feature (county) in meters

Projection:
        
	USA Contiguous Equidistant Conic Projection
        Linear Unit: Meters

Other Variables - not directly referenced in the code sample or not included in the analysis
        
	CTY_FIPS; countyFIPS  -  County Fips code
        CountyName  -  County name
        State  -  State abbreviation
        population - population count by county
        NEW_DTH_PD1  -  number of new death counts from covid-19 during peak period 1 (03/01/20 - 04/30/20)
        NEW_DTH_PD2  -  number of new death counts from covid-19 during peak period 2 (06/01/20 - 07/31/20) 
        NEW_CASE_PD1 -  number of new case counts from covid-19 during peak period 1 (03/01/20 - 04/30/20)
        NEW_CASE_PD2 -  number of new case counts from covid-19 during peak period 2 (06/01/20 - 07/31/20)
        DR1  -  Death-Case ratio for peak period 1 (03/01/20 - 04/30/20)
        DR2  -  Death-Case ratio for peak period 2 (06/01/20 - 07/31/20)
        IR1 - Incidence rate for peak period 1 (03/01/20 - 04/30/20)
        IR2  -  Incidence rate for peak period 2 (06/01/20 - 07/31/20)
        PCT_0to19  -  Percent population aged 0 - 19
        PCT_20to34 -  Percent population aged 20 - 34
        PCT_35to49 - Percent population aged 35 - 49
        INTPTLAT - Latitudinal coordinate of geographic centroid of spatial feature in decimal degrees
        INTPTLON - Longitudinal coordinate of geographic centroid of spatial feature in decimal degrees
        Shape_Length - perimeter of polygon boundary of spatial feature (county) in meters
        Shape_Area - areal extent of polygon of spatial feature (county) in square meters

**G.  Software**

ArcGIS Pro 2.5

Jupyter Notebook

PySAL – access sample code and definitions
https://mgwr.readthedocs.io/en/latest/generated/mgwr.gwr.GWRResults.html#mgwr.gwr.GWRResults

 
**H. OLS Regression**

Run OLS regression for each dataset with incidence rates and death-case ratios for each peak period as the dependent variable. 
Code sample:

![image](https://user-images.githubusercontent.com/73550457/135687577-3191ff71-3815-4ed1-a4ac-c6e67b061c4d.png)
 

**I.   GWR – model specification**

Model Type: Continuous 
Bandwidth:  Number of Neighbors
Weighting Scheme: Gaussian
Bandwidth:
The golden section search method was used to identify the appropriate number of neighbors for each of the datasets based on the lowest AIC value.

Code sample for testing suitable bandwidth:

![image](https://user-images.githubusercontent.com/73550457/135687714-c616ce47-fd71-4453-b55c-4d45442e31e6.png)

 
Bandwidths based on number of neighbors for each dataset provided below:

Peak Period			Dependent Variable	GWR Bandwidth (no. of neighbors)

Peak 1: 03/01/20 - 04/30/20	Incidence Rate		102

Peak 2: 06/01/20 - 07/31/20	Incidence Rate		111


Code sample for specifying the GWR model:

![image](https://user-images.githubusercontent.com/73550457/135687762-564e751e-c826-4db0-ac7a-8504325d0627.png)
 

**J.  Summary of OLS Regression Results**

Example using IR1_log as the dependent variable (dataset 1):
 
![image](https://user-images.githubusercontent.com/73550457/135687822-4a23016a-f14f-4642-a26b-80e6d4ecde8b.png)



**K.  Summary of GWR Results**

Example using IR1_log as the dependent variable (dataset 1).

Code sample and results for model fit statistics:

![image](https://user-images.githubusercontent.com/73550457/135687878-cc8a5821-82f2-4ff4-b9cf-7380ae1064bd.png)


Code sample and results for local b coefficients:
 
 ![image](https://user-images.githubusercontent.com/73550457/135687912-7d4c9d59-0780-461d-8ce3-f6c658377754.png)

Standardized Residual Map:
 
![image](https://user-images.githubusercontent.com/73550457/135687931-b51560f8-2d2b-4852-a7f5-68db1e4968d3.png)
 
Local R2 value map:
 
 ![image](https://user-images.githubusercontent.com/73550457/135687949-2372e944-29c3-4902-9702-639f282d274d.png)

**L.  Jupyter Notebooks**

For complete code sample and results using individual datasets, refer to the detailed notebooks.
Notebook 1: https://cybergisxhub.cigi.illinois.edu/notebook/geographically-weighted-regression-part-i-covid-19-incidence/
Notebook 2: https://cybergisxhub.cigi.illinois.edu/notebook/geographically-weighted-regression-part-ii-covid-19-mortality/


