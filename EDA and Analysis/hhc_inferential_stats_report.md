## Inferential Statistics Report for Hospital Readmissions and Home-Health Care Quality <br>

*Jonathan King*
***
**Goal:** 

The focus of this analysis is to determine if there is a relationship between home health care (HHC) quality and hospital readmissions.  

HHC quality was evaluated by analyzing national HHC survey data taken close to the same time as hospital readmission data by the Centers for Medicare and Medicaid Services (CMS).
***
**Steps Taken:** 

The first step was to see if the Central Limit Theorem applied to the hospital readmission ratios for each state.  Per Figure 1-1 below, a histogram plot of the ratios did not appear to have an obvious normal distribution.  As, such the theoretical normal Cumulative Distribution Function was plotted along with the ratios’ ECDF.  While the ratios did not plot cleanly to the normal CDF (Figure 1-2), they do appear to mostly follow the normal distribution.  Finally, a histogram of readmission ratios by hospital was plotted to reveal a much stronger normal distribution (Figure 1-3).  In conclusion, further statistical testing was done assuming normal distribution as it was felt that there would not be too big of an error by treating the data as such.

The next focus was on correlations within the data to see if any HHC quality measures correlated with a state’s readmission ratio.  A heatmap was plotted, and from it, variables with stronger correlations (0.15 or above) were further evaluated.  A scatter plot, including linear regression line and Pearson Correlation Coefficient was created for each of the variables designated with a stronger correlation.

Finally, the variables associated with stronger correlations were analyzed to see if they were statistically significant.  Using an alpha of 0.01, statistically significant correlations were flagged as being potential answers in determining how HHC can reduce hospital readmissions.

![Figure 1-1](https://github.com/jsking751/Capstone_1/blob/master/Figures/rr_hist1.png "Figure 1-1")
![Figure 1-2](https://github.com/jsking751/Capstone_1/blob/master/Figures/rr_cdf.png "Figure 1-2")
![Figure 1-3](https://github.com/jsking751/Capstone_1/blob/master/Figures/rr_hist2.png "Figure 1-3")
***
**Findings:** 

What was discovered was both expected and surprising.  Most significantly, that there is no correlation between star rating and readmission ratio.  Moreover, the statistically significant findings can be grouped into two bins: positively correlated and negatively correlated.

The negatively correlated measures (Figure 2-1 and 2-2) were associated with preventative care measures.   Specifically, higher flu and pneumonia shot ratings.  This was expected as the whole purpose of preventative care is to prevent serious illness that would require more extensive care or hospitalization.

The positively correlated measures (Figures 2-3 – 2-6) were associated with the client improving.  Specifically, with regards to improved movement, healing, ability to take oral medications, and a decrease in movement pain.  This was highly unexpected as these ratings suggest that the client is recovering, or improving in their health. 
***
**Conclusion:**

There appears to be both expected and unexpected relationships between HHC quality measures and readmission ratios.  These strong relationships will help craft a story to help healthcare providers reduce hospital readmissions, and open up the door to future research on the subject.<br>

![Figure 2-1](https://github.com/jsking751/Capstone_1/blob/master/Figures/flu_shot.png "Figure 2-1")
![Figure 2-2](https://github.com/jsking751/Capstone_1/blob/master/Figures/pneumonia_shot.png "Figure 2-2")<br>

![Figure 2-3](https://github.com/jsking751/Capstone_1/blob/master/Figures/move_buff.png "Figure 2-3")
![Figure 2-4](https://github.com/jsking751/Capstone_1/blob/master/Figures/healing_buff.png "Figure 2-4")
![Figure 2-5](https://github.com/jsking751/Capstone_1/blob/master/Figures/oral_rx.png "Figure 2-5")
![Figure 2-6](https://github.com/jsking751/Capstone_1/blob/master/Figures/pain_debuff.png "Figure 2-6")