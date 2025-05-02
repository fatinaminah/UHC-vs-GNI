
# Visualizing Scatterplot on Kaggle: Universal Health Coverage vs. Gross National Income

Scatter plots serve as robust data visualization tools for establishing the correlation of two variables and their relationship context. This article tries to view Universal Health Coverage (UHC) and Gross National Income (GNI) on Kaggle in a data visualization perspective.

**Understanding the Relationship Between UHC and GNI**

> UHC is the condition in which all people can access basic health services without suffering financial hardship. UHC is a pertinent factor in the Sustainable Development Goals (SDGs) and is specifically mentioned in SDG 3.8. On the other hand, GNI is the gross income of a country in terms of its economic strength. Through this relationship, we approach disparities in healthcare systems and economic development on a worldwide scale.

For the new folks on Kaggle, we will walk through the step-by-step visualization of this data.

# **Step-by-Step Guide**

**1. Access Kaggle Notebooks**

-   Visit the Kaggle website:  [https://www.kaggle.com/](https://www.kaggle.com/)
-   Click the  **+**  button on the upper left and select  **New Notebook**.
-   Kaggle automatically sets up a Python 3 environment. If R is preferred, navigate to the  **File**  tab and select  **Language: R**.

![](https://miro.medium.com/v2/resize:fit:258/1*U4fZXvwKeagKohb15ckdAw.png)

*To create new notebook on Kaggle*

![](https://miro.medium.com/v2/resize:fit:700/1*yK6BBlotjFtpH3wwO-7YDQ.png)

*Message displayed upon creating a new notebook*

**2. Load the Data**

Kaggle offers multiple ways to import data, including searching within Kaggle’s datasets, using URLs, or uploading custom files. In this example, I’ve uploaded an Excel dataset to my Kaggle account and used it to conduct this analysis.

    import kagglehub  
    path = kagglehub.dataset_download("fathinaminah/uhc-data")  
    print("Path to dataset files:", path)

**3. Locate and rename the data file**

After downloading the data from the specified path, I ran the following code to list the dataset files and rename the Excel file.

    import os  
    import pandas as pd  

  
> List dataset files

    files = os.listdir(path)  
    print("Files in dataset:", files)  

  
>  Load and rename the dataset
 

    excel_file_path = os.path.join(path, 'UHCvs GNI 2021.xls')  
    mydata = pd.read_excel(excel_file_path)

**4. Check data integrity**

I then verified that the dataset contains all the required columns and the correct number of countries.

> Display the first 20 rows

    print(mydata.head(20))  

  
> Count unique countries

    print("Number of unique countries:", mydata['Country'].nunique())

![](https://miro.medium.com/v2/resize:fit:372/1*KDgWWUaSvF5D7ML3TJ_wuA.png)
                       
*Dataset verification results*

**5. Apply log transformation to GNI**

Since GNI values vary significantly across countries, a logarithmic transformation is applied for better visualization.

    import numpy as np  
    mydata['log_GNI'] = np.log(mydata['GNI'])  
    print(mydata['log_GNI'])

**6. Create a scatter plot**

Using Matplotlib, I wrote the following code to visualize the relationship between UHC-SCI and the log-transformed GNI.

    import matplotlib.pyplot as plt  
      
    plt.figure(figsize=(20, 10))  
    plt.scatter(mydata['log_GNI'], mydata['UHC-SCI'], alpha=1, color = 'maroon')  

  
> Annotate the Scatter Plot with Country Labels
 

    for i, row in mydata.iterrows():  
        plt.text(row['log_GNI'] + 0.05, row['UHC-SCI'] + 0.05, row['Country'], fontsize=11, alpha=1)  
    
    plt.title('Universal Health Coverage vs. Gross National Income in 2021', fontsize=18)  
    plt.xlabel('GNI (current US$)', fontsize=14)  
    plt.ylabel('UHC service coverage index', fontsize=14)  
    plt.grid(color = 'green', linestyle = '--', linewidth = 0.5)  
    plt.show()

# Insights from the Visualization

![](https://miro.medium.com/v2/resize:fit:700/1*2F6WHRCb11axrUAyTX3O4w.png)

*Source: Plot developed by the author using data from the World Bank ([https://data.worldbank.org/](https://data.worldbank.org/)).*

Each dot represents a single country (i=185 countries), with the horizontal x-axis showing GNI and the vertical y-axis showing the UHC-SCI score. The plot indicates that countries with higher GNI, such as the United States, China, Canada, the United Kingdom, and Japan, tend to have higher UHC-SCI scores compared to lower-income countries. In general, as GNI increases, so does the UHC service score.

