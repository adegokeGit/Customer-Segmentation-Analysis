# *Targeting Prime Segments of One-Time Buyers Could Add ~0.7% to Revenue at Minimal Cost*

**A Customer Segmentation Analysis for Retention Marketing**

### Business Problem

Customer retention campaigns, meaning campaigns focused entirely on keeping existing customers engaged and buying, often rely on a one-size-fits-all message blasted to the whole customer base. My goal was to replace that with tailored recommendations based on each customer’s purchase history, which I expected to increase engagement and purchases.

To get there, I segmented the existing customer base so the marketing team can see which purchasing behavior group each customer belongs to.

### Results

- **Repeat Buyers:** 924 customers (10%)
- **One-Time Buyers:** 8,313 customers (90%)

| Cluster | Segment | Customers |
| --- | --- | --- |
| Repeat Buyers | 3+ orders | 143 |
| Repeat Buyers | 2 orders | 781 |
| One-Time Buyers | Last purchase 0–90 days ago | 296 |
| One-Time Buyers | 91–180 days | 844 |
| One-Time Buyers | 181–365 days | 1,784 |
| One-Time Buyers | 365+ days | 5,389 |

### Key Findings

Among repeat buyers, the gap between the first and second purchase averages about 86 days, with a median of about 37 days. Most customers who come back do so quickly.

### Conclusion

Within the One-Time Buyers cluster, the segment that purchased in the last 0–90 days is the most likely to respond to personalized offers. These customers are still inside the window in which repeat buyers typically make their second purchase, which makes them ripe for a repurchase. A retention campaign targeted at this segment is projected to drive a ~0.7**% lift in total revenue**.

### Technical Review

**Data:** The dataset contained 18,000+ raw sales transactions from an eCommerce brand, including order and sales details.

**Cleaning:** I removed duplicates, corrected incorrect and missing values, fixed formatting issues, and dropped unneeded columns.

**Feature engineering:** I aggregated the transactions into customer-level Recency, Frequency, and Monetary (RFM) features to prepare the data for K-Means.

**Choosing K:** After scaling the RFM values, I used the Elbow and Silhouette methods to find the optimal number of clusters. They disagreed: the Elbow method pointed to K = 4 and the Silhouette method to K = 2. I tested both and chose K = 2, because K = 4 did not produce meaningful, distinct clusters in practical terms.

<img width="1170" height="559" alt="CSA 2" src="https://github.com/user-attachments/assets/5faa3a21-c3df-45cc-b9e5-cc61b1ad169b" />

Image above shows the Elbow Method Graph
<img width="1200" height="555" alt="CSA 3" src="https://github.com/user-attachments/assets/8462ee13-d470-41a9-a40a-e343551a809a" />

Image above shows the Silhouette Score Graph

### Analysis Notebook

The target audience was widen to include 91-180 days segment because they are still relatively near the window in which repeat buyers typically make their second purchase.

### How I arrived at ~0.7% lift

Assuming a 10% incremental response rate for the 0-90 day segment and 5% for the 91-180 day segment, with each responder placing one order at the average order value of ~30,870, the campaign is projected to generate about 72 additional orders and a ~0.7% lift in total revenue

### Limitations

The customer base is dominated by one-time buyers (90%), so Frequency has very little variance, and RFM features are typically right-skewed. I standardized the features with StandardScaler, which rescales but does not correct skew or reduce outlier influence. At K = 3 and K = 4, one cluster contained only 2 customers, almost certainly outliers. In hindsight, I would apply a log transformation before scaling, and examine extreme-value customers separately (they may be bulk or high-value buyers). I’d also test alternative methods such as hierarchical clustering or Gaussian Mixture Models.

### Tech Stack

- Python(Pandas, Sklearn, numpy)
