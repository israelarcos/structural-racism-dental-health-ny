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

#Jupyter Notebook
[Notebook](https://colab.research.google.com/drive/1YBiOc48Iv9LR2r-BgBdoy9x6nv21wgWp?usp=sharing)

# Data Cleaning
The whole process is documented in the notebook above, however let's explain some of the things that we did, here. 
```
def clear_data(df, name):
  #Remove unnamed columns
  cdf = df[['Region/County', 'Percentage (CI)']]
  
  #Remove rows containing the word 'Region'
  cdf = cdf[cdf["Region/County"].str.contains("Region")==False]
  
  #Remove the CI from Percentage (CI) column
  cdf["Percentage (CI)"] = cdf['Percentage (CI)'].replace("[\(\[].*?[\)\]]", "",regex=True)

  cdf = cdf.rename(columns = {'Percentage (CI)' : name}) 

  #Convert the s symbol to na
  
  cdf[name] = cdf[name].replace('s', np.nan)

  # Sort in ascending order just for better reading
  cdf = cdf.sort_values('Region/County')

  return cdf
```
Much of our data contained strings that we did not need, and missing values coded with an s. So we wrote the above function to clean such data. We used regular expressions and Pandas methods to work this out. The function above let us to pass from this
```
	Region/County	Percentage (CI)	Unnamed: 2	Unnamed: 3	Unnamed: 4
0	Region - 1   Long Island	NaN	NaN	NaN	NaN
1	Nassau	27.1 (17.7-36.6)	NaN	NaN	NaN
2	Suffolk	29.6 (15.9-43.3)	NaN	NaN	NaN
3	Region - 3   Mid-Hudson	NaN	NaN	NaN	NaN
4	Dutchess	20.5 (9.4-31.5)	NaN	NaN	NaN
...	...	...	...	...	...
62	Erie	23.2 (15.2-31.3)	NaN	NaN	NaN
63	Genesee	26.7 (13.7-39.6)	NaN	NaN	NaN
64	Niagara	21.4 (12.0-30.8)	NaN	NaN	NaN
65	Orleans	21.4 (12.9-30.0)	NaN	NaN	NaN
66	Wyoming	15.7 (5.6-25.8)	NaN	NaN	NaN
67 rows × 5 columns
```
to this
```
	Region/County	untreatedCaries
12	Albany	11.6
59	Allegany	25.4
43	Broome	42.3
60	Cattaraugus	24.4
36	Cayuga	40.4
61	Chautauqua	32.6
49	Chemung	26.0
44	Chenango	30.6
25	Clinton	31.9
13	Columbia	21.2
37	Cortland	23.5
45	Delaware	31.9
4	Dutchess	20.5
62	Erie	23.2
26	Essex	24.9
27	Franklin	20.5
19	Fulton	NaN
63	Genesee	26.7
14	Greene	13.1
28	Hamilton	NaN
20	Herkimer	42.5
32	Jefferson	29.5
33	Lewis	51.4
50	Livingston	26.3
38	Madison	24.6
51	Monroe	15.6
21	Montgomery	27.4
1	Nassau	27.1
64	Niagara	21.4
39	Oneida	29.0
40	Onondaga	24.9
52	Ontario	17.4
5	Orange	30.0
65	Orleans	21.4
41	Oswego	25.4
22	Otsego	22.4
6	Putnam	19.8
15	Rensselaer	19.7
7	Rockland	22.6
16	Saratoga	20.0
17	Schenectady	NaN
23	Schoharie	NaN
53	Schuyler	14.3
54	Seneca	18.1
34	St. Lawrence	39.5
55	Steuben	23.4
2	Suffolk	29.6
8	Sullivan	52.8
46	Tioga	18.7
47	Tompkins	16.8
9	Ulster	34.2
29	Warren	19.9
30	Washington	38.1
56	Wayne	18.6
10	Westchester	10.1
66	Wyoming	15.7
57	Yates	34.2
```

# Exploratory Data Analysis
We use standard Pandas functions and our statistics knowledge to ask our data for questions such as: Whats is the county with most cases of caries? Make diagrams, etc.
Here are the results.

![image](https://user-images.githubusercontent.com/95376025/144940106-c96d4ae6-e0b3-4693-aa2c-429b1308e566.png)
 In this first figure we see that the difference between people who attended a dentist is notorios for white people, whereas for the other races, the difference is not that strong. So, it is more commen for white people to visit the dentist than for nonwhite people.
 
 ![image](https://user-images.githubusercontent.com/95376025/144940674-bf964df2-f4fe-4e94-b8ce-f408f784dabd.png)
In this figure we see that although there is not too much teeth decay, Black and Hispanic people are more propensous to lose their teeth than white people.

![image](https://user-images.githubusercontent.com/95376025/144941982-29fa6e4a-28b3-4a2b-a465-12405643b6f0.png)
In this graph it is clear that nonwhite people have better oral health after 65 years. Specially Black and Multiracial people, who were the only two groups with more positive cases of lost teeth. 

![image](https://user-images.githubusercontent.com/95376025/145509515-59c650a3-2c57-49a8-8d34-71440d25a4be.png)
We see that the biggest percentages of untreated caries happen in  Sullivan, Lewis and Herkimer. While the smallest ones occur in Albany, Greene and Westchester.

![image](https://user-images.githubusercontent.com/95376025/145512548-63397942-c007-44d2-b9c2-0b5042340bcf.png)
We see that the biggest percentages of caries experience happen in  Madison, St. Lawrence and Chautuqua. While the smallest ones occur in Steuben, Dutchess, and Albany.

![image](https://user-images.githubusercontent.com/95376025/145609426-6eb0bb9f-5e73-401a-bce1-e27e87d55c22.png)
We see that the biggest percentages of dental sealants happen in  Schenectady, St. Lawrence and Wyoming. While the smallest ones occur in Suffolk, Washington, and Schuyler.

![image](https://user-images.githubusercontent.com/95376025/145609442-8f00174b-96e4-4390-88a5-fdcc7d285a93.png)
We see that the biggest percentages of children with dental insurance happen in Fulton, Renssekaer and Madison. While the smallest ones occur in Montgomery, Allegany and Cayuga. 

![image](https://user-images.githubusercontent.com/95376025/145609457-7554e728-f8e7-4203-a02b-2d7a0bb5c7b2.png)

![image](https://user-images.githubusercontent.com/95376025/145609464-26da12b6-b509-4f5c-ac4f-3dfcaf942353.png)

# Results
In counties with more presence of non white people there are more cases of untreated caries and less visits to dentist. So, we can conclude that there is still some structural racism in Oral Health. 

