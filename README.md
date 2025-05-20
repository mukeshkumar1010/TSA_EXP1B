# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:

#### Name : Mukesh Kumar S
#### Register Number : 212223240099

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

# Load the dataset
data = pd.read_csv('silver.csv')

# Convert 'Date' to datetime and set it as the index
data['Date'] = pd.to_datetime(data['Date'])
data.set_index('Date', inplace=True)

# Drop rows with missing values in 'USD'
data.dropna(subset=['USD'], inplace=True)

# ---------- USD Analysis ----------
# Regular differencing
data['usd_diff'] = data['USD'].diff()

# Seasonal decomposition of original USD
result_usd = seasonal_decompose(data['USD'], model='additive', period=12)
data['usd_sea_diff'] = result_usd.resid

# Log transformation
data['usd_log'] = np.log(data['USD'])

# Log transformation + regular differencing
data['usd_log_diff'] = data['usd_log'].diff().dropna()

# Seasonal decomposition after log differencing
if len(data['usd_log_diff'].dropna()) >= 12:  # Check if enough data exists for decomposition
    result_usd_log = seasonal_decompose(data['usd_log_diff'].dropna(), model='additive', period=12)
    data['usd_log_seasonal_diff'] = result_usd_log.resid
else:
    data['usd_log_seasonal_diff'] = np.nan
    print("Not enough data for seasonal decomposition after log differencing for USD.")

# Plotting results
plt.figure(figsize=(16, 12))

plt.subplot(6, 1, 1)
plt.plot(data['USD'], label='Original USD')
plt.legend(loc='best')
plt.title('Original USD Data')

plt.subplot(6, 1, 2)
plt.plot(data['usd_diff'], label='USD Difference')
plt.legend(loc='best')
plt.title('USD Regular Differencing')

plt.subplot(6, 1, 3)
plt.plot(data['usd_sea_diff'], label='USD Seasonal Adjustment')
plt.legend(loc='best')
plt.title('USD Seasonal Adjustment')

plt.subplot(6, 1, 4)
plt.plot(data['usd_log'], label='Log Transformation (USD)')
plt.legend(loc='best')
plt.title('Log Transformation of USD')

plt.subplot(6, 1, 5)
plt.plot(data['usd_log_diff'], label='Log Transformation + Diff (USD)')
plt.legend(loc='best')
plt.title('Log Transformation and Differencing (USD)')

plt.subplot(6, 1, 6)
plt.plot(data['usd_log_seasonal_diff'], label='Log + Diff + Seasonal Diff (USD)')
plt.legend(loc='best')
plt.title('Log, Differencing, and Seasonal Adjustment (USD)')

```

### OUTPUT:

### Original Data:

![image](https://github.com/user-attachments/assets/8979369c-a9b4-4813-9d5e-125f5346cb4d)

### REGULAR DIFFERENCING:

![image](https://github.com/user-attachments/assets/b471d3a3-c0b6-4299-ad9f-c099a56249b7)

### SEASONAL ADJUSTMENT:

![image](https://github.com/user-attachments/assets/e2ae021b-2860-4854-a47e-1dc4ec7774a7)

### LOG TRANSFORMATION:

![image](https://github.com/user-attachments/assets/4f74b77a-4fb3-44d8-b3a5-85be7a153bd9)

### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
