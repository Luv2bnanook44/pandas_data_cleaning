
# Data Cleaning Exercise

Today we will look at Chicago Public School data from the [Chicago Data Portal](https://data.cityofchicago.org/). 

We will use it to practice:
   - Importing Data into a dataframe
   - Subsetting
   - Dropping and filling na's
   - Creating new features


```python
sy_201819 = pd.read_csv('data/sy201819_school_profile.csv', index_col="Unnamed: 0")
```

We will only be using the columns which appear in the mask below.
            

Use the mask to isolate the columns of interest.  


```python
sy_201819 = sy_201819[column_mask]
```

We will only be working with high schools. 

Subset the dataframe to include only schools whose `primary_category` indicated high school.


```python
sy_201819_hs = sy_201819[sy_201819['primary_category'] == 'HS']
```

# NA's 


```python
sy_201819_hs.isna().sum()
```




    school_id                          0
    primary_category                   0
    grades_offered_all                 0
    student_count_total                0
    student_count_low_income           0
    student_count_special_ed           0
    student_count_english_learners     0
    graduation_rate_school            36
    dress_code                         2
    classroom_languages               41
    network                            5
    graduation_rate_mean              36
    dtype: int64



There are several ways to deal with na's. We will explore:
  
  - Dropping any row which has an na in it
  - Interporlating the mean value into the na
  
Only use `inplace=True` in the second instance so we can explore both methods successively.


## Dropping any row which has an `NaN` in it



```python
sy_201819_hs.dropna()

print(sy_201819_hs.shape[0] - sy_201819_hs.dropna().shape[0])
```

    55


## Interpolating the mean value to fillna

Let's work with the graduation_rate_school column.  

Take the value in the `graduation_rate_mean` and fill na's in `graduation_rate_school` with it.



```python
sy_201819_hs['graduation_rate_school'].fillna(sy_201819_hs['graduation_rate_mean'].min(), inplace=True)
```

    /Users/johnmaxbarry/anaconda3/lib/python3.7/site-packages/pandas/core/series.py:4523: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      downcast=downcast,


We will return to the classroom_languages na's in a moment.

# Creating New Features

Create a column called `percent_low_income` which is the number of low income students divided by total student count.


```python
sy_201819_hs['percent_low_income'] = sy_201819_hs['student_count_low_income']/sy_201819_hs['student_count_total']
```

    /Users/johnmaxbarry/.local/lib/python3.7/site-packages/ipykernel_launcher.py:2: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      


Create a column which counts the number of classroom languages offered in a school.


Next, use apply and a lambda function to split each cell's strings on the comma.


```python
sy_201819_hs['classroom_languages_count'] = sy_201819_hs['classroom_languages'].apply(lambda x: x.split(','))
```

    /Users/johnmaxbarry/.local/lib/python3.7/site-packages/ipykernel_launcher.py:2: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      


Now, use a second apply on classroom_languages_count and pass the built in operator `len`


```python
sy_201819_hs['classroom_languages_count'] = sy_201819_hs['classroom_languages_count'].apply(len)
```

    /Users/johnmaxbarry/.local/lib/python3.7/site-packages/ipykernel_launcher.py:2: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      


Convert dress_code from a boolean to a binary using `.map`.

Hint: `.map` takes a dictionary with keys representing the extant data and values representing what you want to replace them with.



```python
sy_201819_hs['dress_code'].map({True: 1, False: 0, np.nan: 0} )
```




    3      0
    11     1
    17     0
    21     1
    33     0
          ..
    635    1
    636    1
    637    1
    639    0
    653    1
    Name: dress_code, Length: 176, dtype: int64



As a bonus challenge, create a  column `students_per_grade` which divides the total number of students by the number of grades offered


```python
sy_201819_hs['students_per_grade'] = sy_201819_hs['grades_offered_all'].apply(lambda x: x.split(','))
sy_201819_hs['students_per_grade'] = sy_201819['student_count_total']/sy_201819_hs['students_per_grade'].apply(len)

```

    /Users/johnmaxbarry/.local/lib/python3.7/site-packages/ipykernel_launcher.py:2: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      
    /Users/johnmaxbarry/.local/lib/python3.7/site-packages/ipykernel_launcher.py:3: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      This is separate from the ipykernel package so we can avoid doing imports until

