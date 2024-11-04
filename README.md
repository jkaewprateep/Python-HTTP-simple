# Python-HTTP-simple
Consume HTTP rest services with a simple method with Alpaca RESTFul services API

<p align="center" width="100%">
    <img width="20%" src="https://github.com/jkaewprateep/Python-HTTP-simple/blob/main/alpaca.png">
    <img width="25%" src="https://github.com/jkaewprateep/Python-HTTP-simple/blob/main/kid_27.jpg">
    <img width="25%" src="https://github.com/jkaewprateep/Python-HTTP-simple/blob/main/kid_29.jpg"> </br>
    <b> Learning Alpaca webservices API and Python codes </b> </br>
</p>

## Simple HTTP request-response with Python request library

```
import requests
import json

url = "https://paper-api.alpaca.markets/v2/account";

headers = { 'content-type': 'application/json', "APCA-API-KEY-ID": "PKJ0VYG7T1NJ6K4EL199",
    "APCA-API-SECRET-KEY": "kuwqUKIpcc4gLvVUAZVPC4IJMJnkI7H0LUReQfpX", 
    "Accept": "*/*", "User-Agent": "DekDee" };

# response = requests.get( url, headers=headers, verify = "D:\\Backup\\certificaiton\\paper-api.alpaca.markets.pem" );
response = requests.get( url, headers=headers, verify = False );

if(response.ok):
    data = json.loads(response.content)
    for idx, row in enumerate(data):
        print(row + " : " + str(data[row]));
else:
    response.raise_for_status()
```
