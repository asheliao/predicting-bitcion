# 以傳統均線法(MA)和指數平滑異同移動平均線(MACD)<br />預測比特幣之最佳買點
Predicting the best buying point of bitcoin with Python Pandas / MA / MACD
<br />

### Bitcoin price source
https://www.coingecko.com/zh-tw

***

### Import packages
* requests, BeautifulSoup for web clawler
* re, json for preprocess cleaning
* pandas for buliding dataframe
* matlibplot, pandas for plot

### Calculate MA, EMA
```
ma_list = [12, 26]
for ma in ma_list:
    df['EMA_' + str(ma)] = df["twd"].ewm(span = ma).mean()
for ma in ma_list:
    df['MA_' + str(ma)] = df["twd"].rolling(window = ma).mean()
```
* `MA` for Moving Average 12d / 26d
* `EMA` for Exponential Moving Averages 12d / 26d

### Calculate DIF, DEM
```
df['dif'] = df['EMA_12'] - df['EMA_26']
df["dem"] = df["dif"].ewm(span = 9).mean()
```
* `dif` for difference between EMA_12 and EMA_26
* `dem` for signal line, using DIF and calculate for its exponential moving average 9d

## Strategy

* If `MA_12` and `MA_26` across through the price line upward ,then buy in bitcoin, vice versa.
* If `dif` across through `dem` upward, then buy in bitcoin, vice versa.


## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments
* references: largitdata.com 

