# AI INSTRUCTIONS: Power BI Data Analyst Interview Plan Generator

## PURPOSE
This template is used to generate customized interview plans for Power BI Data Analyst candidates based on:
1. Candidate's resume/profile
2. Job requirements
3. L1 interview feedback (if available)
4. Experience level and focus areas

---

## HOW TO USE THIS TEMPLATE

### STEP 1: Gather Input Information
When a user requests a new interview plan, collect:

**Required Information:**
- [ ] Candidate name
- [ ] Interview date
- [ ] Years of experience
- [ ] Resume/CV or key project descriptions
- [ ] Position level (L1, L2, L3, etc.)
- [ ] Key technical skills from resume (Power BI, DAX, SQL, Python, etc.)

**Optional Information:**
- [ ] L1 interview feedback/notes
- [ ] Specific areas to focus on or avoid
- [ ] Special requirements or concerns
- [ ] Team/role-specific needs

### STEP 2: Analyze Candidate Profile
Extract from resume/profile:
1. **Major Projects:** List 2-3 most significant projects with:
   - Project name
   - Technologies used
   - Scale (data volume, users, complexity)
   - Measurable impact/achievements

2. **Technical Skills:** Identify proficiency in:
   - Power BI (dashboards, data modeling, RLS, performance optimization)
   - DAX (basic, intermediate, advanced)
   - SQL (query complexity, optimization knowledge)
   - Python (pandas, automation, scripting)
   - Cloud platforms (Azure, Fabric, AWS, etc.)

3. **Domain Experience:** Note industry/domain knowledge

4. **Gaps or Red Flags:** Identify areas that need deeper probing

### STEP 3: Customize the Interview Plan
Use the template structure below and customize:

**File Naming Convention:**
`[Candidate Name] - Data Analyst - Power BI - [DD-Month-YYYY] - [Level].md`
Example: `John Smith - Data Analyst - Power BI - 15-November-2025 - L2.md`

**Customization Points:**

1. **Executive Summary:**
   - Update experience level and targeting
   - List candidate's actual projects in "Candidate Background Highlights"
   - Adjust focus areas based on resume

2. **Question Selection:**
   - Choose questions that align with candidate's experience
   - For Q1 (Main Project Deep Dive): Use their most impressive project
   - For coding challenges: Base on their actual automation/Python work
   - Add follow-ups specific to their resume claims

3. **Expected Answers:**
   - Tailor to their specific projects and technologies
   - Reference their actual work in examples
   - Adjust difficulty based on experience level

4. **Scoring Emphasis:**
   - Weight areas based on job requirements
   - Flag critical skills for the role
   - Note any must-have vs nice-to-have skills

### STEP 4: Incorporate L1 Feedback (if available)
If L1 interview notes are provided:

**Areas to Probe Deeper:**
- If L1 noted "claims X but unclear" → Add specific technical questions on X
- If L1 noted "strong in Y" → Add advanced questions on Y to confirm
- If L1 noted "weak in Z" → Include questions to assess if it's a deal-breaker

**Red Flags from L1:**
- Add questions to validate or disprove concerns
- Include scenario-based questions for soft skill concerns
- Add coding challenges if technical ability is questioned

**Green Flags from L1:**
- Confirm strengths with deeper technical questions
- Add questions to assess leadership/mentoring potential
- Include questions about future growth areas

### STEP 5: Generate Coding Challenges
Create 2 coding challenges based on:
1. **Their Resume:** Use similar problems to what they claim to have solved
2. **Job Requirements:** Test skills needed for the role
3. **Difficulty Level:** Match to their experience (1-2 years = intermediate, 3+ = advanced)

**Challenge 1 (10 min):** Data manipulation with pandas
- Based on their domain (billing, sales, calls, etc.)
- Include: filtering, grouping, aggregation, export

**Challenge 2 (5 min):** Error handling and validation
- Function writing with proper structure
- Data validation logic
- Error handling

---

## TEMPLATE STRUCTURE TO FOLLOW

```markdown
# Power BI Data Analyst Interview Plan
**Date:** [Actual Date]
**Duration:** 60 minutes
**Experience Level:** [X.X years] (targeting [X+] years)
**Focus Areas:** [List actual skills from resume]

---

## 📊 EXECUTIVE SUMMARY
[Customize based on candidate]

### 🎓 Candidate Background Highlights:
- [Actual Project 1 with metrics]
- [Actual Project 2 with metrics]
- [Actual Project 3 with metrics]
- [Key achievements with numbers]
- [Relevant certifications]

---

## SECTION 1: Introduction & Background (5 minutes)
[Standard questions]

---

## SECTION 2: Power BI & Data Modeling (20 minutes)

### Q1: [Actual Project Name] Deep Dive
**Question:** "You mentioned building [actual project]. Walk me through:
- [Specific aspect from resume]
- [Technical challenge they claim to have solved]
- [Performance/scale mentioned in resume]"

**Expected Answer:**
- [What you expect based on their resume claims]
- [Technical details they should know]
- [Metrics they mentioned]

**Follow-up:** "[Probe specific claim or gap]"

[Continue with Q2-Q4 customized to their experience]

---

## SECTION 3: DAX & Calculations (10 minutes)
[Customize DAX questions based on complexity they claim]

---

## SECTION 4: SQL & Data Integration (10 minutes)
[Customize SQL questions based on their database experience]

---

## SECTION 5: Python Automation - CODING (15 minutes)

### Coding Challenge 1: [Based on Their Domain] (10 minutes)
**Question:** "You mentioned [specific automation from resume]. Here's a similar scenario:
[Create challenge based on their actual work]"

### Coding Challenge 2: [Validation/Error Handling] (5 minutes)
[Create challenge relevant to their role]

---

## SECTION 6: Behavioral & Scenario-Based (5 minutes)
[Select behavioral questions based on L1 feedback or role requirements]

---

## SCORING RUBRIC
[Adjust weights based on role requirements]

---

## RED FLAGS TO WATCH FOR
[Add specific red flags based on resume review or L1 feedback]

---

## GREEN FLAGS TO LOOK FOR
[Add specific green flags based on role needs]

---
```

---

## QUALITY CHECKLIST

Before finalizing the interview plan, verify:
- [ ] All placeholders replaced with actual candidate information
- [ ] Questions reference candidate's actual projects
- [ ] Coding challenges are relevant to their domain
- [ ] Expected answers match their experience level
- [ ] L1 feedback incorporated (if provided)
- [ ] File named correctly
- [ ] Scoring rubric weights match role requirements
- [ ] Red flags and areas to probe are clearly identified

---

## EXAMPLE USAGE

**User Request:**
"Create interview plan for Sarah Johnson, 3.5 years experience, interview on Nov 20, 2025, L2 position"

**AI Response:**
1. Request resume or key project details
2. Request L1 feedback if available
3. Analyze provided information
4. Generate customized plan using this template
5. Save as: `Sarah Johnson - Data Analyst - Power BI - 20-November-2025 - L2.md`

---

## NOTES
- Always ask for resume/project details before generating
- If L1 feedback mentions concerns, add 2-3 questions to validate
- Adjust difficulty: L1 (0-2 yrs), L2 (2-4 yrs), L3 (4+ yrs)
- Include at least one question that challenges them beyond their resume
- Make coding challenges practical and relevant to actual job duties

