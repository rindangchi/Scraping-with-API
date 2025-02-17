# Scraping-with-API
Simple Web Scraping with API

In this project i will show how to do a simple scraping using API. Website that we will be used for scraping is GGWP websit (https://ggwp.id/). This is part of Pacmann practice for Data Engineering class.

Here are the steps:

1. Import all needed libraries that will be used for project. Here we will import requests library to create connection with the targeted website, pandas library to create datafrane after we scrape the data, and tqdm library to define the range of page in the website that we would likek to scrape.

```python

import requests

import pandas as pd

from tqdm import tqdm

```



2. Next we will to write a code to establish connection to the API. Here we need to know the API url that is used in the website.
   To get the API URL, Go to Inspect Element --> Network. Double click in the selected URL, then we will directed to the new page.

   ![image](https://github.com/rindangchi/Scraping-with-API/assets/10241058/cc4e7998-804f-4883-81d0-2e16997ebe6a)

   
   After double click we get below URL :

   https://tourney-api.ggwp.id/api/v2/media/getLatestArticle?page=1

   ![image](https://github.com/rindangchi/Scraping-with-API/assets/10241058/f4e60e10-eb84-4cd1-967f-fc1f034bc46f)

   Below is the complete code to establish connection to the API:

   ```python

   raw_response = resp.json()

   raw_response


   ```
   After we run the code we will get below result, the result is in a dictionary format.

   ![image](https://github.com/rindangchi/Scraping-with-API/assets/10241058/9f517e56-2f3a-4348-984c-4f80e387f5ef)

   Until this step we already get the data from the first page. Now let's arrange the data in a dataframe so it will be much easier to read. In the dictionary we see that the keys are ["data"] ["data"],
   then we will create dataframe based on the json keys.

    ```python

   quote_data = pd.DataFrame(raw_response["data"]["data"])

   quote_data

   ```

   Here is the result after we run the code:

   ![image](https://github.com/rindangchi/Scraping-with-API/assets/10241058/33057e60-4621-4468-92f3-e78b91f2e0fd)
   

3. In this step we will scrape not only 1 page, but we will scrape to 10 pages. 
   
   Before that, we will give a one second interval when we scrape the data from the API, the purpose is to avoid detected as a bug.

    ```python

   import time

   ```

    And below is the complete code to get data from page 1 until page 10:

   ```python

   #create empty list to store value in each page

   tmp_data = []

   #get data from page 1-10

   for page in tqdm(range(1,11)):

   #establish connection to API
   resp = requests.get(f"https://tourney-api.ggwp.id/api/v2/media/getLatestArticle?page={page}")

   #convert response to json
   raw_response = resp.json()

   #get data based on key
   get_data = raw_response["data"]["data"]

   #get data into the list
   tmp_data.extend(get_data)

   #give interval 1 second
   time.sleep(1)

   ```

   After get all of the data, we will store the data into a dataframe

    ```python

   final_data = pd.DataFrame(tmp_data)

   final_data

   ```
  
   Here is the result:

   ![image](https://github.com/user-attachments/assets/447b2321-2029-41c3-92d3-68febc9ad1b4)

   Finally, we can save the data in .csv format

   ```python

   final_data.to_csv("scrape_api_data.csv", index= False)

   ```
   

   
