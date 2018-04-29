### Capstone Milestone Report: National Hospital Readmissions and Home-Health Care Quality ###

*Jonathan King*

***
**The Problem:** 

Readmission to a hospital after receiving initial services can be both costly and stressful for a patient dealing with temporary illness or chronic disease.  Furthermore, the cost of hospital readmission is compounded when considering the availability for hospital beds for those who need acute or critical care.  

This analysis will focus on the relationships between hospital readmission rates and Home Health Care (HHC) quality ratings to determine if high-quality home health care, does indeed play a role in reducing hospital readmissions.

***
**The Client:** 

HHC providers are the primary client for this analysis.  Should significant correlations be found, this would incentivize HHC providers to increase their quality ratings as well as give them a selling point that could foster new relationships with local hospitals.  There are also several measures that contribute to what is considered a high-quality HHC provider.  Should significant correlations exist within specific measures, HHC providers could create internal programs that focus on increasing those specific measures to reduce hospital readmission and improve their overall quality.

HHC providers are not the only clients that may take interest in this analysis.  Other interested parties may include hospitals, patients, and the US government.  These parties have a shared interest in reducing hospital readmissions as a reduction would lead to reduced costs for all parties involved.

***
**The Available Data:** 

The Centers for Medicare and Medicaid Services (CMS) have provided open data to www.data.gov that contains 5 data sets regarding this analysis.  

Three of the five datasets have been utilized in this analysis.  The fourth will be held for future machine learning testing, and the fifth will be kept as an indicator of the timing for which the home health care quality survey was taken.

*Data Sets Include:*  

1.  The outcome of the Hospital Readmission Reduction Program, which indicates above-expected or as expected or better readmission rates of individual hospitals signed to accept Medicaid from July 1, 2013 to June 30, 2016

2.  Home health care quality measures for April 1, 2015 to March 31, 2016, broken down by state average.

3.  Additional home health care quality measures from April 1, 2015 to March 31, 2016 broken down by state average.

4.  A dataset of Medicaid accepting HHC providers and their specific quality measures

5.  A dataset indicating when each measure from the home health care quality survey was taken (this list indicates that the data taken is from April 1, 2015 to March 31, 2016 timeframe).  

These data sets can be found at the following links below:

-   [Hospital Readmission Reduciton Data](https://catalog.data.gov/dataset/hospital-readmissions-reduction-program)
-   [All HHC Measures by State Data](https://medicare.gov/download/HomeHealthCompare/2016/October/HHCArchive_Revised_Flatfiles_20161019.zip)
-   [HHC Measures by Agency Data](https://catalog.data.gov/dataset/home-health-care-agencies-c1765)   

While other HHC quality data does exist as another potential dataset, this data does not coincide with the timing of CMS’ hospital readmission reduction program, and thus has a more limited usefulness.

***
**Crafting the Dataset:**

The dataset crafted for this analysis is a merged dataset of the hospital readmission data, the HHC quality measures data, and the HHC additional quality measures data.

The first step required was to clean the readmission data.  Unuseful columns we removed from the original dataset, and the columns were renamed for ease of access while coding.  Furthermore, numeric data was coerced from its original object type to a float64 type.

Subsequently, after being cleaned, the data needed to be grouped down to the state level.  Since hospitals and HHC providers are often separate entities, grouping by state was the only way to meaningfully attached quality measures with the hospital readmission ratios.  Prior to grouping the data, a hospital count by state list and excessive readmission count by state list were created to be added into the final dataset.  Afterwards, each column was added into the final cleaned dataset through use of the groupby method on the state and calculating the sum or mean of the column where appropriate.

All the code used for cleaning the hospital readmission data can be found [here](https://github.com/jsking751/Capstone_1/blob/master/readmissions_cleaning.ipynb).

Now it was time to clean and merge the HHC quality and additional quality measures datasets to the readmission dataset.  Fortunately, very little cleaning was required as the data was already grouped by state and next to no NaN objects were found.  As such, all that was required was dropping unuseful columns, renaming the remaining columns for ease of access, and merging the three datasets together into one by joining them on the state.  It is important to note that joining the data resulted in some observations being lost.  Those observations included US territories that were included in the HHC data, but not in the readmission data.

All the code used for cleaning the HHC data and merging the three datasets can be found [here](https://github.com/jsking751/Capstone_1/blob/master/ratings_cleaning_merging.ipynb).

Please note, the HHC Measures by Agency data was also cleaned to produce a tidy dataset.  Further details about this process will be provided should the data be used in the future.  The code used to clean the HHC Measures by Agency data can be found [here](https://github.com/jsking751/Capstone_1/blob/master/nongrouped_data_cleaning.ipynb).
***
**Initial Findings:** 

After applying some exploratory data analysis and inferential statistics, several expected and surprising discoveries were found.  Most surprising, there is no correlation between star rating and readmission ratio.  Moreover, the statistically significant findings can be grouped into two bins: positively correlated and negatively correlated.

All code for the exploratory data analysis can be found in [Part 1](https://github.com/jsking751/Capstone_1/blob/master/EDA%20and%20Analysis/Capstone1_EDA_Part_1.ipynb) and [Part 2](https://github.com/jsking751/Capstone_1/blob/master/EDA%20and%20Analysis/Capstone1_EDA_Part_2.ipynb).

All code for the inferential statistics can be found [here](https://github.com/jsking751/Capstone_1/blob/master/EDA%20and%20Analysis/inferential_stats.ipynb).

The negatively correlated measures (Figure 1:1 and 1:2) were associated with preventative care measures.   Specifically, higher flu and pneumonia shot ratings.  This was expected as the whole purpose of preventative care is to prevent serious illness that would require more extensive care or hospitalization.

The positively correlated measures (Figures 1:3 – 1:6) were associated with the client improving.  Specifically, with regards to improved movement, healing, ability to take oral medications, and a decrease in movement pain.  This was highly unexpected as these ratings suggest that the client is recovering, or improving in their health. 

There appears to be both expected and unexpected relationships between HHC quality measures and readmission ratios.  These strong relationships will help craft a story to help healthcare providers reduce hospital readmissions, and open the door to future research on the subject. <br>


![Figure 1-1](https://github.com/jsking751/Capstone_1/blob/master/Figures/flu_shot.png "Figure 1-1")
![Figure 1-2](https://github.com/jsking751/Capstone_1/blob/master/Figures/pneumonia_shot.png "Figure 1-2")
![Figure 1-3](https://github.com/jsking751/Capstone_1/blob/master/Figures/move_buff.png "Figure 1-3")
![Figure 1-4](https://github.com/jsking751/Capstone_1/blob/master/Figures/healing_buff.png "Figure 1-4")
![Figure 1-5](https://github.com/jsking751/Capstone_1/blob/master/Figures/oral_rx.png "Figure 1-5")
![Figure 1-6](https://github.com/jsking751/Capstone_1/blob/master/Figures/pain_debuff.png "Figure 1-6")