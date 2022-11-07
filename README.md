
[![Banner](https://github.com/NicolasVollmer/Etsy-Flower-Girl-Market-Analysis/blob/main/Images/banner.jpeg?raw=true "Banner")](https://github.com/NicolasVollmer/Etsy-Flower-Girl-Market-Analysis/blob/main/Images/banner.jpeg?raw=true "Banner")

# My Ironhack Bootcamp Final Project | Exploring the Flower Girl Dress Market on Etsy

## Synopsis
Welcome to my final Ironhack project submission!

In this repository, we analyze the [market for "flower girl" dresses on Etsy][flower girl link] for a client. These are formal dresses for girls to participate as flower girls at wedding ceremonies, or for wearing to any other formal occasion. Our client also sells  gowns for babies and toddlers for their baptism.

## Table of Contents
[TOCM]

## Background
My name is Nicolas Vollmer. This submission is my final project to my Ironhack Data Analytics Bootcamp. 

### My Client
I say client, but actually this is for a friend: She is a private entrepreneur from Germany who wanted to turn a hobby into a side-business for some additional income. She has a shop on Etsy, selling at the time of this writing 35 different dress styles, offering customization (size, color, design elements, etc.). She graciously agreed to participate as the subject of my data analysis, but asked to remain anonymous in any publication. Any mentions of her name or shop are therefore redacted in this repository.

### Why this Market?
In my search for an interesting final project to showcase my skills which I harnessed during the Ironhack Data Analytics bootcam, I found the flower girl dress market to be a wholesome and cute topic idea! It deals with a real-life market and attempts to find insight and recommendations to add value to my aforementioned friend's business.

### Etsy
[Etsy][Etsy] is a leading e-commerce marketplace platform, similar to Amazon.com, but specialized on (mostly) handmade goods. It offers a way for small entrepreneurs and hobbyists to sell their goods to a wider audience.

## Process
This is a competitive analysis first and foremost. We have received some firsthand data from the client but our main effort was directed at scraping flower girl dress listings from the Etsy platform. For this, we have used BeautifulSoup on Python to automate the listing by listing scrape process in two steps:

### Step 1
We ran multiple searches for "flower girl dress" and "christening gown" on Etsy and programmed a web parser in Python using Beautiful Soup to go search page by search page and in a first step, scrape each listing's name, listing url and url to the main image of that listing. The resulting data was combined into a Pandas dataframe and then exported as a .csv for use in Step 2.

### Step 2



[Etsy]: https://www.etsy.com "Etsy"
[flower girl link]: https://www.etsy.com/search?q=flower+girl+dress&explicit=1&order=highest_reviews&page=1&ref=pagination "market for "flower girl" dresses on Etsy"