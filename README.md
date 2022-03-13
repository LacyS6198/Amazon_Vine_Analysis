# Analysis Overview
The purpose of this analysis was to analyze video game reviews. The analysis consisted of games with 20 or more total reviews (total reviews greater than or equal to 20). 
These reviews were then further filtered to helpful reviews. Helpful reviews were determined as having a helpful vote count (out of total votes) of greater than or equal to 50%.

After filtering the data, analysis was done based on whether it was a paid (Vine = Y) or unpaid (Vine = N) review. Analysis was then performed on both of these review types. 

## Code Snippets - Data Filtering
PySpark was used for this analysis using Google Colab. 
Below are the code snippets used to filter the data.

#### Filter for games with 20 or more reviews.
```
vine_filtered_df = df.filter("total_votes>=20").select(["review_id", "star_rating", "helpful_votes", "total_votes", "vine", "verified_purchase"])
vine_filtered_df.show(5)
```

#### Filter for "helpful" reviews
```
vine_filtered_df2 = vine_filtered_df.filter("(helpful_votes/total_votes)>=.5").select(["review_id", "star_rating", "helpful_votes", "total_votes", "vine", "verified_purchase"])
vine_filtered_df2.show(5)
```

#### Create dataframes for (1) Paid and (2) Unpaid reviews
```
vine_filtered_Paid_df = vine_filtered_df2.filter("vine == 'Y'").select(["review_id", "star_rating", "helpful_votes", "total_votes", "vine", "verified_purchase"])
vine_filtered_Paid_df.show(5)
```

```
vine_filtered_Unpaid_df = vine_filtered_df2.filter("vine == 'N'").select(["review_id", "star_rating", "helpful_votes", "total_votes", "vine", "verified_purchase"])
vine_filtered_Unpaid_df.show(5)
```

# Results
Below are the results of Vine (Paid) vs non-Vine (Unpaid) reviews.

## Total Reviews by Type
 - Vine Reviews:  94
 - Non-Vine Reviews:  40471

## Total 5-Star Reviews by Type
 - Vine Reviews with 5-Stars:  48
 - Non-Vine Reviews with 5-Stars:  15663
 
 ## Percentage of 5-Star Reviews by Type
 - Percentage of Vine Reviews with 5-Stars:  51.06%
 - Percentage of Non-Vine Reviews with 5-Stars:  38.70%
 
![Vine](https://user-images.githubusercontent.com/93630042/158064121-b50e33a0-8134-474c-8efd-5d4944b7d65f.png)

![NonVine](https://user-images.githubusercontent.com/93630042/158064125-b35822f0-d562-4584-98c3-8ca49fbd3b4b.png)

# Summary
Vine/Paid reviews had a much higher percentage of 5-star reviews, indicating that these types of reviews may be biased to positive comments. 51.06% of the Vine reviews were 5-stars, compared to only 38.70% of non-Vine reviews. 
It should be noted though that there were significantly fewer Vine reviews taken into account for this analysis (94 Vine reviews vs 40,471 non-Vine reviews). 

Additional analysis could include:
 - Analyzing all stars (1 - 5) percentages to see if the positive-bias trend continues throughout the data.
 - Compare number of helpful reviews by type to determine if the Vine are as helpful as the non-Vine. The high number of Vine 5-star reviews could be due to the number of helpful votes. As a whole, there might not be any bias in the review but rather the voting of helpfulness.
