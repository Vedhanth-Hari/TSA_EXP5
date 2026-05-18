# Ex.No: 05  IMPLEMENTATION OF TIME SERIES ANALYSIS AND DECOMPOSITION
### Date: 18-05-2026


### AIM:
To Illustrates how to perform time series analysis and decomposition on the monthly average temperature of a city/country and for airline passengers.

### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the decomposition process for the required data.
4. Plot the data according to need, either seasonal_decomposition or trend plot.
5. Display the overall results.

### PROGRAM:
```

import pandas as pd
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

# Load dataset
data = pd.read_csv(
    "wb_commodity_price_intelligence_1960_2026.csv"
)

# Create date column
data['date'] = pd.to_datetime(
    data['year'].astype(str) + '-' +
    data['month'].astype(str) + '-01'
)

# Select one commodity
commodity = "Aluminum"
data = data[data['commodity_name'] == commodity]

# Set date as index
data.set_index('date', inplace=True)

# Sort values
data.sort_index(inplace=True)

# Fill missing values
data['price_nominal_usd'] = (
    data['price_nominal_usd'].ffill()
)

# Display first five rows
print("FIRST FIVE ROWS:")
print(data[['commodity_name',
            'price_nominal_usd']].head())

# Plotting the data
print("\nPLOTTING THE DATA:")

plt.figure(figsize=(12,5))

plt.plot(
    data.index,
    data['price_nominal_usd'],
    color='blue'
)

plt.title(f'{commodity} Price Data')
plt.xlabel('Date')
plt.ylabel('Price')
plt.grid(True)

plt.show()

# Seasonal decomposition
decomposition = seasonal_decompose(
    data['price_nominal_usd'],
    model='additive',
    period=12
)

# Seasonal plot
print("\nSEASONAL PLOT REPRESENTATION:")

plt.figure(figsize=(12,4))

plt.plot(
    decomposition.seasonal,
    color='green'
)

plt.title('Seasonal Component')
plt.grid(True)

plt.show()

# Trend plot
print("\nTREND PLOT REPRESENTATION:")

plt.figure(figsize=(12,4))

plt.plot(
    decomposition.trend,
    color='orange'
)

plt.title('Trend Component')
plt.grid(True)

plt.show()

# Overall representation
print("\nOVERAL REPRESENTATION:")

decomposition.plot()
plt.tight_layout()
plt.show()
```

### OUTPUT:
#### FIRST FIVE ROWS:
<img width="469" height="181" alt="image" src="https://github.com/user-attachments/assets/7d4f691c-fae0-4885-beed-2696c0134333" />



#### PLOTTING THE DATA:
<img width="783" height="384" alt="image" src="https://github.com/user-attachments/assets/caa5946f-ce88-49d2-9f34-2f3f513030ca" />

#### SEASONAL PLOT REPRESENTATION :
<img width="792" height="326" alt="image" src="https://github.com/user-attachments/assets/22b7d8f9-1579-4807-9036-467e9a5c7648" />



#### TREND PLOT REPRESENTATION :
<img width="783" height="319" alt="image" src="https://github.com/user-attachments/assets/34402c0a-7c23-462c-808a-610ccb2d40c8" />

#### OVERAL REPRESENTATION:

<img width="713" height="552" alt="image" src="https://github.com/user-attachments/assets/504d7ea3-3e00-4876-a4a2-89f2108897c8" />


### RESULT:
Thus we have created the python code for the time series analysis and decomposition.
