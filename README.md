<div id="header" align="center">
<img width="600" alt="image" src="https://i.ytimg.com/vi/WtLAgUovCIw/maxresdefault.jpg">
</div>

<h3 id="header" align="center">
 Crude Oil Prediction
</h3>


### :globe_with_meridians: Context
The price of oil, or the oil price, generally refers to the spot price of a barrel (159 liters) of benchmark crude oil—a reference price for buyers and sellers of crude oil such as West Texas Intermediate (WTI), Brent Crude, Dubai Crude. We hypothesize that the oil price can be modeled as a weighted lagged moving average of historical oil prices. 
- SPY index and Dollar Index are used as the macroeconomic indicators
- Oil production is used as an indicator of oil supply

We can use it to forecast the short-term oil price which would be useful for the government and companies for planning the budget for the fiscal year.

<img width="719" alt="Screen Shot 2023-05-05 at 9 19 30 PM" src="https://user-images.githubusercontent.com/64395120/236593489-ec5aa662-1bd5-47fd-a201-cb1cca1b7cff.png">


### Data Processing
<img width="800" alt="image" alt="Screen Shot 2023-05-05 at 9 07 42 PM" src="https://user-images.githubusercontent.com/64395120/236593092-ccb3ad55-5bbb-44aa-ba39-370effc0d102.png">
Four data sets are used for this analysis. The data is collected from 2000 to 2022. The files used are as follows and contain the following information:

- OilPrice.xls: U.S Crude Oil Purchase Price (Dollars per Barrel)
- OilProduction.xls: U.S. Field Production of Crude Oil (Thousand Barrels per Day)
- S&P500_Index.xlsx: S&P 500 Index
- DollarIndex.xlsx Dollar Index

The data was loaded into R and converted into monthly time series for analysis. There are 272 rows and no missing observations were detected:

Once the data is plotted, we see the general trend of time series data on crude oil price, crude oil production, dollar index and sp500 index from 2000 to 2022:


<img width="844" alt="Screen Shot 2023-05-05 at 9 13 56 PM" src="https://user-images.githubusercontent.com/64395120/236593231-3e500d37-d9c3-4d51-81b2-6f3fdc463956.png">

The scatter plot analysis shows that there is a significant negative correlation between price and dollar index. The US is one of the largest producer of oil. When the US dollar value increases, the less amount of US dollar is needed to buy a barrel of oil and vice versa. 


<img width="746" alt="Screen Shot 2023-05-05 at 9 16 21 PM" src="https://user-images.githubusercontent.com/64395120/236593344-349fc483-9a2a-4198-acb1-4345c9889b36.png">

#### Linear Regression Model
We also explore the relationship of crude oil price against crude oil production, SP index 500,  and dollar index using linear regression. The p-values of index 500,  and dollar index are significant, hence we can conclude that there seems to be a correlation between crude oil price and index 500, dollar index. 

<img width="610" alt="Screen Shot 2023-05-05 at 9 17 45 PM" src="https://user-images.githubusercontent.com/64395120/236593408-506afac2-e068-4915-adad-897c44e2aaff.png">

Stationary: 
In this section, we observe the stationarity of the data by using the statistical and plots test. The main method is to compute the auto correlation function to determine whether the oil crude price is stationary or not. In the graph, we found out that the pattern of ACF slowly decreases which indicates the non-stationarity of the data. Therefore, we decided to convert the oil crude data to stationary data. Log transformation and differencing are the two major methodologies being used for the conversion.

<img width="745" alt="Screen Shot 2023-05-05 at 9 18 22 PM" src="https://user-images.githubusercontent.com/64395120/236593442-ee95927d-6da1-4100-807f-81bf83f29f6c.png">

By applying Log Transformation, we addressed the skewness in the oil crude price data which made it conform more closely to normal distribution. By using the first differencing method on the log data, the data is stationary, and the pattern of the transformed oil price data is more easily interpretable. We learned about the characteristics of oil crude price and their nature in the plot. It highlights the oil crude price is cyclical since there is a repeating up and down as well as periodic peaks and deep patterns.

<img width="730" alt="Screen Shot 2023-05-05 at 9 20 16 PM" src="https://user-images.githubusercontent.com/64395120/236593507-1a721f99-98b7-404c-85aa-fc5f84edbc5d.png">

Seasonality: 
The seasonality plot suggests that crude oil price tends to go down slightly towards the end of the year, however it does not have the seasonality components. 

<img width="717" alt="Screen Shot 2023-05-05 at 9 21 37 PM" src="https://user-images.githubusercontent.com/64395120/236593567-7fb6ddd3-c8ed-4b19-89c8-8b139eef7ca8.png">

<img width="710" alt="Screen Shot 2023-05-05 at 9 22 08 PM" src="https://user-images.githubusercontent.com/64395120/236593582-84416ada-8ab3-4528-8fb3-ca8a8ce336a9.png">

MODELING
We looked for candidates to build ARIMA models in the next section. With the first differencing data, the extended auto correlation matrix allows us to select the order p and q of an ARIMA model. The proposed ARIMA model candidates are:

- ARIMA(0,1,1) named as the first model 
<img width="760" alt="Screen Shot 2023-05-05 at 9 23 46 PM" src="https://user-images.githubusercontent.com/64395120/236593660-70fe3507-dad2-4192-bd20-1631151b1cf7.png">

- ARIMA(1,1,1) named as the second model

<img width="716" alt="Screen Shot 2023-05-05 at 9 24 17 PM" src="https://user-images.githubusercontent.com/64395120/236593689-b1b5f418-0524-4595-a816-763d2228ef3c.png">

- ARIMA(1,1,3) named as the third model

<img width="715" alt="Screen Shot 2023-05-05 at 9 24 44 PM" src="https://user-images.githubusercontent.com/64395120/236593733-cc9b99ff-c9c4-4b66-bdbb-b98b5ee89492.png">


We can see that the first model ARIMA(0,1,1) and the third model ARIMA(1,1,3) have the data points above the threshold, hence we fail to reject the null hypothesis. However, since the AIC and BIC values of the first model ARIMA(0,1,1) are slightly smaller than the third model and the model is simpler, it is recommended to use the first model for production. The algebra expression of our deployment model is `xt` = `wt` +0.4583`wt`− 1. 

## Oil Crude Price Forecasting and 36-month Prediction

<img width="776" alt="Screen Shot 2023-05-05 at 9 27 11 PM" src="https://user-images.githubusercontent.com/64395120/236593864-1f68a1ea-c7a4-49c4-bcee-14bf3a60af9b.png">

Based on our forecasting, the crude oil price will increase gradually in the next 36 months. To better analyzing the crude oil price more accurately, there might be additional analyses needed in the future work. 


