
# Time_Series_Analysis
Objective: Conducting analysis of MercadoLibre's financial and user data to help company grow.
# Step 1: Find Unusual Patterns in Google Hourly Search Traffic
I sliced the google search trends dataframe to just the month of May 2020 (during which the MercadoLibre released its quarterly financial results). Using hvplot to visualize the results, there were no unsual patterns in hourly search traffic. And the traffic did not particularly increase during the monthly of May in comparison to the monthly median across all months.

![bokeh_plot](https://user-images.githubusercontent.com/98926434/165192132-48e04696-7969-4496-8c37-abc5bc5cc131.png)

# Step 2: Mine the Search Traffic Data for Seasonality
I grouped the hourly search data to plot the average traffic by the day of the week and used a heatmap referencing the index.hour as the x-axis and the index.dayof week as the y-axis and observed that Tuesday during the first two hours has the most concentration. I also grouped the search data by the week of the year and found search traffic tends to increase during the winter holiday period, peaking at week 52.

![bokeh_plot-3](https://user-images.githubusercontent.com/98926434/165192261-21272d1a-f483-4625-8621-16d3e9793d9d.png)
![bokeh_plot-2](https://user-images.githubusercontent.com/98926434/165192419-31be103f-1b2f-4834-8d7e-719bd72b5fad.png)
![bokeh_plot-4](https://user-images.githubusercontent.com/98926434/165192553-4594555a-c2d3-40d2-8adb-4d864be8c194.png)

# Step 3: Relate the Search Traffic to Stock Price Patterns
I imported the mercado stock data and concatenated it to the search trends to form a single dataframe. Market events emerged during the year of 2020 that many companies found difficult, but after the initial shock, new customers and revenue increased for e-commerce platforms. I sliced the data to just the first half od 2020 and used hvplot to visualize the data. Both time series indicated this narrative, there was an increase in stock price and search trends after March 2020. 

![bokeh_plot-5](https://user-images.githubusercontent.com/98926434/165193129-c41f1da2-0996-41c5-a947-8e94aadb6dd7.png)
![bokeh_plot (1)](https://user-images.githubusercontent.com/98926434/165193286-a47bcb90-cea2-4e3c-bfc5-149b7461ec10.png)
![bokeh_plot (2)](https://user-images.githubusercontent.com/98926434/165193293-cfd2c6aa-6117-4183-b7eb-b722d6cd9111.png)

I created a new column in the dataframe named "lagged search trends" that shifts the search traffic by one hour, and additional columns, stock volatility, which holds an exponentially weighted four-hour rolling average of the company's stock volatility, and hourly stock return, which holds the percent change of the company's stock price on an hourly basis. I used a time series correlation of the new dataframe and found that there was a weak negative relationship between the stock volatility and lagged search trends. And a weak positive relationship between lagged search trends and hourly stock returns.

![bokeh_plot-7](https://user-images.githubusercontent.com/98926434/165193351-750148bf-4748-485f-a05d-0a89e46f3d24.png)

# Step 4: Create a Time Series Model with Prophet
In order to produce a time series model that analyses and forecasts patterns in the hourly search data, I set up the prophet forecasting model: model_mercado_trends=Prophet(), Fit the model, and created a future dataframe to hold predictions as far as 2000 hours. After estimating the model, I plotted the forecast and observed that the predicted values are higher indicating possible higher popularity of MercadoLibre.
Plotting the individual time series components showed that midnight has the greatest popularuty, Tuesday gets the most search traffic, while mid October was the lowest point for seach traffic in the calendar year.
