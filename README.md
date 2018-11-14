
# JSON Files

## Introduction

We've started to investigate APIs and briefly got a preview of the most common response format for data: JSON. While there are other formats, such as XML, json is the current standard and the most common format you are apt to encounter. With that, let's take a look at how JSON files are structured.

## JSON

JSON stand for JavaScript Object Notation. It came after XML and was meant to streamline many data transportation issues at the time. It is now the common standard amongst data transfers on the web and has numerous parsing packages for numerous languages (including Python)! Here's a brief preview of the same file above now in JSON:  
<img src="json_preview.png" width=850>

## The JSON Module

https://docs.python.org/3.6/library/json.html


```python
import json
```

To load a json file, we first open the file using python's built in function and then pass that file object to the json module's load method. As you can see, this loaded the data as a dictionary.


```python
f = open('nyc_2001_campaign_finance.json')
data = json.load(f)
print(type(data))
```

    <class 'dict'>


Json files are often nested in a hierarchical strucutre and will have data structures analagous to python dictionaries and lists. We can begin to investigate a particular file by using our traditional python methods. Here's all of the built in supported data types in JSON and their counterparts in python: 

<img src="json_python_datatypes.png" width=500>

Check the keys of the dictionary:


```python
data.keys()
```




    dict_keys(['meta', 'data'])



Investigate what data types are stored within the values associated with those keys:


```python
for v in data.values():
    print(type(v))
```

    <class 'dict'>
    <class 'list'>


We can quickly preview the first dictionary as a DataFrame


```python
pd.DataFrame.from_dict(data['meta'])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>view</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>attribution</th>
      <td>Campaign Finance Board (CFB)</td>
    </tr>
    <tr>
      <th>averageRating</th>
      <td>0</td>
    </tr>
    <tr>
      <th>category</th>
      <td>City Government</td>
    </tr>
    <tr>
      <th>columns</th>
      <td>[{'id': -1, 'name': 'sid', 'dataTypeName': 'me...</td>
    </tr>
    <tr>
      <th>createdAt</th>
      <td>1315950830</td>
    </tr>
    <tr>
      <th>description</th>
      <td>A listing of public funds payments for candida...</td>
    </tr>
    <tr>
      <th>displayType</th>
      <td>table</td>
    </tr>
    <tr>
      <th>downloadCount</th>
      <td>1470</td>
    </tr>
    <tr>
      <th>flags</th>
      <td>[default, restorable, restorePossibleForType]</td>
    </tr>
    <tr>
      <th>grants</th>
      <td>[{'inherited': False, 'type': 'viewer', 'flags...</td>
    </tr>
    <tr>
      <th>hideFromCatalog</th>
      <td>False</td>
    </tr>
    <tr>
      <th>hideFromDataJson</th>
      <td>False</td>
    </tr>
    <tr>
      <th>id</th>
      <td>8dhd-zvi6</td>
    </tr>
    <tr>
      <th>indexUpdatedAt</th>
      <td>1536596254</td>
    </tr>
    <tr>
      <th>metadata</th>
      <td>{'rdfSubject': '0', 'rdfClass': '', 'attachmen...</td>
    </tr>
    <tr>
      <th>name</th>
      <td>2001 Campaign Payments</td>
    </tr>
    <tr>
      <th>newBackend</th>
      <td>False</td>
    </tr>
    <tr>
      <th>numberOfComments</th>
      <td>0</td>
    </tr>
    <tr>
      <th>oid</th>
      <td>4140996</td>
    </tr>
    <tr>
      <th>owner</th>
      <td>{'id': '5fuc-pqz2', 'displayName': 'NYC OpenDa...</td>
    </tr>
    <tr>
      <th>provenance</th>
      <td>official</td>
    </tr>
    <tr>
      <th>publicationAppendEnabled</th>
      <td>False</td>
    </tr>
    <tr>
      <th>publicationDate</th>
      <td>1371845179</td>
    </tr>
    <tr>
      <th>publicationGroup</th>
      <td>240370</td>
    </tr>
    <tr>
      <th>publicationStage</th>
      <td>published</td>
    </tr>
    <tr>
      <th>query</th>
      <td>{}</td>
    </tr>
    <tr>
      <th>rights</th>
      <td>[read]</td>
    </tr>
    <tr>
      <th>rowClass</th>
      <td></td>
    </tr>
    <tr>
      <th>rowsUpdatedAt</th>
      <td>1371845177</td>
    </tr>
    <tr>
      <th>rowsUpdatedBy</th>
      <td>5fuc-pqz2</td>
    </tr>
    <tr>
      <th>tableAuthor</th>
      <td>{'id': '5fuc-pqz2', 'displayName': 'NYC OpenDa...</td>
    </tr>
    <tr>
      <th>tableId</th>
      <td>932968</td>
    </tr>
    <tr>
      <th>tags</th>
      <td>[finance, campaign finance board, cfb, nyccfb,...</td>
    </tr>
    <tr>
      <th>totalTimesRated</th>
      <td>0</td>
    </tr>
    <tr>
      <th>viewCount</th>
      <td>233</td>
    </tr>
    <tr>
      <th>viewLastModified</th>
      <td>1536605717</td>
    </tr>
    <tr>
      <th>viewType</th>
      <td>tabular</td>
    </tr>
  </tbody>
</table>
</div>



Notice the column names which will be very useful!

Investigate further information about the list stored under the 'data' key:


```python
len(data['data'])
```




    285



Previewing the first entry:


```python
data['data'][0]
```




    [1,
     'E3E9CC9F-7443-43F6-94AF-B5A0F802DBA1',
     1,
     1315925633,
     '392904',
     1315925633,
     '392904',
     '{\n  "invalidCells" : {\n    "1519001" : "TOTALPAY",\n    "1518998" : "PRIMARYPAY",\n    "1519000" : "RUNOFFPAY",\n    "1518999" : "GENERALPAY",\n    "1518994" : "OFFICECD",\n    "1518996" : "OFFICEDIST",\n    "1518991" : "ELECTION"\n  }\n}',
     None,
     'CANDID',
     'CANDNAME',
     None,
     'OFFICEBORO',
     None,
     'CANCLASS',
     None,
     None,
     None,
     None]



## Summary
As you can see, there's still a lot going on here with the deeply nested structure of some of these data files. In the upcoming lab, you'll get a chance to practice loading files and conducting some initial preview of the data as we did here.
