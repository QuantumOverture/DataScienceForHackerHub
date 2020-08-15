# Jumping into the deep end of **"Data Science"**
##### By: Mohammad Ismail Daud 
***

## What this guide is
> A super basic overview of data science techniques. I am in no way a seasoned expert. I am just sharing my experience overall. There might many mistakes in this guide(iy uo notice any please setup a pull request) ,so use this guide as more of an outline rather than a textbook. I will try to link to other resources that will go more in depth with regards to certain topics that I will discuss.

## Table of contents:
1. Webscraping with Python(Week#1)
2. Analysis with R (Week#2) - W.I.P
***
# ***Webscraping with Python(Week#1)***

## What are we going to do and what is web scraping?
> The internet has a lot of data. Like a lot. What would you rather do: go through hundreds of pages of a website to get price data for houses in your city or run a script to do that work for you. Webscraping is just that! A script that asks and "cleans" data from a website(s). Okay now what? I have data. Big whoop. 

## Analysis
> Certain algorthims that can predict a lot of useful things (like machine learning algos) require a lot of data to be super effective. Companies pay big bucks for this. Imagine this: Coke wants to find what type of people acutally buy their products so they can market their products more effectively. They can get "trace" data from transactions or other means and run a unsupervised machine learning algorithm to segment their market audience for them! 

## Cool! But where do I start?
> With the data of course(after you have formulated a problem and road map/plan)! Websites are one source of data. Telcomm data, sensor data and other sources exist as well: ripe for the taking(please don't steal data though https://towardsdatascience.com/scraping-the-internets-most-popular-websites-a4c6f0be382d)! 

## Get to the point ya foo'
> Okay, okay...  So we are going to pratice getting data from a website. We are going find the names of the books on this fictional e-commerce website. Before that though: know that the web works by clients(user computer) asking for info/html/css/etc. from company coumputers(servers).
Run this code here: https://repl.it/@IsmailDaud/BookStoreScrape#main.py
```
# A library that will help us make "requests" to our target website.
import requests
# A library that will help us parse our html we get form the website
from bs4 import BeautifulSoup

# The website in question
URL = "http://books.toscrape.com/"

# Ask the website for the html that is given to clients and put in textual form
BookStorePage = requests.get(URL)
BookStorePageHTML = BookStorePage.text

# Use the beautfil soup library to find all the <h3> tags 
BSoup = BeautifulSoup(BookStorePageHTML, features="html5lib")
BookNames = BSoup.find_all(['h3'])

# Go through each <h3> tag in the list and extract the title attributes of the <a> things that are nested in them
# We add some additional formating at the end to correctly format as a csv
BookNameList = []
for i in BookNames:
  BookNameList.append((i.find("a").get("title")).replace(",","")+",\n")


# Open/create a file and shove our data into it
BookFile = open("./BookNames.csv","w")
BookFile.writelines(BookNameList)
BookFile.close()



# Sources Used:
#https://www.practicepython.org/exercise/2014/06/06/17-decode-a-web-page.html
# https://stackoverflow.com/questions/56478652/scraping-text-in-h3-and-p-tags-using-beautifulsoup-python
```
# Now what?
Well that is how we prep our web data for analysis! We ask the web server for data and clean it up. We put it into a format/storage method that is suitable to our needs(like a csv file if wanted to open it up in Excel or Google Sheets). Then we read in the stored info and analyze it with different statistical methods to predict future trends or find patterns! In real life applications, we would have a lot more data and more formating/cleaning would have to be done.

# Next week
We will use a csv data set to make different predictions in R!
