

# Processing Large Data with Pandas

### By Evelyn J. Boettcher

#### DiDacTex, LLC
-----------------------------------------------------------------------
## Motivation
Data sets can get large quickly.  You can quickly go from looking at a few 100 lines and a handful of columns to a million lines and hundred of columns.  

Luckily, we live in a time where most people have laptops processing power that would have been the engineers who put a man on the moon swoon and/or would have thought to be impossible to make.

<br/>

### But, you say,

#### "My data is BIG data, so I neeeedddd a better computer."

-----------------------------------------------------------------------

## Brief (and Subset) of History of Large data

As soon as there has been paper<br/> there has been large data sets.

For example, in the 1600 Johannes Kepler used Tycho Brahe large data set on planet observations to prove how planets orbit the sun.  

Unfortunately, he had to wait until Tycho Brahe died before he could get a hold of a large data set.  

Some even thought he played a hand in Brahe's death

-----------------------------------------------------------------------
## Brief (and Subset) of History of Large data cont.
And in 1676 Ole Roemer (Rømer) armed with only paper, pencil, telescope and wind up watch (which was not even good enough to navigate a ship with) calculated the speed of LIGHT within 30% by looking at Jupiter's moon Io.  
 ![telescope](./images/telescope.jpeg)![watch](./images/watch.jpg)![pen](./images/pen.jpeg)
 <br/>
#### Only equipment needed to measure speed of light
<br/>

-------
## Measuring the Speed of Light

This required LOTS of observations over years and years by multiple people.  

Since Romer was not trying to calculate the speed of light at the time, but when Io would have an eclipse, he must have had to recalculate he calculations over and over again by hand to ensure there was not a mistake in the math or observations.

-----------------------------------------------------------------------

## Brief (and Subset) of History of Large data cont..

So we have it a bit easier, <br/> we only having to deal with:

* NaNs
* Slow downloads speeds


<br/>
### But, you say,
#### "My data is BIG and I want an answer today and not wait a decade."


### Lets talk about the Python library Pandas.

-----------------------------------------------------------------------
## Python Pandas
Python's Pandas is a high performance, easy to use library for analyzing structured data: csv files, SQLite etc.

Pandas is fast, powerful and flexible.   It enables you to quickly parse data. But it is mainly designed to handle ~<100mb.  

There are other tools like Spark to handle LARGE data sets (100 gigabytes to terabytes), but...
#### Pandas does an amazing job at cleaning messy / real data.

-----------------------------------------------------------------------

## How does one handle Large data with Pandas
When you have a gigabyte of real world data <br/>
and  you want to:

* Explore it
* Use your laptop and
* You don't want to switch to Spark.  

<br/>
### First step
Use old programming tricks like **set numbers to int8, floats16 to float32 etc** to reduce the memory size of your dataframe.  

-------------------------------------------------------------------

## Second Step: Use Categories
For numbers, try Int8, floats16 etc, but when you have strings that repeat
SWITCH to
### categories
<br/>

### List of String Examples
#### Non repeating strings

```Python
string_list = ['Hello', 'World', 'More Strings', 'Evelyn','Boettcher']
```
<br/>


#### Repeating String
Many times strings data will be repetitive like days of week.

```Python
val_days = ['Monday', 'Tuesday','Monday', 'Wednesday','Monday', 'Thursday', 'Friday', 'Saturday','Monday','Monday', 'Sunday']
```

-------------------------------------------------------------------
# Outline
### In this tutorial, we will:

* Learn how Python uses memory with Pandas
* How to reduce the Pandas' dataframe memory footprint.
* Learn what data types are
* Speed up reading in csv files by using categories
* Reduce the memory footprint by 90%
-------------------------------------------------------------------
## Data Memory footprint

(sans overhead)
#### Numbers

|memory usage|	int|	uint| float | 	bool|	complex|
|:---:|:----|:----|:----|:----|:----:----|
|1 bytes|		int8 (-128-127)|	uint8 (0-255)||bool| |
|2 bytes|	int16	 (-32768 to 32767)|uint16 (0 to 65535)|float16 (Half precision)	| |			   |
|4 bytes|		int32|	uint32 |	float32 (Single precision)|	|   |
|8 bytes	|	int64	|uint64|float64| |  complex64 (rep. by 2 32-bit floats) |

#### Strings
Python uses three kinds of internal representations for Unicode strings:

* 1 byte per char (Latin-1 encoding)
* 2 bytes per char (UCS-2 encoding)
* 4 bytes per char (UCS-4 encoding)
-------------------------------------------------------------------



## How does categories work?

Pandas category type uses integer values to map to the raw values in a column.  
<br/>
This mapping is useful whenever a column contains a limited set of values.

So instead of writing
#### df.mydays = ["Sunday", "Sunday", "Sunday"]
<br/>
Pandas categories says

#### Sunday = 1
 and the dataframe in memory is now
#### df.mydays =[1,1,1]

-------
## How does categories work?
![Python Categories](./images/numpy_vs_python.png)

-------------------------------------------------------------------

## Convert to Categories
To convert a column to the category we set the data type (dtype).

```Python
df['column name'].astype('category')
```

![SundaySunday df](./images/SundaySunday.png)
<br/>
### But wait..
Converting to categories is not always helpful.
<br/>
The following examples will show the power and pitfalls of categories


-------------------------------------------------------------------

## Interactive Part
### Large Data: Numbers

In terminal, where this tutorial has been downloaded, type the following
```bash
python int_floats_cats.py
```
<br/>
```bash
Building three DF with:
     range of numbers 1- 4
     length of DF  10000
Top 10 rows of data
   INT  INT8     FLOAT
1    2     4  3.329446
2    2     4  1.478631
3    2     3  1.338759
4    3     1  1.846993
5    1     2  2.787727
6    4     3  1.116634
7    1     2  1.064875
8    3     3  3.146007
9    3     2  2.201730
Getting size of the DF we just made
INT    0.0764MB
INT8   0.0096MB
FLOAT  0.0764MB
____________________
Now lets make them into categories
INT  df (plain df, category, SAVINGS)---> 0.0764MB , 0.0098MB , 87 %
INT8 df (plain df, category, SAVINGS)---> 0.0096MB , 0.0098MB , -2 %
___NOTE______NOTE______NOTE______NOTE___
Categories reduced the size INT df!!
   BUT because of the overhead
   it did not reduce the int8 size

Now, lets try this with random Floats
Float         --->  0.0764MB
Float category--->  0.4079MB
Categories only made the DF memory use worse

.
```

---------

### Reduced Frequency of Numbers in DF
Let's try it again but reduce the frequency (e.g. Numbers repeat less) by increasing the range of number from r = 4 to r = 240.


```bash
python int_floats_cats.py -r 240
```

```Bash
Building three DF with:
     range of numbers 1- 240
     length of DF  10000
Top 10 rows of data
   INT  INT8       FLOAT
1   12   100  235.429842
2   19    63  225.656414
3   13    20  173.416396
4   49   -60   36.324557
5  147  -100   42.525923
6   82    63   15.278578
7   15   121  202.143259
8   44   -43  225.630105
9  211   103  179.905616
Getting size of the DF we just made
INT    0.0764MB
INT8   0.0096MB
FLOAT  0.0764MB
____________________
Now lets make them into categories
INT  df (plain df, category, SAVINGS)---> 0.0764MB , 0.0307MB , 59 %
INT8 df (plain df, category, SAVINGS)---> 0.0096MB , 0.0307MB , -219 %
___NOTE______NOTE______NOTE______NOTE___
Categories reduced the size INT df!!
   BUT because of the overhead
   it did not reduce the int8 size

Now, lets try this with random Floats
Float         --->  0.0764MB
Float category--->  0.4079MB
Categories only made the DF memory use worse
```

---------
## Large Data: Numbers cont..
### Increase SIZE

```bash
python int_floats_cats.py -r 4 -n 1000000
```

```Bash
Building three DF with:
     range of numbers 1- 4
     length of DF  1000000
Top 10 rows of data
   INT  INT8     FLOAT
1    2     2  2.684429
2    2     4  1.696423
3    1     2  2.607256
4    3     1  1.247054
5    4     3  2.413925
6    2     3  3.141839
7    1     1  3.438698
8    2     2  3.584329
9    1     3  1.019402
Getting size of the DF we just made
INT    7.6295MB
INT8   0.9538MB
FLOAT  7.6295MB
____________________
Now lets make them into categories
INT  df (plain df, category, SAVINGS)---> 7.6295MB , 0.9539MB , 87 %
INT8 df (plain df, category, SAVINGS)---> 0.9538MB , 0.9539MB , 0 %
___NOTE______NOTE______NOTE______NOTE___
Categories reduced the size INT df!!
   BUT because of the overhead
   it did not reduce the int8 size

Now, lets try this with random Floats
Float         --->  7.6295MB
Float category--->  51.4442MB
Categories only made the DF memory use worse

```

-------------------------------------------------------------------
## Large Data: strings

So lets see how we can reduce size of STRINGS arrays.
If you have a column of strings that repeats, says days of week, states etc, then you may save memory if you switch to columns


```bash
python strings_cat.py
```

```Bash
Building three DF with:
     length of random string in a row 1- 4
     length of DF  10000
Top 10 rows of data
        Days  HELLO      Locations     Days_c HELLO_c    Locations_c Random_String
1    Tuesday  World    Beavercreek    Tuesday   World    Beavercreek          xhka
2  Wednesday  Hello        Oakwood  Wednesday   Hello        Oakwood          wiwh
3   Thursday  World      Fairfield   Thursday   World      Fairfield          gahf
4     Friday  Hello  Huber Heights     Friday   Hello  Huber Heights          ldou
5   Saturday  World      Riverdale   Saturday   World      Riverdale          rynl
6     Sunday  Hello         Dayton     Sunday   Hello         Dayton          oasv
7     Monday  World    Beavercreek     Monday   World    Beavercreek          nuym
8    Tuesday  Hello        Oakwood    Tuesday   Hello        Oakwood          gjvs
9  Wednesday  World      Fairfield  Wednesday   World      Fairfield          nmwn
Getting size of the DF we just made
String NO Categories      2.6724MB
String WITH Categories    0.0306MB
Random String (1 column)  0.5818MB
____________________
Now lets make them all into categories
String Columns: HELLO, Locations, Days
NO CAT to category (plain df, category, SAVINGS)---> 2.6724MB , 0.0306MB , 98 %
Cat df to category (plain df, category, SAVINGS)---> 0.0306MB , 0.0306MB , 0 %
___NOTE______NOTE______NOTE______NOTE___

Now, lets try this with random STRINGS
String: Random         --->  0.5818MB
String: Random category--->  0.9068MB
Categories only made the DF memory use worse


```
----------
## Large Data: STRING
### Now, lets make this BIGGGG

```bash
python strings_cat.py -n 1000000 -r 4
```
#### Interesting Fact:
 When we have a random string of characters of length 4<br/>
  (e.g. 26 x 26 x 26 x 26 = 456,976) <br/>Therefor over 1/2 of the strings should repeat!
```Bash
Building three DF with:
     length of random string in a row 1- 4
     length of DF  1000000
Top 10 rows of data
        Days  HELLO      Locations     Days_c HELLO_c    Locations_c Random_String
1    Tuesday  World    Beavercreek    Tuesday   World    Beavercreek          qbzd
2  Wednesday  Hello        Oakwood  Wednesday   Hello        Oakwood          wixv
3   Thursday  World      Fairfield   Thursday   World      Fairfield          vwjs
4     Friday  Hello  Huber Heights     Friday   Hello  Huber Heights          xiiz
5   Saturday  World      Riverdale   Saturday   World      Riverdale          owon
6     Sunday  Hello         Dayton     Sunday   Hello         Dayton          jihl
7     Monday  World    Beavercreek     Monday   World    Beavercreek          xwon
8    Tuesday  Hello        Oakwood    Tuesday   Hello        Oakwood          zchj
9  Wednesday  World      Fairfield  Wednesday   World      Fairfield          hnjt
Getting size of the DF we just made
String NO Categories      267.2333MB
String WITH Categories    2.8631MB
Random String (1 column)  58.1742MB
____________________
Now lets make them all into categories
String Columns: HELLO, Locations, Days
NO CAT to category (plain df, category, SAVINGS)---> 267.2333MB , 2.8630MB , 98 %
Cat df to category (plain df, category, SAVINGS)---> 2.8631MB , 2.8631MB , 0 %
___NOTE______NOTE______NOTE______NOTE___

Now, lets try this with random STRINGS
String: Random         --->  58.1742MB
String: Random category--->  47.3977MB
____________________________________________________
WHAT.......
   There was an improvement!!!
   HOW  DID  THAT  HAPPEN????
____________________________________________________


.
```

-------------------------------------------------------------------
## Large Data: strings cont.

### SAVE DF  as `csv`

```bash
python strings_cat.py -n 10000000 -s 1 -r 6
```

This should produce a csv file called <br/>
* *My_Awesome.csv* with a size of 550.6MB and
* *My_Awesome_cat.csv* with size of 486.2

<br/>

### This may take a while.
Any questions so far?
-------------------------------------------------------------------


## Read in `My_Awesome.csv`
#### Fact: this file contains a column of random strings

First without using categories
```bash
python read_awesome.py

```

Now with categories
```bash
python read_awesome.py -c 1
```
------
## Read in `My_Awesome_cat.csv`
#### Same data but without the column of random strings

Now without the random strings
```bash
python read_awesome.py -r 0 -d Sunday
```
### With Categories!
```bash
python read_awesome.py -c 1 -r 0 -d Sunday
```
#### WOW
The data in memory is **LESS** than the file size, by almost 90%!

-------------------------------------------------------------------
## Questions?
* We created data that most *GUI* readers (Office Libre, Excel) can not read in.
* We reduced the size of data in memory to something LESS than the file size!
* Categories can be **Helpfull** or **Hurtfull** when we are dealing with large data.
   * Please use care


-------
# Reference
* https://www.dataquest.io/blog/pandas-big-data/
* https://pandas.pydata.org/
* https://jakevdp.github.io/PythonDataScienceHandbook/02.01-understanding-data-types.html
