# Illuminati-case-interview
A dynamic pricing solution for restaurant chain   
# Restaurant Pricing Optimization Dashboard

An interactive prototype that helps restaurant teams evaluate how
pricing changes may affect demand, revenue, and contribution across
different stores and products.

The dashboard combines a regression-based demand model with a pricing
simulator. Users can adjust pricing and demand assumptions, compare
scenarios, and explore the price that produces the highest **estimated
contribution** within a defined test range.

> **Important:** This is a prototype for demonstration and decision
> support. The initial model uses synthetic data. Its recommendations
> are illustrative and must be validated using real transaction data
> before business use.

## Problem Statement

Restaurant chains often operate across locations with different customer
profiles, competitor prices, and demand patterns. A single uniform price
may not work equally well across every store.

-   Increasing price can improve contribution per order but may reduce
    order volume.
-   Discounts can increase orders while reducing profitability.
-   Higher revenue does not necessarily mean higher contribution.

This prototype helps users compare pricing scenarios before testing
changes in the market.

## Key Features

-   **Interactive scenario controls:** Select a store and product and
    adjust own price, competitor price, search interest, weekday/weekend
    conditions, and unit variable cost.
-   **Demand estimation:** Use a regression-based model to estimate
    order volume under the selected assumptions.
-   **Business KPIs:** View estimated orders, revenue, contribution, and
    contribution per order.
-   **Scenario comparison:** Compare current, test, and recommended
    price scenarios.
-   **Price-response curve:** Explore how estimated revenue and
    contribution change across a range of candidate prices.
-   **Data upload:** Upload historical data in CSV or Excel format to
    re-estimate the model in the browser.
-   **CSV template:** Download a template to prepare data in the
    expected structure.

## How It Works

1.  **Load data:** Start with the built-in synthetic dataset or upload
    historical sales data.
2.  **Estimate demand:** The prototype fits a regression model using
    historical order volume and selected demand drivers.
3.  **Change assumptions:** Adjust the selling price and other inputs in
    the dashboard.
4.  **Compare outcomes:** Review the estimated effect on orders,
    revenue, and contribution.
5.  **Explore a recommendation:** The dashboard searches a bounded range
    of candidate prices and displays the price with the highest
    estimated contribution within that range.

The model is intended to support pricing analysis---not to guarantee
future results or replace controlled market testing.

## Getting Started

### Option 1: Open the HTML dashboard

1.  Download or clone this repository.
2.  Locate `restaurant_pricing_optimizer.html`.
3.  Open the file in a modern browser such as Google Chrome or Microsoft
    Edge.
4.  Use the built-in sample data, or upload your own CSV/Excel dataset.

The dashboard is designed as a single-page HTML prototype. CSV parsing
and model calculations run in the browser. Excel file reading may
require an internet connection because the page loads a
spreadsheet-reading library from a CDN.

### Option 2: Clone the repository

``` bash
git clone <YOUR_REPOSITORY_URL>
cd <YOUR_REPOSITORY_FOLDER>
```

Then open `restaurant_pricing_optimizer.html` in your browser.

Replace the placeholders above with your actual GitHub repository URL
and folder name.

## Data Format

The dashboard expects historical observations containing fields similar
to the following. Column aliases may be supported by the current
prototype, but using these names is recommended.

  -----------------------------------------------------------------------
  Column                  Description             Example
  ----------------------- ----------------------- -----------------------
  `Store`                 Store or location       `Store A`
                          identifier              

  `Product`               Product identifier or   `Burger`
                          name                    

  `Selling Price`         Price charged for the   `₹250`
                          product                 

  `Units Sold`            Number of units/orders  `120`
                          sold for the            
                          observation period      

  `Competitor Price`      Relevant competitor     `₹270`
                          price                   

  `Search Index`          Search-interest or      `75`
                          demand proxy            

  `Weekend Flag`          Whether the observation `1`
                          is a weekend (`1`) or   
                          weekday (`0`)           

  `Unit Variable Cost`    Variable cost per unit  `₹100`

  `Fixed Cost (Daily)`    Optional fixed cost for `₹2,000`
                          the observation period  
  -----------------------------------------------------------------------

**Data preparation tips** - Use one row per store, product, and
observation period. - Keep price and cost values numeric; do not include
currency symbols in numeric cells. - Use consistent units and time
periods across rows. - Ensure `Units Sold` is non-negative and check for
missing or invalid values. - Use enough historical observations across
different prices and demand conditions to estimate relationships more
reliably. - Do not upload confidential or personally identifiable
customer data unless you are authorized to do so.

## Model Overview

The prototype uses a regression-based demand model. Its predictors
include:

-   Own selling price
-   Competitor price
-   Search-interest index
-   Weekend indicator
-   Store and product effects

The estimated demand is then used to calculate scenario metrics:

-   **Revenue** = Selling price × Estimated units sold
-   **Variable cost** = Unit variable cost × Estimated units sold
-   **Contribution** = Revenue − Variable cost
-   **Contribution per order** = Selling price − Unit variable cost

Where applicable, fixed costs can be included separately in the
dashboard's analysis. Contribution is not the same as net profit because
other operating costs may not be included.

The recommended price is the candidate price with the highest
model-estimated contribution within the tested price range. It is not
necessarily the price that maximizes revenue or order volume.

## Assumptions and Limitations

-   The default dataset is synthetic and is intended to demonstrate the
    workflow.
-   Regression estimates show associations in the supplied data; they do
    not by themselves prove that price changes cause the predicted
    demand response.
-   Sparse data, limited price variation, missing variables,
    seasonality, promotions, stockouts, delivery fees, and competitor
    changes can affect model quality.
-   Predictions for a store/product combination with little or no
    relevant historical data may be unreliable.
-   The price recommendation is limited to the candidate range searched
    by the prototype.
-   Before deployment, validate predictions on holdout data and run
    controlled pricing experiments where appropriate.
-   Treat results as decision support, not an automatic pricing
    instruction.

## Suggested Validation Before Real-World Use

1.  Replace synthetic observations with clean historical transaction
    data.
2.  Check data quality, outliers, missing values, and consistent time
    intervals.
3.  Evaluate forecast errors on a holdout period.
4.  Review estimated price sensitivity for business plausibility.
5.  Test recommendations against margin, customer, brand, and
    operational constraints.
6.  Pilot price changes in selected stores and monitor orders, revenue,
    contribution, and customer response.

## Repository Structure

A simple repository layout could be:

``` text
restaurant-pricing-optimization/
├── README.md
├── restaurant_pricing_optimizer.html
└── sample_data.csv
```

Include `sample_data.csv` only if you choose to publish a sample dataset
or template. Do not commit confidential business data.

## Demo

For a short demo: 1. Select a store and product. 2. Change the selling
price. 3. Observe the estimated orders, revenue, and contribution. 4.
Compare the current and test scenarios. 5. Review the contribution curve
and recommended price. 6. Explain that the initial results use synthetic
data and require validation.

## Future Enhancements

-   Add model-quality metrics and a holdout validation report.
-   Support store-specific elasticity estimates when sufficient data is
    available.
-   Include promotion, seasonality, stockout, and customer-segment
    variables.
-   Add business guardrails such as minimum contribution, maximum price
    changes, and competitor-price limits.
-   Enable export of scenario comparisons and recommendation summaries.

## License

No license has been specified yet. Add a license before allowing others
to reuse, modify, or distribute this project.
