# 2Market-Sales-and-Customer-Data-Analysis
This was the first project I completed as part of the LSE Data Analytics Career Accelerator course (2022 - 2023), for which I achieved a mark of 88% (distinction). I used Excel, SQL, and Tableau for this project. 

**1. Project background:** 

2Market commissioned this project to better understand its customers, top products and markets by sales, and most effective advertising channels. A kick-off meeting with stakeholders revealed a loss in Q3 2022 revenue that requires immediate cost savings and increased sales. Further investigation shows this was mainly caused by US competition, ineffective marketing, unsuccessful market expansion, and decreased online sales of certain products post-COVID. This project aims to support senior management make decisions about where to focus the business and help regional marketing teams improve campaigns and identify the best advertising channels by product. Stakeholders acknowledged there was no data linking ad conversion to sales but agreed an estimation was sufficient.

**2. Analytical approach:**  

The Marketing_data and Ad_data files were viewed as text to see delimiters and check for any unusual data.
 
Data cleaning:

•	A spellcheck and search for blank cells was conducted – no issues detected. 

•	Conditional Formatting was used on the ID column (‘Unique customer ID’) to check for duplicate rows – none were found. 

•	In the Marital_Status column, ‘YOLO,’ Alone,’ and ‘Absurd’ were replaced with ‘Null,’ as it could not be determined if these meant Single, Divorced, or Widow. 

•	In the Education column, ‘2n Cycle’ was changed to ‘Master.’

•	Data in the Country column was changed to full country names, while several column titles were changed to be more informative. 

•	Outliers were removed for Age and Income. The upper age limit was 89 so customers aged 121, 122 and 128 years were removed, while eight with incomes above $118,351 were removed. 

•	In the Dt_Customer column, Text to Columns was used to fix any dates not in date format.

•	The data type for each column was checked and changed accordingly. For any column with a monetary value, the $ symbol was replaced with a blank and then changed to number format.

Data analysis:

•	Initial exploration with Excel revealed a strong relationship between increasing customer income and sales for all product types. In an interim meeting with the regional marketing teams, income was selected as the most important customer demographic for initial campaigns.

![image](https://github.com/kittyg80/2Market-Sales-and-Customer-Data-Analysis/assets/116217853/03b83527-9599-4cb2-859b-f687e7e0efe9)

•	SQL was used to infer a relationship between product sales and successful lead conversions by advertising channel. 

•	To do this, a new table was created which joined the Marketing_data and Ad_data using an inner join and customer ID (‘ID’) as the primary key. The new table contained the country, total sales per product, and lead conversion data for each customer. 

•	A query was created to show the sum of all successful conversions for each advertising channel  when there were sales of each product type (using > 0) by country. Product type was added to a new ‘product’ column, and the query was repeated for each product using a UNION operator. 

•	Results showed the inferred number of successful ad conversions for each advertising channel by product type and country.

•	Results were saved as the Ad_conversion_by_product CSV file to be uploaded onto Tableau for visualisation.

SQL syntax:

1.	Create new table
   
CREATE TABLE ad_conversion AS
SELECT md.id as customer_id, md.marital_status, md.liquor, md.vegetables, md.non_veg, md.fish_products, 
md.chocolates, md.commodities, md.country, ad.twitter_ad, ad.instagram_ad, ad.facebook_ad, ad.bulkmail_ad, ad.brochure_ad
FROM public.marketing_data md
JOIN public.ad_data ad
USING (id);

2.	Query relationship between product sales and effective advertising conversions by country
   
SELECT adc.country, 'liquor' product, SUM(adc.twitter_ad) as Twitter, SUM(adc.instagram_ad) as Instagram, 
SUM(adc.facebook_ad) as Facebook, SUM(adc.bulkmail_ad) as Bulkmail, SUM(adc.brochure_ad) as Brochure
FROM public.ad_conversion adc
WHERE adc.liquor > 0
GROUP BY adc.country
UNION
SELECT adc.country, 'vegatables' product, SUM(adc.twitter_ad) as Twitter, SUM(adc.instagram_ad) as Instagram, 
SUM(adc.facebook_ad) as Facebook, SUM(adc.bulkmail_ad) as Bulkmail, SUM(adc.brochure_ad) as Brochure
FROM public.ad_conversion adc
WHERE adc.vegetables > 0
GROUP BY adc.country
UNION
SELECT adc.country, 'non_veg' product, SUM(adc.twitter_ad) as Twitter, SUM(adc.instagram_ad) as Instagram, 
SUM(adc.facebook_ad) as Facebook, SUM(adc.bulkmail_ad) as Bulkmail, SUM(adc.brochure_ad) as Brochure
FROM public.ad_conversion adc
WHERE adc.non_veg > 0
GROUP BY adc.country
UNION
SELECT adc.country, 'fish_products' product, SUM(adc.twitter_ad) as Twitter, SUM(adc.instagram_ad) as Instagram, 
SUM(adc.facebook_ad) as Facebook, SUM(adc.bulkmail_ad) as Bulkmail, SUM(adc.brochure_ad) as Brochure
FROM public.ad_conversion adc
WHERE adc.fish_products > 0
GROUP BY adc.country
UNION
SELECT adc.country, 'chocolates' product, SUM(adc.twitter_ad) as Twitter, SUM(adc.instagram_ad) as Instagram, 
SUM(adc.facebook_ad) as Facebook, SUM(adc.bulkmail_ad) as Bulkmail, SUM(adc.brochure_ad) as Brochure
FROM public.ad_conversion adc
WHERE adc.chocolates > 0
GROUP BY adc.country
UNION
SELECT adc.country, 'commodities' product, SUM(adc.twitter_ad) as Twitter, SUM(adc.instagram_ad) as Instagram, 
SUM(adc.facebook_ad) as Facebook, SUM(adc.bulkmail_ad) as Bulkmail, SUM(adc.brochure_ad) as Brochure
FROM public.ad_conversion adc
WHERE adc.commodities > 0
GROUP BY adc.country
ORDER BY country, product;

