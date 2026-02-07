# Marketing A/B Testing Analysis:

This notebook helps you figure out whether your advertising campaign actually worked. It compares two groups of users - one that saw your ads and another that saw public service announcements instead - to measure the real impact of your marketing spend.

## What This Analysis Answers

The notebook is designed to answer four main questions:

1. Did the marketing campaign increase conversions?
2. How much of the conversion lift can we actually attribute to the ads versus people who would have bought anyway?
3. Are the differences between groups statistically significant, or could they just be random chance?
4. Do things like ad frequency, time of day, or day of week affect how well the ads perform?

## Data Requirements

You'll need a CSV file named `marketing_AB.csv` with the following columns:

- **user id**: A unique identifier for each user in the test
- **test group**: Either "ad" (user saw advertisements) or "psa" (user saw public service announcements)
- **converted**: True if the user made a purchase, False if they didn't
- **total ads**: The total number of ads shown to that user
- **most ads day**: Which day of the week the user saw the most ads
- **most ads hour**: Which hour of the day the user saw the most ads

## Required Python Libraries

You'll need to install these libraries if you don't already have them:

```bash
pip install numpy pandas matplotlib seaborn scipy
```

The notebook uses:
- **numpy** and **pandas** for data manipulation
- **matplotlib** and **seaborn** for visualizations
- **scipy** for statistical testing

## How to Use This Notebook

Before you start, there's one important thing you need to do. The notebook currently has a hardcoded file path:

```python
df = pd.read_csv("D:\Chrome\marketing_ab_testing_analysis\data\marketing_AB.csv")
```

Change this to wherever you've actually saved your data file. Once that's done, just run the cells from top to bottom.

The notebook will walk you through:
- Loading and exploring your data
- Calculating conversion rates for both groups
- Creating visualizations that compare the ad group to the control group
- Running statistical tests to determine if your results are significant

## Understanding the Statistical Tests

The analysis uses two main types of statistical tests:

### Chi-Square Tests

These test whether conversion rates differ between groups. The notebook runs chi-square tests for:
- Ad group vs PSA group (the main comparison)
- Different days of the week
- Different hours of the day

The key metric here is the p-value. If it's less than 0.05, that means the difference is statistically significant and probably not just random chance.

### Mann-Whitney U Test

This test compares the distribution of ad exposure between users who converted and those who didn't. The notebook uses this instead of a standard t-test because the data doesn't follow a normal distribution (which is pretty common with ad data).

Again, a p-value below 0.05 indicates a significant difference.

## What the Results Mean

When you run the notebook, look at the p-values from the statistical tests:

- **p-value much less than 0.05** (like 0.001 or smaller): Your ads are having a real, measurable effect on conversions. This is what you want to see.

- **p-value greater than 0.05**: The difference between your ad group and control group could just be random variation. The campaign might not be as effective as you thought.

The visualizations will also help you spot patterns - like whether certain days or times perform better than others, which can inform when you schedule future campaigns.
