# JobAssistAI – Conversational Job Recommendation Chatbot

A simple, end-to-end chatbot that **collects a user’s profile**, **maps job specs from a catalogue**, **scores and filters jobs**, and **presents top recommendations** in a conversational flow. It uses OpenAI Chat Completions for moderation, intent confirmation, dictionary extraction, and natural‑language responses. 

---

## What it does
- **Moderation check** on user input & assistant messages. 
- **Intent confirmation** to validate five required keys: Education, Experience, Technical Skills, Preferred Locations, Expected Salary. 
- **Dictionary extraction** to normalize free‑form user input into a strict profile schema. 
- **Job feature mapping** (Education, Experience range, Skills) parsed from each job description via LLM. 
- **Matching & scoring** on skills overlap, location fit, experience band, and salary threshold; returns **Top‑N** jobs. 
- **Conversational summaries** of recommended jobs with links and salaries. 

---

## Files
- `JobAssistAI_Chatbot_Project.ipynb` – main notebook/script containing all stages (moderation, intent confirmation, product mapping, matching, recommendation, dialogue loop).
- `job_postings.csv` - the data file which contains available jobs with the associated job details and descriptions

---

## Requirements
- Python 3.9+
- Packages: `pandas`, `openai`, `tenacity`, `ast`, `json`, plus any data utilities used in the notebook. 
- An **OpenAI API key** available as environment variable `OPENAI_API_KEY`.

Install (example):
```bash
pip install pandas openai tenacity
```

---

## How to run (quick start)
1. **Prepare a job catalogue** in a DataFrame compatible with the code (columns like *Company Name*, *Job Title*, *Job Description*, *Job Location*, *Job Posting URL*, *Normalized Salary*). The script creates a `Job Features` column by calling `product_map_layer(job_description)`. 
2. **Start the dialogue loop** by calling `dialogue_mgmt_system()`; the bot will greet, collect profile, validate keys, and then print **Top‑5 jobs** with a summary. 
3. **Continue chatting** to request more jobs or ask follow‑ups; moderation runs on every turn. 

---

## Configuration & Notes
- Model names and seeds for Chat Completions are set inside helper functions; adjust as needed (e.g., `MODEL`, `gpt-3.5-turbo`). 
- Experience range parsing uses tuples like `(min, max)` and treats `X+` as `(X, 45)` (cap). 
- Education mapping: `Undergraduate < Graduate < Post Graduate`; user degree must meet or exceed the job’s required level. 
- Score combines: **skills intersection**, **location match (or All)**, **salary threshold**, **experience band fit**. Higher score ranks first; ties break by salary. 

Maintainer: Gouri Karthik Gembali
