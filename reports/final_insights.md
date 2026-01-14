# RetailInsight – Advanced Machine Learning Project Report

## Problem Statement

Modern online retail platforms generate massive volumes of transactional data, yet many struggle to extract meaningful insights from it. Unlike subscription-based services, retail customers do not explicitly state their intent or loyalty. As a result, businesses often treat all customers uniformly—offering discounts to already loyal customers while failing to identify high-value customers who are at risk of churn. This lack of visibility into customer behavior leads to inefficient marketing spend, missed bundling opportunities, and reduced long-term customer value.  
The objective of this project is to address this “marketing blindness” by leveraging advanced unsupervised learning techniques to automatically profile customers and uncover product-level purchase patterns.

---

## Dataset Overview

This project uses the **Online Retail II dataset** from the UCI Machine Learning Repository. The dataset contains approximately **525,000 real-world transactional records** from a UK-based online retail store. Each record represents a single product purchased within an invoice and includes information such as invoice number, product description, quantity, price, purchase timestamp, and customer identifier.  
The dataset is well-suited for advanced machine learning as it includes real-world noise such as missing customer identifiers, product returns, and zero-priced transactions, enabling realistic data cleaning and preprocessing.

---

## Data Cleaning & Feature Engineering

To ensure data integrity, several preprocessing steps were applied. Transactions with missing customer identifiers were removed, as customer-level analysis is not possible without reliable identifiers. Product returns and invalid transactions—identified through negative or zero quantities and prices—were excluded to avoid incorrect monetary calculations.  
A new feature, **TotalPrice**, was engineered by multiplying quantity and unit price to represent transaction-level revenue. The cleaned dataset was then aggregated at the customer level to construct **RFM (Recency, Frequency, Monetary)** features. Recency was calculated as the number of days since a customer’s most recent purchase, Frequency as the number of unique invoices, and Monetary as the total revenue contributed by the customer.

---

## Customer Segmentation (RFM + K-Means)

Using the engineered RFM features, customers were segmented through **K-Means clustering**. All features were standardized to ensure fair contribution during distance-based clustering. The optimal number of clusters was determined using the **Elbow Method**, resulting in four distinct customer segments.

The clusters revealed clear behavioral personas:
- **Elite Whales**: Extremely high-spending and highly frequent customers, representing a very small but critical segment.
- **VIP Customers**: High-value and loyal customers with strong repeat purchasing behavior.
- **Loyal Customers**: Moderately frequent buyers who contribute steady revenue.
- **At-Risk / One-Time Buyers**: Customers with high recency and low engagement, indicating potential churn.

These personas provide a structured and interpretable view of customer behavior, enabling targeted decision-making.

---

## Market Basket Analysis

To understand *what* products drive loyalty, **association rule mining using the Apriori algorithm** was performed on transactions belonging to high-value customers (VIP segment). Transactions were transformed into an invoice–product binary matrix, and frequent itemsets were extracted using a minimum support threshold.  
The resulting association rules demonstrated extremely strong co-purchase behavior, with confidence values exceeding 90% and lift values greater than 10. The strongest rules consistently linked white and wooden home décor items, such as picture frames and storage cabinets, indicating style-driven purchasing behavior. These findings highlight clear opportunities for curated product bundles and recommendation systems.

---

## Business Outcomes

The project delivers multiple actionable business outcomes. Customer personas derived from clustering enable precise targeting strategies, allowing businesses to avoid unnecessary discounting of loyal customers while focusing retention efforts on high-value at-risk segments.  
Market basket analysis provides data-backed bundling opportunities, supporting “frequently bought together” recommendations and curated décor packages aimed at increasing average order value. Additionally, customers exhibiting declining recency despite high historical spending can be proactively targeted through personalized engagement, reducing silent churn and improving long-term customer lifetime value.

---

## Assumptions & Limitations

This analysis assumes that historical purchasing behavior is a strong predictor of future customer actions and that customers within the same cluster exhibit similar intent. However, the dataset is purely transactional and lacks demographic, geographic, or sentiment information. Customer behavior is analyzed as a static snapshot and does not explicitly model temporal changes, seasonality, or external promotional effects.

---

## Conclusion

This project demonstrates how advanced unsupervised learning techniques can convert raw transactional data into meaningful business intelligence. By combining RFM-based customer segmentation with association rule mining, the analysis uncovers high-value customer personas and strong product bundling patterns. The proposed approach enables data-driven marketing strategies, improved customer retention, and smarter merchandising decisions, making it a practical and scalable solution for real-world retail analytics.
