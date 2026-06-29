


### Introduction : 

+ Pandas is an open-source Python library designed for *data manipulation and analysis*. It makes working with structured data fast, flexible, and intuitive especially if you're dealing with CSV files, Excel sheets, SQL tables, JSON, or APIs.
+ In pandas we can Reads different types of data files, Cleaning data, Filtre data and sorting data.
+ The two core data structures in Pandas are :
1.  ***Series :***  a 1D labeled array (like a column)
2. ***DataFrame :*** a 2D labeled data structure (like SQL table)

+ ###### How to import Pandas : 

```Python
import pandas as pd
```

+ ### Pandas Series : 

`series` : to manually create and store data in 1D array ***(a array)***.
+ Each column in DataFrame is a serie

![[Pasted image 20260519215335.png|280]]


```python
data = pd.Series([0.25, 0.5, 0.75, 1.0])
data 
```

+ *Output :*

![[Pasted image 20260626132920.png|160]]

+ As we see in the output, the `Series` wraps both a sequence of values and a sequence of indices, which we can access with the `values` and `index` attributes.

+ *Giving an  the indice :*

```python
data = pd.Series([1, 2, 3, 4], index=['a', 'b', 'c', 'd'])
print(data)
```

![[Pasted image 20260627024643.png|473]]

```python
data['b'] # the output is : 2
```

+ The `Series`-as-dictionary analogy can be made even more clear by constructing a `Series` object directly from a Python dictionary:

```python
population_dict = {'California' : 78198682,
                   'Texas' : 27299277,
                   'New York' : 92895229,
                   'Florida' : 195554271,
                   'Illiones' : 122294258 }
population = pd.Series(population_dict)
population
```

![[Pasted image 20260627143518.png]]

+ *Select an element :*

``` python
print(popultion['California']) # Output = 78198682
```

+ Unlike a dictionary, though, the `Series` also supports array-style operations such as slicing : 

```Python
print(population['California' : 'Illiones']) # from index to index
```

+ *Another Example in indexing :*

```Python
pd.Series({'a': 2, 'c' : 5, 'b' : 10}, index = ['a', 'c'])
```

![[Pasted image 20260627145706.png]]

+ Notice that in this case, the `Series` is populated only with the explicitly identified keys.


+ ### Pandas data table representation : *(DataFrame)*

![[Pasted image 20260518124603.png|503]]


`DataFrame` : To manually store data in a table.

+ *Example :*

```Python
df = pd.DataFrame(
    {
        "Name" : [
            "Othmane",
            "Mehdi",
            "Aymane",
            "Imad",
            "Douae",
        ],
        "Age": [18, 19, 18, 21, 18],
        "Sex" : ["Male", "Male", "Male", "Male", "Female"],
    }
)

	df1 = df["Age"]
df2 = df.max()

print(df)
print(df1)
print(df2)

```

+ *Example results :*

![[Pasted image 20260518131328.png|336]]

![[Pasted image 20260519214556.png]]

+ ###### Constructing DataFrame objects : 

+ A `DataFrame` is a collection of `Series` objects, and a single column `DataFrame` can be constructed from a single `Series`:

+ ###### From a list of dicts :  
+ Any list of dictionaries can be made into a `DataFrame`. We'll use a simple list comprehension to create some data:

```Python
data = [{'a' : i, 'b' : i * 2} for i in range (3)]
pd.DataFrame(data)
```

![[Pasted image 20260628221507.png|448]]

+ Even if some keys in the dictionary are missing, Pandas will fill them in with `NaN` (i.e., "not a number") values:

```Python
data2 = [{'a' : 2, 'b' : 4}, {'a' : 6, 'c' : 55}, {'b' : 5, 'c' : 6}]
pd.DataFrame(data2)
```

![[Pasted image 20260628221528.png|490]]

+ ###### From a two-dimensional NumPy array :

Given a two-dimensional array of data, we can create a `DataFrame` with any specified column and index names. If omitted, an integer index will be used for each:

```Python
pd.DataFrame(np.random.rand(3, 2), columns = ['foo', 'bar'], index = ['a', 'b', 'c'])
```

![[Pasted image 20260628223612.png|543]]

+ Now that we have this along with the `population` Series from before, we can use a dictionary to construct a single two-dimensional object containing this information:

``` Python
population_dict = {'California' : 78198682,
                   'Texas' : 27299277,
                   'New York' : 92895229,
                   'Florida' : 195554271,
                   'Illiones' : 122294258
                }

area_dict = {'California': 423967,
             'Texas': 695662,
             'New York': 141297,
             'Florida': 170312,
             'Illiones': 149995
            }

population = pd.Series(population_dict)
area = pd.Series(area_dict)

states = pd.DataFrame({'population' : population, 'area' : area})

print(states)
```


![[Pasted image 20260627151056.png]]

+ *Select a `Series` from an `DataFram` :*

```Python
pd.DataFrame(population, columns=['population'])
```

![[Pasted image 20260627172745.png]]


+ #### Operation on Data in Pandas : 



1. ***Arithmitic Operation :***

 ```Python
num = pd.Series([1 ,2 , 3])
print(num + 5)
# Output : 
0 6 
1 7 
2 8 
dtype: int64
 ```

2. ***Operation between Series :***

``` Python
s1 = pd.Series([1, 3, 5])
s2 = pd.Series([2, 9, 7])
print(s1 + s2)
# Output : 
0 3
1 12
2 12
dtype: int64
```

3. ***but when we Don't match the Series :***


``` Python
s1 = pd.Series([1,3], index = ['a', 'b'])
s2 = pd.Series([2,9], index = ['b', 'c'])
print(s1 + s2)
# Output : 
a NaN 
b 5.0 
c NaN 
dtype: float64
```

4. ***Operation on DataFrame :***

``` Python
df = pd.DataFrame({
    "Age" : [18, 20],
    "Score" : [15, 22]
})
print(df + 2)
print(df["Age"] + 2)
print(df["Score"] > 20)
print(df[df["Age"] > 18])

#Output : 
  Age  Score 
0  20   17 
1  22   24 
------------ 
0 20 
1 22 
Name: Age, dtype: int64 
------------ 
0 False 
1 True 
Name: Score, dtype: bool 
------------ 
  Age Score 
1 20 22
```

5. ***Operation on Columns***

+ Creating a new columns :

```Python
df['Results'] = df['Score'] * 2
df
# Output :
  Age Score Results 
0  18   15    30 
1  20   22    44
```

+ ***Aggregation :***

```Python
df.describe()
```

|       | Age       | Score     | Results   |
| ----- | --------- | --------- | --------- |
| count | 2.000000  | 2.000000  | 2.000000  |
| mean  | 19.000000 | 18.500000 | 37.000000 |
| std   | 1.414214  | 4.949747  | 9.899495  |
| min   | 18.000000 | 15.000000 | 30.000000 |
| 25%   | 18.500000 | 16.750000 | 33.500000 |
| 50%   | 19.000000 | 18.500000 | 37.000000 |
| 75%   | 19.500000 | 20.250000 | 40.500000 |
| max   | 20.000000 | 22.000000 | 44.000000 |


+ #### Missing Data in Pandas : 

+ Missing data in pandas refers to values that not available in the dataset, it usually represented by `NaN` *(Not a Number)*

+ `NaN` does not mean 0
	 0 it's a valid value and `NaN` is missing value


`isna` : return `True` for missing value and `False` for valid value.
`notna` : the opposite of `isna`.

```Python
s1 = pd.Series([1,3], index = ['a', 'b'])
s2 = pd.Series([2,9], index = ['b', 'c'])
s3 = s1 + s2
pd.isna(s3)

# Output : 
a True 
b False 
c True
```

 + to count missing value : 

```Python
s1 = pd.Series([1,3], index = ['a', 'b'])
s2 = pd.Series([2,9], index = ['b', 'c'])
s3 = s1 + s2
s3.isna()
# Output : 
2 
```

+ to drop missing value : 

``` Python
s3.dropna()
# Output
a NaN 
b 5.0 -----> b 5.0
c NaN 
```


