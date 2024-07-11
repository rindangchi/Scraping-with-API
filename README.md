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

   Until this step we already get the data from the first page.

   

  
