# Python-HTTP-simple
Consume HTTP rest services with a simple method with Alpaca RESTFul services API

<p align="center" width="100%">
    <img width="20%" src="https://github.com/jkaewprateep/Python-HTTP-simple/blob/main/alpaca.png">
    <img width="25%" src="https://github.com/jkaewprateep/Python-HTTP-simple/blob/main/kid_27.jpg">
    <img width="25%" src="https://github.com/jkaewprateep/Python-HTTP-simple/blob/main/kid_29.jpg"> </br>
    <b> Learning Alpaca webservices API and Python codes </b> </br>
</p>

## Simple HTTP request-response with Python request library - ( 1 )

```
import requests
import json

url = "https://paper-api.alpaca.markets/v2/account";

headers = { 'content-type': 'application/json', "APCA-API-KEY-ID": "********************",
    "APCA-API-SECRET-KEY": "************************************************************", 
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

## Sample response

```
<Response [200]>
id : ba451548-8ce6-4dc5-a36d-ca14ecd86c07
admin_configurations : {}
user_configurations : None
account_number : PA3D791JPCCL
status : ACTIVE
crypto_status : ACTIVE
options_approved_level : 2
options_trading_level : 2
...
```

## Simple HTTP request-response with PyCurl request library  - ( 2 )

```
import pycurl
import certifi
from io import BytesIO

buffer = BytesIO()
c = pycurl.Curl()
c.setopt(c.URL, 'https://paper-api.alpaca.markets/v2/account')
c.setopt(pycurl.HTTPHEADER, ["APCA-API-KEY-ID: ************************",
        "APCA-API-SECRET-KEY: *****************************************", "User-Agent: curl/8.7.1", "Accept: */*",
        "Host: paper-api.alpaca.markets"]);
c.setopt(c.WRITEDATA, buffer)
c.setopt(c.CAINFO, certifi.where())
c.perform()
c.close()

body = buffer.getvalue()
print(body.decode('iso-8859-1'))
```

## Sample response

```
{"id":"ba451548-8ce6-4dc5-a36d-ca14ecd86c07","admin_configurations":{},"user_configurations":null,
    "account_number":"PA3D791JPCCL", "status":"ACTIVE","crypto_status":"ACTIVE", ... ,
    "pending_reg_taf_fees":"0"}
```

## Simple HTTP request-response with Curl in command line subprocess  - ( 3 )
 
```
import requests;
# import curlify;
import json;
import subprocess;
import shlex;

url = "https://paper-api.alpaca.markets/v2/account";
payload = "";
target_header = ["APCA-API-KEY-ID", "APCA-API-SECRET-KEY", "accept"];
headers = { "APCA-API-KEY-ID":"********************************", 
    "APCA-API-SECRET-KEY":"************************************", 
    "accept":"application/json" };

r = requests.get(url, data=json.dumps(payload), headers=headers)
r.headers = dict(['"{0}: {1}"'.format(k, v) for k, v in r.headers.items() if k in target_header]);
req = r.request;

command = "curl -X GET";
method = req.method;
uri = req.url;
data = req.body;

headers = ['"{0}: {1}"'.format(k, v) for k, v in req.headers.items() if k in target_header];
headers = " -H " + " -H ".join(headers);
command_tosend = command.format(method=method, headers=headers, data=data, uri=uri);
command_tosend = command_tosend + headers + " " + uri;

args = shlex.split(command_tosend);
process = subprocess.Popen(args, shell=False, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
stdout, stderr = process.communicate();

result = json.loads(stdout.decode('utf-8'));

print( result );

process.stdout.close();
```

## Sample response

```
{'id': 'ba451548-8ce6-4dc5-a36d-ca14ecd86c07', 'admin_configurations': {}, 'user_configurations': None,
    'account_number': 'PA3D791JPCCL', 'status': 'ACTIVE',  ..., 'pending_reg_taf_fees': '0'}
```

## Simple HTTP request-response with Alpaca tradeapi library  - ( 4 )

```
import alpaca_trade_api as tradeapi

from alpaca_trade_api.common import URL
from alpaca_trade_api.stream import Stream


API_KEY = "*******************************************"
API_SECRET = "****************************************"
APCA_API_BASE_URL = "https://paper-api.alpaca.markets"

object = tradeapi.REST(API_KEY, API_SECRET, APCA_API_BASE_URL, api_version="v2")

print( object.get_clock() );
```

## Sample response

```
Clock({   'is_open': True,
    'next_close': '2024-11-04T16:00:00-05:00',
    'next_open': '2024-11-05T09:30:00-05:00',
    'timestamp': '2024-11-04T10:46:29.017761912-05:00'})
```
