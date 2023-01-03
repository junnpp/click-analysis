# Click Analysis

Full project report can be found [here](./analysis.ipynb).

Skills: Python, SQL (DuckDB), and Visualization (Seaborn)

Conducted a clickstream analysis on data for online shopping store offering clothing for pregnant women between April 2008 to August 2008. The data set is publicly posted on [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/clickstream+data+for+online+shopping). It contains approximately 160,000 rows with 14 columns and each row represents a single click per customer. The main scope of the analysis can be summarized on two different points:

1. What is the overall traffic distribution?
2. What factors affect customers behavior on the website?

Columns are as follows:

![column-description](./img/2-columns.png)
 
## Exploratory Data Analysis

### Traffic Distribution Across Weekdays

There are two columns that indicate user traffic: `order`, `session ID`. While each `session ID` represents an unique user, `order` shows the whole sequence of customers behavior on the website by indicating each click. Let's compare them to see if there's any difference.

<p float="left">
  <img src="./img/3-click-dist.png" width="100" />
  <img src="./img/4-session-dist.png" width="100" /> 
</p>

Notice there's hardly any difference between two distributions. Tuesday has the largest amount of traffic while weekends have the least. Recall that this website offers clothings for pregnant women, meaning that the users are most likely pregnant women themselves. Assuming most users are staying at home due to pregnancy, they might have more free time to search for clothings when other family members are not around: weekdays, especially around afternoon. As to Tuesday having the peak, we can make a hypothesis that the more it is close to the weekends, the more time customers have to spend for family business.

### Session Distribution Across Countries

![country](./img/5-country-dist.png)

The majority traffic occurs in european countries.

### Traffic Distribution Across Months

![month](./img/6-month-dist.png)

There is significantly more traffic during April. Accoring to the birthrate analysis "[Do humans have mating seasons?](https://visme.co/blog/most-common-birthday/)", there is an interesting pattern of birth months. Around the world, there is NOT a single country with its peak birth month as April and most european countries have their peak birth month bewteen June-September. This indicates that demand for prenant women's clothing in european countries will be higher between February-April compared to that of June-September.

![peak-birth-month](./img/1.peak-birth-month.png)

### Product Price Distribution

![product-price-dist](./img/7-price-dist.png)

Product price ranges between $18-$80 and the majority products cost about $40.

---

## Click Analysis

### Does the photo location significantly affect the click rate?

![click-order](./img/8-click-order.png)

Notice top-left has the largest amount of traffic for most cases, while the top-right has the least amount of traffic. While the first click has the most traffic, its deviation among photo locations is larger compared to that of other click orders. As customers make more subsequent clicks, they tend to not care about photo location as much.

### Any relationship between photo location and model photography?

![loc-type](./img/9-photo-type-vs-loc.png)

Due to the huge overall difference in traffic between en face and profile photo types, it is difficult to draw any statistical conclusion. However, there are still a few points to which pay close attention.

1. Top-left photo location has the largest traffic discrepancy between the two photo types.
2. Bottom-center has the least traffic difference between the two photo types.
3. While the amount of traffic fluctuates among top-right, bottom-left, and bottom-right for en face type, it does not differ that much for profile photo type.

### Should we inform customers that the price of a particular product is higher than the average price for other products in the same category?

First, let's only consider the click customers make on the website. `price 2` column indicates whether the price of a particular product is higher than the average price for the entire product category.

![price2-1](./img/10-price2-1.png)

Customers are slightly more likely (~1%) to click on a particular product if it is informed that the price of it is higher than the average price for the other products in the same category. Although the difference is trivial, the result is a bit counterintuitive: customers click more for expensive products. One should be careful about drawing such a conclusion since there are other interacted factors such as color, product type, clothing model, etc.

Now, **given first click's `price 2` value, what are the percentage of each `price 2` columne value for the next click?**

![price2-2](./img/11-price2-2.png)

Without taking other factors into account, customers who made first click on the products that are informing whether the price is higher compared to the average price for other products are more likely (~12%) to click on products that are **ALSO** informing about the price.

Now, repeat this analysis for rows whose first click `price 2` value is 2 (No).

![price2-3](./img/12-price2-2.png)

Customers who made the first click on the products that are NOT informing whether the price is higher than the average price for other products are much more likely (~11%) to make second clicks on the products that are NOT informing about the price as well.

###  What is the popular product type, color, or type-color combination?

![color1](./img/13-color.png)

Let's only consider the **first** click customers make when they entered the website. Without considering other factors, blue has significantly more clicks compared to other product colors. Let's consider the photo location this time.

![color2](./img/14-color2.png)

Blue products located at the top left on the first page of the website have the highest number of first clicks. Now let's consider product type as well.

![color3](./img/15-color3.png)

Among all possible color-category combinations, the blue trouser has significantly more clicks than others on the first page. Keep in mind this is only the first response analysis: the first click a customer makes on the first page of the website.