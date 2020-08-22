# Jumping into **"Data Science"**
##### By: Mohammad Ismail Daud 
***

## What this guide is
> A super basic overview of data science techniques. I am in no way a seasoned expert. I am just sharing my experience overall. There might many mistakes in this guide(if you notice any please setup a pull request) ,so use this guide as more of an outline rather than a textbook. I will try to link to other resources that will go more in depth with regards to certain topics that I will discuss.

## Table of contents:
1. Webscraping with Python (Week#1)
2. Data Analysis with R (Week#2)
***
# ***Webscraping with Python(Week#1)***

## What are we going to do and what is web scraping?
> The internet has a lot of data. Like a lot. What would you rather do: go through hundreds of pages of a website to get price data for houses in your city or run a script to do that work for you. Webscraping is just that! A script that asks and extract useful information from a website(s). Okay now what? I have data. Big whoop. 

## Analysis
> Certain algorithms that can predict a lot of useful things (like machine learning algos) require a lot of data to be super effective. Companies pay big bucks for this. Imagine this: Coke wants to find what type of people actually buy their products so they can market their products more effectively. They can get "trace" data from transactions or other means and run an unsupervised machine learning algorithm to segment their market audience for them! 
Trace data is data that is generated as a result of a digital transaction or exchange.


## Cool! But where do I start?
> With the data of course(after you have formulated a problem and road map/plan)! Websites are one source of data. Telcomm data, sensor data and other sources exist as well: ripe for the taking. Please don't steal data though! Always look at the robot.txt before setting up a bot/script to scrape data from a page(se this article for more information: https://towardsdatascience.com/scraping-the-internets-most-popular-websites-a4c6f0be382d).  

## Get to the point ya foo'
> Okay, okay...  So we are going to practice getting data from a website. We are going find the names of the books on this fictional e-commerce website. Before that though: know that the web works by clients(users) asking for info/html/css/etc. from company coumputers(servers).
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

# Use the beautiful soup library to find all the <h3> tags 
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
# https://www.practicepython.org/exercise/2014/06/06/17-decode-a-web-page.html
# https://stackoverflow.com/questions/56478652/scraping-text-in-h3-and-p-tags-using-beautifulsoup-python
```
# Now what?
> Well that is how we prep our web data for analysis! We ask the web server for data and clean it up. We put it into a format/storage method that is suitable to our needs(like a csv file if wanted to open it up in Excel or Google Sheets). Then we read in the stored info and analyze it with different statistical methods to predict future trends or find patterns! In real life applications, we would have a lot more data and more formating/cleaning would have to be done.

# ***Data Analysis with R(Week#2)***

## What are we going to do?
> Last week we learnt how to get data from a data source(namely websites). So, we are going to use what we learnt last and use data stored in a csv file and analyze it! We are going to use the statistical language called R for today's analysis.

## What are we analyzing?
> Good question! We are going to take a look a data set that contains information about life expectancy and factors in each country that might affect it. To be more specific, we want to know if the level of education in a country can affect the citizen's life expectancy or not. And if there is a relationship : we want to be able to predict it (spooky I know).

##  Linear Regression
> We will be using a supervised machine learning algorithm know as "linear regression" to predict the life expectancy of a country's people based on the level of education. The way this algorithm works is simple: it finds "m" and "b" in y=mx + b. But why y=mx+b? That is the formula for a linear/straight line. When we say that two quantities have a linear relationship with each other we are  basically if one increases(or decreases) the other also proportionally increases(or decreases). Therefore, since we believe that the two quantities we are working with are "linearly" related we use this algorithm. 

## The code in question

```
# Read in the data
Data <- read.csv("Life Expectancy Data.csv")
# Remove any rows that have missing data
na.omit(Data)
# Make a basic line plot with x being the years of schooling and 
# y being the country's life expectancy. Also make it look good!
plot(Data$Schooling,Data$Life.expectancy
     ,ylab = "Life Expectency in Age"
     ,xlab = "Years of Schooling"
     ,main = "There is a strong positive relationship between total years of schooling and health."
     ,cex.main = 0.7
     ,pch = 20
     ,col = "skyblue")

# Run linear regression and
# superimpose the predicted line(with the calculated m and b values) on the plot.
RegressionLine <- lm( Data$Life.expectancy ~ Data$Schooling)
abline(RegressionLine,col="orange",lwd=3)

# Are they correlated?
cor(Data$Schooling,Data$Life.expectancy,use="complete.obs")


```

# The Result
![Rplot](https://i.ibb.co/Sn0kbHP/Rplot.png)

> As you can see above, we find that there is strong correlation between the years of schooling and the average life expectancy(0.75 to be exact)!  Our prediction formula is y = 2.103x + 44.1. So if you find a country with the years of schooling being 13: we can predict the life expectancy of its inhabitants to be: 71.4! Insane I know!

# Pitfalls of analysis
>  CORRELATION DOES NOT EQUAL CAUSATION! Just because two things seem to revolve around each other ,that does not mean one thing causes the other. For example: if we find that your SAT score is highly correlated with the amount of soda you drink. That does not mean that drink more or less soda will affect your score! It just shows these two things can be related to each other by some hidden variable we have accounted for. In this case, countries that have a higher level of schooling probably means they are wealthy enough to send most of their children to school for a prolonged period of time. If you have money, you can spend on better drugs and treatment. So whenever you analysis anything, be wary of the assumption you make and what you did to get to your result!
