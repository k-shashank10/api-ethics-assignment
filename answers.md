

# **Task 1 — Classify and Handle PII Fields** 

**Field**                  
1. full_name,  
Type of PII: Direct,  Action: Drop                   
Why: Can be used for direct identification
2. email,                     
Type of PII:Direct,  Action:  Mask                   
Why:Risk of privacy while sharing
3. date_of_birth,             
Type of PII:Direct,  Action:  Pseudonymize           
Why:Converting to Age Group to Protect Identity
4. zip_code,                  
Type of PII:Indirect, Action: Mask                   
Why: Prevents pinpointing exact location
5. job_title,                
Type of PII:Indirect, Action: Keep
Why:It doesn’t identify someone directly
6. diagnosis_notes            
Type of PII:Indirect  Action: Pseudonymize           
Why: Notes may contain sensitive information



# **Task 2 — Audit the API Script for Ethical Compliance** 


1. **Violation 1: Using a free tier API key for bulk/commercial use**

**Problem:** The script uses a free tier key (free_tier_key_abc123) but collects 100 pages of patient records. Free tiers are meant for testing, not large‑scale or commercial use.

**Fix**: Use a proper commercial API key.

**Correction:** API_KEY = "commercial_tier_key_xyz789"

2. **Violation 2: Permanently storing raw patient‑level records.**

**Problem:** The script saves all records permanently, which violates ethical rules and likely the API’s terms of service. Sensitive health data should not be stored forever.

**Fix:** Store only anonymized or aggregated data, and respect retention limits.

**Correction:**
clean_records = anonymize(records)   # (remove names, emails, etc.)
save_to_database(clean_records, retention_days=30)



