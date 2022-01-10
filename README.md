# Estimation Income Group using Iproperty Data

## Description
There are 2 processes for this income group estimation using iproperty data. First, property data will need to be scraped from iproperty website using this notebook - [Scrape Iproperty.ipynb](https://github.com/maryamnuri/income-group-estimation-using-iproperty/blob/b86f566c72ba2e34fc4fc1ac6b97bf09688bf877/Scrape%20Iproperty.ipynb) and this scraped data will be used to map a list of users [Dummy Address Data](https://github.com/maryamnuri/income-group-estimation-using-iproperty/blob/b86f566c72ba2e34fc4fc1ac6b97bf09688bf877/Johor_Address.csv)
using lat and lon

## Data
#### 1. Johor_Address.csv
This data is a dummy address contains for 45 users with home address. All addresses are Johor residential address with latitude and longitude details extracted from Google Maps.

 #### 2. scraped_data.csv
This is the iproperty scraped data of Johor residential address for sales.
 
## Problem Statement
To estimate income group/bucket for a list of users with limited users' information related to income ie. Job, Working Class, Education, etc. 
User data only contains user ID and home location.

## Methodology
1. From Iproperty data, mean property price is calculated using the min and max property price obtained from scraped data
2. Based on mean property price, monthly repayment and household income is estimated using the following criteria/assumptions:
- 30 years tenure
- 4.5% interest rate
- 10% down payment
- 35% monthly spending on property\
_Reference: https://www.propertyguru.com.my/property-guides/are-you-earning-enough-buy-house-malaysia-20860_
3. From estimated household income, 4 income group is created using Income Range from Department of Statistics Malaysia
![image](https://user-images.githubusercontent.com/40256034/148715282-63039821-100f-4580-b66d-9f9e0119a22f.png)\
_Source: Household Income and Basic Amenities Survey Report 2019, Department of Statistics Malaysia_
4. Latitude & longitude from property data and user data is encoded to a geohash to enable mapping without calculating distance. 
5. For each users, addresses are mapped to iproperty geohash with 2 type of Geohash length; lenghth 7 and 6 ![Screenshot 2022-01-10 at 11 37 33 AM](https://user-images.githubusercontent.com/40256034/148715773-6aee086a-93b8-46ba-9016-65c590e659e7.png)


6. We will have the income group for users that can be mapped to property data
##### Note:
- By using geohash length 7, user will be mapped more accurately as the size of grid is smaller. However, only small number of users can be mapped
- Tried using geohash length 6 and more users can be mapped and tagged the income group. 
- Need to note that the trade-off is the accuracy as this method covers all users within appx. 1km grid from a particular property

## Output/Result
<img width="911" alt="Screenshot 2022-01-10 at 11 45 49 AM" src="https://user-images.githubusercontent.com/40256034/148716247-72a446ef-e161-4c6f-99a8-e867237c6400.png">


