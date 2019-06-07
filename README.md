# Repository-1
# For class


"""
************************************************************************
	Aaron Edwards
	Date: June 7, 2019
	Programming Assignment 10: Add Custom Functionality of Your Own Choice 

	DESCRIPTION OF ASSIGNMENT: Build off of lesson 8, I have decided to 
	attempt option A, which is focused on building a pie chart of the 
	value distribution of different stocks in the portfolio via graphing
	library.
	
    In addition, will have to To receive full credit, post this 
    assignment's code on GitHub and provide information to instructor 
    necessary to access it.

************************************************************************
"""

import json
import matplotlib.pyplot as plt

# Dictionary / keys - company name and value list of dates & dates
dates = {}
prices = {}  

# Populating dictionaries and lists from json file for graph
with open('allStocks.json') as json_file:
    allStocks = json.load(json_file)
    for stock in allStocks:
        if stock['Symbol'] in prices:
            dates[stock['Symbol']].append(stock['Date'])
            prices[stock['Symbol']].append(stock['Close'])
        else:
            listPrices = []
            listPrices.append(stock['Close'])
            prices[stock['Symbol']] = listPrices
            listDates = []
            listDates.append(stock['Date'])
            dates[stock['Symbol']] = listDates

# extract company symbol in list
companies = []
for price in prices:
    companies.append(price)

# extract sum of stocks by company
priceSum = []
i = 0.0
for price in prices:
    for tmpPrice in prices[price]:
        i = i + tmpPrice
    priceSum.append(i)
    i = 0.0

totalSum = 0
for p in priceSum:
    totalSum = totalSum + p

patches, texts = plt.pie(priceSum, startangle=90)
plt.legend(labels=['%s, %3.2f %%' % (l, (s/totalSum)*100)
                   for l, s in zip(companies, priceSum)], loc="best")
plt.axis('equal')
plt.tight_layout()
# plt.show()
plt.savefig('pieChart.png')


































