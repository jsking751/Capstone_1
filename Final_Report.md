## An Analysis of Hospital Readmissions and Home-Health Care Quality ##
*Jonathan King*
<br>
<br>
**The Problem:** 
<br><br>
Hospital readmission after having already received services can be both costly and stressful for a patient dealing with temporary illness or chronic disease.  Furthermore, the cost of hospital readmission is compounded when considering the availability of hospital beds for those who need acute or critical care.
<br><br> 
A hospital readmission is broadly defined as a when a patient who has been discharged from a hospital is readmitted to a hospital again within a specified time frame.  The most common time frames being 30-days, 90-days, and 1-year.
<br><br>
In 2010 the Centers for Medicare and Medicaid Services (CMS), under the Affordable Care Act, formally included hospital readmissions in reimbursement decisions.  Subsequently, penalizing health systems that have higher than expected readmission rates.  Specifically, this program was titled the Hospital Readmission Reduction Program.
<br><br>
Another program created to combat hospital readmissions is the Independence at Home Demonstration Program (IAH), which began in 2012.  This program provided mobile teams of physicians, nurse practitioners, pharmacists, social workers, and other providers to assist chronically ill Medicare patients in their homes.  The IAH found patients under their care saw fewer hospital readmissions, which resulted in an average savings of $3,070 in the first year, and $1,010 in the subsequent year.  This program was so successful that it was extended another two years beyond its original three-year window.
<br><br>
More information on the Readmission Reduction Program and IAH can be found [here](https://en.wikipedia.org/wiki/Hospital_readmission).
<br><br>
While the IAH has now concluded, many Home Health Care (HHC) providers exists to provide home health care for patients.  This analysis will focus on the relationships between hospital readmission rates and HHC Quality ratings to determine if high-quality home health care, does indeed play a role in reducing hospital readmissions.
<br>
<br>
**The Client:** 
<br><br>
HHC providers are the primary client for this analysis.  Should significant correlations be found, this would incentivize HHC providers to increase their quality ratings and open an additional opportunity to foster new relationships with local hospitals.  There are several measures that contribute to what is considered a high-quality HHC provider.  Should significant correlations exist within specific measures, HHC providers could create internal programs that focus on increasing those specific measures to reduce hospital readmission and improve their overall quality.
<br><br>
HHC providers are not the only clients that may take interest in this analysis.  Other interested parties may include hospitals, patients, and the US government.  These parties all have a shared interest in reducing hospital readmissions as a reduction would lead to reduced costs for all parties involved.
<br>
<br>
**The Data:**
<br><br>
The data used in this analysis includes the following:
1.  The outcome of the Hospital Readmission Reduction Program, which indicates above-expected and as expected (or better) readmission rates of individual hospitals contracted to accept Medicaid from July 1, 2013 to June 30, 2016
2.  HHC quality measures for April 1, 2015 to March 31, 2016, broken down by state average.
3.  Additional HHC quality measures from April 1, 2015 to March 31, 2016 broken down by state average.
4.  A dataset of Medicaid accepting HHC providers and their specific quality measures.
5.  A dataset indicating when each measure from the HHC quality survey was taken (this list indicates that the data taken is from April 1, 2015 to March 31, 2016 timeframe).  
6.  A dataset of zip codes for health care providers associated with CMS.  This dataset was used to scrape the zip codes of the hospitals listed in the Hospital Readmission dataset.
<br><br>
These data sets can be found at the following links below:
-   [Hospital Readmission Reduciton Data](https://catalog.data.gov/dataset/hospital-readmissions-reduction-program)
-   [All HHC Measures by State Data](https://medicare.gov/download/HomeHealthCompare/2016/October/HHCArchive_Revised_Flatfiles_20161019.zip)
-   [HHC Measures by Agency Data](https://catalog.data.gov/dataset/home-health-care-agencies-c1765) 
-   [CMS Health Care Provider Zipcodes](https://www.cms.gov/Research-Statistics-Data-and-Systems/Downloadable-Public-Use-Files/Provider-of-Services/POS2016.html)

While other HHC quality data does exist as additional potential datasets, this data does not coincide with the timing of CMS’ hospital readmission reduction program, and thus has a more limited usefulness.
<br>
<br>
**Crafting the Datasets:**
<br><br>
*Part 1: Data by State*
<br><br>
The first dataset crafted in this analysis was a merged dataset of the hospital readmission data, the HHC quality measures data, and the HHC additional quality measures data.
<br><br>
To begin, the readmission data needed to be munged.  Unuseful columns were removed from the original dataset, and the remaining columns were renamed for ease of access while coding.  Furthermore, numeric data was coerced from its original object type to a float64 type.
<br><br>
Subsequently, after being cleaned, the data needed to be grouped down to the state level.  Since hospitals and HHC providers are often separate entities, grouping by state was the simplest way to meaningfully attach HHC quality measures with the hospital readmission ratios.  Prior to grouping the data, a hospital count by state list and excessive readmission count by state list were created to be added into the final dataset.  Afterwards, each column was added into the final cleaned dataset through use of the groupby method on the state feature and calculating the sum or mean of the column where appropriate.
<br><br>
All the code used for cleaning the hospital readmission data can be found [here](https://github.com/jsking751/Capstone_1/blob/master/Data%20Munging/readmissions_cleaning.ipynb).
<br><br>
Now it was time to clean both the HHC quality and additional quality measures datasets and merge them onto the readmission dataset.  Fortunately, very little cleaning was required as the data was already grouped by state and next to no NaN values were found.  As such, all that was required was dropping unuseful columns, renaming the remaining columns for ease of access, and merging the three datasets together into one through a merge on the state feature.  It is important to note that merging the data resulted in some observations being lost.  Those observations included US territories that were included in the HHC data, but not in the readmission data.
<br><br>
All the code used for cleaning the HHC data and merging the three datasets can be found [here](https://github.com/jsking751/Capstone_1/blob/master/Data%20Munging/ratings_cleaning_merging.ipynb).
<br><br>
*Part 2: Data by Zip Code*
<br><br>
After exploratory data analysis (EDA), inferential statistics, and machine learning were applied to the grouped by states dataset (Data by State), I became unsatisfied with the results.  This was largely due to over 8,000 observations being reduced to a mere 51 observations.  As such, hospital zip codes were needed to meaningfully group the readmission data to the HHC Measures by Agency (HHC Agency) data.  
<br><br>
The state and zip codes for health care providers associated with CMS were located on CMS’ website.  The Zip Code data set was easily merged to the readmission data though a pandas merge, resulting in a merger of the two datasets.  Prior to merging the two datasets, the readmission data was cleaned similarly to how it was wrangled in the Data by State dataset.
<br><br>
After the readmission and zip code data was merged it was time to munge the HHC Agency data.  Like the readmission data, columns were renamed and unhelpful columns were dropped out of the dataset.  Secondly, the nulls within the data were dropped by row resulting in a total of 8,344 observations.  Unlike the original HHC quality measures data, which was already grouped by state, the HHC Agency data had additional Boolean and categorical features.  These features were converted to numeric equivalents.  Zero and one for the Boolean features and zero through three for the categorical features.
<br><br>
Following the initial munging, extreme outliers were found within some of the features of the HHC Agency data.  A portion of these outliers did not make sense to the rest of the data.  For example, some features had float point ratings like “0.50”, when most of the ratings were represented as “50.0” to represent 50%.  Unfortunately, there were no notations within the data to indicate if these float ratings were accurate and could be converted to their percentile equivalent.  As such, I chose to filter out any outliers outside of 2.5 standard deviations.  I did not wish to remove all outliers using 2 standard deviations, as I felt non-extreme outliers could be considered legitimate ratings and should be included in my analysis.
<br><br>
Finally, like the Data by State, the excessive readmissions count was calculated for each zip code and the final dataset was crafted by grouping the data by zip code and merging the readmissions and HHC Agency data together in a merge.  This resulted in a final dataset with 820 observations.  
<br>
It is important to note, most of the features were grouped by mean.  However, the categorical data was grouped by mode to indicate the majority category for each zip code.  Should a tie occur, the first category in the tie list was selected.
<br><br>
The code used to create the Data by Zip Code dataset can be found [here](https://github.com/jsking751/Capstone_1/blob/master/Data%20Munging/GroupBy_Zipcode.ipynb).
<br><br>
*Part 3: Data by Hospital*
<br><br>
Much to my surprise, and discussed in greater detail in the following section, the strong correlations found in the Data by State were not present in the Data by Zip Code.  As such, I decided producing even more observations may unlock relationships within the two data sets.  To do this, I merged the cleaned readmission data with the HHC Agency data grouped by zip code.  This resulted in a dataset where each hospital observation now contained the HHC Agency data relevant to their shared zip code.
<br><br>
All techniques and decisions used were discussed previously in Parts 1 and 2 of this section.  One new feature was created, which was the number of HHC Agencies in each zip code.  This was calculated by grouping the agencies by zip code and calling count after the groupby method.  The final dataset resulted in an encouraging 5,882 observations. 
<br><br>
The code used to create the Data by Hospital dataset can be found [here](https://github.com/jsking751/Capstone_1/blob/master/Data%20Munging/Merge_by_Hospital.ipynb).
<br>
<br>
**Findings:** 
<br><br>
After applying some EDA and inferential statistics, several relationships were found in the Data by State.  For a quick heatmap overview of these relationships data, refer to Figure 1-1 below.  Some unsupervised machine learning was run on this data, which resulted in unsatisfying and uninformative clustering.  The goal of the unsupervised machine learning was to see if there were deeper relationships within the features of the data that may have contributed to a higher or lower readmission ratio.  After this initial machine learning exercise was completed, I decided more observations were needed.
<br>
![Figure 1-1](https://github.com/jsking751/Capstone_1/blob/master/Figures/state_heatmap.png "Figure 1-1")
<br>
Following this determination, I then ran EDA on the Data by Zip Code.  As previously stated, I was shocked to discover none of the relationships I found between readmission ratio and HHC quality measures in the Data by State were present (Figure 1-2)
<br>
![Figure 1-2](https://github.com/jsking751/Capstone_1/blob/master/Figures/zipcode_heatmap.png "Figure 1-2")
<br>
I knew there was significantly more variation in my data, so I decided to test various scaling methods to see if they would bring out any relationships hidden by noise within the data.  First, I tried scaling one of the quality measures by Ordinary Least Squares (OLS) Regression.  This resulted in an R-Squared of 0.001 and a P-value of 0.27 (Figure 1-3).  As such, I concluded this type of scaling model would unlikely produce any significant results.
<br><br>
![Figure 1-3](https://github.com/jsking751/Capstone_1/blob/master/Figures/zipcode_ols.PNG "Figure 1-3")
<br>
I then used Scikit-Learn’s Standard Scaler to scale the data.  This produced a heatmap nearly identical to the heatmap generated without any applied scaling (Figure 1-4).
<br>
![Figure 1-4](https://github.com/jsking751/Capstone_1/blob/master/Figures/zipcode_ss_heatmap.png "Figure 1-4")
<br>
For my final scaling technique, I tried Scikit-Learn’s Normalizer.  This produced a very interesting heatmap with some significant relationships (Figure 1-5).  However, Normalizer is typically used to find clusters in data.  To achieve this, Normalizer scales the data by observation, not by feature.  As such, while some of these relationships may be interesting, they would not amount to much in the form of an actionable conclusion for my client.  Subsequently, this heatmap was rejected for further analysis.
<br>
![Figure 1-5](https://github.com/jsking751/Capstone_1/blob/master/Figures/zipcode_normalizer_heatmap.png "Figure 1-5")
<br>
The last EDA I ran was on the Data by Hospital.  This too resulted in a similar heatmap to the one produced in the Data by Zip Code (Figure 1-6).  I did not attempt any scaling techniques on this dataset as I learned, from the scaling attempts on the Data by Zip Code, that I would get similar outcomes.
<br>
![Figure 1-6](https://github.com/jsking751/Capstone_1/blob/master/Figures/by_hospital_heatmap.png "Figure 1-6")
<br>
All code for the exploratory data analysis can be found in following notebooks:
[Data by State EDA](https://github.com/jsking751/Capstone_1/blob/master/EDA%20and%20Analysis/Capstone1_EDA_Part_1.ipynb) 
[Data by Zip Code EDA](https://github.com/jsking751/Capstone_1/blob/master/EDA%20and%20Analysis/Capstone1_EDA_Part_2.ipynb).
[Data by Hospital EDA](https://github.com/jsking751/Capstone_1/blob/master/EDA%20and%20Analysis/EDA_Part_3.ipynb).
<br><br>
All code for the inferential statistics can be found [here](https://github.com/jsking751/Capstone_1/blob/master/EDA%20and%20Analysis/inferential_stats.ipynb).
<br>
All code for the unsupervised machine learning can be found [here]( https://github.com/jsking751/Capstone_1/blob/master/EDA%20and%20Analysis/Machine_Learning.ipynb)
<br>
<br>
**Conclusion:**
<br><br>
After an exhaustive review, I have concluded that there is no significant relationship between excessive hospital readmission and CMS’ HHC quality measures and star ratings.  While strong relationships were present on the Data by State level, they do not hold up once more observations are considered.
<br><br>
However, this does not mean HHC Agencies do not impact the readmission ratios of hospitals.  As previously mentioned, the IAH program saw reductions to hospital readmissions and in consumer health care cost during its implementation.
<br><br>
Hospital readmission is a complex problem with many factors at play.  While there is evidence to suggest HHC Agencies may play a part in solving this problem, they are certainly only one piece to a greater puzzle.  This analysis suggests that CMS’ quality measures do not play a role in readmission ratios, closing the door to these particular data points, but leaving other features of HHC open to be explored in the future.
<br>
<br>
**Recommendations and Next Steps:**
<br><br>
*Search for or Generate More HHC Data to Analyze*
<br><br>
While CMS’ quality measures do not correlate with excessive hospital readmissions, other features in HHC might.  For example, the number of clinical staff, the total number of clients, or amount of funding all may be better indicators of how HHC impacts hospital readmission.  While beyond the scope of this analysis, future analysis may be done focusing on these features over quality features.  A great place to start would be any data produced by the IAH program.  This data may give insight as to which features played an important role in the reduction of hospital readmissions.
<br><br>
*Analyze Star Rating*
<br><br>
One series of relationships that were pervasive throughout each EDA iteration, and visible in every heatmap within this report, is the relationship between star ratings and CMS’ other quality measures.  Some measures may be more important than others when it comes to a higher star rating.  As seen in Figure 2-1 below, some of these relationships have high correlation coefficients.   Furthermore, star ratings are very important to HHC Agencies as they are a means to attract clients, compete with other HHC Agencies, and may even create a stronger position for the agency when negotiating rates with insurance providers.  This is a thread I may follow up on myself should time permit.
<br>
![Figure 2-1](https://github.com/jsking751/Capstone_1/blob/master/Figures/move_on_star.png "Figure 2-1")
<br>
*Find Contributions to Excessive Readmission Rate*
<br><br>
Another avenue of exploration would be to analyze hospital data to understand where the bulk of hospital readmissions come from.  While some measures like post heart failure, and knee/hip replacement were included in the readmission data, many other forms of hospital services were not.  A more comprehensive look into hospital readmissions may not only help to resolve excessive readmission, it may also open the door to new services HHC Agencies could provide, thus increasing their customer base and reducing readmissions.
