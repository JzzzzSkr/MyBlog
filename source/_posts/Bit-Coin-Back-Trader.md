---
layout: post
title: Bit Coin Back Trader
date: 2025-12-04 23:39:00
tags: [JupyterNotebook, Pandas]
---

Recently, Bitcoin has dropped from its peak of **$126,200**. This year, numerous countries have begun investing in Bitcoin, sparking widespread debate about its future trajectory: some predict it could plummet to zero, while others anticipate it surging to **$100,000 by 2030**.

To deepen my understanding of Bitcoin’s current market situation and identify viable strategies for profiting in this bear market, I have conducted an analysis and comparison of several trading strategies based on Bitcoin’s historical price data.

<!-- more -->

## Third-party libraries

- **matplotlib**, **plotly.graph_objects** → draw the graph
- **yfinance** → source of the data
- **numpy**, **pandas** → analyze the data

## Pulling data from yfinance 

```python
ticker = "BTC-AUD"           # ← You can change it to anything you need such as NVDA, AAPL
start_date = "2018-12-27"    # ← From
end_date = "2025-12-03"      # ← To

df = yf.download(ticker, start=start_date, end=end_date)

df # check it if you want
```

**We will change column index to a normal format:**

```python
import pandas as pd

if isinstance(df.columns, pd.MultiIndex):
    df.columns = ['_'.join(col).strip() for col in df.columns.values]

df.columns = [col.replace(f"_{ticker}", "") for col in df.columns]

print(df.columns)
```

**The output should be**

```python
['Close', 'High', 'Low', 'Open', 'Volume']
```
