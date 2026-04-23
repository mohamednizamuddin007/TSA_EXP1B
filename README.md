
# Ex.No: 1B CONVERSION OF NON STATIONARY TO STATIONARY DATA

# Date: 23-04-2026

### AIM:

To perform regular differencing, seasonal adjustment and log transformation on daily humidity data using the Daily Delhi Climate dataset.

### TOOLS USED:

Google Colab

### ALGORITHM:

1. Import the required packages like pandas, numpy and matplotlib.
2. Read the dataset using pandas.
3. Convert the date column into datetime format and set it as index.
4. Apply regular differencing, seasonal adjustment and log transformation on humidity data.
5. Plot the original and transformed data.
6. Display the overall results.

### PROGRAM:
```

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

data = pd.read_excel("DailyDelhiClimateTrain.xls")

data['date'] = pd.to_datetime(data['date'])

data.set_index('date', inplace=True)

target_col = 'humidity'

data['diff'] = data[target_col] - data[target_col].shift(1)

result = seasonal_decompose(data[target_col], model='additive', period=30)
data['sea_resid'] = result.resid

data['log_val'] = np.log(data[target_col])

data['log_diff'] = data['log_val'] - data['log_val'].shift(1)

plt.figure(figsize=(16,16))

plt.subplot(4,1,1)
plt.plot(data[target_col], label='Original')
plt.title('Original Humidity Data')
plt.legend()

plt.subplot(4,1,2)
plt.plot(data['diff'], label='Differencing')
plt.title('Regular Differencing')
plt.legend()

plt.subplot(4,1,3)
plt.plot(data['sea_resid'], label='Seasonal Residual')
plt.title('Seasonal Adjustment')
plt.legend()

plt.subplot(4,1,4)
plt.plot(data['log_diff'], label='Log Diff')
plt.title('Log Transformation and Differencing')
plt.legend()

plt.tight_layout()
plt.show()
```

### OUTPUT:

<img width="1589" height="1590" alt="image" src="https://github.com/user-attachments/assets/dc4492b0-0ddb-476a-a318-752ceae6215f" />


### RESULT:

Thus we have created the Python code for the conversion of non stationary to stationary data on daily humidity data using the Daily Delhi Climate dataset.
