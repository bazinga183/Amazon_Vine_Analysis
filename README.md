# Amazon_Vine_Analysis

## Overview of the Analysis 

The purpose of this project was to choose from about 50 datasets in Amazon's review database and perform the ETL process on a random dataset while utilizing the AWS RDS instance for a database. In addition, I would also have to use PySpark to determine if there was any bias from some of the reviews written in a given dataset.

To begin, I created an instance within the AWS RDS to be able to utilize its services [digital videogame reviews](https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Digital_Video_Games_v1_00.tsv.gz). 
Next, I connected the RDS to [Google Colab](https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Digital_Video_Games_v1_00.tsv.gz)
so that I could begin breaking up the data into different tables that could be uploaded into pgAdmin and I could connect these tables all together.

Once I had these tables prepared and ready to upload into pgAdmin, I used a [schema](https://github.com/bazinga183/Amazon_Vine_Analysis/blob/main/table_creation.sql) to create tables so that the loading process into pgAdmin would be fluid.

Then, I began my analysis on the dataset using PySpark.

## Results 

Here are some questions that are needed to be answered so that there is context around the conclusion:

 - How many Vine reviews and non-Vine reviews were there?
   - After filtering to reviews to see if there were more than 20 total votes, there 0 Vine reviews and 631 non-Vine reviews.


   ```
   # Filter for where total_votes is >= 20
vine_df = df.select(['review_id', 'star_rating', 'helpful_votes', 'total_votes', 'vine', 'verified_purchase'])
total_votes_df = vine_df.filter("total_votes >= 20")
total_votes_df.show()
```

 - How many Vine reviews were 5 stars? How many non-Vine reviews were 5 stars?
   - In total, there were 631 five-star reviews there were non-Vine reviews and there were 0 Vine reviews that were Vine reviews.
 - What percentage of Vine reviews were 5 stars? What percentage of non-Vine reviews were 5 stars?
   - The percentage of Vine reviews that were five stars were 0%, which means that the percentage of reviews that were non-Vine was 100%. 

## Summary 
In your summary, state if there is any positivity bias for reviews in the Vine program. Use the results of your analysis to support your statement. Then, provide one additional analysis that you could do with the dataset to support your statement.

Reviewing the results, I think that it is safe to say that there is no positivity bias because there are no Vine-reviews that are five-stars. Only non-Vine reviews make up the five-star reviews, and these are in the hundreds.
Regardless, it would be interesting to see if I excluded the filters where there are at least 20 votes on the game to see if this would impact the findings. Perhaps less votes are targeted to skew the reviews, but that would be for a future project!
