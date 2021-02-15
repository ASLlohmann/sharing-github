```python
import quandl
import pandas as pd
import matplotlib.pyplot as plt                                                                                                                       
import numpy as np
#inflation germany 
german_cpi=quandl.get("RATEINF/INFLATION_DEU", authtoken="b2P8ovo7y75geHc7vMq_",start_date="2001-12-31", end_date="2021-03-01")
euro_cpi=quandl.get("RATEINF/INFLATION_EUR", authtoken="b2P8ovo7y75geHc7vMq_",start_date="2001-12-31", end_date="2021-03-01")    

with plt.style.context('bmh'):
 fig, ax1 = plt.subplots()
 ax1.plot(german_cpi, color="red",  label="CPI - Germany ")
 ax1.plot(euro_cpi, color="grey",  label="CPI - Eurozone ")
 ax1.axhline(y=2, color='r', linestyle="--")
 plt.title("Eurozone and German CPI (YoY - %) x ECB target", color="Black",fontsize=10,fontweight = 'bold')
 fig.tight_layout()
 plt.legend(bbox_to_anchor=(1.05, 1), loc='upper left', borderaxespad=0.)
 plt.show() 
 

```


![png](output_0_0.png)



```python
italy_cpi=quandl.get("RATEINF/INFLATION_ITA", authtoken="b2P8ovo7y75geHc7vMq_",start_date="2001-12-31", end_date="2021-03-01")    

with plt.style.context('bmh'):
 fig, ax1 = plt.subplots()
 ax1.plot(german_cpi, color="red",  label="CPI - Germany ")
 ax1.plot(italy_cpi, color="grey",  label="CPI - Italy ")
 ax1.axhline(y=2, color='r', linestyle="--")
 plt.title("Italian and German CPI (YoY - %) x ECB target", color="Black",fontsize=10,fontweight = 'bold')
 fig.tight_layout()
 plt.legend(bbox_to_anchor=(1.05, 1), loc='upper left', borderaxespad=0.)
 plt.show() 
 
```


![png](output_1_0.png)



```python
us_cpi=quandl.get("RATEINF/INFLATION_USA", authtoken="b2P8ovo7y75geHc7vMq_",start_date="2001-12-31", end_date="2021-03-01")

with plt.style.context('bmh'):
 fig, ax1 = plt.subplots()
 ax1.plot(us_cpi, color="grey",  label="CPI - US (%) ") 
 ax1.axhline(y=2, color='r', linestyle="--")
 plt.title("US CPI (YoY - %) x Fed target", color="Black",fontsize=10,fontweight = 'bold')
 fig.tight_layout()
 plt.legend(bbox_to_anchor=(1.05, 1), loc='upper left', borderaxespad=0.)
 plt.show() 
 
```


![png](output_2_0.png)



```python

bcom=quandl.get("CHRIS/CME_AW1", transform="rdiff", collapse="monthly", authtoken="b2P8ovo7y75geHc7vMq_",start_date="2012-01-01", end_date="2021-02-20")["Last"]
ism=quandl.get("ISM/MAN_PRICES", authtoken="b2P8ovo7y75geHc7vMq_",start_date="2012-01-01", end_date="2021-02-20")["Index"]
fred=quandl.get("FRED/PPIACO", transform="rdiff", authtoken="b2P8ovo7y75geHc7vMq_",start_date="2012-01-01", end_date="2021-02-20")["Value"]

with plt.style.context('bmh'):
 fig, ax1 = plt.subplots()
 ax1.plot(bcom, color="black",  label="ISM prices", linestyle="--" )
 ax2 = ax1.twinx()  # instantiate a second axes that shares the same x-axis
 ax2.plot(fred*100, color="red",  label="PPI index (%)")
 plt.title("Montlhy PPI x Bloomberg commodity index", color="black",fontsize=10,fontweight = 'bold')
 plt.legend(bbox_to_anchor=(1.05, 1), loc='upper left', borderaxespad=0.)
 fig.tight_layout()
 plt.show()

```


![png](output_3_0.png)



```python

ism=quandl.get("ISM/MAN_PRICES", authtoken="b2P8ovo7y75geHc7vMq_",start_date="2005-01-01", end_date="2021-02-20")["Index"]
fred=quandl.get("FRED/PPIACO", transform="rdiff", authtoken="b2P8ovo7y75geHc7vMq_",start_date="2005-01-01", end_date="2021-02-20")["Value"]

with plt.style.context('bmh'):
 fig, ax1 = plt.subplots()
 ax1.plot(ism, color="red",  label="ISM prices")
 ax2 = ax1.twinx()  # instantiate a second axes that shares the same x-axis
 ax2.plot(fred*100, color="grey",  label="PPI index (%)", linestyle="--" )
 plt.title("Montlhy PPI x ISM Manufacturing Prices", color="black",fontsize=10,fontweight = 'bold')
 plt.legend(bbox_to_anchor=(1.05, 1), loc='upper left', borderaxespad=0.)
 fig.tight_layout()
 plt.show()
```


![png](output_4_0.png)



```python
df = pd.read_excel ('C:/Users/Alexandre Lohmann/Desktop/python/Food_price_indices_data_feb1.xls')
x1 = df["Food Price Index"]
index_date=pd.date_range(start="1991-01-01",end="2021-01-31", freq="m")
x1.index=index_date
fred_2=np.log2(quandl.get("FRED/CPIUFDSL", authtoken="b2P8ovo7y75geHc7vMq_",start_date="1991-01-01", end_date="2021-02-20")["Value"]).diff(periods=12)


with plt.style.context('bmh'):
 fig, ax1 = plt.subplots()
 ax1.plot(x1, color="Red",  label="US CPI - Food", linestyle="--" )
 plt.title("US CPI - Food x FAO Food price index (YoY - %) ", color="black",fontsize=10,fontweight = 'bold')
 ax2 = ax1.twinx()  # instantiate a second axes that shares the same x-axis
 ax2.plot(fred_2, color="blue",  label="FAO Food price index")
 plt.legend(bbox_to_anchor=(1.05, 1), loc='upper left', borderaxespad=0.)
 fig.tight_layout()
 plt.show()
```


![png](output_5_0.png)

