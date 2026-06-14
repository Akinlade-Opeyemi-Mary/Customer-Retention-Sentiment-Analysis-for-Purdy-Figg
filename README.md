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

📸 **Preview:**
![Rentention chart](https://github.com/Akinlade-Opeyemi-Mary/Customer-Retention-Sentiment-Analysis-for-Purdy-Figg/blob/c58d4314f6f366f4649ebe9f3df0649078195953/Retention%20and%20engagement%20chart.png)

![R based segement chart](https://github.com/Akinlade-Opeyemi-Mary/Customer-Retention-Sentiment-Analysis-for-Purdy-Figg/blob/b9087b2204b977e63dc61832fd256e113503bc4d/R%20based%20segement%20chart.png)

## 📊 Executive Dashboards & Analysis

This section highlights the key dashboards developed to analyze customer sentiment, review behavior, and reply effectiveness. The objective was to understand customer satisfaction levels, identify drivers of positive and negative sentiment, and evaluate how customer engagement impacts retention and loyalty.

---

### 1. Customer Sentiment Dashboard

**Objective:** Understand overall customer sentiment and identify the key factors driving customer satisfaction and dissatisfaction.

**Key Insights:**

* **Total Reviews:** 3,462
* **Positive Reviews:** 84.89%
* **Neutral Reviews:** 11.93%
* **Negative Reviews:** 3.18%
* **Net Sentiment Score:** 81.72%

#### Sentiment Drivers

* Scent & Fragrance recorded the strongest positive sentiment.
* Customer Service emerged as another major satisfaction driver.
* Delivery, Packaging, and Price-related concerns generated most negative feedback.

#### Theme Contribution Analysis

* All themes contributed positively to overall sentiment.
* Scent & Fragrance (0.90) and Team Experience (0.89) recorded the highest sentiment scores.
* Price & Value (0.47) and Other (0.36) recorded the lowest sentiment contributions.

**Takeaway:** Customers are highly satisfied with Purdy & Figg's products and service experience. However, addressing delivery, packaging, and pricing concerns presents an opportunity to further improve customer satisfaction and reduce churn.

![Customer Sentiment Dashboard](https://github.com/Akinlade-Opeyemi-Mary/Customer-Retention-Sentiment-Analysis-for-Purdy-Figg/blob/92bfa5b9e94f25c5654ba44f22b653905b962145/Customer%20Sentiment%20Dashbord.PNG)

---

### 2. Review Sentiment Dashboard

**Objective:** Analyze how customers express their experiences and identify the themes that drive emotional engagement.

**Key Insights:**

* Positive reviews are concentrated around Scent & Fragrance and Customer Service.
* Average Subjectivity Score: 0.60
* Reviews are largely emotion-driven rather than purely factual.
* Team Experience and Scent & Fragrance recorded the highest polarity scores.

#### Review Emotion Analysis

* Customers frequently express personal experiences and emotions when discussing products and services.
* Emotional engagement is strongest around product quality and customer interactions.

#### Review Length vs Emotion

* Longer reviews tend to contain complaints, concerns, or detailed feedback.
* Shorter reviews are generally associated with positive experiences and quick expressions of satisfaction.

**Takeaway:** Customer feedback is strongly influenced by emotional experiences. Positive product experiences create strong emotional connections, while dissatisfied customers provide more detailed explanations of their concerns.

![Review Sentiment Dashboard](https://github.com/Akinlade-Opeyemi-Mary/Customer-Retention-Sentiment-Analysis-for-Purdy-Figg/blob/a261c0dc64e9cc7c96e58faeaf9e4cecfe02857d/Review%20Sentiment%20Dashbord.PNG)

---

### 3. Reply Effectiveness Dashboard

**Objective:** Measure how business responses influence customer sentiment and support customer relationship recovery.

**Key Insights:**

* **Total Reviews:** 3,462
* **Replied Reviews:** 2,803
* **Non-Replied Reviews:** 659
* **Reply Rate:** 80.96%

#### Reply Rate by Theme

* Customer Service and Subscription/Billing received the highest response rates.
* High response coverage demonstrates strong customer engagement efforts.

#### Sentiment Recovery Analysis

* Reviews that received responses showed significantly better sentiment outcomes than reviews without responses.
* Customer responses contributed positively to sentiment recovery across multiple themes.

#### Average Sentiment Improvement After Reply

| Theme             | With Reply | Without Reply |
| ----------------- | ---------- | ------------- |
| Customer Service  | 0.91       | -0.91         |
| Delivery/Postage  | 0.87       | -0.89         |
| Packaging/Trigger | 0.95       | -0.95         |
| Scent/Fragrance   | 0.97       | -0.95         |
| Team/Experience   | 0.94       | -0.92         |

**Takeaway:** Responding to customer reviews significantly improves sentiment outcomes. Prompt and thoughtful responses help rebuild trust, improve customer experience, and strengthen customer relationships.

![Review Sentiment Dashboard](https://github.com/Akinlade-Opeyemi-Mary/Customer-Retention-Sentiment-Analysis-for-Purdy-Figg/blob/4a70fe491af34d5215f0f7355aaee4d170f72a8f/Reply%20Effectivenesss%20Dashbord.PNG)

---
### Executive Summary of Findings

Across all dashboards, three major patterns emerged:

* Customers consistently praise product quality, fragrance, and customer service.
* Delivery, packaging, and pricing issues represent the primary sources of dissatisfaction.
* Active customer engagement through review responses significantly improves sentiment recovery and customer trust.

These findings demonstrate that while Purdy & Figg has built a strong customer experience foundation, opportunities remain to improve retention and loyalty through enhanced fulfillment processes, personalized engagement, and proactive customer support.

---

### Key Insight

Customer retention and revenue growth can be improved by tailoring marketing campaigns, loyalty programs, and customer engagement strategies to the specific needs of each customer segment.

## Strategic Recommendations

Based on the findings from customer sentiment analysis, customer segmentation, and reply effectiveness analysis, the following strategic actions are recommended to improve customer retention, strengthen loyalty, and support sustainable subscription growth at Purdy & Figg.

---

### 1. Improve Delivery & Fulfillment Experience

* Investigate recurring delivery and postage complaints.
* Improve shipping communication and tracking visibility.
* Monitor delivery performance metrics regularly.

**Business Impact:**
Reduces one of the most common sources of negative sentiment and improves overall customer satisfaction.

---

### 2. Enhance Customer Retention Programs

* Introduce loyalty rewards for long-term subscribers.
* Provide incentives for customers who complete additional subscription cycles.
* Develop retention campaigns targeting customers at risk of cancellation.

**Business Impact:**
Encourages longer subscription tenure and increases customer lifetime value.

---

### 3. Implement Personalized Marketing Strategies

* Leverage customer segmentation insights to tailor messaging and promotions.
* Create targeted campaigns for High-Value Loyalists, Occasional Buyers, Trial Users, and Price-Sensitive Churners.
* Align product recommendations with customer preferences.

**Business Impact:**
Improves marketing efficiency, customer engagement, and conversion rates.

---

### 4. Strengthen Customer Engagement Through Review Responses

* Maintain the current high review response rate.
* Prioritize responses to negative and neutral reviews.
* Establish response-time standards for customer feedback.

**Business Impact:**
Improves sentiment recovery, strengthens customer trust, and enhances brand perception.

---

### 5. Optimize Product & Pricing Strategy

* Promote high-performing products such as Spring and Mixed fragrances.
* Review customer concerns related to price and perceived value.
* Test product bundles and personalized offers to increase perceived value.

**Business Impact:**
Improves customer satisfaction while supporting revenue growth and retention.

---

## Strategic Outcome

By implementing these recommendations, Purdy & Figg can:

* Improve customer retention rates
* Increase customer lifetime value (CLV)
* Reduce subscription churn
* Enhance customer satisfaction
* Improve marketing effectiveness
* Strengthen customer loyalty
* Support sustainable recurring revenue growth

**Long-term growth will be driven not only by acquiring new customers but by retaining existing customers and creating stronger customer relationships.**

---

## Key Strategic Insight

Across all dashboards, the analysis demonstrates that Purdy & Figg's greatest opportunity lies in strengthening customer retention rather than customer acquisition.

While overall customer sentiment remains highly positive, customer segmentation revealed that many customers disengage after only a few subscription cycles. At the same time, sentiment analysis showed that product quality, fragrance, and customer service are powerful loyalty drivers, while delivery, packaging, and pricing concerns contribute most to dissatisfaction.

The findings further demonstrate that proactive customer engagement, particularly through review responses, plays a critical role in rebuilding trust and improving customer sentiment.

---

## Conclusion

This analysis combined customer sentiment analysis, customer segmentation, and customer engagement metrics to provide a comprehensive view of customer behavior at Purdy & Figg.

The findings revealed that customers generally have a highly positive perception of the brand, with an overall Net Sentiment Score of 81.72% and strong appreciation for product quality, fragrance, and customer service. However, retention analysis showed that many customers leave before realizing the full value of their subscription, limiting long-term customer lifetime value.

Customer segmentation identified distinct behavioral groups with different engagement and retention patterns, highlighting the need for personalized marketing and loyalty strategies. Additionally, reply effectiveness analysis demonstrated that responding to customer feedback significantly improves sentiment outcomes and strengthens customer relationships.

By improving delivery experiences, strengthening loyalty initiatives, personalizing customer engagement, and maintaining proactive communication, Purdy & Figg has a clear opportunity to increase retention, reduce churn, and drive sustainable long-term growth.

Overall, this project demonstrates how customer analytics, sentiment analysis, and behavioral segmentation can transform customer feedback into actionable business strategies that improve both customer experience and business performance.

## 👤 Author | Connect With Me

**Akinlade Opeyemi Mary**  
📊 Data Analyst | Business Intelligence | Credit Risk Analysis  

🔗 **LinkedIn:** [Akinlade Opeyemi Mary](https://www.linkedin.com/in/opeyemiakinlademary)  
📧 **Email:** akinladeopeyemi36@gmail.com
