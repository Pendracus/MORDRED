# MORDRED (Model Of Resource Distribution and Resilient Economic Development) Model Documentation
Here we will upload an exhaustive model documentation which will be updated regularly.
# Documentation structure
1. MORDRED-1.0 Structure
   1. Demography
   2. Economy
   3. Labor
   4. Energy
   5. Land
   6. Stressors
   7. Climte
2. MORDRED-1.0 Model Data
     1. Demography
     2. Economy
     3. Labor
     4.  Energy
     5.  Land
     6.  Stressors
     7.  Climte


<details>
           <summary>MORDRED-1.0 Structure</summary>
           <p> The MORDRED IAM consists of various interrelated modules.
              ![MODEL Representation](https://www.markdownguide.org/assets/images/tux.png)
              </p>
         </details>


# 2. MORDRED-1.0 Model Data
## 2.1. Demography
### 2.1.1. Initial population
* Raw data: United Nations, Department of Economic and Social Affairs, Population Division (2019). World Population Prospects 2019, Online Edition. Rev. 1. File POP/7-1: Total population (both sexes combined) by five-year age group, region, subregion and country, 1950-2100 (thousands), https://population.un.org/wpp/Download/Files/5_Archive/WPP2019-Excel-files.zip. File: WPP2019_POP_F07_1_POPULATION_BY_AGE_BOTH_SEXES.xlsx. The data for 2020 were taken because there are no data for 2019. 
* The data was matched to all the countries aggregated in Exiobase3. For countries that were included in Exiobase but not in the UN World Population Prospects, population was set to zero (cf section xx).  
* There are 21 age categories in the raw data (from 0-4 years, 5-9 years, 10-14 years, …, 95-99 years, 100+years). In the MEM, there are 20 age groups (from 0-4 years, 5-9, 10-14, etc., with the last category being people aged 95+). Thus, the last two age groups were aggregated. For every age group, the population of the respective countries was aggregated into the three MEM world regions (cf. section xx). 

### 2.1.2. Initial population in the formal and informal economy
The total initial population in the three world regions and in the 20 age groups were further sub-divided into population working in the formal economy and population working in the subsistence (or informal) economy.
* We assume that globally, at least 800 million people live not fully integrated or even apart from the ‘formal’ global economic structure in different forms of subsistence regimes, including small peasants, fishermen, the rural and urban poor etc. (xx). We chose the number 800 million because it is estimated that 800 million people live in extreme poverty (xx) and there is a high intersection between the extreme poor and those living in subsistence regimes (xx). 
* For simplicity, we assume that (1) the share of people living in subsistence regimes does not differ according to age group and gender, and that (2) the great majority of people living outside the formal economy lives in the periphery, and the remaining people live in the semiperiphery. Given the lack of exact data, we operationalize these qualitative assumptions by matching 85% of the population living under a type of subsistence regime to the periphery, and 15% to the semiperiphery.  
* $ \text{subsistence class}_{age,i} =share_i * population_{age,i}$ with $age \in \{0-4,5-9,…,95+\})$ and $i \in \{semiperiphery,periphery\}$; $$share_1=0.15,share_2=0.85 $$ 
* These people pertain to the ‘subsistence class’ (cf. xx) which is characterized by high but stable mortality and fertility rates and very low but stable per capita consumption through the formal economy. Fertility and mortality rates for the different age groups for the subsistence class are computed by using the respective regression functions (cf. section xx) and the per capita consumption of the subsistence class which is approximated by using the [World Bank’s extreme poverty line](https://databank.worldbank.org/metadataglossary/gender-statistics/series/SI.POV.DDAY) (2.15$ in 2017-PPP, converted to 1.997 (2019-)€ per day) which gives a per capita consumption of 729 2019-€ per year.
* The remaining population in center, semiperiphery and periphery lives within the formal economy and is matched to one of three classes within each MEM region (cf. section xx). 






