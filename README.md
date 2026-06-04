# PYTHON_PANDAS_JUPYTERNOTEBOOK_CafeSalesDataCleaningAndAnalysis

1. Initial Data Inspection

The analysis of missing values revealed that all columns require data cleaning and preprocessing. The highest proportion of missing data occurs in the Location and Payment Method columns. Before deciding how to handle these missing values, it is important to evaluate their potential impact on the results, as removing approximately 30% of the observations could significantly reduce the dataset and affect the reliability of the analysis.

2. Cleaning gaps and errors and recreate columns if possible

Several columns contain missing or undefined values represented as NaN, ERROR, or UNKNOWN. To ensure consistency, I standardized all missing categorical values as "Unknown".
In this case we can replace numeric gaps using Nan. It is not recommended to replace a missing values using 0 because in bussiness context 0 has a meaning 
For products with a consistent unit price, missing values in the Price Per Unit column can be reconstructed.Missing prices for records where Item is marked as Unknown could not be reliably reconstructed, as the same unit prices are associated with multiple product categories. Therefore, there is insufficient information to determine the correct price for these observations. I used a dictionary-based mapping approach to efficiently fill missing values. I have noticed that there are unknows which have prices. Some items have the same price so i didnt take them under consideration. But I connected the unique values to the unknown item category



*** Using the relationship between the Item and Price Per Unit columns, missing Item values were reconstructed whenever the unit price uniquely identified a product. This approach reduced the number of missing records in the Item column from 963 to 480, recovering 483 observations (approximately 50.2% of the original missing values).***


After the reconstruction process, only records with missing Item values associated with unit prices of 3.0 and 4.0 remained. Since a unit price of 3.0 corresponds to both Juice and Cake, these observations were assigned to the combined category "Juice/Cake". Similarly, records with a unit price of 4.0, which corresponds to both Sandwich and Smoothie, were assigned to the combined category "Sandwich/Smoothie". This approach allowed the retention of potentially valuable information.

**After this transformation, only 6 missing values remained in the Item column.**


Missing values in the Total Spent column were reconstructed by multiplying Price Per Unit by Quantity. Before performing the calculation, both columns were converted to numeric data types to enable calculations. Additionally, I identified an opportunity to recover missing values in the Quantity and Price Per Unit columns by dividing Total Spent by the corresponding available numeric value.
Checking if we have duplicates in transaction_id- in this case i don't have a duplicated transaction id


