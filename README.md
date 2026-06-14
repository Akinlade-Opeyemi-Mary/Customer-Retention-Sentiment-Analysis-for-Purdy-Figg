# CUSTOMER RETENTION & SENTIMENT ANALYSIS 
## Executive Summary
Purdy & Figg is a subscription-based eco-friendly cleaning products company focused on delivering sustainable household solutions through recurring customer subscriptions. While the brand enjoys strong customer satisfaction and positive product perception, retention challenges and early subscription cancellations have limited long-term customer value and marketing efficiency.

This analysis was conducted to understand customer retention behavior, identify the drivers of customer satisfaction and dissatisfaction, uncover behavioral customer segments, and recommend data-driven strategies to improve retention, engagement, and customer lifetime value.

Using Python, TextBlob, Power BI, and K-Means Clustering, customer reviews and subscription data were analyzed to measure sentiment, evaluate customer engagement patterns, and segment customers based on purchasing behavior and revenue contribution. Interactive dashboards were developed to visualize customer sentiment trends, retention performance, reply effectiveness, and customer segmentation insights.

The findings revealed that overall customer sentiment was highly positive, driven by product quality, fragrance, eco-friendly values, and customer experience. However, recurring concerns related to delivery delays, packaging issues, subscription management, and limited personalization were identified as key contributors to customer churn and reduced retention rates.

Customer segmentation further revealed distinct behavioral groups, including high-value loyal customers, occasional buyers, trial users, and price-sensitive customers. These insights highlighted opportunities for personalized marketing, targeted loyalty programs, improved customer communication, and enhanced subscription experiences.

## Company Overview

Purdy & Figg is a direct-to-consumer cleaning products company specializing in environmentally friendly household cleaning solutions. The company operates a subscription-based business model that encourages recurring purchases through scheduled product deliveries and personalized customer experiences.

As customer acquisition costs continue to rise across the e-commerce industry, retaining existing customers has become increasingly important for maintaining profitability and sustainable growth. Understanding customer behavior, purchase patterns, and customer sentiment is therefore critical to maximizing customer lifetime value and improving long-term business performance.

This project combines customer retention analysis, sentiment analysis, and customer segmentation techniques to provide a comprehensive understanding of customer experiences and behavioral patterns. The objective is to help business stakeholders identify retention challenges, improve customer satisfaction, and implement targeted strategies that increase loyalty, reduce churn, and drive sustainable revenue growth.

## Business Challenges

Purdy & Figg faced several interconnected customer experience and retention challenges that limited its ability to maximize customer lifetime value despite maintaining strong product satisfaction and positive brand perception.

Key challenges identified include:

* **Low Customer Retention:**
  Analysis revealed that a significant proportion of customers discontinued their subscriptions after only a few completed cycles, limiting long-term revenue generation and customer lifetime value.

* **Subscription Churn and Early Cancellations:**
  Customer feedback and subscription behavior indicated that many users failed to remain engaged long enough to experience the full value of the company's products and subscription offering.

* **Delivery and Fulfillment Concerns:**
  While overall sentiment remained highly positive, recurring complaints related to delivery delays, postage issues, and fulfillment processes negatively impacted portions of the customer experience.

* **Packaging-Related Dissatisfaction:**
  A subset of customer reviews highlighted concerns regarding packaging quality and product presentation, creating friction within an otherwise positive customer journey.

* **Limited Customer Personalization:**
  Existing marketing efforts largely treated customers as a single audience despite clear differences in purchasing behavior, product preferences, and subscription engagement levels.

* **Underutilization of Customer Feedback:**
  Although customers actively shared feedback through reviews and ratings, there was limited visibility into the underlying themes driving customer satisfaction, dissatisfaction, and retention outcomes.

* **Inefficient Customer Segmentation:**
  The absence of behavioral segmentation reduced the company's ability to tailor marketing campaigns, loyalty initiatives, and product recommendations to specific customer groups.

* **Need for Stronger Customer Engagement Strategies:**
  Analysis showed opportunities to strengthen customer relationships through proactive communication, personalized experiences, and structured loyalty programs that encourage long-term commitment.

These challenges collectively highlighted the need for a data-driven approach to understanding customer behavior, improving retention performance, enhancing customer experience, and developing targeted strategies that support sustainable business growth.

## Data Architecture & Tools

**Data Source:**  
The dataset used for this analysis is available [here](https://docs.google.com/spreadsheets/d/1PMVWjVCaBbk-JDB5yNGQBcF34ZXx9KqpWisB9MC0OuE/edit?gid=1794716114#gid=1794716114).

The project utilized two primary datasets:

* **Customer Reviews Dataset** – containing customer review messages, replies, ratings, and sentiment-related information.
* **Customer Dataset** – containing customer information used to support sentiment and behavioral analysis.

These datasets were processed and transformed to generate sentiment metrics, customer themes, and engagement insights used throughout the analysis.

### Tools and Technologies Used

* **Python (Pandas & TextBlob)** → Sentiment analysis, text processing, polarity scoring, subjectivity scoring, and sentiment classification.

* **Microsoft Excel** → Initial data cleaning, validation, transformation, and quality assurance.

* **Power Query** → Data transformation, duplicate removal, data standardization, and theme categorization.

* **Power BI** → Interactive dashboard development, KPI tracking, sentiment visualization, and business storytelling.

* **DAX (Data Analysis Expressions)** → Creation of calculated columns and measures including Net Sentiment Score, Reply Rate, Sentiment Recovery, Subjectivity Metrics, and Customer Engagement KPIs.

* **PowerPoint** → Executive presentation design, dashboard storytelling, and stakeholder communication.

* **GitHub** → Project documentation, portfolio presentation, version control, and knowledge sharing.

### Data Architecture Workflow

```text
Raw Review Data & Customer Data
              ↓
        Data Cleaning
      (Excel / Power Query)
              ↓
      Python Sentiment Analysis
        (Pandas + TextBlob)
              ↓
    Polarity • Subjectivity
     Focus Flag • Sentiment
              ↓
      Processed CSV Files
              ↓
      Power BI Data Model
              ↓
     DAX Measures & KPIs
              ↓
 Interactive Sentiment Dashboards
              ↓
 Business Insights & Recommendations
```
## Sentiment Analysis Methodology

To understand customer emotions and feedback patterns, Natural Language Processing (NLP) techniques were applied using Python and the TextBlob library.

The sentiment analysis process transformed raw customer review text into measurable sentiment indicators, allowing reviews to be classified as Positive, Neutral, or Negative while also measuring emotional intensity and objectivity.

### Libraries Used

```python
import pandas as pd
from textblob import TextBlob
```

#### Pandas

Used for:

* Reading and processing CSV datasets
* Manipulating and transforming review data
* Creating new sentiment-related columns
* Exporting processed datasets for visualization

#### TextBlob

Used for:

* Natural Language Processing (NLP)
* Sentiment Analysis
* Polarity Scoring
* Subjectivity Scoring

---

## Sentiment Metrics

### Polarity

Polarity measures the emotional tone of a review and determines whether customer feedback is positive, neutral, or negative.

| Score Range | Interpretation |
| ----------- | -------------- |
| -1.0        | Very Negative  |
| 0.0         | Neutral        |
| +1.0        | Very Positive  |

---

### Subjectivity

Subjectivity measures how opinion-based or emotionally driven a review is.

| Score Range | Interpretation      |
| ----------- | ------------------- |
| 0.0         | Objective / Factual |
| 1.0         | Highly Opinionated  |

---

### Focus Flag

A custom classification was created using Subjectivity scores to distinguish factual reviews from emotional reviews.

```python
focus_flag = "Focused" if subjectivity < 0.5 else "Opinion"
```

| Focus Flag | Meaning                                    |
| ---------- | ------------------------------------------ |
| Focused    | More factual and objective feedback        |
| Opinion    | More emotional and opinion-driven feedback |

---

### Sentiment Classification Logic

Reviews were classified into sentiment categories using their polarity scores.

```python
if score > 0.1:
    return "Positive"
elif score < -0.1:
    return "Negative"
else:
    return "Neutral"
```

This approach converts numerical sentiment scores into business-friendly categories that can be analyzed and visualized in Power BI dashboards.

---

## Python Sentiment Analysis Script

The following Python script was used to calculate polarity scores, subjectivity scores, focus flags, and sentiment labels for both customer and review datasets.

```python
import pandas as pd
from textblob import TextBlob

df_reviews = pd.read_csv("reviews.csv", encoding="ISO-8859-1")
df_customers = pd.read_csv("customer.csv", encoding="ISO-8859-1")

def analyze_sentiment(text):
    blob = TextBlob(str(text))
    polarity = blob.sentiment.polarity
    subjectivity = blob.sentiment.subjectivity
    focus_flag = "Focused" if subjectivity < 0.5 else "Opinion"
    return pd.Series([polarity, subjectivity, focus_flag])

df_reviews[["Polarity", "Subjectivity", "FocusFlag"]] = df_reviews["Full Messege"].apply(analyze_sentiment)
df_customers[["Polarity", "Subjectivity", "FocusFlag"]] = df_customers["Full Messege"].apply(analyze_sentiment)

def get_sentiment_label(score):
    if score > 0.1:
        return "Positive"
    elif score < -0.1:
        return "Negative"
    else:
        return "Neutral"

df_reviews["Sentiment"] = df_reviews["Polarity"].apply(get_sentiment_label)
df_customers["Sentiment"] = df_customers["Polarity"].apply(get_sentiment_label)

df_reviews.to_csv("reviews_final.csv", index=False, encoding="utf-8")
df_customers.to_csv("customers_final.csv", index=False, encoding="utf-8")
```

### Output Generated

The script generated the following sentiment fields:

* Polarity
* Subjectivity
* FocusFlag
* Sentiment Category (Positive, Neutral, Negative)

These outputs formed the foundation of the Customer Sentiment, Review Sentiment, and Reply Effectiveness dashboards developed in Power BI.

## Customer Segmentation Analysis (K-Means Clustering)

### Business Question

Can customers be grouped into distinct behavioral segments based on their engagement and spending patterns?

---

## Analysis

K-Means Clustering was used to segment customers using:

* Subscription Cycles Completed (Engagement)
* Subscription Line Price (Revenue Contribution)

The analysis identified four distinct customer groups with different purchasing and retention behaviors.

---

## Key Findings

### Cluster 1: High-Value Loyalists

* High engagement
* High spending
* Strong retention

These customers generate the most value and should be prioritized through loyalty and retention programs.

### Cluster 2: Occasional Buyers

* Moderate engagement
* Moderate spending

This segment represents an opportunity for upselling and increased engagement.

### Cluster 3: Trial Users

* Low subscription tenure
* Limited repeat purchases

Many customers enter this segment but fail to convert into long-term subscribers.

### Cluster 4: Price-Sensitive Churners

* Low engagement
* Low spending
* Highest churn risk

These customers are most likely to cancel and require targeted retention efforts.

---

## What the Visualization Tells Us

The clustering results show that customer behavior is not uniform.

A small group of loyal customers contributes most of the revenue, while a large portion of customers disengage after only a few subscription cycles.

The visualization also confirms that customers have different engagement levels, spending habits, and retention patterns, highlighting the need for personalized marketing and loyalty strategies rather than a one-size-fits-all approach.

---

## Key Insight

Customer retention and revenue growth can be improved by tailoring marketing campaigns, loyalty programs, and customer engagement strategies to the specific needs of each customer segment.
