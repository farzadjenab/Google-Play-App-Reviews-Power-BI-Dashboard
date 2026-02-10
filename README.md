# 📱 Google Play Reviews Dashboard

## 📋 Project Overview

Interactive Power BI dashboard analyzing Google Play Store app reviews for a **Password Manager** application. Tracks key metrics including total reviews, average ratings, developer response rates, and response times. Features sentiment analysis with rating categories and yearly trends to help improve app performance and user satisfaction.

---

## 📊 Dashboard Preview

![Dashboard Screenshot](image.png)

---

## 🎯 Key Performance Indicators (KPIs)

| KPI | Value | Description |
|-----|-------|-------------|
| **Total Reviews** | 161 | Total number of user reviews collected |
| **Average Rating** | 4.42 / 5 | Mean rating across all reviews |
| **Response Rate** | 31.06% | Percentage of reviews with developer response |
| **Avg Response Time** | 125 days | Average time to respond to user reviews |
| **Total Thumbs Up** | 314 | Total thumbs up received on reviews |

---

## 📈 Visualizations

### Page 1: Main Dashboard
- **Donut Chart** — Rating distribution by category (Positive / Neutral / Negative)
- **Bar Chart** — Developer response status (Yes / No)
- **Column Chart** — Total reviews by year
- **Column Chart** — Average rating trend by year
- **KPI Cards** — 5 key metrics displayed at the top

---

## 📂 Dataset Information

| Field | Description |
|-------|-------------|
| `review_id` | Unique identifier for each review |
| `user_name` | Name of the reviewer |
| `review_title` | Title of the review |
| `review_description` | Full text of the review |
| `rating` | Rating given (1-5 stars) |
| `thumbs_up` | Number of thumbs up on the review |
| `review_date` | Date the review was posted |
| `developer_response` | Developer's reply to the review |
| `developer_response_date` | Date of developer response |
| `appVersion` | App version at time of review |
| `language_code` | Language of the review |
| `country_code` | Country of the reviewer |

### Dataset Statistics
- **Total Records:** 161 reviews
- **Date Range:** 2019 – 2024
- **Source:** Google Play Store
- **File Format:** CSV
- **App Category:** Password Manager (Utility)

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|------|---------|
| **Power BI Desktop** | Dashboard creation & visualization |
| **DAX** | Calculated columns & measures |
| **Power Query** | Data cleaning & transformation |
| **CSV** | Raw data source format |

---

## 🔧 DAX Measures & Calculated Columns

### Calculated Columns
dax
-- Rating Category
Rating_Category = 
IF('GooglePlay_App_Data'[rating] >= 4, "Positive",
IF('GooglePlay_App_Data'[rating] = 3, "Neutral", "Negative"))

-- Has Response
Has_Response = 
IF(ISBLANK('GooglePlay_App_Data'[developer_response]), "No", "Yes")

-- Year Extraction
Year = YEAR('GooglePlay_App_Data'[review_date])

-- Response Time (Days)
Response_Time_Days = 
IF(
NOT(ISBLANK('GooglePlay_App_Data'[developer_response_date])),
DATEDIFF(
'GooglePlay_App_Data'[review_date],
'GooglePlay_App_Data'[developer_response_date],
DAY
),
BLANK()
)

### Measures

dax
-- Average Response Time
Avg_Response_Time = 
AVERAGE('GooglePlay_App_Data'[Response_Time_Days])

-- Response Rate
Response_Rate = 
DIVIDE(
COUNTROWS(FILTER('GooglePlay_App_Data', 'GooglePlay_App_Data'[Has_Response] = "Yes")),
COUNTROWS('GooglePlay_App_Data'),
0
) * 100

---

## 📊 Key Insights

1. **High Satisfaction Rate:** 85% of reviews are positive (4-5 stars), indicating strong user satisfaction
2. **Low Response Rate:** Only 31% of reviews received developer responses — room for improvement
3. **Delayed Responses:** Average response time of 125 days suggests need for faster engagement
4. **Consistent Quality:** Average rating of 4.42/5 maintained across multiple years
5. **Common Praise:** Users frequently mention simplicity, ease of use, and security
6. **Common Complaints:** Data loss during phone switching, backup issues, and account lockouts

---

## 🚀 How to Use

1. **Download** the `.pbix` file and `GooglePlay_App_Data.csv`
2. **Open** the `.pbix` file in Power BI Desktop
3. **Refresh** the data source if needed (update CSV file path)
4. **Interact** with charts by clicking on segments to filter data
5. **Use slicers** to filter by year or other dimensions

---

## 📁 Project Structure


📦 Google-Play-Reviews-Dashboard
 ┣ 📄 GooglePlay_App_Data.csv        # Raw dataset
 ┣ 📄 Dashboard.pbix                  # Power BI dashboard file
 ┣ 📄 README.md                       # Project documentation
 

---

## 👤 Author

Farzad Moharami Jenab

---

## 📜 License

This project is for educational and analytical purposes only. The review data is sourced from publicly available Google Play Store reviews.

---

## ⭐ Acknowledgments

- Google Play Store for the review data
- Microsoft Power BI for the visualization platform


