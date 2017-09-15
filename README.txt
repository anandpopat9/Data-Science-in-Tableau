TERM PROJECT
=======================================================================================
Participant-1: Anand Prashant Popat (UBIT: apopat)
Participant-2: Omkar Neogi (UBIT: omkargur)
=======================================================================================
ACTIVITY-1:
As per the vignette. Published on tableau public server. 
PATH: “activity1->”. 3 workbooks are present. One for exercise1, exercise2and3 and exercise4.
=======================================================================================
ACITIVITY-2:
Data: USNews University rankings.
Data Source: Overall rankings - left_join - Computer engg. rankings
	     Overall rankings - left_join - Electrical engg. rankings
	     Overall rankings - left_join - Industrial engg. rankings
	     Overall rankings - left_join - Mechanical engg. rankings

New calculated fields for ranks of all the departments are calculated removing “#” and “Tie” and converting the ranks to numerical field.

All the other fields that contained numbers are converted to numerical fields.

ANALYSIS: 
1) Comparing ranks of different departments of Universities.
2) Given this particular information only, determine the number of students per faculty member i.e student-faculty ratio.
3) Know how much does the recruiter assessment score depends on Research expenditure of a school through trend lines.
4) Representation of universities based on overall_rank and acceptance rate for better insight into choosing the university.

SHEET-1: Acceptance Rate
A bars graph to show the acceptance rate of each university.

SHEET-2: QuadChart
Showing distribution of overall_rank vs acceptance rate using scatter plot. Quad chart is prepared to summarise which university to target. For e.g. Apply to a university which has  a good rank and high acceptance - meaning better chance to get into a good university. Known through quadrant 4 of quad chart.

SHEET-3: Overall rank + acceptance rate
Another representation of overall ranks and acceptance rates of different universities using bars graph. Bars represent the rank while dots represent the acceptance rate. Can compare how it varies for different universities.

SHEET-4: Ranks
Side by Side bars to represent the ranks of different departments in universities sorted in ascending order meaning best universities first. An average line is drawn which is different for each department. Left joins done earlier while preparing data source is used for this sheet to get the ranks and represent in a single sheet.

SHEET-5: PhDs granted
A bar graph of the PhDs granted by the universities.

SHEET-6: Num of faculty
Given the data we have, a calculated field is created to predict the number of faculty in a university. The formula: Total Research Expenditure/Research Expenditure on each faculty. Based on no other information, this can give an estimate of the number of faculty in the university. A bar graph is plotted for the number of faculty at each university.

SHEET-7: Ratio
Two more calculated fields are created. 1) Total_students: Graduate students + PhD students. (Data does not contain the number of undergraduate students) 2) Student faculty ratio: Total Students/Num of faculty. Bar graph of the ratio vs university is plotted with different colours for ratio and the size of ratio.

SHEET-8: Recruiter Score
Bar graph of recruiter assessment score and the universities.

SHEET-9:
Trend Lines on the graph of recruiter assessment score vs school expenditures on research to know how much a recruiter assessment score depends on research expenditure. The y-intercept is forced to be 0. For any point on x axis: y axis point can be calculated from the equation of the trend line:
Recruiter assessment score (out of 5) = 2.24248e-08*Engineering school research expenditures (2016 fiscal year)
p-value < 0.0001 which is good.
R-squared: 0.61453

DASHBOARD:
Contains 4 sheets: Overall rank + acceptance rate, QuadChart, Trend Lines, Ratio.

STORY:
Story has all the sheets described here as story points.

======================================================================================
ACTIVITY-3
Rserve() is needed for this activity.
R connection with Tableau is also needed for this activity.

SHEET-1: Cluster1
Clustering the universities over overall acceptance rate and research expenditure to find similar universities. 4 clusters are made. School name is labeled and is shown as a detail.

SHEET-2: Cluster2
Continuing on activity2, this is the cluster which shows the similarities between universities using scatter plot on overall rank and acceptance rate. Clustering divides the plot into 4 clusters which can be interpreted as dividing the universities into 4 tiers, Tier-1, Tier-2, Tier-3 and Tier-4 universities.
For e.g, Northeastern University and University at Buffalo are similar based on rank and acceptance rate…

More analysis is done on overall rank and acceptance rate scatter plot to find given some acceptance rate of the university what would be its overall rank.

Trend lines are used for this.

SHEET-3: Linear TL
Shows the Linear trend lines on overall rank and overall acceptance rate.
Eq: overall_rank = 191.027*Overall acceptance rate + 1.53325
p-value: < 0.0001
R-squared: 0.4959

SHEET-4: Log TL
Shows the Logarithmic trend lines on overall rank and overall acceptance rate.
Eq: overall_rank = 64.1103*log(Overall acceptance rate) + 142.036
p-value: < 0.0001
R-squared: 0.4945

SHEET-5: Exp TL
Shows the Exponential trend lines on overall rank and overall acceptance rate.
Eq: ln(overall_rank) = 3.89856*Overall acceptance rate + 2.54512
p-value: < 0.0001
R-squared: 0.3983

SHEET-6: Poly TL
Shows the Polynomial trend lines on overall rank and overall acceptance rate.
Eq: overall_rank = -1385.12*Overall acceptance rate^3 + 1487.33*Overall acceptance rate^2 + -258.646*Overall acceptance rate + 37.4406
p-value: < 0.0001
R-squared: 0.5395

Clearly, the R-squared value of Polynomial Trend Line is better than other forms of TL by a little margin. So the best predicted value of point on y-axis can be derived using equation: 
overall_rank = -1385.12*Overall acceptance rate^3 + 1487.33*Overall acceptance rate^2 + -258.646*Overall acceptance rate + 37.4406

DASHBOARD-1:
Shows the sheets of all the different forms of trend lines in one dashboard for comparison.

SHEET-8: Predicted acceptance
Based on overall rank, we tried to predict the acceptance rate of the universities.
For this, a calculated field is created called predicted acceptance rate which needs a connection to Rserve. It uses R for Regression.

The formula: 
SCRIPT_REAL('
overall_rank <- .arg1;
a <- .arg2;

l <- lm(a ~ overall_rank)
l$fitted
'
,
SUM([overall_rank]),
SUM([Overall acceptance rate])
)

Based on the predicted acceptance, we compared the actual acceptance rate and predicted acceptance rate using bars as actual acceptance rate and circles as predicted acceptance rate on a dual axis with synchronized axis.

Another calculated field is created which is called the acceptance rate variance.
Formula: [predicted acceptance rate] - SUM([Overall acceptance rate])

This is to measure the variance of the rate and it is described as the colour of the circles on the plot.

DASHBOARD-2:
This dashboard includes the cluster2 - clustering on overall rank and acceptance rate, polynomial trend line on it and the predicted acceptance rate to actual rate with variance plot.

STORY:
Story has all the sheets described here as story points.
========================================================================================
ACTIVITY-4:
The channel through which this data is available is tableau public server:
https://public.tableau.com/profile/anand.popat#!/
except activity3 as it contains R script and cannot be published on public tableau server.

All the activities including activity3 are also served on private tableau server. 

The data input format and expected output details can be known from the public server and this README file.

=========================================================================================


