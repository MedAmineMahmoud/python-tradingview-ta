# Usage

This guide will help you to set up your code to your need. Be sure to install the package first. See [Getting Started](overview.md) if you haven't installed it.

## Importing the module
```python
from tradingview_ta import TA_Handler
```

## Instantiating the TA_Handler class
```python
handler = TA_Handler()
```

## Setting the symbol
[Symbol](https://en.wikipedia.org/wiki/Ticker_symbol) (or ticker symbol) is an abbreviation of a stock or currency.
```python
# Tesla's stock
handler.symbol = "TSLA" 
```
Another example:
```python
# Bitcoin/USD Tether pair
handler.symbol = "BTCUSDT"
```
Another example:
```python
# USD/EUR pair
handler.symbol = "USDEUR"
```

## Setting the exchange
An [exchange](https://en.wikipedia.org/wiki/Stock_exchange) (or exchanger, stock exchage, bourse) is a facility where traders can buy/sell their securities.

Example of exchange:
* Stock: `NASDAQ`, `NYSE`, etc.
* Crypto: `BINANCE`, `BITTREX`, etc.

```python
# Nasdaq stock exchange
handler.exchange = "NASDAQ"
```

For forex, you can use `FX_IDC` as the exchange, and for CFD, you can use `TVC` as the exchange. They are not an exchange, but they provide data to TradingView.

## Setting the screener
Screener is a little bit hard to explain. The meaning can be different.

### Stock
Exchange's country of origin.
For example, since NASDAQ is from the United States of America, put `america` as the screener.
```python
handler.screener = "america"
```

### Crypto
Put `crypto` as the screener.
```python
handler.screener = "crypto"
```

### Forex
Put `forex` as the screener.
```python
handler.screener = "forex"
```

### CFD
Put `cfd` as the screener.
```python
handler.screener = "cfd"
```

## Setting the interval
TradingView has some available intervals to use. From 1 Minute to 1 Month. See available intervals below.

`interval` is case sensitive. So, be careful.

### 1 Minute
```python
handler.interval = "1m"
```

### 5 Minutes
```python
handler.interval = "5m"
```

### 15 Minutes
```python
handler.interval = "15m"
```

### 1 Hour
```python
handler.interval = "1h"
```

### 4 Hours
```python
handler.interval = "4h"
```

### 1 Day (Default)
```python
handler.interval = "1d"
```

### 1 Week
```python
handler.interval = "1W"
```

### 1 Month
```python
handler.interval = "1M"
```

## Getting the analysis
To get the analysis, simply call the `get_analysis()` function.
```python
analysis = handler.get_analysis()
```

The `get_analysis()` function will return an object of `Analysis` class, which store the analysis, time created, ticker symbol, exchange, and screener.

### Analysis
There are 3 types of analysis in TradingView. Oscillators, moving averages, and summary (which is oscillators and moving averages combined).

#### Summary
```python
print(analysis.summary)
# Example output: {'RECOMMENDATION': 'BUY', 'BUY': 12, 'SELL': 7, 'NEUTRAL': 9}
```

#### Oscillators
```python
print(analysis.oscillators)
# Example output: {'RECOMMENDATION': 'BUY', 'BUY': 2, 'SELL': 1, 'NEUTRAL': 8, 'COMPUTE': {'RSI': 'NEUTRAL', 'STOCH.K': 'NEUTRAL', 'CCI': 'NEUTRAL', 'ADX': 'NEUTRAL', 'AO': 'NEUTRAL', 'Mom': 'BUY', 'MACD': 'SELL', 'Stoch.RSI': 'NEUTRAL', 'W%R': 'NEUTRAL', 'BBP': 'BUY', 'UO': 'NEUTRAL'}}
```

#### Moving Averages
```python
print(analysis.moving_averages)
# Example output: {'RECOMMENDATION': 'BUY', 'BUY': 10, 'SELL': 6, 'NEUTRAL': 1, 'COMPUTE': {'EMA5': 'SELL', 'SMA5': 'BUY', 'EMA10': 'SELL', 'SMA10': 'SELL', 'EMA20': 'SELL', 'SMA20': 'SELL', 'EMA30': 'BUY', 'SMA30': 'BUY', 'EMA50': 'BUY', 'SMA50': 'BUY', 'EMA100': 'BUY', 'SMA100': 'BUY', 'EMA200': 'BUY', 'SMA200': 'BUY', 'Ichimoku': 'NEUTRAL', 'VWMA': 'SELL', 'HullMA': 'BUY'}}
```

Notice that if we sum the oscillators and the moving averages, we'll get the result similar to the summary.

### Indicator values
You can also get the value of the indicators used in the analysis.

```python
print(analysis.indicators)
# Example output: {'Recommend.Other': 0.09090909, 'Recommend.All': 0.17878788, 'Recommend.MA': 0.26666667, 'RSI': 51.35657473, 'RSI[1]': 56.0809039, 'Stoch.K': 40.83410422, 'Stoch.D': 36.71946441, 'Stoch.K[1]': 31.67255276, 'Stoch.D[1]': 39.57313164, 'CCI20': -52.17234223, 'CCI20[1]': 4.5072255, 'ADX': 35.60476973, 'ADX+DI': 28.49583595, 'ADX-DI': 25.60684839, 'ADX+DI[1]': 29.85479333, 'ADX-DI[1]': 26.11840839, 'AO': 8.26394676, 'AO[1]': 12.62397794, 'Mom': -15.22, 'Mom[1]': -2.67, 'MACD.macd': 7.00976885, 'MACD.signal': 10.30480624, 'Rec.Stoch.RSI': 0, 'Stoch.RSI.K': 9.72185595, 'Rec.WR': 0, 'W.R': -62.00277521, 'Rec.BBPower': 1, 'BBPower': -6.09964786, 'Rec.UO': 0, 'UO': 50.27359668, 'EMA5': 376.90090141, 'close': 373.01, 'SMA5': 376.636, 'EMA10': 378.95440164, 'SMA10': 382.691, 'EMA20': 375.62919667, 'SMA20': 379.2195, 'EMA30': 369.05104155, 'SMA30': 371.84066667, 'EMA50': 355.34346605, 'SMA50': 353.6286, 'EMA100': 330.92744806, 'SMA100': 313.3713, 'EMA200': 300.82801448, 'SMA200': 298.2719, 'Rec.Ichimoku': 0, 'Ichimoku.BLine': 375.485, 'Rec.VWMA': -1, 'VWMA': 378.72121396, 'Rec.HullMA9': 1, 'HullMA9': 370.20948148, 'Pivot.M.Classic.S3': 241.12333333, 'Pivot.M.Classic.S2': 296.29333333, 'Pivot.M.Classic.S1': 330.54666667, 'Pivot.M.Classic.Middle': 351.46333333, 'Pivot.M.Classic.R1': 385.71666667, 'Pivot.M.Classic.R2': 406.63333333, 'Pivot.M.Classic.R3': 461.80333333, 'Pivot.M.Fibonacci.S3': 296.29333333, 'Pivot.M.Fibonacci.S2': 317.36827333, 'Pivot.M.Fibonacci.S1': 330.38839333, 'Pivot.M.Fibonacci.Middle': 351.46333333, 'Pivot.M.Fibonacci.R1': 372.53827333, 'Pivot.M.Fibonacci.R2': 385.55839333, 'Pivot.M.Fibonacci.R3': 406.63333333, 'Pivot.M.Camarilla.S3': 349.62825, 'Pivot.M.Camarilla.S2': 354.6855, 'Pivot.M.Camarilla.S1': 359.74275, 'Pivot.M.Camarilla.Middle': 351.46333333, 'Pivot.M.Camarilla.R1': 369.85725, 'Pivot.M.Camarilla.R2': 374.9145, 'Pivot.M.Camarilla.R3': 379.97175, 'Pivot.M.Woodie.S3': 282.365, 'Pivot.M.Woodie.S2': 299.7875, 'Pivot.M.Woodie.S1': 337.535, 'Pivot.M.Woodie.Middle': 354.9575, 'Pivot.M.Woodie.R1': 392.705, 'Pivot.M.Woodie.R2': 410.1275, 'Pivot.M.Woodie.R3': 447.875, 'Pivot.M.Demark.S1': 341.005, 'Pivot.M.Demark.Middle': 356.6925, 'Pivot.M.Demark.R1': 396.175}
```

### Time Created, Symbol, Exchange, and Screener
Details about the analysis. Most of them are values that you set before.

#### Time Created
```python
print(analysis.time)
# Example output: 2020-07-29 11:57:28.719879
```
`time` is when the get_analysis is called. `time` is a `datetime.datetime` object. The time is your local time.

#### Symbol
```python
print(analysis.symbol)
# Example output: TSLA
```
`symbol` is the ticker symbol you set before. `symbol` is a string.

#### Exchange
```python
print(analysis.exchange)
# Example output: NASDAQ
```
`exchange` is the exchange you set before. `exchange` is a string.

#### Screener
```python
print(analysis.screener)
# Example output: america
```
`screener` is the screener you set before. `screener` is a string.