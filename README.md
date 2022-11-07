
[![Banner](https://github.com/NicolasVollmer/Etsy-Flower-Girl-Market-Analysis/blob/main/Images/banner.jpeg?raw=true "Banner")](https://github.com/NicolasVollmer/Etsy-Flower-Girl-Market-Analysis/blob/main/Images/banner.jpeg?raw=true "Banner")

# My Ironhack Bootcamp Final Project | Exploring the Flower Girl Dress Market on Etsy

## Synopsis
Welcome to my final Ironhack project submission!

In this repository, we analyze the market for "[flower girl dresses](https://www.etsy.com/search?q=flower+girl+dress&explicit=1&order=highest_reviews&page=1&ref=pagination "flower girl dresses")" on Etsy for a client. These are formal dresses for girls to participate as flower girls at wedding ceremonies, or for wearing to any other formal occasion. Our client also sells  gowns for babies and toddlers for their baptism. 

## Table of Contents

[TOC]

## Background
My name is Nicolas Vollmer. This submission is my final project to my Ironhack Data Analytics Bootcamp. I was given eight days to complete this project from start to delivery of the current version here. I do have plans to return and update this analysis in the future. More on that further below. 

### My Client
I say client, but actually this is for a friend: She is a private entrepreneur from Germany who wanted to turn a hobby into a side-business for some additional income. She has a shop on Etsy, selling at the time of this writing 35 different dress styles, offering customization (size, color, design elements, etc.). She graciously agreed to participate as the subject of my data analysis, but asked to remain anonymous in any publication. Any mentions of her name or shop are therefore redacted in this repository.

### Why this Market?
In my search for an interesting final project to showcase my skills which I harnessed during the Ironhack Data Analytics bootcamp, I found the flower girl dress market to be a wholesome, unique and cute topic idea! It deals with a real-life market and attempts to find insight and recommendations to add value to my aforementioned friend's business.

### Etsy
[Etsy](https://www.etsy.com "Etsy") is a leading e-commerce marketplace platform, similar to Amazon.com, but specialized on (mostly) handmade goods. It offers a way for small entrepreneurs and hobbyists to sell their goods to a wider audience.

## Research Questions
1. How does our client rank compared to the competition on Etsy?
2. How might we increse traffic to our client's shop?
	- I had ambitious plans for this point, to analyze listing names (which are not traditional item names like e.g. "red flower girl dress", but actually as many potential search terms bunched together as the Etsy character limit would allow for search engine optimization (SEO) - see a random example [here](https://www.etsy.com/listing/1119428952/flower-girl-dress-christmas-event-dress?click_key=7929896ff346d0596a7b9847ba4c407834572193%3A1119428952&click_sum=d7d8dfaa&ref=hp_opfy-5 "here")) for potential keywords our client may use. 
	- As a "strech goal" I had also planned to make a pallette analysis of listing images and potentially a subject matter analyis to see wheter listings had a model in them or not (our client has no models in her listing photos) and whether this negatively impacts her business by contrasting it to the overall sales numbers of shops which use models.
	- Due to problems in my data acquisition (see further below) I had to cut these plans for my initial report due date. I plan to revisit this at a later date.

3. How could we drive up sales conversion and improve our rank (within reason)? I.e. Is there something we can do about pricing or our shop terms to improve traffic and drive sales? We want to examine the impact of pricing level on overall sales, and if a higher price may still lead to success. Additionally, could implementing an open returns policy drive conversion?

By herself, in her current live situation, our client estimates a maximum sales quantity of ca. 250-300 dresses annually to be viable.

## Data Acquisition
This is a competitive analysis first and foremost. We have received some firsthand data from the client but our main effort was directed at scraping flower girl dress listings from the Etsy platform. For this, we have used BeautifulSoup on Python to automate the listing by listing scrape process in two steps:

### Step 1
We ran multiple searches for "flower girl dress" and "christening gown" on Etsy and programmed a web parser in Python using Beautiful Soup to go search page by search page and in a first step, scrape each listing's name, listing url and url to the main image of that listing. The resulting data was combined into a Pandas dataframe and then exported as a .csv for use in Step 2.

### Step 2
We trained a second web parser with Beautiful Soup to take the listing urls we scraped in step 1 and go listing by listing to scrape the necessary details. We later join these onto the step 1 data to complete the dataset. The following is scraped in step 2:

| Value Name | Description |
|:---|:---|
| shop_name | name of the Etsy shop, could be used to create a URL for those shop's listings for further scraping |
| start_price | minimum price in EUR for this listing item, prices may scale with size or extra wishes |
| size_options | size options that are offered for this dress |
| ship_cost_germany | cost in EUR to ship to any German address |
| allows_returns | yes/no on return policy (our client does not currently allow returns, as all items she sells are made-to-order bespoke) |
| shop_location | country where the shop ships from |
| shop_5_star_rating_percentage | on the site, ratings are displayed in a 5/5 star rating for the shop which offers the listed item (not for the item itself), but in the html source code one can only find the percentage of reviews which awarded a certain score, which then gets calculated into the 5/5 rating |
| shop_4_star_rating_percentage | same as above |
| shop_3_star_rating_percentage | same as above |
| shop_2_star_rating_percentage | same as above |
| shop_1_star_rating_percentage | same as above |
| shop_reviews_count | total number of reviews for the shop that offers this listing |
| item_reviews_count | total number of reviews for this indidvidual listing |
| listing_customer_reviews | up to four written customer reviews for this item |
| total_shop_sales | total number of sales made by this shop through Etsy |

### Data Collection Problems
Etsy has their own API programme, for which I had requested access at the onset of this project, but by the time of this writing two weeks later my access request is still pending approval. Having checked about this online, it seems that Etsy is not very forthcoming in handing out API access, which is why I had to resort to the more painstaking process of html parsing using Beautiful Soup.

The step1/step2 web parsers I built took several days of trial and error to construct in order to scrape each element. It should be noted here, that Etsy is not an easy website to scrape. They rely heavily on JavaScript, which Beautiful Soup cannot read reliably. Additionally, while most listings feature the same repeating elements, they are often coded differently in the html source accross different listings. Therefore, despite multiple trial and error checks, the star rating percentages where not scraped reliably across listings. I was therefore unable to utilize this metric in my current analysis.

While the underlying scraping codes were more or less completed by day three, the process did not work reliable as scraping large amounts of data, even on a small 2000 listing step 1 dataset, in step 2 takes several hours to append. Additionally, step 2 until the latest version (completed by day five) was prone to failure, losing the scraped data gathered until that point. 

Etsy relying on JavaScript meant that I had to accept severe restictions in the amount of listings I could scrape. A simple search for "flower girl dress" will give you around 60,700 search results (including ads). By default on most computers, a default results page should show 16x4 rows of listings, this should amount to ca .949 results pages! However, when reaching page 250 we cannot go further, thus opposing a limit of 16,000 listings. However, using the scraper the limit is actually just 2,000 listings, as only the first four listings of any results page are visible to Beautiful Soup while the remaining 14 rows of listings are JavaScript encoded. Additionally, there is a diminishing relevance of the search results in the latter pages. In the end, one needs to specify they are looking for "girls clothing" in the search filter in order to also cut out results like tutu pricess dresses for dogs. There is also quite a noticeable difference between my personal search results on the page vs. the ones pulled by the sraper.

## Data Analysis
With the problems I faced during data collection, I had less time to focus on data cleaning and the analyis portion of my project.

### Modeling, Findings and Suggestions
Our client's rank worldwide is 381 out of 1210 flower girl shops globally, and 27 of 98 from the German market. Rank was determined from number of sales and customer reviews. Her rank is not terrible, but there are many shops that outsell her. My client lamented her poor conversion rate, where only a few shop visitors actually end up buying anything, but it is actually not too bad at 5.9% in 2022 considering the average for Etsy shops is about 2-4%. 

Our client is offering a great deal of customisation on each dress. A suggestion is to stick to more standard sizing and styles at a competitive price point and maybe offer a stock of these with the option to return, while still retaining the option to customise colour, style elements, and fit at a higher surcharge and no return option.

Running our data through various analytical models, we received very poor results. In our main file, we tried to run linear and logistic regression, as well as KNN and an MLPregressor to see if factors like pricing and return policy have influence on shop success (total sales). 

On the one hand this may clearly suggest that these factors do not have much influence. And yes, this is a very subjective market where users pick what they like for importaint events (meaning that price may be of lesser import to these customers). Instead, to improve traffic and in return increase sales, our client should seriously consider to invest in photoshoots of her items with (real-life) models to draw more attention of shoppers. Although we were unable to confirm the hypothesis that shops using models get more sales using ML, this seems like a "no-brainer" fact.

On the other hand, our data is incomplete (not every item from relevant shops was scraped, we were unable to reliably scrape shop star ratings for use in our evaluations) and "spotty" (possible interference from irrelevant listings not related to flower girl dresses). So this may contribute to our poor model performance. Better data through improved scraping may cast a different picture. I will play around with the data further to see if I can change anything by eliminating other outliers (like no shops with no or very few sales). 

## Presentation
A requirement for completion was to create a presentation to my teaching staff and cohort. I created my presentation using Apple Keynote. Find it online for review here: https://www.icloud.com/keynote/09fb3Z31Rpscv9xFo2ko0DD3Q#Etsy_Flower_Shop_Presentation

## Future Development Ideas
I have further ideas on recoding a V2 scraper that will use Selenium to grab more listings and their respective data. Additionally, we should spend some time to go shop by shop and scrape their relevant listings where possible. More data would mean a more grounded analysis. Additionally, if we could continue to scrape data on a monthly basis, we could build up some historical data on pricing developments that would no doubt be interestig!

I will also spend more time to form a better analysis for my friend and "client", mainly by making sure I get on the keyword natural language processing analysis of listing titles to find potential keywords we could leverage in SEO. 

Ideally, I'd like to build a dashboard using Python for competitive analysis for my friend. 

I also had the idea to build a dashboard for our client’s competitor analysis that is fed on procedurally updated data snapshots. This would be a different repository in the future.
