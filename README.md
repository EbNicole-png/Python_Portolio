# Gibbs_Python_Portolio
This is the portfolio of python coding that I learned during BISC 450C.


## Using Jupyter Notebooks


 ```python
%matplotlib inline
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
sns.set(style = "darkgrid")
```


```python
df = pd.read_csv('/home/student/Desktop/classroom/myfiles/notebooks/fortune500.csv')
```


```python
df.head()
```


```python
df.tail()
```


```python
df.columns = ['year', 'rank','company','revenue','profit']
```


```python
df.head()
```


```python
len(df)
```


```python
df.dtypes
```


```python
non_numeric_profits = df.profit.str.contains ('[^0-9.-]')
df.loc[non_numeric_profits].head()
```


```python
set(df.profit[non_numeric_profits])
```


```python
len(df.profit[non_numeric_profits])
```


```python
bin_sizes, _, _ = plt.hist(df.year[non_numeric_profits], bins = range(1955, 2006) )
```


```python
df = df.loc[~non_numeric_profits]
df.profit = df.profit.apply(pd.to_numeric)
```


```python
len(df)
```


```python
df.dtypes
```


```python
group_by_year = df.loc[:, ['year', 'revenue', 'profit']].groupby('year')
avgs = group_by_year.mean()
x = avgs.index
y1 = avgs.profit
def plot(x, y, ax, title, y_label):
    ax.set_title(title)
    ax.set_ylabel(y_label)
    ax.plot(x, y)
    ax.margins(x = 0, y= 0)
```


```python
fig, ax = plt.subplots()
plot(x, y1, ax, 'Increase in mean Fortune 500 company profits from 1955 to 2005', 'Profit (millons)')
```


```python
y2 = avgs.revenue
fig, ax = plt.subplots()
plot(x, y2, ax, 'Increase in mean Fortune 500 company revenues from 1955 to 2005', 'Revenue (millions)')
```


```python
def plot_with_std(x, y, stds, ax, title, y_label):
    ax.fill_between(x, y - stds, y + stds, alpha = 0.2)
    plot(x, y, ax, title, y_label)
fig, (ax1, ax2) = plt.subplots(ncols= 2)
title = 'Increase in mean and std fortune 500 company %s from 1955 to 2005'
stds1 = group_by_year.std().profit.values
stds2 = group_by_year.std().revenue.values
plot_with_std(x, y1.values, stds1, ax1, title % 'profits', 'Profit (millions)' )
plot_with_std(x, y2.values, stds2, ax2, title % 'revenues', 'Revenue (millions)')
fig.set_size_inches (14,4)
fig.tight_layout()
```


## Python Fundamentals


```python
# Any python interpreter can be used as a calculator: 
3 + 5 * 4
```




    23




```python
# Lets save a value to a variable
weight_kg = 60
```


```python
print(weight_kg)
```

    60



```python
# Weight0 = valid
# 0weight = invalid
# weight and Weight are different
```


```python
# Types of data
# There are three common types of data
# Integer numbers
# floating point numbers
# Strings 
```


```python
# Floating point number
weight_kg = 60.3
```


```python
# String comprised of letters
patient_name = "Jon Smith"
```


```python
# String comprised of numbers
patient_id = '001'
```


```python
# Use variables in python

weight_lb = 2.2 * weight_kg

print(weight_lb)
```

    132.66



```python
# Lets add a prefix to our patient id

patient_id = 'inflam_' + patient_id

print(patient_id)
```

    inflam_001



```python
# Lets combine print statements


print(patient_id, 'weight in kilograms:', weight_kg)
```

    inflam_001 weight in kilograms: 60.3



```python
# we can call a function inside another function

print(type(60.3))

print(type(patient_id))
```

    <class 'float'>
    <class 'str'>



```python
# We can also do calculations inside the pring function

print('weight in lbs:', 2.2 * weight_kg)
```

    weight in lbs: 132.66



```python
print(weight_kg)
```

    60.3



```python
weight_kg = 65.0
print('weight in kilograms is now:', weight_kg)
```

    weight in kilograms is now: 65.0


## Analyzing Data

```python
import numpy
```


```python
numpy.loadtxt(fname = 'inflammation-01.csv', delimiter= ',')
```


    ---------------------------------------------------------------------------

    OSError                                   Traceback (most recent call last)

    <ipython-input-4-593eb3d520cf> in <module>
    ----> 1 numpy.loadtxt(fname = 'inflammation-01.csv', delimiter= ',')
    

    ~/anaconda3/lib/python3.7/site-packages/numpy/lib/npyio.py in loadtxt(fname, dtype, comments, delimiter, converters, skiprows, usecols, unpack, ndmin, encoding, max_rows)
        966             fname = os_fspath(fname)
        967         if _is_string_like(fname):
    --> 968             fh = np.lib._datasource.open(fname, 'rt', encoding=encoding)
        969             fencoding = getattr(fh, 'encoding', 'latin1')
        970             fh = iter(fh)


    ~/anaconda3/lib/python3.7/site-packages/numpy/lib/_datasource.py in open(path, mode, destpath, encoding, newline)
        267 
        268     ds = DataSource(destpath)
    --> 269     return ds.open(path, mode, encoding=encoding, newline=newline)
        270 
        271 


    ~/anaconda3/lib/python3.7/site-packages/numpy/lib/_datasource.py in open(self, path, mode, encoding, newline)
        621                                       encoding=encoding, newline=newline)
        622         else:
    --> 623             raise IOError("%s not found." % path)
        624 
        625 


    OSError: inflammation-01.csv not found.





## Storing Values in Lists

```python
odds = [1, 3, 5, 7]
print('odds are:', odds)
```

    odds are: [1, 3, 5, 7]



```python
print('first element:', odds[0])
print('last element:', odds[3])
print('"-1" element:', odds[ -1])
```

    first element: 1
    last element: 7
    "-1" element: 7



```python
names = ['Curie', 'Darwing', 'Turing'] # Typo in Darwin's name

print('names is originally:', names)

names[1] = 'Darwin' # Correct the name

print('final value of names:' , names)
```

    names is originally: ['Curie', 'Darwing', 'Turing']
    final value of names: ['Curie', 'Darwin', 'Turing']



```python
#name = 'Darwin'
#name[0] = 'd'
```


```python
odds.append(11)
print('odds after adding a value:' , odds)
```

    odds after adding a value: [1, 3, 5, 7, 11]



```python
removed_element = odds.pop(0)
print('odds after removing the first element:', odds)
print('removed_element:', removed_element)
```

    odds after removing the first element: [3, 5, 7, 11]
    removed_element: 1



```python
odds.reverse()
print('odds after reversing:', odds)

```

    odds after reversing: [11, 7, 5, 3]



```python
odds = [3,5,7]
primes = odds
primes.append(2)
print('primes:',primes)
print('odds:', odds)
```

    primes: [3, 5, 7, 2]
    odds: [3, 5, 7, 2]



```python
odds = [3,5,7]
primes = list(odds)
primes.append(2)
print('primes:', primes)
print('odds:', odds)
```

    primes: [3, 5, 7, 2]
    odds: [3, 5, 7]



```python
binomial_name = "Drosophila melanogaster"
group = binomial_name[0:10]
print('group:', group)

species = binomial_name[11:23]
print('species:', species)

chromosomes = ['X', 'Y', '2', '3', '4']
autosomes = chromosomes[2:5]
print('autosomes:', autosomes)

last = chromosomes[-1]
print('last:', last)
```

    group: Drosophila
    species: melanogaster
    autosomes: ['2', '3', '4']
    last: 4



```python
date = 'Monday 4 January 2023'
day = date[0:6]
print('Using 0 to begin range:', day)
day = date[:6]
print('Omitting beginning index:', day)
```

    Using 0 to begin range: Monday
    Omitting beginning index: Monday



```python
months = ['jan', 'feb', 'mar', 'apr', 'may', 'jun', 'jul', 'aug', 'sep', 'oct', 'nov', 'dec']
sond = months [8:12]
print('With known last position:', sond)

sond = months[8:len(months)]
print('Using len() to get last entry:', sond)

sond = months[8:]
print('Omitting ending index:', sond)
```

    With known last position: ['sep', 'oct', 'nov', 'dec']
    Using len() to get last entry: ['sep', 'oct', 'nov', 'dec']
    Omitting ending index: ['sep', 'oct', 'nov', 'dec']


## Using Loops


```python
odds = [1, 3, 5, 7]
print('odds are:', odds)
```

    odds are: [1, 3, 5, 7]



```python
print('first element:', odds[0])
print('last element:', odds[3])
print('"-1" element:', odds[ -1])
```

    first element: 1
    last element: 7
    "-1" element: 7



```python
names = ['Curie', 'Darwing', 'Turing'] # Typo in Darwin's name

print('names is originally:', names)

names[1] = 'Darwin' # Correct the name

print('final value of names:' , names)
```

    names is originally: ['Curie', 'Darwing', 'Turing']
    final value of names: ['Curie', 'Darwin', 'Turing']



```python
#name = 'Darwin'
#name[0] = 'd'
```


```python
odds.append(11)
print('odds after adding a value:' , odds)
```

    odds after adding a value: [1, 3, 5, 7, 11]



```python
removed_element = odds.pop(0)
print('odds after removing the first element:', odds)
print('removed_element:', removed_element)
```

    odds after removing the first element: [3, 5, 7, 11]
    removed_element: 1



```python
odds.reverse()
print('odds after reversing:', odds)

```

    odds after reversing: [11, 7, 5, 3]



```python
odds = [3,5,7]
primes = odds
primes.append(2)
print('primes:',primes)
print('odds:', odds)
```

    primes: [3, 5, 7, 2]
    odds: [3, 5, 7, 2]



```python
odds = [3,5,7]
primes = list(odds)
primes.append(2)
print('primes:', primes)
print('odds:', odds)
```

    primes: [3, 5, 7, 2]
    odds: [3, 5, 7]



```python
binomial_name = "Drosophila melanogaster"
group = binomial_name[0:10]
print('group:', group)

species = binomial_name[11:23]
print('species:', species)

chromosomes = ['X', 'Y', '2', '3', '4']
autosomes = chromosomes[2:5]
print('autosomes:', autosomes)

last = chromosomes[-1]
print('last:', last)
```

    group: Drosophila
    species: melanogaster
    autosomes: ['2', '3', '4']
    last: 4



```python
date = 'Monday 4 January 2023'
day = date[0:6]
print('Using 0 to begin range:', day)
day = date[:6]
print('Omitting beginning index:', day)
```

    Using 0 to begin range: Monday
    Omitting beginning index: Monday



```python
months = ['jan', 'feb', 'mar', 'apr', 'may', 'jun', 'jul', 'aug', 'sep', 'oct', 'nov', 'dec']
sond = months [8:12]
print('With known last position:', sond)

sond = months[8:len(months)]
print('Using len() to get last entry:', sond)

sond = months[8:]
print('Omitting ending index:', sond)
```

    With known last position: ['sep', 'oct', 'nov', 'dec']
    Using len() to get last entry: ['sep', 'oct', 'nov', 'dec']
    Omitting ending index: ['sep', 'oct', 'nov', 'dec']



## Using Multiple Files




## Making Choices

```python
num = 37
if num > 100:
    print('greater')
else: 
    print('not greater')
print('done')
```

    not greater
    done



```python
num = 53 
print('before conditional...')
if num > 100:
    print(num, 'is greater than 100')
```

    before conditional...



```python
num = 14

if num > 0:
    print(num, 'is positive')
elif num ==0:
    print(num, 'is zero')
else: 
    print(num, 'is negative')
```

    14 is positive



```python
if (1 > 0) and (-1 >=0):
    print('both parts are true')
else: 
    print('at least one part if false')
```

    at least one part if false



```python
if (1 > 0) or (-1 >=0):
    print('at least one part is true')
else: 
    print('both of these are false')
```

    at least one part is true



```python
import numpy
```


## Functions (1, 2, 3, and 4)

```python
fahrenheit_val = 99
celsius_val = ((fahrenheit_val - 32) *(5/9))

print(celsius_val)
```

    37.22222222222222



```python
fahrenheit_val2 = 43
celsius_val2 = ((fahrenheit_val2 - 32) *(5/9))

print(celsius_val2)
```

    6.111111111111112



```python
def explicit_fahr_to_celsius(temp):
    # Assign the converted value to a variable
    converted = ((temp - 32) *(5/9))
    # Return the values of the new variable
    return converted
```


```python
def fahr_to_celsius(temp):
    # Return converted values more effeciently using the reutrn function without creating
    # a new variable. This code does the same thing as the previous function but it is more 
    # explicit in explaining how the return command works. 
    return ((temp - 32) * (5/9))
```


```python
fahr_to_celsius(32)
```




    0.0




```python
explicit_fahr_to_celsius(32)
```




    0.0




```python
print('Freezing point of water:', fahr_to_celsius, 'C')
print('Boiling point of water:', fahr_to_celsius, 'C')
```

    Freezing point of water: <function fahr_to_celsius at 0x7f9be8e0da70> C
    Boiling point of water: <function fahr_to_celsius at 0x7f9be8e0da70> C



```python
def celsius_to_kelvin(temp_c):
    return temp_c + 273.15

print('freezing point of water in Kelvin:', celsius_to_kelvin(0.))

```

    freezing point of water in Kelvin: 273.15



```python
def fahr_to_kelvin(temp_f):
    temp_c = fahr_to_celsius(temp_f)
    temp_k = celsius_to_kelvin(temp_c)
    return temp_k

print('freezing point of water in Kelvin:', fahr_to_kelvin(212.0))
```

    freezing point of water in Kelvin: 373.15



```python
temp_kelvin = fahr_to_kelvin(212.0)
print('Temprature in Kelvin was:', temp_kelvin)
```

    Temprature in Kelvin was: 373.15



```python
temp_kelvin
```




    373.15




```python
def print_temperatures():
    print('Temperature in Fahrenheit was:', temp_fahr)
    print('Temperature in Kelvin was:', temp_kelvin)

temp_fahr = 212.0
temp_kelvin = fahr_to_kelvin(temp_fahr)

print_temperatures()
```

    Temperature in Fahrenheit was: 212.0
    Temperature in Kelvin was: 373.15


## Errors

```python
# This code has an intentional error. You can type it directly
# or use it for reference to understand the error message below. 

def favorite_ice_icream():
    ice_creams = [
        'chocolate'
        'vanilla'
        'strawberry'
    ]
    print(ice_creams[3])
    
favorite_ice_cream()
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-1-ed5d4e748ebb> in <module>
         10     print(ice_creams[3])
         11 
    ---> 12 favorite_ice_cream()
    

    NameError: name 'favorite_ice_cream' is not defined



```python
def some_function():
    msg = 'hello, world!'
    print(msg)
    return msg
```


```python
print(a)
```


```python
print('hello')
```


```python
count = 0
for number in range(10):
    count = count + number
print('The count is:', count)
```


```python
letters = ['a','b','c']

print('Letter #1 is', letters[0])
print('Letter #2 is', letters[1])
print('Letter #3 is', letters[2])
print('Letter #4 is', letters[3])
```


```python
letters = ['a','b','c']

print('Letter #1 is', letters[0])
print('Letter #2 is', letters[1])
print('Letter #3 is', letters[2])
#print('Letter #4 is', letters[3])
```


```python
file_handle = open('myfile.txt', 'w')
```


## Defensive Programming

```python
numbers = [1.5, 2.3, 0.7, 0.001, 4.4]
total = 0.0
for num in numbers:
    assert num > 0.0, 'Data should only contain positive values'
    total += num
print('total is:', total)
```

    total is: 8.901



```python
def normalize_rectangle(rect):
    """Normalizes a rectangle so that it is at the origin and 1.0 units long on its logest axis
    input should be of the format (x0, y0, x1, y1).
    (x0, y0), and (x1, y1) define the lower left and upper right ocrners of the rectangle resepctively."""
    assert len(rect) == 4,  'Rectangles must contain 4 coordinates'
    x0, y0, x1, y1 = rect
    assert x0 < x1, 'Invalid X coordinates'
    assert y0 < y1, 'Invalid Y coordinates'
    
    dx = x1 - x0
    dy = y1 - y0
    if dx > dy: 
        scaled = dx / dy
        upper_x, upper_y = 1.0, scaled
    else: 
        scaled = dx / dy
        upper_x, upper_y = scaled, 1.0
    assert 0 < upper_x <= 1.0, 'Calculated upper x corrdinate invalid'
    assert 0 < upper_y <= 1.0, 'Calculated upper y coordinate invalid'
    
    return (0,0, upper_x, upper_y)
```


```python
print(normalize_rectangle( (0.0, 1.0, 2.0) ))
```


```python
print(normalize_rectangle( (4.0, 2.0, 1.0, 5.0) ))
```


```python
print(normalize_rectangle( (0.0, 0.0, 1.0, 5.0)))
```

## Transcribing DNA into RNA

```python
# Prompt the user to enter the input fasta file name

input_file_name = input("Enter the name of the input fasta file: ")
```

    Enter the name of the input fasta file:  BRCA_1_sequence.txt



```python
# Open the input fasta file and read the DNA sequence

with open(input_file_name, "r") as input_file:
    dna_sequence = ""
    for line in input_file:
        if line.startswith(">"):
            continue 
        dna_sequence += line.strip()
```


```python
# Transcribe the DNA to RNA
rna_sequence = ""
for nucleotide in dna_sequence:
    if nucleotide == "T":
        rna_sequence += "U"
    else: 
        rna_sequence += nucleotide
```


```python
# Prompt the user to enter the output file name

output_file_name = input("Enter the name of the output file: ")
```

    Enter the name of the output file:  BRCA1_RNA.txt



```python
# Save the RNA sequence to a text file

with open(output_file_name, "w") as output_file:
    output_file.write(rna_sequence)
    print("The RNA sequence has been saved to (output_file_name)")
```

    The RNA sequence has been saved to (output_file_name)



```python
print(rna_sequence)
```

    AUGGAUUUAUCUGCUCUUCGCGUUGAAGAAGUACAAAAUGUCAUUAAUGCUAUGCAGAAAAUCUUAGAGUGUCCCAUCUGGAGCCUACAAGAAAGUACGAGAUUUAGUCAACUUGUUGAAGAGCUAUUGAAAAUCAUUUGUGCUUUUCAGCUUGACACAGGUUUGGAGUAUGCAAACAGCUAUAAUUUUGCAAAAAAGGAAAAUAACUCUCCUGAACAUCUAAAAGAUGAAGUUUCUAUCAUCCAAAGUAUGGGCUACAGAAACCGUGCCAAAAGACUUCUACAGAGUGAACCCGAAAAUCCUUCCUUGGAAACCAGUCUCAGUGUCCAACUCUCUAACCUUGGAACUGUGAGAACUCUGAGGACAAAGCAGCGGAUACAACCUCAAAAGACGUCUGUCUACAUUGAAUUGGGAUCUGAUUCUUCUGAAGAUACCGUUAAUAAGGCAACUUAUUGCAGUGUGGGAGAUCAAGAAUUGUUACAAAUCACCCCUCAAGGAACCAGGGAUGAAAUCAGUUUGGAUUCUGCAAAAAAGGCUGCUUGUGAAUUUUCUGAGACGGAUGUAACAAAUACUGAACAUCAUCAACCCAGUAAUAAUGAUUUGAACACCACUGAGAAGCGUGCAGCUGAGAGGCAUCCAGAAAAGUAUCAGGGUGAAGCAGCAUCUGGGUGUGAGAGUGAAACAAGCGUCUCUGAAGACUGCUCAGGGCUAUCCUCUCAGAGUGACAUUUUAACCACUCAGCAGAGGGAUACCAUGCAACAUAACCUGAUAAAGCUCCAGCAGGAAAUGGCUGAACUAGAAGCUGUGUUAGAACAGCAUGGGAGCCAGCCUUCUAACAGCUACCCUUCCAUCAUAAGUGACUCUUCUGCCCUUGAGGACCUGCGAAAUCCAGAACAAAGCACAUCAGAAAAAGCAGUAUUAACUUCACAGAAAAGUAGUGAAUACCCUAUAAGCCAGAAUCCAGAAGGCCUUUCUGCUGACAAGUUUGAGGUGUCUGCAGAUAGUUCUACCAGUAAAAAUAAAGAACCAGGAGUGGAAAGGUCAUCCCCUUCUAAAUGCCCAUCAUUAGAUGAUAGGUGGUACAUGCACAGUUGCUCUGGGAGUCUUCAGAAUAGAAACUACCCAUCUCAAGAGGAGCUCAUUAAGGUUGUUGAUGUGGAGGAGCAACAGCUGGAAGAGUCUGGGCCACACGAUUUGACGGAAACAUCUUACUUGCCAAGGCAAGAUCUAGAGGGAACCCCUUACCUGGAAUCUGGAAUCAGCCUCUUCUCUGAUGACCCUGAAUCUGAUCCUUCUGAAGACAGAGCCCCAGAGUCAGCUCGUGUUGGCAACAUACCAUCUUCAACCUCUGCAUUGAAAGUUCCCCAAUUGAAAGUUGCAGAAUCUGCCCAGAGUCCAGCUGCUGCUCAUACUACUGAUACUGCUGGGUAUAAUGCAAUGGAAGAAAGUGUGAGCAGGGAGAAGCCAGAAUUGACAGCUUCAACAGAAAGGGUCAACAAAAGAAUGUCCAUGGUGGUGUCUGGCCUGACCCCAGAAGAAUUUAUGCUCGUGUACAAGUUUGCCAGAAAACACCACAUCACUUUAACUAAUCUAAUUACUGAAGAGACUACUCAUGUUGUUAUGAAAACAGAUGCUGAGUUUGUGUGUGAACGGACACUGAAAUAUUUUCUAGGAAUUGCGGGAGGAAAAUGGGUAGUUAGCUAUUUCUGGGUGACCCAGUCUAUUAAAGAAAGAAAAAUGCUGAAUGAGCAUGAUUUUGAAGUCAGAGGAGAUGUGGUCAAUGGAAGAAACCACCAAGGUCCAAAGCGAGCAAGAGAAUCCCAGGACAGAAAGAUCUUCAGGGGGCUAGAAAUCUGUUGCUAUGGGCCCUUCACCAACAUGCCCACAGAUCAACUGGAAUGGAUGGUACAGCUGUGUGGUGCUUCUGUGGUGAAGGAGCUUUCAUCAUUCACCCUUGGCACAGGUGUCCACCCAAUUGUGGUUGUGCAGCCAGAUGCCUGGACAGAGGACAAUGGCUUCCAUGCAAUUGGGCAGAUGUGUGAGGCACCUGUGGUGACCCGAGAGUGGGUGUUGGACAGUGUAGCACUCUACCAGUGCCAGGAGCUGGACACCUACCUGAUACCCCAGAUCCCCCACAGCCACUACUGAAUGGAUUUAUCUGCUCUUCGCGUUGAAGAAGUACAAAAUGUCAUUAAUGCUAUGCAGAAAAUCUUAGAGUGUCCCAUCUGUCUGGAGUUGAUCAAGGAACCUGUCUCCACAAAGUGUGACCACAUAUUUUGCAAGAGCCUACAAGAAAGUACGAGAUUUAGUCAACUUGUUGAAGAGCUAUUGAAAAUCAUUUGUGCUUUUCAGCUUGACACAGGUUUGGAGUAUGCAAACAGCUAUAAUUUUGCAAAAAAGGAAAAUAACUCUCCUGAACAUCUAAAAGAUGAAGUUUCUAUCAUCCAAAGUAUGGGCUACAGAAACCGUGCCAAAAGACUUCUACAGAGUGAACCCGAAAAUCCUUCCUUGGAAACCAGUCUCAGUGUCCAACUCUCUAACCUUGGAACUGUGAGAACUCUGAGGACAAAGCAGCGGAUACAACCUCAAAAGACGUCUGUCUACAUUGAAUUGGCUGCUUGUGAAUUUUCUGAGACGGAUGUAACAAAUACUGAACAUCAUCAACCCAGUAAUAAUGAUUUGAACACCACUGAGAAGCGUGCAGCUGAGAGGCAUCCAGAAAAGUAUCAGGGUGAAGCAGCAUCUGGGUGUGAGAGUGAAACAAGCGUCUCUGAAGACUGCUCAGGGCUAUCCUCUCAGAGUGACAUUUUAACCACUCAGCAGAGGGAUACCAUGCAACAUAACCUGAUAAAGCUCCAGCAGGAAAUGGCUGAACUAGAAGCUGUGUUAGAACAGCAUGGGAGCCAGCCUUCUAACAGCUACCCUUCCAUCAUAAGUGACUCUUCUGCCCUUGAGGACCUGCGAAAUCCAGAACAAAGCACAUCAGAAAAAGCAGUAUUAACUUCACAGAAAAGUAGUGAAUACCCUAUAAGCCAGAAUCCAGAAGGCCUUUCUGCUGACAAGUUUGAGGUGUCUGCAGAUAGUUCUACCAGUAAAAAUAAAGAACCAGGAGUGGAAAGGUCAUCCCCUUCUAAAUGCCCAUCAUUAGAUGAUAGGUGGUACAUGCACAGUUGCUCUGGGAGUCUUCAGAAUAGAAACUACCCAUCUCAAGAGGAGCUCAUUAAGGUUGUUGAUGUGGAGGAGCAACAGCUGGAAGAGUCUGGGCCACACGAUUUGACGGAAACAUCUUACUUGCCAAGGCAAGAUCUAGAGGGAACCCCUUACCUGGAAUCUGGAAUCAGCCUCUUCUCUGAUGACCCUGAAUCUGAUCCUUCUGAAGACAGAGCCCCAGAGUCAGCUCGUGUUGGCAACAUACCAUCUUCAACCUCUGCAUUGAAAGUUCCCCAAUUGAAAGUUGCAGAAUCUGCCCAGAGUCCAGCUGCUGCUCAUACUACUGAUACUGCUGGGUAUAAUGCAAUGGAAGAAAGUGUGAGCAGGGAGAAGCCAGAAUUGACAGCUUCAACAGAAAGGGUCAACAAAAGAAUGUCCAUGGUGGUGUCUGGCCUGACCCCAGAAGAAUUUAUGCUCGUGUACAAGUUUGCCAGAAAACACCACAUCACUUUAACUAAUCUAAUUACUGAAGAGACUACUCAUGUUGUUAUGAAAACAGAUGCUGAGUUUGUGUGUGAACGGACACUGAAAUAUUUUCUAGGAAUUGCGGGAGGAAAAUGGGUAGUUAGCUAUUUCUGGGUGACCCAGUCUAUUAAAGAAAGAAAAAUGCUGAAUGAGCAUGAUUUUGAAGUCAGAGGAGAUGUGGUCAAUGGAAGAAACCACCAAGGUCCAAAGCGAGCAAGAGAAUCCCAGGACAGAAAGAUCUUCAGGGGGCUAGAAAUCUGUUGCUAUGGGCCCUUCACCAACAUGCCCACAGAUCAACUGGAAUGGAUGGUACAGCUGUGUGGUGCUUCUGUGGUGAAGGAGCUUUCAUCAUUCACCCUUGGCACAGGUGUCCACCCAAUUGUGGUUGUGCAGCCAGAUGCCUGGACAGAGGACAAUGGCUUCCAUGCAAUUGGGCAGAUGUGUGAGGCACCUGUGGUGACCCGAGAGUGGGUGUUGGACAGUGUAGCACUCUACCAGUGCCAGGAGCUGGACACCUACCUGAUACCCCAGAUCCCCCACAGCCACUACUGA


# Translating RNA into Protein

```python
# Prompt the user to enter the input RNA file name

input_file_name = input("Enter the name of the input RNA file:")
```

    Enter the name of the input RNA file: BRCA1_RNA.txt



```python
# Open the input RNA file and read the RNA sequence

with open(input_file_name, "r") as input_file:
    rna_sequence = input_file.read().strip()
```


```python
# Define the codon table

codon_table = { 
    "UUU": "F", "UUC": "F", "UUA": "L", "UUG": "L",
    "CUU": "L", "CUC": "L", "CUA": "L", "CUG": "L",
    "AUU": "I", "AUC": "I", "AUA": "I", "AUG": "M",
    "GUU": "V", "GUC": "V", "GUA": "V", "GUG": "V",
    "UCU": "S", "UCC": "S", "UCA": "S", "UCG": "S",
    "CCU": "P", "CCC": "P", "CCA": "P", "CCG": "P",
    "ACU": "T", "ACC": "T", "ACA": "T", "ACG": "T",
    "GCU": "A", "GCC": "A", "GCA": "A", "GCG": "A",
    "UAU": "Y", "UAC": "Y", "UAA": "*", "UAG": "*",
    "CAU": "H", "CAC": "H", "CAA": "Q", "CAG": "Q",
    "AAU": "N", "AAC": "N", "AAA": "K", "AAG": "K",
    "GAU": "D", "GAC": "D", "GAA": "E", "GAG": "E",
    "UGU": "C", "UGC": "C", "UGA": "*", "UGG": "W",
    "CGU": "R", "CGC": "R", "CGA": "R", "CGG": "R",
    "AGU": "S", "AGC": "S", "AGA": "R", "AGG": "R",
    "GGU": "G", "GGC": "G", "GGA": "G", "GGG": "G"
}
```


```python
# Translate RNA to protein

protein_sequence = " "
for i in range(0, len(rna_sequence), 3):
    codon = rna_sequence[i:i+3]
    if len(codon) == 3:
        amino_acid = codon_table[codon]
        if amino_acid == "*":
            break
        protein_sequence += amino_acid
```


```python
# Prompt the user to enter the output file name

output_file_name = input("Enter the name of the output file: ")
```

    Enter the name of the output file:  BRCA1_gene.txt



```python
# Save the gene sequence to a text file

with open(output_file_name, "w") as output_file:
    output_file.write(protein_sequence)
    print(f"The protein sequence has been saved to {output_file_name}")
```

    The protein sequence has been saved to BRCA1_gene.txt



```python
print(protein_sequence)
```

     MDLSALRVEEVQNVINAMQKILECPIWSLQESTRFSQLVEELLKIICAFQLDTGLEYANSYNFAKKENNSPEHLKDEVSIIQSMGYRNRAKRLLQSEPENPSLETSLSVQLSNLGTVRTLRTKQRIQPQKTSVYIELGSDSSEDTVNKATYCSVGDQELLQITPQGTRDEISLDSAKKAACEFSETDVTNTEHHQPSNNDLNTTEKRAAERHPEKYQGEAASGCESETSVSEDCSGLSSQSDILTTQQRDTMQHNLIKLQQEMAELEAVLEQHGSQPSNSYPSIISDSSALEDLRNPEQSTSEKAVLTSQKSSEYPISQNPEGLSADKFEVSADSSTSKNKEPGVERSSPSKCPSLDDRWYMHSCSGSLQNRNYPSQEELIKVVDVEEQQLEESGPHDLTETSYLPRQDLEGTPYLESGISLFSDDPESDPSEDRAPESARVGNIPSSTSALKVPQLKVAESAQSPAAAHTTDTAGYNAMEESVSREKPELTASTERVNKRMSMVVSGLTPEEFMLVYKFARKHHITLTNLITEETTHVVMKTDAEFVCERTLKYFLGIAGGKWVVSYFWVTQSIKERKMLNEHDFEVRGDVVNGRNHQGPKRARESQDRKIFRGLEICCYGPFTNMPTDQLEWMVQLCGASVVKELSSFTLGTGVHPIVVVQPDAWTEDNGFHAIGQMCEAPVVTREWVLDSVALYQCQELDTYLIPQIPHSHY


