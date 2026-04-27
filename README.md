#EX.NO:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output

import pandas as pd
import numpy as np

df=pd.read_csv("Loan_data.csv")

df.info()
<img width="608" height="404" alt="image" src="https://github.com/user-attachments/assets/6256727e-4481-44b2-adc9-d1a25ef2dbe4" />


df.describe()
<img width="907" height="379" alt="image" src="https://github.com/user-attachments/assets/e1f9797d-e7ce-4f1c-897e-d448bd8bda5d" />


df.head(10)
<img width="981" height="568" alt="image" src="https://github.com/user-attachments/assets/db9cb6da-57fe-42a2-81a6-8f7292b94615" />


df.tail(5)
<img width="977" height="279" alt="image" src="https://github.com/user-attachments/assets/87ce1dae-ed3e-4bd1-a7ff-dde37f2ee562" />


df.shape
(367, 12)


df.dropna(inplace=True)

df.isnull().sum()
<img width="319" height="521" alt="image" src="https://github.com/user-attachments/assets/780d8c03-8c32-4dfe-8155-c3fbb6001cab" />

df.to_csv("clean_data.csv", index=False)



numeric_df = df.select_dtypes(include=np.number)

Q1 = numeric_df.quantile(0.25)
Q3 = numeric_df.quantile(0.75)

IQR = Q3 - Q1

low = Q1 - 1.5 * IQR
high = Q3 + 1.5 * IQR

outlier_mask_numeric_cols = ((numeric_df < low) | (numeric_df > high)).any(axis=1)

df_iqr = df[~outlier_mask_numeric_cols]



numeric_df_for_zscore = df.select_dtypes(include=np.number)
z = np.abs(stats.zscore(numeric_df_for_zscore))

z_df = pd.DataFrame(z, columns=numeric_df_for_zscore.columns)
print(z_df)
<img width="913" height="558" alt="image" src="https://github.com/user-attachments/assets/fafd64fa-4452-41db-b6a5-71f3fe0ca586" />


df_clean = df[(z < 3).all(axis=1)]
print(df_clean)
<img width="753" height="822" alt="image" src="https://github.com/user-attachments/assets/47bb4c10-d9a2-4cd2-86de-6d421a5c8a61" />




# Result
Thus, the data cleaning process was performed successfully and the cleaned dataset was generated.
