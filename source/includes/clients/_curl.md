## cURL

You can use cURL to call any algorithm on the marketplace as well as interact with the Data API.

### Calling an Algorithm via cURL

```
curl -X POST -d 'Liz' -H 'Content-Type: application/json' -H 'Authorization: Simple YOUR_API_KEY' https://api.algorithmia.com/v1/algo/demo/Hello

-> {"result": 42,"metadata":{"duration":0.0001}}
```

To call an algorithm, use cURL to POST to the API. Be sure to specify the content type and authorize by passing in your API key.


### Working with Data via cURL

#### Create a collection

```
curl -X POST -d '{"name":"newCollection"}' -H 'Content-Type: application/json' -H 'Authorization: Simple YOUR_API_KEY' https://api.algorithmia.com/v1/data/YOUR_USERNAME

-> {"result": "data://YOUR_USERNAME/newCollection"}
```
You can use cURL to interact with the Data API from the command line. To create a collection, POST the new collection name to the Data API URL formatted with your user name. You will get a result that returns the address of the new data collection.


#### Upload File

```
curl -X PUT -F file=@@filename.csv -H 'Authorization: Simple YOUR_API_KEY' https://api.algorithmia.com/v1/data/YOUR_USERNAME/newCollection

-> {"result": "data://YOUR_USERNAME/newCollection/filename.csv"}
```

To upload a file, use cURL to `PUT` the file to a collection. Be sure to pass in your API key and the data collection URL. The response will return a result with the location of the file.

#### Upload data as a file

```
curl -X PUT -H 'Content-Type:application/json' -d '{"key1": "value1"}' -H 'Authorization: Simple YOUR_API_KEY' https://api.algorithmia.com/v1/data/YOUR_USERNAME/newCollection/myFile.json

-> {"result": "data://YOUR_USERNAME/newCollection/myFile.json"}
```

You can also use cURL to upload data to the collection as a file. Be sure to pass in your API key and the data collection URL. The response will return a result with the location of the file.
