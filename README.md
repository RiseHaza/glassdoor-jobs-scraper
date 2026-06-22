[Glassdoor Jobs Scraper](https://apify.com/kaix/glassdoor-jobs-scraper?fpr=data)

# Glassdoor Jobs Scraper

Scrape job listings from Glassdoor by keyword and location, or from any employer page or search URL. Full job descriptions, salary data, employer profiles with CEO and ratings, geo coordinates, skills, and education requirements. Structured JSON output.

## Why use this scraper?

- Full HTML job description, not just a snippet
- Salary range (min/median/max), currency, period, and source (employer-provided vs Glassdoor estimate)
- Employer profile: size, revenue, HQ, industry, CEO, year founded, website
- 8 employer rating categories: overall, career opportunities, comp & benefits, culture, management, work-life balance, CEO approval, recommend to friend
- Geo coordinates (lat/lng), city, state, country for every listing
- Extracted skills, education requirements, years of experience
- Job type, remote work type, easy apply flag, expired status
- Search by keyword and location, or paste any employer/search URL
- Filter by date posted, job type, seniority, remote work, salary, company size, and more

## Use cases

- Build a job board or aggregator with rich structured data
- Track open positions at specific companies over time
- Analyze salary ranges by role, location, or company
- Feed job descriptions into NLP pipelines for skill extraction
- Compare employer profiles and ratings across companies

## How to use

### Search by keyword + location

```
{
  "keyword": "Software Engineer",
  "location": "San Francisco, CA"
}
```

### Search with filters

```
{
  "keyword": "Software Engineer",
  "location": "San Francisco, CA",
  "fromAge": 7,
  "jobType": ["fulltime"],
  "remoteWorkType": ["1"],
  "seniorityType": ["midseniorlevel"],
  "minSalary": 100000,
  "maxJobs": 50
}
```

### Search by keyword only (all locations)

```
{
  "keyword": "Data Scientist",
  "maxJobs": 50
}
```

### Scrape a specific company

```
{
  "urls": ["https://www.glassdoor.com/Jobs/Google-Jobs-E9079.htm"]
}
```

### Scrape multiple companies

```
{
  "urls": [
    "https://www.glassdoor.com/Jobs/Google-Jobs-E9079.htm",
    "https://www.glassdoor.com/Jobs/Meta-Jobs-E40772.htm"
  ],
  "maxJobs": 50
}
```

### Scrape a search results URL

```
{
  "urls": [
    "https://www.glassdoor.com/Job/san-francisco-software-engineer-jobs-SRCH_IL.0,13_IC1147401_KO14,31.htm"
  ]
}
```

### Combine keyword + URL targets

```
{
  "keyword": "Product Manager",
  "location": "New York",
  "urls": ["https://www.glassdoor.com/Jobs/Google-Jobs-E9079.htm"],
  "maxJobs": 30
}
```

## Input

**Search:**

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| **keyword** | string | — | Job title, skill, or company name |
| **location** | string | — | City, state, or country |

**Filters:**

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| **maxJobs** | number | 20 | Maximum results per target. Set to 0 for no limit. |
| **fromAge** | number | any | Posted within 1, 3, 7, 14, or 30 days |
| **jobType** | string[] | any | `fulltime`, `parttime`, `contract`, `internship`, `temporary` |
| **seniorityType** | string[] | any | `entrylevel`, `midseniorlevel`, `director`, `executive` |
| **remoteWorkType** | string[] | any | `1` (Remote), `2` (Hybrid), `3` (On-site) |
| **easyApply** | boolean | false | Only Easy Apply jobs |
| **minSalary** | number | — | Minimum annual salary (local currency) |
| **maxSalary** | number | — | Maximum annual salary (local currency) |
| **radius** | number | — | Search radius in miles: 5, 10, 15, 25, 50, 100 |
| **employerSizes** | string[] | any | `1to50`, `51to200`, `201to500`, `501to1000`, `1001to5000`, `5001to10000`, `10001+` |
| **postedBy** | string[] | any | `jobPoster` (Employer), `staffingAgency` (Staffing Agency) |

> Filters apply to all targets (keyword search and URLs).

**URL Lookup:**

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| **urls** | string[] | — | Glassdoor employer pages (`/Jobs/Google-Jobs-E9079.htm`) or search URLs. Optional if keyword is provided. |

## Output

Each job is a single JSON object:

### Job profile

```
{
  "jobId": 1010094160099,
  "url": "https://www.glassdoor.com/job-listing/administrative-business-partner-ii-metro-data-centers-google-JV_IC1155091_KO0,53_KE54,60.htm?jl=1010094160099",
  "profile": {
    "title": "Administrative Business Partner II, Metro Data Centers",
    "normalizedTitle": "hr business partner",
    "description": "<div><h3 class=\"jobSectionHeader\"><b>Minimum qualifications:</b></h3><ul>...",
    "descriptionSnippet": "Perform administrative tasks (including managing calendars, booking travel, expenses, and scheduling facilities or equipment), and planning, managing, and…",
    "ageInDays": 13,
    "discoverDate": "2026-04-08T00:00:00",
    "expired": false,
    "easyApply": false,
    "jobType": ["Full-time"],
    "remoteWorkTypes": [],
    "skills": ["Expense management", "Facilities management", "Project management", "Calendar management", "Communication skills"],
    "education": [],
    "yearsOfExperience": "2"
  }
}
```

### Location

```
{
  "location": {
    "name": "Moncks Corner, SC",
    "type": "C",
    "city": "Moncks Corner, SC",
    "state": "South Carolina",
    "country": "United States",
    "lat": 33.19583,
    "lng": -80.01333
  }
}
```

### Compensation

```
{
  "compensation": {
    "salaryMin": 79000,
    "salaryMax": 112000,
    "salaryMedian": 95500,
    "currency": "USD",
    "period": "ANNUAL",
    "source": "EMPLOYER_PROVIDED"
  }
}
```

### Employer

```
{
  "employer": {
    "id": 9079,
    "name": "Google Inc.",
    "shortName": "Google",
    "logoUrl": "https://media.glassdoor.com/sql/9079/google-squarelogo-1441130773284.png",
    "size": "10000+ Employees",
    "sizeCategory": "GIANT",
    "type": "Company - Public",
    "revenue": "$10+ billion (USD)",
    "yearFounded": 1998,
    "headquarters": "Mountain View, CA",
    "industry": "Internet & Web Services",
    "sector": "Information Technology",
    "website": "https://goo.gle/4ehVuXi",
    "ceo": {
      "name": "Sundar Pichai",
      "photoUrl": "https://media.glassdoor.com/people/sql/9079/google-sundar-pichai.png"
    },
    "ratings": {
      "overall": 4.4,
      "careerOpportunities": 4.2,
      "compensationAndBenefits": 4.5,
      "cultureAndValues": 4.2,
      "seniorManagement": 3.9,
      "workLifeBalance": 4.2,
      "ceoRating": 0.82,
      "recommendToFriend": 0.87
    }
  }
}
```

### Meta

```
{
  "meta": {
    "seoJobLink": "https://www.glassdoor.com/job-listing/administrative-business-partner-ii-metro-data-centers-google-JV_IC1155091_KO0,53_KE54,60.htm?jl=1010094160099",
    "scrapedAt": "2026-04-22T10:55:07.341Z"
  }
}
```

## Limitations

- Employer data (CEO, ratings, industry, etc.) is the same for all jobs at the same company.
- `maxJobs` is per target, not total across all targets.