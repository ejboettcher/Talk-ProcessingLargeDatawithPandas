

# Motivation
Data sets can get large quickly.  
You can quickly go from looking at a few 100 lines and a handful of columns to a million lines and hundred of columns.  

Python Pandas with smart use of Categories can enable on to reduce the size of your data in memory by up to 90%.

This repository contains a tutorial and supporting scripts to show case the power of python pandas with categories.  

The tutorial located in the file called:
* *slides.md*

## Tutorial Hosted on a Webserver

The tutorial is hosted here

* [Link to talk](https://didactexgit.github.io/Talk-ProcessingLargeDatawithPandas/)


## Outline
In this tutorial, we will:
* Learn how Python uses memory with Pandas
* How to reduce the Pandas' dataframe memory footprint.
* Learn what data types are
* Speed up reading in csv files by using categories
* Reduce the memory footprint by 90%


### In a nut shell

Instead of writing "Sunday","Sunday","Sunday"... Pandas with **categories** says

"Sunday = 1" and the df =[1,1,1].

uint8 "1" takes a lot less memory than "Sunday"

To convert a column to the category you change the  dtype via the follow command.

```Python
df['column name'].astype('category')
```

![SundaySunday df](./images/SundaySunday.png)

## Slide Deck
The tutorial can be run locally as an html slide deck.
Assuming Python3. To activate the html you need to first set up a server in the main directory.  This can be done via python.

```python
python -m  http.server
```

Then open a browser and type the following url
[http://localhost:8000](http://localhost:8000)

# Reference
* https://www.dataquest.io/blog/pandas-big-data/
* https://pandas.pydata.org/
* https://jakevdp.github.io/PythonDataScienceHandbook/02.01-understanding-data-types.html
