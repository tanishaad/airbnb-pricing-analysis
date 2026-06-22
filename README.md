# NYC Airbnb Pricing Analysis

This project analyzes Airbnb listing prices in New York City using exploratory data analysis and supervised learning methods. The goal was to understand which listing characteristics are most related to price and to build predictive models that estimate Airbnb listing prices based on features such as location, room type, property type, bedrooms, guest capacity, booking rules, and host information.

## Project Overview

Airbnb prices can vary widely across listings, even within the same city. A private room in one neighborhood may be much cheaper than an entire apartment in another, and listing characteristics such as size, location, and privacy can strongly influence price.

The original dataset included Airbnb listings from multiple cities. During early exploration, I found that prices did not appear to be standardized into one common currency across cities, so I limited the final analysis to New York listings only. This allowed for a cleaner and more meaningful comparison of pricing patterns within one market.

## Research Questions

This project focuses on the following questions:

* Which listing characteristics are most associated with Airbnb prices in New York?
* How do room type, property type, neighborhood, bedrooms, and guest capacity affect price?
* How accurately can supervised learning models predict Airbnb listing prices?
* Which model performs best for this pricing prediction task?

## Dataset

The dataset used in this project is the Airbnb Listings dataset from Kaggle.

Dataset source:
https://www.kaggle.com/datasets/ulrikthygepedersen/airbnb-listings/data

### Dataset Size

| Stage                           | Listings | Variables |
| ------------------------------- | -------: | --------: |
| Original Airbnb dataset         |  279,712 |        33 |
| New York subset before cleaning |   37,012 |        33 |
| Final modeling dataset          |   33,044 |        16 |

The final modeling dataset includes variables such as:

* Price
* Room type
* Property type
* Neighborhood
* Number of bedrooms
* Number of guests accommodated
* Minimum and maximum nights
* Host total listings count
* Host verification status
* Instant bookable status
* Latitude and longitude

## Methods

### Data Cleaning and Preprocessing

The data was cleaned and prepared by:

* Filtering the dataset to New York listings
* Removing missing values in key modeling variables
* Removing prices below $10
* Capping extreme prices above the 99th percentile
* Creating a log-transformed price variable
* Simplifying high-cardinality categorical variables such as neighborhood and property type
* Splitting the data into training and test sets

Since Airbnb prices were right-skewed, I modeled `log_price` instead of raw price to improve model stability.

### Exploratory Data Analysis

I explored pricing patterns by:

* Room type
* Property type
* Neighborhood
* Number of bedrooms
* Number of guests accommodated
* Price and log-price distributions

The EDA showed that listing size, privacy, and location were strongly related to price.

### Predictive Modeling

I compared three supervised learning models:

1. Multiple Linear Regression
2. Regression Tree
3. Random Forest Regression

All models were trained on log-transformed price and evaluated on the same test set.

## Model Results

| Model             | RMSE Log | MAE Log | RMSE Price | MAE Price | Test R² |
| ----------------- | -------: | ------: | ---------: | --------: | ------: |
| Linear Regression |   0.4430 |  0.3399 |     $77.82 |    $43.72 |  0.5687 |
| Regression Tree   |   0.4747 |  0.3659 |     $84.02 |    $47.30 |  0.5048 |
| Random Forest     |   0.3892 |  0.2903 |     $69.88 |    $38.22 |  0.6672 |

The random forest model performed best overall, explaining about 66.7% of the variation in log Airbnb price and achieving an average absolute prediction error of about $38.22 on the original price scale.

## Key Findings

* Entire places and hotel rooms had much higher median prices than private or shared rooms.
* Listings with more bedrooms and higher guest capacity generally had higher prices.
* Central and high-demand neighborhoods such as Greenwich Village, Murray Hill, West Village, Theater District, SoHo, Midtown, Chelsea, and Hell’s Kitchen had some of the highest median prices.
* Location, listing size, room type, property type, and host-related characteristics were all important pricing factors.
* The random forest model outperformed linear regression and a single regression tree by capturing more complex relationships between listing features.

## Tools and Technologies

* R
* tidyverse
* ggplot2
* rpart
* rpart.plot
* randomForest
* knitr
* R Markdown

## How to Run This Project

1. Download the Airbnb Listings dataset from Kaggle:
   https://www.kaggle.com/datasets/ulrikthygepedersen/airbnb-listings/data

2. Place the dataset in a local folder.

3. Open `airbnb_pricing_analysis.Rmd` in RStudio.

4. Update the file path in the code if needed:

```r
listings <- read.csv("~/Downloads/Listings.csv")
```

5. Install the required R packages if they are not already installed:

```r
install.packages(c("tidyverse", "knitr", "rpart", "rpart.plot", "randomForest"))
```

6. Knit the R Markdown file to generate the PDF report.

## Project Files

- [Final Report PDF](airbnb_pricing_analysis.pdf)  
  *Note: If GitHub does not render the PDF preview, download the file to view the full report.*
- [R Markdown Source Code](airbnb_pricing_analysis.Rmd)

## Future Improvements

Future versions of this project could include:

* Additional models such as gradient boosting or tuned random forests
* More advanced hyperparameter tuning
* Feature engineering from amenities text
* Incorporating review scores or review text if more complete review data is available
* Comparing New York to other cities after converting all prices into a common currency

## Author

**Tanisha Dutta**
B.S. Statistics & Data Science
B.A. Computational Linguistics
University of California, Santa Barbara
