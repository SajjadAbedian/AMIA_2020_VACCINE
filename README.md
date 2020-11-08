**Augmenting Publicly Available Social Determinants of Health Datasets with Clinical Data to Power Multi-Institutional Clinical Research**

# Summary

_This instructional workshop was inspired by the current approaches taken at Weill Cornell Medicine&#39;s Research Informatics team to support the clinical studies utilizing the Social Determinants of Health (SDoH) data by creating a comprehensive SDoH dataset - Variables Affecting Care and Community in New York (VACCINe). This workshop provides an introduction to augmenting clinical data with publicly available SDoH datasets to support the research enterprise at large, as well as supporting multi-institutional studies leveraging common data models such as the OMOP Common Data Model. In this workshop, we cover a brief introduction to SDoH and the current landscape of SDoH data collection methods. We will review the current approaches to obtain SDoH data from federal and local government agencies, as well as individual SDoH data. During the interactive part, the audience will learn how to merge and harmonize these publicly available datasets, recreating the VACCINe dataset on their own. We then introduce methods of geocoding for any number of the patient population. Lastly, we will demonstrate how researchers can use the OMOP Common Data Model combined with the SDoH dataset created at the workshop._

# Introduction

Social determinants of health (SDoH) constitute a broad array of environmental factors related to the circumstances in which individuals live their daily lives, including both individual-level factors, such as socioeconomic status (SES) and neighborhood social conditions, such as the availability of healthy food, local crime rates, and educational standards. The role of SDoH as a principal driver of health inequality and a substantial predictor of population health has been well-studied1,2,3. Healthcare organizations and researchers are increasingly seeking to augment their clinical data with SDoH data to improve patients&#39; health outcomes. With the advent of technology and the increasing ubiquity of the electronic health record (EHR), collecting and analyzing large volumes of patient data has become more feasible, as these data are captured during routine clinical care. However, the aggregation of similar volumes of SDoH data remains a challenge. Collecting individual SDoH variables, such as housing stability, education, and food accessibility requires the integration of data capture into clinical workflows, which poses issues both from the standpoint of resource allocation and patient comfort4. An alternate method for imputing patient SDoH data is the aggregation of neighborhood-level data through publicly available sources, under the hypothesis that patients living close to one another are likely to be subject to the same social determinants of health.

To serve the need for neighborhood-level SDoH data, federal and local government agencies have assembled several publicly available datasets aggregating SDoH measures that may have an impact on patient outcomes with varying degrees of geographic granularity. For example, the Centers for Disease Control and Prevention (CDC) make available a data set aggregating the Social Vulnerability Index (SVI)5 at the census-tract level for the entire United States, whereas in New York City, the Department of Parks and Recreation (DPR)6 offers a dataset that identifies all city-planted trees within the confines of the city&#39;s borders by latitude and longitude. To render these data sets useful for health services and clinical research, they must be first harmonized to a common geographic unit and then aggregated to a common data set describing each SDoH variable at the most granular level possible.

At Weill Cornell Medicine, a quarternary care center on Manhattan&#39;s Upper East Side, we have implemented a technique to geocode patient addresses derived from the electronic health record, assigning to each patient a latitude and longitude, where possible, and deriving for each the Federal Information Processing Standards (FIPS) code for their individual census block group. Utilizing the Federal Communications Commission&#39;s publicly available application processing interface (API), we extract patient addresses from the electronic health record, strip unnecessary data (such as apartment numbers), and return from the API all available geocoded data for each patient&#39;s address.

To make use of the data derived through this geocoding pipeline, we connect clinical data stored in the Observational Medical Outcomes Partnership (OMOP) Common Data Model7 to neighborhood-level SDoH data. Specifically, we used the techniques introduced in this workshop to develop an SDoH dataset—Variables Affecting Care and Communities in NewYork (VACCINe) which has been used for several studies focusing on healthcare quality, utilization, and outcomes in Weill Cornell Medicine. VACCINe was developed by merging and harmonizing more than 5 publicly available sources and contains more than 25 variables at two different geographical units (census tract and census block group). By connecting our local instance of the OMOP common data model to VACCINe, we are able to conduct research investigating the relationship between neighborhood-level SDoH and clinical outcomes stored in the electronic health record.

# Objective

In this workshop, we aim to review the current landscape of SDoH collection methods and their strengths and limitations. Accordingly, we will review viable options to access neighborhood-level SDoH with an eye towards publicly available datasets. We will then evaluate the limitations of publicly available sources, and methods to merge and harmonize them into a comprehensive SDoH dataset to support the research enterprise. In the second portion of the workshop, we will then demonstrate techniques for connecting SDoH with clinical data, using the OMOP common data model as a standard storage technique, illustrating how researchers can use publicly-available data to examine the impact of neighborhood-level SDoH on patient-level health outcomes.

# Who Should Attend?

The expected audience for this workshop includes:

- Researchers in the field of social determinants of health
  - They will benefit from both parts of the workshop. Learning about how to create a ready-to-use SDoH dataset for research, as well as familiarize themselves with how to link the data to clinical data
- Healthcare organizations who are interested in ways to support research enterprise at large
  - Using the completed projects by Weill Cornell Medicine&#39;s Research Informatics team to geocode patients at large scale as a template, they will learn how to augment clinical data with SDoH data.
- General audience interested in learning more about available sources of SDoH data, its strengths and limitations

# Prerequisites

The workshop is a mixture of basic (40%) and intermediate (60%) material.

Prior knowledge of Social Determinants of Health and relevant topics is highly recommended, although there will be a quick overview of the basic concepts during the lecture portion of the workshop.

Familiarity with Python programming language is recommended to follow the interactive portion of the workshop. Although we will provide the code-base with all attendees.

Prior familiarity with the OMOP Common Data Model as well as experience working with EHR data for research will be useful. This will be more pertinent to the second part of this workshop.

# Personal experience of presenters

Sajjad Abedian is a business analyst on Weill Cornell Medicine&#39;s Research Informatics team, part of the Architecture for Research Computing in Health (ARCH) program. In his current role he supports the research enterprise at WCM by matching investigators seeking to use electronic patient data for research with the appropriate informatics tools and services. Mr. Abedian led the effort to create and manage Variable Affecting Care and Community in New York (VACCINe) dataset, and is trained as s biomedical informatician with a focus on health informatics. He has previously hosted a workshop style class for masters&#39; students within WCM&#39;s Department of Population Health Sciences, walking students through the process of creating and using the VACCINe dataset (the same dataset that inspired this workshop proposal)

Evan Sholle serves as Manager of Research Informatics Services within WCM&#39;s ARCH program. In his operational role, Mr. Sholle coordinates efforts to support researchers with electronic patient data, as well as providing scientific guidance for WCM&#39;s implementation of the OMOP common data model and adoption of the Observational Health Data Sciences &amp; Informatics (OHDSI) consortium&#39;s suite of OMOP-related tools. In his academic role, Mr. Sholle conducts biomedical informatics research at WCM, focusing on the implementation of innovative informatics techniques to support research in multiple clinical areas, including health disparities, cancer, and others. He has authored multiple publications in peer-reviewed informatics and health services research journals.

Yongkang Zhang is a Research Associate in the Department of Population Health Sciences in the Weill Cornell Medical College. Dr. Zhang&#39;s research focuses on improving care delivery to high-need, high-cost patients, including those with vulnerable social conditions. His research has examined the association between vulnerable social conditions and total and preventable healthcare utilization among Medicare patients. Dr. Zhang&#39;s current project are examining the predictive power of individual- and neighborhood-level social determinants of health data to predict patients with high and preventable healthcare utilization.

# Outline

## SDoH Data Section
- Lecture: Introduction to SDoH
  - SDoH definition and why they are important to health and healthcare
  - Individual level vs. Community level SDoH
- Lecture: Data collection (both levels)
- Lecture: Geographical area (Census tract vs. Block group vs. Zip)
- Lecture: Challenges of data collection
  - Large scale data collection
  - Individual – at the point of care
- Lecture: Current effort (review of recent work on collecting SDoH data)
- Lecture: Publicly available sources
  - NYC OpenData
  - Census Data
  - CDC
  -
- Interactive: Creating the dataset
  - Step-by-step process of creating the SDoH dataset (i.e. VACCINe dataset)

## Clinical Data Section
- Lecture: Augmenting SDoH data on Clinical Data and current papers
  - Recent papers using SDoH data and the type of data they used
- Lecture: OMOP as the standardize data model to encourage multi-institutional studies
- Interactive/Lecture: Geocoding patients at large scale
- Interactive: A clinical example that utilizes OMOP and VACCINe

**Acknowledgments**

This work received support from NewYork-Presbyterian Hospital (NYPH) and Weill Cornell Medical College (WCMC), including the Clinical and Translational Science Center (CTSC) (UL1 TR000457) and Joint Clinical Trials Office (JCTO).

This work was also supported by the Weill Cornell Dean&#39;s Diversity and Health Disparities program (PI: Ancker) and the Cornell Center for Transportation, Environment, and Community Health (PI: Zhang).

**References**

1. Giuse NB, Koonce TY, Kusnoor SV, et al. Institute of Medicine Measures of Social and Behavioral Determinants of Health: A Feasibility Study. American journal of preventive medicine. 2017;52(2):199-206.
2. Social Determinants of Health | Healthy People 2020 [Internet]. [cited 2020 Mar 25]. Available from: [https://www.healthypeople.gov/2020/topics-objectives/topic/social-determinants-of-health](https://www.healthypeople.gov/2020/topics-objectives/topic/social-determinants-of-health)
3. Sharpe TT, Harrison KM, Dean HD. Summary of CDC consultation to address social determinants of health for prevention of disparities in HIV/AIDS, viral hepatitis, sexually transmitted diseases, and tuberculosis. December 9-10, 2008. Public Health Rep. 2010 Aug;125 Suppl 4:11–5.
4. Gruß I, Bunce A, Davis J, Dambrun K, Cottrell E, Gold R. Initiating and Implementing Social Determinants of Health Data Collection in Community Health Centers. Population Health Management. 2020;.
5. CDC&#39;s Social Vulnerability Index [Internet]. [cited 2020 Mar 25]. Available from: [https://svi.cdc.gov/index.html](https://svi.cdc.gov/index.html)
6. NYC Open Data - Overview [Internet]. [cited 2020 Mar 25]. Available from: [https://opendata.cityofnewyork.us/overview/](https://opendata.cityofnewyork.us/overview/)
7. Hripcsak G, Duke JD, Shah NH, et al. Observational Health Data Sciences and Informatics (OHDSI): Opportunities for Observational Researchers. Stud Health Technol Inform. 2015;216:574–578.
