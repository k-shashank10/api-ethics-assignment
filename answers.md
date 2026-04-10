
Problem Statement
You are a junior data analyst at a healthcare startup. Your team has built a Python script that calls a public health statistics API to collect patient-level records. The raw response data includes fields such as full name, email, date of birth, zip code, job title, and diagnosis notes. Your manager has asked you to clean and prepare this dataset responsibly before it is shared with an external research partner.

**Task 1 — Classify and Handle PII Fields** 

**Field**                  **Type of PII**       **Action to be Taken**        **Why**
1. full_name,                 Direct                       Drop                   Can be used for direct identification
2. email,                     Direct                       Mask                   Risk of privacy while sharing
3. date_of_birth,             Direct                       Pseudonymize           Converting to Age Group to Protect Identity
4. zip_code,                  Indirect                     Mask                   Prevents pinpointing exact location
5. job_title,                 Indirect                     Keep                   It doesn’t identify someone directly
6. diagnosis_notes            Indirect                     Pseudonymize           Notes may contain sensitive information



**Task 2 — Audit the API Script for Ethical Compliance** 

Data collection script is shown below:

import requests

API_URL = "https://healthstats-api.example.com/records"
API_KEY = "free_tier_key_abc123"

records = []
for page in range(1, 101):
    response = requests.get(API_URL, params={"page": page, "key": API_KEY})
    data = response.json()
    records.extend(data["results"])

1. **Violation 1: Using a free tier API key for bulk/commercial use**
**Problem:** The script uses a free tier key (free_tier_key_abc123) but collects 100 pages of patient records. Free tiers are meant for testing, not large‑scale or commercial use.
**Fix**: Use a proper commercial API key.
Correction: API_KEY = "commercial_tier_key_xyz789"

2. **Violation 2: Permanently storing raw patient‑level records.**
**Problem:** The script saves all records permanently, which violates ethical rules and likely the API’s terms of service. Sensitive health data should not be stored forever.
**Fix:** Store only anonymized or aggregated data, and respect retention limits.
**Correction:**
clean_records = anonymize(records)   # (remove names, emails, etc.)
save_to_database(clean_records, retention_days=30)



