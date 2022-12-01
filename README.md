# Amazon_Vine_Analysis

## Overview of Project
In this project, Big Data is used as well as Cloud Services, specifically Amazon's Simple Storage Service (S3). Spark will be used into to handle the big data because it allows processing and analyzing data quickly and at a massive scale. In order to work with Spark, Google Colab will be where the code is programmed since it is hosted in the cloud. This makes it easier to read datasets that are from the cloud as well.

### Tools used in project
**AWS**  
**PySprak**  
**Google Colab**  
**PostgreSQL**

## Purpose
The purpose of the project is to analyze Amazon reviews written by members of the paid Amazon Vine program. Amazon Vine members are delivered products and in return, they publish a review on the product. PySpark is used to extract the dataset, transform the data, connect to an AWS RDS instance, and load the transformed data into pgAdmin. PySpark is used again to analyze the data to determine if there is any bias toward favorable Vine member reviews.

## Results
### ETL process
Before the notebook was started, pgAdmin was connected to an AWS database in order to store the data within Amazon's S3. Tables were created so that after the data is transformed, it can be loaded onto the tables.  
The first thing that was done was installing and setting up the variables need to use Spark. Next, was downloading the Postgres driver to allow Spark to interact with Postgres. Once that was done and starting a SparkSession, the Amazon reviews were extracted and converted to the dataframe seen below.
![ETL_1](https://user-images.githubusercontent.com/109183214/204965522-92638b55-993e-4a1c-88c4-b1acc37cf61a.png)  

Once the data was extracted into dataframe are created, the data is transformed into 4 dataframes: the customers, vine reviews, review id, and the products which is shown below.
![ETL_2](https://user-images.githubusercontent.com/109183214/204965895-91506bdb-6690-46ff-a0b6-3c3ef52f518d.png)  

After the dataframe is transformed to the dataframes needed, the AWS RDS instance was connected in order to write the dataframes into thier respective table. The tables are checked to make sure the daataframes successfully loaded.  
![ETL_3](https://user-images.githubusercontent.com/109183214/204966746-de590d78-dafa-48dc-b9ea-136e56716cfb.png)

![Customers_t](https://user-images.githubusercontent.com/109183214/204964483-8c04cd7e-c6a7-4ace-8f50-3b4fc9329c08.png)
![Products_t](https://user-images.githubusercontent.com/109183214/204964486-6f686b7e-3e1c-48c0-ac99-f7d0c2fa14a0.png)
![Review_id_t](https://user-images.githubusercontent.com/109183214/204964488-78b00fc4-02d7-4f71-8895-20fe279f674b.png)
![Vine_t](https://user-images.githubusercontent.com/109183214/204964482-eb6081a2-0b28-4595-8c4a-13fd9e1edec7.png)  

### Vine review analysis
![ETL_4](https://user-images.githubusercontent.com/109183214/204972126-b7691940-caf4-4be6-ad1f-6be5dd3f184d.png)

The image above is the code used to get the count of 5 star reivews, total reviews, and the percentage of 5 star reviews compared to the total reviews. The top code was for the paid reviews (Vine) while the bottom is for unpaid reviews (Non-Vine). In order from left to right, the numbers that were printed are the  number of 5 star reivews, total reviews, and the percentage of 5 star reviews compared to the total reviews.  

* How many Vine reviews and non-Vine reviews were there?  
There were 334 Vine reviews and 61614 Non-Vine reviews
* How many Vine reviews were 5 stars? How many non-Vine reviews were 5 stars?  
There were 139 Vine reviews that got 5 stars and 32665 Non-Vine reviews that got 5 stars
* What percentage of Vine reviews were 5 stars? What percentage of non-Vine reviews were 5 stars?
For Vine reviews, the percentage of Vine reviews that were 5 stars was around 42 percent while the the percentage of Non-Vine reviews that were 5 stars was 53 percent

## Summary
After reviewing the results comparing the Vine vs. Non-Vine reviews, there is no bias for reviews in the Vine program. As seen in the images above, 42% of Vine members reviews were 5-star and 53% of Non-Vine reviews were 5-star. However, the number of Vine reviews total in comparison to Non-Vine reviews is significantly less.

In order to confirm the Non-Vine customers actually purchased the item from Amazon or that it wasn't gifted, we can also filter based on the verified_purchase column. After rerunning the calculations on this new dataframe, 68% of Non-Vine members reviews were 5-star and verified that they purchased the item.
