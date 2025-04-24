# Data-400-Final-Project



Model
Results/imps

## Introduction

With grocery prices seeming to be a challenge for quite a while now, we wanted to explore grocery pricing regionally and divisonally through the lens of rural, suburban, and urban separations. 

## Data Sources and Retrieval
Data was collected from https://target.com, https://rentdata.org, https://census.gov, https://warehouse.ninja/target-distribution-center-locations/,
and the github file located here: https://gist.github.com/pramodpendyala/e5688b6a63d2983eac804bbaa1fd7cc0. 

These websites were scraped. See below for sample code. 



Here are all the packages that we used to complete this project. 
  ```sh
  from selenium import webdriver
  from selenium.webdriver.firefox.options import Options
  from selenium.webdriver.common.by import By
  from selenium.webdriver.common.keys import Keys
  from selenium.webdriver.support.ui import WebDriverWait
  from selenium.webdriver.support import expected_conditions as EC
  import time
  import math
  import pandas as pd
  import numpy as np
  import matplotlib.pyplot as plt
  import plotly.graph_objects as go
  import plotly.express as px
  import seaborn as sns
  import statsmodels.api as sm
  from sklearn.cluster import KMeans
  from sklearn.model_selection import train_test_split
  from sklearn.linear_model import LinearRegression
  from sklearn.metrics import mean_squared_error
  from sklearn.preprocessing import StandardScaler
  ```


Variables:
For our variables:
     -Unemployment rate
     -Target data (bananas, diapers, t-shirts, AirPods, vegetable oil, gum, toilet paper, cotton swabs, eggs, shampoo, and milk)
     -Target warehouse distance in relation to Target locations 
     -Median income
     -Population
     -Rent pricing

Various y variables are from the Target data compared to other target data and rest of variables (x). 


# Data Scraping
  Please see the code in the file Target Data! updated 4-6-25.ipynb for the full code. 

# Data Cleaning 
  Certain zip codes were changed to strings as some selected zip codes had a 0 in front 

  
# Exploratory Data Analysis 

Figure 1: 
 ![poster pics eda png-1](https://github.com/user-attachments/assets/7013ccc2-28a3-4721-9716-8bd5ac588986)
 
Figure 2:
![poster pics eda png-2](https://github.com/user-attachments/assets/e04faa13-944d-4a55-9eff-766a86842e20)

Figure 3:
![poster pics eda png-3](https://github.com/user-attachments/assets/69f4a397-2b88-48c6-a7ad-1c056924bfac)

Figure 4:
![poster pics eda png-4](https://github.com/user-attachments/assets/88840098-e0d2-4cb0-949a-ee55127233a9)


Figure 5:


![poster pics eda png-5](https://github.com/user-attachments/assets/4c3a116a-0eee-4eb7-a2a1-3e8b4a8c887e)






 
