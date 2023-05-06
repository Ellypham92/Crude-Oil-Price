<div id="header" align="center">
<img width="850" alt="image" src="https://i.ytimg.com/vi/WtLAgUovCIw/maxresdefault.jpg">
</div>

<h3 id="header" align="center">
 Crude Oil Prediction
</h3>


### :globe_with_meridians: Context
The price of oil, or the oil price, generally refers to the spot price of a barrel (159 liters) of benchmark crude oil—a reference price for buyers and sellers of crude oil such as West Texas Intermediate (WTI), Brent Crude, Dubai Crude. We hypothesize that the oil price can be modeled as a weighted lagged moving average of historical oil prices. 
- SPY index and Dollar Index are used as the macroeconomic indicators
- Oil production is used as an indicator of oil supply

We can use it to forecast the short-term oil price which would be useful for the government and companies for planning the budget for the fiscal year.

### Data Processing
<img width="800" alt="image" alt="Screen Shot 2023-05-05 at 9 07 42 PM" src="https://user-images.githubusercontent.com/64395120/236593092-ccb3ad55-5bbb-44aa-ba39-370effc0d102.png">
Four data sets are used for this analysis. The data is collected from 2000 to 2022. The files used are as follows and contain the following information: 
•	OilPrice.xls: U.S Crude Oil Purchase Price (Dollars per Barrel)
•	OilProduction.xls: U.S. Field Production of Crude Oil (Thousand Barrels per Day)
•	S&P500_Index.xlsx: S&P 500 Index
•	DollarIndex.xlsx Dollar Index

The data was loaded into R and converted into monthly time series for analysis. There are 272 rows and no missing observations were detected:

Once the data is plotted, we see the general trend of time series data on crude oil price, crude oil production, dollar index and sp500 index from 2000 to 2022:
<img width="744" alt="Screen Shot 2023-05-05 at 9 13 56 PM" src="https://user-images.githubusercontent.com/64395120/236593231-3e500d37-d9c3-4d51-81b2-6f3fdc463956.png">

