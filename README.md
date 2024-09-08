# Visualize-Stocks-Data-Using-CandleStick
This project visualizes stock price data using candlestick charts in Python with mplfinance and matplotlib. It provides a clear way to analyze Open, High, Low, and Close (OHLC) prices, offering insights into market trends and price movements. The repo also demonstrates data preprocessing for accurate and effective stock visualization

## Install Packages 
```python
!pip install mpl-finance
!pip install yfinance
```

## Import packages
```python
import yfinance as yf
import datetime as dt
import matplotlib.pyplot as plt
import matplotlib.dates as mdates
from mpl_finance import candlestick_ohlc  #open high low close
```

## Set Timeframe
```python
start = dt.datetime(2023,7,1)
end = dt.datetime.now()  #sets end date to today's date
```

## Load Data
```python
ticker = 'META'
data = yf.download(ticker, start=start, end=end)
data
```
<img width="627" alt="Screenshot 2024-09-07 at 20 20 12" src="https://github.com/user-attachments/assets/d91074a9-bce3-43de-8a38-3d53bd8d5654">


## For our CandleStick, We need only four Variables 
- Open, High, Low, Close

### Restructure DataFrame
```python
data = data[['Open', 'High', 'Low', 'Close']]
data
```
<img width="495" alt="Screenshot 2024-09-07 at 20 22 21" src="https://github.com/user-attachments/assets/3ce10a62-ef17-44c6-9cd2-acc785a6ae86">


## Reset_index to make use of the Date Variable/column
```python
data.reset_index(inplace=True)
data
```
<img width="514" alt="Screenshot 2024-09-07 at 20 23 02" src="https://github.com/user-attachments/assets/29aede5d-b102-4a47-ae2e-9abbb3007e32">

## Convert date to Float Points for matplotlib use
```python
data['Date'] = data['Date'].map(mdates.date2num)
data
```
<img width="497" alt="Screenshot 2024-09-07 at 20 23 50" src="https://github.com/user-attachments/assets/537c16b7-4471-489b-b470-64c818f54015">

## Plot Stock Values
```python
plt.figure(figsize=(15, 8))  # Set figure size

ax = plt.subplot()  # Initialize subplot

ax.grid(True)
ax.set_axisbelow(True)
ax.set_facecolor('black')
ax.figure.set_facecolor('#121212')
ax.tick_params(axis='x', colors='white')
ax.tick_params(axis='y', colors='white')
ax.set_title('{} Share Price'.format(ticker), color='white')
ax.xaxis_date()  # The x-axis will display dates

candlestick_ohlc(ax, data.values, width=0.5, colorup='#00ff00')

plt.show()  # Display the plot
```
<img width="1235" alt="Screenshot 2024-09-07 at 20 24 41" src="https://github.com/user-attachments/assets/cccd95ef-6501-4233-bfe0-b674fa79aa80">




















