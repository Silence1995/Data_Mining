# Data Mining & Machine Learning

Package: 
- pandas
- scikit-Learn
- mlxtend
- numpy
- scipy
- folium
- geopy
- matplotlib


## :memo: Homework0

##### Dataset: [AirBox Dataset](https://sites.google.com/site/cclljj/dataset-airbox)(We will use March 2017, Taiwan )
- filesize:263MB
- columns:

|    Date    |   Time   |   device_id  | PM2.5 | PM10 | PM1 | Temperature | Humidity |   lat  |   lon   |
|:----------:|:--------:|:------------:|:-----:|:----:|:---:|:-----------:|:--------:|:------:|:-------:|
| 2017-03-01 | 08:00:00 | 74DA388FF5F6 |   41  |  48  |  28 |     20.0    |    89    | 25.059 | 121.499 |

### Tasks:
- you need to do some data preprocessing, and then get some
basic information about the dataset 

#### Task1 - Preprocessing Tasks

- Remove the anomal records. 
  Ex: value of PM2.5 is 0
- Remove the sensors with few data.
- Remove the sensors with few long time gap.

#### Task2 - Data alignment
 
- We require aligned-time data for future works. However, the sensors don¡¦t have a static record time. In order to solve this problem, we can use linear interplolation.
    - Original Data
    
  | time  | 17:04 | 17:18 | 17:22 | 17:29 | 17:36 |
  |-------|-------|-------|-------|-------|-------|
  | pm2.5 | 10    | 20    | 30    | 40    | 50    |
    - New Data
    
  |  time |  17:10 | 17:20 |  17:30 |
  |:-----:|:------:|:-----:|:------:|
  | pm2.5 | 14.286 |   25  | 41.429 | 

#### Task3 - Visualization:
    
- Compare different sensors in same time interval.
  ex: Sensor 1 on 8/10 v.s. Sensor 2 on 8/10
   <p>
   <img src="https://github.com/Silence1995/Data_Mining/blob/master/figure/hw0_1.PNG" width="400" height="300" />
   </p>
- Plot all sensors on the map and describe the dataset.
    <p>
      <img src="https://github.com/Silence1995/Data_Mining/blob/master/figure/hw0_2.PNG" width="400" height="300" />
    </p>
#### Task4 - Query:

- How many sensors are there in the dataset?
- Which sensor recorded the highest temperature in March? What¡¦s the temperature? And where's the sensor?
- What were the maximal PM2.5 values of each sensors on 3/5?

#### Task5 - Time Series Data Comparsion :
- Choose two sensors to do the following steps.
Q: Sequence from Sensor 1
C: Sequence from Sensor 2
Distance(Q, C): Distance between Q & C
    
    1. Offset Translation 
    Q = Q - mean( Q ), C = C - mean( C )
    2. Amplitude Scaling
    Q = (Q - mean( Q )) / std(Q), C = (C - mean( C )) / std( C )
    3. Linear Trend Removal
    Q = detrend( Q ), C = detrend( C )
    4. Noise Removal
    Q = smooth( Q ), C = smooth( C )
    5. Calculate Distance(Q, C) at each step, and compare the difference between original data and transformed data.
    
    | Q | C |
    |:-:|:-:|
    | <p> <img src="https://github.com/Silence1995/Data_Mining/blob/master/figure/hw0_3.PNG" width="400" height="300" /></p> |<p> <img src="https://github.com/Silence1995/Data_Mining/blob/master/figure/hw0_4.PNG" width="400" height="300" /> </p> |

## :memo: Homework1

##### Dataset: Same as Homework_0
You can use the dataset before or after preprocessing

### Tasks:
- Define three different transaction, and conduct some experiments on the three mining tasks to find association rules 
- For each task, you should try 
    - Two discretization methods 
        - Divided by 10
        - Divided by 20 
    - Two algorithms 
         - [Apriori](http://rasbt.github.io/mlxtend/user_guide/frequent_patterns/apriori/)
         - [Fp-growth](http://rasbt.github.io/mlxtend/user_guide/frequent_patterns/fpgrowth/) 

- For example, I define a transaction is (pm2.5, humidity, temperature) for device_id=74DA3895C538, then the transaction are (20, 64, 35), (42, 76, 28) ...

### Transactions for each task:

#### Task 1: transaction (PM2.5, humidity, temperature)

| PM2.5 | Humidity | Temperature | 
|:-----:|:--------:|:-----------:|
|  89.0 |   85.0   |    22.12    | 
|  88.0 |   85.0   |    22.12    | 
|  ...  |   ...    |    ...      |
|  90.0	|   86.0   |    21.87    |
#### Task 2: transaction (PM2.5, Humidity , Time)

| PM2.5 | Humidity |   Time   |
|:-----:|:--------:|:--------:|
|  89.0 |   85.0   | 00:00:00 |
|  88.0 |   85.0   | 00:10:00 |
|  ...  |    ...   |    ...   |
|  90.0 |   86.0   | 00:40:00 |
#### Task 3: transaction (PM2.5, PM10, PM1)

| PM2.5 |  PM10 |  PM1 | 
|:-----:|:-----:|:----:|
|  89.0 | 106.0 | 63.0 | 
|  88.0 | 106.0 | 62.0 | 
|  .... | ....  | .... |
|  90.0	| 108.0	| 64.0 |




## :memo: Homework2

##### Dataset: Same as Homework_0
You can use the dataset before or after preprocessing

### Tasks:
- Turn data into different clusters, and you should use three kinds of clustering methods for this homework in total.
    - KMeans
    - Agglomerative Clustering
    - DBSCAN



#### Tasks1 - Spatial Clustering:
- Use geometric information to do clustering. (i.e. lat and lon)
- Use two kinds of clustering methods and compare the differences
  | Kmeans | DBSCAN|
    |:-:|:-:|
    | <p> <img src="https://github.com/Silence1995/Data_Mining/blob/master/figure/hw2_kmeans.PNG" width="300" height="300" /></p> |<p> <img src="https://github.com/Silence1995/Data_Mining/blob/master/figure/hw2_dbscan.PNG" width="300" height="300" /> </p> |
#### Tasks2 - Spatial + PM2.5 Clustering:

- Combine geometric information and PM2.5 data 
at certain timestamp 
    - Ex: PM2.5 at 2017/3/10 17:10:00
- Do clustering
- Normalize the data and do clustering again.
- Compare the differences between clustering before normalization and clustering after normalization

|    | before normalization | after normalization |
|:--:|:--------------------:|---------------------|
| 2d |           <img src="https://github.com/Silence1995/Data_Mining/blob/master/figure/hw2_kmeans2d.PNG" width="300" height="300" />            |              <img src="https://github.com/Silence1995/Data_Mining/blob/master/figure/hw2_kmeans2d_n.PNG" width="300" height="300" />        |
| 3d |        <img src="https://github.com/Silence1995/Data_Mining/blob/master/figure/hw2_kmeans3d.PNG" width="300" height="300" />               |             <img src="https://github.com/Silence1995/Data_Mining/blob/master/figure/hw2_kmeans3d_n.PNG" width="300" height="300" />         |
#### Tasks3 - Temporal Clustering:
- Use a static time interval to do clustering.
    - For example, the sample rate is 1 data / 10 minutes 
        - Aligned-time data from Homework0
    
      |  time |  17:10 | 17:20 |  17:30 |
      |:-----:|:------:|:-----:|:------:|
      | pm2.5 | 14.2 |   25  | 41.9 | 

     - We use all data on 03/10, and each sensor will have 6 records in 1 hour, so there will have 24(hours)*6 = 144 records
        - 144-dimension  Data

        |   device_id  |   0  |   1  |   2  |   3  | ... |  143 |
        |:------------:|:----:|:----:|:----:|:----:|:---:|:----:|
        | 28C2DDDD459E | 18.0 | 19.0 | 18.5 | 18.0 | ... | 14.7 |
        | 28C2DDDD45E6 | 29.0 | 29.6 | 30.0 | 31.0 | ... | 43.0 |
        - Do the 144-dimension clustering
- Use PCA to reduce the dimension, and do clustering again
- Compare the differences between clustering before PCA and clustering after PCA
| 144-dimension| PCA|
    |:-:|:-:|
    | <p> <img src="https://github.com/Silence1995/Data_Mining/blob/master/figure/hw2_144d.PNG" width="300" height="300" /></p> |<p> <img src="https://github.com/Silence1995/Data_Mining/blob/master/figure/hw2_pca.PNG" width="300" height="300" /> </p> |
#### Tasks2 - Spatial + PM2.5 Clustering:
## :memo: Homework3

##### Dataset: [AirBox Dataset](https://sites.google.com/site/cclljj/dataset-airbox)
    
- You need to use three-month-data in this homework. (January, February & March 2017)
- We only need one sensor



### Tasks:
- Use historical data to predict the PM2.5 value after 1 hour
- For example, the sample rate is 1 data / 15 minutes, and we use previous hour to predict the PM2.5 value next hour, the **Input X** and **Output Y** will look like the following 

-  **Input X**:

    | Date_Time | 2017-01-01 08:00:00 | 2017-01-01 08:15:00 | 2017-01-01 08:30:00 | 2017-01-01 08:45:00 |
    |:---------:|:-------------------:|:-------------------:|:-------------------:|:-------------------:|
    |   PM2.5   |         30.5        |         23.0        |         23.0        |         21.5        |


-  **Output Y**:

    | Date_Time | 2017-01-01 09:45:00 |
    |:---------:|:-------------------:|
    |   PM2.5   |         17.0        |

- After preprocessing the data into **Input X** and **Output Y**, we randomly split the data into 70% training data and 30% testing data

- Train models and do evaluations





#### Task 1 - Try classification models to predict PM2.5 value

- Descritization
The output of classification models are categories (labels), you need to encode the Output Y to categories(labels) by using discretization methods
    - Divided by 10 
    - Divided by 20


- Try following models
    - K-Nearest-Neighbor
    - Naive Bayes
    - Random Forest
    - Support vector machine (SVC)
- Evaluation and Comprasion
     <p>
      <img src="https://github.com/Silence1995/Data_Mining/blob/master/figure/hw3_classification.PNG" width="450" height="450" />
    </p>

#### Task 2 - Try regression models to predict PM2.5 value

- Try following models
    - Bayesian Regression
    - Decision tree Regression
    - Support vector machine (SVR)
-  Evaluation and Comprasion 
 <p>
      <img src="https://github.com/Silence1995/Data_Mining/blob/master/figure/hw3_regression.PNG" width="450" height="450" />
    </p>
