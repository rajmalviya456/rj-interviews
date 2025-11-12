# L2 Interview Plan: Prakhar - Power BI Data Analyst

**Candidate:** Prakhar
**Position:** Power BI Data Analyst - L2
**Interview Date:** 13-November-2025
**Experience:** 3 years
**Interviewer:** _______________
**Duration:** 60 minutes

---

## EXECUTIVE SUMMARY

### Candidate Background:
- **Experience:** 3 years as Data Analyst
- **Certifications:** PL-300 Microsoft Certified Power BI Data Analyst
- **Key Strengths:** Power BI end-to-end, DAX, data modeling, visualization
- **Notable Achievement:** Led complete migration from Spotfire/Tableau to Power BI, 99% data accuracy improvement

### L1 Interview Performance:
**✅ Strong Areas:**
- Excellent Power BI/DAX knowledge (CALCULATE, SUMX, filter context)
- Excellent data modeling (star schema, relationships)
- Very good SQL/Power Query proficiency
- Excellent visualization and storytelling
- Strong communication and business understanding
- Good RLS implementation knowledge

**🎯 Areas to Validate/Probe:**
- Power BI REST API and automation capabilities
- Large-scale performance tuning (enterprise datasets)
- Advanced optimization techniques beyond basics
- Real-world migration challenges and solutions

### L2 Interview Focus:
1. **Deep dive into Spotfire/Tableau → Power BI migration** (technical challenges, decisions)
2. **Advanced performance optimization** (validate enterprise-scale experience)
3. **Complex DAX scenarios** (confirm L1 assessment of "excellent")
4. **Power BI REST API / Automation** (explore growth area)
5. **Live coding challenges** (validate practical skills)

### Passing Criteria:
- **Technical Score:** 70+ / 100
- **Must demonstrate:** Advanced DAX, performance optimization, migration expertise
- **Red flags:** Cannot explain migration details, vague on optimization, DAX knowledge doesn't match L1 assessment

---

## L1 FEEDBACK INTEGRATION

### Strengths to Confirm:
- [ ] Advanced DAX proficiency (CALCULATE, SUMX, context transition)
- [ ] Star schema and data modeling best practices
- [ ] Clean, interactive dashboard design
- [ ] Business KPI understanding and translation

### Areas to Explore/Develop:
- [ ] **Power BI REST API** - Ask about automation needs, API awareness
- [ ] **Power Automate integration** - Explore use cases and experience
- [ ] **Enterprise-scale performance** - Probe with large dataset scenarios
- [ ] **Advanced optimization** - Beyond basic techniques

### Questions Added Based on L1:
- Q1: Migration project deep dive (validate technical leadership)
- Q3: Performance optimization with large datasets (address L1 gap)
- Q7: Advanced DAX context scenarios (confirm "excellent" rating)
- Q10: Power BI REST API and automation (explore growth area)

---

## INTERVIEW STRUCTURE (60 minutes)

### Timeline:
- **0:00-0:05** (5 min) - Introduction & Background
- **0:05-0:25** (20 min) - Power BI & Data Modeling Deep Dive
- **0:25-0:35** (10 min) - DAX & Calculations
- **0:35-0:45** (10 min) - SQL & Data Integration
- **0:45-0:55** (10 min) - Python Coding Challenge
- **0:55-1:00** (5 min) - Behavioral & Q&A

---

## SECTION 1: Introduction & Background (5 minutes)

### Q1: Spotfire/Tableau to Power BI Migration Deep Dive

**Question:**
"You led the complete migration of dashboards from Spotfire and Tableau to Power BI. This is impressive for someone with 3 years of experience. Walk me through:
- How many dashboards did you migrate?
- What was the biggest technical challenge you faced?
- How did you handle data sources that were configured differently in Spotfire/Tableau?
- What was your approach to ensuring feature parity or improvement?
- How did you manage stakeholder expectations during the migration?"

**Expected Answer:**

**Migration Scope:**
- Should mention specific number of dashboards (e.g., "15-20 dashboards" or similar)
- Timeline for migration (e.g., "3-month project")
- Team involvement (solo or team effort)

**Technical Challenges:**
- **Data Source Differences:**
  - Spotfire/Tableau may have used different connection methods
  - Had to reconfigure connections in Power BI (DirectQuery vs Import)
  - Handled authentication and gateway setup

- **Visualization Parity:**
  - Some Spotfire/Tableau visuals don't have direct Power BI equivalents
  - Had to recreate custom visuals or find alternatives
  - Improved some visualizations using Power BI's strengths

- **DAX vs Tableau Calculations:**
  - Converted Tableau calculated fields to DAX measures
  - Rewrote complex calculations to leverage DAX patterns
  - Optimized for Power BI's calculation engine

**Stakeholder Management:**
- Conducted training sessions for end users
- Created documentation for new dashboards
- Managed change management and adoption
- Gathered feedback and iterated

**Follow-up Questions:**
1. "What was one calculation that was difficult to convert from Tableau to DAX? How did you solve it?"
2. "Did you improve performance compared to the old tools? How did you measure it?"
3. "How did you handle users who were resistant to the change?"

**Scoring:**
- **Basic (5/10):** Participated in migration, basic understanding
- **Intermediate (7/10):** Led portions, solved technical challenges, good stakeholder communication
- **Advanced (10/10):** Led entire migration, overcame complex challenges, measurable improvements, excellent change management

**Red Flags:**
- Cannot provide specific details about the migration
- Vague about technical challenges
- No mention of stakeholder management
- Claims to have "led" but can't explain decisions

**Green Flags:**
- Specific examples of challenges and solutions
- Mentions measurable improvements (performance, user adoption)
- Shows leadership and project management skills
- Discusses lessons learned

---

### Q2: What motivated you to get PL-300 certified?

**Question:**
"You have the PL-300 certification. What motivated you to get certified, and how has it helped in your work?"

**Expected Answer:**
- Career growth and skill validation
- Structured learning of Power BI best practices
- Helped in migration project or specific work scenarios
- Shows commitment to continuous learning

**Scoring:** Quick assessment (2-3 minutes)
- Shows learning mindset and professional development

---

## SECTION 2: Power BI & Data Modeling (20 minutes)

### Q3: Performance Optimization with Large Datasets

**Context:** L1 noted need for more exposure to large-scale performance tuning.

**Question:**
"You mentioned improving data accuracy to 99%. Let's talk about performance optimization. Imagine you have a Power BI report with:
- 50 million rows in the fact table
- 10+ dimension tables
- 20+ measures with complex DAX
- Report is slow (15-20 seconds to load visuals)

Walk me through your systematic approach to diagnose and fix this performance issue."

**Expected Answer:**

**Diagnosis Approach:**
1. **Performance Analyzer:**
   - Use Performance Analyzer in Power BI Desktop
   - Identify which visuals are slow
   - Check DAX query times vs visual rendering times

2. **DAX Studio:**
   - Analyze query plans
   - Check for expensive operations (scans vs seeks)
   - Identify measures causing issues
   - Look at storage engine vs formula engine usage

3. **Data Model Analysis:**
   - Check model size and cardinality
   - Review relationships and cross-filtering
   - Identify unnecessary columns

**Optimization Techniques:**

**Data Model Level:**
- **Remove unnecessary columns** from tables
- **Use integer keys** instead of text for relationships
- **Disable auto date/time hierarchy** if not needed
- **Split date and time** into separate columns if appropriate
- **Use star schema** instead of snowflake where possible
- **Reduce cardinality** where possible (e.g., group categories)

**DAX Optimization:**
- **Use variables** to avoid recalculation:
  ```dax
  Sales YoY % =
  VAR CurrentSales = SUM(Sales[Amount])
  VAR PreviousSales = CALCULATE(SUM(Sales[Amount]), SAMEPERIODLASTYEAR(Date[Date]))
  RETURN DIVIDE(CurrentSales - PreviousSales, PreviousSales)
  ```
- **Avoid calculated columns** where measures work
- **Use SUMMARIZE carefully** (can be expensive)
- **Avoid iterators** (SUMX, FILTER) when simple aggregations work
- **Use KEEPFILTERS** instead of FILTER when appropriate

**Query Optimization:**
- **Aggregations:** Create aggregation tables for common queries
- **Incremental Refresh:** Only refresh recent data
  - Set up date-based partitioning
  - Configure refresh policy (e.g., last 2 years, refresh last 7 days)
- **Composite Models:** Use DirectQuery for large historical data, Import for recent data

**Visual Optimization:**
- **Limit visuals per page** (max 10-15)
- **Avoid high-cardinality visuals** (e.g., table with 10K rows)
- **Use bookmarks** to toggle between views instead of multiple visuals
- **Reduce filter interactions** where not needed

**Follow-up Questions:**
1. "What's the difference between storage engine and formula engine in DAX? Which is faster?"
   - **Expected:** Storage engine (VertiPaq) is faster, works with compressed data. Formula engine handles complex calculations that can't be pushed to storage engine.

2. "When would you use DirectQuery vs Import mode for a 50M row table?"
   - **Expected:**
     - Import: If data fits in memory, need fast performance, data doesn't change frequently
     - DirectQuery: Real-time data needed, data too large for memory, security requirements
     - Composite: Best of both - Import for dimensions, DirectQuery for large facts

3. "You mentioned incremental refresh. What are the prerequisites?"
   - **Expected:**
     - Power BI Premium or Premium Per User
     - Date/time column for partitioning
     - RangeStart and RangeEnd parameters in Power Query
     - Proper filter configuration

**Scoring:**
- **Basic (5/10):** Knows some optimization techniques (remove columns, use variables)
- **Intermediate (7/10):** Systematic approach, multiple techniques, understands trade-offs
- **Advanced (10/10):** Comprehensive diagnosis process, advanced techniques (aggregations, incremental refresh), understands storage vs formula engine

**Red Flags:**
- Cannot explain systematic diagnosis approach
- Only knows basic optimizations
- Doesn't understand when to use different techniques
- Cannot explain trade-offs

**Green Flags:**
- Mentions DAX Studio or Performance Analyzer
- Systematic, methodical approach
- Understands storage engine vs formula engine
- Knows advanced techniques (aggregations, incremental refresh)
- Can explain when to use each technique

---

### Q4: Row-Level Security (RLS) Implementation

**Context:** L1 noted "Good" knowledge of RLS. Let's validate depth.

**Question:**
"You mentioned implementing RLS for role-based data access. Describe a specific scenario where you implemented RLS:
- What was the business requirement?
- Did you use static or dynamic RLS?
- How did you design the security model?
- How did you test it?"

**Expected Answer:**

**Business Scenario Example:**
- "Sales managers should only see their region's data"
- "Account managers should only see their assigned clients"
- "Executives should see all data"

**RLS Design:**

**Static RLS:**
```dax
[Region] = "North"
```
- Hard-coded filters
- Need separate role for each region
- Less scalable

**Dynamic RLS (Preferred):**
```dax
[Email] = USERPRINCIPALNAME()
```
Or with a security table:
```dax
[Region] = LOOKUPVALUE(
    UserSecurity[Region],
    UserSecurity[Email], USERPRINCIPALNAME()
)
```

**Implementation Steps:**
1. Created a UserSecurity table with Email and Region columns
2. Created relationship between UserSecurity and fact/dimension tables
3. Created roles in Power BI Desktop
4. Applied DAX filter using USERPRINCIPALNAME()
5. Published to Power BI Service
6. Assigned users to roles in workspace settings

**Testing:**
- Used "View as Role" in Power BI Desktop
- Created test accounts with different permissions
- Validated with actual users before full rollout
- Checked for performance impact

**Follow-up:** "What's the performance impact of RLS? How would you optimize it?"

**Expected Answer:**
- RLS adds filters to every query, can impact performance
- Optimize by:
  - Using efficient DAX in RLS rules
  - Avoiding complex calculations in RLS filters
  - Testing with large datasets
  - Consider using object-level security for very complex scenarios

**Scoring:**
- **Basic (5/10):** Understands concept, implemented simple RLS
- **Intermediate (7/10):** Implemented dynamic RLS, proper testing
- **Advanced (10/10):** Complex RLS with multiple roles, performance considerations, thorough testing

---

### Q5: Data Modeling - Star Schema

**Context:** L1 noted "Excellent" data modeling. Validate understanding.

**Question:**
"You mentioned using star schema. Explain:
- Why star schema over snowflake schema in Power BI?
- How do you handle slowly changing dimensions (SCD)?
- What's your approach to handling many-to-many relationships?"

**Expected Answer:**

**Star Schema vs Snowflake:**
- **Star Schema (Preferred in Power BI):**
  - Denormalized dimension tables
  - Simpler queries, better performance
  - Easier for users to understand
  - Better compression in VertiPaq

- **Snowflake Schema:**
  - Normalized dimension tables
  - More complex queries
  - Can impact performance
  - Use only if necessary (e.g., very large dimensions)

**Slowly Changing Dimensions (SCD):**

**Type 1 (Overwrite):**
- Simply update the record
- No history maintained
- Use when history not important

**Type 2 (Add new row):**
- Add new row with effective dates
- Maintain full history
- Use StartDate, EndDate, IsCurrent columns
```
ProductKey | ProductName | Category | StartDate  | EndDate    | IsCurrent
1          | Widget A    | Cat1     | 2023-01-01 | 2024-06-30 | 0
1          | Widget A    | Cat2     | 2024-07-01 | 9999-12-31 | 1
```

**Type 3 (Add new column):**
- Add columns for previous values
- Limited history (e.g., Current_Category, Previous_Category)

**Many-to-Many Relationships:**

**Approach 1: Bridge Table**
- Create intermediate table
- Two one-to-many relationships
- Use CROSSFILTER or bidirectional filtering carefully

**Approach 2: DAX Measures**
```dax
Sales Amount =
CALCULATE(
    SUM(Sales[Amount]),
    CROSSFILTER(Product[ProductID], Sales[ProductID], Both)
)
```

**Approach 3: Composite Models**
- Use DirectQuery for one side, Import for other
- Leverage Power BI's many-to-many relationship feature

**Scoring:**
- **Basic (5/10):** Understands star schema basics
- **Intermediate (7/10):** Knows SCD types, can handle many-to-many
- **Advanced (10/10):** Deep understanding, can explain trade-offs, knows multiple approaches

---

## SECTION 3: DAX & Calculations (10 minutes)

### Q6: Write DAX Measures - Business Scenario

**Question:**
"You're working on a sales dashboard. Write DAX measures for:

1. **Month-over-Month Growth %** for sales amount
2. **Year-to-Date (YTD) Sales**
3. **Top 5 Products by Sales** (dynamic measure that works in any visual)"

**Expected Answer:**

**1. Month-over-Month Growth %:**
```dax
MoM Growth % =
VAR CurrentMonth = SUM(Sales[Amount])
VAR PreviousMonth =
    CALCULATE(
        SUM(Sales[Amount]),
        DATEADD(Date[Date], -1, MONTH)
    )
RETURN
    DIVIDE(CurrentMonth - PreviousMonth, PreviousMonth, 0)
```

**Alternative using PARALLELPERIOD:**
```dax
MoM Growth % =
VAR CurrentMonth = [Total Sales]
VAR PreviousMonth =
    CALCULATE(
        [Total Sales],
        PARALLELPERIOD(Date[Date], -1, MONTH)
    )
RETURN
    DIVIDE(CurrentMonth - PreviousMonth, PreviousMonth, 0)
```

**2. Year-to-Date Sales:**
```dax
YTD Sales =
CALCULATE(
    SUM(Sales[Amount]),
    DATESYTD(Date[Date])
)
```

**With fiscal year:**
```dax
YTD Sales (Fiscal) =
CALCULATE(
    SUM(Sales[Amount]),
    DATESYTD(Date[Date], "06/30")  // Fiscal year ends June 30
)
```

**3. Top 5 Products by Sales:**
```dax
Top 5 Products Sales =
VAR CurrentProduct = SELECTEDVALUE(Product[ProductName])
VAR ProductRank =
    RANKX(
        ALL(Product[ProductName]),
        [Total Sales],
        ,
        DESC,
        DENSE
    )
RETURN
    IF(ProductRank <= 5, [Total Sales], BLANK())
```

**Alternative using TOPN:**
```dax
Top 5 Products Sales =
IF(
    SELECTEDVALUE(Product[ProductName]) IN
        SELECTCOLUMNS(
            TOPN(5, ALL(Product[ProductName]), [Total Sales], DESC),
            "Product", Product[ProductName]
        ),
    [Total Sales],
    BLANK()
)
```

**Follow-up Questions:**

1. **"Why use DIVIDE instead of the / operator?"**
   - **Expected:** DIVIDE handles division by zero gracefully, returns alternate result (default BLANK or custom value), prevents errors

2. **"What's the difference between DATEADD and PARALLELPERIOD?"**
   - **Expected:**
     - DATEADD: Shifts dates by specified interval, returns same number of days
     - PARALLELPERIOD: Returns complete parallel period (e.g., entire previous month)
     - For MoM, both work, but PARALLELPERIOD is more intuitive

3. **"Explain the difference between ALL and ALLSELECTED."**
   - **Expected:**
     - ALL: Removes all filters from specified columns/table
     - ALLSELECTED: Removes filters but respects filters from outside the visual (e.g., slicers)
     - Use ALLSELECTED when you want to respect page-level filters

**Scoring:**
- **Basic (5/10):** Can write simple measures, basic time intelligence
- **Intermediate (7/10):** Correct measures, uses variables, understands functions
- **Advanced (10/10):** Multiple approaches, explains trade-offs, handles edge cases

**Red Flags:**
- Cannot write basic time intelligence measures
- Doesn't use variables (inefficient code)
- Doesn't handle division by zero
- Cannot explain function differences

**Green Flags:**
- Uses variables for efficiency
- Handles edge cases (division by zero, no selection)
- Knows multiple approaches
- Can explain when to use each function

---

### Q7: Context Transition & Filter Context (Advanced)

**Context:** L1 noted "Excellent" DAX knowledge. Validate advanced understanding.

**Question:**
"Explain the difference between these two measures and when each would be used:

```dax
Measure 1 = SUMX(Sales, Sales[Quantity] * Sales[Price])

Measure 2 = SUMX(Sales, [Total Sales])
```

What is context transition and when does it occur?"

**Expected Answer:**

**Measure 1:**
```dax
SUMX(Sales, Sales[Quantity] * Sales[Price])
```
- Iterates row by row through Sales table
- For each row, multiplies Quantity * Price
- Sums all results
- **Row context only** - no filter context created
- Efficient for simple calculations

**Measure 2:**
```dax
SUMX(Sales, [Total Sales])
```
- Iterates row by row through Sales table
- For each row, evaluates the measure [Total Sales]
- **Context transition occurs** - row context converts to filter context
- Less efficient due to context transition overhead
- Use when you need to evaluate complex measures row by row

**Context Transition:**
- Occurs when a measure is evaluated inside a row context (e.g., inside SUMX, FILTER, calculated column)
- DAX automatically converts row context to filter context
- Equivalent to wrapping in CALCULATE
- Can be expensive performance-wise

**Example:**
```dax
// These are equivalent:
Measure A = SUMX(Sales, [Total Sales])

Measure B = SUMX(Sales, CALCULATE([Total Sales]))
```

**When to Use Each:**

**Use Measure 1 (Direct column reference):**
- Simple calculations
- Better performance
- When you don't need measure logic

**Use Measure 2 (Measure reference):**
- Need to reuse complex measure logic
- Measure has filters or complex calculations
- Accept performance trade-off for code reusability

**Follow-up:** "How would you optimize Measure 2 if it's causing performance issues?"

**Expected Answer:**
- Avoid context transition by rewriting logic directly in iterator
- Use variables to cache results
- Consider calculated column if appropriate
- Use SUMMARIZE or ADDCOLUMNS to pre-aggregate

**Scoring:**
- **Basic (5/10):** Knows both work, vague on differences
- **Intermediate (7/10):** Understands context transition concept
- **Advanced (10/10):** Deep understanding, can explain performance implications, knows optimization techniques

---

## SECTION 4: SQL & Data Integration (10 minutes)

### Q8: SQL Query - Business Intelligence Scenario

**Question:**
"You're working with a sales database. Write a SQL query to find:

**The top 10 customers by total sales amount in the last 12 months, showing:**
- Customer Name
- Total Sales Amount
- Number of Orders
- Average Order Value
- Rank by sales amount

Assume tables:
- `Customers` (CustomerID, CustomerName)
- `Orders` (OrderID, CustomerID, OrderDate, TotalAmount)"

**Expected Answer:**

```sql
SELECT
    c.CustomerName,
    SUM(o.TotalAmount) AS TotalSales,
    COUNT(o.OrderID) AS NumberOfOrders,
    AVG(o.TotalAmount) AS AvgOrderValue,
    RANK() OVER (ORDER BY SUM(o.TotalAmount) DESC) AS SalesRank
FROM Customers c
INNER JOIN Orders o ON c.CustomerID = o.CustomerID
WHERE o.OrderDate >= DATEADD(MONTH, -12, GETDATE())
GROUP BY c.CustomerName
ORDER BY TotalSales DESC
LIMIT 10;
```

**Alternative with CTE:**
```sql
WITH CustomerSales AS (
    SELECT
        c.CustomerName,
        SUM(o.TotalAmount) AS TotalSales,
        COUNT(o.OrderID) AS NumberOfOrders,
        AVG(o.TotalAmount) AS AvgOrderValue
    FROM Customers c
    INNER JOIN Orders o ON c.CustomerID = o.CustomerID
    WHERE o.OrderDate >= DATEADD(MONTH, -12, GETDATE())
    GROUP BY c.CustomerName
)
SELECT
    *,
    RANK() OVER (ORDER BY TotalSales DESC) AS SalesRank
FROM CustomerSales
ORDER BY TotalSales DESC
LIMIT 10;
```

**Follow-up Questions:**

1. **"What's the difference between RANK(), DENSE_RANK(), and ROW_NUMBER()?"**

   **Expected Answer:**
   - **RANK():** Assigns same rank to ties, skips next rank (1, 2, 2, 4)
   - **DENSE_RANK():** Assigns same rank to ties, doesn't skip (1, 2, 2, 3)
   - **ROW_NUMBER():** Always unique, no ties (1, 2, 3, 4)

2. **"How would you optimize this query for a table with 100 million rows?"**

   **Expected Answer:**
   - **Indexes:**
     - Index on `OrderDate` for WHERE clause
     - Index on `CustomerID` for JOIN
     - Covering index: `(OrderDate, CustomerID) INCLUDE (TotalAmount, OrderID)`

   - **Partitioning:**
     - Partition Orders table by OrderDate (monthly or yearly)
     - Query will only scan relevant partitions

   - **Materialized Views:**
     - Pre-aggregate customer sales monthly
     - Query the aggregated view instead

   - **Query Optimization:**
     - Use `TOP 10` instead of `LIMIT 10` (SQL Server)
     - Consider filtering by date first, then joining
     - Use `WITH (NOLOCK)` if dirty reads acceptable

3. **"What's the difference between INNER JOIN and LEFT JOIN? When would you use each?"**

   **Expected Answer:**
   - **INNER JOIN:** Returns only matching rows from both tables
   - **LEFT JOIN:** Returns all rows from left table, matching rows from right (NULL if no match)
   - **Use INNER JOIN:** When you only want customers who have orders
   - **Use LEFT JOIN:** When you want all customers, even those without orders

**Scoring:**
- **Basic (5/10):** Can write basic query with JOIN and GROUP BY
- **Intermediate (7/10):** Correct query with window functions, understands optimization basics
- **Advanced (10/10):** Multiple approaches (CTE), deep optimization knowledge, explains trade-offs

---

### Q9: Data Integration - Power Query

**Question:**
"You mentioned using Power Query for data cleansing and transformation. Describe a complex transformation you implemented. What M code did you write, if any?"

**Expected Answer:**

**Example Scenario:**
"I had to integrate sales data from multiple regional Excel files with inconsistent column names and formats."

**Transformation Steps:**
1. **Combine Files:**
   - Used "Combine Files" feature or `Folder.Files()`
   - Created function to process each file

2. **Standardize Column Names:**
   - Renamed columns to consistent naming
   - Used `Table.RenameColumns()`

3. **Data Type Conversion:**
   - Converted date columns (different formats across regions)
   - Handled currency symbols and decimal separators

4. **Data Cleansing:**
   - Removed duplicates
   - Handled null values
   - Trimmed whitespace
   - Standardized categorical values (e.g., "NY" → "New York")

5. **Add Calculated Columns:**
   - Extracted year/month from date
   - Calculated derived metrics

**M Code Example:**
```m
let
    Source = Folder.Files("C:\SalesData"),
    FilteredFiles = Table.SelectRows(Source, each Text.EndsWith([Name], ".xlsx")),

    // Function to process each file
    ProcessFile = (FilePath as text) =>
        let
            Source = Excel.Workbook(File.Contents(FilePath)),
            Data = Source{[Name="Sales"]}[Data],

            // Standardize column names
            RenamedColumns = Table.RenameColumns(Data, {
                {"Cust Name", "CustomerName"},
                {"Sale Amt", "SalesAmount"},
                {"Dt", "Date"}
            }),

            // Data type conversion
            TypedData = Table.TransformColumnTypes(RenamedColumns, {
                {"Date", type date},
                {"SalesAmount", type number},
                {"CustomerName", type text}
            }),

            // Clean data
            TrimmedData = Table.TransformColumns(TypedData, {
                {"CustomerName", Text.Trim}
            }),

            // Add calculated columns
            AddedColumns = Table.AddColumn(TrimmedData, "Year",
                each Date.Year([Date]), Int64.Type)
        in
            AddedColumns,

    // Apply function to all files
    ProcessedFiles = Table.AddColumn(FilteredFiles, "Data",
        each ProcessFile([Folder Path] & [Name])),

    // Expand and combine
    ExpandedData = Table.ExpandTableColumn(ProcessedFiles, "Data",
        {"CustomerName", "SalesAmount", "Date", "Year"}),

    // Remove file metadata columns
    FinalData = Table.SelectColumns(ExpandedData,
        {"CustomerName", "SalesAmount", "Date", "Year"})
in
    FinalData
```

**Follow-up:** "What's the difference between Power Query and DAX? When do you use each?"

**Expected Answer:**
- **Power Query (M):**
  - ETL - Extract, Transform, Load
  - Runs during data refresh
  - Shapes and cleans data before loading
  - Creates tables and columns
  - Better for data transformation

- **DAX:**
  - Calculations on loaded data
  - Runs at query time
  - Creates measures and calculated columns
  - Better for business logic and aggregations

- **Use Power Query for:** Data cleansing, merging sources, unpivoting, filtering rows
- **Use DAX for:** KPIs, time intelligence, complex calculations, measures

**Scoring:**
- **Basic (5/10):** Basic Power Query transformations, UI-based
- **Intermediate (7/10):** Complex transformations, some M code knowledge
- **Advanced (10/10):** Advanced M code, custom functions, understands query folding

---

### Q10: Power BI REST API & Automation (Growth Area)

**Context:** L1 noted this as an area to explore.

**Question:**
"Have you worked with Power BI REST API or Power Automate for automation? If yes, describe a use case. If no, can you think of scenarios where you'd use them?"

**Expected Answer:**

**If Yes (Experienced):**
- Specific use case (e.g., automated report distribution, dataset refresh monitoring)
- API endpoints used (e.g., `/datasets/{datasetId}/refreshes`, `/reports`)
- Authentication method (Service Principal, user credentials)
- Implementation details

**If No (Thinking Through):**

**Power BI REST API Use Cases:**
1. **Automated Dataset Refresh:**
   - Trigger refresh after ETL completion
   - Monitor refresh status
   - Send alerts on failure

2. **Report Distribution:**
   - Export reports to PDF/PowerPoint
   - Email to stakeholders on schedule
   - Customize per recipient (RLS)

3. **Workspace Management:**
   - Automate workspace creation
   - Manage user permissions
   - Deploy reports across environments

4. **Monitoring & Governance:**
   - Track report usage
   - Monitor dataset refresh history
   - Audit user access

**Power Automate Use Cases:**
1. **Scheduled Report Export:**
   - Export report to PDF daily
   - Email to distribution list
   - Save to SharePoint

2. **Alert on Data Threshold:**
   - Monitor KPI values
   - Send alert when threshold exceeded
   - Create ticket in system

3. **Approval Workflows:**
   - Request access to reports
   - Approval routing
   - Automatic provisioning

**Example Flow:**
```
Trigger: Daily at 8 AM
→ Power BI: Refresh Dataset
→ Wait for completion
→ Power BI: Export Report to PDF
→ Email: Send to stakeholders
→ SharePoint: Save copy
```

**Follow-up:** "What authentication methods can you use with Power BI REST API?"

**Expected Answer:**
- **Service Principal:** For automated/unattended scenarios
- **User Credentials:** For user-context operations
- **Azure AD App Registration:** Most common for automation
- Requires appropriate permissions and API access

**Scoring:**
- **Basic (3/10):** No experience, vague ideas
- **Intermediate (6/10):** No hands-on but clear understanding of use cases
- **Advanced (10/10):** Hands-on experience, implemented automation

**Note:** Since this is a growth area per L1, score of 3-6 is acceptable. Look for learning mindset and clear thinking.

---

## SECTION 5: Python Coding Challenge (10 minutes)

### Coding Challenge: Sales Data Analysis & Automation

**Context:** You mentioned automating monthly reporting with Python. Let's validate your pandas skills.

**Question:**
"You receive a CSV file with sales data each month. Write Python code to:

**Given CSV structure:**
```
OrderID,CustomerName,Product,Quantity,Price,OrderDate,Region
1001,Acme Corp,Widget A,10,25.50,2024-11-01,North
1002,Beta Inc,Widget B,5,30.00,2024-11-02,South
1003,Acme Corp,Widget A,15,25.50,2024-11-03,North
...
```

**Tasks:**
1. Load the CSV file
2. Add a `TotalAmount` column (Quantity * Price)
3. Filter for orders in the last 30 days
4. Group by `Region` and calculate:
   - Total Sales
   - Number of Orders
   - Average Order Value
5. Sort by Total Sales (descending)
6. Export to Excel with formatting (bold headers, currency format for amounts)
7. Handle errors (file not found, invalid data)

**You have 10 minutes. It's OK to look up syntax.**"

**Expected Answer:**

```python
import pandas as pd
from datetime import datetime, timedelta
import openpyxl
from openpyxl.styles import Font, numbers

def process_sales_data(input_file, output_file):
    """
    Process monthly sales data and generate summary report.

    Args:
        input_file (str): Path to input CSV file
        output_file (str): Path to output Excel file

    Returns:
        pd.DataFrame: Processed summary data
    """
    try:
        # 1. Load CSV
        df = pd.read_csv(input_file)

        # Validate required columns
        required_cols = ['OrderID', 'CustomerName', 'Product', 'Quantity',
                        'Price', 'OrderDate', 'Region']
        if not all(col in df.columns for col in required_cols):
            raise ValueError(f"Missing required columns. Expected: {required_cols}")

        # 2. Add TotalAmount column
        df['TotalAmount'] = df['Quantity'] * df['Price']

        # 3. Convert OrderDate to datetime and filter last 30 days
        df['OrderDate'] = pd.to_datetime(df['OrderDate'])
        cutoff_date = datetime.now() - timedelta(days=30)
        df_filtered = df[df['OrderDate'] >= cutoff_date].copy()

        if df_filtered.empty:
            print("Warning: No orders in the last 30 days")
            return None

        # 4. Group by Region and calculate metrics
        summary = df_filtered.groupby('Region').agg({
            'TotalAmount': 'sum',
            'OrderID': 'count',
        }).rename(columns={
            'TotalAmount': 'Total Sales',
            'OrderID': 'Number of Orders'
        })

        # Calculate average order value
        summary['Average Order Value'] = summary['Total Sales'] / summary['Number of Orders']

        # 5. Sort by Total Sales descending
        summary = summary.sort_values('Total Sales', ascending=False)

        # Reset index to make Region a column
        summary = summary.reset_index()

        # 6. Export to Excel with formatting
        with pd.ExcelWriter(output_file, engine='openpyxl') as writer:
            summary.to_excel(writer, sheet_name='Sales Summary', index=False)

            # Get workbook and worksheet
            workbook = writer.book
            worksheet = writer.sheets['Sales Summary']

            # Format headers (bold)
            for cell in worksheet[1]:
                cell.font = Font(bold=True)

            # Format currency columns (B, C, D - Total Sales and Avg Order Value)
            for row in worksheet.iter_rows(min_row=2, min_col=2, max_col=4):
                for cell in row:
                    if cell.column in [2, 4]:  # Total Sales and Avg Order Value
                        cell.number_format = '$#,##0.00'

            # Auto-adjust column widths
            for column in worksheet.columns:
                max_length = 0
                column_letter = column[0].column_letter
                for cell in column:
                    try:
                        if len(str(cell.value)) > max_length:
                            max_length = len(cell.value)
                    except:
                        pass
                adjusted_width = (max_length + 2)
                worksheet.column_dimensions[column_letter].width = adjusted_width

        print(f"✅ Report generated successfully: {output_file}")
        print(f"📊 Summary:\n{summary}")

        return summary

    except FileNotFoundError:
        print(f"❌ Error: File '{input_file}' not found")
        return None
    except ValueError as e:
        print(f"❌ Data validation error: {e}")
        return None
    except Exception as e:
        print(f"❌ Unexpected error: {e}")
        return None

# Usage
if __name__ == "__main__":
    result = process_sales_data('sales_data.csv', 'sales_summary.xlsx')
```

**Evaluation Criteria:**

✅ **Must Have (7/10):**
- [ ] Loads CSV correctly
- [ ] Calculates TotalAmount
- [ ] Filters by date (last 30 days)
- [ ] Groups by Region with correct aggregations
- [ ] Sorts by Total Sales
- [ ] Exports to Excel
- [ ] Basic error handling (try-except)

✅ **Good to Have (8-9/10):**
- [ ] Validates data/columns
- [ ] Handles empty results
- [ ] Good code structure (functions, docstrings)
- [ ] Meaningful variable names
- [ ] Comments explaining logic

✅ **Excellent (10/10):**
- [ ] All of the above
- [ ] Excel formatting (bold headers, currency)
- [ ] Auto-adjust column widths
- [ ] Comprehensive error handling
- [ ] User-friendly error messages
- [ ] Clean, production-ready code

**Red Flags:**
- Cannot complete basic tasks (load CSV, group by)
- No error handling
- Hardcoded values everywhere
- Cannot explain code logic
- Messy, unreadable code

**Green Flags:**
- Clean, well-structured code
- Proper error handling
- Good variable names and comments
- Handles edge cases
- Production-ready quality
- Can explain trade-offs

**Scoring:**
- **Basic (5/10):** Completes 50-60% of tasks, basic pandas knowledge
- **Intermediate (7/10):** Completes 70-80% of tasks, good error handling
- **Advanced (10/10):** Completes all tasks, excellent code quality, production-ready

---

## SECTION 6: Behavioral & Scenario-Based (5 minutes)

### Q11: Migration Project - Stakeholder Management

**Question:**
"During the Spotfire/Tableau to Power BI migration, you must have faced resistance from users who were comfortable with the old tools. How did you handle this? Give me a specific example."

**Expected Answer (STAR Method):**

**Situation:**
- Users were comfortable with Spotfire/Tableau
- Concerned about learning new tool
- Some features worked differently in Power BI

**Task:**
- Ensure smooth transition
- Minimize disruption
- Maintain user adoption

**Action:**
- Conducted training sessions (hands-on workshops)
- Created user documentation and quick reference guides
- Set up office hours for questions
- Gathered feedback and addressed concerns
- Highlighted Power BI advantages (better mobile experience, easier sharing, etc.)
- Migrated in phases (pilot group first, then broader rollout)
- Provided side-by-side comparison showing feature parity

**Result:**
- Successful adoption (e.g., "90% user adoption within 2 months")
- Positive feedback from users
- Some users preferred Power BI features
- Reduced support tickets over time

**Follow-up:** "What would you do differently if you had to do this migration again?"

**Expected Answer:**
- More upfront communication
- Longer pilot phase
- Better documentation
- More training sessions
- Gather requirements earlier
- Shows reflection and learning mindset

**Scoring:**
- **Basic (5/10):** Vague answer, no specific examples
- **Intermediate (7/10):** STAR method, specific actions, good outcome
- **Advanced (10/10):** Detailed example, measurable results, lessons learned, shows leadership

---

### Q12: Continuous Learning

**Question:**
"You got PL-300 certified and have worked with multiple BI tools. How do you stay updated with Power BI's rapid evolution? What's a recent feature you learned and applied?"

**Expected Answer:**

**Learning Methods:**
- Microsoft Learn and documentation
- Power BI blog and monthly updates
- Community forums (Power BI Community, Reddit)
- YouTube channels (Guy in a Cube, SQLBI)
- Hands-on experimentation
- Peer learning and knowledge sharing

**Recent Feature Example:**
Could mention any of these (as of 2024):
- **Direct Lake mode** in Fabric
- **New visual types** (e.g., Decomposition Tree improvements)
- **Smart Narrative** enhancements
- **Power BI Goals**
- **Dataflows Gen2** in Fabric
- **Copilot in Power BI** (if available)

**Application:**
- How they learned it
- Where they applied it
- What benefit it provided

**Example Answer:**
"I recently learned about Direct Lake mode in Microsoft Fabric through the Power BI blog. I experimented with it in a test environment and found it combines the best of Import and DirectQuery - fast performance without data duplication. I'm planning to propose it for our next large-scale project where we currently struggle with refresh times."

**Scoring:**
- **Basic (5/10):** Generic answer, no specific examples
- **Intermediate (7/10):** Clear learning methods, recent feature mentioned
- **Advanced (10/10):** Specific recent feature, applied it, shows proactive learning

---

## SCORING RUBRIC

### Technical Skills (60 points)

| Area | Points | Criteria | Candidate Score |
|------|--------|----------|----------------|
| **Power BI & Data Modeling** | 20 | - Migration project depth (5 pts)<br>- Performance optimization (5 pts)<br>- RLS implementation (5 pts)<br>- Data modeling (star schema, SCD, M:M) (5 pts) | ___ / 20 |
| **DAX** | 15 | - Measure creation (5 pts)<br>- Context understanding (5 pts)<br>- Advanced concepts (context transition) (5 pts) | ___ / 15 |
| **SQL** | 10 | - Query writing (4 pts)<br>- Window functions (3 pts)<br>- Optimization knowledge (3 pts) | ___ / 10 |
| **Python** | 10 | - Pandas proficiency (4 pts)<br>- Error handling (3 pts)<br>- Code quality (3 pts) | ___ / 10 |
| **Power Query** | 5 | - M code knowledge (3 pts)<br>- Complex transformations (2 pts) | ___ / 5 |

**Technical Skills Subtotal:** ___ / 60

### Problem-Solving & Architecture (20 points)

| Area | Points | Criteria | Candidate Score |
|------|--------|----------|----------------|
| **Analytical Thinking** | 10 | - Systematic approach to problems<br>- Considers trade-offs<br>- Multiple solution approaches | ___ / 10 |
| **Performance Optimization** | 10 | - Diagnosis methodology<br>- Advanced techniques<br>- Understands storage vs formula engine | ___ / 10 |

**Problem-Solving Subtotal:** ___ / 20

### Communication & Soft Skills (10 points)

| Area | Points | Criteria | Candidate Score |
|------|--------|----------|----------------|
| **Clarity of Explanations** | 5 | - Clear and structured responses<br>- Appropriate technical depth | ___ / 5 |
| **Stakeholder Management** | 5 | - Migration change management<br>- User training and adoption<br>- Business understanding | ___ / 5 |

**Communication Subtotal:** ___ / 10

### Experience & Leadership (10 points)

| Area | Points | Criteria | Candidate Score |
|------|--------|----------|----------------|
| **Project Complexity** | 5 | - Led migration project<br>- Technical depth demonstrated<br>- Measurable outcomes | ___ / 5 |
| **Continuous Learning** | 5 | - PL-300 certification<br>- Stays updated with new features<br>- Learning mindset | ___ / 5 |

**Experience Subtotal:** ___ / 10

---

### **TOTAL SCORE:** ___ / 100

### Score Interpretation:
- **85-100:** 🟢 **Strong Hire** - Exceeds expectations, advanced skills, ready for complex projects
- **70-84:** 🟢 **Hire** - Meets all requirements, solid L2 candidate
- **60-69:** 🟡 **Maybe** - Some gaps, consider for junior L2 or with training plan
- **<60:** 🔴 **No Hire** - Significant gaps in critical areas

---

## RED FLAGS & GREEN FLAGS

### 🚩 Red Flags to Watch For:

**General Red Flags:**
- [ ] Cannot explain migration project details (claimed to "lead" but vague)
- [ ] L1 "Excellent" DAX rating doesn't match L2 performance
- [ ] Cannot write basic DAX time intelligence measures
- [ ] No systematic approach to performance optimization
- [ ] Blames others for project challenges
- [ ] Defensive when asked about technical depth

**Technical Red Flags:**
- [ ] Cannot explain context transition (L1 said "excellent" DAX)
- [ ] Doesn't know storage engine vs formula engine
- [ ] Cannot write SQL window functions
- [ ] Struggles with basic pandas operations
- [ ] No knowledge of incremental refresh or aggregations
- [ ] Cannot explain RLS implementation details

**Prakhar-Specific Red Flags:**
- [ ] Migration project story doesn't hold up under scrutiny
- [ ] 99% data accuracy claim is vague or unsubstantiated
- [ ] Cannot demonstrate "excellent" data modeling from L1
- [ ] Power Query knowledge is superficial (UI-only, no M code)

---

### ✅ Green Flags to Look For:

**General Green Flags:**
- [ ] Detailed migration project explanation with specific challenges
- [ ] Measurable outcomes (user adoption %, performance improvements)
- [ ] Systematic approach to problem-solving
- [ ] Mentions DAX Studio or Performance Analyzer
- [ ] Shows continuous learning (recent features, experimentation)
- [ ] Good stakeholder management during migration

**Technical Green Flags:**
- [ ] Deep DAX knowledge (context transition, optimization)
- [ ] Understands storage engine vs formula engine
- [ ] Advanced SQL (window functions, CTEs, optimization)
- [ ] Clean, production-ready Python code
- [ ] M code knowledge (custom functions, query folding)
- [ ] Knows advanced Power BI features (aggregations, incremental refresh, composite models)

**Prakhar-Specific Green Flags:**
- [ ] L1 "Excellent" ratings confirmed in L2 deep dive
- [ ] Migration project shows leadership and technical depth
- [ ] PL-300 certification knowledge evident in answers
- [ ] Can explain trade-offs and alternatives
- [ ] Proactive about learning (REST API, automation)

---

## L1 TO L2 VALIDATION

### L1 Assessment vs L2 Performance:

| Skill Area | L1 Rating | L2 Validation Questions | L2 Result |
|------------|-----------|------------------------|-----------|
| **Power BI/DAX** | Excellent | Q6, Q7 (DAX measures, context transition) | ___ |
| **Data Modeling** | Excellent | Q5 (Star schema, SCD, M:M) | ___ |
| **SQL/Power Query** | Very Good | Q8, Q9 (SQL query, M code) | ___ |
| **Visualization** | Excellent | Q1 (Migration project) | ___ |
| **RLS** | Good | Q4 (RLS implementation) | ___ |
| **Communication** | Clear, confident | Throughout interview | ___ |

**Consistency Check:**
- [ ] ✅ L1 ratings confirmed - Candidate is as strong as L1 indicated
- [ ] ⚠️ Some gaps - L1 may have overestimated in certain areas
- [ ] ❌ Significant discrepancy - L1 ratings don't match L2 performance

**Notes:**


---

## DECISION MATRIX

### Hiring Decision Framework:

| Criteria | Weight | Assessment | Score |
|----------|--------|------------|-------|
| **Technical Depth** | 40% | DAX, SQL, Power BI, Python | ___ / 40 |
| **Migration Project** | 20% | Leadership, technical challenges, outcomes | ___ / 20 |
| **Problem-Solving** | 20% | Performance optimization, systematic approach | ___ / 20 |
| **Communication** | 10% | Clarity, stakeholder management | ___ / 10 |
| **Learning & Growth** | 10% | PL-300, continuous learning, growth mindset | ___ / 10 |

**Total Weighted Score:** ___ / 100

### Recommendation:

**If 85-100:**
- ✅ **Strong Hire** - Extend offer immediately
- Advanced technical skills confirmed
- Migration project demonstrates leadership
- Ready for complex, client-facing projects
- Consider for senior L2 or L3 track

**If 70-84:**
- ✅ **Hire** - Extend offer
- Solid L2 candidate
- L1 assessment confirmed
- Good fit for BI analyst role
- Provide growth opportunities (REST API, automation)

**If 60-69:**
- ⚠️ **Maybe** - Additional considerations needed
- Some gaps in advanced topics
- L1 may have overestimated certain areas
- Consider if:
  - Strong cultural fit and learning mindset
  - Willing to provide training on gaps
  - Junior L2 role acceptable
- Otherwise, decline

**If <60:**
- ❌ **No Hire** - Decline
- Significant gaps don't match L1 "Excellent" ratings
- Cannot demonstrate claimed migration leadership
- Technical depth insufficient for L2 role

---

## EVALUATION FORM

**Candidate Name:** Prakhar
**Interviewer Name:** _______________
**Date:** 13-November-2025
**Position:** Power BI Data Analyst - L2
**L1 Interviewer:** _______________

### Section Scores:

| Section | Max Points | Score | Notes |
|---------|-----------|-------|-------|
| Q1: Migration Project | 10 | ___ | |
| Q3: Performance Optimization | 10 | ___ | |
| Q4: RLS Implementation | 5 | ___ | |
| Q5: Data Modeling | 5 | ___ | |
| Q6: DAX Measures | 5 | ___ | |
| Q7: Context Transition | 10 | ___ | |
| Q8: SQL Query | 10 | ___ | |
| Q9: Power Query | 5 | ___ | |
| Q10: REST API/Automation | 5 | ___ | |
| Q11: Python Coding | 10 | ___ | |
| Q12: Behavioral | 10 | ___ | |
| Communication | 10 | ___ | |
| Problem-Solving | 5 | ___ | |

**TOTAL:** ___ / 100

---

### Detailed Feedback:

**Strengths:**
1.
2.
3.

**Areas for Improvement:**
1.
2.
3.

**Specific Examples (Good or Concerning):**
-
-
-

**L1 to L2 Consistency:**
- Power BI/DAX: [ ] Confirmed [ ] Overestimated [ ] Underestimated
- Data Modeling: [ ] Confirmed [ ] Overestimated [ ] Underestimated
- SQL/Power Query: [ ] Confirmed [ ] Overestimated [ ] Underestimated
- Communication: [ ] Confirmed [ ] Overestimated [ ] Underestimated

**Technical Depth Assessment:**
- Power BI: [ ] Beginner [ ] Intermediate [ ] Advanced [ ] Expert
- DAX: [ ] Beginner [ ] Intermediate [ ] Advanced [ ] Expert
- SQL: [ ] Beginner [ ] Intermediate [ ] Advanced [ ] Expert
- Python: [ ] Beginner [ ] Intermediate [ ] Advanced [ ] Expert
- Power Query: [ ] Beginner [ ] Intermediate [ ] Advanced [ ] Expert

**Cultural Fit:**
- [ ] Excellent - Would thrive in our environment
- [ ] Good - Would fit well
- [ ] Neutral - Could work
- [ ] Poor - Not a good fit

**Learning Mindset:**
- [ ] Excellent - Proactive learner, seeks growth (PL-300, exploring new features)
- [ ] Good - Open to learning
- [ ] Neutral - Learns when needed
- [ ] Poor - Resistant to feedback/learning

---

### Final Recommendation:

- [ ] **Strong Hire** - Extend offer immediately, consider senior L2/L3 track
- [ ] **Hire** - Extend offer, solid L2 candidate
- [ ] **Maybe** - Additional interview or specific role consideration
- [ ] **No Hire** - Decline, gaps too significant

**Justification:**


**Suggested Compensation Range (if hire):** _______________

**Start Date Preference:** _______________

**Growth Areas to Focus On (if hired):**
- [ ] Power BI REST API and automation
- [ ] Enterprise-scale performance tuning
- [ ] Advanced DAX patterns
- [ ] Other: _______________

**Additional Notes:**


---

**Interviewer Signature:** _______________
**Date:** _______________

---

## INTERVIEWER PREPARATION CHECKLIST

### Before the Interview:
- [x] Reviewed Prakhar's resume
- [x] Reviewed L1 interview feedback
- [x] Identified migration project as key discussion point
- [x] Prepared performance optimization scenario
- [x] Prepared Python coding challenge
- [x] Set up screen sharing for coding section
- [x] Have code editor ready (VS Code, Jupyter, or online IDE)
- [x] Printed/opened this interview plan
- [x] Reviewed L1 "Excellent" ratings to validate

### During the Interview:
- [ ] Take detailed notes on migration project
- [ ] Validate L1 "Excellent" DAX rating with Q7
- [ ] Probe performance optimization depth (L1 gap area)
- [ ] Assess REST API knowledge (L1 growth area)
- [ ] Watch for consistency with resume claims
- [ ] Note specific examples and metrics provided
- [ ] Mark red flags and green flags

### After the Interview:
- [ ] Complete scoring rubric within 1 hour
- [ ] Fill out evaluation form
- [ ] Compare L2 results with L1 assessment
- [ ] Document specific examples (good and bad)
- [ ] Make hiring recommendation
- [ ] Share feedback with hiring team
- [ ] Follow up on any questions or concerns

---

## NOTES SECTION

**Use this space for real-time notes during the interview:**

**Migration Project (Q1):**


**Performance Optimization (Q3):**


**DAX Deep Dive (Q6, Q7):**


**SQL & Power Query (Q8, Q9):**


**Python Coding (Q11):**


**Behavioral (Q12):**


**Overall Impression:**


**L1 vs L2 Consistency:**


**Questions to Follow Up On:**


---

**END OF INTERVIEW PLAN**

---

## APPENDIX: L1 Interview Feedback (Full)

**Summary:**
Prakhar has strong command over Power BI end-to-end — from data modeling, DAX, and Power Query to visualization and deployment. Demonstrates clear practical experience, business understanding, and good communication skills.

**Technical Skills:**
- Power BI / DAX: Excellent – strong grasp of CALCULATE, SUMX, filter context, and KPI creation.
- Data Modeling: Excellent – well-structured star schema approach and relationship handling.
- SQL / Power Query: Very Good – proficient in joins, transformations, and query optimization.
- Visualization: Excellent – clean, interactive dashboards with strong storytelling ability.
- Python (optional integration): Good – understands use for data preprocessing and analytics.
- Security / RLS: Good – knows both static and dynamic RLS setup.

**Soft Skills:**
- Communicates clearly, confident, and analytical.
- Understands business KPIs and translates requirements effectively.

**Areas to Improve:**
- Explore Power BI REST API and automation (Power Automate).
- More exposure to large-scale performance tuning (enterprise datasets).

**Final Recommendation:**
Selected – technically strong, confident communicator, and ready for client-facing BI work.

---

**L2 Interview Focus Based on L1:**
1. ✅ Validate "Excellent" DAX rating with advanced questions
2. ✅ Validate "Excellent" data modeling with SCD, M:M scenarios
3. ✅ Deep dive into migration project (leadership, technical depth)
4. ✅ Probe performance optimization (identified gap area)
5. ✅ Explore REST API/automation knowledge (growth area)
6. ✅ Confirm communication and business understanding

