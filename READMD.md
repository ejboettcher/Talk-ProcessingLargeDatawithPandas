

# Motivation
Data sets can get large quickly.  You can quickly go from looking at a few 100 lines and a handful of columns to a million lines and hundred of columns.  

Luckily, we live in a time where most people have laptops processing power that would have been the engineers who put a man on the moon swoon and/or would have thought to be impossible to make.

But, you say my data is BIG data so I neeeedddd even better computer.

## Brief and Subset of History of Large data

As soon as there has been paper there has been large data sets. For example, in the 1600  Johannes Kepler had to wait until Tycho Brahe died before he could get a hold of a large data sets to prove how planets orbit the sun.  

And in 1676 Ole Roemer (Rømer) armed with only paper, pencil, telescope and wind up watch (which was not even good enough to navigate a ship with) calculated the speed of LIGHT within 30% by looking at Jupiter's moon Io.  

This required LOTS of observations over years and years by multiple people.  Since Romer was not trying to calculate the speed of light at the time, but when Io would have an ellipse, he must have had to recalculate he calculations over and over again by hand.

So we have it a bit easier.  With only having to deal with NaNs.

But, you say my data is BIG and I want an answer today and not wait a decade.
Lets talk about the library Pandas.

## Python pandas
Python's Pandas is a high performance, easy to use library for analyzing structured data: csv files, SQLite etc.

Pandas is fast, powerful and flexible.   It enables you to quickly parse data. But it is mainly designed to handle ~<100mb.  There are tools like Spark to handle LARGE data sets (100 gigabytes to terabytes).  Plus it does an amazing job at cleaning messy or real data.

So what do you do when you have a gigabyte of real world data that you want to explore it and don't want to switch to Spark.  

You can do old programming tricks like set integers to ints, floats to float 32 etc to reduce the memory size of your dataframe.  That works great for numbers, but what do you do when you have strings.

~~~Python
val_days = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday']

~~~

SWITCH to categories.  Many times strings data will be repetitive like days of week.


# Outline
In this tutorial, we will:
* Learn how Python uses memory with Pandas
* How to reduce the Pandas' dataframe memory footprint.
* Learn what data types are
* Speed up reading in csv files by using categories
* Reduce the memory footprint by 90%

## Why

(sans overhead)

|memory usage|	int|	uint| float | datetime|	bool|	complex|
|:---:|:----|:----|:----|:----|:----|:----|:----|
|1 bytes|		int8 (-128-127)|	uint8 (0-255)|	|	|bool| |
|2 bytes|	int16	 (-32768 to 32767)|uint16 (0 to 65535)|float16 (Half precision)	| |			|   |
|4 bytes|		int32|	uint32 |	float32 (Single precision)|	|  | |
|8 bytes	|	int64	|uint64|float64|	datetime6 | |  complex64 (rep. by 2 32-bit floats) |


## How does categories work?

## Build large array

## Create Large DF and save as csv

## Test Memory on Cat and non cat

## Read in via category


# Reference
* https://www.dataquest.io/blog/pandas-big-data/
* https://pandas.pydata.org/
* https://jakevdp.github.io/PythonDataScienceHandbook/02.01-understanding-data-types.html
