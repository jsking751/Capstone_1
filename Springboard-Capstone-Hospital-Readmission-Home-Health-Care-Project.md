### An Analysis of National Hospital Readmissions and Home-Health Care Quality
*Jonathan King*
<br>
<br>
<br>

**1. What is the problem you want to solve?:** 

Readmission to a hospital after receiving initial services can be both costly and stressful for a patient dealing with temporary illness or chronic disease.  Furthermore, the cost of hospital readmission is compounded when considering the availability for hospital beds for those who need acute or critical care.  

A hospital readmission is broadly defined as a when a patient who has been discharged from a hospital is readmitted to a hospital again within a specified time frame.  The most common time frames being 30-days, 90-days, and 1-year.

In 2010 the Centers for Medicare and Medicaid Services (CMS), under the Affordable Care Act, formally included hospital readmissions in reimbursement decisions.  Subsequently, penalizing health systems that have higher than expected readmission rates.  Specifically, this program was titled the Hospital Readmission Reduction Program.

Another program created to combat hospital readmissions is the Independence at Home Demonstration Program (IAH), which started in 2012.  This program provided mobile teams of physicians, nurse practitioners, pharmacists, social workers, and other providers to assist chronically ill Medicare patients in their homes.  The IAH found patients under their care saw fewer hospital readmissions, which resulted in an average savings of $3,070 in the first year, and $1,010 in the subsequent year.  This program was so successful that it was extended another two years beyond its original three-year window. 

https://en.wikipedia.org/wiki/Hospital_readmission

While the IAH has now concluded, many Home Health Care providers exists to provide home health care for patients.  This analysis will focus on the relationships between hospital readmission rates and Home Health Care Quality ratings to determine if high-quality home health care, does indeed play a role in reducing hospital readmissions.
<br>
<br>

**2. Who is your client and why do they care about this problem?:** 

There are multiple clients who would take interest in the conclusions found in this project.

1)	Hospitals:  Under CMS’s Hospital Readmission Reduction Program hospitals are penalized if they exceed their expected readmission rates.  If a correlation is found between high-quality home health care and a reduction in hospital readmission, this would incentivize hospitals to build relationships with high-quality home health care providers and provide education to patients directing them to these providers post-hospitalization.

2)	Home Health Care Providers:  Should a correlation be found, this would incentivize Home Health Care Providers to increase their overall quality ratings as well as give them a selling point for local hospitals to build relationships with them.  There are also several measures that contribute to what is considered a high-quality home health care provider.  This analysis will also look at these measures to determine if some of the quality rankings have a larger effect on hospital readmission than others.  This analysis would enable the home health care provider to create internal programs that focus on increasing specific quality measures to improve their standing with both patients and hospitals.

3)	Patients:  While likely not a direct client, this information will better inform patients considering home health care.  Should a correlation be found, patients may be more swayed or dissuaded from utilizing home health care to reduce their overall cost and reduce the risk of hospital readmission.  Furthermore, patients could use this information to seek out home health care providers that rank high in specific quality measures that show a correlated reduction of hospital readmissions.

4)	The US Government:  The Affordable Care Act was created by the US government to reform health care in the United States.  As such, the results of this analysis could be presented to the US government to either continue pursuing programs like the IAH or create incentives for providers, patients, and health insurance companies to utilize home health care providers, which may result in the creation of more home health care providers for areas in need.
<br>
<br>


**3.  What data are you going to use for this? How will you acquire this data?:**

CMS has provided open data to www.data.gov that contains 5 data sets regarding this analysis.  

I will be utilizing all 4 of the datasets, and keeping the 5th as an indicator of the timing for which the home health care quality survey was taken.

Data Sets Include:  

1)	The outcome of the Hospital Readmission Reduction Program, which indicates above-expected or as expected or better readmission rates of individual hospitals signed to accept Medicaid from July 1, 2013 to June 30, 2016

2)	Home health care quality measures for April 1, 2015 to March 31, 2016, broken down by state average.

3)	Additional home health care quality measures from April 1, 2015 to March 31, 2016 broken down by state average.

4)	A dataset of Medicaid accepting home health care providers and their specific quality measures

5)	A dataset indicating when each measure from the home health care quality survey was taken (this list indicates that the data taken is from April 1, 2015 to March 31, 2016 timeframe).

https://catalog.data.gov/dataset/hospital-readmissions-reduction-program
https://medicare.gov/download/HomeHealthCompare/2016/October/HHCArchive_Revised_Flatfiles_20161019.zip
https://catalog.data.gov/dataset/home-health-care-agencies-c1765
<br>
<br>
**4. In brief, outline your approach to solving this problem:**

First, I intend to compact the data from the Hospital Readmission Reduction Program to the state level.  To do this I will find the average for hospital readmissions, the total count of hospitals, the total count of hospitals with excessive readmissions, the percent of hospitals with excessive readmissions, and the percent of hospitals with better than expected readmissions.

Second, I will merge the home health care quality survey data with the additional measures data into one data set. I will also get a total count of the number of Medicaid approved home health care providers for each state using the corresponding dataset.

Finally, I will create data visualizations to compare ratings, measures, and counts, along with some inferential statistics, to determine if there is a correlation between high-quality care and lower hospital readmission.
<br>
<br>
**5. What are your deliverables?:**

My deliverables will include a narrative of the project in the form of a paper, and the code, which will be made available as part of a GitHub repository.  I may also include a PowerPoint slide deck upon request, and time-permitting.
