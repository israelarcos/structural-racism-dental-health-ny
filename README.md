# Structural racism in the dental health of New Yorkers

# Abstract 
It is known that structural racism negatively affects the health of Non-white populations in the U.S. For example, it is known
that U.S. Black populations experience a higher burden of oral diseases. The objective of this project is to determine if this 
phenomenon is the same in other populations of color, specifically in New York State. We use data analysis techniques to determine if there is a relationship between a person's skin color and their dental health. We make a descriptive study of the data and provide maps that allow us to visualize the level of dental health in New York. 


# Data Collection and Pre-processing
We search for free databases on the Internet. Our goal was to find data related to the ethnography of New York State and the dental health of its inhabitants. 

The first website we consulted was the site for Centers for Disease Control and Prevention (CDC).
From here we found summary data regarding three categories:
- Adults aged 18+ who have visited a dentist or dental clinic in the past year
- Adults aged 65+ who have lost all of their natural teeth due to tooth decay or gum disease
- Adults aged 65+ who have lost six or more teeth due to tooth decay or gum disease

[Source 1](https://nccd.cdc.gov/oralhealthdata/rdPage.aspx?rdReport=DOH_DATA.ExploreByLocation&rdProcessAction=&SaveFileGenerated=1&islLocation=36&rdICL-iclTopic=ADT&iclTopic_rdExpandedCollapsedHistory=&iclTopic=ADT&islYear=2018&hidLocation=36&hidTopic=ADT&hidYear=2018&irbShowFootnotes=Show&rdICL-iclIndicators=ADT1_1%2cADT1_3%2cADT1_4&iclIndicators_rdExpandedCollapsedHistory=&iclIndicators=ADT1_1%2cADT1_3%2cADT1_4&hidPreviouslySelectedIndicators=&DashboardColumnCount=2&rdShowElementHistory=&rdScrollX=0&rdScrollY=0&rdRnd=86496)

This data could not be exported so we made our own csv files with the information provided. 

The final website we use was the one for the Department of Health. We use the data from New York State Community Health Indicator Reports 
(CHIRS). From this, we get the following datasets in xls format:
- [Percentage of 3rd grade children with caries experience](https://webbi1.health.ny.gov/SASStoredProcess/guest?_program=/EBI/PHIG/apps/chir_dashboard/chir_dashboard&p=it&ind_id=Lg84) 
- [Percentage of 3rd grade children with untreated caries, 2009-2011](https://webbi1.health.ny.gov/SASStoredProcess/guest?_program=/EBI/PHIG/apps/chir_dashboard/chir_dashboard&p=it&ind_id=Lg85) 
- [Percentage of 3rd grade children with dental sealants, 2009-2011](https://webbi1.health.ny.gov/SASStoredProcess/guest?_program=/EBI/PHIG/apps/chir_dashboard/chir_dashboard&p=it&ind_id=Lg86)
- [Percentage of 3rd grade children with dental insurance, 2009-2011](https://webbi1.health.ny.gov/SASStoredProcess/guest?_program=/EBI/PHIG/apps/chir_dashboard/chir_dashboard&p=it&ind_id=Lg87)
- [Percentage of 3rd grade children with at least one dental visit in last year, 2009-2011](https://webbi1.health.ny.gov/SASStoredProcess/guest?_program=/EBI/PHIG/apps/chir_dashboard/chir_dashboard&p=it&ind_id=Lg88)
- [Percentage of 3rd grade children reported taking fluoride tablets regularly, 2009-2011](https://webbi1.health.ny.gov/SASStoredProcess/guest?_program=/EBI/PHIG/apps/chir_dashboard/chir_dashboard&p=it&ind_id=Lg89)
- [Caries outpatient visit rate per 10,000 - Aged 3-5 years, 2016-2018](https://webbi1.health.ny.gov/SASStoredProcess/guest?_program=/EBI/PHIG/apps/chir_dashboard/chir_dashboard&p=it&ind_id=Le1)
- [Percentage of children (aged 2-20 years) with at least one dental visit in government sponsored insurance programs, 2018](https://webbi1.health.ny.gov/SASStoredProcess/guest?_program=/EBI/PHIG/apps/chir_dashboard/chir_dashboard&p=it&ind_id=Lg116)
- [Oral cavity and pharynx cancer incidence rate per 100,000, 2015-2017](https://webbi1.health.ny.gov/SASStoredProcess/guest?_program=/EBI/PHIG/apps/chir_dashboard/chir_dashboard&p=it&ind_id=Lg3)

# Data Cleaning
We use Google Colab with Jupyter Notebooks to clean the data using standard functions from Pandas library.
[Data Cleaning Jupyter Notebook](https://colab.research.google.com/drive/1YBiOc48Iv9LR2r-BgBdoy9x6nv21wgWp?usp=sharing)

