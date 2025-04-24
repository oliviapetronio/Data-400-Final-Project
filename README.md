# Data-400-Final-Project


## Introduction

With grocery prices seeming to continue rising and variations of economic pressures, people are finding challenges living. We wanted to explore grocery pricing regionally and divisonally through the lens of rural, suburban, and urban separations. 

**Research Question** : How do factors like location (regionally, division, state, urban, suburban, or rural), rent prices, unemployment, distance to distribution centers, median income, and population impact Target's pricing strategies? 


## Data Sources and Retrieval
Data was collected from [Target](https://target.com), [Rent](https://rentdata.org), [Census](https://census.gov), [Warehouse Data](https://warehouse.ninja/target-distribution-center-locations/), and the github file located here: [Zip Code Latitudes and Longitudes](https://gist.github.com/pramodpendyala/e5688b6a63d2983eac804bbaa1fd7cc0).


These websites were scraped. See Data Scraping section for more information. 


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


## Variables: 
For our variables:  
-Unemployment rate  
-Target data (bananas, diapers, t-shirts, AirPods, vegetable oil, gum, toilet paper, cotton swabs, eggs, shampoo, and milk)  
-Target warehouse distance in relation to Target locations   
-Median income  
-Population  
-Rent pricing  

Various variables are from the Target data (y) compared to other target data and rest of variables (x). 


# Data Scraping
  Please see the code in the file [Target Data! updated 4-6-25.ipynb](https://github.com/oliviapetronio/Data-400-Final-Project/blob/main/Target%20Data!%20updated%204-6-25.ipynb) for the full code.

# Data Cleaning 
  Certain zip codes were changed to strings as some selected zip codes had a 0 in front and were not registering as integers. The rent and price were changed to floats removing the $. Also some AirPods rows had name variations and therefore had to be unified. Since all of the data was in a separate file from web scraping, data was appended and then pivoted (columns turn into rows and rows into columns) so data is tidy with zip code as id. Then the distribution center distance was added.

  
# Exploratory Data Analysis 
   Here is the first plot and analysis we did:

   Figure 1: 
 ![poster pics eda png-1](https://github.com/user-attachments/assets/7013ccc2-28a3-4721-9716-8bd5ac588986)

AirPods and diapers were removed from this chart due to consistent pricing for each area and distortion of pricing ($179.99 and $44.99 respectively). And also skewed data since everything else is ranged $1-14. Please contact if full chart is desired. Since there are lines on all of the milk and eggs, these are high price variance items. While other things like toilet paper, gum, vegetable oil, shampoo, t-shirts, cotton swabs have less confidence intervals. Even though they are present. Since Alaska does not have a distribution center and Hawaii, it needs to be shipped by plane or sailed. Another thing to note is the consistency between urban, suburban, and rural.

 
The rest of our analysis can be found under the [Final Poster](https://github.com/oliviapetronio/Data-400-Final-Project/blob/main/Final%20Poster.pdf) section on the github and the [analysis section]()

## Model
Inference multiple linear regression was chosen to find the relationship between one Target product and the rest of the variables. 



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








 
