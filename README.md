[Glassdoor Jobs Scraper](https://apify.com/fatihtahta/glassdoor-jobs-scraper?fpr=data)

# Enterprise Grade Glassdoor Jobs Scraper

**Slug:** `fatihtahta/glassdoor-jobs-scraper`

## Overview

Enterprise Grade Glassdoor Jobs Scraper collects structured job listing data from Glassdoor, including job titles, descriptions, job URLs, locations, compensation details, company information, ratings, and employer insight fields when available. It supports both direct collection from Glassdoor URLs and broader discovery from keyword-based searches with reusable filters. [Glassdoor](https://www.glassdoor.com) is a widely used destination for job and employer research, which makes its listings useful for hiring analysis, market intelligence, company research, and operational reporting. The actor automates collection into consistent JSON records so teams can work from one predictable output format instead of manual copying and cleanup. This saves time for analysts, operators, and developers who need fresh job data on a recurring basis.

## Why Use This Actor

- **Market research and analytics:** Analyze hiring demand, salary ranges, employer ratings, and role distribution across industries, cities, and time periods.
- **Product and content teams:** Find trending roles, employer signals, and location patterns to inform content calendars, landing pages, comparison pages, and editorial research.
- **Developers and data engineering pipelines:** Feed structured job data into warehouses, dashboards, ETL jobs, internal APIs, and enrichment workflows without custom post-processing.
- **Lead generation and enrichment:** Add current job, company, compensation, and location context to account lists, prospecting datasets, and CRM records.
- **Monitoring and competitive tracking:** Track which employers are hiring, where they are hiring, and how job mix changes over time for selected markets or competitor groups.

## Input Parameters

Provide any combination of URLs, queries, and filters to control what gets collected.

| Parameter | Type | Description | Default |
| --- | --- | --- | --- |
| `startUrls` | `array<string>` | One or more Glassdoor URLs to collect directly. You can mix search result pages, category pages, and individual job listing pages in the same run. | `–` |
| `queries` | `array<string>` | One or more search keywords to run on Glassdoor, such as job titles, brands, locations, or categories. | `–` |
| `location` | `string` | Location text applied to every query, such as `San Francisco, CA`, `new york`, or `10001`. | `–` |
| `datePosted` | `string` | Date filter for query-based runs. Allowed values: `1` = Last 24 hours, `3` = Last 3 days, `7` = Last 7 days, `14` = Last 14 days. | `–` |
| `minRating` | `string` | Minimum company rating filter. Allowed values: `1` = 4 stars & up, `2` = 3 stars & up, `3` = 2 stars & up, `4` = 1 star & up. | `–` |
| `minSalary` | `integer` | Minimum salary filter applied to every query. | `–` |
| `maxSalary` | `integer` | Maximum salary filter applied to every query. | `–` |
| `jobType` | `string` | Job type filter. Allowed values: `CF3CP` = Full-time, `5QWDV` = Permanent, `75GKK` = Part-time, `NJXCK` = Contract, `T9BXE` = Fixed Term Contract, `VDTG7` = Internship. | `–` |
| `radius` | `string` | Search radius in miles. Allowed values: `10`, `20`, `30`, `50`, `100`, `200`. | `–` |
| `industryNid` | `string` | Industry filter. Allowed values: `10002` = Aerospace & Defense, `10019` = Energy, Mining & Utilities, `10010` = Finance, `10012` = Healthcare, `10026` = Human Resources and Staffing, `10013` = Information Technology, `10014` = Insurance, `10006` = Management and Consulting, `10015` = Manufacturing, `10016` = Media and Communications, `10024` = Transportation and Logistics. | `–` |
| `sgocId` | `string` | Job function filter. Allowed values: `1003` = Business, `1004` = Consulting, `1007` = Engineering, `1011` = Information Technology, `1016` = Operations, `1017` = Other, `1018` = Product & Project Management, `1019` = Research & Science, `1022` = Skilled Labor & Manufacturing, `1023` = Transportation. | `–` |
| `seniorityType` | `string` | Seniority filter text, for example `midseniorlevel`. | `–` |
| `employerSize` | `string` | Employer size filter. Allowed values: `1` = 1-200 employees, `2` = 201-500 employees, `3` = 501-1000 employees, `4` = 1001-5000 employees, `5` = 5001+ employees. | `–` |
| `sortBy` | `string` | Search result sort order. Allowed values: `relevant_desc` = Most relevant, `date_desc` = Most recent. | `–` |
| `applicationType` | `boolean` | When enabled, collects only jobs marked as Easy Apply. | `–` |
| `remoteWorkType` | `boolean` | When enabled, collects only remote jobs. | `–` |
| `limit` | `integer` | Maximum number of listings to save per query. Use smaller values for testing and larger values for broader collection. | `50000` |

## Example Input

```
{
  "queries": [
    "software engineer",
    "devops engineer"
  ],
  "location": "New York, NY",
  "datePosted": "7",
  "minSalary": 100000,
  "remoteWorkType": true,
  "sortBy": "date_desc",
  "limit": 500
}
```

## Output

### 6.1 Output destination

The actor writes results to an Apify dataset as JSON records. And the dataset is designed for direct consumption by analytics tools, ETL pipelines, and downstream APIs without post-processing.

### 6.2 Record envelope (all items)

The following identifiers are stable across all records:

- **type** *(string, required)*
- **id** *(number, required)*
- **url** *(string, required)*

Recommended idempotency key: `type + ":" + id`

Use this key for deduplication and upserts when the same listing appears in multiple runs, search seeds, or source URLs.

### 6.3 Examples

Example: Standard Output:

```
{
    "listingId": 1010077745431,
    "jobTitle": "Change Management and Training Associate",
    "jobPosting": {
      "descriptionHtml": "Assist in designing and implementing training programs and content tailored to diverse roles and business units, ensuring employees are equipped to utilize…",
      "descriptionText": "Assist in designing and implementing training programs and content tailored to diverse roles and business units, ensuring employees are equipped to utilize…",
      "jobPageUrl": "https://www.glassdoor.com/partner/jobListing.htm?ao=1136043&cb=1774685542072&cs=1_1fac977c&guid=0000019d33805554b9e6662bdfff8cad&jobListingId=1010077745431&jrtk=5-yul1-0-1jkpo0lcgjn2c800-179576c7f04d16b0&pos=103&s=58&src=GD_JOB_AD&t=SR&vt=w",
      "seoJobPageUrl": "https://www.glassdoor.com/job-listing/change-management-and-training-associate-morgan-stanley-JV_IC1132348_KO0,40_KE41,55.htm?jl=1010077745431",
      "listingAgeDays": 2,
      "isExpired": false,
      "hasEasyApply": false,
      "importConfigId": 322429,
      "titleId": 0
    },
    "jobTaxonomy": {
      "normalizedTitle": "trainer",
      "occupationName": "trainer",
      "occupationId": 100518,
      "occupations": [
        {
          "key": "4DNWZ"
        },
        {
          "key": "EHPW9"
        },
        {
          "key": "HBYNN"
        },
        {
          "key": "MGTWW"
        },
        {
          "key": "N3YNG"
        },
        {
          "key": "YWAE8"
        }
      ],
      "countryId": 1,
      "searchAttributes": {
        "extractedJobAttributes": [
          {
            "key": "3A8KY",
            "value": "Commission pay"
          },
          {
            "key": "A7SFW",
            "value": "Writing skills"
          },
          {
            "key": "B4GAW",
            "value": "Content writing"
          },
          {
            "key": "CF3CP",
            "value": "Full-time"
          },
          {
            "key": "DN563",
            "value": "Mid-level"
          },
          {
            "key": "FDAXP",
            "value": "Change management"
          },
          {
            "key": "G9RC5",
            "value": "Key Performance Indicators"
          },
          {
            "key": "GGXEU",
            "value": "Analysis skills"
          },
          {
            "key": "HFDVW",
            "value": "Bachelor's degree"
          },
          {
            "key": "HT6WW",
            "value": "Machine learning"
          },
          {
            "key": "PERR8",
            "value": "Developing new training programs"
          },
          {
            "key": "R6MKU",
            "value": "Financial services"
          },
          {
            "key": "T3K5N",
            "value": "Training & development"
          },
          {
            "key": "TV45R",
            "value": "Employee engagement"
          },
          {
            "key": "UJF52",
            "value": "AI"
          },
          {
            "key": "UN5V2",
            "value": "Cross-functional collaboration"
          },
          {
            "key": "WGZWZ",
            "value": "Corporate instructional development"
          },
          {
            "key": "WSBNK",
            "value": "Communication skills"
          },
          {
            "key": "WZ42A",
            "value": "Project stakeholder communication"
          },
          {
            "key": "Y3M6U",
            "value": "Stakeholder relationship building"
          },
          {
            "key": "Y6B2U",
            "value": "Generative AI"
          },
          {
            "key": "Y8657",
            "value": "Cross-functional communication"
          },
          {
            "key": "YM24M",
            "value": "Training delivery"
          },
          {
            "key": "ZN6XN",
            "value": "Stakeholder management"
          }
        ],
        "skills": [
          "A7SFW",
          "FDAXP",
          "GGXEU",
          "HT6WW",
          "R6MKU",
          "T3K5N",
          "UJF52",
          "WSBNK"
        ]
      }
    },
    "jobLocation": {
      "locationId": 1132348,
      "locationName": "New York, NY",
      "locationType": "C",
      "location": {
        "id": 1132348,
        "name": "New York, NY",
        "type": "C"
      }
    },
    "compensation": {
      "currency": "USD",
      "payPeriod": "ANNUAL",
      "salarySource": "EMPLOYER_PROVIDED",
      "range": {
        "p10": 90000,
        "p50": 122500,
        "p90": 155000
      },
      "searchMidpoint": 122500
    },
    "company": {
      "companyId": 2282,
      "companyName": "Morgan Stanley",
      "legalName": "Morgan Stanley",
      "shortName": "Morgan Stanley",
      "logoUrl": "https://media.glassdoor.com/sql/2282/morgan-stanley-squareLogo-1670774499083.png",
      "overallRating": 3.9,
      "ratings": {
        "overallRating": 3.9
      },
      "overview": {
        "shortName": "Morgan Stanley",
        "squareLogoUrl": "https://media.glassdoor.com/sql/2282/morgan-stanley-squareLogo-1670774499083.png"
      },
      "recognitions": [
        {
          "isCurrent": true
        },
        {
          "isCurrent": true
        }
      ]
    },
    "platformMetadata": {
      "adOrderId": 1136043,
      "jobResultTrackingKey": "5-yul1-0-1jkpo0lcgjn2c800-179576c7f04d16b0",
      "isSponsoredEmployer": false,
      "isSponsoredJob": false,
      "adminDetails": {
        "userEligibleForAdminJobDetails": false
      }
    },
    "sourceMetadata": {
      "seed": {
        "id": "3893d2983777",
        "type": "query",
        "value": "{\"filters\":{\"datePosted\":\"3\",\"minRating\":\"2\",\"minSalary\":\"40000\"},\"location\":\"new york\",\"query\":\"software\"}"
      },
      "sourceUrl": "https://www.glassdoor.com/job-search-next/bff/jobSearchResultsQuery",
      "recordUrl": "https://www.glassdoor.com/job-listing/change-management-and-training-associate-morgan-stanley-JV_IC1132348_KO0,40_KE41,55.htm?jl=1010077745431",
      "pageIndex": 1,
      "scrapedAt": "2026-03-28T08:12:22.446547Z",
      "searchListingSnapshot": {
        "listingId": "1010077745431",
        "jobTitle": "Change Management and Training Associate",
        "recordUrl": "https://www.glassdoor.com/job-listing/change-management-and-training-associate-morgan-stanley-JV_IC1132348_KO0,40_KE41,55.htm?jl=1010077745431",
        "jobPageUrl": "https://www.glassdoor.com/partner/jobListing.htm?ao=1136043&cb=1774685542072&cs=1_1fac977c&guid=0000019d33805554b9e6662bdfff8cad&jobListingId=1010077745431&jrtk=5-yul1-0-1jkpo0lcgjn2c800-179576c7f04d16b0&pos=103&s=58&src=GD_JOB_AD&t=SR&vt=w",
        "companyName": "Morgan Stanley",
        "locationName": "New York, NY",
        "currency": "USD",
        "payMidpoint": 122500,
        "payPeriod": "ANNUAL",
        "salarySource": "EMPLOYER_PROVIDED",
        "hasEasyApply": false,
        "listingAgeDays": 2,
        "companyId": 2282,
        "companyRating": 3.9,
        "extractionStrategy": "api"
      }
    },
    "detailFetch": {
      "status": "skipped"
    }
  }
```

Example: Enriched Output

```
{
  "type": "job",
  "id": 1010024904229,
  "url": "https://www.glassdoor.com/job-listing/application-platform-devops-engineer-pasona-na-JV_IC1132348_KO0,36_KE37,46.htm?jl=1010024904229",
  "listingId": 1010024904229,
  "jobTitle": "Application Platform DevOps Engineer",
  "jobPosting": {
    "descriptionHtml": "<div><ul><li><b>Japanese language skills are highly preferred.</b></li><li><b>Experience of DevOps and CI/CD is required.</b></li></ul><p></p><p><b><br> Job Details</b></p><ul><li> <b>Job Title:</b> Application Platform / DevOps Engineer</li><li> <b>Working Location:</b> NY</li><li> <b>Working style: </b>Hybrid (Onsite preferred 2&ndash;3 days/week, flexible)</li><li> <b>Working Hours:</b> Full-time preferred (negotiable)</li><li> <b>Language: </b>English (Japanese is a plus)</li><li> <b>Pay Rate:</b> $48-53/hour</li><li> <b>Employment type:</b> Temp to Perm</li></ul><p></p><p><b><br> ︎Job Summary</b></p><p> We are looking for a versatile Application Platform / DevOps Engineer to support an IT organization within a Japanese financial services firm in the Americas.</p><p> This role focuses on application platform operations, development support, and migration initiatives, working closely with multiple application teams in an Agile environment.</p><p><b> This position requires a broad technical skill set, hands-on mindset, and the ability to flexibly support various tools and processes across the application lifecycle.</b></p><p></p><p><b><br> ︎ Key Responsibilities:</b></p><ul><li> Provide operational support for application platforms, including maintenance, troubleshooting, and incident response.</li><li> Support application development initiatives, including coordination with multiple application teams.</li><li> Manage and support DevOps, CI/CD pipelines, container-based environments, and release processes</li><li> Support frequent application releases in an Agile development environment</li><li> Utilize GitHub for module management and application operational support</li><li> Support front-office and middle-office applications across the Americas (primarily web-based and microservices)</li></ul><p></p><p><b><br> ︎ Required Qualifications &amp; Skills:</b></p><ul><li> Broad experience across application platform operations, development support, and migration projects</li><li> Strong understanding of the full SDLC, with hands-on experience completing at least two full development cycles</li><li> Experience working in Agile development environments with frequent releases</li><li> Ability to coordinate effectively with multiple application teams</li><li> Strong communication skills in English</li></ul><p></p><p><b><br> ︎Preferred Qualifications</b></p><ul><li> Experience with DevOps-related technologies such as:</li></ul><p> o GitHub / GitHub Actions</p><p> o CI/CD pipelines</p><p> o Container technologies (e.g., Docker, Kubernetes)</p><p> o Cloud platforms (AWS and/or Azure)</p><ul><li> Experience supporting financial services</li></ul><p></p><p><b><br> ﻿</b><b>*Knowledge of accounting and SAP is required.</b></p><ul><li><b>Spanish or Japanese language skills are highly preferred.</b></li></ul><p></p><p><br> A Japanese company is seeking a SAP Helpdesk Support.</p><p></p><p><br> Work Hours: 7 hours shifts （Morning shift : 9:00 A.M. to 5:00 P.M. / Late Shift 12:00 P.M. to 8:00 P.M., Monday through Friday except holidays.</p><p> Base Salary $60K～$72K</p><p> Work Location: Client&rsquo;s Onsite in NYC. (depends on the client&rsquo;s needs/policy/regulations, might be changed assign number of days for working at their Onsite.)</p><p></p><p><br> Job Description</p><p> This position is stationed at the client&rsquo;s site. However, might be assigned for Telecommuting as Hybrid, depending on the client&rsquo;s needs. Responsibilities include providing troubleshoots for SAP<i>.</i></p><p></p><p><br> Summary</p><p> Essential Job Functions:</p><p> 1. SAP helpdesk support in English/Spanish or Japanese language</p><p> 1) Trouble shooting</p><p> Technical support at on-site or by email or telephone or remote access tool</p><p> 2) Operation support</p><p> User support for SAP software</p><p> 3) Documentation (user manual, FAQ, user announcement)</p><p> 4) User Education</p><p> 5) Record work (Help) log</p><p> Miscellaneous Job :</p><p> 2.Translation</p><p> ・Translation and proofreading English/Spanish materials or English/Japanese materials</p><p></p><p><br> Job Requirements</p><p> a)Education</p><p> Associate or bachelor&rsquo;s degree in Computer Science, Information Technology, or a related field for SAP would be plus.</p><p> b)Business Travel</p><p> Yes (depends on client&rsquo;s needs)</p><p></p><p><br> To apply please email your resume to myamamoto@pasona.com</p></div>",
    "descriptionText": "Japanese language skills are highly preferred.\nExperience of DevOps and CI/CD is required.\nJob Details\nJob Title:\nApplication Platform / DevOps Engineer\nWorking Location:\nNY\nWorking style:\nHybrid (Onsite preferred 2–3 days/week, flexible)\nWorking Hours:\nFull-time preferred (negotiable)\nLanguage:\nEnglish (Japanese is a plus)\nPay Rate:\n$48-53/hour\nEmployment type:\nTemp to Perm\n︎Job Summary\nWe are looking for a versatile Application Platform / DevOps Engineer to support an IT organization within a Japanese financial services firm in the Americas.\nThis role focuses on application platform operations, development support, and migration initiatives, working closely with multiple application teams in an Agile environment.\nThis position requires a broad technical skill set, hands-on mindset, and the ability to flexibly support various tools and processes across the application lifecycle.\n︎ Key Responsibilities:\nProvide operational support for application platforms, including maintenance, troubleshooting, and incident response.\nSupport application development initiatives, including coordination with multiple application teams.\nManage and support DevOps, CI/CD pipelines, container-based environments, and release processes\nSupport frequent application releases in an Agile development environment\nUtilize GitHub for module management and application operational support\nSupport front-office and middle-office applications across the Americas (primarily web-based and microservices)\n︎ Required Qualifications & Skills:\nBroad experience across application platform operations, development support, and migration projects\nStrong understanding of the full SDLC, with hands-on experience completing at least two full development cycles\nExperience working in Agile development environments with frequent releases\nAbility to coordinate effectively with multiple application teams\nStrong communication skills in English\n︎Preferred Qualifications\nExperience with DevOps-related technologies such as:\no GitHub / GitHub Actions\no CI/CD pipelines\no Container technologies (e.g., Docker, Kubernetes)\no Cloud platforms (AWS and/or Azure)\nExperience supporting financial services\n﻿\n*Knowledge of accounting and SAP is required.\nSpanish or Japanese language skills are highly preferred.\nA Japanese company is seeking a SAP Helpdesk Support.\nWork Hours: 7 hours shifts （Morning shift : 9:00 A.M. to 5:00 P.M. / Late Shift 12:00 P.M. to 8:00 P.M., Monday through Friday except holidays.\nBase Salary $60K～$72K\nWork Location: Client’s Onsite in NYC. (depends on the client’s needs/policy/regulations, might be changed assign number of days for working at their Onsite.)\nJob Description\nThis position is stationed at the client’s site. However, might be assigned for Telecommuting as Hybrid, depending on the client’s needs. Responsibilities include providing troubleshoots for SAP\n.\nSummary\nEssential Job Functions:\nSAP helpdesk support in English/Spanish or Japanese language\n1) Trouble shooting\nTechnical support at on-site or by email or telephone or remote access tool\n2) Operation support\nUser support for SAP software\n3) Documentation (user manual, FAQ, user announcement)\n4) User Education\n5) Record work (Help) log\nMiscellaneous Job :\n2.Translation\n・Translation and proofreading English/Spanish materials or English/Japanese materials\nJob Requirements\na)Education\nAssociate or bachelor’s degree in Computer Science, Information Technology, or a related field for SAP would be plus.\nb)Business Travel\nYes (depends on client’s needs)\nTo apply please email your resume to myamamoto@pasona.com",
    "jobPageUrl": "https://www.glassdoor.com/partner/jobListing.htm?ao=1110586&cb=1773983005122&cpc=451933188B21919D&cs=1_b33d2003&guid=0000019d09a06b078f14733fcf925081&jobListingId=1010024904229&jrtk=5-yul1-0-1jk4q0qpsgmvh800-5ab88e2ae74b63b7---6NYlbfkN0BQ0BgX18I10G6uoQ7vFAhySPo543-EiU2WryMBkb_AmY7Ep3qJ4G2RmxulaXh7nbU_1Lr61cyIrEDpHiap53j9OyooCF3fxIUZMyqP7JxVtlvnasSpkfBq6L3m3S_5_dIbc8pGOMsvXEn2q1wYXRdG56LvvVGYUVZMUvOKL5mhiknyG5WDNg40vVYgEkAtOqdJVe9TSB9OBqityIMT3fsmEAP9fuLe9URVc2QRDX7MTPV8StW52v8tospit78O6bcXTs5P4J3HLSudq0dyKNcusGGiZSG6oGyVFj8FwJyfdHpm46L7u6lR16yu3TMj4nRf5w5OdvS_EgTmYYaTBVq4osSfWOmPzUiF5sjC-BH92sZadtK6EoaJT-pjpm3RoQelE9cL-zxDBFtrg0SZfO86Ke9HVyuPp5I5XcjjXML8DCZR9Joi183gotQNHS59fDtfCArlBFurcrqcK8sNSjC72HuBaAVojXmREmfmAsbrtweZpUXe8l6Wx3fyRA2eeq71s0hivMS7EZG7qgApcYsIcUDsHTgmGtwD9AVqsinxcqSIUdD8RURPGeaKpVnqkQFWAOz3OjmAgDhLcd6pxYSDmuhqNsvGz85uj7NWDlqb85X6v7HVPm2X0wHXrvnm-hG5m9SZMQB-z5sAkyTKAKJKu85eUQH8HuM0aiao3vcYxNDT9d1Jc7Vz2Bf8XWjgV-puoaXPAGag8u18anrduIo2gZZGdBFLYBejoQHSn68RcFV8PU7GAjEyGyrgJzb5W_3nOlAeYoy8bhugwgOgXTrqsYXGlSQ74Bl3VlQKVEClUZ0CpliJ0URpmBhYlzQUUAO7Nv93Zpw3qubObujFuWNwNFI6EAC5d-y-zUucM-2ewmM0-jJphf-l&pos=104&s=58&src=GD_JOB_AD&t=SR&vt=w",
    "seoJobPageUrl": "https://www.glassdoor.com/job-listing/application-platform-devops-engineer-pasona-na-JV_IC1132348_KO0,36_KE37,46.htm?jl=1010024904229",
    "applyUrl": "https://www.glassdoor.com/partner/jobListing.htm?ao=1110586&cb=1773983005122&cpc=451933188B21919D&cs=1_9d15e368&guid=0000019d09a06b078f14733fcf925081&jobListingId=1010024904229&jrtk=5-yul1-3-1jk4q0uc9294hg00-1jk4q0qpsgmvh800---6NYlbfkN0BQ0BgX18I10G6uoQ7vFAhySPo543-EiU2WryMBkb_AmY7Ep3qJ4G2RmxulaXh7nbU_1Lr61cyIrEDpHiap53j9OyooCF3fxIUZMyqP7JxVtlvnasSpkfBq6L3m3S_5_dIbc8pGOMsvXEn2q1wYXRdG56LvvVGYUVZMUvOKL5mhiknyG5WDNg40vVYgEkAtOqdJVe9TSB9OBqityIMT3fsmEAP9fuLe9URVc2QRDX7MTPV8StW52v8tospit78O6bcXTs5P4J3HLSudq0dyKNcusGGiZSG6oGyVFj8FwJyfdHpm46L7u6lR16yu3TMj4nRf5w5OdvS_EgTmYYaTBVq4osSfWOmPzUiF5sjC-BH92sZadtK6EoaJT-pjpm3RoQelE9cL-zxDBFtrg0SZfO86Ke9HVyuPp5I5XcjjXML8DCZR9Joi183gotQNHS59fDtfCArlBFurcrqcK8sNSjC72HuBaAVojXmREmfmAsbrtweZpUXe8l6Wx3fyRA2eeq71s0hivMS7EZG7qgApcYsIcUDsHTgmGtwD9AVqsinxcqSIUdD8RURPGeaKpVnqkQFWAOz3OjmAgDhLcd6pxYSDmuhqNsvGz85uj7NWDlqb85X6v7HVPm2X0wHXrvnm-hG5m9SZMQB-z5sAkyTKAKJKu85eUQH8HuM0aiao3vcYxNDT9d1Jc7Vz2Bf8XWjgV-puoaXPAGag8u18anrduIo2gZZGdBFLYBejoQHSn68RcFV8PU7GAjEyGyrgJzb5W_3nOlAeYoy8bhugwgOgXTrqsYXGlSQ74Bl3VlQKVEClUZ0CpliJ0URpmBhYlzQUUAO7Nv93Zpw3qubObujFuWNwNFI6EAC5d-y-zUucM-2ewmM0-jJphf-l&pos=104&s=58&src=GD_JOB_VIEW&t=SR&vt=w",
    "searchResultsUrl": "https://www.glassdoor.com/Job/new-york-ny-devops-engineer-jobs-SRCH_IL.0,11_IC1132348_KO12,27.htm?jl=1010024904229&srs=JV_APPLYPANE",
    "discoveredAt": "2026-03-05T00:00:00",
    "listingAgeDays": 42,
    "isExpired": false,
    "hasEasyApply": false,
    "isApplyButtonDisabled": false,
    "applicationId": 0,
    "importConfigId": 322429,
    "titleId": 0,
    "eolHashCode": 0
  },
  "jobTaxonomy": {
    "normalizedTitle": "devops engineer",
    "occupationName": "devops engineer",
    "occupationId": 102489,
    "categoryId": 10132,
    "subCategoryId": 1007,
    "countryId": 1,
    "searchAttributes": {
      "education": [
        "UTPWG"
      ],
      "educationLabel": [
        "Associate's degree"
      ],
      "skills": [
        "44AQZ",
        "64VXT",
        "A3TZC",
        "BC7SU",
        "D866K",
        "DKNQM",
        "FADZP",
        "GFRKJ",
        "GWKWY",
        "H98DC",
        "J3CT2",
        "R6MKU",
        "RZR2K",
        "T65FY",
        "WSBNK"
      ],
      "skillsLabel": [
        "Spanish",
        "Azure",
        "SAP",
        "Accounting software",
        "English",
        "Japanese",
        "Microservices",
        "AWS",
        "Incident response",
        "Docker",
        "Release management",
        "Financial services",
        "Translation",
        "Proofreading",
        "Communication skills"
      ]
    }
  },
  "jobLocation": {
    "locationId": 1132348,
    "locationName": "New York, NY",
    "locationType": "C",
    "location": {
      "id": 1132348,
      "name": "New York, NY",
      "type": "C"
    },
    "map": {
      "cityName": "New York, NY",
      "country": "United States",
      "employer": {
        "id": 285118,
        "name": "Pasona NA Inc."
      },
      "lat": 40.71417,
      "lng": -74.00639,
      "locationName": "New York, NY",
      "stateName": "New York State"
    }
  },
  "compensation": {
    "currency": "USD",
    "payPeriod": "HOURLY",
    "salarySource": "EMPLOYER_PROVIDED",
    "range": {
      "p10": 48,
      "p50": 50.5,
      "p90": 53
    },
    "searchMidpoint": 50.5
  },
  "company": {
    "companyId": 285118,
    "companyName": "Pasona NA",
    "shortName": "Pasona NA",
    "activeStatus": "ACTIVE",
    "industryId": 200032,
    "bestProfileId": 313190,
    "logoUrl": "https://media.glassdoor.com/sql/285118/pasona-na-squarelogo-1426237112600.png",
    "overallRating": 3.5,
    "ratings": {
      "careerOpportunitiesRating": 3.4,
      "ceoRatingsCount": 2,
      "compensationAndBenefitsRating": 3.1,
      "cultureAndValuesRating": 3.6,
      "overallRating": 3.5,
      "recommendToFriendRating": 0.66,
      "seniorManagementRating": 3.2,
      "workLifeBalanceRating": 3.6
    },
    "attributes": [
      {
        "attributeName": "TRACKING_PROFILE_XSP",
        "attributeValue": "4759269"
      }
    ],
    "content": {
      "managedContent": [
        {
          "body": "<p><strong>Corporate Philosophy</strong></p> <p>一 Creating a society in which every person is able to find work that they like and a career that complements their personal goals.</p> <p>一 Working towards a society in which people are free to exercise their talents through an egalitarian relationship between the workplace and the individual.</p> <p>一 Continually building opportunities for individuals to achieve their dreams, regardless of age or gender.</p>",
          "id": 103274,
          "photos": [
            "https://media.glassdoor.com/template/l/285118/pasona-na-template-1645641263119.jpg"
          ],
          "title": "Philosophy",
          "type": "OMEDIA"
        },
        {
          "body": "<p><strong>Learn &amp; Be Ambitious!</strong></p> <p>In a world that changes every day, our possibilities as a partner to pursue needs are endless. With Learn &amp; Ambitious in mind, we will continue to challenge new possibilities. We are waiting for friends who can increase corporate value and grow together.</p>",
          "id": 233491,
          "photos": [
            "https://media.glassdoor.com/template/l/285118/pasona-na-template-1645641014510.jpg"
          ],
          "title": "Join Us",
          "type": "OMEDIA"
        }
      ]
    },
    "overview": {
      "ceo": {
        "name": "Kenji Furushiro"
      },
      "headquarters": "New York, NY",
      "id": 285118,
      "links": {
        "benefitsUrl": "https://www.glassdoor.com/Benefits/Pasona-NA-Benefits-E285118.htm",
        "overviewUrl": "https://www.glassdoor.com/Overview/Working-at-Pasona-NA-EI_IE285118.11,20.htm",
        "photosUrl": "https://www.glassdoor.com/Photos/Pasona-NA-Office-Photos-E285118.htm",
        "reviewsUrl": "https://www.glassdoor.com/Reviews/Pasona-NA-Reviews-E285118.htm",
        "salariesUrl": "https://www.glassdoor.com/Salary/Pasona-NA-Salaries-E285118.htm"
      },
      "name": "Pasona NA Inc.",
      "primaryIndustry": {
        "industryId": 200032,
        "industryName": "HR Consulting",
        "sectorId": 10026,
        "sectorName": "Human Resources & Staffing"
      },
      "ratings": {
        "careerOpportunitiesRating": 3.4,
        "ceoRatingsCount": 2,
        "compensationAndBenefitsRating": 3.1,
        "cultureAndValuesRating": 3.6,
        "overallRating": 3.5,
        "recommendToFriendRating": 0.66,
        "seniorManagementRating": 3.2,
        "workLifeBalanceRating": 3.6
      },
      "revenue": "$25 to $100 million (USD)",
      "shortName": "Pasona NA",
      "size": "51 to 200 Employees",
      "sizeCategory": "SMALL_TO_MEDIUM",
      "squareLogoUrl": "https://media.glassdoor.com/sql/285118/pasona-na-squarelogo-1426237112600.png",
      "type": "Company - Private",
      "website": "https://www.pasona.com",
      "yearFounded": 1985
    }
  },
  "companyInsights": {
    "benefitsSummary": {
      "benefitsHighlights": [
        {
          "benefit": {
            "icon": "health",
            "name": "Health Insurance"
          },
          "commentCount": 3,
          "highlightPhrase": "Health insurance covers more thank I expected. They also offer FSA"
        },
        {
          "benefit": {
            "icon": "retirement",
            "name": "401K Plan"
          },
          "commentCount": 3,
          "highlightPhrase": "Matching up to 5%. Not bad."
        }
      ],
      "employerBenefitSummary": {
        "comment": "<p><u><strong>Holiday Pay</strong></u></p> <p>Holiday pay will be eight (8) hours at the regular straight time rate if they are scheduled to work the</p> <p>last scheduled work day before the holiday and the first scheduled work day after the holiday.</p> <p>Company Holiday is about 10 days per year (including 6 major holidays—New year/President’s</p> <p>day/Memorial Day/Independence Day/Labor Day/Thanksgiving Day)</p> <p><u><strong><br>Paid Time Off</strong></u></p> <p>PTO - 128 hours per year (about 10.66 hours per month)</p> <p>Full-Time employees begin accruing PTO upon completion of the first pay period after the date of</p> <p>hire and may request to use their accrued PTO hours at the minimum increments of one (1) hour.</p> <p>Physical Check-up Leave Time- 16 hours per calendar year and become eligible to use after 90</p> <p>days of employment at the minimum increment of one (1) hour. The balance resets on January 1st.</p> <p> </p> <p><u><strong>Health insurance and other benefit plans</strong></u></p> <p>Group medical insurance plan- The company offers group medical, dental, prescription drug</p> <p>vision, life and short term/long term disability insurance coverage to employees upon the date of</p> <p>hire.</p> <p>Other Group benefit plans- The company offers Health Care/Dependent Care FSA to regular</p> <p>full-time employees after 90 days from the date of hire.</p> <p> </p> <p><u><strong>401k plan</strong></u></p> <p>Eligibility- upon completion of six (6) months of service and if they are at least twenty-one (21)</p> <p>years old.</p> <p>Company match- The Company will make a Safe Harbor Matching Contribution equal to 100.0% of</p> <p>your Elective Deferrals between 1 ~ 3%, 50% of your Elective Deferrals between 4 ~ 5%. (Thus, the</p> <p>maximum matching contribution is 4.0 %.)</p> <p> </p> <p>*Note: Benefit information may change without notice</p> <p><em><strong>Last revised on October 2019</strong></em></p>"
      },
      "overallBenefitRating": 3.6,
      "totalBenefitReviews": 22
    },
    "benefitReviews": [
      {
        "benefitComments": [
          {
            "comment": "Not perfect but comprehensive package",
            "id": 11676003
          }
        ],
        "city": {
          "name": "Torrance, CA"
        },
        "createDate": "2025-02-18T20:39:34.323",
        "currentJob": false,
        "rating": 5,
        "state": {
          "name": "California"
        },
        "userEnteredJobTitle": "Talent Acquisition"
      },
      {
        "benefitComments": [
          {
            "comment": "Employee of this company are provided with 401K.",
            "id": 10609500
          }
        ],
        "city": {
          "name": "California City, CA"
        },
        "createDate": "2024-08-21T17:10:31.66",
        "currentJob": false,
        "rating": 3,
        "state": {
          "name": "California"
        }
      },
      {
        "benefitComments": [
          {
            "comment": "The benefits that the company offers are great. I believe the price and the plan coverage are impressive. I haven’t had any issues in the past.",
            "id": 9891768
          }
        ],
        "city": {
          "name": "Los Angeles, CA"
        },
        "createDate": "2024-05-04T21:42:39.253",
        "currentJob": true,
        "rating": 5,
        "state": {
          "name": "California"
        },
        "userEnteredJobTitle": "Business Development"
      }
    ],
    "reviewHighlights": [
      {
        "categoryReviewCount": 5,
        "sentence": "Bad management and not following current trends",
        "sentiment": "NEGATIVE"
      },
      {
        "categoryReviewCount": 6,
        "sentence": "Culture is not good, need to improvement PMS and salary date",
        "sentiment": "NEGATIVE"
      },
      {
        "categoryReviewCount": 6,
        "sentence": "We will learn the Japanese culture of working style.",
        "sentiment": "POSITIVE"
      },
      {
        "categoryReviewCount": 4,
        "sentence": "Flexible and people were nice",
        "sentiment": "POSITIVE"
      },
      {
        "categoryReviewCount": 2,
        "sentence": "Never bored as multiple clients are assigned, benefits are good",
        "sentiment": "POSITIVE"
      },
      {
        "categoryReviewCount": 3,
        "sentence": "I was not busy at work but I found some colleagues worked overtime a lot due to the low salary.",
        "sentiment": "NEGATIVE"
      }
    ]
  },
  "platformMetadata": {
    "adOrderId": 1110586,
    "jobResultTrackingKey": "5-yul1-3-1jk4q0uc9294hg00-1jk4q0qpsgmvh800---6NYlbfkN0BQ0BgX18I10G6uoQ7vFAhySPo543-EiU2WryMBkb_AmY7Ep3qJ4G2RmxulaXh7nbU_1Lr61cyIrEDpHiap53j9OyooCF3fxIUZMyqP7JxVtlvnasSpkfBq6L3m3S_5_dIbc8pGOMsvXEn2q1wYXRdG56LvvVGYUVZMUvOKL5mhiknyG5WDNg40vVYgEkAtOqdJVe9TSB9OBqityIMT3fsmEAP9fuLe9URVc2QRDX7MTPV8StW52v8tospit78O6bcXTs5P4J3HLSudq0dyKNcusGGiZSG6oGyVFj8FwJyfdHpm46L7u6lR16yu3TMj4nRf5w5OdvS_EgTmYYaTBVq4osSfWOmPzUiF5sjC-BH92sZadtK6EoaJT-pjpm3RoQelE9cL-zxDBFtrg0SZfO86Ke9HVyuPp5I5XcjjXML8DCZR9Joi183gotQNHS59fDtfCArlBFurcrqcK8sNSjC72HuBaAVojXmREmfmAsbrtweZpUXe8l6Wx3fyRA2eeq71s0hivMS7EZG7qgApcYsIcUDsHTgmGtwD9AVqsinxcqSIUdD8RURPGeaKpVnqkQFWAOz3OjmAgDhLcd6pxYSDmuhqNsvGz85uj7NWDlqb85X6v7HVPm2X0wHXrvnm-hG5m9SZMQB-z5sAkyTKAKJKu85eUQH8HuM0aiao3vcYxNDT9d1Jc7Vz2Bf8XWjgV-puoaXPAGag8u18anrduIo2gZZGdBFLYBejoQHSn68RcFV8PU7GAjEyGyrgJzb5W_3nOlAeYoy8bhugwgOgXTrqsYXGlSQ74Bl3VlQKVEClUZ0CpliJ0URpmBhYlzQUUAO7Nv93Zpw3qubObujFuWNwNFI6EAC5d-y-zUucM-2ewmM0-jJphf-l",
    "savedJobId": 0,
    "isSearchIndexable": false,
    "isSponsoredEmployer": true,
    "isSponsoredJob": true,
    "tracking": {
      "jobViewDisplayTimeMillis": 0,
      "pageRequestGuid": "0000019d09a079699898816197251cb4",
      "requiresTracking": true,
      "searchTypeCode": "NS",
      "trackingUrl": "https://www.indeed.com/rc/gd/png?a=9yr8FVtIpDy83VVaQMQxTJWCTRgI8IAQuLCpmrri1g5QvKAN4OLTFG9NL3wYNjL0_ck5Vp4sX3FMPh1hZrY4zr9kEf3IIzwVjWsnpJ6oTgVpzjNPBxKdx3XqfatFtEGY2hsyVbvuOFlKdakU_4aFZYE5vpxOAXMKVk17Z1eS4gvMROt6YNiVZH14C3l16slTyxP7QrNdsOEyvWIplua0pDwrEdYDmJ3UlZ0Fc8WLrENokG9t9-7xKIJejb4IteTHWsu3H9NBiA0MSYO812jqIY2a0ZC2GlDkRMfjSnaCWEc6BQqcix9RlbrTBhoXqDkLMMOsgRlyWnt3sVfNbD5YGkZC6pLV_ScZs_yw-YWPc8KCXo2-CLXkx0LpfzbL1Yl8g73X5c6ZLYsJi-lYhUDpjWFLGgde6n1TBvttd_moTog6vcZLaKj4syQ2dqgmKZmcjZx-vR156Ko7MfEmLO_pNkbZXYdfAZ0H7rIY-UA9qaa1itujrf4TQYCr-jEngnKBWDQ-BJGcAHMM3nbkJF50jpd3M2cgG1DZbTzX2q0ReUGPEnYEo0vHQnzx1shz5IRPF4z-5YKzU8EBNUuUQnKicjIWZ2YaJpI2-bd81FVhcjzWFLR_3niWKDPtZx_wXl2vLlX_2E3T4jhUG1_SH5hrbBjngldjLLLrbFdypdLLhacGlyuskYb5W12NJShhMm7oMwSNXT1pWOkpxdZ8wyQQI9vanXEg3l1frSxPqGuT8c7G35hY8zcqIoIBF0yjuFy1CLLyeMCkpXXJeANOu8goluEdiQG9_CGTaqONIlSRWrVGnk--i2M560tjcErPxkXyggEXTKO4XLVZRPZoYyUDt07-dAELXVQSNaZLIlyGgF3nYJ8Gh5Z1FePOg0IjE9-q9XPR0dEGAUmjXg62Lmtd3FnXEiC2d_EzNsmj0eUTRdp-wSvGhhpN9B-LiVNLhZd2dTr5_WOMl06icHK3iz836VlE9mhjJQO3SdZ3gmMtZiVKVp8_zKg4UZx9mivmXdaq41zDE2m7dHLE4r35-Z5MfYhI3zgMUJPeEk8qAMMEvso83bdBQ8B-SV1ABGxqqtWc-nnlss3sWoq7oxo_Y81pHfNH41cfUqeG-l3GFHxTL-1VDQQI2bYlB_i3ztwyyjPV-l3GFHxTL-1VDQQI2bYlB0xODlht1vilWKFhYQFNdXImr04pYOj_HHspXaHXpx5ulHniVsx08V-b25D2_EIuYwbUHFbd675PSBJYyF7c9AbpXjrzpsBdPk3SWcKaedzQFMPaWCk_ddVVdlxdDd5uoP6wcAOl9MGLg2DgKJ6OBlhldFo5_MJFd8ZUUbniQMl61CgBZz2_FL24HheraShOfItSGXV7xIVn68zYvizVk583DK5WXl8w20yVSb2YqVWFEOBkoguFmMDnfKyLsjZeBXITyhANlQ-rfk5Zdbqbr1dHzZ6kvwFHCSXCadzpw2ftNQgH1CxJ261ISosxRHw0HjYjdkABtG-vjB0kYjZzS6qt5oncwOsfmAM4GuGQbhtt-6rBVMje2mvtmnLoMcyR7WkUgPBkbPszlvHhbcSSv_I&channel=sr-s_58&ctk=1jk4q0rohiucv800&org=0",
      "isSponsoredJob": true,
      "isSponsoredEmployer": true,
      "jobExpired": false,
      "lashedEmployer": "Pasona NA",
      "lashedEmployerId": 285118,
      "lashedIndustry": "HR Consulting",
      "lashedIndustryId": 200032,
      "lashedLocation": "New York, NY",
      "lashedLocationId": 1132348,
      "lashedLocationType": "C",
      "lashedOccupation": "Application Platform DevOps Engineer",
      "lashedOccupationId": 1010024904229,
      "lashedSector": "Human Resources & Staffing",
      "lashedSectorId": 10026
    }
  },
  "sourceMetadata": {
    "seed": {
      "id": "9769ed2b9726",
      "type": "query",
      "value": "{\"filters\":{\"minSalary\":\"40000\"},\"location\":\"new york\",\"query\":\"software\"}"
    },
    "sourceUrl": "https://www.glassdoor.com/job-search-next/bff/jobSearchResultsQuery",
    "recordUrl": "https://www.glassdoor.com/job-listing/application-platform-devops-engineer-pasona-na-JV_IC1132348_KO0,36_KE37,46.htm?jl=1010024904229",
    "detailApiUrl": "https://www.glassdoor.com/job-listing/api/job-details?countryId=1&jobListingId=1010024904229&pageTypeEnum=SERP&queryString=%2Fpartner%2FjobListing.htm%3Fpos%3D104%26ao%3D1110586%26s%3D58%26guid%3D0000019d09a06b078f14733fcf925081%26src%3DGD_JOB_AD%26t%3DSR%26vt%3Dw%26cs%3D1_b33d2003%26cb%3D1773983001773%26jobListingId%3D1010024904229%26cpc%3D451933188B21919D%26jrtk%3D5-yul1-0-1jk4q0qpsgmvh800-5ab88e2ae74b63b7---6NYlbfkN0BQ0BgX18I10G6uoQ7vFAhySPo543-EiU2WryMBkb_AmY7Ep3qJ4G2RmxulaXh7nbU_1Lr61cyIrEDpHiap53j9OyooCF3fxIUZMyqP7JxVtlvnasSpkfBq6L3m3S_5_dIbc8pGOMsvXEn2q1wYXRdG56LvvVGYUVZMUvOKL5mhiknyG5WDNg40vVYgEkAtOqdJVe9TSB9OBqityIMT3fsmEAP9fuLe9URVc2QRDX7MTPV8StW52v8tospit78O6bcXTs5P4J3HLSudq0dyKNcusGGiZSG6oGyVFj8FwJyfdHpm46L7u6lR16yu3TMj4nRf5w5OdvS_EgTmYYaTBVq4osSfWOmPzUiF5sjC-BH92sZadtK6EoaJT-pjpm3RoQelE9cL-zxDBFtrg0SZfO86Ke9HVyuPp5I5XcjjXML8DCZR9Joi183gotQNHS59fDtfCArlBFurcrqcK8sNSjC72HuBaAVojXmREmfmAsbrtweZpUXe8l6Wx3fyRA2eeq71s0hivMS7EZG7qgApcYsIcUDsHTgmGtwD9AVqsinxcqSIUdD8RURPGeaKpVnqkQFWAOz3OjmAgDhLcd6pxYSDmuhqNsvGz85uj7NWDlqb85X6v7HVPm2X0wHXrvnm-hG5m9SZMQB-z5sAkyTKAKJKu85eUQH8HuM0aiao3vcYxNDT9d1Jc7Vz2Bf8XWjgV-puoaXPAGag8u18anrduIo2gZZGdBFLYBejoQHSn68RcFV8PU7GAjEyGyrgJzb5W_3nOlAeYoy8bhugwgOgXTrqsYXGlSQ74Bl3VlQKVEClUZ0CpliJ0URpmBhYlzQUUAO7Nv93Zpw3qubObujFuWNwNFI6EAC5d-y-zUucM-2ewmM0-jJphf-l",
    "pageIndex": 1,
    "scrapedAt": "2026-03-20T05:03:25.737782Z",
    "searchListingSnapshot": {
      "listingId": "1010024904229",
      "jobTitle": "Application Platform DevOps Engineer",
      "recordUrl": "https://www.glassdoor.com/job-listing/application-platform-devops-engineer-pasona-na-JV_IC1132348_KO0,36_KE37,46.htm?jl=1010024904229",
      "jobPageUrl": "https://www.glassdoor.com/partner/jobListing.htm?ao=1110586&cb=1773983001773&cpc=451933188B21919D&cs=1_b33d2003&guid=0000019d09a06b078f14733fcf925081&jobListingId=1010024904229&jrtk=5-yul1-0-1jk4q0qpsgmvh800-5ab88e2ae74b63b7---6NYlbfkN0BQ0BgX18I10G6uoQ7vFAhySPo543-EiU2WryMBkb_AmY7Ep3qJ4G2RmxulaXh7nbU_1Lr61cyIrEDpHiap53j9OyooCF3fxIUZMyqP7JxVtlvnasSpkfBq6L3m3S_5_dIbc8pGOMsvXEn2q1wYXRdG56LvvVGYUVZMUvOKL5mhiknyG5WDNg40vVYgEkAtOqdJVe9TSB9OBqityIMT3fsmEAP9fuLe9URVc2QRDX7MTPV8StW52v8tospit78O6bcXTs5P4J3HLSudq0dyKNcusGGiZSG6oGyVFj8FwJyfdHpm46L7u6lR16yu3TMj4nRf5w5OdvS_EgTmYYaTBVq4osSfWOmPzUiF5sjC-BH92sZadtK6EoaJT-pjpm3RoQelE9cL-zxDBFtrg0SZfO86Ke9HVyuPp5I5XcjjXML8DCZR9Joi183gotQNHS59fDtfCArlBFurcrqcK8sNSjC72HuBaAVojXmREmfmAsbrtweZpUXe8l6Wx3fyRA2eeq71s0hivMS7EZG7qgApcYsIcUDsHTgmGtwD9AVqsinxcqSIUdD8RURPGeaKpVnqkQFWAOz3OjmAgDhLcd6pxYSDmuhqNsvGz85uj7NWDlqb85X6v7HVPm2X0wHXrvnm-hG5m9SZMQB-z5sAkyTKAKJKu85eUQH8HuM0aiao3vcYxNDT9d1Jc7Vz2Bf8XWjgV-puoaXPAGag8u18anrduIo2gZZGdBFLYBejoQHSn68RcFV8PU7GAjEyGyrgJzb5W_3nOlAeYoy8bhugwgOgXTrqsYXGlSQ74Bl3VlQKVEClUZ0CpliJ0URpmBhYlzQUUAO7Nv93Zpw3qubObujFuWNwNFI6EAC5d-y-zUucM-2ewmM0-jJphf-l&pos=104&s=58&src=GD_JOB_AD&t=SR&vt=w",
      "companyName": "Pasona NA",
      "locationName": "New York, NY",
      "currency": "USD",
      "payMidpoint": 50.5,
      "payPeriod": "HOURLY",
      "salarySource": "EMPLOYER_PROVIDED",
      "hasEasyApply": false,
      "listingAgeDays": 42,
      "companyId": 285118,
      "companyRating": 3.5,
      "extractionStrategy": "api"
    },
    "rawDetailPayload": {
      "adOrderId": 1110586,
      "categoryMgocId": 10132,
      "companyRatings": {
        "careerOpportunitiesRating": 3.4,
        "ceoRatingsCount": 2,
        "compensationAndBenefitsRating": 3.1,
        "cultureAndValuesRating": 3.6,
        "overallRating": 3.5,
        "recommendToFriendRating": 0.66,
        "seniorManagementRating": 3.2,
        "workLifeBalanceRating": 3.6
      },
      "employerActiveStatus": "ACTIVE",
      "employerAttributes": [
        {
          "attributeName": "TRACKING_PROFILE_XSP",
          "attributeValue": "4759269"
        }
      ],
      "employerContent": {
        "managedContent": [
          {
            "body": "<p><strong>Corporate Philosophy</strong></p> <p>一 Creating a society in which every person is able to find work that they like and a career that complements their personal goals.</p> <p>一 Working towards a society in which people are free to exercise their talents through an egalitarian relationship between the workplace and the individual.</p> <p>一 Continually building opportunities for individuals to achieve their dreams, regardless of age or gender.</p>",
            "id": 103274,
            "photos": [
              "https://media.glassdoor.com/template/l/285118/pasona-na-template-1645641263119.jpg"
            ],
            "title": "Philosophy",
            "type": "OMEDIA"
          },
          {
            "body": "<p><strong>Learn &amp; Be Ambitious!</strong></p> <p>In a world that changes every day, our possibilities as a partner to pursue needs are endless. With Learn &amp; Ambitious in mind, we will continue to challenge new possibilities. We are waiting for friends who can increase corporate value and grow together.</p>",
            "id": 233491,
            "photos": [
              "https://media.glassdoor.com/template/l/285118/pasona-na-template-1645641014510.jpg"
            ],
            "title": "Join Us",
            "type": "OMEDIA"
          }
        ]
      },
      "employerId": 285118,
      "employerBestProfileId": 313190,
      "employerIndustryId": 200032,
      "employerName": "Pasona NA",
      "employerOverview": {
        "ceo": {
          "name": "Kenji Furushiro"
        },
        "headquarters": "New York, NY",
        "id": 285118,
        "links": {
          "benefitsUrl": "https://www.glassdoor.com/Benefits/Pasona-NA-Benefits-E285118.htm",
          "overviewUrl": "https://www.glassdoor.com/Overview/Working-at-Pasona-NA-EI_IE285118.11,20.htm",
          "photosUrl": "https://www.glassdoor.com/Photos/Pasona-NA-Office-Photos-E285118.htm",
          "reviewsUrl": "https://www.glassdoor.com/Reviews/Pasona-NA-Reviews-E285118.htm",
          "salariesUrl": "https://www.glassdoor.com/Salary/Pasona-NA-Salaries-E285118.htm"
        },
        "name": "Pasona NA Inc.",
        "primaryIndustry": {
          "industryId": 200032,
          "industryName": "HR Consulting",
          "sectorId": 10026,
          "sectorName": "Human Resources & Staffing"
        },
        "ratings": {
          "careerOpportunitiesRating": 3.4,
          "ceoRatingsCount": 2,
          "compensationAndBenefitsRating": 3.1,
          "cultureAndValuesRating": 3.6,
          "overallRating": 3.5,
          "recommendToFriendRating": 0.66,
          "seniorManagementRating": 3.2,
          "workLifeBalanceRating": 3.6
        },
        "revenue": "$25 to $100 million (USD)",
        "shortName": "Pasona NA",
        "size": "51 to 200 Employees",
        "sizeCategory": "SMALL_TO_MEDIUM",
        "squareLogoUrl": "https://media.glassdoor.com/sql/285118/pasona-na-squarelogo-1426237112600.png",
        "type": "Company - Private",
        "website": "https://www.pasona.com",
        "yearFounded": 1985
      },
      "employerRating": 3.5,
      "employerSquareLogo": "https://media.glassdoor.com/sql/285118/pasona-na-squarelogo-1426237112600.png",
      "expired": false,
      "gocId": 102489,
      "isEasyApply": false,
      "isIndexable": false,
      "isSponsoredEmployer": true,
      "isSponsoredJob": true,
      "jobCountryId": 1,
      "jobDescription": "<div><ul><li><b>Japanese language skills are highly preferred.</b></li><li><b>Experience of DevOps and CI/CD is required.</b></li></ul><p></p><p><b><br> Job Details</b></p><ul><li> <b>Job Title:</b> Application Platform / DevOps Engineer</li><li> <b>Working Location:</b> NY</li><li> <b>Working style: </b>Hybrid (Onsite preferred 2&ndash;3 days/week, flexible)</li><li> <b>Working Hours:</b> Full-time preferred (negotiable)</li><li> <b>Language: </b>English (Japanese is a plus)</li><li> <b>Pay Rate:</b> $48-53/hour</li><li> <b>Employment type:</b> Temp to Perm</li></ul><p></p><p><b><br> ︎Job Summary</b></p><p> We are looking for a versatile Application Platform / DevOps Engineer to support an IT organization within a Japanese financial services firm in the Americas.</p><p> This role focuses on application platform operations, development support, and migration initiatives, working closely with multiple application teams in an Agile environment.</p><p><b> This position requires a broad technical skill set, hands-on mindset, and the ability to flexibly support various tools and processes across the application lifecycle.</b></p><p></p><p><b><br> ︎ Key Responsibilities:</b></p><ul><li> Provide operational support for application platforms, including maintenance, troubleshooting, and incident response.</li><li> Support application development initiatives, including coordination with multiple application teams.</li><li> Manage and support DevOps, CI/CD pipelines, container-based environments, and release processes</li><li> Support frequent application releases in an Agile development environment</li><li> Utilize GitHub for module management and application operational support</li><li> Support front-office and middle-office applications across the Americas (primarily web-based and microservices)</li></ul><p></p><p><b><br> ︎ Required Qualifications &amp; Skills:</b></p><ul><li> Broad experience across application platform operations, development support, and migration projects</li><li> Strong understanding of the full SDLC, with hands-on experience completing at least two full development cycles</li><li> Experience working in Agile development environments with frequent releases</li><li> Ability to coordinate effectively with multiple application teams</li><li> Strong communication skills in English</li></ul><p></p><p><b><br> ︎Preferred Qualifications</b></p><ul><li> Experience with DevOps-related technologies such as:</li></ul><p> o GitHub / GitHub Actions</p><p> o CI/CD pipelines</p><p> o Container technologies (e.g., Docker, Kubernetes)</p><p> o Cloud platforms (AWS and/or Azure)</p><ul><li> Experience supporting financial services</li></ul><p></p><p><b><br> ﻿</b><b>*Knowledge of accounting and SAP is required.</b></p><ul><li><b>Spanish or Japanese language skills are highly preferred.</b></li></ul><p></p><p><br> A Japanese company is seeking a SAP Helpdesk Support.</p><p></p><p><br> Work Hours: 7 hours shifts （Morning shift : 9:00 A.M. to 5:00 P.M. / Late Shift 12:00 P.M. to 8:00 P.M., Monday through Friday except holidays.</p><p> Base Salary $60K～$72K</p><p> Work Location: Client&rsquo;s Onsite in NYC. (depends on the client&rsquo;s needs/policy/regulations, might be changed assign number of days for working at their Onsite.)</p><p></p><p><br> Job Description</p><p> This position is stationed at the client&rsquo;s site. However, might be assigned for Telecommuting as Hybrid, depending on the client&rsquo;s needs. Responsibilities include providing troubleshoots for SAP<i>.</i></p><p></p><p><br> Summary</p><p> Essential Job Functions:</p><p> 1. SAP helpdesk support in English/Spanish or Japanese language</p><p> 1) Trouble shooting</p><p> Technical support at on-site or by email or telephone or remote access tool</p><p> 2) Operation support</p><p> User support for SAP software</p><p> 3) Documentation (user manual, FAQ, user announcement)</p><p> 4) User Education</p><p> 5) Record work (Help) log</p><p> Miscellaneous Job :</p><p> 2.Translation</p><p> ・Translation and proofreading English/Spanish materials or English/Japanese materials</p><p></p><p><br> Job Requirements</p><p> a)Education</p><p> Associate or bachelor&rsquo;s degree in Computer Science, Information Technology, or a related field for SAP would be plus.</p><p> b)Business Travel</p><p> Yes (depends on client&rsquo;s needs)</p><p></p><p><br> To apply please email your resume to myamamoto@pasona.com</p></div>",
      "jobDetailsRawData": {
        "jobview": {
          "employerAttributes": {
            "attributes": [
              {
                "attributeName": "TRACKING_PROFILE_XSP",
                "attributeValue": "4759269"
              }
            ]
          },
          "employerContent": {
            "managedContent": [
              {
                "body": "<p><strong>Corporate Philosophy</strong></p> <p>一 Creating a society in which every person is able to find work that they like and a career that complements their personal goals.</p> <p>一 Working towards a society in which people are free to exercise their talents through an egalitarian relationship between the workplace and the individual.</p> <p>一 Continually building opportunities for individuals to achieve their dreams, regardless of age or gender.</p>",
                "id": 103274,
                "photos": [
                  "https://media.glassdoor.com/template/l/285118/pasona-na-template-1645641263119.jpg"
                ],
                "title": "Philosophy",
                "type": "OMEDIA"
              },
              {
                "body": "<p><strong>Learn &amp; Be Ambitious!</strong></p> <p>In a world that changes every day, our possibilities as a partner to pursue needs are endless. With Learn &amp; Ambitious in mind, we will continue to challenge new possibilities. We are waiting for friends who can increase corporate value and grow together.</p>",
                "id": 233491,
                "photos": [
                  "https://media.glassdoor.com/template/l/285118/pasona-na-template-1645641014510.jpg"
                ],
                "title": "Join Us",
                "type": "OMEDIA"
              }
            ]
          },
          "gaTrackerData": {
            "jobViewDisplayTimeMillis": 0,
            "pageRequestGuid": "0000019d09a079699898816197251cb4",
            "requiresTracking": true,
            "searchTypeCode": "NS",
            "trackingUrl": "https://www.indeed.com/rc/gd/png?a=9yr8FVtIpDy83VVaQMQxTJWCTRgI8IAQuLCpmrri1g5QvKAN4OLTFG9NL3wYNjL0_ck5Vp4sX3FMPh1hZrY4zr9kEf3IIzwVjWsnpJ6oTgVpzjNPBxKdx3XqfatFtEGY2hsyVbvuOFlKdakU_4aFZYE5vpxOAXMKVk17Z1eS4gvMROt6YNiVZH14C3l16slTyxP7QrNdsOEyvWIplua0pDwrEdYDmJ3UlZ0Fc8WLrENokG9t9-7xKIJejb4IteTHWsu3H9NBiA0MSYO812jqIY2a0ZC2GlDkRMfjSnaCWEc6BQqcix9RlbrTBhoXqDkLMMOsgRlyWnt3sVfNbD5YGkZC6pLV_ScZs_yw-YWPc8KCXo2-CLXkx0LpfzbL1Yl8g73X5c6ZLYsJi-lYhUDpjWFLGgde6n1TBvttd_moTog6vcZLaKj4syQ2dqgmKZmcjZx-vR156Ko7MfEmLO_pNkbZXYdfAZ0H7rIY-UA9qaa1itujrf4TQYCr-jEngnKBWDQ-BJGcAHMM3nbkJF50jpd3M2cgG1DZbTzX2q0ReUGPEnYEo0vHQnzx1shz5IRPF4z-5YKzU8EBNUuUQnKicjIWZ2YaJpI2-bd81FVhcjzWFLR_3niWKDPtZx_wXl2vLlX_2E3T4jhUG1_SH5hrbBjngldjLLLrbFdypdLLhacGlyuskYb5W12NJShhMm7oMwSNXT1pWOkpxdZ8wyQQI9vanXEg3l1frSxPqGuT8c7G35hY8zcqIoIBF0yjuFy1CLLyeMCkpXXJeANOu8goluEdiQG9_CGTaqONIlSRWrVGnk--i2M560tjcErPxkXyggEXTKO4XLVZRPZoYyUDt07-dAELXVQSNaZLIlyGgF3nYJ8Gh5Z1FePOg0IjE9-q9XPR0dEGAUmjXg62Lmtd3FnXEiC2d_EzNsmj0eUTRdp-wSvGhhpN9B-LiVNLhZd2dTr5_WOMl06icHK3iz836VlE9mhjJQO3SdZ3gmMtZiVKVp8_zKg4UZx9mivmXdaq41zDE2m7dHLE4r35-Z5MfYhI3zgMUJPeEk8qAMMEvso83bdBQ8B-SV1ABGxqqtWc-nnlss3sWoq7oxo_Y81pHfNH41cfUqeG-l3GFHxTL-1VDQQI2bYlB_i3ztwyyjPV-l3GFHxTL-1VDQQI2bYlB0xODlht1vilWKFhYQFNdXImr04pYOj_HHspXaHXpx5ulHniVsx08V-b25D2_EIuYwbUHFbd675PSBJYyF7c9AbpXjrzpsBdPk3SWcKaedzQFMPaWCk_ddVVdlxdDd5uoP6wcAOl9MGLg2DgKJ6OBlhldFo5_MJFd8ZUUbniQMl61CgBZz2_FL24HheraShOfItSGXV7xIVn68zYvizVk583DK5WXl8w20yVSb2YqVWFEOBkoguFmMDnfKyLsjZeBXITyhANlQ-rfk5Zdbqbr1dHzZ6kvwFHCSXCadzpw2ftNQgH1CxJ261ISosxRHw0HjYjdkABtG-vjB0kYjZzS6qt5oncwOsfmAM4GuGQbhtt-6rBVMje2mvtmnLoMcyR7WkUgPBkbPszlvHhbcSSv_I&channel=sr-s_58&ctk=1jk4q0rohiucv800&org=0"
          },
          "header": {
            "adOrderId": 1110586,
            "ageInDays": 42,
            "applicationId": 0,
            "applyButtonDisabled": false,
            "applyUrl": "https://www.glassdoor.com/partner/jobListing.htm?ao=1110586&cb=1773983005122&cpc=451933188B21919D&cs=1_9d15e368&guid=0000019d09a06b078f14733fcf925081&jobListingId=1010024904229&jrtk=5-yul1-3-1jk4q0uc9294hg00-1jk4q0qpsgmvh800---6NYlbfkN0BQ0BgX18I10G6uoQ7vFAhySPo543-EiU2WryMBkb_AmY7Ep3qJ4G2RmxulaXh7nbU_1Lr61cyIrEDpHiap53j9OyooCF3fxIUZMyqP7JxVtlvnasSpkfBq6L3m3S_5_dIbc8pGOMsvXEn2q1wYXRdG56LvvVGYUVZMUvOKL5mhiknyG5WDNg40vVYgEkAtOqdJVe9TSB9OBqityIMT3fsmEAP9fuLe9URVc2QRDX7MTPV8StW52v8tospit78O6bcXTs5P4J3HLSudq0dyKNcusGGiZSG6oGyVFj8FwJyfdHpm46L7u6lR16yu3TMj4nRf5w5OdvS_EgTmYYaTBVq4osSfWOmPzUiF5sjC-BH92sZadtK6EoaJT-pjpm3RoQelE9cL-zxDBFtrg0SZfO86Ke9HVyuPp5I5XcjjXML8DCZR9Joi183gotQNHS59fDtfCArlBFurcrqcK8sNSjC72HuBaAVojXmREmfmAsbrtweZpUXe8l6Wx3fyRA2eeq71s0hivMS7EZG7qgApcYsIcUDsHTgmGtwD9AVqsinxcqSIUdD8RURPGeaKpVnqkQFWAOz3OjmAgDhLcd6pxYSDmuhqNsvGz85uj7NWDlqb85X6v7HVPm2X0wHXrvnm-hG5m9SZMQB-z5sAkyTKAKJKu85eUQH8HuM0aiao3vcYxNDT9d1Jc7Vz2Bf8XWjgV-puoaXPAGag8u18anrduIo2gZZGdBFLYBejoQHSn68RcFV8PU7GAjEyGyrgJzb5W_3nOlAeYoy8bhugwgOgXTrqsYXGlSQ74Bl3VlQKVEClUZ0CpliJ0URpmBhYlzQUUAO7Nv93Zpw3qubObujFuWNwNFI6EAC5d-y-zUucM-2ewmM0-jJphf-l&pos=104&s=58&src=GD_JOB_VIEW&t=SR&vt=w",
            "categoryMgocId": 10132,
            "easyApply": false,
            "employer": {
              "activeStatus": "ACTIVE",
              "bestProfile": {
                "id": 313190
              },
              "id": 285118,
              "name": "Pasona NA Inc.",
              "ratings": {
                "overallRating": 3.5
              },
              "shortName": "Pasona NA",
              "size": "51 to 200 Employees",
              "squareLogoUrl": "https://media.glassdoor.com/sql/285118/pasona-na-squarelogo-1426237112600.png"
            },
            "employerNameFromSearch": "PASONA N A, INC.",
            "expired": false,
            "goc": "devops engineer",
            "gocId": 102489,
            "hideCEOInfo": false,
            "indeedJobAttribute": {
              "education": [
                "UTPWG"
              ],
              "educationLabel": [
                "Associate's degree"
              ],
              "skills": [
                "44AQZ",
                "64VXT",
                "A3TZC",
                "BC7SU",
                "D866K",
                "DKNQM",
                "FADZP",
                "GFRKJ",
                "GWKWY",
                "H98DC",
                "J3CT2",
                "R6MKU",
                "RZR2K",
                "T65FY",
                "WSBNK"
              ],
              "skillsLabel": [
                "Spanish",
                "Azure",
                "SAP",
                "Accounting software",
                "English",
                "Japanese",
                "Microservices",
                "AWS",
                "Incident response",
                "Docker",
                "Release management",
                "Financial services",
                "Translation",
                "Proofreading",
                "Communication skills"
              ]
            },
            "isIndexableJobViewPage": false,
            "isSponsoredEmployer": true,
            "isSponsoredJob": true,
            "jobCountryId": 1,
            "jobLink": "https://www.glassdoor.com/partner/jobListing.htm?ao=1110586&cb=1773983005122&cpc=451933188B21919D&cs=1_b33d2003&guid=0000019d09a06b078f14733fcf925081&jobListingId=1010024904229&jrtk=5-yul1-0-1jk4q0qpsgmvh800-5ab88e2ae74b63b7---6NYlbfkN0BQ0BgX18I10G6uoQ7vFAhySPo543-EiU2WryMBkb_AmY7Ep3qJ4G2RmxulaXh7nbU_1Lr61cyIrEDpHiap53j9OyooCF3fxIUZMyqP7JxVtlvnasSpkfBq6L3m3S_5_dIbc8pGOMsvXEn2q1wYXRdG56LvvVGYUVZMUvOKL5mhiknyG5WDNg40vVYgEkAtOqdJVe9TSB9OBqityIMT3fsmEAP9fuLe9URVc2QRDX7MTPV8StW52v8tospit78O6bcXTs5P4J3HLSudq0dyKNcusGGiZSG6oGyVFj8FwJyfdHpm46L7u6lR16yu3TMj4nRf5w5OdvS_EgTmYYaTBVq4osSfWOmPzUiF5sjC-BH92sZadtK6EoaJT-pjpm3RoQelE9cL-zxDBFtrg0SZfO86Ke9HVyuPp5I5XcjjXML8DCZR9Joi183gotQNHS59fDtfCArlBFurcrqcK8sNSjC72HuBaAVojXmREmfmAsbrtweZpUXe8l6Wx3fyRA2eeq71s0hivMS7EZG7qgApcYsIcUDsHTgmGtwD9AVqsinxcqSIUdD8RURPGeaKpVnqkQFWAOz3OjmAgDhLcd6pxYSDmuhqNsvGz85uj7NWDlqb85X6v7HVPm2X0wHXrvnm-hG5m9SZMQB-z5sAkyTKAKJKu85eUQH8HuM0aiao3vcYxNDT9d1Jc7Vz2Bf8XWjgV-puoaXPAGag8u18anrduIo2gZZGdBFLYBejoQHSn68RcFV8PU7GAjEyGyrgJzb5W_3nOlAeYoy8bhugwgOgXTrqsYXGlSQ74Bl3VlQKVEClUZ0CpliJ0URpmBhYlzQUUAO7Nv93Zpw3qubObujFuWNwNFI6EAC5d-y-zUucM-2ewmM0-jJphf-l&pos=104&s=58&src=GD_JOB_AD&t=SR&vt=w",
            "jobResultTrackingKey": "5-yul1-3-1jk4q0uc9294hg00-1jk4q0qpsgmvh800---6NYlbfkN0BQ0BgX18I10G6uoQ7vFAhySPo543-EiU2WryMBkb_AmY7Ep3qJ4G2RmxulaXh7nbU_1Lr61cyIrEDpHiap53j9OyooCF3fxIUZMyqP7JxVtlvnasSpkfBq6L3m3S_5_dIbc8pGOMsvXEn2q1wYXRdG56LvvVGYUVZMUvOKL5mhiknyG5WDNg40vVYgEkAtOqdJVe9TSB9OBqityIMT3fsmEAP9fuLe9URVc2QRDX7MTPV8StW52v8tospit78O6bcXTs5P4J3HLSudq0dyKNcusGGiZSG6oGyVFj8FwJyfdHpm46L7u6lR16yu3TMj4nRf5w5OdvS_EgTmYYaTBVq4osSfWOmPzUiF5sjC-BH92sZadtK6EoaJT-pjpm3RoQelE9cL-zxDBFtrg0SZfO86Ke9HVyuPp5I5XcjjXML8DCZR9Joi183gotQNHS59fDtfCArlBFurcrqcK8sNSjC72HuBaAVojXmREmfmAsbrtweZpUXe8l6Wx3fyRA2eeq71s0hivMS7EZG7qgApcYsIcUDsHTgmGtwD9AVqsinxcqSIUdD8RURPGeaKpVnqkQFWAOz3OjmAgDhLcd6pxYSDmuhqNsvGz85uj7NWDlqb85X6v7HVPm2X0wHXrvnm-hG5m9SZMQB-z5sAkyTKAKJKu85eUQH8HuM0aiao3vcYxNDT9d1Jc7Vz2Bf8XWjgV-puoaXPAGag8u18anrduIo2gZZGdBFLYBejoQHSn68RcFV8PU7GAjEyGyrgJzb5W_3nOlAeYoy8bhugwgOgXTrqsYXGlSQ74Bl3VlQKVEClUZ0CpliJ0URpmBhYlzQUUAO7Nv93Zpw3qubObujFuWNwNFI6EAC5d-y-zUucM-2ewmM0-jJphf-l",
            "jobTitleText": "Application Platform DevOps Engineer",
            "jobType": [
              "Full-time"
            ],
            "jobTypeKeys": [
              "search-jobs.job-type-options.fulltime"
            ],
            "locId": 1132348,
            "locationName": "New York, NY",
            "locationType": "C",
            "normalizedJobTitle": "devops engineer",
            "payCurrency": "USD",
            "payPeriod": "HOURLY",
            "payPeriodAdjustedPay": {
              "p10": 48,
              "p50": 50.5,
              "p90": 53
            },
            "rating": 3.5,
            "salarySource": "EMPLOYER_PROVIDED",
            "seoJobLink": "https://www.glassdoor.com/job-listing/application-platform-devops-engineer-pasona-na-JV_IC1132348_KO0,36_KE37,46.htm?jl=1010024904229",
            "serpUrlForJobListing": "/Job/new-york-ny-devops-engineer-jobs-SRCH_IL.0,11_IC1132348_KO12,27.htm?jl=1010024904229&srs=JV_APPLYPANE",
            "sgocId": 1007
          },
          "job": {
            "description": "<div><ul><li><b>Japanese language skills are highly preferred.</b></li><li><b>Experience of DevOps and CI/CD is required.</b></li></ul><p></p><p><b><br> Job Details</b></p><ul><li> <b>Job Title:</b> Application Platform / DevOps Engineer</li><li> <b>Working Location:</b> NY</li><li> <b>Working style: </b>Hybrid (Onsite preferred 2&ndash;3 days/week, flexible)</li><li> <b>Working Hours:</b> Full-time preferred (negotiable)</li><li> <b>Language: </b>English (Japanese is a plus)</li><li> <b>Pay Rate:</b> $48-53/hour</li><li> <b>Employment type:</b> Temp to Perm</li></ul><p></p><p><b><br> ︎Job Summary</b></p><p> We are looking for a versatile Application Platform / DevOps Engineer to support an IT organization within a Japanese financial services firm in the Americas.</p><p> This role focuses on application platform operations, development support, and migration initiatives, working closely with multiple application teams in an Agile environment.</p><p><b> This position requires a broad technical skill set, hands-on mindset, and the ability to flexibly support various tools and processes across the application lifecycle.</b></p><p></p><p><b><br> ︎ Key Responsibilities:</b></p><ul><li> Provide operational support for application platforms, including maintenance, troubleshooting, and incident response.</li><li> Support application development initiatives, including coordination with multiple application teams.</li><li> Manage and support DevOps, CI/CD pipelines, container-based environments, and release processes</li><li> Support frequent application releases in an Agile development environment</li><li> Utilize GitHub for module management and application operational support</li><li> Support front-office and middle-office applications across the Americas (primarily web-based and microservices)</li></ul><p></p><p><b><br> ︎ Required Qualifications &amp; Skills:</b></p><ul><li> Broad experience across application platform operations, development support, and migration projects</li><li> Strong understanding of the full SDLC, with hands-on experience completing at least two full development cycles</li><li> Experience working in Agile development environments with frequent releases</li><li> Ability to coordinate effectively with multiple application teams</li><li> Strong communication skills in English</li></ul><p></p><p><b><br> ︎Preferred Qualifications</b></p><ul><li> Experience with DevOps-related technologies such as:</li></ul><p> o GitHub / GitHub Actions</p><p> o CI/CD pipelines</p><p> o Container technologies (e.g., Docker, Kubernetes)</p><p> o Cloud platforms (AWS and/or Azure)</p><ul><li> Experience supporting financial services</li></ul><p></p><p><b><br> ﻿</b><b>*Knowledge of accounting and SAP is required.</b></p><ul><li><b>Spanish or Japanese language skills are highly preferred.</b></li></ul><p></p><p><br> A Japanese company is seeking a SAP Helpdesk Support.</p><p></p><p><br> Work Hours: 7 hours shifts （Morning shift : 9:00 A.M. to 5:00 P.M. / Late Shift 12:00 P.M. to 8:00 P.M., Monday through Friday except holidays.</p><p> Base Salary $60K～$72K</p><p> Work Location: Client&rsquo;s Onsite in NYC. (depends on the client&rsquo;s needs/policy/regulations, might be changed assign number of days for working at their Onsite.)</p><p></p><p><br> Job Description</p><p> This position is stationed at the client&rsquo;s site. However, might be assigned for Telecommuting as Hybrid, depending on the client&rsquo;s needs. Responsibilities include providing troubleshoots for SAP<i>.</i></p><p></p><p><br> Summary</p><p> Essential Job Functions:</p><p> 1. SAP helpdesk support in English/Spanish or Japanese language</p><p> 1) Trouble shooting</p><p> Technical support at on-site or by email or telephone or remote access tool</p><p> 2) Operation support</p><p> User support for SAP software</p><p> 3) Documentation (user manual, FAQ, user announcement)</p><p> 4) User Education</p><p> 5) Record work (Help) log</p><p> Miscellaneous Job :</p><p> 2.Translation</p><p> ・Translation and proofreading English/Spanish materials or English/Japanese materials</p><p></p><p><br> Job Requirements</p><p> a)Education</p><p> Associate or bachelor&rsquo;s degree in Computer Science, Information Technology, or a related field for SAP would be plus.</p><p> b)Business Travel</p><p> Yes (depends on client&rsquo;s needs)</p><p></p><p><br> To apply please email your resume to myamamoto@pasona.com</p></div>",
            "discoverDate": "2026-03-05T00:00:00",
            "eolHashCode": 0,
            "importConfigId": 322429,
            "jobTitleId": 0,
            "jobTitleText": "Application Platform DevOps Engineer",
            "listingId": 1010024904229
          },
          "map": {
            "cityName": "New York, NY",
            "country": "United States",
            "employer": {
              "id": 285118,
              "name": "Pasona NA Inc."
            },
            "lat": 40.71417,
            "lng": -74.00639,
            "locationName": "New York, NY",
            "stateName": "New York State"
          },
          "overview": {
            "ceo": {
              "name": "Kenji Furushiro"
            },
            "headquarters": "New York, NY",
            "id": 285118,
            "links": {
              "benefitsUrl": "https://www.glassdoor.com/Benefits/Pasona-NA-Benefits-E285118.htm",
              "overviewUrl": "https://www.glassdoor.com/Overview/Working-at-Pasona-NA-EI_IE285118.11,20.htm",
              "photosUrl": "https://www.glassdoor.com/Photos/Pasona-NA-Office-Photos-E285118.htm",
              "reviewsUrl": "https://www.glassdoor.com/Reviews/Pasona-NA-Reviews-E285118.htm",
              "salariesUrl": "https://www.glassdoor.com/Salary/Pasona-NA-Salaries-E285118.htm"
            },
            "name": "Pasona NA Inc.",
            "primaryIndustry": {
              "industryId": 200032,
              "industryName": "HR Consulting",
              "sectorId": 10026,
              "sectorName": "Human Resources & Staffing"
            },
            "ratings": {
              "careerOpportunitiesRating": 3.4,
              "ceoRatingsCount": 2,
              "compensationAndBenefitsRating": 3.1,
              "cultureAndValuesRating": 3.6,
              "overallRating": 3.5,
              "recommendToFriendRating": 0.66,
              "seniorManagementRating": 3.2,
              "workLifeBalanceRating": 3.6
            },
            "revenue": "$25 to $100 million (USD)",
            "shortName": "Pasona NA",
            "size": "51 to 200 Employees",
            "sizeCategory": "SMALL_TO_MEDIUM",
            "squareLogoUrl": "https://media.glassdoor.com/sql/285118/pasona-na-squarelogo-1426237112600.png",
            "type": "Company - Private",
            "website": "https://www.pasona.com",
            "yearFounded": 1985
          }
        },
        "employerReviewHighlights": [
          {
            "categoryReviewCount": 5,
            "sentence": "Bad management and not following current trends",
            "sentiment": "NEGATIVE"
          },
          {
            "categoryReviewCount": 6,
            "sentence": "Culture is not good, need to improvement PMS and salary date",
            "sentiment": "NEGATIVE"
          },
          {
            "categoryReviewCount": 6,
            "sentence": "We will learn the Japanese culture of working style.",
            "sentiment": "POSITIVE"
          },
          {
            "categoryReviewCount": 4,
            "sentence": "Flexible and people were nice",
            "sentiment": "POSITIVE"
          },
          {
            "categoryReviewCount": 2,
            "sentence": "Never bored as multiple clients are assigned, benefits are good",
            "sentiment": "POSITIVE"
          },
          {
            "categoryReviewCount": 3,
            "sentence": "I was not busy at work but I found some colleagues worked overtime a lot due to the low salary.",
            "sentiment": "NEGATIVE"
          }
        ],
        "employerBenefitsOverview": {
          "benefitsHighlights": [
            {
              "benefit": {
                "icon": "health",
                "name": "Health Insurance"
              },
              "commentCount": 3,
              "highlightPhrase": "Health insurance covers more thank I expected. They also offer FSA"
            },
            {
              "benefit": {
                "icon": "retirement",
                "name": "401K Plan"
              },
              "commentCount": 3,
              "highlightPhrase": "Matching up to 5%. Not bad."
            }
          ],
          "employerBenefitSummary": {
            "comment": "<p><u><strong>Holiday Pay</strong></u></p> <p>Holiday pay will be eight (8) hours at the regular straight time rate if they are scheduled to work the</p> <p>last scheduled work day before the holiday and the first scheduled work day after the holiday.</p> <p>Company Holiday is about 10 days per year (including 6 major holidays—New year/President’s</p> <p>day/Memorial Day/Independence Day/Labor Day/Thanksgiving Day)</p> <p><u><strong><br>Paid Time Off</strong></u></p> <p>PTO - 128 hours per year (about 10.66 hours per month)</p> <p>Full-Time employees begin accruing PTO upon completion of the first pay period after the date of</p> <p>hire and may request to use their accrued PTO hours at the minimum increments of one (1) hour.</p> <p>Physical Check-up Leave Time- 16 hours per calendar year and become eligible to use after 90</p> <p>days of employment at the minimum increment of one (1) hour. The balance resets on January 1st.</p> <p> </p> <p><u><strong>Health insurance and other benefit plans</strong></u></p> <p>Group medical insurance plan- The company offers group medical, dental, prescription drug</p> <p>vision, life and short term/long term disability insurance coverage to employees upon the date of</p> <p>hire.</p> <p>Other Group benefit plans- The company offers Health Care/Dependent Care FSA to regular</p> <p>full-time employees after 90 days from the date of hire.</p> <p> </p> <p><u><strong>401k plan</strong></u></p> <p>Eligibility- upon completion of six (6) months of service and if they are at least twenty-one (21)</p> <p>years old.</p> <p>Company match- The Company will make a Safe Harbor Matching Contribution equal to 100.0% of</p> <p>your Elective Deferrals between 1 ~ 3%, 50% of your Elective Deferrals between 4 ~ 5%. (Thus, the</p> <p>maximum matching contribution is 4.0 %.)</p> <p> </p> <p>*Note: Benefit information may change without notice</p> <p><em><strong>Last revised on October 2019</strong></em></p>"
          },
          "overallBenefitRating": 3.6,
          "totalBenefitReviews": 22
        },
        "employerBenefitsReviews": [
          {
            "benefitComments": [
              {
                "comment": "Not perfect but comprehensive package",
                "id": 11676003
              }
            ],
            "city": {
              "name": "Torrance, CA"
            },
            "createDate": "2025-02-18T20:39:34.323",
            "currentJob": false,
            "rating": 5,
            "state": {
              "name": "California"
            },
            "userEnteredJobTitle": "Talent Acquisition"
          },
          {
            "benefitComments": [
              {
                "comment": "Employee of this company are provided with 401K.",
                "id": 10609500
              }
            ],
            "city": {
              "name": "California City, CA"
            },
            "createDate": "2024-08-21T17:10:31.66",
            "currentJob": false,
            "rating": 3,
            "state": {
              "name": "California"
            }
          },
          {
            "benefitComments": [
              {
                "comment": "The benefits that the company offers are great. I believe the price and the plan coverage are impressive. I haven’t had any issues in the past.",
                "id": 9891768
              }
            ],
            "city": {
              "name": "Los Angeles, CA"
            },
            "createDate": "2024-05-04T21:42:39.253",
            "currentJob": true,
            "rating": 5,
            "state": {
              "name": "California"
            },
            "userEnteredJobTitle": "Business Development"
          }
        ]
      },
      "jobLink": "https://www.glassdoor.com/partner/jobListing.htm?ao=1110586&cb=1773983005122&cpc=451933188B21919D&cs=1_b33d2003&guid=0000019d09a06b078f14733fcf925081&jobListingId=1010024904229&jrtk=5-yul1-0-1jk4q0qpsgmvh800-5ab88e2ae74b63b7---6NYlbfkN0BQ0BgX18I10G6uoQ7vFAhySPo543-EiU2WryMBkb_AmY7Ep3qJ4G2RmxulaXh7nbU_1Lr61cyIrEDpHiap53j9OyooCF3fxIUZMyqP7JxVtlvnasSpkfBq6L3m3S_5_dIbc8pGOMsvXEn2q1wYXRdG56LvvVGYUVZMUvOKL5mhiknyG5WDNg40vVYgEkAtOqdJVe9TSB9OBqityIMT3fsmEAP9fuLe9URVc2QRDX7MTPV8StW52v8tospit78O6bcXTs5P4J3HLSudq0dyKNcusGGiZSG6oGyVFj8FwJyfdHpm46L7u6lR16yu3TMj4nRf5w5OdvS_EgTmYYaTBVq4osSfWOmPzUiF5sjC-BH92sZadtK6EoaJT-pjpm3RoQelE9cL-zxDBFtrg0SZfO86Ke9HVyuPp5I5XcjjXML8DCZR9Joi183gotQNHS59fDtfCArlBFurcrqcK8sNSjC72HuBaAVojXmREmfmAsbrtweZpUXe8l6Wx3fyRA2eeq71s0hivMS7EZG7qgApcYsIcUDsHTgmGtwD9AVqsinxcqSIUdD8RURPGeaKpVnqkQFWAOz3OjmAgDhLcd6pxYSDmuhqNsvGz85uj7NWDlqb85X6v7HVPm2X0wHXrvnm-hG5m9SZMQB-z5sAkyTKAKJKu85eUQH8HuM0aiao3vcYxNDT9d1Jc7Vz2Bf8XWjgV-puoaXPAGag8u18anrduIo2gZZGdBFLYBejoQHSn68RcFV8PU7GAjEyGyrgJzb5W_3nOlAeYoy8bhugwgOgXTrqsYXGlSQ74Bl3VlQKVEClUZ0CpliJ0URpmBhYlzQUUAO7Nv93Zpw3qubObujFuWNwNFI6EAC5d-y-zUucM-2ewmM0-jJphf-l&pos=104&s=58&src=GD_JOB_AD&t=SR&vt=w",
      "jobListingDetails": {
        "adOrderId": 1110586,
        "ageInDays": 42,
        "applicationId": 0,
        "applyButtonDisabled": false,
        "applyUrl": "https://www.glassdoor.com/partner/jobListing.htm?ao=1110586&cb=1773983005122&cpc=451933188B21919D&cs=1_9d15e368&guid=0000019d09a06b078f14733fcf925081&jobListingId=1010024904229&jrtk=5-yul1-3-1jk4q0uc9294hg00-1jk4q0qpsgmvh800---6NYlbfkN0BQ0BgX18I10G6uoQ7vFAhySPo543-EiU2WryMBkb_AmY7Ep3qJ4G2RmxulaXh7nbU_1Lr61cyIrEDpHiap53j9OyooCF3fxIUZMyqP7JxVtlvnasSpkfBq6L3m3S_5_dIbc8pGOMsvXEn2q1wYXRdG56LvvVGYUVZMUvOKL5mhiknyG5WDNg40vVYgEkAtOqdJVe9TSB9OBqityIMT3fsmEAP9fuLe9URVc2QRDX7MTPV8StW52v8tospit78O6bcXTs5P4J3HLSudq0dyKNcusGGiZSG6oGyVFj8FwJyfdHpm46L7u6lR16yu3TMj4nRf5w5OdvS_EgTmYYaTBVq4osSfWOmPzUiF5sjC-BH92sZadtK6EoaJT-pjpm3RoQelE9cL-zxDBFtrg0SZfO86Ke9HVyuPp5I5XcjjXML8DCZR9Joi183gotQNHS59fDtfCArlBFurcrqcK8sNSjC72HuBaAVojXmREmfmAsbrtweZpUXe8l6Wx3fyRA2eeq71s0hivMS7EZG7qgApcYsIcUDsHTgmGtwD9AVqsinxcqSIUdD8RURPGeaKpVnqkQFWAOz3OjmAgDhLcd6pxYSDmuhqNsvGz85uj7NWDlqb85X6v7HVPm2X0wHXrvnm-hG5m9SZMQB-z5sAkyTKAKJKu85eUQH8HuM0aiao3vcYxNDT9d1Jc7Vz2Bf8XWjgV-puoaXPAGag8u18anrduIo2gZZGdBFLYBejoQHSn68RcFV8PU7GAjEyGyrgJzb5W_3nOlAeYoy8bhugwgOgXTrqsYXGlSQ74Bl3VlQKVEClUZ0CpliJ0URpmBhYlzQUUAO7Nv93Zpw3qubObujFuWNwNFI6EAC5d-y-zUucM-2ewmM0-jJphf-l&pos=104&s=58&src=GD_JOB_VIEW&t=SR&vt=w",
        "categoryMgocId": 10132,
        "easyApply": false,
        "employer": {
          "activeStatus": "ACTIVE",
          "bestProfile": {
            "id": 313190
          },
          "id": 285118,
          "name": "Pasona NA Inc.",
          "ratings": {
            "overallRating": 3.5
          },
          "shortName": "Pasona NA",
          "size": "51 to 200 Employees",
          "squareLogoUrl": "https://media.glassdoor.com/sql/285118/pasona-na-squarelogo-1426237112600.png"
        },
        "employerNameFromSearch": "PASONA N A, INC.",
        "expired": false,
        "goc": "devops engineer",
        "gocId": 102489,
        "hideCEOInfo": false,
        "indeedJobAttribute": {
          "education": [
            "UTPWG"
          ],
          "educationLabel": [
            "Associate's degree"
          ],
          "skills": [
            "44AQZ",
            "64VXT",
            "A3TZC",
            "BC7SU",
            "D866K",
            "DKNQM",
            "FADZP",
            "GFRKJ",
            "GWKWY",
            "H98DC",
            "J3CT2",
            "R6MKU",
            "RZR2K",
            "T65FY",
            "WSBNK"
          ],
          "skillsLabel": [
            "Spanish",
            "Azure",
            "SAP",
            "Accounting software",
            "English",
            "Japanese",
            "Microservices",
            "AWS",
            "Incident response",
            "Docker",
            "Release management",
            "Financial services",
            "Translation",
            "Proofreading",
            "Communication skills"
          ]
        },
        "isIndexableJobViewPage": false,
        "isSponsoredEmployer": true,
        "isSponsoredJob": true,
        "jobCountryId": 1,
        "jobLink": "https://www.glassdoor.com/partner/jobListing.htm?ao=1110586&cb=1773983005122&cpc=451933188B21919D&cs=1_b33d2003&guid=0000019d09a06b078f14733fcf925081&jobListingId=1010024904229&jrtk=5-yul1-0-1jk4q0qpsgmvh800-5ab88e2ae74b63b7---6NYlbfkN0BQ0BgX18I10G6uoQ7vFAhySPo543-EiU2WryMBkb_AmY7Ep3qJ4G2RmxulaXh7nbU_1Lr61cyIrEDpHiap53j9OyooCF3fxIUZMyqP7JxVtlvnasSpkfBq6L3m3S_5_dIbc8pGOMsvXEn2q1wYXRdG56LvvVGYUVZMUvOKL5mhiknyG5WDNg40vVYgEkAtOqdJVe9TSB9OBqityIMT3fsmEAP9fuLe9URVc2QRDX7MTPV8StW52v8tospit78O6bcXTs5P4J3HLSudq0dyKNcusGGiZSG6oGyVFj8FwJyfdHpm46L7u6lR16yu3TMj4nRf5w5OdvS_EgTmYYaTBVq4osSfWOmPzUiF5sjC-BH92sZadtK6EoaJT-pjpm3RoQelE9cL-zxDBFtrg0SZfO86Ke9HVyuPp5I5XcjjXML8DCZR9Joi183gotQNHS59fDtfCArlBFurcrqcK8sNSjC72HuBaAVojXmREmfmAsbrtweZpUXe8l6Wx3fyRA2eeq71s0hivMS7EZG7qgApcYsIcUDsHTgmGtwD9AVqsinxcqSIUdD8RURPGeaKpVnqkQFWAOz3OjmAgDhLcd6pxYSDmuhqNsvGz85uj7NWDlqb85X6v7HVPm2X0wHXrvnm-hG5m9SZMQB-z5sAkyTKAKJKu85eUQH8HuM0aiao3vcYxNDT9d1Jc7Vz2Bf8XWjgV-puoaXPAGag8u18anrduIo2gZZGdBFLYBejoQHSn68RcFV8PU7GAjEyGyrgJzb5W_3nOlAeYoy8bhugwgOgXTrqsYXGlSQ74Bl3VlQKVEClUZ0CpliJ0URpmBhYlzQUUAO7Nv93Zpw3qubObujFuWNwNFI6EAC5d-y-zUucM-2ewmM0-jJphf-l&pos=104&s=58&src=GD_JOB_AD&t=SR&vt=w",
        "jobResultTrackingKey": "5-yul1-3-1jk4q0uc9294hg00-1jk4q0qpsgmvh800---6NYlbfkN0BQ0BgX18I10G6uoQ7vFAhySPo543-EiU2WryMBkb_AmY7Ep3qJ4G2RmxulaXh7nbU_1Lr61cyIrEDpHiap53j9OyooCF3fxIUZMyqP7JxVtlvnasSpkfBq6L3m3S_5_dIbc8pGOMsvXEn2q1wYXRdG56LvvVGYUVZMUvOKL5mhiknyG5WDNg40vVYgEkAtOqdJVe9TSB9OBqityIMT3fsmEAP9fuLe9URVc2QRDX7MTPV8StW52v8tospit78O6bcXTs5P4J3HLSudq0dyKNcusGGiZSG6oGyVFj8FwJyfdHpm46L7u6lR16yu3TMj4nRf5w5OdvS_EgTmYYaTBVq4osSfWOmPzUiF5sjC-BH92sZadtK6EoaJT-pjpm3RoQelE9cL-zxDBFtrg0SZfO86Ke9HVyuPp5I5XcjjXML8DCZR9Joi183gotQNHS59fDtfCArlBFurcrqcK8sNSjC72HuBaAVojXmREmfmAsbrtweZpUXe8l6Wx3fyRA2eeq71s0hivMS7EZG7qgApcYsIcUDsHTgmGtwD9AVqsinxcqSIUdD8RURPGeaKpVnqkQFWAOz3OjmAgDhLcd6pxYSDmuhqNsvGz85uj7NWDlqb85X6v7HVPm2X0wHXrvnm-hG5m9SZMQB-z5sAkyTKAKJKu85eUQH8HuM0aiao3vcYxNDT9d1Jc7Vz2Bf8XWjgV-puoaXPAGag8u18anrduIo2gZZGdBFLYBejoQHSn68RcFV8PU7GAjEyGyrgJzb5W_3nOlAeYoy8bhugwgOgXTrqsYXGlSQ74Bl3VlQKVEClUZ0CpliJ0URpmBhYlzQUUAO7Nv93Zpw3qubObujFuWNwNFI6EAC5d-y-zUucM-2ewmM0-jJphf-l",
        "jobTitleText": "Application Platform DevOps Engineer",
        "jobType": [
          "Full-time"
        ],
        "jobTypeKeys": [
          "search-jobs.job-type-options.fulltime"
        ],
        "locId": 1132348,
        "locationName": "New York, NY",
        "locationType": "C",
        "normalizedJobTitle": "devops engineer",
        "payCurrency": "USD",
        "payPeriod": "HOURLY",
        "payPeriodAdjustedPay": {
          "p10": 48,
          "p50": 50.5,
          "p90": 53
        },
        "rating": 3.5,
        "salarySource": "EMPLOYER_PROVIDED",
        "seoJobLink": "https://www.glassdoor.com/job-listing/application-platform-devops-engineer-pasona-na-JV_IC1132348_KO0,36_KE37,46.htm?jl=1010024904229",
        "serpUrlForJobListing": "/Job/new-york-ny-devops-engineer-jobs-SRCH_IL.0,11_IC1132348_KO12,27.htm?jl=1010024904229&srs=JV_APPLYPANE",
        "sgocId": 1007
      },
      "jobOverview": {
        "description": "<div><ul><li><b>Japanese language skills are highly preferred.</b></li><li><b>Experience of DevOps and CI/CD is required.</b></li></ul><p></p><p><b><br> Job Details</b></p><ul><li> <b>Job Title:</b> Application Platform / DevOps Engineer</li><li> <b>Working Location:</b> NY</li><li> <b>Working style: </b>Hybrid (Onsite preferred 2&ndash;3 days/week, flexible)</li><li> <b>Working Hours:</b> Full-time preferred (negotiable)</li><li> <b>Language: </b>English (Japanese is a plus)</li><li> <b>Pay Rate:</b> $48-53/hour</li><li> <b>Employment type:</b> Temp to Perm</li></ul><p></p><p><b><br> ︎Job Summary</b></p><p> We are looking for a versatile Application Platform / DevOps Engineer to support an IT organization within a Japanese financial services firm in the Americas.</p><p> This role focuses on application platform operations, development support, and migration initiatives, working closely with multiple application teams in an Agile environment.</p><p><b> This position requires a broad technical skill set, hands-on mindset, and the ability to flexibly support various tools and processes across the application lifecycle.</b></p><p></p><p><b><br> ︎ Key Responsibilities:</b></p><ul><li> Provide operational support for application platforms, including maintenance, troubleshooting, and incident response.</li><li> Support application development initiatives, including coordination with multiple application teams.</li><li> Manage and support DevOps, CI/CD pipelines, container-based environments, and release processes</li><li> Support frequent application releases in an Agile development environment</li><li> Utilize GitHub for module management and application operational support</li><li> Support front-office and middle-office applications across the Americas (primarily web-based and microservices)</li></ul><p></p><p><b><br> ︎ Required Qualifications &amp; Skills:</b></p><ul><li> Broad experience across application platform operations, development support, and migration projects</li><li> Strong understanding of the full SDLC, with hands-on experience completing at least two full development cycles</li><li> Experience working in Agile development environments with frequent releases</li><li> Ability to coordinate effectively with multiple application teams</li><li> Strong communication skills in English</li></ul><p></p><p><b><br> ︎Preferred Qualifications</b></p><ul><li> Experience with DevOps-related technologies such as:</li></ul><p> o GitHub / GitHub Actions</p><p> o CI/CD pipelines</p><p> o Container technologies (e.g., Docker, Kubernetes)</p><p> o Cloud platforms (AWS and/or Azure)</p><ul><li> Experience supporting financial services</li></ul><p></p><p><b><br> ﻿</b><b>*Knowledge of accounting and SAP is required.</b></p><ul><li><b>Spanish or Japanese language skills are highly preferred.</b></li></ul><p></p><p><br> A Japanese company is seeking a SAP Helpdesk Support.</p><p></p><p><br> Work Hours: 7 hours shifts （Morning shift : 9:00 A.M. to 5:00 P.M. / Late Shift 12:00 P.M. to 8:00 P.M., Monday through Friday except holidays.</p><p> Base Salary $60K～$72K</p><p> Work Location: Client&rsquo;s Onsite in NYC. (depends on the client&rsquo;s needs/policy/regulations, might be changed assign number of days for working at their Onsite.)</p><p></p><p><br> Job Description</p><p> This position is stationed at the client&rsquo;s site. However, might be assigned for Telecommuting as Hybrid, depending on the client&rsquo;s needs. Responsibilities include providing troubleshoots for SAP<i>.</i></p><p></p><p><br> Summary</p><p> Essential Job Functions:</p><p> 1. SAP helpdesk support in English/Spanish or Japanese language</p><p> 1) Trouble shooting</p><p> Technical support at on-site or by email or telephone or remote access tool</p><p> 2) Operation support</p><p> User support for SAP software</p><p> 3) Documentation (user manual, FAQ, user announcement)</p><p> 4) User Education</p><p> 5) Record work (Help) log</p><p> Miscellaneous Job :</p><p> 2.Translation</p><p> ・Translation and proofreading English/Spanish materials or English/Japanese materials</p><p></p><p><br> Job Requirements</p><p> a)Education</p><p> Associate or bachelor&rsquo;s degree in Computer Science, Information Technology, or a related field for SAP would be plus.</p><p> b)Business Travel</p><p> Yes (depends on client&rsquo;s needs)</p><p></p><p><br> To apply please email your resume to myamamoto@pasona.com</p></div>",
        "discoverDate": "2026-03-05T00:00:00",
        "eolHashCode": 0,
        "importConfigId": 322429,
        "jobTitleId": 0,
        "jobTitleText": "Application Platform DevOps Engineer",
        "listingId": 1010024904229
      },
      "jobResultTrackingKey": "5-yul1-3-1jk4q0uc9294hg00-1jk4q0qpsgmvh800---6NYlbfkN0BQ0BgX18I10G6uoQ7vFAhySPo543-EiU2WryMBkb_AmY7Ep3qJ4G2RmxulaXh7nbU_1Lr61cyIrEDpHiap53j9OyooCF3fxIUZMyqP7JxVtlvnasSpkfBq6L3m3S_5_dIbc8pGOMsvXEn2q1wYXRdG56LvvVGYUVZMUvOKL5mhiknyG5WDNg40vVYgEkAtOqdJVe9TSB9OBqityIMT3fsmEAP9fuLe9URVc2QRDX7MTPV8StW52v8tospit78O6bcXTs5P4J3HLSudq0dyKNcusGGiZSG6oGyVFj8FwJyfdHpm46L7u6lR16yu3TMj4nRf5w5OdvS_EgTmYYaTBVq4osSfWOmPzUiF5sjC-BH92sZadtK6EoaJT-pjpm3RoQelE9cL-zxDBFtrg0SZfO86Ke9HVyuPp5I5XcjjXML8DCZR9Joi183gotQNHS59fDtfCArlBFurcrqcK8sNSjC72HuBaAVojXmREmfmAsbrtweZpUXe8l6Wx3fyRA2eeq71s0hivMS7EZG7qgApcYsIcUDsHTgmGtwD9AVqsinxcqSIUdD8RURPGeaKpVnqkQFWAOz3OjmAgDhLcd6pxYSDmuhqNsvGz85uj7NWDlqb85X6v7HVPm2X0wHXrvnm-hG5m9SZMQB-z5sAkyTKAKJKu85eUQH8HuM0aiao3vcYxNDT9d1Jc7Vz2Bf8XWjgV-puoaXPAGag8u18anrduIo2gZZGdBFLYBejoQHSn68RcFV8PU7GAjEyGyrgJzb5W_3nOlAeYoy8bhugwgOgXTrqsYXGlSQ74Bl3VlQKVEClUZ0CpliJ0URpmBhYlzQUUAO7Nv93Zpw3qubObujFuWNwNFI6EAC5d-y-zUucM-2ewmM0-jJphf-l",
      "jobTitle": "Application Platform DevOps Engineer",
      "listingId": 1010024904229,
      "location": {
        "id": 1132348,
        "name": "New York, NY",
        "type": "C"
      },
      "locationName": "New York, NY",
      "map": {
        "cityName": "New York, NY",
        "country": "United States",
        "employer": {
          "id": 285118,
          "name": "Pasona NA Inc."
        },
        "lat": 40.71417,
        "lng": -74.00639,
        "locationName": "New York, NY",
        "stateName": "New York State"
      },
      "normalizedJobTitle": "devops engineer",
      "payCurrency": "USD",
      "payPeriod": "HOURLY",
      "payPeriodAdjustedPay": {
        "p10": 48,
        "p50": 50.5,
        "p90": 53
      },
      "salarySource": "EMPLOYER_PROVIDED",
      "savedJobId": 0,
      "seoJobLink": "https://www.glassdoor.com/job-listing/application-platform-devops-engineer-pasona-na-JV_IC1132348_KO0,36_KE37,46.htm?jl=1010024904229",
      "trackingData": {
        "jobViewDisplayTimeMillis": 0,
        "pageRequestGuid": "0000019d09a079699898816197251cb4",
        "requiresTracking": true,
        "searchTypeCode": "NS",
        "trackingUrl": "https://www.indeed.com/rc/gd/png?a=9yr8FVtIpDy83VVaQMQxTJWCTRgI8IAQuLCpmrri1g5QvKAN4OLTFG9NL3wYNjL0_ck5Vp4sX3FMPh1hZrY4zr9kEf3IIzwVjWsnpJ6oTgVpzjNPBxKdx3XqfatFtEGY2hsyVbvuOFlKdakU_4aFZYE5vpxOAXMKVk17Z1eS4gvMROt6YNiVZH14C3l16slTyxP7QrNdsOEyvWIplua0pDwrEdYDmJ3UlZ0Fc8WLrENokG9t9-7xKIJejb4IteTHWsu3H9NBiA0MSYO812jqIY2a0ZC2GlDkRMfjSnaCWEc6BQqcix9RlbrTBhoXqDkLMMOsgRlyWnt3sVfNbD5YGkZC6pLV_ScZs_yw-YWPc8KCXo2-CLXkx0LpfzbL1Yl8g73X5c6ZLYsJi-lYhUDpjWFLGgde6n1TBvttd_moTog6vcZLaKj4syQ2dqgmKZmcjZx-vR156Ko7MfEmLO_pNkbZXYdfAZ0H7rIY-UA9qaa1itujrf4TQYCr-jEngnKBWDQ-BJGcAHMM3nbkJF50jpd3M2cgG1DZbTzX2q0ReUGPEnYEo0vHQnzx1shz5IRPF4z-5YKzU8EBNUuUQnKicjIWZ2YaJpI2-bd81FVhcjzWFLR_3niWKDPtZx_wXl2vLlX_2E3T4jhUG1_SH5hrbBjngldjLLLrbFdypdLLhacGlyuskYb5W12NJShhMm7oMwSNXT1pWOkpxdZ8wyQQI9vanXEg3l1frSxPqGuT8c7G35hY8zcqIoIBF0yjuFy1CLLyeMCkpXXJeANOu8goluEdiQG9_CGTaqONIlSRWrVGnk--i2M560tjcErPxkXyggEXTKO4XLVZRPZoYyUDt07-dAELXVQSNaZLIlyGgF3nYJ8Gh5Z1FePOg0IjE9-q9XPR0dEGAUmjXg62Lmtd3FnXEiC2d_EzNsmj0eUTRdp-wSvGhhpN9B-LiVNLhZd2dTr5_WOMl06icHK3iz836VlE9mhjJQO3SdZ3gmMtZiVKVp8_zKg4UZx9mivmXdaq41zDE2m7dHLE4r35-Z5MfYhI3zgMUJPeEk8qAMMEvso83bdBQ8B-SV1ABGxqqtWc-nnlss3sWoq7oxo_Y81pHfNH41cfUqeG-l3GFHxTL-1VDQQI2bYlB_i3ztwyyjPV-l3GFHxTL-1VDQQI2bYlB0xODlht1vilWKFhYQFNdXImr04pYOj_HHspXaHXpx5ulHniVsx08V-b25D2_EIuYwbUHFbd675PSBJYyF7c9AbpXjrzpsBdPk3SWcKaedzQFMPaWCk_ddVVdlxdDd5uoP6wcAOl9MGLg2DgKJ6OBlhldFo5_MJFd8ZUUbniQMl61CgBZz2_FL24HheraShOfItSGXV7xIVn68zYvizVk583DK5WXl8w20yVSb2YqVWFEOBkoguFmMDnfKyLsjZeBXITyhANlQ-rfk5Zdbqbr1dHzZ6kvwFHCSXCadzpw2ftNQgH1CxJ261ISosxRHw0HjYjdkABtG-vjB0kYjZzS6qt5oncwOsfmAM4GuGQbhtt-6rBVMje2mvtmnLoMcyR7WkUgPBkbPszlvHhbcSSv_I&channel=sr-s_58&ctk=1jk4q0rohiucv800&org=0",
        "isSponsoredJob": true,
        "isSponsoredEmployer": true,
        "jobExpired": false,
        "lashedEmployer": "Pasona NA",
        "lashedEmployerId": 285118,
        "lashedIndustry": "HR Consulting",
        "lashedIndustryId": 200032,
        "lashedLocation": "New York, NY",
        "lashedLocationId": 1132348,
        "lashedLocationType": "C",
        "lashedOccupation": "Application Platform DevOps Engineer",
        "lashedOccupationId": 1010024904229,
        "lashedSector": "Human Resources & Staffing",
        "lashedSectorId": 10026
      },
      "employerBenefitsOverview": {
        "benefitsHighlights": [
          {
            "benefit": {
              "icon": "health",
              "name": "Health Insurance"
            },
            "commentCount": 3,
            "highlightPhrase": "Health insurance covers more thank I expected. They also offer FSA"
          },
          {
            "benefit": {
              "icon": "retirement",
              "name": "401K Plan"
            },
            "commentCount": 3,
            "highlightPhrase": "Matching up to 5%. Not bad."
          }
        ],
        "employerBenefitSummary": {
          "comment": "<p><u><strong>Holiday Pay</strong></u></p> <p>Holiday pay will be eight (8) hours at the regular straight time rate if they are scheduled to work the</p> <p>last scheduled work day before the holiday and the first scheduled work day after the holiday.</p> <p>Company Holiday is about 10 days per year (including 6 major holidays—New year/President’s</p> <p>day/Memorial Day/Independence Day/Labor Day/Thanksgiving Day)</p> <p><u><strong><br>Paid Time Off</strong></u></p> <p>PTO - 128 hours per year (about 10.66 hours per month)</p> <p>Full-Time employees begin accruing PTO upon completion of the first pay period after the date of</p> <p>hire and may request to use their accrued PTO hours at the minimum increments of one (1) hour.</p> <p>Physical Check-up Leave Time- 16 hours per calendar year and become eligible to use after 90</p> <p>days of employment at the minimum increment of one (1) hour. The balance resets on January 1st.</p> <p> </p> <p><u><strong>Health insurance and other benefit plans</strong></u></p> <p>Group medical insurance plan- The company offers group medical, dental, prescription drug</p> <p>vision, life and short term/long term disability insurance coverage to employees upon the date of</p> <p>hire.</p> <p>Other Group benefit plans- The company offers Health Care/Dependent Care FSA to regular</p> <p>full-time employees after 90 days from the date of hire.</p> <p> </p> <p><u><strong>401k plan</strong></u></p> <p>Eligibility- upon completion of six (6) months of service and if they are at least twenty-one (21)</p> <p>years old.</p> <p>Company match- The Company will make a Safe Harbor Matching Contribution equal to 100.0% of</p> <p>your Elective Deferrals between 1 ~ 3%, 50% of your Elective Deferrals between 4 ~ 5%. (Thus, the</p> <p>maximum matching contribution is 4.0 %.)</p> <p> </p> <p>*Note: Benefit information may change without notice</p> <p><em><strong>Last revised on October 2019</strong></em></p>"
        },
        "overallBenefitRating": 3.6,
        "totalBenefitReviews": 22
      },
      "employerBenefitsReviews": [
        {
          "benefitComments": [
            {
              "comment": "Not perfect but comprehensive package",
              "id": 11676003
            }
          ],
          "city": {
            "name": "Torrance, CA"
          },
          "createDate": "2025-02-18T20:39:34.323",
          "currentJob": false,
          "rating": 5,
          "state": {
            "name": "California"
          },
          "userEnteredJobTitle": "Talent Acquisition"
        },
        {
          "benefitComments": [
            {
              "comment": "Employee of this company are provided with 401K.",
              "id": 10609500
            }
          ],
          "city": {
            "name": "California City, CA"
          },
          "createDate": "2024-08-21T17:10:31.66",
          "currentJob": false,
          "rating": 3,
          "state": {
            "name": "California"
          }
        },
        {
          "benefitComments": [
            {
              "comment": "The benefits that the company offers are great. I believe the price and the plan coverage are impressive. I haven’t had any issues in the past.",
              "id": 9891768
            }
          ],
          "city": {
            "name": "Los Angeles, CA"
          },
          "createDate": "2024-05-04T21:42:39.253",
          "currentJob": true,
          "rating": 5,
          "state": {
            "name": "California"
          },
          "userEnteredJobTitle": "Business Development"
        }
      ],
      "employerReviewHighlights": [
        {
          "categoryReviewCount": 5,
          "sentence": "Bad management and not following current trends",
          "sentiment": "NEGATIVE"
        },
        {
          "categoryReviewCount": 6,
          "sentence": "Culture is not good, need to improvement PMS and salary date",
          "sentiment": "NEGATIVE"
        },
        {
          "categoryReviewCount": 6,
          "sentence": "We will learn the Japanese culture of working style.",
          "sentiment": "POSITIVE"
        },
        {
          "categoryReviewCount": 4,
          "sentence": "Flexible and people were nice",
          "sentiment": "POSITIVE"
        },
        {
          "categoryReviewCount": 2,
          "sentence": "Never bored as multiple clients are assigned, benefits are good",
          "sentiment": "POSITIVE"
        },
        {
          "categoryReviewCount": 3,
          "sentence": "I was not busy at work but I found some colleagues worked overtime a lot due to the low salary.",
          "sentiment": "NEGATIVE"
        }
      ]
    }
  }
}
```

## Field reference

### Job record (`type = "job"`)

- **type** *(string, required)*: Record type.
- **id** *(number, required)*: Stable job identifier.
- **url** *(string, required)*: Canonical job URL.
- **listingId** *(number, optional)*: Listing identifier.
- **jobTitle** *(string, optional)*: Job title shown on the listing.
- **jobPosting.descriptionHtml** *(string, optional)*: HTML version of the job description.
- **jobPosting.descriptionText** *(string, optional)*: Plain-text version of the job description.
- **jobPosting.jobPageUrl** *(string, optional)*: Job page URL.
- **jobPosting.seoJobPageUrl** *(string, optional)*: Search-friendly public job URL.
- **jobPosting.applyUrl** *(string, optional)*: Apply destination URL.
- **jobPosting.searchResultsUrl** *(string, optional)*: Search results URL associated with the listing.
- **jobPosting.discoveredAt** *(string, optional)*: Discovery date for the listing.
- **jobPosting.listingAgeDays** *(number, optional)*: Listing age in days.
- **jobPosting.isExpired** *(boolean, optional)*: Whether the job is marked expired.
- **jobPosting.hasEasyApply** *(boolean, optional)*: Whether Easy Apply is available.
- **jobPosting.isApplyButtonDisabled** *(boolean, optional)*: Whether the apply action is disabled.
- **jobPosting.applicationId** *(number, optional)*: Application-related identifier.
- **jobPosting.importConfigId** *(number, optional)*: Source-side configuration identifier when present.
- **jobPosting.titleId** *(number, optional)*: Title identifier when present.
- **jobPosting.eolHashCode** *(number, optional)*: Source hash value when present.
- **jobTaxonomy.normalizedTitle** *(string, optional)*: Normalized job title.
- **jobTaxonomy.occupationName** *(string, optional)*: Occupation label.
- **jobTaxonomy.occupationId** *(number, optional)*: Occupation identifier.
- **jobTaxonomy.occupations[].key** *(string, optional)*: Source occupation key associated with the listing.
- **jobTaxonomy.categoryId** *(number, optional)*: Category identifier.
- **jobTaxonomy.subCategoryId** *(number, optional)*: Subcategory or job-function identifier.
- **jobTaxonomy.countryId** *(number, optional)*: Country identifier.
- **jobTaxonomy.searchAttributes.education** *(array[string], optional)*: Education attribute codes.
- **jobTaxonomy.searchAttributes.educationLabel** *(array[string], optional)*: Education labels.
- **jobTaxonomy.searchAttributes.skills** *(array[string], optional)*: Skill attribute codes.
- **jobTaxonomy.searchAttributes.skillsLabel** *(array[string], optional)*: Skill labels.
- **jobLocation.locationId** *(number, optional)*: Location identifier.
- **jobLocation.locationName** *(string, optional)*: Display location.
- **jobLocation.locationType** *(string, optional)*: Location type code.
- **jobLocation.location.id** *(number, optional)*: Nested location identifier.
- **jobLocation.location.name** *(string, optional)*: Nested location name.
- **jobLocation.location.type** *(string, optional)*: Nested location type.
- **jobLocation.map.cityName** *(string, optional)*: City name.
- **jobLocation.map.country** *(string, optional)*: Country name.
- **jobLocation.map.locationName** *(string, optional)*: Map display location.
- **jobLocation.map.stateName** *(string, optional)*: State or region name.
- **jobLocation.map.lat** *(number, optional)*: Latitude.
- **jobLocation.map.lng** *(number, optional)*: Longitude.
- **jobLocation.map.employer.id** *(number, optional)*: Employer identifier linked to the map entry.
- **jobLocation.map.employer.name** *(string, optional)*: Employer name linked to the map entry.
- **compensation.currency** *(string, optional)*: Currency code.
- **compensation.payPeriod** *(string, optional)*: Pay period label.
- **compensation.salarySource** *(string, optional)*: Salary source label.
- **compensation.range.p10** *(number, optional)*: Lower-end pay estimate.
- **compensation.range.p50** *(number, optional)*: Midpoint pay estimate.
- **compensation.range.p90** *(number, optional)*: Upper-end pay estimate.
- **compensation.searchMidpoint** *(number, optional)*: Search midpoint value.
- **company.companyId** *(number, optional)*: Company identifier.
- **company.companyName** *(string, optional)*: Company name.
- **company.legalName** *(string, optional)*: Legal or full employer name from the search result payload.
- **company.shortName** *(string, optional)*: Short company name.
- **company.activeStatus** *(string, optional)*: Company status.
- **company.industryId** *(number, optional)*: Industry identifier.
- **company.bestProfileId** *(number, optional)*: Best-profile identifier.
- **company.logoUrl** *(string, optional)*: Logo URL.
- **company.overallRating** *(number, optional)*: Overall company rating.
- **company.ratings.careerOpportunitiesRating** *(number, optional)*: Career opportunities rating.
- **company.ratings.ceoRatingsCount** *(number, optional)*: CEO ratings count.
- **company