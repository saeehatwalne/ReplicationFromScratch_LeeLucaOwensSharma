# ReplicationFromScratch_LeeLucaOwensSharma
Replication exercise: Can Alcohol Prohibition Reduce Violence Against Women? By Dara Lee Luca, Emily Owens, and Gunjan Sharma*
This project was a part of the econometrics course. Here I have tried to match the authors' regression tables by attempting to clean the NFHS-3 from scratch.
Note: This was a part of a group project. Out of my group of three, I was responsible for the entire code.

# Introduction
The paper titled ‘Can Alcohol Prohibition Reduce Violence Against Women?’ is authored by Dr. Dara
Lee Luca (Senior Economist at Amazon), Dr. Emily Owens (Chair, Department of Criminology at UC
Irvine) and Dr. Gunjan Sharma (Asst. Professor at Smith College). It was published in the American
Economic Review in 2015 in Volume 105 and Issue 5.

Main research goals of the paper:
To study the impact of alcohol prohibition state laws on the following:
• Alcohol drinking behaviour of husbands in households
• Domestic violence against women
• Crimes against women (fatal and nonfatal crimes, and other types of crimes)

# Datasets used
The authors of the paper utilized three main datasets to investigate the impact of alcohol prohibition on
alcohol consumption and violence against women in India.

* National Family Health Survey (NFHS):
NFHS-2 conducted in 1998-1999 and NFHS-3 from 2005-2006 are the two datasets
used. These panel surveys provide rich microdata on household members' alcohol
consumption, as well as information from a subset of women on their experiences with
and attitudes toward intimate partner violence.

* Independently Collected Data: collated together
Data pertaining to literacy rates, percentage of male population, police expenditures in
states, percentage of urban population etc. for every state for every year is collated
through independent research.

* State GDP per capita and government expenditure on education and welfare from the
Reserve Bank of India. State level unemployment rates, urbanization, and literacy rates
are interpolated from the Decennial Census of India, collected in 1981, 1991, 2001 and
2011

* National Crime Records Bureau (NCRB) Data from 1980-2010: Information on
various crimes targeted towards women, such as rape, sexual harassment, molestation,
cruelty by husband and relatives, accidental deaths by fire, and dowry deaths.

# Brief description of authors’ sample & sample restrictions
The study sample in this paper consists of married women aged 15-49 (both included). The sample is
drawn from the Indian National Family Health Survey (NFHS) conducted in 1998-1999 and 2005-2006.
The NFHS-2 and NFHS-3 panel data together spans a total 109,936 observations across 5 years viz.
1998,1999,2000,2005 and 2006. Data from 36 States and Union Territories is included. From these,
53,697 are from the years 1998-2000 whereas the remaining 55,395 are from years 2005-06. However,
for regressions, the observation count are around 77,800 for the authors.

Although the authors have not mentioned any steps as to exactly how they have arrived at their sample,
trial and error of getting close to their observations makes us logically believe that they have used
married women (including, who were selected for and actually interviewed for the domestic violence
module as their ultimate sample across all the states. The state wise NCRB data comprises 1080
observations in total. The data includes information on crimes targeted towards women, such as rape,
sexual molestation, sexual assault, cruelty by husband and relatives, accidental deaths by fire, and
dowry deaths for each state for each year.

# Matching authors’ data: Process, challenges, assumptions, critical comments

## NCRB Data – Procedure, assumption, challenges:
We obtained crime data from annual reports published by the National Crime Records Bureau (NCRB),
which compile various criminal incidents reported across different states in India. The annual reports
document all information and are available in State wise report chapters.

The absolute numbers of crimes such as rape, dowry death etc. were directly extracted from the'Incidence Of Crimes Committed Against Women' reports. Each of these crimes is categorized into subgroups denoted by the columns labelled as I, P, and R. For our analysis, we used the figures listed under the I column. We matched the value with the author's values and figured out that the authors have used the I column for their crime data. With respect to state-wise population data, we initially checked Census values, however, we later cross-tallied and figured out that the author has used yearly population data available in the NCRB reports themselves. To calculate the crime rates, we divided the absolute number of crimes by the population of the respective state in the corresponding year and multiplied the result by 10,000. The authors have developed three indices related to women's issues: the Women Index (women_index), Women Index Non-Fatal (women_index_nf), and Women Index Fatal (women_index_f). The Women Index Fatal is computed by aggregating fatal crimes like suicide, fire-related deaths, and dowry deaths. In contrast, the Women Index Non-Fatal is derived from aggregating non-fatal crimes, including rape, molestation, sexual harassment, and cruelty by husbands and relatives. The Women Index is then calculated by combining both the indices. As no information pertaining to such indices was not provided in the paper, we cross-tallied values and figured out the formulae to be applied.

In the context of another research paper by the same authors based on a similar topic we discovered
that they have interpolated values of unemployment rate, urbanization and literacy from the Decennial
Census of India State level collected in 1981, 1991, 2001 and 2011 (Luca et al., 2015a). We have tried
collating data independently through this where ever we could, and have referred to the author’s data
when we could not find an appropriate value match. Despite our efforts to obtain state- and year-wise
data for these variables, we have encountered quite a few challenges.
Alcohol prohibition status of states involved collecting data on laws. Hence this primary data was
directly sourced from the author’s dataset.

## Some critical comments on authors’ crime data used

The dataset provided by the authors lacks values, particularly for Union Territories (UTs), with Delhi
being one of them. Delhi stands out with one of the highest crime rates in India, making it crucial to
include its crime data for a comprehensive analysis. Hence, in our regression analysis, we have made
use of this data for Delhi which was readily available, which is also a potential source of differences in
the coefficients. The authors do not specify why they have omitted data for these Union Territories even
though the data is available on the NCRB portal. In the original paper on page 628, there is a typing
error of categorizing all types of crimes as non-fatal, which is quite surprising. Through the codes we
have understood that rape and molestation are listed as nonfatal crimes. However, it might be possible
that some of these crimes are also fatal. In such a case, labelling a whole category of crimes as non-
fatal might not be the best.

## NFHS Data – Procedure, assumption, challenges

In NFHS-2 (1998-99-2000), the variable indicating whether a woman's husband drinks or not was not
available in the women's file, unlike in NFHS-3. To address this gap, we merged the household person's
recode file with the individual women's file. The household person's file provided the drinking status
of all individuals in the household. Each woman may have had a different husband, and their relationship to the household head varied. There was no universal rule that could be applied to all
women in this regard. Upon reaching out to the author’s they advised that exact matching was not
possible for NFHS-2. Hence, due to feasibility and time constraints, we have considered the author’s
data of NFHS-2 and appended it to our cleaned NFHS-3 data.

In NFHS-3 a sample of married women interviewed for domestic violence yields a sample of 65,610.
Even after dropping variables, missing values, values in which women didn’t know the answer to any
question, we were still left with 62,901 observations. Upon analyzing how we could get to the authors’
sample size, we also encountered that in author’s data for 2005-06, we consistently found that even in
multiple religion categories our observations were more by around 1000. When we tried removing
observations in which the respondent was not working (since author just mentions white collar job or
not, doesn’t mention unemployed), we were left with around 26,000 observations. Hence, this was not
an option either. Thus, we took a logical and practical decision to continue with a sample size of around
62,000 for NFHS-3 data.

In the NFHS 3, the authors have not provided any information on the specific values that were excluded
from the analysis. Additionally, despite excluding missing values, we still encounter discrepancies in
the sample counts, resulting in variations in the number of observations.
Additionally, Uttaranchal, which was formed in 2000, was not included as a separate entity in the 1998-
99 data. However, in NFHS-3, segregation between Uttaranchal and UP was introduced. Given that the
authors did not treat Uttaranchal as a distinct entity, we have not used Uttaranchal in NFHS-3 for
analysis and merging purposes. Furthermore, since the definition of a white-collar job was not provided
by the authors, we made assumptions based on the occupations listed in the report. For instance,
professional, clerical, sales, service jobs etc. were deemed as white collar jobs. Other indicators such as
age gap categories, education gap categories relative to the husband are prepared newly upon analyzing
the author’s dataset.
Hence, these are factors which are bound to affect our regression estimates.
