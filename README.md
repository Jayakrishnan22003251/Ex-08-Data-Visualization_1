# Ex-08-Data-Visualization-

## AIM
To Perform Data Visualization on a complex dataset and save the data to a file. 

# Explanation
Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, data visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data.

# ALGORITHM
### STEP 1
Read the given Data
### STEP 2
Clean the Data Set using Data Cleaning Process
### STEP 3
Apply Feature generation and selection techniques to all the features of the data set
### STEP 4
Apply data visualization techniques to identify the patterns of the data.


# CODE
### Loading the dataset :
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
df=pd.read_csv("/content/Superstore (3).csv",encoding='unicode_escape')
df
```

### Removing unnecessary data variables :
```
df.drop('Row ID',axis=1,inplace=True)
df.drop('Order ID',axis=1,inplace=True)
df.drop('Customer ID',axis=1,inplace=True)
df.drop('Customer Name',axis=1,inplace=True)
df.drop('Country',axis=1,inplace=True)
df.drop('Postal Code',axis=1,inplace=True)
df.drop('Product ID',axis=1,inplace=True)
df.drop('Product Name',axis=1,inplace=True)
df.drop('Order Date',axis=1,inplace=True)
df.drop('Ship Date',axis=1,inplace=True)
print("Updated dataset")
df

df.isnull().sum()
```
### Detecting and removing outliers in current numeric data :
```
plt.figure(figsize=(12,10))
plt.title("Data with outliers")
df.boxplot()
plt.show()

plt.figure(figsize=(12,10))
cols = ['Sales','Quantity','Discount','Profit']
Q1 = df[cols].quantile(0.25)
Q3 = df[cols].quantile(0.75)
IQR = Q3 - Q1
df = df[~((df[cols] < (Q1 - 1.5 * IQR)) |(df[cols] > (Q3 + 1.5 * IQR))).any(axis=1)]
plt.title("Dataset after removing outliers")
df.boxplot()
plt.show()
```

## data visualization :
### line plots :
```
import seaborn as sns
sns.lineplot(x="Sub-Category",y="Sales",data=df,marker='o')
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.lineplot(x="Category",y="Profit",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Categories vs Profit")
plt.show()

sns.lineplot(x="Region",y="Sales",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Region area vs Sales")
plt.show()

sns.lineplot(x="Category",y="Discount",data=df,marker='o')
plt.title("Categories vs Discount")
plt.show()

sns.lineplot(x="Sub-Category",y="Quantity",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Sub Categories vs Quantity")
plt.show()
#bar plots
sns.barplot(x="Sub-Category",y="Sales",data=df)
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Profit",data=df)
plt.title("Categories vs Profit")
plt.show()

sns.barplot(x="Sub-Category",y="Quantity",data=df)
plt.title("Sub Categories vs Quantity")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Discount",data=df)
plt.title("Categories vs Discount")
plt.show()

plt.figure(figsize=(12,7))
sns.barplot(x="State",y="Sales",data=df)
plt.title("States vs Sales")
plt.xticks(rotation = 90)
plt.show()

plt.figure(figsize=(25,8))
sns.barplot(x="State",y="Sales",hue="Region",data=df)
plt.title("State vs Sales based on Region")
plt.xticks(rotation = 90)
plt.show()
```

### HISTOGRAM :
```
sns.histplot(data = df,x = 'Region',hue='Ship Mode')
sns.histplot(data = df,x = 'Category',hue='Quantity')
sns.histplot(data = df,x = 'Sub-Category',hue='Category')
plt.xticks(rotation = 90)
plt.show()
sns.histplot(data = df,x = 'Quantity',hue='Segment')
plt.hist(data = df,x = 'Profit')
plt.show()
```
### count plot :
```
plt.figure(figsize=(10,7))
sns.countplot(x ='Segment', data = df,hue = 'Sub-Category')
sns.countplot(x ='Region', data = df,hue = 'Segment')
sns.countplot(x ='Category', data = df,hue='Discount')
sns.countplot(x ='Ship Mode', data = df,hue = 'Quantity')
```
### Barplot :
```
sns.boxplot(x="Sub-Category",y="Discount",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot( x="Profit", y="Category",data=df)
plt.xticks(rotation = 90)
plt.show()
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Profit",data=df)
sns.boxplot(x="Region",y="Sales",data=df)
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Quantity",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Discount",data=df)
plt.figure(figsize=(15,7))
sns.boxplot(x="State",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
```
### KDE plot :
```
sns.kdeplot(x="Profit", data = df,hue='Category')
sns.kdeplot(x="Sales", data = df,hue='Region')
sns.kdeplot(x="Quantity", data = df,hue='Segment')
sns.kdeplot(x="Discount", data = df,hue='Segment')
```
### violin plot
```
sns.violinplot(x="Profit",data=df)
sns.violinplot(x="Discount",y="Ship Mode",data=df)
sns.violinplot(x="Quantity",y="Ship Mode",data=df)
```
### Point plot :
```
sns.pointplot(x=df["Quantity"],y=df["Discount"])
sns.pointplot(x=df["Quantity"],y=df["Category"])
sns.pointplot(x=df["Sales"],y=df["Sub-Category"])
```
### Pie Chart :
```
df.groupby(['Category']).sum().plot(kind='pie', y='Discount',figsize=(6,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Sub-Category']).sum().plot(kind='pie', y='Sales',figsize=(10,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Region']).sum().plot(kind='pie', y='Profit',figsize=(6,9),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Ship Mode']).sum().plot(kind='pie', y='Quantity',figsize=(8,11),pctdistance=1.7,labeldistance=1.2)

df1=df.groupby(by=["Category"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)  
plt.figure(figsize=(8,8))
colors = sns.color_palette('pastel')
plt.pie(df1["Profit"],colors = colors,labels=labels, autopct = '%0.0f%%')
plt.show()

df1=df.groupby(by=["Ship Mode"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)
colors=sns.color_palette("bright")
plt.pie(df1["Sales"],labels=labels,autopct="%0.0f%%")
plt.show()
#HeatMap
df4=df.copy() 
```
### encoding :
```
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder,OneHotEncoder
le=LabelEncoder()
ohe=OneHotEncoder
oe=OrdinalEncoder()

df4["Ship Mode"]=oe.fit_transform(df[["Ship Mode"]])
df4["Segment"]=oe.fit_transform(df[["Segment"]])
df4["City"]=le.fit_transform(df[["City"]])
df4["State"]=le.fit_transform(df[["State"]])
df4['Region'] = oe.fit_transform(df[['Region']])
df4["Category"]=oe.fit_transform(df[["Category"]])
df4["Sub-Category"]=le.fit_transform(df[["Sub-Category"]])
Scaling :
from sklearn.preprocessing import RobustScaler
sc=RobustScaler()
df5=pd.DataFrame(sc.fit_transform(df4),columns=['Ship Mode', 'Segment', 'City', 'State','Region',
                                               'Category','Sub-Category','Sales','Quantity','Discount','Profit'])
```
### Heatmap :
```
plt.subplots(figsize=(12,7))
sns.heatmap(df5.corr(),cmap="PuBu",annot=True)
plt.show()
```
# OUPUT
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/73d2a30b-0da0-46a0-bfa7-2ee1270e8779)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/b5f9d5f9-e479-490b-a8e8-959e7a17181d)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/86977f25-6295-4cc4-a14a-5dbacfc4c39d)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/ee492467-620c-4823-a420-71ccccf312dc)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/4ef49e56-dd2d-4bd0-bdc0-374daa226544)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/ed879da4-ca8a-431e-a5ef-c42fec8653cf)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/75e3a2b7-b7e3-49aa-a079-d21663a8a0cd)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/e0477a17-c485-472c-91a4-34e14082597a)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/3c95b1e5-581d-45d9-b840-bb11d4b9b796)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/5be4ed55-409a-4353-a63f-886907bd36a1)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/0db849a1-af60-4d12-b5ba-e33788bbb1b2)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/e7d148ea-7e3c-4035-8d19-b0573e3e3fef)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/d0664a58-9bea-4833-9a2d-549d1e84fe9c)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/5a7441c8-99c5-49d7-b322-aaf552744d4e)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/096ce11d-d742-460c-8517-cc692c373a8d)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/a1100267-9fb2-4697-851c-b477599bcebb)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/cb8add47-3d7b-4e90-b247-eec9db70a97b)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/48c8c10a-4c0b-41cf-882e-7cf27fa72e14)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/4d8eff99-12d9-4f16-ae03-194e95cabd25)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/08bd8e40-656e-4a6e-9540-fecfe1b65e30)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/56670061-5146-4b7f-a2d8-107cce435287)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/8e6cbf0c-e1d5-43b2-8ca9-502ea582ea2b)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/54e032b0-21a7-4178-9daa-752e8cddc489)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/1970d21e-a6b5-4f7e-a3f8-71d2aaa1de55)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/e8f83404-00b7-4a08-b8e3-67ed4f89d671)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/5c266b05-843a-426e-8f54-f90bfab266d7)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/4ce80a01-5578-4853-a47a-415c60122c06)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/c01fd834-47a9-44f2-b023-cbd87a9f9ee3)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/84e37cad-b76d-4964-baee-4f35bfb00e6a)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/2575a71a-c457-4fc5-90c1-c17c63801d4c)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/dc75774a-f218-4c8f-a3e1-2cffb0669012)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/5bd6f644-3875-4152-be1b-ad3be5ce32da)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/3192ca5e-5282-41f4-9380-d1d7f10f9650)
![image](https://github.com/Jayakrishnan22003251/Ex-08-Data-Visualization_1/assets/120232371/4505eb66-29d0-457f-8526-4dbe70926920)

# RESULT:

Hence,Data Visualization is applied on the complex dataset using libraries like Seaborn and Matplotlib successfully and the data is saved to file.







