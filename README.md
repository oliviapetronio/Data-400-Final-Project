# Data-400-Final-Project

Introduction-hook
Data sources/got data
variables
Model
Results/imps

Data Sources: Data was collected from target.com, rentdata.org, census.gov, https://warehouse.ninja/target-distribution-center-locations/,
and the github file located here: https://gist.github.com/pramodpendyala/e5688b6a63d2983eac804bbaa1fd7cc0. 

Data retrieval:
  


In this project we will be utilizing data from the Bureau of Labor, Target grocery stores, and rent data at the national and division levels. 


Here are the packages that we used to complete this project. 
* npm
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
