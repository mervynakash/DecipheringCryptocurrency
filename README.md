# DecipheringCryptocurrency
The case is financial time-series prediction with cryptocurrencies and it integrates knowledge from various sources - Crypto Currencies, Quantitative Finance, and Machine learning. The data consists of time-series of various cryptocurrencies with open, high, low, close prices and volumes from different crypto exchanges. The goal is to build a successful investing/trading model on the cryptocurrency markets.

# Academia Datathon
The Academia Datathon is a weekend-long online competition where more than 100 students from several universities across 6 countries are challenged to work on one real-world business case.
Their mission is to build in 48 hours not only the best machine learning algorithms but also to build up their knowledge and expertise helped by mentors, experts and other like-minded students in the field coming from all over the world.
The most creative and precise solutions of the provided dataset for the challenge will be awarded by a world known jury.
The Academia Datathon is entirely held online and opened to the global community via our platform.
This year's Academia Datathon was held between 27th - 30th of April. And universities from Greece, Ukraine, India had participated.

# Occam's Data Ninjas
To participate in this event we could either go solo, or form our own team or let the event organisers make a random match with other students. 
My team consisted of 5 members namely: @ravindrareddytamma, Sowmya, @noir976, @vijaybabyjoseph and me. Our team name was Occam's Data Ninja.

# Data Understanding 
The data was provided in the format of .csv files. The data contains the information regarding the 687 cryptocurrencies, whose individual parameters such as opening value, closing value, low, high, volume are provided as individual files. There are 2 Consolidated files that have the summary information regarding the price of each bitcoin captured for every 5 minutes interval from 17th Jan 2018 to 23rd Mar 2018. The ID’s of each crypto-currenciy and the names of each crypto-currency are provided in another consolidated file.

# Data Preparation: 
The data provided in form of the .csv file should be qualified to be a time series. But if we observe the data, it has lot of missing observations that are not captured at regular intervals of time. The main and basic requirement of Time Series is data should be captured at regular intervals of time which are equally spaced. So we need to impute the missing values to get the best prediction model.

# Identifying the Missing Values: 
First we have created a vector having the sequence of timestamps from the starting time in data to the ending time in data with a equal spaced interval of five 5 minutes. Now we have performed the outer join of the vector with the actual data set. When we perform this operation, if there is match of timestamps in both the vector and data set then the values in data set are considered, but for the timestamps, which is present in the vector but not present in the data set, we will have an empty value for the all columns in the row. In the next section, we deal with filling these Missing Values.

# Imputing the Missing Values: 
Now we have designed a trivial approach in filling the missing values for the empty rows. Let X(t) be the missing value then, it will be imputed by AVG(X(t-1),X(t+1)). Let us consider another scenario. Let X(t),X(t+1),X(t+2) be the sequential missing values then we will compare the values at X(t-1) and X(t+3), If there is increase in value from X(t-1) to X(t+3) then the amount of increment will be proportionally distributed among all the missing values. Suppose if there is a K amount of increment the K/5 is for first missing value , 2K/5 is for next missing value and 3K/5 is for the last missing value. The same logic is applied even in the case of Decrements.

# Data Modelling: 
We have used ARIMA Model to forecast the time series data. Auto Regression (AR) will determine the relation between the previous values and the current value in the time series. Moving Average (MA) summarizes the relation of the error term that appear in each observation. Integrated in ARIMA refers to the order of differencing that need to be performed to make the time series stationary. To build the model we have started in this way.
To Predict values of Y(t) (which is the first data-point in a day), we use all the data from Y(0) to Y(t-1) and form a time series with them, and next we find the order of AR, order of MA & d-value that best fit for the time series. We check the ACF and PACF values to determine the the parameters for the ARIMA(p,d,q) model and passed the ARIMA model to forecast the future values. After that we take Y(1) to Y(t) to predict Y(t+1) and we carry on these activities till all 288 data-points in a day are predicted. 

# Evaluation: 
We have divided the data into  2 parts namely training and test data set. we have fed the model with the train data set that helped the model to learn something about the data. Now we have predicted the values present in the train data set. We have compared the Predicted values with the Observed values and calculated the SSE (Sum of squared error). We have selected the model which has the least SSE Value and higher Accuracy.
