# This is my first project using an API to pull data from a website.

The Code inside of the function is provided by CoinmarketCap.com.
you should creat a account at coinmarketcap for using it.


### Defining a function for automation
### Important note
you should go Into the Anaconda Prompt to change this to allow to pull data 
use this in Anaconda Prompt: "jupyter notebook --NotebookApp.iopub_data_rate_limit=1e10"

def api_runner():
    global df
    url = 'https://pro-api.coinmarketcap.com/v1/cryptocurrency/listings/latest' 
    #Original Sandbox Environment: 'https://sandbox-api.coinmarketcap.com/v1/cryptocurrency/listings/latest'
    parameters = {
      'start':'1',
      'limit':'15',
      'convert':'USD'
    }
    headers = {
      'Accepts': 'application/json',
      'X-CMC_PRO_API_KEY': '0ad53085-1cb2-4eb8-ad9e-3ffbd7e56509',
    }
    session = Session()
    session.headers.update(headers)
    try:
      response = session.get(url, params=parameters)
      data = json.loads(response.text)
      #print(data)
    except (ConnectionError, Timeout, TooManyRedirects) as e:
      print(e)
    #Transform this data into a dataframe
    df2 = pd.json_normalize(data['data'])
    df2['Timestamp'] = pd.to_datetime('now')
    df = df.append(df2)
    
### defining a loop for automation:
    import os 
    from time import time
    from time import sleep

    for i in range(333):
        api_runner()
        print('API Runner completed')
        sleep(300) #sleep for 5 minute
    exit()



    
