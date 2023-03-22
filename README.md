# Pre-Processing-Python-Script-of-Type-1-diabetes-Anderson-2016-Dataset
pre-processing is a crucial step in preparing the Anderson 2016 CGM dataset for analysis, as it ensures data quality, selects relevant features, standardizes data formats, and optimizes storage. These improvements ultimately lead to more accurate and efficient analyses, models, and insights. 
> # Links
> 
> 1. [Link to dataset](https://public.jaeb.org/jdrfapp2/stdy/465)
> 2. [Link to orginal study](https://www.liebertpub.com/doi/10.1089/dia.2016.0333)
> 
> # Study Summary
> ## Background: 
> In the past few years, the artificial pancreas—the commonly accepted term for closed-loop control (CLC) of blood glucose in diabeteshas become a hot topic in research and technology development. In the summer of 2014,  a 6-month trial evaluating the safety of 24/7 CLC during free-living conditions. was evaluated.
> 
> ## Research Design and Methods: 
> Following an initial 1-month Phase 1, 14 individuals (10 males/4 females) with type 1 diabetes at three clinical centers in the United States and one in Italy continued with a 5-month Phase 2, which included 24/7 CLC using the wireless portable Diabetes Assistant (DiAs) developed at the University of Virginia Center for Diabetes Technology. Median subject characteristics were age 45 years, duration of diabetes 27 years, total daily insulin 0.53 U/kg/day, and baseline HbA1c 7.2% (55 mmol/mol).
> 
> ## Results:
> Compared with the baseline observation period, the frequency of hypoglycemia below 3.9 mmol/L during the last 3 months of CLC was lower: 4.1% versus 1.3%, P < 0.001. This was accompanied by a downward trend in HbA1c from 7.2% (55 mmol/mol) to 7.0% (53 mmol/mol) at 6 months. HbA1c improvement was correlated with system use (Spearman r = 0.55). The user experience was favorable with identified benefit particularly at night and overall trust in the system. There were no serious adverse events, severe hypoglycemia, or diabetic ketoacidosis.
> 
> 
> # Covariate Data

1. A1c
2. Insulin
3. Mealtimes
4. Ketones
5. Medications

# Pre Processing Python Script - Flow 
Anderson 2016 CGM (Continuous Glucose Monitoring) dataset, which is a collection of glucose measurements taken from patients. The primary goal of this pre-processing is to clean and organize the data, making it more accessible for further analysis.

The steps taken in the pre-processing of the Anderson 2016 CGM dataset are as follows:

1. Import the pandas library to handle data manipulation.

2. Read the dataset using pandas' read_csv() function, specifying the file path and the delimiter (in this case, the pipe character '|').

3. Select the relevant columns from the dataset, namely 'RecID', 'DisplayTime', and 'CGM', and store them in a new DataFrame called 'table'.

4. Rename the columns in 'table' to more straightforward names: 'id', 'Time', and 'Glucose value'.

5. Convert the 'Glucose value' column to a numeric data type using pandas' to_numeric() function to ensure that all values are properly formatted as numbers.

6. Standardize the date and time format in the 'Time' column using pandas' to_datetime() function, specifying the desired format as "%Y-%m-%d %H:%M:%S".

7. Save the cleaned dataset as a parquet file, which is more suitable for handling large datasets, using the pandas' to_parquet() function. Specify the file path, set 'index' to False, and set the 'engine' to 'pyarrow'.

8. By following these steps, we have successfully pre-processed the Anderson 2016 CGM dataset, making it ready for further analysis or machine learning tasks.

# Python Script

## Initial Data Import

 The dataset is imported using `pandas` library by reading the `CGM.txt` file with '|' as the separator.
```python
import pandas as pd

data = pd.read_csv('Enter your file path',sep='|')
`
```
### Data Cleaning and Transformation

- We select the relevant columns: 'RecID', 'DisplayTime', and 'CGM' and create a new DataFrame table.
- Rename the columns to more user-friendly names: 'id', 'Time', and 'Glucose value'.
- Convert the 'Glucose value' column to a numeric data type.
- Standardize the 'Time' column to a datetime object with a specific format.
```
table = data[['RecID','DisplayTime','CGM']]
table.columns = ['id','Time','Glucose value']
table['Glucose value'] = pd.to_numeric(table['Glucose value'])
table['Time'] = pd.to_datetime(table['Time'],format= "%Y-%m-%d %H:%M:%S")

```
```
```
Note: If you encounter a SettingWithCopyWarning, use the .loc[] indexer to avoid the warning.

### Saving Cleaned Data
Save the cleaned dataset to a folder as a parquet file. We choose parquet format due to its efficient storage for large datasets and its compatibility with various data processing tools.

```
table.to_parquet('enter the filepath\\name_of_the_file_you_want_to_save.parquet',index=False,engine='pyarrow')
