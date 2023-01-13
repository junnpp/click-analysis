# Click Analysis

![uci-logo](./img/0-uci.png)

## [Full Report can be found here](./analysis.ipynb).

Conducted a clickstream analysis on data for an online shopping store offering clothing for pregnant women between April 2008 to August 2008. The data set is publicly posted on [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/clickstream+data+for+online+shopping). It contains approximately 160,000 rows with 14 columns and each row represents a single click per customer. Column value description can be found in the full project report.

## Motivation

To optimize the user experience on a website, it is essential to understand how customers behave on the current version of the website. Such analysis not only provides a direction to minimize customer loss but also shows how factors such as photo location, product types, and product color affect customer behavior.

## Project goals

- What is the overall traffic distribution?
- Which factors of products affect customers' behavior on the website?
- Which factor combinations attract more clicks?

## Exploratory Data Analysis

### Traffic Distribution - Click/Session

- There are two columns indicate the user traffic: `order` and `session ID`.
    - `session ID`: a unique user in a specific time frame (each `session ID` has more than 1 clicks)
    - `order`: the whole sequence of customers' behavior on the website (order of 1 indicates the first click and 2 indicates the second click, and so on)
- The week day distributions of the two are almost identical.
- Tuesday has the largest amount of traffic while weekends have the least. A hypothesis is that the more it is close to the weekends, the more time customers (pregnant women) have to spend time on the family business.

### Traffic Distribution - Countries

The majority of traffic occurs in European countries:

1. Poland: n=19582
2. Czech Republic: n=2261
3. Lithuania: n=527
4. United Kingdom: n=127
5. Ireland: n=102
6. Germany: n=101
7. Slovakia: n=88

### Traffic Distribution - Month

- There is significantly more traffic during April compared to May, July, June, and August (least). 

<p align="left">
    <img src="./img/1.peak-birth-month.png" width="35%"> 
</p>

 According to a [birthrate analysis](https://visme.co/blog/most-common-birthday/)", there is NOT a single country with its peak birth month as April and most European countries have their peak birth month between June-September. This indicates that demand for pregnant women's clothing in European countries will be higher between February-April compared to that of June-September.

### Product Price Distribution

- The clicked product price ranges between $18-$80. $40 products received the most clicks and $40 had the second most clicks.

## Click Analysis

### Q. Does the photo location significantly affect the click rate?

![click-order](./img/8-click-order.png)

Notice top-left has the largest amount of traffic for most cases, while the top-right has the least amount of traffic. While the first click has the most traffic, its deviation among photo locations is larger compared to that of other click orders. As customers make more subsequent clicks, they tend to not care about photo location as much.

### Q. Any relationship between photo location and model photography?

![loc-type](./img/9-photo-type-vs-loc.png)

- Huge overall difference in traffic between en face and profile photo types (ef face > profile). 
- However, there are still a few points to which pay close attention.
    1. Top-left photo location has the largest traffic discrepancy between the two photo types.
    2. Bottom-center has the least traffic difference between the two photo types.
    3. While the amount of traffic fluctuates among top-right, bottom-left, and bottom-right for en face type, it does not differ that much for profile photo type.

### Q. Should we inform customers that the price of a particular product is higher than the average price for other products in the same category?

`price 2` column indicates whether the price of a particular product is higher than the average price for the entire product category. This analysis only considers the first click.

- Yes: 50.48%
- No: 49.52%

**Given the first click's `price 2` value, what are the percentages of each `price 2` column value for the subsequent click?**

- **First Click: Yes**
  - Second Click:
    - Yes: 56.02%
    - No: 43.98%

- **First Click: No**
  - Second Click:
    - Yes: 44.94%
    - No: 55.05%

### Q. What is the popular product type, color, or type-color combination (first click)?

### Color-Photo Location

Blue products located at the top left on the first page of the website have the highest number of first clicks

![color2](./img/14-color2.png)


### Color-Product Type

The blue trouser has significantly more clicks than others on the first page.

![color3](./img/15-color3.png)

## References

- [Sessions vs. Clicks: What’s the Difference Anyway?](https://blog.stackadapt.com/sessions-vs-clicks-what-s-the-difference-anyway)
- [Do humans have mating seasons? This heat map reveals the surprising link between birthdays and seasons](https://visme.co/blog/most-common-birthday/)
- [Human birth seasonality: latitudinal gradient and interplay with childhood disease dynamics](https://royalsocietypublishing.org/doi/10.1098/rspb.2013.2438)
