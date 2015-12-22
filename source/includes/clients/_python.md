## Python Client

We offer a client library for accessing the Algorithmia API in Python.

### Installation

> PyPi installation (recommended):

```
pip install algorithmia
```

> Install from source:

```
python setup.py bdist_wheel
```

> Install a wheel manually:

```
pip install --user --upgrade dist/algorithmia-*.whl
```

The Algorithmia python client can be installed through PyPi or from the source.

To install from PyPi, simply run `pip install algorithmia`. We recommend installing through this method for its ease of use!

When ready to use the python client, be sure to import the package at the top of your file:
`import Algorithmia`

### Usage

#### Calling an Algorithm

```
import Algorithmia
input = "liz"
Algorithmia.apiKey = 'Simple YOUR_API_KEY'
result = Algorithmia.algo('demo/Hello').pipe(input)
print(result)
-> "Hello Liz"
```
You can use the python client to call any algorithm in the marketplace. 

Simply pass the name of the algorithm to the client:

`Algorithmia.algo('demo/Hello')`

Then use the `.pipe` function to pass your input:

`Algorithmia.algo('demo/Hello').pipe(input)`

See the right pane for a full example of how to call an algorithm with the python client.

### Data access

The Algorithmia Python Client provides an easy way to manage data stored within Algorithmia. Basic usage samples are shown to the right. See the Data API for more information.

#### Read access

> Get a file object:

```
file = Algorithmia.file("data://.my/test/test.txt").getFile()
```

> Get a file's contents as bytes:

```
fileAsBytes = Algorithmia.file("data://.my/test/test.txt").getBytes()
```

> Get a file's contents as a string:

```
fileAsString = Algorithmia.file("data://.my/test/test.txt").getString() 
print(fileAsString)
-> this is only a test.
```

> Get a file's contents as JSON: 

```
fileAsJson = Algorithmia.file("data://.my/test/test.txt").getJson() 
print(fileAsJson)
->"this is only a test."
```

> Check if a file exists:

```
fileExists = Algorithmia.file("data://.my/test/test.txt").exists()
print(fileExists)
-> True
```

With the Python client, you can:

* get a file
* get the file's contents as bytes
* get the file's contents as a string
* get the file's contents as JSON
* check if the file exists

#### Write access


> Create or update a file from a string:

```
Algorithmia.file("data://.my/test/test.txt").put("this is only a test.")
```

> Create or update a file from JSON. Will automatically convert many python types into JSON:

```
Algorithmia.file("data://.my/test/test.txt").putJson({'a': 31415})
```

> Create or update a file from a local file. The file will be opened and closed within the putFile method:

```
Algorithmia.file("data://.my/test/test.txt").putFile(localFile)
```

> Delete file:

```
Algorithmia.file("data://.my/test/test.txt").delete()
```


With the Python client, you can do the following operations with the Data API:

* create or update a file from a string
* create or update a file from JSON
* create or update a file from a local file
* delete files

#### Additional resources

<a href="https://github.com/algorithmiaio/algorithmia-python">Algorithmia Python Client Source Code<i class="fa fa-external-link"></i></a>
