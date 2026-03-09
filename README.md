# Gurgaon Real Estate Market Analysis

## Project Overview

This project performs **Exploratory Data Analysis (EDA)** on residential property listings in **Gurgaon, India**. The objective is to discover useful insights about property prices, localities, and builders that can help **buyers, investors, and developers** make better real estate decisions.

The dataset contains information such as **price, area, BHK configuration, property type, builder details, locality, and RERA approval status**. Using Python and data analysis libraries, we analyze patterns and trends in the Gurgaon real estate market.

---

## Problem Statement

A real estate advisory firm operating in Gurgaon collected data on residential properties across various sectors. The firm wants **data-backed insights** to guide buyers, investors, and developers in making informed real estate decisions.

Using the dataset, the goal is to analyze property listings and answer key business questions related to pricing, locality comparisons, builder influence, and property characteristics.

---

## Dataset

The dataset contains residential property listings across multiple sectors in Gurgaon.

Main features include:

* Price
* Area (sqft)
* Rate per square foot
* BHK configuration
* Property type (Apartment / Floor / Plot)
* Builder or company name
* Locality
* Property status (Ready-to-move or Under Construction)
* RERA approval status

Dataset Source:
https://www.kaggle.com/datasets/nikhilmehrahr26/gurgaon-real-estate-dataset

---

## Tools Used

* Python
* Pandas
* Matplotlib
* Seaborn
* Jupyter Notebook / Google Colab

---

## Project Workflow

### 1. Import Required Libraries

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

### 2. Load the Dataset

```python
df = pd.read_csv("gurgaon_real_estate.csv")
df.head()
```

### 3. Dataset Overview

```python
df.shape
df.info()
```

### 4. Data Cleaning

Standardize column names

```python
df.columns = df.columns.str.strip().str.lower().str.replace(" ", "_")
```

Convert numeric columns

```python
df["price"] = df["price"].astype(str).str.replace(",", "").astype(int)
df["area"] = df["area"].astype(str).str.replace(",", "").astype(int)
df["rate_per_sqft"] = df["rate_per_sqft"].astype(str).str.replace(",", "").astype(int)
```

Clean categorical columns

```python
df["status"] = df["status"].str.strip().str.lower()
df["rera_approval"] = df["rera_approval"].str.strip().str.lower()
df["flat_type"] = df["flat_type"].str.strip().str.lower()
```

Remove duplicates

```python
df = df.drop_duplicates()
```

---

## Analysis / Questions


### 1. Which is the costliest flat in the dataset?

**Answer:**
The costliest property in the dataset can be identified by selecting the property with the maximum price value.

```python
df.loc[df["price"].idxmax()]
```

This query returns the full row containing details of the most expensive property, including locality, builder, area, and configuration.

---

### 2. Which locality has the highest average price?

**Answer:**
To find the locality with the highest average property price, we group the data by locality and calculate the mean price.

```python
df.groupby("locality")["price"].mean().sort_values(ascending=False)
```

The locality appearing at the top of the result has the highest average property price.

---

### 3. Which locality has the highest rate per square foot?

**Answer:**
This analysis helps identify premium areas by comparing the average price per square foot across different localities.

```python
df.groupby("locality")["rate_per_sqft"].mean().sort_values(ascending=False)
```

Localities with higher rate per square foot are considered more premium.

---

### 4. Do ready-to-move properties cost more than under-construction properties?

**Answer:**
To compare pricing between ready-to-move and under-construction properties, we calculate the median price for each category.

```python
df.groupby("status")["price"].median()
```

Median is used instead of mean because property prices often contain extreme values.

---

### 5. Do RERA-approved properties command a price premium?

**Answer:**
We compare the median price of RERA-approved properties with non-approved properties.

```python
df.groupby("rera_approval")["price"].median()
```

If the median price of RERA-approved properties is higher, it suggests that buyers are willing to pay a premium for regulatory assurance.

---

### 6. How does area (sqft) impact property price?

**Answer:**
A scatter plot helps visualize the relationship between property size and price.

```python
sns.scatterplot(x="area", y="price", data=df)
plt.title('Price vs Area')
plt.xlabel('Area (sqft)')
plt.ylabel('Price (INR)')
plt.show()
```

This visualization helps identify whether larger properties tend to cost more.

---

### 7. Which BHK configuration is the most expensive on average?

**Answer:**
We calculate the average price for each BHK configuration.

```python
df.groupby("bhk_count")["price"].mean()
```

Higher BHK configurations usually have higher prices due to larger space and amenities.

---

### 8. Which property type is the costliest?

**Answer:**
This analysis compares the average price of Apartments, Floors, and Plots.

```python
df.groupby("flat_type")["price"].mean()
```

The property type with the highest mean price is considered the costliest.

---

### 9. Do certain builders consistently price higher?

**Answer:**
To analyze builder pricing trends, we calculate the average property price for each builder.

```python
df.groupby("company_name")["price"].mean().sort_values(ascending=False)
```

Builders at the top of this list generally price their properties higher than others.

---

### 10. Are larger homes always more expensive per square foot?

**Answer:**
We examine the relationship between property area and price per square foot.

```python
sns.scatterplot(x="area", y="rate_per_sqft", data=df)
plt.title('Rate per Square Foot vs Area')
plt.xlabel('Area (sqft)')
plt.ylabel('Rate per Square Foot (INR)')
plt.show()
```

This helps determine whether larger homes offer better value per square foot or if premium pricing applies regardless of size.

---

## Key Insights

* Premium localities tend to have higher property prices and higher rate per square foot.
* Ready-to-move properties often cost more than under-construction properties.
* RERA-approved properties generally command higher trust and pricing.
* Builder reputation significantly impacts property pricing.
* Larger homes are not always more expensive per square foot.
* Apartments typically have higher price per square foot compared to plots and floors.

---

## Conclusion

The analysis of Gurgaon real estate data reveals several important patterns in the property market. Premium localities tend to command significantly higher prices and higher rates per square foot. Ready-to-move properties often have higher prices compared to under-construction projects, likely due to reduced risk for buyers.

RERA-approved properties also tend to attract higher prices, indicating that regulatory trust plays an important role in buyer decisions. Builder reputation and project location significantly influence pricing as well.

Overall, the analysis demonstrates how data analysis can help investors, buyers, and developers make more informed real estate decisions.
