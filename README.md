# 2Market-Sales-and-Customer-Data-Analysis

This was the first project I completed as part of the LSE Data Analytics Career Accelerator course (2022 - 2023), for which I achieved a mark of 88% (distinction). I used Excel, SQL, and Tableau for this project. 

**1. Project background:** 

2Market commissioned this project to better understand its customers, top products and markets by sales, and most effective advertising channels. A kick-off meeting with stakeholders revealed a loss in Q3 2022 revenue that requires immediate cost savings and increased sales. Further investigation shows this was mainly caused by US competition, ineffective marketing, unsuccessful market expansion, and decreased online sales of certain products post-COVID. This project aims to support senior management make decisions about where to focus the business and help regional marketing teams improve campaigns and identify the best advertising channels by product. Stakeholders acknowledged there was no data linking ad conversion to sales but agreed an estimation was sufficient.

**2. Analytical approach:**  

The Marketing_data and Ad_data files were first viewed as text to see delimiters and check for any unusual data.
 
**2(a) Data cleaning:**

•	A spellcheck and search for blank cells was conducted – no issues detected. 

•	Conditional Formatting was used on the ID column (‘Unique customer ID’) to check for duplicate rows – none were found. 

•	In the Marital_Status column, ‘YOLO,’ Alone,’ and ‘Absurd’ were replaced with ‘Null,’ as it could not be determined if these meant Single, Divorced, or Widow. 

•	In the Education column, ‘2n Cycle’ was changed to ‘Master.’

•	Data in the Country column was changed to full country names, while several column titles were changed to be more informative. 

•	Outliers were removed for Age and Income. The upper age limit was 89 so customers aged 121, 122 and 128 years were removed, while eight with incomes above $118,351 were removed. 

•	In the Dt_Customer column, Text to Columns was used to fix any dates not in date format.

•	The data type for each column was checked and changed accordingly. For any column with a monetary value, the $ symbol was replaced with a blank and then changed to number format.

**2(b) Data analysis:**

Initial exploration with Excel revealed a strong relationship between increasing customer income and sales for all product types. In an interim meeting with the regional marketing teams, income was selected as the most important customer demographic for initial campaigns.

![image](https://github.com/kittyg80/2Market-Sales-and-Customer-Data-Analysis/assets/116217853/03b83527-9599-4cb2-859b-f687e7e0efe9)

SQL was used to infer a relationship between product sales and successful lead conversions by advertising channel. To do this, a new table was created which joined the Marketing_data and Ad_data using an inner join and customer ID (‘ID’) as the primary key. The new table contained the country, total sales per product, and lead conversion data for each customer. A query was created to show the sum of all successful conversions for each advertising channel  when there were sales of each product type (using > 0) by country. Product type was added to a new ‘product’ column, and the query was repeated for each product using a UNION operator. Results showed the inferred number of successful ad conversions for each advertising channel by product type and country. Results were saved as the Ad_conversion_by_product CSV file to be uploaded onto Tableau for visualisation.


**3. Dashboard design:** 

The 2Market Dashboard consists of four visualizations and has been designed without red or green colours as one member of the regional marketing team is colour blind. Tooltips have been added to all charts to ensure they are interpreted accurately, whereas labels have only been used in static charts to avoid overcrowding in the dashboard. Chart titles have been edited to be meaningful and dynamic titles also added where relevant.

![image](https://github.com/kittyg80/2Market-Sales-and-Customer-Data-Analysis/assets/116217853/27abf655-757b-44ca-9878-6336f0b54987)

The **Product Sales by Category** and **Product Sales by Country** visualisations were created from the Marketing_data and are intended to quickly show overall sales performance for senior management. This will allow them to make decisions on which markets to focus on or withdraw from, and which products to focus on or discontinue. 

   •	**Product Sales by Category** shows product sales as a percentage of total sales. This was creating with a calculated field (‘Total Sales’), with further calculated fields created for each product as a percentage of ‘Total Sales.’ Aliases were created on charts e.g., ‘% Sales Liquor’ changed to ‘Liquor.’ 

   •	The **Product Sales by Country** chart shows sales by country as a percentage of total sales. A map was originally considered, but a bar chart was deemed more impactful.

The **Sales by Income** visualisation was created from the Marketing_data and is intended to support the regional marketing teams assess the impact of customer income on product sales.

   •	The data has been broken down by adding income categories to the colour marks, with income categories created using bins of $20,000. 

   •	The chart includes both a filter and dynamic title for Country so data can be seen at a regional level. 

   •	A caption has been added to note that tooltips show data as a percentage of total sales and not sales by country.

The **Estimated Ad Conversions by Channel** visualisation is also intended for the regional marketing teams to see the inferred relationship between successful ad conversions and product sales by country. 

   •	This was created from the Ad_conversion_by_product data from SQL. 

   •	A dynamic title has been added to show data by country.

   •	Labels have not been included as the chart is only meant to show which channel may be best. 

   •	A caption highlights that the data infers a relationship and should not be used for other purposes.


**4. Patterns, Trends, and Insights:** 

Analysis shows that liquor and non-vegetables account for >75% of sales, while **vegetables and chocolate make up <10% of sales**. This should enable management to decide whether to discontinue certain products in order to reduce storage and distribution costs.

![image](https://github.com/kittyg80/2Market-Sales-and-Customer-Data-Analysis/assets/116217853/513a9f3e-4031-4415-9346-8b88913d16b1)

Data shows Spain as the leading market, with almost 50% of sales. **The US makes up <5% while Macedonia has ~0.2%**. This should allow management to decide whether to withdraw from certain countries in order to make operational savings.

![image](https://github.com/kittyg80/2Market-Sales-and-Customer-Data-Analysis/assets/116217853/06c95f98-f70c-4fb5-aecd-affba508ae68)

Data also shows that **different customer income impacts total sales**. For example, customers in Spain earning $60-$79,999 account for 13.4% of total liquor sales, whereas those earning $80-$99,999 account for 5.5%. This will support regional marketing teams in targeting different customer groups with personalised campaigns, offers, or discounts. 

![image](https://github.com/kittyg80/2Market-Sales-and-Customer-Data-Analysis/assets/116217853/d8a18163-bbd3-465f-9ce7-71940ccf38f4)

Data shows the **relationship between ad conversions and sales is impacted by country**. For example, sales of non-vegetables are driven by Twitter in Canada but by Instagram in Australia. This will support the regional marketing teams choose effective ad channels.

![image](https://github.com/kittyg80/2Market-Sales-and-Customer-Data-Analysis/assets/116217853/7cfde542-99c3-4aea-bc1b-da186b436c00)


**5. Recommendations for further exploration:** 

•	Gather data to see true sales performance over time by product and country, including a breakdown of online and in-person sales. 

•	Gather data on the impact of campaigns on sales, such as campaign date, country, and product. 

•	Conduct further analysis on the impact of other demographics on sales, such as age. 

