[Glassdoor Jobs Scraper](https://apify.com/devcake/glassdoor-jobs-scraper?fpr=data)

# 💼 GlassDoor Scraper - Jobs, Reviews, Salaries & Interview Questions

**Extract GlassDoor data at scale**: job listings, employee salaries, company reviews, ratings, and real interview questions. The most comprehensive GlassDoor crawler for recruitment intelligence, salary benchmarking, compensation analysis, and employer research. **Now supports 15+ international GlassDoor domains with multi-language extraction!**

---

## 🎯 What It Does

This GlassDoor data extraction tool scrapes comprehensive workplace intelligence from the world's largest job and company review platform (glassdoor.com). Perfect for salary research, job market analysis, employer branding analysis, and competitive intelligence gathering.

**Four Powerful Scraping Modes:**

- 🔍 **Jobs** - Extract job listings with salary ranges, company ratings, benefits, and requirements
- 💰 **Salaries** - Scrape detailed salary data with base pay, bonuses, and percentile distributions by company and job title
- ⭐ **Reviews** - Scrape employee reviews with pros, cons, culture ratings, and management feedback
- 💬 **Interviews** - Get real interview questions, difficulty ratings, and candidate experiences

**Unique Features:**

- 🔗 **URL-Based Scraping** - Paste any GlassDoor employer URL and auto-detect employer ID and language
- 🌍 **Multi-Language Support** - Extract reviews and interviews in original language from 15+ GlassDoor domains (France, Germany, Spain, UK, and more)
- ⚡ **Unified Workflow** - Run in "All" mode to automatically extract employer IDs from job listings and fetch their reviews and interviews
- 📊 **Comprehensive Salary Data** - Get base pay, total compensation, bonus structures, and salary percentiles for informed salary negotiations

---

## 👥 Who It's For

- 🤝 **Recruiters & HR Teams** - Research companies, salary benchmarks, and interview processes for candidate preparation
- 💼 **Job Seekers** - Research salaries, prepare for interviews with real questions, and get insider company insights before applying
- 💵 **Salary Researchers & Compensation Analysts** - Extract salary data across companies and roles for compensation benchmarking and market analysis
- 🎓 **Career Coaches** - Provide data-driven advice on companies, roles, and compensation packages
- 📈 **Market Researchers** - Track hiring trends, workplace sentiment, and employer branding across industries
- 🏢 **Business Intelligence Teams** - Monitor competitor benefits, culture ratings, salary trends, and hiring patterns

---

## 💡 Use Cases

### 💰 Salary Research & Compensation Benchmarking

Extract detailed salary data with percentile distributions for informed compensation decisions. Perfect for HR teams setting competitive pay rates, recruiters benchmarking offers, or job seekers negotiating salaries with data-backed insights.

### 📊 Job Market Intelligence & Hiring Trends

Analyze salary trends across companies, locations, and job titles. Essential for understanding market rates, identifying high-paying employers, and tracking compensation changes over time.

### 🎯 Interview Preparation & Coaching

Access real interview questions and experiences by company and job title. Help candidates prepare with actual questions from successful applicants.

### 📈 Employer Brand Monitoring & Analysis

Monitor company reviews and ratings to understand employee sentiment. Track changes in culture scores and identify workplace trends over time.

### 🔍 Competitive Intelligence & Market Research

Compare benefits, culture ratings, salary ranges, and hiring patterns across competitors. Essential for strategic HR planning and talent acquisition strategy.

### 📋 Recruitment & Talent Acquisition Research

Research potential employers with comprehensive data on ratings, reviews, salaries, and interview processes. Make informed decisions about company culture fit and compensation expectations.

### 🌍 International Market Intelligence

Scrape reviews from local GlassDoor domains to understand employee sentiment in specific countries. Get insights in French, German, Spanish, and more.

---

## ⚡ Quick Start

1. 🔧 **Choose scraping mode** - Jobs, Salaries, Reviews, Interviews, or All combined
2. 📝 **Configure your search** - Add job keywords, employer URLs, or GlassDoor employer IDs
3. 🚀 **Run the scraper** - Get comprehensive workplace data in minutes

---

## ⚙️ Input Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| scrapeType | string | No | What to scrape: `jobs`, `salaries`, `reviews`, `interviews`, or `all` |
| searchQueries | array | No | Job search keywords (for jobs/salaries mode) |
| employerUrls | array | No | GlassDoor employer URLs - language auto-detected from domain |
| employerIds | array | No | GlassDoor employer IDs (alternative to URLs) |
| location | string | No | Location filter for jobs/salaries |
| maxPages | integer | No | Max pages per job/salary query (1-50) |
| countryId | string | No | US, UK, Canada, Australia, India, Germany, France, Spain, Netherlands |
| reviewPages | integer | No | Max review pages per employer (1-100) |
| interviewPages | integer | No | Max interview pages per employer (1-100) |
| minSalary | integer | No | Minimum salary filter (USD) |
| salarySort | string | No | Sort salaries by: `popular`, `highest_pay`, `most_reports` |
| remoteOk | boolean | No | Filter for remote jobs only |
| easyApplyOnly | boolean | No | Filter for Easy Apply jobs only |
| proxyConfiguration | object | No | Proxy settings (residential recommended) |

---

## 📝 Example

### 🔍 Input - Job Search

```
{
  "scrapeType": "jobs",
  "searchQueries": ["software engineer", "data scientist"],
  "location": "San Francisco",
  "maxPages": 3,
  "remoteOk": true
}
```

### 💼 Output - Job Listing

```
{
  "dataType": "job",
  "jobId": "1009234567890",
  "jobTitle": "Senior Software Engineer",
  "employerName": "Google",
  "employerId": 9079,
  "locationName": "Mountain View, CA",
  "payRange": "$150K - $250K",
  "salaryMin": 150000,
  "salaryMax": 250000,
  "overallRating": 4.4,
  "isRemote": true,
  "workLifeBalanceRating": 4.2,
  "cultureAndValuesRating": 4.3
}
```

### 💰 Input - Salary Search

```
{
  "scrapeType": "salaries",
  "searchQueries": ["Senior Python Developer", "Software Engineer"],
  "location": "New York",
  "maxPages": 5,
  "salarySort": "highest_pay"
}
```

### 💵 Output - Salary Data

```
{
  "dataType": "salary",
  "employerName": "Google",
  "employerId": 9079,
  "jobTitle": "Senior Python Developer",
  "location": "New York, NY",
  "totalPayMin": 180000,
  "totalPayMax": 320000,
  "totalPayMean": 245000,
  "basePayMin": 150000,
  "basePayMax": 260000,
  "basePayMean": 200000,
  "additionalPayMin": 30000,
  "additionalPayMax": 60000,
  "payPercentiles": {
    "p10": 175000,
    "p25": 200000,
    "p50": 245000,
    "p75": 290000,
    "p90": 315000
  },
  "payPeriod": "ANNUAL",
  "salaryCount": 127,
  "currency": "USD",
  "employerRating": 4.4
}
```

### 🌍 Input - Reviews from French GlassDoor

```
{
  "scrapeType": "reviews",
  "employerUrls": [
    "https://www.glassdoor.fr/Avis/Azae-Avis-E1360610.htm",
    "https://www.glassdoor.de/Bewertungen/Google-Bewertungen-E9079.htm"
  ],
  "reviewPages": 5
}
```

### ⭐ Output - French Review

```
{
  "dataType": "review",
  "reviewId": "123456789",
  "employerName": "Azae",
  "employerId": 1360610,
  "summary": "Excellente entreprise avec une belle culture",
  "pros": "Bonne ambiance, equipe sympa, management bienveillant",
  "cons": "Quelques defis d'organisation",
  "overallRating": 4,
  "reviewLanguage": "fra",
  "sourceDomain": "glassdoor.fr"
}
```

### 🎯 Input - Reviews & Interviews (US)

```
{
  "scrapeType": "all",
  "employerIds": ["9079"],
  "reviewPages": 5,
  "interviewPages": 5
}
```

### 💬 Output - Review

```
{
  "dataType": "review",
  "reviewId": "123456789",
  "employerName": "Google",
  "summary": "Great place to work with amazing perks",
  "pros": "Great benefits, smart colleagues, good work-life balance",
  "cons": "Can be competitive, some teams have long hours",
  "overallRating": 5,
  "jobTitle": "Software Engineer",
  "isCurrentEmployee": true,
  "reviewLanguage": "eng",
  "sourceDomain": "glassdoor.com"
}
```

### 🗣️ Output - Interview

```
{
  "dataType": "interview",
  "interviewId": "987654321",
  "employerName": "Google",
  "jobTitle": "Software Engineer",
  "difficulty": "Difficult",
  "outcome": "Received Offer",
  "experience": "Positive Experience",
  "interviewLanguage": "eng",
  "sourceDomain": "glassdoor.com",
  "questions": [
    {"question": "Design a system for real-time notifications"},
    {"question": "Explain your approach to debugging complex issues"}
  ]
}
```

---

## 🌍 Supported GlassDoor Domains

The scraper supports **15+ GlassDoor domains** worldwide with automatic language detection:

| Domain | Country | Language | TLD ID |
| --- | --- | --- | --- |
| 🇺🇸 glassdoor.com | United States | English | 1 |
| 🇫🇷 glassdoor.fr | France | French | 16 |
| 🇩🇪 glassdoor.de | Germany | German | 5 |
| 🇪🇸 glassdoor.es | Spain | Spanish | 10 |
| 🇬🇧 glassdoor.co.uk | United Kingdom | English | 3 |
| 🇮🇳 glassdoor.in | India | English | 4 |
| 🇦🇺 glassdoor.com.au | Australia | English | 6 |
| 🇨🇦 glassdoor.ca | Canada | English | 2 |
| 🇳🇱 glassdoor.nl | Netherlands | Dutch | 11 |
| 🇮🇪 glassdoor.ie | Ireland | English | 12 |
| 🇧🇪 glassdoor.be | Belgium | French | 17 |
| 🇨🇭 glassdoor.ch | Switzerland | German | 18 |
| 🇦🇹 glassdoor.at | Austria | German | 19 |
| 🇵🇹 glassdoor.pt | Portugal | Portuguese | 20 |
| 🇮🇹 glassdoor.it | Italy | Italian | 21 |