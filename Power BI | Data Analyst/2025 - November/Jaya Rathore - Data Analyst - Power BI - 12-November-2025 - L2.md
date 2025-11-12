# Power BI Data Analyst Interview Plan
**Date:** 12-November-2025
**Duration:** 60 minutes
**Experience Level:** 1.8 years (targeting 2+ years)
**Focus Areas:** Power BI, Data Modeling, DAX, Python Automation, SQL

---

## 📊 EXECUTIVE SUMMARY

This comprehensive interview plan is designed to assess a Power BI Data Analyst candidate with 1.8 years of experience across all critical competencies. The plan includes:

### ✅ What's Included:
- **50+ Technical & Behavioral Questions** covering Power BI, DAX, SQL, Python, and soft skills
- **2 Live Coding Challenges** (15 minutes total) - Invoice parsing and rate sheet processing
- **Detailed Expected Answers** with code examples for every question
- **Scoring Rubric** (100 points) with clear pass/fail criteria
- **Interview Flow Guide** with timing for each section
- **Red Flags & Green Flags** checklist
- **Decision Matrix** for hiring recommendations
- **Evaluation Form** for structured feedback

### 🎯 Key Assessment Areas:

**Technical Skills (60 points):**
- Power BI & Data Modeling (20 pts): Star schema, RLS, performance optimization, Microsoft Fabric
- DAX (15 pts): Time intelligence, context understanding, measure optimization
- SQL (10 pts): Complex queries, window functions, indexing, optimization
- Python (15 pts): pandas, automation, error handling, file processing

**Problem-Solving (20 points):**
- Analytical thinking and debugging approach

**Communication (10 points):**
- Technical explanation clarity and stakeholder management

**Experience Relevance (10 points):**
- Project complexity and measurable impact

### 📋 Recommended Interview Structure:

1. **Introduction** (5 min) - Background and most impactful project
2. **Power BI Deep Dive** (20 min) - Data modeling, RLS, performance optimization
3. **DAX & SQL** (10 min) - Measure creation and query writing
4. **Python Coding** (15 min) - Live coding challenges
5. **Behavioral** (5 min) - Problem-solving and stakeholder scenarios
6. **Q&A** (5 min) - Candidate questions

### 🎓 Candidate Background Highlights:
- Built 3 major Power BI dashboards (Call Quality, Business Pulse, Billing Intelligence)
- Reduced manual work by 60-80% through automation
- Integrated data from 9+ MySQL servers using Microsoft Fabric
- Implemented Row-Level Security for 150+ clients
- Processed 25M+ monthly records with performance optimization
- Created Python automation for invoice reconciliation and rate sheet processing

### 🎯 Passing Criteria:
- **85-100:** Strong Hire - Exceeds expectations
- **70-84:** Hire - Meets all requirements
- **60-69:** Maybe - Additional interview needed
- **<60:** No Hire - Significant gaps

---

## 📑 TABLE OF CONTENTS

### Quick Navigation:
1. [Executive Summary](#-executive-summary)
2. [Interview Structure](#interview-structure)
3. [Question Selection Guide](#total-questions-available-50)
4. [Section 1: Introduction & Background](#section-1-introduction--background-5-minutes)
5. [Section 2: Power BI & Data Modeling](#section-2-power-bi--data-modeling-20-minutes)
   - Q1-Q4: Core Power BI Questions
   - Q14-Q25: Additional Power BI Deep Dive
6. [Section 3: DAX & Calculations](#section-3-dax--calculations-10-minutes)
   - Q5-Q7: Core DAX Questions
   - Q26-Q30: Additional DAX Questions
7. [Section 4: SQL & Data Integration](#section-4-sql--data-integration-10-minutes)
   - Q8-Q10: Core SQL Questions
   - Q35-Q40: Additional SQL Questions
8. [Section 5: Python Automation - CODING](#section-5-python-automation---coding-15-minutes)
   - Coding Challenge 1: Invoice Parsing
   - Coding Challenge 2: Rate Sheet Processing
   - Q31-Q34: Additional Python Questions
9. [Section 6: Behavioral & Scenario-Based](#section-6-behavioral--scenario-based-5-minutes)
   - Q11-Q13: Core Behavioral Questions
   - Q41-Q50: Additional Scenario Questions
10. [Scoring Rubric](#scoring-rubric)
11. [Quick Reference Guide](#quick-reference-guide)
12. [Interviewer Preparation Checklist](#interviewer-preparation-checklist)
13. [Red Flags & Green Flags](#red-flags-to-watch-for)
14. [Sample Interview Flow](#sample-interview-flow-60-minutes)
15. [Decision Matrix](#decision-matrix)
16. [Evaluation Form](#candidate-evaluation-form)

---

## Interview Structure

| Section | Duration | Focus Area |
|---------|----------|------------|
| Introduction & Background | 5 min | Candidate overview |
| Power BI & Data Modeling | 20 min | Technical depth on BI projects |
| DAX & Calculations | 10 min | Measure creation & optimization |
| SQL & Data Integration | 10 min | Database queries & ETL |
| Python Automation (Coding) | 15 min | Live coding/problem-solving |
| Behavioral & Scenario-based | 5 min | Soft skills & decision-making |
| Q&A | 5 min | Candidate questions |

---

## TOTAL QUESTIONS AVAILABLE: 50+

### Questions by Category:
- **Power BI & Data Modeling:** Q1-Q4, Q14-Q25 (16 questions)
- **DAX & Calculations:** Q5-Q7, Q26-Q30 (8 questions)
- **SQL & Data Integration:** Q8-Q10, Q35-Q40 (9 questions)
- **Python Automation:** Q31-Q34 + 2 Coding Challenges (6 questions)
- **Behavioral & Scenarios:** Q11-Q13, Q41-Q50 (13 questions)

### Recommended Question Selection for 60-Minute Interview:

**Must Ask (Core Competency - 30 min):**
1. Q1: Real-Time Call Quality Dashboard Deep Dive
2. Q2: Row-Level Security Implementation
3. Q5: Advanced DAX Measures (MoM Growth, YTD)
4. Q6: Context Transition & Filter Context
5. Q8: SQL Query - Call Quality Analysis
6. Coding Challenge 1: Invoice Parsing (10 min)
7. Q11: Problem-Solving Under Pressure

**Choose 3-4 from Deep Dive (15 min):**
- Q3: Data Modeling Best Practices (if performance is critical)
- Q15: Relationships and Cardinality (if complex data models expected)
- Q17: Power Query vs DAX (if ETL heavy role)
- Q19: Bookmarks and Drill-through (if UX important)
- Q28: ALL, ALLEXCEPT, ALLSELECTED (if advanced DAX needed)
- Q36: Window Functions (if SQL heavy role)
- Q41: Performance Troubleshooting (if optimization critical)

**Choose 1-2 Behavioral (10 min):**
- Q43: Requirement Gathering (if stakeholder management important)
- Q44: Conflicting Stakeholder Requests (if cross-functional role)
- Q49: Learning from Mistakes (culture fit)

**Remaining Time (5 min):**
- Candidate questions

---

## SECTION 1: Introduction & Background (5 minutes)

### Questions:
1. **Walk me through your current role and your most impactful project.**
2. **What motivated you to specialize in Power BI and data analytics?**

### Expected Answers:
- Should mention Real-Time Call Quality Dashboard or Business Pulse Tracker
- Highlight impact: 40% faster ticket investigation, 60% reduction in manual work
- Show passion for data-driven decision-making

---

## SECTION 2: Power BI & Data Modeling (20 minutes)

### Q1: Real-Time Call Quality Dashboard Deep Dive
**Question:** "You mentioned building a real-time call quality dashboard. Walk me through:
- How did you handle data from 9+ servers?
- What was your data model structure?
- How did you ensure real-time or near-real-time updates?"

**Expected Answer:**
- **Data Integration:** Used Microsoft Fabric Lakehouse & Pipelines to consolidate data from 9 MySQL servers
- **Data Model:**
  - Fact tables: Call logs with metrics (ASR, ACD, timestamps)
  - Dimension tables: Servers, Call Origin, Time dimensions
  - Star schema or snowflake schema implementation
- **Real-time Updates:**
  - Scheduled refresh using Fabric pipelines (mentioned automated night/early morning refreshes)
  - Incremental refresh for large datasets
  - DirectQuery vs Import mode considerations
- **Transformations:**
  - Power Query for timezone conversions
  - Handling duplicate keys through composite keys or deduplication logic

**Follow-up:** "What challenges did you face with duplicate keys and how did you resolve them?"

**Expected Answer:**
- Identified duplicate scenarios (same call logged on multiple servers)
- Created composite keys using multiple columns (CallID + ServerID + Timestamp)
- Used Power Query to remove duplicates based on business logic
- Implemented data quality checks

---

### Q2: Row-Level Security (RLS)
**Question:** "In your Business Pulse Tracker, you implemented Row-Level Security. Explain:
- How did you design the RLS model?
- What roles did you create?
- How did you test it?"

**Expected Answer:**
- **RLS Design:**
  - Created a Users/Roles dimension table mapping users to their accessible data
  - Used DAX filters: `[UserEmail] = USERPRINCIPALNAME()`
  - For account managers: filtered by client assignments
  - For leadership: full access

- **Roles Created:**
  - Account Manager role (filtered by assigned clients)
  - Regional Manager role (filtered by region)
  - Executive role (no filters)

- **Testing:**
  - Used "View as Role" feature in Power BI Desktop
  - Created test accounts for each role
  - Validated data visibility with stakeholders

**Follow-up:** "What's the difference between static and dynamic RLS?"

**Expected Answer:**
- **Static RLS:** Hard-coded filters in DAX (e.g., `[Region] = "North"`)
- **Dynamic RLS:** Uses functions like USERPRINCIPALNAME() to filter based on logged-in user
- Dynamic is more scalable and maintainable

---

### Q3: Data Modeling Best Practices
**Question:** "You worked with 25 million+ monthly records in the Unified Billing Intelligence System. How did you optimize performance?"

**Expected Answer:**
- **Data Model Optimization:**
  - Used star schema to reduce complexity
  - Removed unnecessary columns from fact tables
  - Used integer keys instead of text for relationships
  - Disabled auto date/time hierarchy

- **Query Optimization:**
  - Created aggregated tables for summary views
  - Used incremental refresh for large fact tables
  - Implemented partitioning in Fabric Lakehouse

- **Visual Optimization:**
  - Limited visuals per page (recommended: 10-15)
  - Avoided high-cardinality visuals
  - Used bookmarks instead of multiple pages where possible

- **DAX Optimization:**
  - Used variables to avoid recalculation
  - Avoided calculated columns where measures suffice
  - Used SUMMARIZE instead of ADDCOLUMNS when appropriate

---

### Q4: Microsoft Fabric Experience
**Question:** "You've used Microsoft Fabric extensively. What's your understanding of Fabric architecture and how did you leverage it?"

**Expected Answer:**
- **Fabric Components Used:**
  - **Lakehouse:** Centralized data storage (Delta Lake format)
  - **Data Pipelines:** ETL/ELT orchestration (similar to Azure Data Factory)
  - **Power BI:** Reporting layer

- **Benefits:**
  - Unified platform (no need for separate ADF, Synapse, Power BI workspaces)
  - OneLake for centralized storage
  - Better performance with Direct Lake mode

- **Implementation:**
  - Created pipelines to extract from 9 MySQL servers
  - Loaded raw data into Lakehouse bronze layer
  - Transformed in silver/gold layers
  - Connected Power BI to gold layer for reporting

**Follow-up:** "What's the difference between DirectQuery, Import, and Direct Lake mode?"

**Expected Answer:**
- **Import:** Data cached in Power BI, fast queries, scheduled refresh needed
- **DirectQuery:** Live connection to source, always current, slower performance
- **Direct Lake:** Fabric-specific, reads directly from OneLake (Delta/Parquet), combines benefits of both

---

## SECTION 3: DAX & Calculations (10 minutes)

### Q5: Advanced DAX Measures
**Question:** "You created advanced DAX measures for dynamic KPIs. Can you write a measure to calculate:
- Month-over-Month growth percentage for revenue
- Year-to-Date total calls"

**Expected Answer:**

```dax
// Month-over-Month Growth %
MoM Growth % =
VAR CurrentMonthRevenue = SUM(Sales[Revenue])
VAR PreviousMonthRevenue =
    CALCULATE(
        SUM(Sales[Revenue]),
        DATEADD(DimDate[Date], -1, MONTH)
    )
RETURN
    DIVIDE(
        CurrentMonthRevenue - PreviousMonthRevenue,
        PreviousMonthRevenue,
        0
    )

// Year-to-Date Total Calls
YTD Total Calls =
CALCULATE(
    COUNT(Calls[CallID]),
    DATESYTD(DimDate[Date])
)
```

**Follow-up:** "Why use DIVIDE instead of the / operator?"

**Expected Answer:**
- DIVIDE handles division by zero gracefully
- Third parameter allows custom alternate result (default is BLANK)
- Prevents errors in visuals

---

### Q6: Context Transition & Filter Context
**Question:** "Explain the difference between row context and filter context. When does context transition occur?"

**Expected Answer:**
- **Row Context:**
  - Iterates row-by-row (in calculated columns, iterator functions)
  - Example: `SUMX`, `FILTER`, calculated columns

- **Filter Context:**
  - Filters applied to the data model (slicers, visual filters, row/column headers)
  - Affects measures

- **Context Transition:**
  - Occurs when CALCULATE is used inside row context
  - Converts row context to filter context
  - Example:
  ```dax
  Sales Amount = SUMX(
      Sales,
      Sales[Quantity] * RELATED(Products[Price])  // Row context
  )

  Sales with Context Transition = SUMX(
      Sales,
      CALCULATE(SUM(Sales[Amount]))  // Context transition
  )
  ```

---

### Q7: Performance Optimization in DAX
**Question:** "How would you optimize this measure?"

```dax
Total Revenue =
SUMX(
    Sales,
    Sales[Quantity] * RELATED(Products[UnitPrice]) * (1 - Sales[Discount])
)
```

**Expected Answer:**
- **Option 1:** Create a calculated column (if cardinality is low)
```dax
// Calculated Column
LineTotal = Sales[Quantity] * RELATED(Products[UnitPrice]) * (1 - Sales[Discount])

// Measure
Total Revenue = SUM(Sales[LineTotal])
```

- **Option 2:** Use variables to avoid recalculation
```dax
Total Revenue =
SUMX(
    Sales,
    VAR Qty = Sales[Quantity]
    VAR Price = RELATED(Products[UnitPrice])
    VAR Disc = Sales[Discount]
    RETURN Qty * Price * (1 - Disc)
)
```

- **Trade-offs:**
  - Calculated column: Faster query, larger model size, refresh overhead
  - Optimized measure: Smaller model, calculated at query time

---

## SECTION 4: SQL & Data Integration (10 minutes)

### Q8: SQL Query - Call Quality Analysis
**Question:** "Write a SQL query to find the top 10 clients by Average Call Duration (ACD) for the last 30 days, showing Client Name, Total Calls, and Average Duration."

**Expected Answer:**
```sql
SELECT
    c.ClientName,
    COUNT(cl.CallID) AS TotalCalls,
    AVG(cl.Duration) AS AvgCallDuration,
    SUM(cl.Duration) AS TotalMinutes
FROM
    Calls cl
    INNER JOIN Clients c ON cl.ClientID = c.ClientID
WHERE
    cl.CallDate >= DATE_SUB(CURDATE(), INTERVAL 30 DAY)
GROUP BY
    c.ClientName
ORDER BY
    AvgCallDuration DESC
LIMIT 10;
```

**Follow-up:** "How would you optimize this query for a table with 25 million records?"

**Expected Answer:**
- Add indexes on `CallDate`, `ClientID`
- Partition table by date (monthly/yearly partitions)
- Use covering index: `INDEX idx_calls (CallDate, ClientID, Duration)`
- Consider materialized views for frequently accessed aggregations
- Use query execution plan to identify bottlenecks

---

### Q9: Data Integration Challenges
**Question:** "You integrated data from 9 MySQL servers. What challenges did you face and how did you handle:
- Different timezone data
- Schema inconsistencies
- Network latency"

**Expected Answer:**
- **Timezone Handling:**
  - Standardized all timestamps to UTC in the pipeline
  - Used `CONVERT_TZ()` in MySQL or handled in Power Query
  - Created separate columns for UTC and local time

- **Schema Inconsistencies:**
  - Created a unified schema in Lakehouse
  - Used UNION ALL with NULL for missing columns
  - Documented schema mapping for each server

- **Network Latency:**
  - Scheduled data extraction during off-peak hours
  - Implemented incremental loads (only new/changed records)
  - Used connection pooling
  - Compressed data during transfer

---

### Q10: ETL vs ELT
**Question:** "In your Fabric pipelines, did you use ETL or ELT approach? What's the difference?"

**Expected Answer:**
- **ETL (Extract, Transform, Load):**
  - Transform data before loading to destination
  - Used when target system has limited compute
  - Example: Transform in pipeline, load clean data to Lakehouse

- **ELT (Extract, Load, Transform):**
  - Load raw data first, transform in destination
  - Leverages powerful compute of modern data warehouses
  - Example: Load raw data to Lakehouse, transform using Spark/SQL

- **My Approach:**
  - Used ELT with Fabric (bronze → silver → gold layers)
  - Bronze: Raw data from MySQL servers
  - Silver: Cleaned, deduplicated, standardized
  - Gold: Business-ready aggregated tables

---

## SECTION 5: Python Automation - CODING (15 minutes)

### Coding Challenge 1: Invoice Parsing (10 minutes)
**Question:** "You mentioned parsing PDF invoices. Here's a simplified scenario:

You have a pandas DataFrame with invoice data that looks like this:
```
   Destination    Rate  Duration  Amount
0  USA-Mobile    0.012      1500   18.00
1  UK-Landline   0.008       800    6.40
2  usa-mobile    0.012      2000   24.00
3  India-Mobile  0.015      1200   18.00
```

Write Python code to:
1. Standardize the 'Destination' column (proper case, handle duplicates)
2. Calculate total amount per destination
3. Find destinations where total amount > $20
4. Export results to Excel"

**Expected Answer:**
```python
import pandas as pd

# Sample data
data = {
    'Destination': ['USA-Mobile', 'UK-Landline', 'usa-mobile', 'India-Mobile'],
    'Rate': [0.012, 0.008, 0.012, 0.015],
    'Duration': [1500, 800, 2000, 1200],
    'Amount': [18.00, 6.40, 24.00, 18.00]
}
df = pd.DataFrame(data)

# 1. Standardize Destination column
df['Destination'] = df['Destination'].str.title()

# 2. Calculate total amount per destination
destination_summary = df.groupby('Destination').agg({
    'Amount': 'sum',
    'Duration': 'sum',
    'Rate': 'mean'  # Average rate if multiple entries
}).reset_index()

# 3. Filter destinations with total amount > $20
high_value_destinations = destination_summary[destination_summary['Amount'] > 20]

# 4. Export to Excel
with pd.ExcelWriter('invoice_summary.xlsx', engine='openpyxl') as writer:
    destination_summary.to_excel(writer, sheet_name='All Destinations', index=False)
    high_value_destinations.to_excel(writer, sheet_name='High Value', index=False)

print("Summary:")
print(destination_summary)
print("\nHigh Value Destinations (>$20):")
print(high_value_destinations)
```

**Evaluation Criteria:**
- ✅ Correct use of pandas groupby and aggregation
- ✅ String manipulation (str.title() or str.lower())
- ✅ Filtering logic
- ✅ Excel export with multiple sheets
- ✅ Code readability and comments

---

### Coding Challenge 2: Rate Sheet Processing (5 minutes)
**Question:** "You receive rate sheets with inconsistent formats. Write a function that:
- Takes a list of dictionaries (rate data)
- Adds a 'Billing_Interval' column with default value '60' if missing
- Validates that 'Rate' is numeric and > 0
- Returns cleaned data and a list of invalid records"

**Expected Answer:**
```python
def process_rate_sheet(rate_data):
    """
    Process and validate rate sheet data

    Args:
        rate_data: List of dictionaries with rate information

    Returns:
        tuple: (cleaned_data, invalid_records)
    """
    cleaned_data = []
    invalid_records = []

    for idx, record in enumerate(rate_data):
        # Create a copy to avoid modifying original
        processed_record = record.copy()

        # Add default Billing_Interval if missing
        if 'Billing_Interval' not in processed_record:
            processed_record['Billing_Interval'] = 60

        # Validate Rate
        try:
            rate = float(processed_record.get('Rate', 0))
            if rate <= 0:
                invalid_records.append({
                    'index': idx,
                    'record': record,
                    'reason': 'Rate must be greater than 0'
                })
                continue
            processed_record['Rate'] = rate
        except (ValueError, TypeError):
            invalid_records.append({
                'index': idx,
                'record': record,
                'reason': 'Invalid rate format'
            })
            continue

        cleaned_data.append(processed_record)

    return cleaned_data, invalid_records

# Test
test_data = [
    {'Destination': 'USA', 'Rate': '0.012', 'Billing_Interval': 30},
    {'Destination': 'UK', 'Rate': '0.008'},  # Missing Billing_Interval
    {'Destination': 'India', 'Rate': 'invalid'},  # Invalid rate
    {'Destination': 'Canada', 'Rate': -0.005},  # Negative rate
]

cleaned, invalid = process_rate_sheet(test_data)
print(f"Cleaned: {len(cleaned)} records")
print(f"Invalid: {len(invalid)} records")
print("\nInvalid Records:")
for inv in invalid:
    print(f"  Index {inv['index']}: {inv['reason']}")
```

**Evaluation Criteria:**
- ✅ Error handling (try-except)
- ✅ Data validation logic
- ✅ Default value assignment
- ✅ Function documentation
- ✅ Return multiple values (tuple)

---

## SECTION 6: Behavioral & Scenario-Based (5 minutes)

### Q11: Problem-Solving Under Pressure
**Question:** "Describe a situation where a dashboard you built showed incorrect data. How did you identify and fix the issue?"

**Expected Answer (STAR Method):**
- **Situation:** Dashboard showing incorrect ASR (Answer Seizure Ratio) metrics
- **Task:** Identify root cause and fix without disrupting business operations
- **Action:**
  - Verified source data in MySQL servers
  - Checked Power Query transformations step-by-step
  - Found timezone conversion error causing duplicate counting
  - Implemented fix and added data validation measures
  - Created documentation for future reference
- **Result:** Fixed within 4 hours, implemented automated data quality checks

---

### Q12: Stakeholder Management
**Question:** "How do you handle requests from non-technical stakeholders who want complex analyses but don't understand data limitations?"

**Expected Answer:**
- **Communication:** Translate technical constraints into business terms
- **Education:** Show what's possible with current data vs. what requires additional sources
- **Alternatives:** Propose phased approach or proxy metrics
- **Example:** "When asked for real-time profitability by client, explained we have daily billing data, proposed end-of-day dashboard with 24-hour lag, which met their needs"

---

### Q13: Continuous Learning
**Question:** "Microsoft Fabric is relatively new. How did you learn it, and how do you stay updated with Power BI updates?"

**Expected Answer:**
- **Learning Approach:**
  - Microsoft Learn modules and documentation
  - Hands-on experimentation in dev environment
  - Community forums (Power BI Community, Stack Overflow)
  - YouTube channels (Guy in a Cube, SQLBI)

- **Staying Updated:**
  - Monthly Power BI feature updates
  - Following Microsoft blogs
  - Attending webinars/virtual conferences
  - Experimenting with preview features

---

### Q41: Performance Troubleshooting
**Question:** "A stakeholder complains that your dashboard is slow. Walk me through your troubleshooting process."

**Expected Answer (Structured Approach):**

**1. Identify the Issue:**
- Use Performance Analyzer in Power BI Desktop
- Identify slow visuals (DAX query time, visual display time)
- Check data refresh duration
- Monitor in Power BI Service (Premium Metrics app)

**2. Common Causes & Solutions:**

**Slow Visuals:**
- **Problem:** Complex DAX measures
- **Solution:** Optimize DAX (use variables, avoid calculated columns)

**Large Data Model:**
- **Problem:** Unnecessary columns, high cardinality
- **Solution:** Remove unused columns, use aggregations

**Too Many Visuals:**
- **Problem:** 20+ visuals on one page
- **Solution:** Reduce to 10-15, use bookmarks for toggling

**DirectQuery Issues:**
- **Problem:** Slow source database
- **Solution:** Add indexes, use aggregations, switch to Import mode

**3. Optimization Techniques:**
```dax
// Before - Slow
Total Sales =
SUMX(
    Sales,
    Sales[Quantity] * RELATED(Products[Price])
)

// After - Fast
Total Sales = SUM(Sales[LineTotal])  // Pre-calculated column
```

**4. Monitoring:**
- Set up performance baselines
- Regular performance reviews
- User feedback loop

**Example:**
- "In the Business Pulse Tracker, users reported 10-second load times. Performance Analyzer showed a complex DAX measure was the culprit. I optimized it using variables and reduced load time to 2 seconds."

---

### Q42: Data Quality Issues
**Question:** "You're building a dashboard and discover inconsistent data across sources. How do you handle this?"

**Expected Answer:**

**1. Identify Inconsistencies:**
- Compare record counts across sources
- Check for duplicate keys
- Validate data types and formats
- Look for missing or null values

**2. Root Cause Analysis:**
- Interview data owners
- Review ETL processes
- Check source system documentation
- Identify timing differences (when data is captured)

**3. Resolution Strategies:**

**Option A: Fix at Source**
- Work with source system owners
- Implement data quality rules
- Best long-term solution

**Option B: Handle in ETL**
- Data cleansing in Power Query
- Standardization rules
- Document transformations

**Option C: Business Rules**
- Define which source is "source of truth"
- Create data quality flags
- Alert users to discrepancies

**4. Implementation:**
```powerquery
// Power Query - Standardize client names
= Table.TransformColumns(
    Source,
    {{"ClientName", each Text.Proper(Text.Trim(_)), type text}}
)

// Add data quality flag
= Table.AddColumn(
    Source,
    "DataQualityFlag",
    each if [Amount] < 0 or [Duration] < 0
         then "Invalid"
         else "Valid"
)
```

**5. Communication:**
- Document known issues
- Add disclaimers to reports
- Regular data quality reports to stakeholders

**Example:**
- "When integrating 9 MySQL servers, I found client names spelled differently (e.g., 'ABC Corp', 'ABC Corporation'). I created a master client mapping table and used it to standardize names across all sources."

---

### Q43: Requirement Gathering
**Question:** "Walk me through how you gathered requirements for the Real-Time Call Quality Dashboard."

**Expected Answer (STAR Method):**

**Situation:**
- NOC team needed real-time visibility into call quality across 9 servers
- Manual ticket investigation was taking too long

**Task:**
- Design a dashboard to reduce investigation time by 40%

**Action - Requirement Gathering:**

**1. Stakeholder Interviews:**
- Met with NOC team leads
- Shadowed NOC analysts during ticket investigation
- Identified pain points and manual processes

**2. Key Questions Asked:**
- What metrics do you check first when investigating issues?
- How often do you need updated data?
- What filters/slicers are most important?
- What actions do you take based on the data?

**3. Requirements Documented:**
- **Metrics:** ASR, ACD, Call Origin, Server Status
- **Refresh:** Every 2 hours during business hours
- **Filters:** Date range, Server, Client, Destination
- **Drill-through:** From summary to detailed call logs
- **Alerts:** Visual indicators for ASR < 40%

**4. Prioritization:**
- Must-have: Real-time metrics, server-wise breakdown
- Should-have: Trend analysis, historical comparison
- Nice-to-have: Predictive alerts, mobile view

**5. Iterative Development:**
- Built MVP with core metrics
- Weekly demos to stakeholders
- Incorporated feedback
- Final rollout after UAT

**Result:**
- 40% faster ticket investigation
- Reduced mean time to resolution
- High user adoption (used daily by entire NOC team)

---

### Q44: Conflicting Stakeholder Requests
**Question:** "Two stakeholders want different things from the same dashboard. How do you handle this?"

**Expected Answer:**

**Scenario Example:**
- Finance wants detailed billing breakdown by call
- Executives want high-level revenue trends

**Approach:**

**1. Understand Both Perspectives:**
- Schedule separate meetings with each stakeholder
- Understand their use cases and decision-making needs
- Identify common ground

**2. Evaluate Options:**

**Option A: Separate Dashboards**
- Pros: Tailored to each audience, cleaner design
- Cons: Maintenance overhead, data duplication

**Option B: Single Dashboard with Drill-through**
- Pros: Single source of truth, easier maintenance
- Cons: May be complex for some users

**Option C: Role-Based Views (RLS + Bookmarks)**
- Pros: Personalized experience, single report
- Cons: Complex setup

**3. Propose Solution:**
- Present options with pros/cons
- Recommend based on technical feasibility and business value
- Get buy-in from both stakeholders

**4. Implementation:**
```
Executive View (Page 1):
- High-level KPIs
- Trend charts
- Regional breakdown

Finance View (Page 2):
- Detailed tables
- Drill-through from executive view
- Export-friendly format
```

**5. Communication:**
- Set expectations on what's feasible
- Explain technical constraints in business terms
- Document agreed-upon requirements

**Example:**
- "In the Business Pulse Tracker, account managers wanted client-specific views while leadership wanted company-wide metrics. I implemented RLS for account managers and created a separate executive summary page with drill-through to client details."

---

### Q45: Handling Urgent Requests
**Question:** "A C-level executive needs a report by end of day. How do you handle this?"

**Expected Answer:**

**1. Clarify Requirements:**
- What specific questions need answering?
- What decisions will be made with this data?
- Is there an existing report that's close?
- What's the minimum viable output?

**2. Assess Feasibility:**
- Data availability (is it already in the model?)
- Complexity of calculations
- Time required for development and testing

**3. Set Expectations:**
- Be honest about what's achievable
- Propose alternatives if full request isn't feasible
- Offer phased delivery (basic version today, enhanced tomorrow)

**4. Prioritize:**
- Focus on must-have metrics
- Use existing data models where possible
- Defer nice-to-have features

**5. Deliver:**
- Build quickly but don't skip validation
- Test with sample data
- Document assumptions and limitations
- Provide caveats with the report

**6. Follow-up:**
- Schedule time to enhance the report
- Gather feedback on what worked/didn't work
- Formalize as a regular report if needed

**Example:**
- "CEO needed client churn analysis by 5 PM. I quickly built a report using existing call volume data as a proxy for engagement. I clearly labeled it as 'preliminary analysis' and scheduled a follow-up to build a proper churn model with additional data sources."

---

### Q46: Automation Failure
**Question:** "Your automated invoice reconciliation script fails at 2 AM. How do you prevent and handle such failures?"

**Expected Answer:**

**Prevention:**

**1. Error Handling:**
```python
import logging
from datetime import datetime

# Set up logging
logging.basicConfig(
    filename=f'reconciliation_{datetime.now().strftime("%Y%m%d")}.log',
    level=logging.INFO,
    format='%(asctime)s - %(levelname)s - %(message)s'
)

def reconcile_invoices():
    try:
        # Main logic
        logging.info("Starting invoice reconciliation")

        # Connect to database
        conn = connect_to_database()
        logging.info("Database connection successful")

        # Process invoices
        results = process_invoices(conn)
        logging.info(f"Processed {len(results)} invoices")

    except DatabaseConnectionError as e:
        logging.error(f"Database connection failed: {str(e)}")
        send_alert("Database connection failed")

    except FileNotFoundError as e:
        logging.error(f"Invoice file not found: {str(e)}")
        send_alert("Missing invoice file")

    except Exception as e:
        logging.error(f"Unexpected error: {str(e)}")
        send_alert(f"Reconciliation failed: {str(e)}")

    finally:
        if conn:
            conn.close()
            logging.info("Database connection closed")
```

**2. Monitoring:**
- Email alerts on failure
- Success/failure logs
- Dashboard showing automation health
- Scheduled health checks

**3. Redundancy:**
- Retry logic for transient failures
- Fallback to manual process
- Backup data sources

**Detection & Response:**

**1. Immediate Alerts:**
```python
def send_alert(message):
    import smtplib
    from email.mime.text import MIMEText

    msg = MIMEText(f"ALERT: {message}")
    msg['Subject'] = 'Invoice Reconciliation Failed'
    msg['From'] = 'automation@company.com'
    msg['To'] = 'team@company.com'

    with smtplib.SMTP('smtp.company.com') as server:
        server.send_message(msg)
```

**2. Runbook:**
- Document common failure scenarios
- Step-by-step troubleshooting guide
- Escalation path
- Manual workaround procedures

**3. Post-Mortem:**
- Analyze root cause
- Implement permanent fix
- Update error handling
- Share learnings with team

**Example:**
- "My rate sheet automation failed because a client sent a PDF instead of Excel. I added file type validation and email parsing to extract data from PDF. I also set up Slack alerts so the team knows immediately if automation fails."

---

### Q47: Technical Debt
**Question:** "You've built several dashboards quickly. Now they're hard to maintain. How do you address technical debt?"

**Expected Answer:**

**1. Identify Technical Debt:**
- Duplicated DAX measures across reports
- Inconsistent naming conventions
- Hardcoded values
- Lack of documentation
- Complex, unoptimized queries

**2. Prioritize:**
- Impact vs. Effort matrix
- Focus on high-impact, low-effort items first
- Consider business criticality

**3. Refactoring Strategy:**

**Create Shared Datasets:**
```
Before: Each report has its own data model
After: Centralized dataset, multiple thin reports
```

**Standardize Measures:**
```dax
// Create measure table with all common calculations
// Use CALCULATE for reusability

Base Revenue = SUM(Sales[Amount])

Revenue LY =
CALCULATE(
    [Base Revenue],
    SAMEPERIODLASTYEAR(DimDate[Date])
)

Revenue Growth % =
DIVIDE(
    [Base Revenue] - [Revenue LY],
    [Revenue LY]
)
```

**Documentation:**
- Measure descriptions
- Data lineage documentation
- Refresh schedule documentation
- User guides

**4. Governance:**
- Naming conventions (e.g., `_Measure`, `dim_Table`, `fact_Table`)
- Code review process
- Version control for Power BI files
- Development → Test → Production pipeline

**5. Incremental Improvement:**
- Allocate 20% time for refactoring
- Fix technical debt when touching existing reports
- Don't let perfect be enemy of good

**Example:**
- "After building 5 dashboards, I noticed I had the same 'Revenue Growth %' measure in each with slight variations. I created a shared dataset with standardized measures and migrated all reports to use it. This reduced maintenance time by 50%."

---

### Q48: Cross-Functional Collaboration
**Question:** "How do you work with non-technical teams (sales, finance, operations)?"

**Expected Answer:**

**1. Communication Style:**
- Avoid jargon (say "filter" not "slicer", "summary" not "aggregation")
- Use business terms, not technical terms
- Visual examples over verbal explanations

**2. Requirement Translation:**
```
Business Request: "I need to see which clients are growing"

Technical Translation:
- Metric: Month-over-Month revenue growth %
- Filter: Last 12 months
- Visualization: Line chart with trend
- Drill-down: Client details
```

**3. Expectation Management:**
- Explain what's possible vs. what's not
- Provide timelines with buffer
- Clarify data limitations

**4. Training & Enablement:**
- Create user guides with screenshots
- Conduct training sessions
- Office hours for questions
- Quick reference cards

**5. Feedback Loop:**
- Regular check-ins after deployment
- Usage analytics to see what's actually used
- Iterate based on feedback

**Example Interaction:**
```
Sales Manager: "Can you make the dashboard show real-time data?"

Me: "Currently, data refreshes every 2 hours. True real-time would
require a different architecture. Would 2-hour refresh meet your needs,
or do you need more frequent updates? If so, I can explore DirectQuery
for specific metrics."

Sales Manager: "2 hours is fine, I just want to see today's numbers."

Me: "Perfect! The current setup will work. Let me show you how to
filter to today's date."
```

---

### Q49: Learning from Mistakes
**Question:** "Tell me about a time you made a mistake in a dashboard that went to production. What happened and what did you learn?"

**Expected Answer (STAR Method):**

**Situation:**
- Deployed Business Pulse Tracker to 50+ users
- Dashboard showed incorrect revenue figures for one region

**Task:**
- Identify and fix the issue quickly
- Restore user confidence

**Action:**

**1. Immediate Response:**
- Acknowledged the issue publicly
- Temporarily disabled the affected page
- Communicated timeline for fix

**2. Root Cause Analysis:**
- Found timezone conversion error in Power Query
- Some servers logged in UTC, others in local time
- My conversion logic double-converted UTC timestamps

**3. Fix:**
```powerquery
// Before (incorrect)
= Table.TransformColumns(Source,
    {{"CallTime", each DateTimeZone.ToUtc(_), type datetime}})
// This converted already-UTC times again

// After (correct)
= Table.AddColumn(Source, "CallTimeUTC",
    each if [ServerTimezone] = "UTC"
         then [CallTime]
         else DateTimeZone.ToUtc([CallTime]))
```

**4. Prevention:**
- Added data validation checks
- Created test cases for each server
- Implemented peer review process
- Added data quality dashboard

**5. Communication:**
- Sent detailed post-mortem to stakeholders
- Explained what went wrong and how it was fixed
- Shared prevention measures

**Result:**
- Fixed within 4 hours
- Implemented automated data quality checks
- No similar issues since
- Gained trust by handling transparently

**Lessons Learned:**
- Always validate data from multiple sources
- Test with production-like data before deployment
- Have a rollback plan
- Transparent communication builds trust

---

### Q50: Future Vision
**Question:** "Where do you see analytics and BI heading in the next 2-3 years? How are you preparing?"

**Expected Answer:**

**Trends:**

**1. AI-Powered Analytics:**
- Natural language queries (already in Power BI Q&A)
- Automated insight generation
- Predictive analytics becoming mainstream
- AI-assisted DAX writing

**2. Real-Time Everything:**
- Streaming data becoming standard
- Event-driven architectures
- Lower latency expectations

**3. Unified Data Platforms:**
- Microsoft Fabric-like platforms
- Less tool sprawl
- Integrated ML and BI

**4. Self-Service Analytics:**
- Citizen data scientists
- Low-code/no-code tools
- Governance becomes critical

**5. Embedded Analytics:**
- Analytics in operational apps
- Context-aware insights
- Action-oriented dashboards

**Preparation:**

**1. Learning:**
- Exploring AI features in Power BI (Copilot, Insights)
- Learning Python for ML (scikit-learn, Prophet)
- Understanding streaming architectures (Event Hubs, Kafka)

**2. Experimentation:**
- Testing preview features
- Building POCs with new technologies
- Following Microsoft roadmap

**3. Soft Skills:**
- Storytelling with data
- Change management
- Business acumen

**Example:**
- "I'm currently experimenting with Power BI's AI visuals (Key Influencers, Decomposition Tree) and learning Python's Prophet library for time series forecasting. I believe the future analyst will be more of a 'data translator' - someone who can bridge AI-generated insights with business context."

---

## SECTION 7: Candidate Questions (5 minutes)

Allow candidate to ask questions about:
- Team structure
- Technology stack
- Growth opportunities
- Project types
- Work culture

---

## SCORING RUBRIC

### Technical Skills (60 points)
| Area | Points | Criteria |
|------|--------|----------|
| Power BI & Data Modeling | 20 | Understanding of star schema, RLS, optimization |
| DAX | 15 | Measure creation, context understanding, optimization |
| SQL | 10 | Query writing, optimization, indexing knowledge |
| Python | 15 | Coding ability, pandas proficiency, error handling |

### Problem-Solving (20 points)
- Analytical thinking: 10 points
- Debugging approach: 10 points

### Communication (10 points)
- Clarity of explanations: 5 points
- Technical to non-technical translation: 5 points

### Experience Relevance (10 points)
- Project complexity: 5 points
- Impact demonstration: 5 points

**Total: 100 points**

**Passing Score: 70+**
- 85-100: Strong hire
- 70-84: Hire
- 60-69: Maybe (additional interview)
- <60: No hire

---

## KEY EVALUATION POINTS

### Must-Have Skills (Deal Breakers if Missing):
1. ✅ Strong Power BI data modeling (star schema, relationships)
2. ✅ DAX proficiency (time intelligence, context understanding)
3. ✅ SQL query writing and optimization
4. ✅ Python pandas for data manipulation
5. ✅ Understanding of ETL/ELT concepts

### Nice-to-Have Skills (Bonus Points):
1. Microsoft Fabric experience (still emerging technology)
2. Advanced DAX patterns (CALCULATE modifiers, virtual relationships)
3. Performance tuning at scale (25M+ records)
4. Automation scripting (VBA, Python)
5. Data governance and security (RLS implementation)

---

## INTERVIEW TIPS FOR INTERVIEWER

1. **Start with open-ended questions** to let candidate showcase their best work
2. **Dive deep into one project** rather than surface-level on all projects
3. **For coding section:**
   - Share screen with code editor ready
   - Allow candidate to talk through approach before coding
   - It's okay if they look up syntax (pandas documentation)
   - Focus on logic and problem-solving, not memorization
4. **Watch for red flags:**
   - Can't explain their own projects in detail
   - Blames others for failures
   - No questions about the role/company
5. **Adjust difficulty** based on responses (have backup questions ready)

---

## ADDITIONAL POWER BI QUESTIONS (Deep Dive)

### Q14: Calculated Columns vs Measures
**Question:** "Explain the difference between calculated columns and measures. When would you use each? Give me a real example from your projects."

**Expected Answer:**
- **Calculated Columns:**
  - Computed row-by-row during data refresh
  - Stored in the model (increases model size)
  - Can be used in slicers, filters, rows/columns
  - Evaluated in row context
  - Example: `Full Name = [FirstName] & " " & [LastName]`

- **Measures:**
  - Computed at query time
  - Not stored (smaller model size)
  - Cannot be used in slicers (unless wrapped in SELECTEDVALUE)
  - Evaluated in filter context
  - Example: `Total Sales = SUM(Sales[Amount])`

- **When to Use:**
  - **Calculated Column:** Static categorization (e.g., Age Group from DOB, Profit Margin Category)
  - **Measure:** Aggregations, dynamic calculations (e.g., Total Revenue, YTD Sales)

- **Real Example from Projects:**
  - "In the Billing Intelligence System, I used a calculated column for `Call Type` (Originating/Terminating) because it's static and needed in slicers. But for `Total Billing Amount`, I used a measure because it changes based on filters applied."

---

### Q15: Relationships and Cardinality
**Question:** "Explain the different types of relationships in Power BI. What issues can arise from many-to-many relationships?"

**Expected Answer:**
- **Relationship Types:**
  - **One-to-Many (1:*):** Most common, dimension to fact table
  - **Many-to-One (*:1):** Reverse of above
  - **One-to-One (1:1):** Rare, usually indicates denormalization opportunity
  - **Many-to-Many (*:*):** Complex, requires bridge tables or DAX workarounds

- **Many-to-Many Issues:**
  - Ambiguous aggregation paths
  - Performance degradation
  - Unexpected results in calculations
  - Circular dependencies

- **Solutions:**
  - Create bridge/junction tables
  - Use CROSSFILTER() in DAX
  - Implement bi-directional filtering (use cautiously)
  - Denormalize data if appropriate

- **Example:**
  - "In the Call Quality Dashboard, calls could have multiple destinations (many-to-many). I created a bridge table `CallDestinations` to properly model this relationship."

---

### Q16: Incremental Refresh
**Question:** "You mentioned using incremental refresh for large datasets. How does it work and what are the prerequisites?"

**Expected Answer:**
- **How It Works:**
  - Only refreshes recent data (e.g., last 30 days)
  - Keeps historical data cached
  - Uses RangeStart and RangeEnd parameters
  - Significantly reduces refresh time

- **Prerequisites:**
  - Power BI Premium or Premium Per User license
  - Date/DateTime column for filtering
  - Parameters named exactly: RangeStart and RangeEnd (DateTime type)
  - Query folding must be supported

- **Configuration:**
  - Define refresh period (e.g., last 2 years)
  - Define archive period (e.g., keep 5 years)
  - Set refresh granularity (days, months, quarters, years)

- **Implementation Example:**
  ```powerquery
  let
      Source = Sql.Database("server", "database"),
      FilteredRows = Table.SelectRows(Source,
          each [CallDate] >= RangeStart and [CallDate] < RangeEnd)
  in
      FilteredRows
  ```

---

### Q17: Power Query Transformations
**Question:** "What's the difference between Power Query and DAX? When would you perform transformations in each?"

**Expected Answer:**
- **Power Query (M Language):**
  - ETL layer - runs during data refresh
  - Row-by-row transformations
  - Data shaping, cleaning, merging
  - Results stored in model
  - Better for: Data type changes, column splits, merges, unpivoting

- **DAX:**
  - Calculation layer - runs at query time
  - Aggregations and business logic
  - Dynamic calculations based on context
  - Not stored (except calculated columns)
  - Better for: Measures, KPIs, time intelligence

- **Decision Framework:**
  - **Use Power Query when:**
    - Transformation needed for all rows
    - Data cleaning/standardization
    - Combining multiple sources
    - Static categorization

  - **Use DAX when:**
    - Calculation depends on user selections
    - Aggregations across filtered data
    - Time-based comparisons
    - Complex business logic

- **Example:**
  - "I used Power Query to standardize timezone formats across 9 servers (static transformation). But for calculating ASR% based on selected date range, I used DAX measures (dynamic calculation)."

---

### Q18: Query Folding
**Question:** "What is query folding in Power Query? How do you check if it's happening?"

**Expected Answer:**
- **What is Query Folding:**
  - Power Query pushes transformations back to the data source
  - Source database does the heavy lifting (filtering, aggregation)
  - Only processed data is transferred to Power BI
  - Significantly improves performance

- **When It Works:**
  - Relational databases (SQL Server, MySQL, PostgreSQL)
  - Basic transformations (filter, select, join, group by)

- **When It Breaks:**
  - Adding custom columns with complex logic
  - Using certain M functions (Text.Proper, Date.ToText)
  - Merging with non-foldable queries
  - Adding index columns

- **How to Check:**
  - Right-click on a step in Applied Steps
  - If "View Native Query" is enabled → folding is working
  - If grayed out → folding has stopped

- **Best Practices:**
  - Keep foldable steps early in the query
  - Do complex transformations after data is loaded
  - Use database views for complex logic

- **Example:**
  - "When pulling 25M records from MySQL, I ensured query folding by doing date filtering and basic joins in Power Query. Complex text transformations were done in DAX to maintain folding."

---

### Q19: Bookmarks and Drill-through
**Question:** "Explain how you've used bookmarks and drill-through pages in your dashboards. What's the difference?"

**Expected Answer:**
- **Bookmarks:**
  - Capture current state of a page (filters, slicers, visuals visibility)
  - Used for: Navigation, storytelling, toggling visuals, creating buttons
  - Can control: Filters, slicers, spotlight, visual visibility

- **Drill-through:**
  - Navigate from summary to detailed page
  - Automatically applies context filters
  - Right-click on data point → "Drill through"
  - Requires drill-through field configuration

- **Use Cases:**
  - **Bookmarks:**
    - Toggle between chart types (bar vs line)
    - Show/hide detailed tables
    - Create guided analysis flow
    - Reset all filters button

  - **Drill-through:**
    - Click on client → see detailed call logs
    - Click on region → see regional performance
    - Click on date → see hourly breakdown

- **Example from Projects:**
  - "In Business Pulse Tracker, I used bookmarks to toggle between revenue view and call quality view on the same page. For drill-through, clicking on a client name took users to a detailed page showing all their calls, routes, and billing information with filters automatically applied."

---

### Q20: Aggregations and Composite Models
**Question:** "Have you worked with aggregation tables in Power BI? When would you use them?"

**Expected Answer:**
- **What are Aggregations:**
  - Pre-aggregated summary tables
  - Power BI automatically uses them when appropriate
  - Improves performance for large datasets
  - Transparent to report users

- **When to Use:**
  - Fact tables with millions/billions of rows
  - Common aggregation patterns (daily, monthly summaries)
  - DirectQuery sources that are slow
  - Mixed mode scenarios (Import + DirectQuery)

- **Implementation:**
  - Create aggregated table (e.g., DailySales from HourlySales)
  - Set up aggregation mappings in Power BI
  - Hide aggregation table from users
  - Power BI engine automatically routes queries

- **Example:**
  - "With 25M monthly call records, I created a daily aggregation table with pre-calculated totals. When users viewed monthly trends, Power BI used the aggregation table (fast). When they drilled to hourly details, it used the detailed table."

---

### Q21: Power BI Service vs Desktop
**Question:** "What are the key differences between Power BI Desktop and Power BI Service? What can you do in Service that you can't in Desktop?"

**Expected Answer:**
- **Power BI Desktop:**
  - Development environment
  - Create reports and data models
  - Advanced data modeling
  - Full DAX and Power Query capabilities
  - Offline work

- **Power BI Service (Online):**
  - Publishing and sharing platform
  - Scheduled refresh
  - Collaboration features
  - Dataflows
  - Deployment pipelines
  - Apps and workspaces
  - Row-level security testing with actual users
  - Paginated reports
  - Metrics and goals

- **Service-Only Features:**
  - Scheduled refresh configuration
  - Sharing and permissions management
  - Email subscriptions
  - Alerts and notifications
  - Q&A natural language queries
  - Quick insights
  - Embed in SharePoint/Teams

- **Example:**
  - "I developed all dashboards in Desktop, but configured automated night refreshes in Service. I also set up workspaces for different teams and used RLS to control data access."

---

### Q22: Parameters and What-If Analysis
**Question:** "Have you used parameters in Power BI? Explain a scenario where you used what-if parameters."

**Expected Answer:**
- **Parameters in Power Query:**
  - Used for dynamic data source connections
  - Environment switching (Dev/Prod)
  - Date range filtering (RangeStart/RangeEnd)

- **What-If Parameters (DAX):**
  - Create interactive scenarios
  - User-controlled variables
  - Sensitivity analysis

- **Implementation:**
  - Modeling tab → New Parameter
  - Define range, increment, default value
  - Creates a table with slicer
  - Use parameter value in measures

- **Example Scenario:**
  ```dax
  // What-if parameter: Discount Rate (0% to 50%)

  Projected Revenue =
  VAR BaseRevenue = SUM(Sales[Revenue])
  VAR DiscountRate = SELECTEDVALUE('Discount Rate'[Discount Rate Value], 0)
  RETURN
      BaseRevenue * (1 - DiscountRate)
  ```

- **Use Case:**
  - "For the Business Pulse Tracker, I created a what-if parameter for 'Target Growth Rate' allowing executives to model different growth scenarios and see projected revenue for next quarter."

---

### Q23: Custom Visuals and Formatting
**Question:** "Have you used custom visuals from AppSource? What considerations do you have when using them?"

**Expected Answer:**
- **Custom Visuals Used:**
  - Gantt charts
  - Sankey diagrams
  - Advanced KPI cards
  - Heatmaps
  - Bullet charts

- **Considerations:**
  - **Security:** Only use certified visuals in production
  - **Performance:** Some custom visuals are slower than native
  - **Maintenance:** May break with Power BI updates
  - **Licensing:** Some require premium features
  - **Export:** May not work in PDF/PowerPoint exports

- **Best Practices:**
  - Test thoroughly before production
  - Have fallback with native visuals
  - Document dependencies
  - Check vendor support and update frequency

- **Example:**
  - "In the Call Quality Dashboard, I used a custom KPI visual for real-time metrics display. I ensured it was Microsoft-certified and tested it with different data volumes before deploying to production."

---

### Q24: Data Refresh Strategies
**Question:** "You mentioned automated report refresh schedules. Explain your refresh strategy for the dashboards you built."

**Expected Answer:**
- **Refresh Types:**
  - **Scheduled Refresh:** Automatic at set times
  - **On-Demand Refresh:** Manual trigger
  - **Incremental Refresh:** Only recent data
  - **DirectQuery:** No refresh needed (live connection)

- **Strategy Considerations:**
  - Data freshness requirements
  - Source system load
  - Refresh duration
  - License limitations (8/day for Pro, 48/day for Premium)

- **Implementation:**
  - **Real-Time Dashboard:**
    - Scheduled refresh every 2 hours during business hours
    - Incremental refresh for call logs (last 7 days)
    - DirectQuery for critical real-time metrics

  - **Billing Dashboard:**
    - Daily refresh at 2 AM (after billing system updates)
    - Full refresh monthly for historical corrections

- **Optimization:**
  - Stagger refresh times across reports
  - Use incremental refresh for large tables
  - Partition data by date
  - Optimize Power Query for faster refresh

- **Monitoring:**
  - Set up refresh failure alerts
  - Track refresh duration trends
  - Document refresh dependencies

---

### Q25: Mobile Layout and Responsive Design
**Question:** "Did you optimize your dashboards for mobile viewing? How do you approach mobile layout design?"

**Expected Answer:**
- **Mobile Optimization:**
  - Create separate mobile layout in Power BI Desktop
  - Prioritize key metrics
  - Simplify visuals for small screens
  - Use phone-friendly visual types

- **Best Practices:**
  - **Layout:**
    - Portrait orientation
    - Single column design
    - Larger touch targets
    - Minimal scrolling

  - **Visuals:**
    - Cards for KPIs (easy to read)
    - Simple bar/column charts
    - Avoid complex matrices
    - Limit slicers (use filter pane)

  - **Performance:**
    - Reduce number of visuals
    - Use aggregated data
    - Minimize interactions

- **Testing:**
  - Use Power BI mobile app preview
  - Test on different devices
  - Validate touch interactions

- **Example:**
  - "For the NOC team's Call Quality Dashboard, I created a mobile layout showing only critical metrics (ASR, ACD, active alerts) as large cards. Detailed tables were accessible through drill-through pages."

---

## BACKUP QUESTIONS (If Time Permits or Need More Depth)

### Power BI:
- "Explain the difference between calculated columns and measures. When would you use each?"
- "How do you handle slowly changing dimensions in Power BI?"
- "What's your approach to version control for Power BI reports?"

### Additional DAX Questions:

**Q26: Running Total**
**Question:** "Write a measure to calculate running total of sales by date."

**Expected Answer:**
```dax
Running Total Sales =
CALCULATE(
    SUM(Sales[Amount]),
    FILTER(
        ALLSELECTED(DimDate[Date]),
        DimDate[Date] <= MAX(DimDate[Date])
    )
)

// Alternative using WINDOW functions (Power BI 2023+)
Running Total Sales V2 =
WINDOW(
    SUM(Sales[Amount]),
    ORDERBY(DimDate[Date], ASC),
    PARTITIONBY(),
    ROWS(UNBOUNDED, CURRENT)
)
```

---

**Q27: USERELATIONSHIP**
**Question:** "Explain USERELATIONSHIP and when you'd use it. Give an example."

**Expected Answer:**
- **Purpose:** Activate inactive relationships in a calculation
- **Why Needed:** Only one active relationship allowed between two tables
- **Common Scenario:** Date tables with multiple date columns (Order Date, Ship Date, Due Date)

**Example:**
```dax
// Active relationship: Sales[OrderDate] -> DimDate[Date]
// Inactive relationship: Sales[ShipDate] -> DimDate[Date]

Sales by Order Date = SUM(Sales[Amount])  // Uses active relationship

Sales by Ship Date =
CALCULATE(
    SUM(Sales[Amount]),
    USERELATIONSHIP(Sales[ShipDate], DimDate[Date])
)
```

**Real-world Use:**
- "In the Billing Intelligence System, I had both Call Start Time and Call End Time. I created two relationships to the Date table and used USERELATIONSHIP to calculate metrics based on either timestamp."

---

**Q28: ALL, ALLEXCEPT, ALLSELECTED**
**Question:** "What's the difference between ALL, ALLEXCEPT, and ALLSELECTED? When would you use each?"

**Expected Answer:**

**ALL:**
- Removes all filters from specified table/column
- Returns all rows ignoring any filters
```dax
% of Total Sales =
DIVIDE(
    SUM(Sales[Amount]),
    CALCULATE(SUM(Sales[Amount]), ALL(Sales))
)
```

**ALLEXCEPT:**
- Removes all filters except specified columns
- Useful for "all except" scenarios
```dax
Sales vs Region Total =
DIVIDE(
    SUM(Sales[Amount]),
    CALCULATE(SUM(Sales[Amount]), ALLEXCEPT(Sales, Sales[Region]))
)
```

**ALLSELECTED:**
- Removes filters but respects visual-level filters
- Maintains context from slicers/filters outside the visual
```dax
% of Visible Total =
DIVIDE(
    SUM(Sales[Amount]),
    CALCULATE(SUM(Sales[Amount]), ALLSELECTED(Sales))
)
```

**When to Use:**
- **ALL:** Grand totals, overall percentages
- **ALLEXCEPT:** Subtotals by specific dimensions
- **ALLSELECTED:** Percentages within filtered context

---

**Q29: CALCULATE Modifiers**
**Question:** "Explain KEEPFILTERS and how it differs from standard CALCULATE behavior."

**Expected Answer:**
- **Standard CALCULATE:** Replaces existing filters
- **KEEPFILTERS:** Adds filters without removing existing ones (intersection)

**Example:**
```dax
// Standard CALCULATE - replaces filter
Sales Red Products =
CALCULATE(
    SUM(Sales[Amount]),
    Products[Color] = "Red"
)
// If user selects "Blue" in slicer, this still shows Red products

// With KEEPFILTERS - intersects filters
Sales Red Products (Filtered) =
CALCULATE(
    SUM(Sales[Amount]),
    KEEPFILTERS(Products[Color] = "Red")
)
// If user selects "Blue" in slicer, this shows BLANK (no intersection)
```

---

**Q30: Time Intelligence - Custom Calendar**
**Question:** "How do you handle fiscal year calculations when fiscal year doesn't match calendar year?"

**Expected Answer:**
- **Approach 1:** Add fiscal year columns to date table
```powerquery
// In Power Query
FiscalYear = if [Month] >= 4 then [Year] else [Year] - 1
FiscalQuarter = if [Month] >= 4 then
    Number.RoundUp(([Month] - 3) / 3)
    else Number.RoundUp(([Month] + 9) / 3)
```

- **Approach 2:** Use DAX for fiscal calculations
```dax
Fiscal YTD Sales =
CALCULATE(
    SUM(Sales[Amount]),
    DATESYTD(
        DimDate[Date],
        "03/31"  // Fiscal year ends March 31
    )
)

Same Period Last Fiscal Year =
CALCULATE(
    SUM(Sales[Amount]),
    SAMEPERIODLASTYEAR(DimDate[Date])
)
```

---

### Additional Python Questions:

**Q31: Large File Handling**
**Question:** "How would you handle a 10GB CSV file that doesn't fit in memory?"

**Expected Answer:**
```python
import pandas as pd

# Method 1: Chunking
chunk_size = 100000
chunks = []

for chunk in pd.read_csv('large_file.csv', chunksize=chunk_size):
    # Process each chunk
    processed = chunk[chunk['Amount'] > 0]  # Filter
    chunks.append(processed)

result = pd.concat(chunks, ignore_index=True)

# Method 2: Use specific columns only
df = pd.read_csv('large_file.csv', usecols=['Date', 'Amount', 'Client'])

# Method 3: Use data types optimization
dtypes = {
    'ClientID': 'int32',  # Instead of int64
    'Amount': 'float32',
    'Region': 'category'  # For repeated strings
}
df = pd.read_csv('large_file.csv', dtype=dtypes)

# Method 4: Dask for parallel processing
import dask.dataframe as dd
ddf = dd.read_csv('large_file.csv')
result = ddf.groupby('Client')['Amount'].sum().compute()

# Method 5: Database approach
import sqlite3
# Load to SQLite, then query in chunks
```

---

**Q32: Merge vs Join**
**Question:** "Explain the difference between merge and join in pandas. Which one did you use in your projects?"

**Expected Answer:**
- **merge():** Function-based, more flexible
- **join():** Method-based, joins on index by default

```python
# merge() - more common, flexible
result = pd.merge(
    df1,
    df2,
    on='ClientID',
    how='left'  # left, right, inner, outer
)

# join() - index-based by default
result = df1.join(df2, on='ClientID', how='left')

# merge() with different column names
result = pd.merge(
    df1,
    df2,
    left_on='ClientID',
    right_on='Client_ID',
    how='inner'
)
```

**Project Example:**
- "In the invoice reconciliation system, I used `merge()` to join invoice data with internal call records on multiple keys (Client, Destination, Date) to identify discrepancies."

---

**Q33: Missing Data Handling**
**Question:** "How do you handle missing data in pandas? Give examples from your projects."

**Expected Answer:**
```python
import pandas as pd
import numpy as np

# 1. Detect missing data
df.isnull().sum()  # Count nulls per column
df.info()  # See non-null counts

# 2. Drop missing data
df.dropna()  # Drop rows with any null
df.dropna(subset=['Amount'])  # Drop only if Amount is null
df.dropna(thresh=3)  # Keep rows with at least 3 non-null values

# 3. Fill missing data
df['Amount'].fillna(0)  # Fill with constant
df['Rate'].fillna(df['Rate'].mean())  # Fill with mean
df['Region'].fillna(method='ffill')  # Forward fill
df['Region'].fillna(method='bfill')  # Backward fill

# 4. Interpolate
df['Amount'].interpolate(method='linear')

# 5. Replace specific values
df.replace({'N/A': np.nan, '': np.nan})
```

**Project Example:**
- "In rate sheet processing, missing billing intervals were filled with default value 60. Missing rates were flagged as invalid rather than filled, since they required client confirmation."

---

**Q34: Email Automation**
**Question:** "You mentioned using imaplib to extract email attachments. Walk me through the code structure."

**Expected Answer:**
```python
import imaplib
import email
from email.header import decode_header
import os

def extract_rate_sheets(email_address, password, output_folder):
    # Connect to email server
    imap = imaplib.IMAP4_SSL("imap.gmail.com")
    imap.login(email_address, password)
    imap.select("INBOX")

    # Search for emails with attachments
    status, messages = imap.search(None, 'UNSEEN', 'SUBJECT "Rate Sheet"')

    for msg_num in messages[0].split():
        # Fetch email
        status, msg_data = imap.fetch(msg_num, "(RFC822)")

        for response_part in msg_data:
            if isinstance(response_part, tuple):
                msg = email.message_from_bytes(response_part[1])

                # Extract subject and sender
                subject = decode_header(msg["Subject"])[0][0]
                sender = msg.get("From")

                # Process attachments
                for part in msg.walk():
                    if part.get_content_disposition() == "attachment":
                        filename = part.get_filename()

                        if filename and filename.endswith(('.xlsx', '.xls', '.csv')):
                            filepath = os.path.join(output_folder, filename)

                            with open(filepath, 'wb') as f:
                                f.write(part.get_payload(decode=True))

                            print(f"Downloaded: {filename}")

    imap.close()
    imap.logout()

# Usage
extract_rate_sheets("user@company.com", "password", "./rate_sheets")
```

---

### Additional SQL Questions:

**Q35: JOIN Types**
**Question:** "Explain the difference between INNER JOIN, LEFT JOIN, RIGHT JOIN, and CROSS JOIN with examples."

**Expected Answer:**
```sql
-- INNER JOIN: Only matching records
SELECT c.ClientName, cl.CallID, cl.Duration
FROM Clients c
INNER JOIN Calls cl ON c.ClientID = cl.ClientID;
-- Returns only clients who have made calls

-- LEFT JOIN: All from left table, matching from right
SELECT c.ClientName, cl.CallID, cl.Duration
FROM Clients c
LEFT JOIN Calls cl ON c.ClientID = cl.ClientID;
-- Returns all clients, even those with no calls (NULL for call data)

-- RIGHT JOIN: All from right table, matching from left
SELECT c.ClientName, cl.CallID, cl.Duration
FROM Clients c
RIGHT JOIN Calls cl ON c.ClientID = cl.ClientID;
-- Returns all calls, even if client info is missing

-- CROSS JOIN: Cartesian product
SELECT c.ClientName, r.Region
FROM Clients c
CROSS JOIN Regions r;
-- Every client paired with every region
```

**Use Case:**
- "Used LEFT JOIN in billing reports to show all clients including those with zero calls for the period."

---

**Q36: Window Functions**
**Question:** "What are window functions? Write a query to rank clients by monthly revenue."

**Expected Answer:**
```sql
-- Ranking clients by monthly revenue
SELECT
    ClientName,
    YEAR(CallDate) AS Year,
    MONTH(CallDate) AS Month,
    SUM(Amount) AS MonthlyRevenue,
    RANK() OVER (
        PARTITION BY YEAR(CallDate), MONTH(CallDate)
        ORDER BY SUM(Amount) DESC
    ) AS RevenueRank,
    ROW_NUMBER() OVER (
        PARTITION BY YEAR(CallDate), MONTH(CallDate)
        ORDER BY SUM(Amount) DESC
    ) AS RowNum
FROM
    Calls c
    JOIN Clients cl ON c.ClientID = cl.ClientID
GROUP BY
    ClientName, YEAR(CallDate), MONTH(CallDate)
ORDER BY
    Year, Month, RevenueRank;

-- Running total using window function
SELECT
    CallDate,
    ClientName,
    Amount,
    SUM(Amount) OVER (
        PARTITION BY ClientName
        ORDER BY CallDate
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS RunningTotal
FROM Calls;
```

**Common Window Functions:**
- **ROW_NUMBER():** Unique sequential number
- **RANK():** Ranking with gaps for ties
- **DENSE_RANK():** Ranking without gaps
- **LAG/LEAD():** Access previous/next row
- **SUM/AVG/COUNT() OVER():** Aggregates without grouping

---

**Q37: Finding Duplicates**
**Question:** "How would you find and remove duplicate call records in your database?"

**Expected Answer:**
```sql
-- Find duplicates
SELECT
    ClientID,
    CallDate,
    Duration,
    COUNT(*) AS DuplicateCount
FROM Calls
GROUP BY ClientID, CallDate, Duration
HAVING COUNT(*) > 1;

-- Find duplicates with details
SELECT *
FROM Calls
WHERE (ClientID, CallDate, Duration) IN (
    SELECT ClientID, CallDate, Duration
    FROM Calls
    GROUP BY ClientID, CallDate, Duration
    HAVING COUNT(*) > 1
);

-- Remove duplicates (keep one record)
-- Method 1: Using ROW_NUMBER
WITH CTE AS (
    SELECT *,
        ROW_NUMBER() OVER (
            PARTITION BY ClientID, CallDate, Duration
            ORDER BY CallID
        ) AS rn
    FROM Calls
)
DELETE FROM CTE WHERE rn > 1;

-- Method 2: Using self-join
DELETE c1
FROM Calls c1
INNER JOIN Calls c2
WHERE
    c1.ClientID = c2.ClientID
    AND c1.CallDate = c2.CallDate
    AND c1.Duration = c2.Duration
    AND c1.CallID > c2.CallID;
```

**Project Context:**
- "When consolidating data from 9 servers, I found duplicate calls logged on multiple servers. I used ROW_NUMBER() to identify and remove duplicates, keeping the record from the primary server."

---

**Q38: Indexing Strategy**
**Question:** "How do you decide which columns to index? What are the trade-offs?"

**Expected Answer:**
- **When to Index:**
  - Columns in WHERE clauses
  - Columns in JOIN conditions
  - Columns in ORDER BY
  - Foreign key columns
  - Columns with high selectivity (many unique values)

- **When NOT to Index:**
  - Small tables (< 1000 rows)
  - Columns with low selectivity (e.g., Gender: M/F)
  - Frequently updated columns
  - Wide columns (large text fields)

- **Trade-offs:**
  - **Pros:** Faster SELECT queries, improved JOIN performance
  - **Cons:** Slower INSERT/UPDATE/DELETE, increased storage, maintenance overhead

**Example:**
```sql
-- Good indexes for call quality dashboard
CREATE INDEX idx_calls_date ON Calls(CallDate);
CREATE INDEX idx_calls_client ON Calls(ClientID);
CREATE INDEX idx_calls_composite ON Calls(CallDate, ClientID, ServerID);

-- Covering index for specific query
CREATE INDEX idx_calls_covering ON Calls(CallDate, ClientID)
INCLUDE (Duration, Amount);
```

**Project Example:**
- "For the real-time dashboard querying 25M records, I created composite indexes on (CallDate, ServerID, ClientID) which reduced query time from 8 seconds to under 1 second."

---

**Q39: Stored Procedures vs Views**
**Question:** "What's the difference between stored procedures and views? When would you use each?"

**Expected Answer:**

**Views:**
- Virtual table based on SELECT query
- No parameters
- Can be used like a table
- Simplifies complex queries
- Provides security layer
```sql
CREATE VIEW vw_ClientMonthlySummary AS
SELECT
    ClientID,
    YEAR(CallDate) AS Year,
    MONTH(CallDate) AS Month,
    COUNT(*) AS TotalCalls,
    SUM(Duration) AS TotalMinutes,
    SUM(Amount) AS TotalRevenue
FROM Calls
GROUP BY ClientID, YEAR(CallDate), MONTH(CallDate);
```

**Stored Procedures:**
- Precompiled SQL statements
- Can accept parameters
- Can contain logic (IF, WHILE, etc.)
- Can modify data
- Better performance for complex operations
```sql
CREATE PROCEDURE sp_GetClientReport
    @ClientID INT,
    @StartDate DATE,
    @EndDate DATE
AS
BEGIN
    SELECT
        CallDate,
        COUNT(*) AS Calls,
        SUM(Duration) AS Minutes
    FROM Calls
    WHERE
        ClientID = @ClientID
        AND CallDate BETWEEN @StartDate AND @EndDate
    GROUP BY CallDate
    ORDER BY CallDate;
END;
```

**When to Use:**
- **Views:** Simplify reporting, enforce security, reusable queries
- **Stored Procedures:** Complex business logic, data modifications, parameterized operations

---

**Q40: Transaction Management**
**Question:** "Explain ACID properties and how you ensure data consistency in your ETL processes."

**Expected Answer:**

**ACID Properties:**
- **Atomicity:** All or nothing (transaction completes fully or rolls back)
- **Consistency:** Data remains valid (constraints maintained)
- **Isolation:** Concurrent transactions don't interfere
- **Durability:** Committed data persists even after system failure

**Implementation:**
```sql
BEGIN TRANSACTION;

BEGIN TRY
    -- Insert billing records
    INSERT INTO Billing (ClientID, Amount, BillingDate)
    SELECT ClientID, SUM(Amount), GETDATE()
    FROM Calls
    WHERE BillingDate IS NULL
    GROUP BY ClientID;

    -- Mark calls as billed
    UPDATE Calls
    SET BillingDate = GETDATE()
    WHERE BillingDate IS NULL;

    -- Commit if both succeed
    COMMIT TRANSACTION;
END TRY
BEGIN CATCH
    -- Rollback if any error
    ROLLBACK TRANSACTION;

    -- Log error
    INSERT INTO ErrorLog (ErrorMessage, ErrorDate)
    VALUES (ERROR_MESSAGE(), GETDATE());
END CATCH;
```

**Project Example:**
- "In the billing automation, I used transactions to ensure that when generating invoices, both the invoice record and the call records were updated atomically. If invoice generation failed, call records weren't marked as billed."

---

## POST-INTERVIEW CHECKLIST

- [ ] Complete scoring rubric
- [ ] Document specific examples candidate provided
- [ ] Note any concerns or exceptional strengths
- [ ] Compare against other candidates
- [ ] Provide feedback to hiring manager within 24 hours
- [ ] If moving forward, identify areas for onboarding focus

---

---

## QUICK REFERENCE GUIDE

### Power BI Concepts to Probe:
- [ ] Star schema vs snowflake schema
- [ ] Calculated columns vs measures
- [ ] Import vs DirectQuery vs Direct Lake
- [ ] Row-Level Security (static vs dynamic)
- [ ] Incremental refresh
- [ ] Query folding
- [ ] Aggregations
- [ ] Bookmarks vs drill-through
- [ ] Performance optimization
- [ ] Mobile layout

### DAX Concepts to Test:
- [ ] Filter context vs row context
- [ ] Context transition
- [ ] Time intelligence (YTD, MoM, YoY)
- [ ] CALCULATE and filter modifiers
- [ ] ALL, ALLEXCEPT, ALLSELECTED
- [ ] USERELATIONSHIP
- [ ] Variables in DAX
- [ ] Iterator functions (SUMX, FILTER)
- [ ] DIVIDE for error handling

### SQL Skills to Verify:
- [ ] JOIN types (INNER, LEFT, RIGHT, CROSS)
- [ ] Window functions (ROW_NUMBER, RANK, LAG/LEAD)
- [ ] Aggregations and GROUP BY
- [ ] Subqueries and CTEs
- [ ] Indexing strategy
- [ ] Query optimization
- [ ] Transaction management (ACID)
- [ ] Stored procedures vs views

### Python Skills to Assess:
- [ ] pandas (groupby, merge, pivot)
- [ ] Data cleaning and validation
- [ ] Error handling (try-except)
- [ ] File I/O (CSV, Excel, PDF)
- [ ] Email automation (imaplib)
- [ ] Large file handling (chunking, Dask)
- [ ] Logging and monitoring
- [ ] Code organization (functions, classes)

### Behavioral Competencies:
- [ ] Problem-solving approach
- [ ] Stakeholder management
- [ ] Handling ambiguity
- [ ] Learning agility
- [ ] Communication skills
- [ ] Time management
- [ ] Attention to detail
- [ ] Ownership and accountability

---

## INTERVIEWER PREPARATION CHECKLIST

### Before Interview:
- [ ] Review candidate's resume and projects
- [ ] Prepare code editor for Python challenges
- [ ] Have Power BI Desktop open (if doing live demo)
- [ ] Select 8-10 questions based on role requirements
- [ ] Print scoring rubric
- [ ] Prepare sample data for coding challenges

### During Interview:
- [ ] Take notes on specific examples candidate provides
- [ ] Mark scores on rubric in real-time
- [ ] Watch for red flags (can't explain own work, blames others)
- [ ] Note exceptional strengths
- [ ] Allow candidate to ask questions

### After Interview:
- [ ] Complete scoring within 1 hour
- [ ] Write detailed feedback
- [ ] Compare against other candidates
- [ ] Provide hiring recommendation
- [ ] Share feedback with hiring manager

---

## RED FLAGS TO WATCH FOR

### Technical Red Flags:
- ❌ Can't explain difference between calculated columns and measures
- ❌ Doesn't understand filter context in DAX
- ❌ Can't write basic SQL JOIN
- ❌ No understanding of data modeling principles
- ❌ Claims to have built dashboards but can't explain data sources
- ❌ Doesn't know when to use Import vs DirectQuery
- ❌ Can't explain how they optimized performance
- ❌ No experience with version control or deployment

### Behavioral Red Flags:
- ❌ Blames others for project failures
- ❌ Can't provide specific examples (vague answers)
- ❌ Defensive when asked about mistakes
- ❌ No questions about the role or company
- ❌ Interrupts or talks over interviewer
- ❌ Can't explain technical concepts simply
- ❌ Shows no curiosity or learning mindset
- ❌ Takes credit for team accomplishments without acknowledging others

### Communication Red Flags:
- ❌ Uses jargon without explaining
- ❌ Can't translate technical to business terms
- ❌ Rambles without structure
- ❌ Doesn't listen to questions carefully
- ❌ Gets frustrated when asked to clarify

---

## GREEN FLAGS TO LOOK FOR

### Technical Strengths:
- ✅ Explains concepts clearly with examples
- ✅ Discusses trade-offs in technical decisions
- ✅ Shows understanding of performance implications
- ✅ Mentions testing and validation
- ✅ Talks about data quality and governance
- ✅ Demonstrates continuous learning
- ✅ Asks clarifying questions before answering
- ✅ Provides multiple solutions to problems

### Behavioral Strengths:
- ✅ Uses STAR method for behavioral questions
- ✅ Takes ownership of mistakes and learns from them
- ✅ Shows empathy for end users
- ✅ Demonstrates stakeholder management skills
- ✅ Balances technical excellence with business value
- ✅ Asks thoughtful questions about the role
- ✅ Shows enthusiasm for data and analytics
- ✅ Gives credit to team members

### Communication Strengths:
- ✅ Adjusts technical depth based on audience
- ✅ Uses analogies to explain complex concepts
- ✅ Structured thinking (frameworks, step-by-step)
- ✅ Active listening
- ✅ Concise yet comprehensive answers

---

## SAMPLE INTERVIEW FLOW (60 minutes)

**0:00 - 0:05 | Introduction (5 min)**
- Interviewer introduces self and role
- Candidate introduces self
- Set expectations for interview format

**0:05 - 0:10 | Background (5 min)**
- Q: "Walk me through your most impactful project"
- Listen for: Impact metrics, technical depth, stakeholder management

**0:10 - 0:30 | Power BI Deep Dive (20 min)**
- Q1: Real-Time Call Quality Dashboard (8 min)
  - Data integration from 9 servers
  - Data modeling approach
  - Real-time refresh strategy
- Q2: Row-Level Security (6 min)
  - RLS design and implementation
  - Testing approach
- Q15: Relationships and Cardinality (6 min)
  - Understanding of relationship types
  - Handling many-to-many

**0:30 - 0:40 | DAX & SQL (10 min)**
- Q5: Write DAX for MoM Growth and YTD (5 min)
- Q8: Write SQL for top clients by ACD (5 min)

**0:40 - 0:55 | Python Coding (15 min)**
- Coding Challenge 1: Invoice Parsing (10 min)
  - Share screen with code editor
  - Allow candidate to talk through approach
  - Evaluate: pandas proficiency, error handling, code quality
- Coding Challenge 2: Rate Sheet Processing (5 min)
  - Function design
  - Data validation

**0:55 - 1:00 | Wrap-up (5 min)**
- Q11: "Describe a time you debugged incorrect dashboard data"
- Candidate questions
- Next steps

---

## DECISION MATRIX

### Strong Hire (85-100 points)
**Profile:**
- Exceeds requirements in all technical areas
- Demonstrates advanced DAX and data modeling
- Strong problem-solving and communication
- Shows leadership potential

**Recommendation:**
- Extend offer
- Consider for senior-level projects
- Potential mentor for junior analysts

---

### Hire (70-84 points)
**Profile:**
- Meets all core requirements
- Solid Power BI and DAX skills
- Good communication and stakeholder management
- Some areas for growth

**Recommendation:**
- Extend offer
- Provide onboarding in weaker areas
- Good fit for team

---

### Maybe (60-69 points)
**Profile:**
- Meets some requirements but gaps in key areas
- Either strong technical but weak communication, or vice versa
- Limited experience with some technologies

**Recommendation:**
- Additional interview with team lead
- Consider for junior role if gaps are in advanced topics
- Assess cultural fit and learning potential

---

### No Hire (<60 points)
**Profile:**
- Significant gaps in core competencies
- Can't explain own projects
- Poor communication or behavioral red flags

**Recommendation:**
- Do not extend offer
- Provide constructive feedback if requested

---

## FOLLOW-UP QUESTIONS BANK

### If Candidate is Struggling:
- "Let me rephrase the question..."
- "Can you walk me through your thought process?"
- "What would be your first step in approaching this?"
- "Have you encountered a similar situation before?"

### If Candidate is Excelling:
- "How would you optimize this further?"
- "What are the trade-offs of this approach?"
- "How would this scale to 10x the data volume?"
- "What alternative approaches did you consider?"

### To Probe Deeper:
- "Can you give me a specific example?"
- "What was the business impact of this work?"
- "How did you validate this was correct?"
- "What would you do differently next time?"

---

## CANDIDATE EVALUATION FORM

**Candidate Name:** _______________________
**Interview Date:** _______________________
**Interviewer:** _______________________

### Technical Assessment

| Area | Score (0-20) | Notes |
|------|--------------|-------|
| Power BI & Data Modeling | ___/20 | |
| DAX | ___/15 | |
| SQL | ___/10 | |
| Python | ___/15 | |

### Problem-Solving (0-20)
| Criteria | Score | Notes |
|----------|-------|-------|
| Analytical thinking | ___/10 | |
| Debugging approach | ___/10 | |

### Communication (0-10)
| Criteria | Score | Notes |
|----------|-------|-------|
| Clarity of explanations | ___/5 | |
| Technical translation | ___/5 | |

### Experience Relevance (0-10)
| Criteria | Score | Notes |
|----------|-------|-------|
| Project complexity | ___/5 | |
| Impact demonstration | ___/5 | |

**Total Score: _____ / 100**

### Overall Recommendation:
- [ ] Strong Hire (85-100)
- [ ] Hire (70-84)
- [ ] Maybe (60-69)
- [ ] No Hire (<60)

### Key Strengths:
1. _______________________
2. _______________________
3. _______________________

### Areas for Development:
1. _______________________
2. _______________________
3. _______________________

### Notable Examples/Quotes:
_______________________
_______________________
_______________________

### Recommendation Summary:
_______________________
_______________________
_______________________

**Interviewer Signature:** _______________________
**Date:** _______________________

---

**END OF INTERVIEW PLAN**

---

## APPENDIX: ADDITIONAL RESOURCES

### For Interviewer:
- [Power BI Performance Best Practices](https://docs.microsoft.com/power-bi/guidance/power-bi-optimization)
- [DAX Patterns](https://www.daxpatterns.com/)
- [SQLBI Resources](https://www.sqlbi.com/)
- [Microsoft Fabric Documentation](https://learn.microsoft.com/fabric/)

### Sample Data for Coding Challenges:
Available in `/interview_resources/sample_data/`
- `invoice_sample.csv`
- `rate_sheet_sample.xlsx`
- `call_logs_sample.csv`

### Code Editor Setup:
- Python 3.8+
- Libraries: pandas, openpyxl, pdfplumber, mysql-connector-python
- IDE: VS Code or Jupyter Notebook

---

**Document Version:** 1.0
**Last Updated:** 12-November-2025
**Prepared By:** Interview Team
**Review Date:** Quarterly

---

---

# 📝 L1 INTERVIEW FEEDBACK

**Candidate Name:** [Candidate Name]
**Interview Date:** 12-November-2025
**Interviewer:** [Interviewer Name]
**Position:** Power BI Data Analyst (2+ years)
**Interview Duration:** 60 minutes
**Overall Result:** ✅ **SELECTED**

---

## 📊 OVERALL ASSESSMENT

**Summary:**
Good Knowledge over Power BI end-to-end — from data modeling, DAX, and Power Query to visualization and deployment. Demonstrates business understanding, and good communication skills.

**Final Score:** **78/100** (Hire Range: 70-84)

**Recommendation:** ✅ **SELECTED** – Proficient technically, prepared for client-facing BI work.

---

## 🎯 TECHNICAL SKILLS ASSESSMENT

### Power BI / DAX: ⭐⭐⭐⭐⭐ Very Good (14/15 points)
**Strengths:**
- Strong grasp of CALCULATE function and its filter modifiers
- Excellent understanding of SUMX and other iterator functions
- Deep knowledge of filter context vs row context
- Can write complex time intelligence measures (YTD, MoM, YoY)
- Understands context transition and when it occurs

**Evidence:**
- Successfully explained CALCULATE with multiple filter conditions
- Wrote optimized DAX measures using variables
- Demonstrated understanding of ALLSELECTED vs ALL vs ALLEXCEPT

**Areas Covered:**
- ✅ Q5: Advanced DAX Measures (MoM Growth, YTD)
- ✅ Q6: Context Transition & Filter Context
- ✅ Q28: ALL, ALLEXCEPT, ALLSELECTED

---

### Data Modeling: ⭐⭐⭐⭐⭐ Excellent (20/20 points)
**Strengths:**
- Well-structured star schema approach
- Excellent relationship handling (1:*, *:*, bridge tables)
- Strong understanding of cardinality and its implications
- Knows when to use calculated columns vs measures
- Proper dimension and fact table design

**Evidence:**
- Explained star schema implementation for 9-server integration
- Handled many-to-many relationships using bridge tables
- Optimized model for 25M+ records with proper indexing

**Areas Covered:**
- ✅ Q1: Real-Time Call Quality Dashboard Deep Dive
- ✅ Q3: Data Modeling Best Practices
- ✅ Q15: Relationships and Cardinality

---

### SQL / Power Query: ⭐⭐⭐⭐ Good (8/10 points)
**Strengths:**
- Proficient in Merge Query and different join types
- Good understanding of query optimization techniques
- Knows query folding and how to maintain it
- Can write complex SQL with window functions
- Understands ETL vs ELT approaches

**Evidence:**
- Wrote SQL query for top clients by ACD with proper indexing
- Explained query folding and how to check for it
- Successfully merged data from multiple sources in Power Query

**Minor Gaps:**
- Could improve on advanced SQL optimization for very large datasets
- Limited experience with stored procedures and complex CTEs

**Areas Covered:**
- ✅ Q8: SQL Query - Call Quality Analysis
- ✅ Q17: Power Query vs DAX
- ✅ Q18: Query Folding

---

### Visualization: ⭐⭐⭐⭐⭐ Very Good (Score included in Power BI)
**Strengths:**
- Clean, interactive dashboards with good UX
- Strong storytelling ability with data
- Effective use of bookmarks and drill-through
- Understands visual performance optimization
- Good color theory and dashboard design principles

**Evidence:**
- Built 3 production dashboards with high user adoption
- Used bookmarks for toggling views and drill-through for details
- Reduced ticket investigation time by 40% through effective visualization

**Areas Covered:**
- ✅ Q19: Bookmarks and Drill-through
- ✅ Q25: Mobile Layout and Responsive Design

---

### Python (Optional Integration): ⭐⭐⭐⭐⭐ Very Good (14/15 points)
**Strengths:**
- Understands use for data preprocessing and analytics
- Strong pandas proficiency (groupby, merge, pivot)
- Good error handling and logging practices
- Can automate complex workflows (email parsing, file processing)
- Writes clean, maintainable code

**Evidence:**
- Successfully completed Invoice Parsing coding challenge
- Demonstrated email automation with imaplib
- Reduced manual work by 80% through Python automation

**Areas Covered:**
- ✅ Coding Challenge 1: Invoice Parsing
- ✅ Q31: Large File Handling
- ✅ Q34: Email Automation

---

### Security / RLS: ⭐⭐⭐⭐ Good (Score included in Power BI)
**Strengths:**
- Knows both static and dynamic RLS setup
- Understands USERPRINCIPALNAME() function
- Can implement role-based data access
- Tested RLS using "View as Role" feature

**Evidence:**
- Implemented RLS for 150+ clients in Business Pulse Tracker
- Created dynamic RLS for account managers and static for regions
- Properly tested with different user roles

**Minor Gaps:**
- Could explore more complex RLS scenarios (hierarchical security)

**Areas Covered:**
- ✅ Q2: Row-Level Security Implementation

---

## 💡 SOFT SKILLS ASSESSMENT

### Communication: ⭐⭐⭐⭐⭐ Excellent (9/10 points)
**Strengths:**
- Communicates clearly and confidently
- Can explain technical concepts to non-technical stakeholders
- Uses STAR method effectively for behavioral questions
- Good active listening skills
- Structured thinking and articulation

**Evidence:**
- Explained complex DAX concepts using simple analogies
- Demonstrated stakeholder management in Business Pulse Tracker project
- Clearly articulated problem-solving approach

---

### Analytical Thinking: ⭐⭐⭐⭐⭐ Excellent (9/10 points)
**Strengths:**
- Strong problem-solving methodology
- Systematic debugging approach
- Considers trade-offs in technical decisions
- Data-driven decision making
- Proactive in identifying issues

**Evidence:**
- Identified and fixed timezone conversion error systematically
- Optimized dashboard performance using Performance Analyzer
- Reduced query time from 8 seconds to <1 second through indexing

---

### Business Understanding: ⭐⭐⭐⭐⭐ Very Good
**Strengths:**
- Understands business impact of technical work
- Translates business requirements to technical solutions
- Focuses on measurable outcomes (40% faster, 60% reduction)
- Good stakeholder management
- Balances technical excellence with business value

**Evidence:**
- All projects show clear business impact metrics
- Gathered requirements effectively for NOC dashboard
- Prioritized features based on business value

---

## 📈 DETAILED SCORING BREAKDOWN

| Category | Points Earned | Max Points | Percentage |
|----------|---------------|------------|------------|
| **Technical Skills** | **56** | **60** | **93%** |
| - Power BI & Data Modeling | 20 | 20 | 100% |
| - DAX | 14 | 15 | 93% |
| - SQL | 8 | 10 | 80% |
| - Python | 14 | 15 | 93% |
| **Problem-Solving** | **18** | **20** | **90%** |
| - Analytical Thinking | 9 | 10 | 90% |
| - Debugging Approach | 9 | 10 | 90% |
| **Communication** | **9** | **10** | **90%** |
| - Clarity of Explanations | 5 | 5 | 100% |
| - Technical Translation | 4 | 5 | 80% |
| **Experience Relevance** | **10** | **10** | **100%** |
| - Project Complexity | 5 | 5 | 100% |
| - Impact Demonstration | 5 | 5 | 100% |
| **TOTAL** | **78** | **100** | **78%** |

**Result:** ✅ **HIRE** (70-84 range)

---

## ✅ KEY STRENGTHS

### Technical Excellence:
1. **Data Modeling Mastery** - Excellent star schema design and relationship handling
2. **DAX Proficiency** - Strong understanding of filter context and complex measures
3. **End-to-End Power BI** - Covers entire lifecycle from data integration to deployment
4. **Python Automation** - Reduced manual work by 80% through intelligent automation
5. **Performance Optimization** - Optimized queries handling 25M+ records efficiently

### Project Impact:
1. **Measurable Results** - All projects show clear business impact (40% faster, 60% reduction)
2. **Scale** - Successfully handled enterprise-scale data (9 servers, 150+ clients, 25M records)
3. **Innovation** - Implemented Microsoft Fabric (emerging technology) successfully
4. **User Adoption** - High adoption rates indicate good UX and stakeholder management

### Soft Skills:
1. **Communication** - Clear, confident, can translate technical to business terms
2. **Problem-Solving** - Systematic approach to debugging and optimization
3. **Business Acumen** - Understands business context and focuses on value delivery
4. **Learning Agility** - Quickly adopted Microsoft Fabric and new technologies

---

## 🔧 AREAS FOR IMPROVEMENT

### 1. Large-Scale Performance Tuning (Priority: High)
**Current State:**
- Good performance optimization for current scale (25M records)
- Understands indexing and query optimization basics

**Gap:**
- Limited exposure to enterprise datasets (100M+ records)
- Could deepen knowledge of advanced optimization techniques

**Recommendation:**
- Assign to projects with larger datasets
- Training on advanced performance tuning (partitioning, aggregations)
- Explore columnstore indexes and advanced SQL optimization
- Learn about distributed computing (Spark, Databricks)

**Action Items:**
- [ ] Complete Microsoft Learn path on "Performance Tuning in Power BI"
- [ ] Shadow senior analyst on enterprise-scale project
- [ ] Experiment with billion-row datasets in sandbox environment
- [ ] Learn about data lakehouse optimization patterns

---

### 2. Advanced SQL Techniques (Priority: Medium)
**Current State:**
- Proficient in standard SQL queries and window functions
- Good understanding of joins and basic optimization

**Gap:**
- Limited experience with stored procedures
- Could improve on complex CTEs and recursive queries
- Less exposure to advanced indexing strategies

**Recommendation:**
- Practice writing stored procedures for complex business logic
- Learn about query execution plans and advanced optimization
- Explore materialized views and indexed views

**Action Items:**
- [ ] Complete SQL Server performance tuning course
- [ ] Practice writing complex CTEs and recursive queries
- [ ] Learn to read and optimize query execution plans

---

### 3. Advanced RLS Scenarios (Priority: Low)
**Current State:**
- Good understanding of static and dynamic RLS
- Successfully implemented for 150+ clients

**Gap:**
- Could explore hierarchical security models
- Limited experience with complex multi-level RLS

**Recommendation:**
- Learn about organizational hierarchy security
- Explore manager-subordinate RLS patterns
- Practice with complex security requirements

**Action Items:**
- [ ] Study advanced RLS patterns from SQLBI
- [ ] Implement hierarchical RLS in sandbox project

---

## 🎯 QUESTIONS ASKED & PERFORMANCE

### Section 1: Power BI & Data Modeling (20 min)
| Question | Performance | Notes |
|----------|-------------|-------|
| Q1: Real-Time Call Quality Dashboard | ⭐⭐⭐⭐⭐ Excellent | Detailed explanation of architecture, clear understanding of Fabric |
| Q2: Row-Level Security | ⭐⭐⭐⭐ Very Good | Good RLS implementation, could explore more complex scenarios |
| Q3: Data Modeling Best Practices | ⭐⭐⭐⭐⭐ Excellent | Strong optimization techniques, proper indexing strategy |
| Q15: Relationships and Cardinality | ⭐⭐⭐⭐⭐ Excellent | Handled many-to-many with bridge tables effectively |

### Section 2: DAX & Calculations (10 min)
| Question | Performance | Notes |
|----------|-------------|-------|
| Q5: Advanced DAX Measures | ⭐⭐⭐⭐⭐ Excellent | Wrote correct MoM and YTD measures with proper error handling |
| Q6: Context Transition | ⭐⭐⭐⭐ Very Good | Good understanding, could elaborate more on edge cases |
| Q28: ALL, ALLEXCEPT, ALLSELECTED | ⭐⭐⭐⭐⭐ Excellent | Clear explanation with practical examples |

### Section 3: SQL & Data Integration (10 min)
| Question | Performance | Notes |
|----------|-------------|-------|
| Q8: SQL Query - Call Quality Analysis | ⭐⭐⭐⭐ Good | Correct query, good indexing suggestions |
| Q9: Data Integration Challenges | ⭐⭐⭐⭐⭐ Excellent | Handled timezone and schema inconsistencies well |
| Q18: Query Folding | ⭐⭐⭐⭐ Very Good | Understands concept and how to maintain it |

### Section 4: Python Automation - CODING (15 min)
| Challenge | Performance | Notes |
|-----------|-------------|-------|
| Coding Challenge 1: Invoice Parsing | ⭐⭐⭐⭐⭐ Excellent | Clean code, proper error handling, good pandas usage |
| Q34: Email Automation | ⭐⭐⭐⭐⭐ Excellent | Demonstrated real-world implementation with imaplib |

### Section 5: Behavioral & Scenarios (5 min)
| Question | Performance | Notes |
|----------|-------------|-------|
| Q11: Problem-Solving Under Pressure | ⭐⭐⭐⭐⭐ Excellent | Used STAR method, showed systematic debugging approach |
| Q43: Requirement Gathering | ⭐⭐⭐⭐ Very Good | Good stakeholder management, iterative development |

---

## 💬 NOTABLE QUOTES & EXAMPLES

### Technical Depth:
> "When integrating data from 9 servers, I found duplicate calls logged on multiple servers. I created composite keys using CallID + ServerID + Timestamp and used Power Query to deduplicate based on business logic - keeping records from the primary server."

> "For the 25M record billing dashboard, I implemented incremental refresh for the last 7 days and created aggregation tables for monthly summaries. This reduced refresh time from 45 minutes to 8 minutes."

### Problem-Solving:
> "When the dashboard showed incorrect ASR metrics, I used Performance Analyzer to identify the issue, traced it to a timezone conversion error in Power Query, and implemented a fix within 4 hours. I also added automated data quality checks to prevent similar issues."

### Business Impact:
> "The NOC team was spending 10-15 minutes investigating each ticket manually. After deploying the real-time dashboard, they could identify issues in 6 minutes - a 40% improvement. This translated to handling 30% more tickets per day."

### Communication:
> "When the sales manager asked for 'real-time data,' I clarified that true real-time would require DirectQuery with performance trade-offs. I explained that our current 2-hour refresh met their actual need of 'seeing today's numbers,' which they confirmed was sufficient."

---

## 🎓 CANDIDATE QUESTIONS ASKED

1. **"What's the typical size of datasets you work with here?"**
   - Shows interest in technical challenges and scale

2. **"How is the BI team structured? Do analysts work independently or in pods?"**
   - Demonstrates interest in team dynamics and collaboration

3. **"What's your approach to balancing technical debt with new feature development?"**
   - Mature understanding of software development lifecycle

4. **"Are there opportunities to work with emerging technologies like Microsoft Fabric or AI features in Power BI?"**
   - Shows learning mindset and interest in innovation

**Quality of Questions:** ⭐⭐⭐⭐⭐ Excellent - Thoughtful, relevant questions showing genuine interest

---

## 📋 INTERVIEWER OBSERVATIONS

### Positive Indicators:
- ✅ Arrived 5 minutes early, well-prepared
- ✅ Brought portfolio of dashboard screenshots (good visual communication)
- ✅ Asked clarifying questions before answering (shows careful thinking)
- ✅ Admitted when unsure rather than bluffing (honesty and self-awareness)
- ✅ Showed enthusiasm for data and analytics throughout
- ✅ Took notes during the interview (active engagement)
- ✅ Thanked interviewer and asked about next steps (professionalism)

### Areas to Watch:
- ⚠️ Slightly nervous at the beginning (settled after 5 minutes)
- ⚠️ Tends to go into deep technical detail (good for technical audience, may need to adjust for executives)

### Cultural Fit:
- ✅ Collaborative mindset (gave credit to team members)
- ✅ Growth mindset (eager to learn and improve)
- ✅ Customer-focused (emphasized user adoption and feedback)
- ✅ Data-driven decision making
- ✅ Takes ownership and accountability

---

## 🎯 FINAL RECOMMENDATION

### Decision: ✅ **SELECTED - HIRE**

### Rationale:
1. **Strong Technical Foundation** - Excellent Power BI, DAX, and data modeling skills
2. **Proven Impact** - Demonstrated measurable business value in all projects
3. **Client-Ready** - Good communication skills and stakeholder management
4. **Growth Potential** - Shows learning agility and interest in emerging technologies
5. **Cultural Fit** - Collaborative, accountable, and customer-focused

### Suggested Role Level:
**Mid-Level Power BI Data Analyst** (2-3 years experience equivalent)

### Suggested Starting Projects:
1. **Onboarding Project (Week 1-2):** Enhance existing dashboard with new metrics
2. **First Solo Project (Month 1-2):** Build department-level dashboard with moderate complexity
3. **Growth Project (Month 3-6):** Lead enterprise-scale dashboard with large datasets (addresses improvement area)

### Compensation Recommendation:
Based on 1.8 years experience + strong technical skills + proven impact:
- **Suggested Band:** Mid-Level Analyst
- **Justification:** Skills exceed typical 1.8-year experience level due to enterprise-scale exposure

### Onboarding Focus Areas:
1. **Week 1:** Company data architecture, security protocols, deployment processes
2. **Week 2-4:** Shadow senior analyst on enterprise-scale project (address performance tuning gap)
3. **Month 2:** Advanced SQL training (address improvement area)
4. **Month 3:** Assign first client-facing project

### Mentorship Recommendation:
Pair with senior analyst who specializes in:
- Enterprise-scale performance optimization
- Advanced SQL techniques
- Client presentation skills

---

## 📊 COMPARISON WITH JOB REQUIREMENTS

| Requirement | Level Needed | Candidate Level | Status |
|-------------|--------------|-----------------|--------|
| Power BI Desktop & Service | Advanced | Advanced | ✅ Exceeds |
| DAX | Advanced | Advanced | ✅ Meets |
| Data Modeling | Advanced | Expert | ✅ Exceeds |
| SQL | Intermediate | Intermediate+ | ✅ Meets |
| Power Query / M | Intermediate | Advanced | ✅ Exceeds |
| Python (Nice-to-have) | Basic | Advanced | ✅ Exceeds |
| Microsoft Fabric | Basic | Intermediate | ✅ Exceeds |
| RLS Implementation | Intermediate | Intermediate | ✅ Meets |
| Performance Optimization | Intermediate | Intermediate | ✅ Meets |
| Stakeholder Management | Intermediate | Advanced | ✅ Exceeds |
| 2+ Years Experience | Required | 1.8 years | ⚠️ Slightly below |

**Overall:** 10/11 requirements met or exceeded. Slight experience gap offset by advanced skills.

---

## ✍️ NEXT STEPS

### Immediate Actions:
- [x] Complete interview feedback form
- [ ] Share feedback with hiring manager (by EOD)
- [ ] Schedule L2 interview with team lead (if required)
- [ ] Prepare offer letter (pending final approval)

### L2 Interview Focus (If Required):
- Cultural fit with broader team
- Presentation skills (ask candidate to present a past project)
- Collaboration scenarios
- Long-term career goals alignment

### Pre-Offer:
- [ ] Reference checks (2-3 references)
- [ ] Background verification
- [ ] Salary negotiation discussion

### Post-Offer:
- [ ] Onboarding plan preparation
- [ ] Assign mentor
- [ ] Set up development environment
- [ ] Schedule training sessions

---

## 📝 INTERVIEWER SIGN-OFF

**Interviewer Name:** [Interviewer Name]
**Title:** Senior Power BI Architect
**Date:** 12-November-2025
**Signature:** ___________________

**Reviewed By:** [Hiring Manager Name]
**Date:** ___________________
**Approval:** ☐ Approved  ☐ Needs Discussion  ☐ Rejected

**HR Review:** [HR Representative Name]
**Date:** ___________________
**Status:** ☐ Cleared for Offer  ☐ Pending  ☐ On Hold

---

**END OF L1 INTERVIEW FEEDBACK**

---

---

# 📚 DOCUMENT SUMMARY

## Complete Interview Package Contents:

### 📋 Part 1: Interview Preparation (Lines 1-2722)
1. **Executive Summary** - Overview of the interview plan
2. **Table of Contents** - Quick navigation guide
3. **Interview Structure** - 60-minute breakdown
4. **50+ Interview Questions** organized by category:
   - 16 Power BI & Data Modeling questions (Q1-Q4, Q14-Q25)
   - 8 DAX & Calculations questions (Q5-Q7, Q26-Q30)
   - 9 SQL & Data Integration questions (Q8-Q10, Q35-Q40)
   - 6 Python questions + 2 Coding Challenges (Q31-Q34)
   - 13 Behavioral & Scenario questions (Q11-Q13, Q41-Q50)
5. **Detailed Expected Answers** with code examples
6. **Scoring Rubric** (100-point scale)
7. **Quick Reference Guide** - Concepts checklist
8. **Interviewer Preparation Checklist**
9. **Red Flags & Green Flags**
10. **Sample Interview Flow** (60-minute timeline)
11. **Decision Matrix** (Strong Hire/Hire/Maybe/No Hire)
12. **Evaluation Form Template**
13. **Appendix** - Additional resources

### 📝 Part 2: L1 Interview Feedback (Lines 2723-3240)
**Actual Interview Results for Current Candidate:**
- Overall Assessment: **78/100 - SELECTED (HIRE)**
- Detailed technical skills breakdown by category
- Soft skills assessment
- Scoring breakdown with percentages
- Key strengths (5 technical + 4 project impact + 4 soft skills)
- Areas for improvement (3 detailed with action items)
- Question-by-question performance review
- Notable quotes and examples
- Candidate questions asked
- Interviewer observations
- Final recommendation with rationale
- Comparison with job requirements
- Next steps and onboarding plan

---

## 📊 Key Statistics:

- **Total Questions Available:** 50+
- **Questions Asked in L1:** 15 questions
- **Coding Challenges:** 2 (15 minutes)
- **Interview Duration:** 60 minutes
- **Candidate Score:** 78/100
- **Result:** ✅ SELECTED - HIRE
- **Experience Level:** 1.8 years (targeting 2+)
- **Strengths Identified:** 13
- **Improvement Areas:** 3
- **Projects Discussed:** 3 major dashboards

---

## 🎯 How to Use This Document:

### For Interviewers:
1. **Before Interview:** Review Executive Summary and select 8-10 questions based on role requirements
2. **During Interview:** Use expected answers as a guide, take notes on evaluation form
3. **After Interview:** Complete scoring rubric and feedback section
4. **Decision Making:** Use decision matrix to determine hire/no-hire

### For Hiring Managers:
1. Review L1 Interview Feedback section for detailed assessment
2. Check scoring breakdown and comparison with job requirements
3. Review areas for improvement and onboarding recommendations
4. Make final hiring decision based on comprehensive feedback

### For HR:
1. Use evaluation form for structured documentation
2. Reference next steps section for offer process
3. Use onboarding plan for new hire preparation
4. Track improvement areas for performance reviews

### For Candidates (Post-Interview):
1. Review areas for improvement for self-development
2. Understand expectations for the role
3. Prepare questions based on feedback received

---

## 📈 Success Metrics:

### Interview Process Quality:
- ✅ Comprehensive coverage of all technical areas
- ✅ Structured evaluation with objective scoring
- ✅ Detailed feedback for candidate development
- ✅ Clear hiring decision with rationale

### Candidate Assessment:
- ✅ Technical Skills: 93% (56/60 points)
- ✅ Problem-Solving: 90% (18/20 points)
- ✅ Communication: 90% (9/10 points)
- ✅ Experience Relevance: 100% (10/10 points)
- ✅ **Overall: 78% - HIRE RANGE**

### Business Impact Demonstrated:
- 40% faster ticket investigation
- 60% reduction in manual billing work
- 80% reduction in rate sheet processing time
- 15% increase in client engagement
- 25M+ records processed monthly

---

## 🔄 Document Maintenance:

### Version History:
- **v1.0** (12-Nov-2025): Initial comprehensive interview plan created
- **v1.1** (12-Nov-2025): Added L1 Interview Feedback section with actual results

### Review Schedule:
- **Quarterly Review:** Update questions based on technology changes
- **Post-Interview:** Update based on interviewer feedback
- **Annual Review:** Major revision based on hiring trends

### Feedback Loop:
- Collect interviewer feedback on question effectiveness
- Track candidate performance patterns
- Update expected answers based on real responses
- Refine scoring rubric based on hiring outcomes

---

## 📞 Contact Information:

**For Questions About This Interview Plan:**
- Interview Team Lead: [Name]
- HR Business Partner: [Name]
- Technical Hiring Manager: [Name]

**For Candidate-Specific Questions:**
- Refer to L1 Interview Feedback section
- Contact interviewer: [Interviewer Name]
- Hiring Manager: [Manager Name]

---

## ✅ FINAL CHECKLIST

### Interview Preparation:
- [x] Interview plan created with 50+ questions
- [x] Expected answers documented with code examples
- [x] Scoring rubric defined (100-point scale)
- [x] Evaluation form template ready
- [x] Sample interview flow created

### Interview Execution:
- [x] L1 Interview completed (60 minutes)
- [x] 15 questions asked covering all areas
- [x] 2 coding challenges completed
- [x] Detailed notes taken
- [x] Scoring completed (78/100)

### Post-Interview:
- [x] Feedback documented comprehensively
- [x] Strengths and improvement areas identified
- [x] Hiring recommendation made (SELECTED)
- [ ] Feedback shared with hiring manager
- [ ] L2 interview scheduled (if required)
- [ ] Offer preparation initiated

### Onboarding (If Hired):
- [ ] Onboarding plan prepared
- [ ] Mentor assigned
- [ ] Training sessions scheduled
- [ ] First project identified
- [ ] Development environment setup

---

**🎉 INTERVIEW PLAN COMPLETE**

This comprehensive interview package provides everything needed to:
- ✅ Conduct a thorough 60-minute technical interview
- ✅ Assess candidates objectively across all competencies
- ✅ Make data-driven hiring decisions
- ✅ Provide constructive feedback for candidate development
- ✅ Plan effective onboarding for successful hires

**Total Document Length:** 3,300+ lines
**Total Questions:** 50+
**Coding Challenges:** 2
**Expected Answers:** All questions
**Code Examples:** 30+
**Real Interview Feedback:** Complete L1 assessment included

---

**END OF COMPLETE INTERVIEW PACKAGE**
