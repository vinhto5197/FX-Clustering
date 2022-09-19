# FX-Clustering
Exploration of Foreign Exchange (FX) log-return structure Pre- and During- COVID

## Requirements
`R` and `RStudio` installed as we will call clustering functions from `R`

`rpy2` corresponding to version of `R`

Library `factoextra` installed in `R`. This can be called inside jupyter notebook with `install.packages("factoextra")` after calling `%%R`

## Clustering Foreign Exchange Rates Pre- and During- COVID with distance correlation
### <em>Introduction</em>

This paper focuses on an application of methods used by Martί Renedo and Argimiro Arratia in “Clustering of exchange rates and their dynamics under different dependence measures” (Ref. [1]). Our main task is to see if clustering exchange rates by log returns would reveal insights into their relationships as funding/investment currencies. We use alternative distance correlation to cluster novel FX (Foreign Exchange) time series during the coronavirus pandemic to discover if the groupings/shape of clusters change between the 10 months preceding the pandemic and the 10 months during the pandemic When clustering data from pre- and during-COVID periods, we found an interesting cluster where the pairs have a clear relationship pre-COVID, but during-COVID it is not as clear.

### <em>Data Overview</em>

We utilize daily FX exchange rates across 13 different currencies and all possible pairings between them. The data comes from the federal reserve website (U.S. FRED) and we standardized our data. The original time frame ranged from 01/01/2010 - 12/31/2020. We chose to compare the clustering structure 10 months before (5/02/2019 - 3/02/2020) and after (3/02/2020 - 12/31/2020) lockdowns related to COVID-19. In order to explore this objective, we conducted alternative research to determine which currencies generally carried the lowest and highest interest rates and looked to see if indeed clustering methods would group them together.

### <em>Background</em>

13 of the most traded securities as of April 2013 are included. These include the US Dollar (USD), Euro (EUR), Yen (JPY), Pound Sterling (GBP), Australian Dollar (AUD), Swiss Franc (CHF), Canadian Dollar (CAD), Mexican Peso (MXN), Chinese Yuan, (CNY), New Zealand Dollar (NZD), Swedish Krona (SEK), Hong Kong Dollar (HKD), and Singapore Dollar (SGD). Log returns over a time step were calculated using:

r_t= ln  P_t/P_(t-1)   

Then, through a standardizing technique, converted through the US dollar as an auxiliary step. Specifically, the exchange rate between currencies XXX and YYY where neither of them are USD is:

XXX/YYY =  (XXX/USD)/(YYY/USD)

#### Currency Carry Trade Background

In a currency carry trade transaction, two types of currencies are typically exchanged: Funding currencies and Investment currencies. Funding currencies are typically characterized as having a low interest rate in relation to the high-yielding investment currency. For example, the Japanese Yen (JPY) generally has low-zero interest rates which often lead to FX traders borrowing Japanese Yen as a “funding” currency. Then, the investors would use the borrowed currency to trade for higher spread currencies such as the New Zealand dollar (NZD) or Australian currency (AUD) and invest in assets in the country to benefit from interest rate difference. If the exchange rate remains the same throughout the duration of the investment, then the FX trader will have made a profit.  Another common currency carry trade involves the Swiss franc (CHF) and the Euro (EUR).

Typically, in times of economic crisis, funding currencies will typically outperform the investment currencies because they are seen as a safe haven for holding money.

### <em>Analysis/Results</em> 

Pre-COVID and During-COVID clustering comparison:

We implement 2 separate hierarchical clusterings with complete linkage on two subsets of the original dataset: 10 months before lockdown (05/02/2019 - 02/28/2020) and 10 months after lockdown (03/03/2020 - 12/31/2020). We use distance correlation to measure the similarity between FX pairs. Reciprocal pairs are therefore not included as “correlations detected will be the same for XXX/YYY and YYY/XXX”. We would expect them to be in another cluster compared to the original pairs.

Pre-COVID dendrogram:				

![image](https://user-images.githubusercontent.com/54465320/190936480-8d00bfc1-9ede-4917-915c-1031792553ae.png)

During-COVID dendrogram:

![image](https://user-images.githubusercontent.com/54465320/190936485-634d518f-54f7-46c8-92e5-ec6d3ca90496.png)

<em>Fig. 1: Phylogenetic dendrograms of Pre- and During-COVID data</em>

<em>Colors are meaningless - we are interested in which currency pairs are clustered together before and during COVID</em>

Visually, we can see 3 fairly well-defined clusters in the dendrogram for both the pre-COVID and during-COVID periods. A better visualization of the dendrograms are in circle forms, where we can see more clearly the pairs that have the same numerator currency.

#### Results

Some currencies are generally used as funding currencies because of their low interest rates. In this case, we define whichever currency has a lower interest rate in a pair as a funding currency because there are many pairs where both currencies have low interest rates. 

There are 24 pairs in total whose interest rate differentials pre-COVID are positive (the numerator currency is investment currency, and the denominator currency is funding currency). Of the 24 pairs, 22 pairs are clustered into one cluster (green cluster in Appendix Fig. 3.A), where there are 25 pairs in total. Heuristically, we can see from the pre-COVID dendrogram that many of the numerator currencies have high interest rates (MXN, CNY, HKD). Appendix Table 2.A shows the specific interest rate differentials and clusterings.

This is indicative that the log returns structure of investment/funding pairs pre-COVID is similar: whenever an investment/funding pair has negative/positive log returns, most other investment/funding pairs behave the same way.

During COVID, only 2 pairs in this cluster switch from being investment/funding to funding/investment, but the pairs are no longer concentrated in a single group, being split across all 3 clusters as illustrated in the dendrograms above.  Even the pairs that switch from funding/investment to investment/funding are not as concentrated as they were prior to COVID. This suggests that FX pairs which have the same investment and funding relationships are no longer correlated by their log returns structure. Therefore, the carry trade is no longer consistent during COVID.

One can combine this result with a “COVID severity” indicator/index to formulate an investment strategy. When COVID is expected to be close to over, we can expect that the pre-COVID clustering will be valid again, and we will have a basket of correlated currency pairs in terms of log returns.

#### Problems/Caveats:

We implemented only hierarchical clustering with complete linkage using distance correlation. There could be more relationships to be found if another clustering method was implemented.

### <em>Conclusion</em>

For comparison between pre-COVID and during-COVID, using hierarchical clustering with complete linkage and distance correlation, we found that there is a correlation between the log returns structure between investment/funding currency pairs and thus these pairs are clustered together. The relationship breaks down during COVID, and log returns provide no clear clustering between funding and investment currencies.

</br>
</br>
<em>Citations</em>:
</br>
[1] Arratia, A., & Renedo, M. (2014, April). Retrieved March 10, 2021, from 
https://www.cs.upc.edu/~argimiro/mypapers/Journals/MRARmidas16final.pdf
[2] FRED. “FRED: St. Louis Fed Interest Rate Data.” FRED, 
fred.stlouisfed.org/searchresults/?st=exchange+rate. 
[3] Interest rates - long-term interest rates - oecd data. (n.d.). Retrieved March 10, 2021, from 

https://data.oecd.org/interest/long-term-interest-rates.htm
[4] Singapore average overnight Interest RATE 1988-2020 data: 2021-2023 forecast. (n.d.). 
Retrieved March 10, 2021, from https://tradingeconomics.com/singapore/interest-rate

</br>
</br>
<em>APPENDIX</em>

![Untitled](https://user-images.githubusercontent.com/54465320/190936783-b2a51c86-ad6f-4bc4-a3cf-c34377e43a0b.png)
</br>
Table 1.A: Short Term Interest Rates by Country during our data period and during pre/post the beginning of the coronavirus pandemic

For the time frame of interest, the interest rates for each bucket are an historical average of the short term interest rates of the countries included in each cluster. Where we see a clear separation between investment currencies with high interest rates and funding currencies with low interest rates, we can speculate that a carry trade would be feasible.

![image](https://user-images.githubusercontent.com/54465320/190936860-4b86fa9e-838f-44ba-9abc-891d4aca1019.png)

Table 2.A: Green cluster numbers

</br>
Pre-COVID clustering of currency pairs:

![image](https://user-images.githubusercontent.com/54465320/190936882-46190c09-09c2-4d97-a4ec-1033835c4f9d.png)

During COVID clustering of currency pairs:

![image](https://user-images.githubusercontent.com/54465320/190936932-d1ebb9f5-1a31-4980-a1a1-12aa9f91edf4.png)

Figure 3.A: Circle dendrograms of Pre- and During-COVID data

(These are included to provide a nice visualization of which clusters the currency pairs fall into pre-and post-COVID lockdowns)
