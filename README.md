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

 ```sh
# --- Product Data ---
products = [
    ("Bananas", "https://www.target.com/p/organic-bananas-2lb-good-38-gather-8482/-/A-85759852#lnk=sametab"),
    ("Vegetable Oil", "https://www.target.com/p/vegetable-oil-good-gather/-/A-89467834?preselect=78376315#lnk=sametab"),
    ("Gum", "https://www.target.com/p/extra-spearmint-sugarfree-gum-15ct/-/A-13307857#lnk=sametab"),
    ("Toilet Paper", "https://www.target.com/p/cottonelle-ultra-comfort-toilet-paper/-/A-54605704?preselect=75665830#lnk=sametab"),
    ("AirPods", "https://www.target.com/p/apple-airpods-4/-/A-93606140?preselect=85978618#lnk=sametab"),
    ("Cotton Swabs", "https://www.target.com/p/q-tips-cotton-swabs-375ct/-/A-11223546#lnk=sametab"),
    ("Diapers", "https://www.target.com/p/pampers-swaddlers-active-baby-diapers-select-size-and-count/-/A-14783999?preselect=53461432#lnk=sametab"),
    ("T-Shirt", "https://www.target.com/p/women-s-linen-short-sleeve-t-shirt-universal-thread/-/A-93711326?preselect=92878440#lnk=sametab"),
    ("Eggs", "https://www.target.com/p/grade-a-large-eggs-12ct-good-38-gather-8482-packaging-may-vary/-/A-14713534#lnk=sametab"),
    ("Shampoo", "https://www.target.com/p/native-coconut-vanilla-moisturizing-shampoo/-/A-94666723?preselect=80120273#lnk=sametab"),
    ("Milk", "https://www.target.com/p/milk-good-gather/-/A-94602358?preselect=13276134#lnk=sametab")
]

#       rural, suburban, urban
zips = ['50702', '50009', '52404',
        '67401', '66062', '66111',
        '56601', '55066', '55403',
        '63010', '63033', '64114',
        '68073', '68123', '68116',
        '58563', '58701', '58103',
        '57701', '57401', '57110']

location = ['Waterloo, IA', 'Altoona, IA', 'Cedar Rapids, IA',
            'Salina, KS', 'Olathe, KS', 'Kansas City, KS',
            'Bemidji, MN', 'Red Wing, MN', 'Minneapolis, MN',
            'Arnold, MO', 'Florissant, MO', 'Kansas City, MO',
            'Yutan, NE', 'Bellevue, NE', 'Omaha, NE',
            'New Salem, ND', 'Minot, ND', 'Fargo, ND',
            'Rapid City, SD', 'Aberdeen, SD', 'Sioux Falls, SD']

city_town = ['Rural', 'Suburban', 'Urban',
             'Rural', 'Suburban', 'Urban',
             'Rural', 'Suburban', 'Urban',
             'Rural', 'Suburban', 'Urban',
             'Rural', 'Suburban', 'Urban',
             'Rural', 'Suburban', 'Urban',
             'Rural', 'Suburban', 'Urban'] 


combined_data = []

# --- Setup Driver ---
def setup_driver():
    options = Options()
    options.add_argument("--disable-blink-features=AutomationControlled")
    options.add_argument("--window-size=1920x1080")
    driver = webdriver.Firefox(options=options)
    driver.set_page_load_timeout(30)
    return driver

def close_modal(driver):
    try:
        WebDriverWait(driver, 5).until(
            EC.element_to_be_clickable((By.CLASS_NAME, "styles_overlay__3ZDC1"))
        )
        close_btn = driver.find_element(By.CLASS_NAME, "styles_overlay__3ZDC1")
        driver.execute_script("arguments[0].click();", close_btn)
        time.sleep(2)
    except:
        pass

# --- Scraping Loop ---
for product_name, url in products:
    print(f"📦 Scraping {product_name}...")
    driver = setup_driver()
    try:
        driver.get(url)
        time.sleep(5)
        close_modal(driver)

        price_element = WebDriverWait(driver, 10).until(
            EC.presence_of_element_located((By.XPATH, "//span[contains(@data-test, 'product-price')]"))
        )
        price = price_element.text
        #combined_data.append({"Product": product_name, "Zip Code": zips[0], "Price": price})
        print(f"✅ Zip Code: {zips} , Price: {price}")
        time.sleep(2)

        for zip_code in zips:
            try:
                time.sleep(2)
                
                edit_buttons = driver.find_elements(By.XPATH, '//*[@id="web-store-id-msg-btn"]/div/div[2]/span')
                time.sleep(3)
                if not edit_buttons:
                    print(f"❌ Could not find 'Edit your location' for zip {zip_code}")
                    continue
                edit_buttons[0].click()
                time.sleep(1)
                zip_input = driver.find_element(By.XPATH, '//*[@id="zip-or-city-state"]')
                zip_input.send_keys(Keys.COMMAND + "a")
                zip_input.send_keys(Keys.BACKSPACE)
                zip_input.send_keys(zip_code)
                time.sleep(1)
                
                print("Clicking the button to update zip")
                
                lookup = driver.find_element(By.XPATH, "/html/body/div[5]/div/div/div[2]/div[1]/div/div[1]/div[2]/button")
                lookup.click()
                time.sleep(3)
                
                first_available_store = driver.find_element(By.XPATH, "/html/body/div[5]/div/div/div[2]/div[2]/fieldset/div[1]/div/div[1]/label")
                first_available_store.click()
                time.sleep(1)
                
                shop_this_store = driver.find_element(By.XPATH, "/html/body/div[5]/div/div/div[3]/button")
                shop_this_store.click()
                time.sleep(3)
                
                price_element = WebDriverWait(driver, 10).until(
                    EC.presence_of_element_located((By.XPATH, "//span[contains(@data-test, 'product-price')]"))
                )
                price = price_element.text
                combined_data.append({"Product": product_name, "Zip Code": zip_code, "Price": price})
                print(f"✅ Zip Code: {zip_code} , Price: {price}")

            except Exception as e:
                print(f"❌ Error processing zip {zip_code}: {e}")
    except Exception as e:
        print(f"❌ Error on main product for {product_name}: {e}")
    finally:
        driver.quit()
```

