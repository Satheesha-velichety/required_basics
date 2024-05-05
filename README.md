################################################################################################################################################################
################################################################################################################################################################
################################################################################################################################################################
import pandas as pd
# Read the JSON file into a DataFrame
df = pd.read_json('data/json_basic.json')

# Display the DataFrame
print("Original DataFrame:")
print(df)

# Drop the 'id' column
df.drop(columns=['id'], inplace=True)

# Convert 'age' and 'salary' columns to numeric
df['age'] = pd.to_numeric(df['age'], errors='coerce')
df['salary'] = pd.to_numeric(df['salary'], errors='coerce')

# Drop rows with missing values
df.dropna(inplace=True)
df.drop_duplicates(inplace=True)

# Display the cleaned DataFrame
print("\nCleaned DataFrame:")
print(df)

print("df.T: "+ str(df.T))
print("df.axes: "+ str(df.axes))
print("df.dtypes: "+ str(df.dtypes))

print("df.empty: "+ str(df.empty))
print("df.ndim: "+ str(df.ndim))
print("df.shape: "+ str(df.shape))
print("df.size: "+ str(df.size))

print(df.sum()) 
print(df.describe())
print(df.describe(include=['object']))

#1	count()	Number of non-null observations
#2	sum()	Sum of values
#3	mean()	Mean of Values
#4	median()	Median of Values
#5	mode()	Mode of values
#6	std()	Standard Deviation of the Values
#7	min()	Minimum Value
#8	max()	Maximum Value
#9	abs()	Absolute Value
#10	prod()	Product of Values
#11	cumsum()	Cumulative Sum
#12	cumprod()	Cumulative Product


print('------------------------------------')
for col in df:
   print(col)
print('------------------------------------')
for key,value in df.iteritems():
   print('------------------------------------')
   print ("key:"+str(key),"value:"+str(value))
   print('------------------------------------')
print('------------------------------------')

print('------------------------------------')
for row_index,row in df.iterrows():
   print('------------------------------------')
   print(row_index,row)
   print('------------------------------------')
print('------------------------------------')

#sorted_df = df.sort_index(ascending=False)
#sorted_df=unsorted_df.sort_index(axis=1)
sorted_df = unsorted_df.sort_values(by='col1')
sorted_df = unsorted_df.sort_values(by=['col1','col2'])
################################################################################################################################################################
################################################################################################################################################################
################################################################################################################################################################

#multi records json
import pandas as pd  
import numpy as np 


# Read the JSON file into a DataFrame
df = pd.read_json('data/multi_record_json.json')
print(df)

df_grades = pd.json_normalize(df['grades'])
df_grades=df_grades.add_prefix("grades_")
print(df_grades)

df_details = pd.json_normalize(df['details'])
df_details=df_details.add_prefix("details_")
print(df_details)

df2=pd.concat([df.drop(columns=['details','grades']),df_grades,df_details],axis=1 )
print(df2)
print(df2)

import re
df2['details_salary'] = df2['details_salary'].apply(lambda x : re.search(r'\d{1,3}(?:,\d{3})*(?:\.\d{1,2})?',x).group())

df2['total_grades'] = df2 ['grades_math'] +   df2 ['grades_english']

print(df2)

def double_mean(x):
    x=x*2
    return x.mean()

print(df2.groupby(['name']).agg([np.sum, np.mean, np.std,double_mean]))

sorted_df = df2.sort_values(by=['grades_math','grades_english'],ascending=False)

print(sorted_df)


#with open('data/multi_record_json.json') as file:
#    json_data=json
################################################################################################################################################################
unittest

#nestedjson
import json
import pandas as pd

with open('data/nested_json.json') as data_file:    
    data = json.load(data_file)  


df = pd.json_normalize(data, 'locations', ['date', 'number', 'name'], 
                    record_prefix='locations_')
print (df)

#every line a josn
#pd.read_json('file_name', orient='records', lines=True)




import unittest
class TestStringMethods(unittest.TestCase):

    def test_upper(self):
        self.assertEqual('foo'.upper(), 'FOO')

    def test_isupper(self):
        self.assertTrue('FOO'.isupper())
        self.assertFalse('Foo'.isupper())

    def test_split(self):
        s = 'hello world'
        self.assertEqual(s.split(), ['hello', 'world'])
        # check that s.split fails when the separator is not a string
        with self.assertRaises(TypeError):
            s.split(2)
        

if __name__ == '__main__':
    unittest.main()

################################################################################################################################################################
string
isalnum()/isalpha()/isdigit()/isnumeric()

islower()/isupper()/lower()/upper()/swapcase()/capitalize()/casefold()
	
isspace()/rstrip()/lstrip()/strip()

rfind()/rindex()/split()/splitlines()	

endswith()/ startswith()

find()/index()	 #Searches the string for a specified value and returns the position of where it was found

txt = "Hello Sam!"
print(txt.replace("S", "P"))

mytable = str.maketrans("S", "P")
print(txt.translate(mytable))


print("Hello, World!".center(19,'0')) 	#Converts string into lower case
print("apples, apple ".count("apple",0,20))  #count the repeating string inside the string


