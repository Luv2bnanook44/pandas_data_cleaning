
# Data Cleaning Exercise

Today we will look at Chicago Public School data from the [Chicago Data Portal](https://data.cityofchicago.org/). 

We will use it to practice:
   - Importing Data into a dataframe
   - Subsetting
   - Dropping and filling na's
   - Creating new features


```python
import pandas as pd
import numpy as np

import sys
from src.student_caller import one_random_student
from src.student_list import student_first_names

pd.set_option('display.max_columns', None)

```


```python
# import the csv 'sy201819_school_profile' from the data folder. 
# Set the index to the column 'Unnamed: 0'

sy_201819 = None
```


```python
one_random_student(student_first_names)
```

    Svitlana



```python
# print out the head of the dataframe
sy_201819.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school_id</th>
      <th>legacy_unit_id</th>
      <th>finance_id</th>
      <th>short_name</th>
      <th>long_name</th>
      <th>primary_category</th>
      <th>is_high_school</th>
      <th>is_middle_school</th>
      <th>is_elementary_school</th>
      <th>is_pre_school</th>
      <th>summary</th>
      <th>administrator_title</th>
      <th>administrator</th>
      <th>secondary_contact_title</th>
      <th>secondary_contact</th>
      <th>address</th>
      <th>city</th>
      <th>state</th>
      <th>zip</th>
      <th>phone</th>
      <th>fax</th>
      <th>cps_school_profile</th>
      <th>website</th>
      <th>facebook</th>
      <th>attendance_boundaries</th>
      <th>grades_offered_all</th>
      <th>grades_offered</th>
      <th>student_count_total</th>
      <th>student_count_low_income</th>
      <th>student_count_special_ed</th>
      <th>student_count_english_learners</th>
      <th>student_count_black</th>
      <th>student_count_hispanic</th>
      <th>student_count_white</th>
      <th>student_count_asian</th>
      <th>student_count_native_american</th>
      <th>student_count_other_ethnicity</th>
      <th>student_count_asian_pacific</th>
      <th>student_count_multi</th>
      <th>student_count_hawaiian_pacific</th>
      <th>student_count_ethnicity_not</th>
      <th>statistics_description</th>
      <th>demographic_description</th>
      <th>dress_code</th>
      <th>prek_school_day</th>
      <th>kindergarten_school_day</th>
      <th>school_hours</th>
      <th>after_school_hours</th>
      <th>earliest_drop_off_time</th>
      <th>classroom_languages</th>
      <th>bilingual_services</th>
      <th>title_1_eligible</th>
      <th>preschool_inclusive</th>
      <th>preschool_instructional</th>
      <th>transportation_bus</th>
      <th>transportation_el</th>
      <th>school_latitude</th>
      <th>school_longitude</th>
      <th>overall_rating</th>
      <th>rating_status</th>
      <th>rating_statement</th>
      <th>classification_description</th>
      <th>school_year</th>
      <th>third_contact_title</th>
      <th>third_contact_name</th>
      <th>network</th>
      <th>is_gocps_participant</th>
      <th>is_gocps_prek</th>
      <th>is_gocps_elementary</th>
      <th>is_gocps_high_school</th>
      <th>open_for_enrollment_date</th>
      <th>twitter</th>
      <th>youtube</th>
      <th>pinterest</th>
      <th>college_enrollment_rate_school</th>
      <th>college_enrollment_rate_mean</th>
      <th>graduation_rate_school</th>
      <th>graduation_rate_mean</th>
      <th>significantly_modified</th>
      <th>transportation_metra</th>
      <th>fourth_contact_title</th>
      <th>fourth_contact_name</th>
      <th>fifth_contact_title</th>
      <th>fifth_contact_name</th>
      <th>seventh_contact_title</th>
      <th>seventh_contact_name</th>
      <th>refugee_services</th>
      <th>visual_impairments</th>
      <th>freshman_start_end_time</th>
      <th>sixth_contact_title</th>
      <th>sixth_contact_name</th>
      <th>hard_of_hearing</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>609966</td>
      <td>3750</td>
      <td>23531</td>
      <td>HAMMOND</td>
      <td>Charles G Hammond Elementary School</td>
      <td>ES</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>Hammond creates a challenging learning environ...</td>
      <td>Principal</td>
      <td>Ms.Anamaria Orbe</td>
      <td>Asst Principal</td>
      <td>Nicole McConnell</td>
      <td>2819 W 21ST PL</td>
      <td>Chicago</td>
      <td>Illinois</td>
      <td>60623</td>
      <td>7.735355e+09</td>
      <td>7.735355e+09</td>
      <td>https://www.cps.edu/schools/schoolprofiles/609966</td>
      <td>https://cps.edu/hammond</td>
      <td>https://www.facebook.com/Charles-G-Hammond-Sch...</td>
      <td>True</td>
      <td>PK,K,1,2,3,4,5,6,7,8</td>
      <td>PK,K-8</td>
      <td>342</td>
      <td>336</td>
      <td>63</td>
      <td>132</td>
      <td>33</td>
      <td>304</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>There are 342 students enrolled at HAMMOND.  9...</td>
      <td>The largest demographic at HAMMOND is Hispanic...</td>
      <td>False</td>
      <td>Full and Half Day</td>
      <td>Full Day</td>
      <td>07:30 AM-02:30 PM</td>
      <td>2:30 pm - 5:30 pm</td>
      <td>7:30 am</td>
      <td>Spanish</td>
      <td>True</td>
      <td>True</td>
      <td>Y</td>
      <td>Y</td>
      <td>21, 94</td>
      <td>Pink</td>
      <td>41.852719</td>
      <td>-87.696243</td>
      <td>Level 1</td>
      <td>GOOD STANDING</td>
      <td>This school received a Level 1 rating, which i...</td>
      <td>Schools that have an attendance boundary. Gene...</td>
      <td>School Year 2019-2020</td>
      <td>Clerk</td>
      <td>Migdalia Nikolic</td>
      <td>Network 7</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>2004-09-01T00:00:00.000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>400069</td>
      <td>4150</td>
      <td>67081</td>
      <td>POLARIS</td>
      <td>Polaris Charter Academy</td>
      <td>ES</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>Polaris is committed to helping students becom...</td>
      <td>Director</td>
      <td>Michelle Navarre</td>
      <td>Other</td>
      <td>Francesca Peck</td>
      <td>620 N SAWYER AVE</td>
      <td>Chicago</td>
      <td>Illinois</td>
      <td>60624</td>
      <td>7.735341e+09</td>
      <td>7.735347e+09</td>
      <td>https://www.cps.edu/schools/schoolprofiles/400069</td>
      <td>https://pcachicago.org</td>
      <td>https://www.facebook.com/PolarisCharterAcademy</td>
      <td>False</td>
      <td>K,1,2,3,4,5,6,7,8</td>
      <td>K-8</td>
      <td>378</td>
      <td>343</td>
      <td>64</td>
      <td>8</td>
      <td>337</td>
      <td>33</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>There are 378 students enrolled at POLARIS.  9...</td>
      <td>The largest demographic at POLARIS is Black.  ...</td>
      <td>True</td>
      <td>NaN</td>
      <td>Full Day</td>
      <td>7:50 am-4:00 pm</td>
      <td>4:00 pm-6:00 pm</td>
      <td>07:20 AM</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>True</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>41.892550</td>
      <td>-87.707796</td>
      <td>Level 2</td>
      <td>NOT APPLICABLE</td>
      <td>This school received a Level 2 rating, which i...</td>
      <td>Schools that are open to all Chicago children,...</td>
      <td>School Year 2019-2020</td>
      <td>Office Manager</td>
      <td>Robin Alexander</td>
      <td>Charter</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>2007-07-01T00:00:00.000</td>
      <td>https://twitter.com/PolarisCA</td>
      <td>https://www.youtube.com/channel/UCHblvjecJ7Bp2...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>610191</td>
      <td>6070</td>
      <td>29291</td>
      <td>STONE</td>
      <td>Stone Elementary Scholastic Academy</td>
      <td>ES</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>Stone Academy offers full-day kindergarten, al...</td>
      <td>Principal</td>
      <td>James Joseph Brandon</td>
      <td>Assistant Principal</td>
      <td>Kate Nestler</td>
      <td>6239 N LEAVITT ST</td>
      <td>Chicago</td>
      <td>Illinois</td>
      <td>60659</td>
      <td>7.735342e+09</td>
      <td>7.735342e+09</td>
      <td>https://www.cps.edu/schools/schoolprofiles/610191</td>
      <td>http://stoneacademy.net/</td>
      <td>NaN</td>
      <td>False</td>
      <td>K,1,2,3,4,5,6,7,8</td>
      <td>K-8</td>
      <td>607</td>
      <td>319</td>
      <td>52</td>
      <td>121</td>
      <td>142</td>
      <td>98</td>
      <td>171</td>
      <td>166</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>26</td>
      <td>2</td>
      <td>0</td>
      <td>There are 607 students enrolled at STONE.  52....</td>
      <td>The largest demographic at STONE is White.  Th...</td>
      <td>True</td>
      <td>NaN</td>
      <td>Full Day</td>
      <td>8:00  AM - 3:00  PM</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>True</td>
      <td>False</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>49B, 84</td>
      <td>Brown</td>
      <td>41.995359</td>
      <td>-87.684793</td>
      <td>Level 1+</td>
      <td>GOOD STANDING</td>
      <td>This school received a Level 1+ rating, which ...</td>
      <td>Schools that specialize in a specific subject ...</td>
      <td>School Year 2019-2020</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Network 2</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>2004-09-01T00:00:00.000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>400173</td>
      <td>9648</td>
      <td>66801</td>
      <td>PATHWAYS - BRIGHTON PARK HS</td>
      <td>Pathways in Education- Brighton Park</td>
      <td>HS</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>NaN</td>
      <td>Principal</td>
      <td>Nicholas F Perez</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3124 W 47TH ST</td>
      <td>Chicago</td>
      <td>Illinois</td>
      <td>60632</td>
      <td>7.735791e+09</td>
      <td>7.735791e+09</td>
      <td>https://www.cps.edu/schools/schoolprofiles/400173</td>
      <td>https://pathwaysineducation.org</td>
      <td>https://www.facebook.com/PathwaysInEducationIL</td>
      <td>False</td>
      <td>9,10,11,12</td>
      <td>9-12</td>
      <td>408</td>
      <td>341</td>
      <td>42</td>
      <td>67</td>
      <td>12</td>
      <td>378</td>
      <td>14</td>
      <td>3</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>There are 408 students enrolled at PATHWAYS - ...</td>
      <td>The largest demographic at PATHWAYS - BRIGHTON...</td>
      <td>False</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>41.808226</td>
      <td>-87.702645</td>
      <td>Level 2+</td>
      <td>NOT APPLICABLE</td>
      <td>This school received a Level 2+ rating, which ...</td>
      <td>Schools that have their own processes for enro...</td>
      <td>School Year 2019-2020</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Options</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>2014-07-01T00:00:00.000</td>
      <td>https://twitter.com/pathwaysil</td>
      <td>NaN</td>
      <td>https://www.pinterest.com/PieIllinois/</td>
      <td>19.4</td>
      <td>67.2</td>
      <td>11.3</td>
      <td>78.9</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>610153</td>
      <td>5670</td>
      <td>25191</td>
      <td>RYDER</td>
      <td>William H Ryder Math &amp; Science Specialty ES</td>
      <td>ES</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>Our mission is to provide rigorous data driven...</td>
      <td>Principal</td>
      <td>Aaron Rucker</td>
      <td>Assistant Principal</td>
      <td>Darnell Garner</td>
      <td>8716 S WALLACE ST</td>
      <td>Chicago</td>
      <td>Illinois</td>
      <td>60620</td>
      <td>7.735354e+09</td>
      <td>7.735354e+09</td>
      <td>https://www.cps.edu/schools/schoolprofiles/610153</td>
      <td>https://ryderschool.org</td>
      <td>NaN</td>
      <td>True</td>
      <td>PK,K,1,2,3,4,5,6,7,8</td>
      <td>PK,K-8</td>
      <td>402</td>
      <td>360</td>
      <td>116</td>
      <td>3</td>
      <td>396</td>
      <td>4</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>There are 402 students enrolled at RYDER.  89....</td>
      <td>The largest demographic at RYDER is Black.  Th...</td>
      <td>True</td>
      <td>Half Day</td>
      <td>Full Day</td>
      <td>08:45 AM-03:45 PM</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>True</td>
      <td>NaN</td>
      <td>Y</td>
      <td>24, 87</td>
      <td>Red</td>
      <td>41.735379</td>
      <td>-87.638843</td>
      <td>Level 1</td>
      <td>GOOD STANDING</td>
      <td>This school received a Level 1 rating, which i...</td>
      <td>Schools that have an attendance boundary. Gene...</td>
      <td>School Year 2019-2020</td>
      <td>Technology Coordinator</td>
      <td>Montell Pinkston</td>
      <td>Network 11</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>2004-09-01T00:00:00.000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>True</td>
      <td>Rock Island District (RI)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



We will only be using the columns which appear in the mask below.
            


```python
column_mask = ['school_id',
               'primary_category',
               'grades_offered_all',
               'student_count_total',
               'student_count_low_income',
               'student_count_special_ed',
               'student_count_english_learners',
               'graduation_rate_school',
               'dress_code',
               'classroom_languages',
               'network',
               'graduation_rate_mean'
              ]
```

Use the mask to isolate the columns of interest.  


```python
# Your code here

```


```python
one_random_student(student_first_names)
```

    Christos


We will only be working with high schools. 

Subset the dataframe to include only schools whose `primary_category` indicated high school.


```python
# Your code here
sy_201819_hs = None
```


```python
one_random_student(student_first_names)
```

    Christos


# NA's 


```python
# Count the na's across all columns of the high school dataframe

```


```python
one_random_student(student_first_names)
```

    Christos


There are several ways to deal with na's. We will explore:
  
  - Dropping any row which has an na in it
  - Interporlating the mean value into the na
  
Only use `inplace=True` in the second instance so we can explore both methods successively.


## Dropping any row which has an `NaN` in it



```python
# Your code here

```


```python
# How many records were lost using this method?
```


```python
one_random_student(student_first_names)
```

    Joe


## Interporlating the mean value to fillna

Let's work with the graduation_rate_school column.  

Take the value in the `graduation_rate_mean` and fill na's in `graduation_rate_school` with it.



```python
# Your code here
```


```python
one_random_student(student_first_names)
```

    Jamie


We will return to the classroom_languages na's in a moment.

# Creating New Features

Create a column called `percent_low_income` which is the number of low income students divided by total student count.


```python
# Your answer here
```


```python
one_random_student(student_first_names)
```

    Marcos


Create a column which counts the number of classroom languages offered in a school.



```python
# To help do so, we will first, replace na's in the column with the string None
sy_201819_hs['classroom_languages'].fillna('None', inplace=True)

```

Next, use apply and a lambda function to split each cell's strings on the comma.


```python
# Your code here

sy_201819_hs['classroom_languages_count'] = None
```

    /Users/johnmaxbarry/.local/lib/python3.7/site-packages/ipykernel_launcher.py:3: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      This is separate from the ipykernel package so we can avoid doing imports until


Now, use a second apply on classroom_languages_count and pass the built in operator `len`


```python
# Your Code Here

```


```python
one_random_student(student_first_names)
```

    Svitlana



```python
sy_201819_hs.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school_id</th>
      <th>primary_category</th>
      <th>grades_offered_all</th>
      <th>student_count_total</th>
      <th>student_count_low_income</th>
      <th>student_count_special_ed</th>
      <th>student_count_english_learners</th>
      <th>graduation_rate_school</th>
      <th>dress_code</th>
      <th>classroom_languages</th>
      <th>network</th>
      <th>graduation_rate_mean</th>
      <th>percent_low_income</th>
      <th>classroom_languages_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>400173</td>
      <td>HS</td>
      <td>9,10,11,12</td>
      <td>408</td>
      <td>341</td>
      <td>42</td>
      <td>67</td>
      <td>11.3</td>
      <td>False</td>
      <td>None</td>
      <td>Options</td>
      <td>78.9</td>
      <td>0.835784</td>
      <td>1</td>
    </tr>
    <tr>
      <th>11</th>
      <td>609704</td>
      <td>HS</td>
      <td>9,10,11,12</td>
      <td>559</td>
      <td>555</td>
      <td>145</td>
      <td>159</td>
      <td>68.9</td>
      <td>True</td>
      <td>Spanish, Spanish for Heritage Speakers</td>
      <td>Network 16</td>
      <td>78.9</td>
      <td>0.992844</td>
      <td>2</td>
    </tr>
    <tr>
      <th>17</th>
      <td>609734</td>
      <td>HS</td>
      <td>7,8,9,10,11,12</td>
      <td>3644</td>
      <td>1871</td>
      <td>447</td>
      <td>334</td>
      <td>83.9</td>
      <td>False</td>
      <td>Arabic, French, Korean, Polish, Spanish, Spani...</td>
      <td>Network 14</td>
      <td>78.9</td>
      <td>0.513447</td>
      <td>6</td>
    </tr>
    <tr>
      <th>21</th>
      <td>400106</td>
      <td>HS</td>
      <td>9,10,11,12</td>
      <td>607</td>
      <td>571</td>
      <td>142</td>
      <td>3</td>
      <td>72.0</td>
      <td>True</td>
      <td>Spanish</td>
      <td>Charter</td>
      <td>78.9</td>
      <td>0.940692</td>
      <td>1</td>
    </tr>
    <tr>
      <th>33</th>
      <td>609750</td>
      <td>HS</td>
      <td>6,7,8,9,10,11,12</td>
      <td>31</td>
      <td>30</td>
      <td>6</td>
      <td>3</td>
      <td>78.9</td>
      <td>False</td>
      <td>Spanish</td>
      <td>Network 15</td>
      <td>NaN</td>
      <td>0.967742</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



Convert dress_code from a boolean to a binary using `.map`.

Hint: `.map` takes a dictionary with keys representing the extant data and values representing what you want to replace them with.



```python
# Your code here
```


```python
one_random_student(student_first_names)
```

    Marcos


As a bonus challenge, create a  column `students_per_grade` which divides the total number of students by the number of grades offered


```python
# Your code here
```
