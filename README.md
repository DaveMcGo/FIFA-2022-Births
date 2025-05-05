# Exploring Footballer Birth Dates Through Data Science


## Executive Summary

In this project, I looked into whether the birth month of footballers has any impact on their chances of becoming professionals. Similar patterns have been noted in studies on educational performance, where *“being the youngest in the school-entry cohort has an impact on self-confidence, notably on self-perceived competence and self-efficacy, and also on future education outcomes.” (Givord, 2020)*

Like many, with football being the global game, it’s a topic I am interested in, so was able to bring my basic knowledge. In addition, having spent many a Saturday morning stood on the sidelines, as a parent, watching youth football matches of varying quality, the physical mismatch between some of the players has been extremely evident.

Using publicly available data on football players' birth dates, my analysis shows that birth months are not evenly distributed. Globally, more professionals are born from January to March, with fewer in October to December. In English and Welsh football, there are significantly more professionals born in the early months of the academic cohort, and fewer in the later months.

Further research should examine the seasonality of birth rates across the entire population and consider more nationalities regarding youth football eligibility. Currently, in England and Wales, young footballers can compete in an older age group if they possess the requisite skills. It might be worthwhile to allow summer-born players to compete in a younger age group. If these summer-born players are dropping out due to physical disadvantages rather than a lack of ability, this adjustment could provide them with a fairer opportunity. This approach might enable skilled summer-born players to succeed rather than less talented but more physically developed autumn-born players.





## Data Infrastructure & Tools

The dataset for this project was sourced from https://www.kaggle.com/datasets/stefanoleone992/fifa-22-complete-player-dataset which includes detailed data on football players' birth dates and nationalities from the EA FIFA games (FourFourTwo, 2021). As all the data is public, GDPR and privacy issues weren’t a concern.

Initially, I considered Power BI for its ease of use in visualisations, but it lacked advanced statistical tools. So, I chose Python for its robust data science capabilities, using libraries like Pandas, NumPy, Matplotlib, Seaborn, Ydata_profiling, and SciPy (VanderPlas, 2016). Python requires setting up your own programming environments, which can be tricky without administrative permissions (McGowan, 2025). Security concerns are significant, especially for those engaging with the latest Generative AI advancements (Spracklen et al., 2025). See also AI code suggestions sabotage software supply chain • The Register

- The Python libraries I used in this project were:

- Pandas and NumPy for data handling and manipulation

- Matplotlib and Seaborn for visualisations

- Ydata_profiling for exploratory analysis

- SciPy for advanced statistical analysis





## Data Engineering

I only used the FIFA 2022 data from the multiyear Kaggle dataset because it has the latest information and avoids duplication of footballers who appear in multiple years. Initial exploratory data analysis (EDA) helped me identify what was available and what additional data was needed.

Out of the dataset's 110 columns, I picked the ones necessary for my analysis:



The following were retained for further data verification, if needed:

	Club_name, league_name, league_level

Additional calculated columns were added to aid analysis:



### Country Groups

I also added an extra 'country_group' column to differentiate England and Wales from the rest of the world, which was crucial for comparing them against the global dataset. Initially, I aimed to compare the UK with the rest of the world based on my knowledge of England's youth eligibility rules, which align with the academic year from 1 September to 31 August. However, further investigation revealed:

England and Wales follow the same academic year (Gov.uk, 2025) and youth eligibility (Welsh FA, 2024).

Scotland's academic year starts in mid-August, with more complex year group cut-offs (Gov.scot, 2025).

Northern Ireland also begins its academic year in September, but again with more complex eligibility cut-offs (nidirect.gov.uk, 2025).



### Brazilian Players

I found an anomaly of a suspiciously high number of footballers listed with a birthdate of 29 February. Upon investigation, I discovered that almost all of these leap day birthdays belonged to Brazilian players who weren't real (Dorn, 2024), they were just made up to deal with EA not having the rights to use their images. Consequently, I removed Brazilian players from the analysis.



### Outliers

After analysing the ages of players, the dataset showed a right-skewed normal distribution with few younger and older footballers. To ensure fair representation, I excluded those below the 5th percentile and above the 95th percentile, leaving an age range of 19 to 34 years.



## Data Visualisation & Dashboards



Figure 1 Violinplot comparing age distribution of footballers, at the start of the 2021-22 academic year, split between "Rest of World" and "England+Wales". Both have a median age of around 25 years and a similar age spread.



Figure 2 Boxplot comparing age at the start of the academic year 2021-22 split between "Rest of World" and "England+Wales". It displays the median, interquartile range, and potential outliers more clearly.







Figure 3 Bar chart showing the distribution of footballers by age, the highest concentration’s around 21-23. Distribution is right-skewed, with a long tail indicating fewer footballers at older ages.





Figure 4 Barchart showing the number of footballers born each quarter for the "Rest of World." Births are highest in Q1 (Jan-Mar) and decline steadily through to Q4 (Oct-Dec). An even distribution of births would be 1,272 each month.





Figure 5 For England & Wales births are highest in September and October and decline through Q4 (Jun-Aug). Compared to the "Rest of World," the peak birth period follows the academic year rather than calendar year. The even distribution would be 142 births per month.



## Data Analytics

Figure 4, for “Rest of World” shows considerable variation in monthly birth rates compared to an even distribution throughout the year. The higher months are at the beginning of the calendar year and the rate is lower-than-average throughout the second half.

Figure 5, for “England+Wales” also shows a considerable difference. In contrast to the “Rest of World”, the higher months are at the beginning of the academic year, with lower-than-average numbers at the end.

### Testing for Statistical Significance

To determine if these differences are statistically significant, I performed the Chi-Squared (χ²) Goodness-of-Fit test using SciPy in Python. The similar Fisher Exact Probability Test was considered, but since all expected and observed values were greater than five, the Chi-Squared test was more appropriate.

### The Concept

Null Hypothesis (H₀): The births of footballers are uniformly distributed across all 12 months. Any observed variation is merely random chance.

Alternative Hypothesis (H₁): The births of footballers are not uniformly distributed across the 12 months. The observed pattern is statistically significant.

The test compares observed counts for each month to the expected counts (what would be expected if the null hypothesis were true). If the difference between observed and expected is large enough, the null hypothesis is rejected (Lowry, 2023).

### Results

The tests were conducted on each subset of data:



Using the usual significance threshold of 0.05 for the p-value, I can reject the null hypothesis for both subsets. This means that the distribution of birth dates among football players is quite different from what we'd expect in a uniform distribution.



## Recommendations for Future Iterations

For future research, I'd like to include female footballers and investigate the dates other countries use for youth football teams and see if there's a similar pattern in footballers' birth months in those countries. It'd also be beneficial to check if the seasonality of birth rates in a country's whole population plays a role.

Another idea is to explore the dataset's overall column, which scores a footballer's ability. There might be a link between this and their birth month. If there's a strong correlation, it could help football academies understand and nurture young talent better.

Moreover, expanding this research to different sports could be interesting. For instance, looking at birth month distributions among Gaelic Football or rugby players might show whether this phenomenon is specific to football or common across various sports.



The Jupyter Notebook and data used for ‘Exploring Footballer Birth Dates Through Data Science’ can be found at the following:

https://davemcgo.github.io/portfolio/ 







References

Dorn, J. (2024) Why Isn‘t Brazil On FIFA 22? Unpacking A Conspicuous Absence - ExpertBeacon. Available at: https://expertbeacon.com/why-isn-t-brazil-on-fifa-22/ (Accessed: 13 April 2025).

FourFourTwo (2021) FIFA 22: Player ratings explained, fourfourtwo.com. Available at: https://www.fourfourtwo.com/features/fifa-22-player-ratings-explained-chemistry-fut-ultimate-team-pace-passing-speed-card (Accessed: 15 March 2025).

Givord, P. (2020) ‘How a student’s month of birth is linked to performance at school: New evidence from PISA’. Available at: https://doi.org/10.1787/822ea6ce-en (Accessed: 8 March 2025).

Gov.scot (2025) Attending school. Available at: https://education.gov.scot/parentzone/my-school/general-school-information/attending-school (Accessed: 23 March 2025).

Gov.uk (2025) School admissions, GOV.UK. Available at: https://www.gov.uk/schools-admissions/school-starting-age (Accessed: 23 March 2025).

Lowry, R. (2023) Ch8 Chi-Square, Pt 1, Concepts & Applications of Inferential Statistics. Available at: http://vassarstats.net/textbook/ch8pt1.html (Accessed: 19 April 2025).

McGowan, D. (2025) Personal Experience of Anaconda and Jupyter Notebooks set up on laptop provided by employer. Cambridge: Unpublished.

nidirect.gov.uk (2025) Compulsory education | Department of Education. Available at: https://www.education-ni.gov.uk/articles/compulsory-education (Accessed: 1 May 2025).

Spracklen, J. et al. (2025) ‘We Have a Package for You! A Comprehensive Analysis of Package Hallucinations by Code Generating LLMs’. arXiv. Available at: https://doi.org/10.48550/arXiv.2406.10279.

VanderPlas, J. (2016) Python Data Science Handbook: Essential Tools for Working with Data. O’Reilly Media, Inc.

Welsh FA (2024) ‘Small-Sided-Football-Regulations-24-25-V2.pdf’. Available at: https://media-faw-cymru.s3.eu-west-2.amazonaws.com/faw/20240906101438/Small-Sided-Football-Regulations-24-25-V2.pdf (Accessed: 23 March 2025).


