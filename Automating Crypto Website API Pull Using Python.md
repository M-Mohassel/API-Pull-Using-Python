# This is my first project using an API to pull data from a website.

The Code inside of the function is provided by CoinmarketCap.com.
you should creat a account at coinmarketcap for using it.

### Important note
you should go Into the Anaconda Prompt to change this to allow to pull data 
use this in Anaconda Prompt: "jupyter notebook --NotebookApp.iopub_data_rate_limit=1e10"

### Defining a function for automation

    def api_runner():
        url = 'https://pro-api.coinmarketcap.com/v1/cryptocurrency/listings/latest'
        parameters = {
        'start':'1',
        'limit':'5000',
        'convert':'USD'
        }
        headers = {
        'Accepts': 'application/json',
        'X-CMC_PRO_API_KEY': 'YOUR API KEY',
        }

        session = Session()
        session.headers.update(headers)

        try:
        response = session.get(url, params=parameters)
        data = json.loads(response.text)
        print(data)
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



    
