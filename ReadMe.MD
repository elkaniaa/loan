
# Loan Prediction Based on Customer Behavior

### EDA            
df.info()             
RangeIndex: 252000 entries, 0 to 251999                   
Data columns (total 13 columns):            
![df.info](https://drive.google.com/file/d/1_pgvFVLAHSIOpb2d7I4w-KHtWmobay1J/view?usp=sharing)
     
 #   Column             Non-Null Count   Dtype                      
---  ------             --------------   -----                         
 0   Id                 252000 non-null  int64                          
 1   Income             252000 non-null  int64                      
 2   Age                252000 non-null  int64                   
 3   Experience         252000 non-null  int64                     
 4   Married/Single     252000 non-null  object                   
 5   House_Ownership    252000 non-null  object                  
 6   Car_Ownership      252000 non-null  object                      
 7   Profession         252000 non-null  object                     
 8   CITY               252000 non-null  object                       
 9   STATE              252000 non-null  object                        
 10  CURRENT_JOB_YRS    252000 non-null  int64                            
 11  CURRENT_HOUSE_YRS  252000 non-null  int64                                 
 12  Risk_Flag          252000 non-null  int64                             
dtypes: int64(7), object(6)                             
memory usage: 25.0+ MB                              

### Data Preprocessing
#### A. Menyamakan Style Pada Kolom
df.rename(columns={'CITY':'City','STATE':'State','CURRENT_JOB_YRS':'Current_Job_Yrs','CURRENT_HOUSE_YRS':'Current_House_Yrs'}, inplace=True)

#### B. Split Numerical & Categorical
##### List of column names containing numerical data
nums = df.select_dtypes(include='number').drop(columns=['Id', 'Risk_Flag'])

##### List of column names containing categorical/object data
cats = df.select_dtypes(include='object').columns.tolist()

#### C. Append Uttar Pradesh
df['State'] = df['State'].replace('Uttar_Pradesh[5]', 'Uttar_Pradesh')

#### D. Split Risk & Non-Risk
risk0 = df[df['Risk_Flag']==0]
risk1 = df[df['Risk_Flag']==1]


###  1. Data Cleansing
#### A. Handling Missing Values, 
df.isna().sum() ................ 0
df.isnull().sum() .............. 0

#### B. Hanglind Dubplicated Data
df.duplicated().sum() ........... 0

#### C. Handling Outliers, tidak ada outliers

#### D. Feature Transformation / menghandle outlier (z-score, log-transform)
#### E. Feature Encoding (One-Hot Encoding, categorical menjadi numerical)
#### F. Handle Class Imbalance ( SMOTE )
tidak dilakukan Feature Transformation, Feature Encoding, Handle Class Imbalance karena akan dilakukan model yang robust terhadap outlier 
dan melakukan proses scorecard yang umum dipakai dalam dunia Perbankan & Fintech


### 2. Feature Engineering
#### A. Feature Selection (membuang feature yang kurang relevan atau redundan)
dalam heatmap dengan target Risk_Flag, fitur Current_House_Yrs & Current_Job_Yrs redundan, namun karena fitur sangat sedikit dan
predictive model yang digunakan menggunakan scorecard yang memberikan valuasi berbeda dengan sns.heatmap.
Scorecard adalah alat yang digunakan dalam industri keuangan dan kredit untuk menilai risiko kredit seseorang atau entitas.

#### B. Feature Extraction (mengurangi fitur)
tidak ada. Fitur City memiliki 317 unique, namun  bisa dideksi dengan State

#### C. 4 Feature tambahan 
a. Job Duration Categorical
b. Experience Categorial
c. Income Categorical
d. Age Categorical

Categorical diambil dari Q1,Q2 & Q3 dalam menentukan range


## Disusun oleh :
1. Amarindra Ardinova
2. Annisa Millah T
