# Stock/Crypto Dashboard
# Downloads historical data for 5 stocks and cryptocurrencies (2023-2026)
# Calculates daily returns
# Plots closing prices
# Saves CSVs, charts, and summary table
# Tools: Python, Pandas, Matplotlib, Plotly, yfinance

# Step 1: Import libraries
import yfinance as yf
import pandas as pd
import matplotlib.pyplot as plt

# Step 2: List of stocks / crypto
assets = ["AAPL", "TSLA", "MSFT", "BTC-USD", "ETH-USD"]

# Step 3: Download data for each asset
all_data = {}
for asset in assets:
    print(f"Downloading {asset} data...")
    all_data[asset] = yf.download(asset, start="2023-01-01", end="2026-01-01")
    all_data[asset].reset_index(inplace=True)  # Makes Date a column

# Step 4: Print first 5 rows of each asset to check
for asset in all_data:
    print(f"\n{asset} data preview:")
    print(all_data[asset].head())
# Step 5: Plot closing price for first stock
first_asset = assets[0]  # AAPL
plt.plot(all_data[first_asset]['Date'], all_data[first_asset]['Close'])
plt.title(f"{first_asset} Closing Price Over Time")
plt.xlabel("Date")
plt.ylabel("Close Price")
plt.show()
# Step 6: Calculate daily % change (return)
all_data[first_asset]['Daily_Return'] = all_data[first_asset]['Close'].pct_change() * 100
print(f"\n{first_asset} daily returns preview:")
print(all_data[first_asset][['Date','Daily_Return']].head())
# Save each asset's data to CSV so we can share or upload
for asset in assets:
    filename = f"{asset}_data.csv"
    all_data[asset].to_csv(filename, index=False)
    print(f"{filename} saved!")
# Save the plot of the first asset
plt.figure(figsize=(10,6))  # optional, makes image bigger
plt.plot(all_data[first_asset]['Date'], all_data[first_asset]['Close'])
plt.title(f"{first_asset} Closing Price Over Time")
plt.xlabel("Date")
plt.ylabel("Close Price")
plt.savefig(f"{first_asset}_chart.png")
plt.show()  # shows the chart as before
# Summary: average daily return and max daily return for each asset
summary = pd.DataFrame(columns=['Asset','Average Daily Return','Max Daily Return'])
for asset in assets:
    avg_return = all_data[asset]['Daily_Return'].mean()
    max_return = all_data[asset]['Daily_Return'].max()
    summary = summary.append({'Asset': asset,
                              'Average Daily Return': round(avg_return,2),
                              'Max Daily Return': round(max_return,2)}, ignore_index=True)

print("\nSummary of all assets:")
print(summary)
summary.to_csv("summary.csv", index=False)
