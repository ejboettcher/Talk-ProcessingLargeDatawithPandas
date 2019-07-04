

# Processing Large Data with Pandas

### By Evelyn J. Boettcher

#### DiDacTex, LLC
-----------------------------------------------------------------------
## Motivation
Data sets can get large quickly.  You can quickly go from looking at a few 100 lines and a handful of columns to a million lines and hundred of columns.  

Luckily, we live in a time where most people have laptops processing power that would have been the engineers who put a man on the moon swoon and/or would have thought to be impossible to make.

<br/>
### But, you say,
####"My data is BIG data, so I neeeedddd a better computer."
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
####Only equipment needed to measure speed of light
<br/>
-------
## Measuring the Speed of Light

This required LOTS of observations over years and years by multiple people.  

Since Romer was not trying to calculate the speed of light at the time, but when Io would have an ellipse, he must have had to recalculate he calculations over and over again by hand to ensure there was not a mistake in the math or observations.
-----------------------------------------------------------------------
## Brief (and Subset) of History of Large data cont..
So we have it a bit easier, <br/>when we only having to deal with:

* NaNs
* Slow downloads

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

## Categories
That works great for numbers, but what do you do when you have strings.

~~~Python
string_list = ['Hello', 'World', 'More Strings', 'Evelyn','Boettcher']

~~~


SWITCH to
### categories
<br/>
Many times strings data will be repetitive like days of week.

~~~Python
val_days = ['Monday', 'Tuesday','Monday', 'Wednesday','Monday', 'Thursday', 'Friday', 'Saturday','Monday','Monday', 'Sunday']
~~~
-------------------------------------------------------------------
# Outline
### In this tutorial, we will:

* Learn how Python uses memory with Pandas
* How to reduce the Pandas' dataframe memory footprint.
* Learn what data types are
* Speed up reading in csv files by using categories
* Reduce the memory footprint by 90%
-------------------------------------------------------------------
## Why

(sans overhead)

|memory usage|	int|	uint| float | 	bool|	complex|
|:---:|:----|:----|:----|:----|:----:----|
|1 bytes|		int8 (-128-127)|	uint8 (0-255)||bool| |
|2 bytes|	int16	 (-32768 to 32767)|uint16 (0 to 65535)|float16 (Half precision)	| |			   |
|4 bytes|		int32|	uint32 |	float32 (Single precision)|	|   |
|8 bytes	|	int64	|uint64|float64| |  complex64 (rep. by 2 32-bit floats) |
-------------------------------------------------------------------

## How does categories work?
![Python Categories](./images/numpy_vs_python.png)

Pandas category type uses integer values to map to the raw values in a column.  This mapping is useful whenever a column contains a limited set of values.

So instead of writing "Sunday","Sunday","Sunday"... Pandas says "Sunday = 1" and the df =[1,1,1].

To convert a column to the category dtype.

```Python
df['column name'].astype('category')
```

![SundaySunday df](./images/SundaySunday.png)

## Large Data: Numbers

```bash
python int_floats_cats.py
```

### Reduced Frequency of Numbers in DF
Let's try it again but reduce the frequency (e.g. Numbers repeat less) by increasing r to 240.


```bash
python int_floats_cats.py -r 240
```

### Increase SIZE

```bash
python int_floats_cats.py -r 7 -n 1000000
```

## Large Data: strings

So lets see how we can reduce size of STRINGS arrays.
If you have a column of strings that repeats, says days of week, states etc, then you may save memory if you switch to columns


```bash
python strings_cat.py
```


```bash
python strings_cat.py -n 1000000
```
NOTE: When we have a random string of characters of length 4
  (e.g. 26 x 26 x 26 x 26 = 456,976) over 1/2 of the strings should repeat!


## SAVE DF  as `csv`

```bash
python strings_cat.py -n 1000000 -s 1 -r 20
```


## Read `csv` via category

First without using categories
```bash
python read_awesome.py

```

Now with categories
```bash
python read_awesome.py -c 1
```

# Reference
* https://www.dataquest.io/blog/pandas-big-data/
* https://pandas.pydata.org/
* https://jakevdp.github.io/PythonDataScienceHandbook/02.01-understanding-data-types.html
