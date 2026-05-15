# 📊 Job Market Salary Analysis — CASE WHEN in SQL

Exploratory SQL analysis on job posting data using conditional logic (`CASE WHEN`) to bucket, categorize, and standardize salaries across data roles.

**Tool:** DuckDB  
**Dataset:** `job_postings_fact` (~100k+ job postings)  
**Skills practiced:** `CASE WHEN`, `LIKE`, conditional aggregation, CTEs, NULL handling

---

## 📁 File

```
queries/
└── salary_analysis.sql
```

---

## 🔍 What's Inside

### 1. Basic Salary Bucketing
Classify hourly salaries into `Low / Medium / High` tiers using `CASE WHEN`.

### 2. Handling Missing Data
Add a `'Missing'` branch to explicitly surface NULLs — defensive best practice for data quality.

### 3. Job Title Categorization
Use `LIKE '%keyword%'` pattern matching to map messy free-text titles into clean categories (`Data Analyst`, `Data Engineer`, `Data Scientist`, `Other`).

### 4. Conditional Aggregation
Use `CASE WHEN` inside `MEDIAN()` to split salary distributions by tier — comparing low-end vs high-end pay per role.

### 5. Standardized Salary + Tiering (CTE)
Unify hourly and yearly salary into one comparable column using a CTE, then apply consistent `Low / Medium / High` tier labels across all roles.

---

## 💡 Key Insights

| Role | Total Postings | High-Tier Median |
|---|---|---|
| Software Engineer | 1,578 | $174,400 |
| Machine Learning Engineer | 1,334 | $166,000 |
| Senior Data Scientist | 3,271 | $157,500 |
| **Data Engineer** | **10,551** | **$140,000** |
| Data Scientist | 12,625 | $140,000 |
| Data Analyst | 13,600 | $114,978 |

- **Data Engineer** hits the sweet spot — large job market (10k+ postings) with strong high-tier pay ($140k median)
- **ML Engineer** commands a premium for AI/ML skills despite fewer postings
- **Data Analyst** has the lowest salary ceiling among data roles, reinforcing the value of upskilling toward DE/DS
- Hourly roles at ~$20/hr standardize to ~$41.6k/year — firmly entry-level / contract territory
- $300k Data Engineer outliers are likely Staff/Principal level at top-tier tech companies

---

## 🧠 What I Learned

- `CASE WHEN` is SQL's Swiss Army knife — works inside `SELECT`, aggregate functions, and `WHERE` conditions
- Always add a `NULL` branch even when filtering with `WHERE IS NOT NULL` — defensive coding habit
- `LIKE` pattern matching works but has gaps with edge cases like `"Analytics Engineer"` (no `%Data%` keyword)
- CTEs make complex transformations readable and reusable — especially for multi-step salary normalization
- Conditional aggregation with `MEDIAN(CASE WHEN ...)` is a powerful way to split distributions without multiple subqueries
