# Data-400-Final-Project


## Introduction

With grocery prices seeming to be a challenge for quite a while now, we wanted to explore grocery pricing regionally and divisonally through the lens of rural, suburban, and urban separations. 

## Data Sources and Retrieval
Data was collected from [Target]https://target.com, [Rent]https://rentdata.org, [Census]https://census.gov, [Warehouse Data]https://warehouse.ninja/target-distribution-center-locations/,
and the github file located here: [Zip Code Lats and Longs]https://gist.github.com/pramodpendyala/e5688b6a63d2983eac804bbaa1fd7cc0. 

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

## Model
Multiple linear regression was chosen to find the relationship between one Target product and the rest of the variables. 




## Results

Perishable goods like milk and eggs show significant regional price variation: Influenced by transportation costs, supply chain logistics, and local retail infrastructure.
Non-perishable and manufacturer-controlled items maintain stable pricing, such as AirPods and bananas, across regions, likely due to standardized national pricing.
Geographic area type influences pricing: Urban areas benefit from lower prices due to proximity to distribution hubs and retail competition, while rural areas experience higher prices due to longer supply chains and fewer retailers. Suburban regions show mixed pricing patterns based on local conditions.
Distance from distribution centers: Longer distances drive up costs, especially for perishables.


## Implications

Social: 
Individual: knowledge and awareness. Lots of people feel financial pressure paying for their necessities.
Community: knowledge and advocation.
Law: gives policymakers insight to pricing differences between regions and area types.
Ethical: 
Although there are supply chain issues to getting to rural areas, rural customers have lower median incomes but are paying more for necessities. Therefore, placing the burden on the consumers  and creating financial stress.
Legal:
Concerns of scraping legally for data privacy and in regulation with Target's policies. 








 
