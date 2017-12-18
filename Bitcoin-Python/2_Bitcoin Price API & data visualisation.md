Please visit Part 1 below:
* **Utopian** - https://utopian.io/utopian-io/@abhi3700/learn-bitcoin-python-1-installation-guide-basic-commands
* **Steemit** - https://steemit.com/utopian-io/@abhi3700/learn-bitcoin-python-1-installation-guide-basic-commands


## Bitcoin Price API
Here, we fetch the **Bitcoin-price** using an API provided by **Coindesk**.
**Tools required** - Requests library. For more, click [here](https://www.coindesk.com/api/).
 
Install from the 'cmd' using ```pip install requests``` - 
![requests_install.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513566920/qe6azgz6cuemw9umnmhu.png)

Let's get started with the coding part-
Open notebook.
```python
import requests
r = requests.get('https://api.coindesk.com/v1/bpi/currentprice.json')
print(r.json())
```
![request_json.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513567152/wt1fohgqil5oemengoy1.png)
This displays the complete json data.

The complete json file looks like this. Click [here](https://api.coindesk.com/v1/bpi/currentprice.json) - 
![view_price_json.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513567394/m9jc7w5fvu1cqyi4x35y.png)

Now, to get the price, we need to fetch the 'rate' parameter inside 'USD'. Follow the steps - 
* Fetch the 'bpi' data -
```python
print(r.json()['bpi'])
```
![price_json_bpi.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513567612/ivp8lne2izuau1nko63w.png)

* Fetch the 'USD' data -
```python
print(r.json()['bpi']['USD'])
```
![price_bpi_usd.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513567810/va6c2n22pkszwapqpkbj.png)

* Fetch the 'rate' value - 
```python
print("The price of Bitcoin is: " + r.json()['bpi']['USD']['rate'])
```
![bitcoin_api_price.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513567947/wtqttopw8u8cajffsqeb.png)

Now, let's jump on to the next section which is in more details i.e. **Price data visualisation.**

## Bitcoin data visualisation
Here, we will look at the graph of the **Bitcoin Price** from day 1 to current date. For this, we will fetch the data from [Coindesk](https://www.coindesk.com/price/) in csv format.

### Tools Installation 
Following tools required for this:
* **Pandas**- for reading the csv file data.  ```pip install pandas```
![install_pandas.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513555779/humbtjrmdiyt9e01abul.png)

* **Matplotlib**- plot the data. ```pip install matplotlib```
![install_matplotlib.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513555806/gddauxjzamrmhizhagbn.png)

* **Jupyter notebook** - writing commands for data visualisation. ```pip install jupyter```
![install_jupyter.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513555860/nmbd9gxb1kojdg1zossr.png)

### Download the csv file. 
Click on the 'Export' button on right side of the graph. And 'save as' in 'csv' format in the directory of the notebook editor file.

### Coding
Now, open the notebook and start writing commands as follows:
* Import the pandas library
```python
import pandas as pd
```
![import_pandas.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513556212/oaqohmisyg3sfvby3oox.png)

* Import the matplotlib library
```python
import matplotlib.pyplot as plt
```
![import_matplotlib.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513556431/bysomgvenjxodoedpuxz.png)

* Plot the graph inline. Also, we need to to make the changes to the data onto the original set, not onto the copy.
```python
# The changed happen to the original dataset, not to the copy
pd.set_option('mode.chained_assignment', None)
```

```python
# plot the charts within the notebook
%matplotlib inline
```
![plot_inline.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513556655/ilswe8e7l8wopomowviw.png)

* Data manipulation
```python
# Reading the csv file using pandas
price = pd.read_csv("coindesk_data.csv")
```
```python
# look into the first 5 rows of the data.
price.head()
```
![price_head.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513558138/sehdkyjciei7ddwodjri.png)
 
Now, let's get some info about the data.
```python
price.info()
```
![price_info.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513559344/zqerkwcyge2kcumatyzs.png)

Here, we have 2 columns i.e. *'Date'* - 2713 entries and *'Close Price'* - 2711 entries. Now, we have to look at the *'Date'* entries which has 2 extra entries. Also, the *'Date'* entries is of type 'object' which needs to be changed into date-format.

Now, look at the data from bottom. 
```python
price.tail()
```
![price_tail.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513560101/wwmi3oynbpurifk310kr.png)
 We find here that the last 2 rows have *Close Price* value as 'NaN', which needs to be deleted.
Use ```price = price.dropna()``` method for this.
Just check that the data is removed.
![price_tail.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513560403/kluy8ginhd5kamivr7bi.png)
So, the last 2 rows have been removed.
Now, we need to convert the *Date* entries into date-format.
```python
price['Date'] = pd.to_datetime(price['Date'], format = '%Y-%m-%d')
```
Now, to check if implemented. Use this method ```price.info()```
![price_datetime_format.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513560927/qlvof0b2qmrbw5rrlsul.png)
Here, we can see that the *Date* column has entries of type *'datetime'*.
Now, we have to set the *Date* column as index column.
```python
price.index = price['Date']
```
![price_index.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513561344/vg7oshu4cqv4fta4m3oe.png)
Here, we see that the previous *Date* column is also present.

So, we need to delete that using ```del price['Date']```. Now look at the output.
![del_price.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513561493/yix20x1h7edymmj5gjmw.png)

Now, we can see the price of the **year 2010** using ```price['2010']```
![price_2010.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513564057/twcx4jjt11yi2ai1cilr.png)

If we want to see the price on a particular date, use this method ```price['2017-12-18']```
![price_date.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513564281/tleb4jwlevi6lfwpnhsh.png)

Now, to get the price from a date till current date, use this ```price['2017-08-01':]```
![price_august onwards.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513564809/iasjonhliyzxycug7avk.png)

Now, to see the min. and max. price, use these commands - ```price.min()``` & ```price.max()``` .
![price_min_max.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513564956/phyjsgb8rqnnpa0zqqqg.png)

To know everything at a glance, use this syntax - ```price.describe()```
![price_describe.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513565547/qawuby0s20vaunxm1kqy.png)

Now, plot the graph of *Price* vs *Date* . Use ```price.plot()```
![price_plot.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513565711/madfywsar2a76ciygdfb.png)

Now, to plot the graph for the year 2017, use ```price['2017'].plot()```
![price2017_plot.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513565879/bxhqoajgbjajxeygoyct.png)

That's all for now...



## Reference 
* Price API - https://www.youtube.com/watch?v=WyOYwfIgPDQ
* Price visualisation - https://www.youtube.com/watch?v=EDcOadyVWj8
