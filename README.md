# Using Alpha Vantage API to Analyse Financial Data
In this section I will use Alpha Vantage API to analyze forex data. Let's first import some required libraries. To use any API we are generally required to pass an API key with the search parameters. So, for AlphaVantageAPI we can get one from https://www.alphavantage.co/. In this approach I'll rather use a library by RomellTorres to explore the AlphaVantageAPI, and not the API site.
Let's begin.


```python
import pandas as pd        #for dataframe visualization
from alpha_vantage.foreignexchange import ForeignExchange as FX    #library to use AlphaVantageAPI without link requests
```

* The alpha_vantage Library is the library I'm going to use to interact with Alpha Vantage API. Full documentation is available at https://github.com/RomelTorres/alpha_vantage. 


```python
APIkey = 'ABC'
```

* We'll replace 'ABC' with our API key


```python
fx = FX(key="APIkey")   # defining the forex instance
```


```python
pd.set_option("display.max_rows", 500)    # optional, to display all the rows of the dataframe
```


```python
data = fx.get_currency_exchange_intraday(from_symbol='EUR', to_symbol='USD', interval='60min', outputsize='full')
```

* In the just above cell I passed the parameters to get the intraday data of EURUSD currency pair, and the time interval is set to 1h.


```python
type(data)
```




    tuple



* The data retreived is a tuple. Let's convert it to a datframe for our future operations.


```python
df = pd.DataFrame(data)
```


```python
df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>2021-02-26 11:00:00</th>
      <th>2021-02-26 10:00:00</th>
      <th>2021-02-26 09:00:00</th>
      <th>2021-02-26 08:00:00</th>
      <th>2021-02-26 07:00:00</th>
      <th>2021-02-26 06:00:00</th>
      <th>2021-02-26 05:00:00</th>
      <th>2021-02-26 04:00:00</th>
      <th>2021-02-26 03:00:00</th>
      <th>2021-02-26 02:00:00</th>
      <th>...</th>
      <th>2021-01-01 05:00:00</th>
      <th>2021-01-01 04:00:00</th>
      <th>2021-01-01 03:00:00</th>
      <th>1. Information</th>
      <th>2. From Symbol</th>
      <th>3. To Symbol</th>
      <th>4. Last Refreshed</th>
      <th>5. Interval</th>
      <th>6. Output Size</th>
      <th>7. Time Zone</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>{'1. open': '1.2125', '2. high': '1.2129', '3....</td>
      <td>{'1. open': '1.2149', '2. high': '1.2151', '3....</td>
      <td>{'1. open': '1.2134', '2. high': '1.2160', '3....</td>
      <td>{'1. open': '1.2155', '2. high': '1.2155', '3....</td>
      <td>{'1. open': '1.2154', '2. high': '1.2160', '3....</td>
      <td>{'1. open': '1.2155', '2. high': '1.2160', '3....</td>
      <td>{'1. open': '1.2160', '2. high': '1.2161', '3....</td>
      <td>{'1. open': '1.2172', '2. high': '1.2176', '3....</td>
      <td>{'1. open': '1.2164', '2. high': '1.2183', '3....</td>
      <td>{'1. open': '1.2157', '2. high': '1.2165', '3....</td>
      <td>...</td>
      <td>{'1. open': '1.2214', '2. high': '1.2214', '3....</td>
      <td>{'1. open': '1.2214', '2. high': '1.2214', '3....</td>
      <td>{'1. open': '1.2214', '2. high': '1.2214', '3....</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>FX Intraday (60min) Time Series</td>
      <td>EUR</td>
      <td>USD</td>
      <td>2021-02-26 11:00:00</td>
      <td>60min</td>
      <td>Full size</td>
      <td>UTC</td>
    </tr>
  </tbody>
</table>
<p>2 rows × 968 columns</p>
</div>



So, just above is the output. And, it's quite confusing. Last 7 columns comprise different information. Let's separate them to have a clear idea of the information in these columns.


```python
df[df.columns[-7:]]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>1. Information</th>
      <th>2. From Symbol</th>
      <th>3. To Symbol</th>
      <th>4. Last Refreshed</th>
      <th>5. Interval</th>
      <th>6. Output Size</th>
      <th>7. Time Zone</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>FX Intraday (60min) Time Series</td>
      <td>EUR</td>
      <td>USD</td>
      <td>2021-02-26 11:00:00</td>
      <td>60min</td>
      <td>Full size</td>
      <td>UTC</td>
    </tr>
  </tbody>
</table>
</div>



These columns represent the parameters that we passed with our query to fetch data about the currency pair. The data of our interest lies in the columns before these columns. So, I'll leave these columns as alone and select the rest of columns.


```python
df_col = df.iloc[0, 0:-7]
```


```python
df_col
```




    2021-02-26 11:00:00    {'1. open': '1.2125', '2. high': '1.2129', '3....
    2021-02-26 10:00:00    {'1. open': '1.2149', '2. high': '1.2151', '3....
    2021-02-26 09:00:00    {'1. open': '1.2134', '2. high': '1.2160', '3....
    2021-02-26 08:00:00    {'1. open': '1.2155', '2. high': '1.2155', '3....
    2021-02-26 07:00:00    {'1. open': '1.2154', '2. high': '1.2160', '3....
                                                 ...                        
    2021-01-01 07:00:00    {'1. open': '1.2214', '2. high': '1.2214', '3....
    2021-01-01 06:00:00    {'1. open': '1.2214', '2. high': '1.2214', '3....
    2021-01-01 05:00:00    {'1. open': '1.2214', '2. high': '1.2214', '3....
    2021-01-01 04:00:00    {'1. open': '1.2214', '2. high': '1.2214', '3....
    2021-01-01 03:00:00    {'1. open': '1.2214', '2. high': '1.2214', '3....
    Name: 0, Length: 961, dtype: object



Here the data looks somewhat legible. But, still not as beautiful. Let's decorate it and make it quite legible.


```python
json_data = df_col.to_json('json_data.json')
```

I converted it into a JSON file to store it locally. Now, let's have a look at this data.

First, read this file from the directory.


```python
record = pd.read_json('json_data.json')
```


```python
record
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>2021-02-26 11:00:00</th>
      <th>2021-02-26 10:00:00</th>
      <th>2021-02-26 09:00:00</th>
      <th>2021-02-26 08:00:00</th>
      <th>2021-02-26 07:00:00</th>
      <th>2021-02-26 06:00:00</th>
      <th>2021-02-26 05:00:00</th>
      <th>2021-02-26 04:00:00</th>
      <th>2021-02-26 03:00:00</th>
      <th>2021-02-26 02:00:00</th>
      <th>...</th>
      <th>2021-01-01 12:00:00</th>
      <th>2021-01-01 11:00:00</th>
      <th>2021-01-01 10:00:00</th>
      <th>2021-01-01 09:00:00</th>
      <th>2021-01-01 08:00:00</th>
      <th>2021-01-01 07:00:00</th>
      <th>2021-01-01 06:00:00</th>
      <th>2021-01-01 05:00:00</th>
      <th>2021-01-01 04:00:00</th>
      <th>2021-01-01 03:00:00</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1. open</th>
      <td>1.2125</td>
      <td>1.2149</td>
      <td>1.2134</td>
      <td>1.2155</td>
      <td>1.2154</td>
      <td>1.2155</td>
      <td>1.2160</td>
      <td>1.2172</td>
      <td>1.2164</td>
      <td>1.2157</td>
      <td>...</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
    </tr>
    <tr>
      <th>2. high</th>
      <td>1.2129</td>
      <td>1.2151</td>
      <td>1.2160</td>
      <td>1.2155</td>
      <td>1.2160</td>
      <td>1.2160</td>
      <td>1.2161</td>
      <td>1.2176</td>
      <td>1.2183</td>
      <td>1.2165</td>
      <td>...</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
    </tr>
    <tr>
      <th>3. low</th>
      <td>1.2112</td>
      <td>1.2121</td>
      <td>1.2132</td>
      <td>1.2127</td>
      <td>1.2145</td>
      <td>1.2147</td>
      <td>1.2143</td>
      <td>1.2158</td>
      <td>1.2160</td>
      <td>1.2149</td>
      <td>...</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
    </tr>
    <tr>
      <th>4. close</th>
      <td>1.2114</td>
      <td>1.2125</td>
      <td>1.2150</td>
      <td>1.2135</td>
      <td>1.2153</td>
      <td>1.2153</td>
      <td>1.2155</td>
      <td>1.2160</td>
      <td>1.2172</td>
      <td>1.2163</td>
      <td>...</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
    </tr>
  </tbody>
</table>
<p>4 rows × 961 columns</p>
</div>



Eye-catching!

But, I want the dates as indexes for our price values. And for that, I'll use transpose function of Pandas.


```python
intraday_EURUSD = pd.DataFrame.transpose(record)
```


```python
intraday_EURUSD.head()
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>1. open</th>
      <th>2. high</th>
      <th>3. low</th>
      <th>4. close</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2021-02-26 11:00:00</th>
      <td>1.2125</td>
      <td>1.2129</td>
      <td>1.2112</td>
      <td>1.2114</td>
    </tr>
    <tr>
      <th>2021-02-26 10:00:00</th>
      <td>1.2149</td>
      <td>1.2151</td>
      <td>1.2121</td>
      <td>1.2125</td>
    </tr>
    <tr>
      <th>2021-02-26 09:00:00</th>
      <td>1.2134</td>
      <td>1.2160</td>
      <td>1.2132</td>
      <td>1.2150</td>
    </tr>
    <tr>
      <th>2021-02-26 08:00:00</th>
      <td>1.2155</td>
      <td>1.2155</td>
      <td>1.2127</td>
      <td>1.2135</td>
    </tr>
    <tr>
      <th>2021-02-26 07:00:00</th>
      <td>1.2154</td>
      <td>1.2160</td>
      <td>1.2145</td>
      <td>1.2153</td>
    </tr>
  </tbody>
</table>
</div>



It looks much better.


```python
intraday_EURUSD.reset_index()
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>1. open</th>
      <th>2. high</th>
      <th>3. low</th>
      <th>4. close</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2021-02-26 11:00:00</td>
      <td>1.2125</td>
      <td>1.2129</td>
      <td>1.2112</td>
      <td>1.2114</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2021-02-26 10:00:00</td>
      <td>1.2149</td>
      <td>1.2151</td>
      <td>1.2121</td>
      <td>1.2125</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2021-02-26 09:00:00</td>
      <td>1.2134</td>
      <td>1.2160</td>
      <td>1.2132</td>
      <td>1.2150</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2021-02-26 08:00:00</td>
      <td>1.2155</td>
      <td>1.2155</td>
      <td>1.2127</td>
      <td>1.2135</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2021-02-26 07:00:00</td>
      <td>1.2154</td>
      <td>1.2160</td>
      <td>1.2145</td>
      <td>1.2153</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>956</th>
      <td>2021-01-01 07:00:00</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
    </tr>
    <tr>
      <th>957</th>
      <td>2021-01-01 06:00:00</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
    </tr>
    <tr>
      <th>958</th>
      <td>2021-01-01 05:00:00</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
    </tr>
    <tr>
      <th>959</th>
      <td>2021-01-01 04:00:00</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
    </tr>
    <tr>
      <th>960</th>
      <td>2021-01-01 03:00:00</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
      <td>1.2214</td>
    </tr>
  </tbody>
</table>
<p>961 rows × 5 columns</p>
</div>



Let's plot this.


```python
import matplotlib.pyplot as plt     #the plotting library
```


```python
plt.subplots(figsize=(15, 7.5))
intraday_EURUSD['4. close'].plot()
plt.title('Intraday EURUSD (60 min)')
plt.show()
```


    
![png](Using%20AlphaVantageAPI_files/Using%20AlphaVantageAPI_32_0.png)
    


Beautiful!

Let's represent this in candlestick format.


```python
import plotly.graph_objects as go
```


```python
fig = go.Figure(data=[go.Candlestick(
                open=intraday_EURUSD['1. open'],
                high=intraday_EURUSD['2. high'],
                low=intraday_EURUSD['3. low'],
                close=intraday_EURUSD['4. close'])])
```


```python
fig.update_layout(
    width = 1000,
    height = 700,
    paper_bgcolor="LightSteelBlue",
)
```


<div>                            <div id="a694e134-4f64-469c-8d65-6ccf1522119d" class="plotly-graph-div" style="height:700px; width:1000px;"></div>                </div>


Hurrah, we have plotted candlesticks for EURUSD.
