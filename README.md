# forex_Vantage
Using AlphaVantageAPI for fetching and analysing forex data.
{
 "cells": [
  {
   "cell_type": "markdown",
   "id": "compliant-policy",
   "metadata": {},
   "source": [
    "# Using Alpha Vantage API to Analyse Financial Data\n",
    "In this section I will use Alpha Vantage API to analyze forex data. Let's first import some required libraries. To use any API we are generally required to pass an API key with the search parameters. So, for AlphaVantageAPI we can get one from https://www.alphavantage.co/. In this approach I'll rather use a library by RomellTorres to explore the AlphaVantageAPI, and not the API site.\n",
    "Let's begin."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 160,
   "id": "elegant-rubber",
   "metadata": {},
   "outputs": [],
   "source": [
    "import pandas as pd        #for dataframe visualization\n",
    "from alpha_vantage.foreignexchange import ForeignExchange as FX    #library to use AlphaVantageAPI without link requests"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "norman-speaking",
   "metadata": {},
   "source": [
    "* The alpha_vantage Library is the library I'm going to use to interact with Alpha Vantage API. Full documentation is available at https://github.com/RomelTorres/alpha_vantage. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 161,
   "id": "obvious-banana",
   "metadata": {},
   "outputs": [],
   "source": [
    "APIkey = 'ABC'"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "sharing-andrew",
   "metadata": {},
   "source": [
    "* We'll replace 'ABC' with our API key"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 165,
   "id": "valid-relief",
   "metadata": {},
   "outputs": [],
   "source": [
    "fx = FX(key=\"APIkey\")   # defining the forex instance"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 166,
   "id": "signal-milwaukee",
   "metadata": {},
   "outputs": [],
   "source": [
    "pd.set_option(\"display.max_rows\", 500)    # optional, to display all the rows of the dataframe"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 168,
   "id": "published-wagner",
   "metadata": {},
   "outputs": [],
   "source": [
    "data = fx.get_currency_exchange_intraday(from_symbol='EUR', to_symbol='USD', interval='60min', outputsize='full')"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "stunning-aurora",
   "metadata": {},
   "source": [
    "* In the just above cell I passed the parameters to get the intraday data of EURUSD currency pair, and the time interval is set to 1h."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 171,
   "id": "capital-truck",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "tuple"
      ]
     },
     "execution_count": 171,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "type(data)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "analyzed-flooring",
   "metadata": {},
   "source": [
    "* The data retreived is a tuple. Let's convert it to a datframe for our future operations."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 175,
   "id": "regulated-catch",
   "metadata": {
    "scrolled": true,
    "tags": []
   },
   "outputs": [],
   "source": [
    "df = pd.DataFrame(data)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 176,
   "id": "wired-landing",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>2021-02-25 11:00:00</th>\n",
       "      <th>2021-02-25 10:00:00</th>\n",
       "      <th>2021-02-25 09:00:00</th>\n",
       "      <th>2021-02-25 08:00:00</th>\n",
       "      <th>2021-02-25 07:00:00</th>\n",
       "      <th>2021-02-25 06:00:00</th>\n",
       "      <th>2021-02-25 05:00:00</th>\n",
       "      <th>2021-02-25 04:00:00</th>\n",
       "      <th>2021-02-25 03:00:00</th>\n",
       "      <th>2021-02-25 02:00:00</th>\n",
       "      <th>...</th>\n",
       "      <th>2020-12-31 05:00:00</th>\n",
       "      <th>2020-12-31 04:00:00</th>\n",
       "      <th>2020-12-31 03:00:00</th>\n",
       "      <th>1. Information</th>\n",
       "      <th>2. From Symbol</th>\n",
       "      <th>3. To Symbol</th>\n",
       "      <th>4. Last Refreshed</th>\n",
       "      <th>5. Interval</th>\n",
       "      <th>6. Output Size</th>\n",
       "      <th>7. Time Zone</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>{'1. open': '1.2220', '2. high': '1.2231', '3....</td>\n",
       "      <td>{'1. open': '1.2208', '2. high': '1.2223', '3....</td>\n",
       "      <td>{'1. open': '1.2187', '2. high': '1.2208', '3....</td>\n",
       "      <td>{'1. open': '1.2181', '2. high': '1.2189', '3....</td>\n",
       "      <td>{'1. open': '1.2178', '2. high': '1.2182', '3....</td>\n",
       "      <td>{'1. open': '1.2176', '2. high': '1.2183', '3....</td>\n",
       "      <td>{'1. open': '1.2169', '2. high': '1.2177', '3....</td>\n",
       "      <td>{'1. open': '1.2159', '2. high': '1.2170', '3....</td>\n",
       "      <td>{'1. open': '1.2157', '2. high': '1.2163', '3....</td>\n",
       "      <td>{'1. open': '1.2162', '2. high': '1.2165', '3....</td>\n",
       "      <td>...</td>\n",
       "      <td>{'1. open': '1.2291', '2. high': '1.2291', '3....</td>\n",
       "      <td>{'1. open': '1.2289', '2. high': '1.2294', '3....</td>\n",
       "      <td>{'1. open': '1.2306', '2. high': '1.2309', '3....</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>...</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>FX Intraday (60min) Time Series</td>\n",
       "      <td>EUR</td>\n",
       "      <td>USD</td>\n",
       "      <td>2021-02-25 11:00:00</td>\n",
       "      <td>60min</td>\n",
       "      <td>Full size</td>\n",
       "      <td>UTC</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>2 rows × 968 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "                                 2021-02-25 11:00:00  \\\n",
       "0  {'1. open': '1.2220', '2. high': '1.2231', '3....   \n",
       "1                                                NaN   \n",
       "\n",
       "                                 2021-02-25 10:00:00  \\\n",
       "0  {'1. open': '1.2208', '2. high': '1.2223', '3....   \n",
       "1                                                NaN   \n",
       "\n",
       "                                 2021-02-25 09:00:00  \\\n",
       "0  {'1. open': '1.2187', '2. high': '1.2208', '3....   \n",
       "1                                                NaN   \n",
       "\n",
       "                                 2021-02-25 08:00:00  \\\n",
       "0  {'1. open': '1.2181', '2. high': '1.2189', '3....   \n",
       "1                                                NaN   \n",
       "\n",
       "                                 2021-02-25 07:00:00  \\\n",
       "0  {'1. open': '1.2178', '2. high': '1.2182', '3....   \n",
       "1                                                NaN   \n",
       "\n",
       "                                 2021-02-25 06:00:00  \\\n",
       "0  {'1. open': '1.2176', '2. high': '1.2183', '3....   \n",
       "1                                                NaN   \n",
       "\n",
       "                                 2021-02-25 05:00:00  \\\n",
       "0  {'1. open': '1.2169', '2. high': '1.2177', '3....   \n",
       "1                                                NaN   \n",
       "\n",
       "                                 2021-02-25 04:00:00  \\\n",
       "0  {'1. open': '1.2159', '2. high': '1.2170', '3....   \n",
       "1                                                NaN   \n",
       "\n",
       "                                 2021-02-25 03:00:00  \\\n",
       "0  {'1. open': '1.2157', '2. high': '1.2163', '3....   \n",
       "1                                                NaN   \n",
       "\n",
       "                                 2021-02-25 02:00:00  ...  \\\n",
       "0  {'1. open': '1.2162', '2. high': '1.2165', '3....  ...   \n",
       "1                                                NaN  ...   \n",
       "\n",
       "                                 2020-12-31 05:00:00  \\\n",
       "0  {'1. open': '1.2291', '2. high': '1.2291', '3....   \n",
       "1                                                NaN   \n",
       "\n",
       "                                 2020-12-31 04:00:00  \\\n",
       "0  {'1. open': '1.2289', '2. high': '1.2294', '3....   \n",
       "1                                                NaN   \n",
       "\n",
       "                                 2020-12-31 03:00:00  \\\n",
       "0  {'1. open': '1.2306', '2. high': '1.2309', '3....   \n",
       "1                                                NaN   \n",
       "\n",
       "                    1. Information 2. From Symbol 3. To Symbol  \\\n",
       "0                              NaN            NaN          NaN   \n",
       "1  FX Intraday (60min) Time Series            EUR          USD   \n",
       "\n",
       "     4. Last Refreshed 5. Interval 6. Output Size 7. Time Zone  \n",
       "0                  NaN         NaN            NaN          NaN  \n",
       "1  2021-02-25 11:00:00       60min      Full size          UTC  \n",
       "\n",
       "[2 rows x 968 columns]"
      ]
     },
     "execution_count": 176,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "facial-customs",
   "metadata": {},
   "source": [
    "So, just above is the output. And, it's quite confusing. Last 7 columns comprise different information. Let's separate them to have a clear idea of the information in these columns."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 177,
   "id": "weird-hypothetical",
   "metadata": {
    "scrolled": true,
    "tags": []
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>1. Information</th>\n",
       "      <th>2. From Symbol</th>\n",
       "      <th>3. To Symbol</th>\n",
       "      <th>4. Last Refreshed</th>\n",
       "      <th>5. Interval</th>\n",
       "      <th>6. Output Size</th>\n",
       "      <th>7. Time Zone</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>FX Intraday (60min) Time Series</td>\n",
       "      <td>EUR</td>\n",
       "      <td>USD</td>\n",
       "      <td>2021-02-25 11:00:00</td>\n",
       "      <td>60min</td>\n",
       "      <td>Full size</td>\n",
       "      <td>UTC</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                    1. Information 2. From Symbol 3. To Symbol  \\\n",
       "0                              NaN            NaN          NaN   \n",
       "1  FX Intraday (60min) Time Series            EUR          USD   \n",
       "\n",
       "     4. Last Refreshed 5. Interval 6. Output Size 7. Time Zone  \n",
       "0                  NaN         NaN            NaN          NaN  \n",
       "1  2021-02-25 11:00:00       60min      Full size          UTC  "
      ]
     },
     "execution_count": 177,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df[df.columns[-7:]]"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "varying-italic",
   "metadata": {},
   "source": [
    "These columns represent the parameters that we passed with our query to fetch data about the currency pair. The data of our interest lies in the columns before these columns. So, I'll leave these columns as alone and select the rest of columns."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 179,
   "id": "statistical-fiber",
   "metadata": {},
   "outputs": [],
   "source": [
    "df_col = df.iloc[0, 0:-7]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 181,
   "id": "subject-hotel",
   "metadata": {
    "scrolled": true,
    "tags": []
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "2021-02-25 11:00:00    {'1. open': '1.2220', '2. high': '1.2231', '3....\n",
       "2021-02-25 10:00:00    {'1. open': '1.2208', '2. high': '1.2223', '3....\n",
       "2021-02-25 09:00:00    {'1. open': '1.2187', '2. high': '1.2208', '3....\n",
       "2021-02-25 08:00:00    {'1. open': '1.2181', '2. high': '1.2189', '3....\n",
       "2021-02-25 07:00:00    {'1. open': '1.2178', '2. high': '1.2182', '3....\n",
       "                                             ...                        \n",
       "2020-12-31 07:00:00    {'1. open': '1.2289', '2. high': '1.2293', '3....\n",
       "2020-12-31 06:00:00    {'1. open': '1.2286', '2. high': '1.2297', '3....\n",
       "2020-12-31 05:00:00    {'1. open': '1.2291', '2. high': '1.2291', '3....\n",
       "2020-12-31 04:00:00    {'1. open': '1.2289', '2. high': '1.2294', '3....\n",
       "2020-12-31 03:00:00    {'1. open': '1.2306', '2. high': '1.2309', '3....\n",
       "Name: 0, Length: 961, dtype: object"
      ]
     },
     "execution_count": 181,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df_col"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "differential-hometown",
   "metadata": {},
   "source": [
    "Here the data looks somewhat legible. But, still not as beautiful. Let's decorate it and make it quite legible."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 186,
   "id": "fallen-western",
   "metadata": {},
   "outputs": [],
   "source": [
    "json_data = df_col.to_json('json_data.json')"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "abstract-compact",
   "metadata": {},
   "source": [
    "I converted it into a JSON file to store it locally. Now, let's have a look at this data."
   ]
  },
  {
   "cell_type": "markdown",
   "id": "threatened-schema",
   "metadata": {},
   "source": [
    "First, read this file from the directory."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 188,
   "id": "latter-wrapping",
   "metadata": {},
   "outputs": [],
   "source": [
    "record = pd.read_json('json_data.json')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 189,
   "id": "outdoor-wallace",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>2021-02-25 11:00:00</th>\n",
       "      <th>2021-02-25 10:00:00</th>\n",
       "      <th>2021-02-25 09:00:00</th>\n",
       "      <th>2021-02-25 08:00:00</th>\n",
       "      <th>2021-02-25 07:00:00</th>\n",
       "      <th>2021-02-25 06:00:00</th>\n",
       "      <th>2021-02-25 05:00:00</th>\n",
       "      <th>2021-02-25 04:00:00</th>\n",
       "      <th>2021-02-25 03:00:00</th>\n",
       "      <th>2021-02-25 02:00:00</th>\n",
       "      <th>...</th>\n",
       "      <th>2020-12-31 12:00:00</th>\n",
       "      <th>2020-12-31 11:00:00</th>\n",
       "      <th>2020-12-31 10:00:00</th>\n",
       "      <th>2020-12-31 09:00:00</th>\n",
       "      <th>2020-12-31 08:00:00</th>\n",
       "      <th>2020-12-31 07:00:00</th>\n",
       "      <th>2020-12-31 06:00:00</th>\n",
       "      <th>2020-12-31 05:00:00</th>\n",
       "      <th>2020-12-31 04:00:00</th>\n",
       "      <th>2020-12-31 03:00:00</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>1. open</th>\n",
       "      <td>1.2220</td>\n",
       "      <td>1.2208</td>\n",
       "      <td>1.2187</td>\n",
       "      <td>1.2181</td>\n",
       "      <td>1.2178</td>\n",
       "      <td>1.2176</td>\n",
       "      <td>1.2169</td>\n",
       "      <td>1.2159</td>\n",
       "      <td>1.2157</td>\n",
       "      <td>1.2162</td>\n",
       "      <td>...</td>\n",
       "      <td>1.2279</td>\n",
       "      <td>1.2279</td>\n",
       "      <td>1.2301</td>\n",
       "      <td>1.2296</td>\n",
       "      <td>1.2291</td>\n",
       "      <td>1.2289</td>\n",
       "      <td>1.2286</td>\n",
       "      <td>1.2291</td>\n",
       "      <td>1.2289</td>\n",
       "      <td>1.2306</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2. high</th>\n",
       "      <td>1.2231</td>\n",
       "      <td>1.2223</td>\n",
       "      <td>1.2208</td>\n",
       "      <td>1.2189</td>\n",
       "      <td>1.2182</td>\n",
       "      <td>1.2183</td>\n",
       "      <td>1.2177</td>\n",
       "      <td>1.2170</td>\n",
       "      <td>1.2163</td>\n",
       "      <td>1.2165</td>\n",
       "      <td>...</td>\n",
       "      <td>1.2288</td>\n",
       "      <td>1.2288</td>\n",
       "      <td>1.2301</td>\n",
       "      <td>1.2304</td>\n",
       "      <td>1.2303</td>\n",
       "      <td>1.2293</td>\n",
       "      <td>1.2297</td>\n",
       "      <td>1.2291</td>\n",
       "      <td>1.2294</td>\n",
       "      <td>1.2309</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3. low</th>\n",
       "      <td>1.2216</td>\n",
       "      <td>1.2202</td>\n",
       "      <td>1.2185</td>\n",
       "      <td>1.2166</td>\n",
       "      <td>1.2172</td>\n",
       "      <td>1.2174</td>\n",
       "      <td>1.2165</td>\n",
       "      <td>1.2158</td>\n",
       "      <td>1.2154</td>\n",
       "      <td>1.2155</td>\n",
       "      <td>...</td>\n",
       "      <td>1.2265</td>\n",
       "      <td>1.2273</td>\n",
       "      <td>1.2275</td>\n",
       "      <td>1.2285</td>\n",
       "      <td>1.2289</td>\n",
       "      <td>1.2284</td>\n",
       "      <td>1.2284</td>\n",
       "      <td>1.2284</td>\n",
       "      <td>1.2285</td>\n",
       "      <td>1.2284</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4. close</th>\n",
       "      <td>1.2228</td>\n",
       "      <td>1.2220</td>\n",
       "      <td>1.2206</td>\n",
       "      <td>1.2186</td>\n",
       "      <td>1.2180</td>\n",
       "      <td>1.2178</td>\n",
       "      <td>1.2176</td>\n",
       "      <td>1.2168</td>\n",
       "      <td>1.2160</td>\n",
       "      <td>1.2157</td>\n",
       "      <td>...</td>\n",
       "      <td>1.2275</td>\n",
       "      <td>1.2280</td>\n",
       "      <td>1.2278</td>\n",
       "      <td>1.2301</td>\n",
       "      <td>1.2296</td>\n",
       "      <td>1.2291</td>\n",
       "      <td>1.2289</td>\n",
       "      <td>1.2287</td>\n",
       "      <td>1.2290</td>\n",
       "      <td>1.2288</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>4 rows × 961 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "          2021-02-25 11:00:00  2021-02-25 10:00:00  2021-02-25 09:00:00  \\\n",
       "1. open                1.2220               1.2208               1.2187   \n",
       "2. high                1.2231               1.2223               1.2208   \n",
       "3. low                 1.2216               1.2202               1.2185   \n",
       "4. close               1.2228               1.2220               1.2206   \n",
       "\n",
       "          2021-02-25 08:00:00  2021-02-25 07:00:00  2021-02-25 06:00:00  \\\n",
       "1. open                1.2181               1.2178               1.2176   \n",
       "2. high                1.2189               1.2182               1.2183   \n",
       "3. low                 1.2166               1.2172               1.2174   \n",
       "4. close               1.2186               1.2180               1.2178   \n",
       "\n",
       "          2021-02-25 05:00:00  2021-02-25 04:00:00  2021-02-25 03:00:00  \\\n",
       "1. open                1.2169               1.2159               1.2157   \n",
       "2. high                1.2177               1.2170               1.2163   \n",
       "3. low                 1.2165               1.2158               1.2154   \n",
       "4. close               1.2176               1.2168               1.2160   \n",
       "\n",
       "          2021-02-25 02:00:00  ...  2020-12-31 12:00:00  2020-12-31 11:00:00  \\\n",
       "1. open                1.2162  ...               1.2279               1.2279   \n",
       "2. high                1.2165  ...               1.2288               1.2288   \n",
       "3. low                 1.2155  ...               1.2265               1.2273   \n",
       "4. close               1.2157  ...               1.2275               1.2280   \n",
       "\n",
       "          2020-12-31 10:00:00  2020-12-31 09:00:00  2020-12-31 08:00:00  \\\n",
       "1. open                1.2301               1.2296               1.2291   \n",
       "2. high                1.2301               1.2304               1.2303   \n",
       "3. low                 1.2275               1.2285               1.2289   \n",
       "4. close               1.2278               1.2301               1.2296   \n",
       "\n",
       "          2020-12-31 07:00:00  2020-12-31 06:00:00  2020-12-31 05:00:00  \\\n",
       "1. open                1.2289               1.2286               1.2291   \n",
       "2. high                1.2293               1.2297               1.2291   \n",
       "3. low                 1.2284               1.2284               1.2284   \n",
       "4. close               1.2291               1.2289               1.2287   \n",
       "\n",
       "          2020-12-31 04:00:00  2020-12-31 03:00:00  \n",
       "1. open                1.2289               1.2306  \n",
       "2. high                1.2294               1.2309  \n",
       "3. low                 1.2285               1.2284  \n",
       "4. close               1.2290               1.2288  \n",
       "\n",
       "[4 rows x 961 columns]"
      ]
     },
     "execution_count": 189,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "record"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "stuck-mixture",
   "metadata": {},
   "source": [
    "Eye-catching!"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "later-apparatus",
   "metadata": {},
   "source": [
    "But, I want the dates as indexes for our price values. And for that, I'll use transpose function of Pandas."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 210,
   "id": "exempt-dance",
   "metadata": {},
   "outputs": [],
   "source": [
    "intraday_EURUSD = pd.DataFrame.transpose(record)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 219,
   "id": "detected-courage",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>1. open</th>\n",
       "      <th>2. high</th>\n",
       "      <th>3. low</th>\n",
       "      <th>4. close</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2021-02-25 11:00:00</th>\n",
       "      <td>1.2220</td>\n",
       "      <td>1.2231</td>\n",
       "      <td>1.2216</td>\n",
       "      <td>1.2228</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2021-02-25 10:00:00</th>\n",
       "      <td>1.2208</td>\n",
       "      <td>1.2223</td>\n",
       "      <td>1.2202</td>\n",
       "      <td>1.2220</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2021-02-25 09:00:00</th>\n",
       "      <td>1.2187</td>\n",
       "      <td>1.2208</td>\n",
       "      <td>1.2185</td>\n",
       "      <td>1.2206</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2021-02-25 08:00:00</th>\n",
       "      <td>1.2181</td>\n",
       "      <td>1.2189</td>\n",
       "      <td>1.2166</td>\n",
       "      <td>1.2186</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2021-02-25 07:00:00</th>\n",
       "      <td>1.2178</td>\n",
       "      <td>1.2182</td>\n",
       "      <td>1.2172</td>\n",
       "      <td>1.2180</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                     1. open  2. high  3. low  4. close\n",
       "2021-02-25 11:00:00   1.2220   1.2231  1.2216    1.2228\n",
       "2021-02-25 10:00:00   1.2208   1.2223  1.2202    1.2220\n",
       "2021-02-25 09:00:00   1.2187   1.2208  1.2185    1.2206\n",
       "2021-02-25 08:00:00   1.2181   1.2189  1.2166    1.2186\n",
       "2021-02-25 07:00:00   1.2178   1.2182  1.2172    1.2180"
      ]
     },
     "execution_count": 219,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "intraday_EURUSD.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "enclosed-intention",
   "metadata": {},
   "source": [
    "It looks much better."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 220,
   "id": "criminal-cleanup",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>index</th>\n",
       "      <th>1. open</th>\n",
       "      <th>2. high</th>\n",
       "      <th>3. low</th>\n",
       "      <th>4. close</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>2021-02-25 11:00:00</td>\n",
       "      <td>1.2220</td>\n",
       "      <td>1.2231</td>\n",
       "      <td>1.2216</td>\n",
       "      <td>1.2228</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2021-02-25 10:00:00</td>\n",
       "      <td>1.2208</td>\n",
       "      <td>1.2223</td>\n",
       "      <td>1.2202</td>\n",
       "      <td>1.2220</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>2021-02-25 09:00:00</td>\n",
       "      <td>1.2187</td>\n",
       "      <td>1.2208</td>\n",
       "      <td>1.2185</td>\n",
       "      <td>1.2206</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>2021-02-25 08:00:00</td>\n",
       "      <td>1.2181</td>\n",
       "      <td>1.2189</td>\n",
       "      <td>1.2166</td>\n",
       "      <td>1.2186</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>2021-02-25 07:00:00</td>\n",
       "      <td>1.2178</td>\n",
       "      <td>1.2182</td>\n",
       "      <td>1.2172</td>\n",
       "      <td>1.2180</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>956</th>\n",
       "      <td>2020-12-31 07:00:00</td>\n",
       "      <td>1.2289</td>\n",
       "      <td>1.2293</td>\n",
       "      <td>1.2284</td>\n",
       "      <td>1.2291</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>957</th>\n",
       "      <td>2020-12-31 06:00:00</td>\n",
       "      <td>1.2286</td>\n",
       "      <td>1.2297</td>\n",
       "      <td>1.2284</td>\n",
       "      <td>1.2289</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>958</th>\n",
       "      <td>2020-12-31 05:00:00</td>\n",
       "      <td>1.2291</td>\n",
       "      <td>1.2291</td>\n",
       "      <td>1.2284</td>\n",
       "      <td>1.2287</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>959</th>\n",
       "      <td>2020-12-31 04:00:00</td>\n",
       "      <td>1.2289</td>\n",
       "      <td>1.2294</td>\n",
       "      <td>1.2285</td>\n",
       "      <td>1.2290</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>960</th>\n",
       "      <td>2020-12-31 03:00:00</td>\n",
       "      <td>1.2306</td>\n",
       "      <td>1.2309</td>\n",
       "      <td>1.2284</td>\n",
       "      <td>1.2288</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>961 rows × 5 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "                  index  1. open  2. high  3. low  4. close\n",
       "0   2021-02-25 11:00:00   1.2220   1.2231  1.2216    1.2228\n",
       "1   2021-02-25 10:00:00   1.2208   1.2223  1.2202    1.2220\n",
       "2   2021-02-25 09:00:00   1.2187   1.2208  1.2185    1.2206\n",
       "3   2021-02-25 08:00:00   1.2181   1.2189  1.2166    1.2186\n",
       "4   2021-02-25 07:00:00   1.2178   1.2182  1.2172    1.2180\n",
       "..                  ...      ...      ...     ...       ...\n",
       "956 2020-12-31 07:00:00   1.2289   1.2293  1.2284    1.2291\n",
       "957 2020-12-31 06:00:00   1.2286   1.2297  1.2284    1.2289\n",
       "958 2020-12-31 05:00:00   1.2291   1.2291  1.2284    1.2287\n",
       "959 2020-12-31 04:00:00   1.2289   1.2294  1.2285    1.2290\n",
       "960 2020-12-31 03:00:00   1.2306   1.2309  1.2284    1.2288\n",
       "\n",
       "[961 rows x 5 columns]"
      ]
     },
     "execution_count": 220,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "intraday_EURUSD.reset_index()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "gross-boston",
   "metadata": {},
   "source": [
    "Let's plot this."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 214,
   "id": "severe-millennium",
   "metadata": {
    "scrolled": true,
    "tags": []
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Requirement already satisfied: matplotlib in c:\\users\\irfan\\miniconda3\\lib\\site-packages (3.3.4)\n",
      "Requirement already satisfied: python-dateutil>=2.1 in c:\\users\\irfan\\miniconda3\\lib\\site-packages (from matplotlib) (2.8.1)\n",
      "Requirement already satisfied: pillow>=6.2.0 in c:\\users\\irfan\\miniconda3\\lib\\site-packages (from matplotlib) (8.1.0)\n",
      "Requirement already satisfied: numpy>=1.15 in c:\\users\\irfan\\miniconda3\\lib\\site-packages (from matplotlib) (1.20.1)\n",
      "Requirement already satisfied: cycler>=0.10 in c:\\users\\irfan\\miniconda3\\lib\\site-packages (from matplotlib) (0.10.0)\n",
      "Requirement already satisfied: pyparsing!=2.0.4,!=2.1.2,!=2.1.6,>=2.0.3 in c:\\users\\irfan\\miniconda3\\lib\\site-packages (from matplotlib) (2.4.7)\n",
      "Requirement already satisfied: kiwisolver>=1.0.1 in c:\\users\\irfan\\miniconda3\\lib\\site-packages (from matplotlib) (1.3.1)\n",
      "Requirement already satisfied: six>=1.5 in c:\\users\\irfan\\miniconda3\\lib\\site-packages (from python-dateutil>=2.1->matplotlib) (1.14.0)\n",
      "Note: you may need to restart the kernel to use updated packages.\n"
     ]
    }
   ],
   "source": [
    "pip install matplotlib  "
   ]
  },
  {
   "cell_type": "markdown",
   "id": "tired-delicious",
   "metadata": {},
   "source": [
    "I have just installed the matplotlib library for plotting the graph. Let's plot the forex values."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 217,
   "id": "exceptional-barrel",
   "metadata": {},
   "outputs": [],
   "source": [
    "import matplotlib.pyplot as plt     #the plotting library"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 231,
   "id": "outside-archives",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 1080x540 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.subplots(figsize=(15, 7.5))\n",
    "intraday_EURUSD['4. close'].plot()\n",
    "plt.title('Intraday EURUSD (60 min)')\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "postal-canyon",
   "metadata": {},
   "source": [
    "Beautiful!"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "increased-synthetic",
   "metadata": {},
   "source": [
    "# With this, good bey. "
   ]
  },
  {
   "cell_type": "markdown",
   "id": "featured-confidentiality",
   "metadata": {},
   "source": [
    "# If you enjoyed, make sure to join me."
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.8.3"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 5
}
