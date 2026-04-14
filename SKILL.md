---
name: harvard-cv-formatter
description: "Transform any resume/CV into Harvard Business School format optimized for data analytics, analytics engineering, and data engineering roles. Use this skill whenever someone asks to: format their CV/resume in Harvard style, optimize their resume for data roles, convert their CV to a professional Harvard format, adapt their experience for analytics/engineering positions, or create a data-focused resume. Also trigger when users upload a CV/resume file and mention 'Harvard format', 'data analytics', 'analytics engineer', 'data engineer', or want to highlight technical/analytical skills. This skill handles the complete end-to-end transformation including reading the source CV, restructuring content, optimizing descriptions with quantifiable metrics and technical terminology, and generating a professionally formatted .docx file."
compatibility: "Requires docx npm package (npm install -g docx), pandoc for reading source CVs"
---

# Harvard CV Formatter for Data Professionals

## Overview

This skill transforms any resume/CV into the Harvard Business School format, specifically optimized for data analytics, analytics engineering, and data engineering roles. It maintains truthfulness while reframing experience to emphasize technical skills, quantifiable impact, and data-driven decision making.

## When to Use This Skill

Trigger this skill when the user:
- Asks to format their CV in "Harvard format" or "Harvard style"
- Wants to optimize their resume for data analytics, analytics engineer, or data engineering positions
- Uploads a CV and mentions wanting it professionally formatted
- Requests their experience be reframed to highlight data/analytical capabilities
- Asks for a resume that emphasizes technical competencies and metrics

## Workflow

### Step 1: Read the Source CV

First, determine the format of the uploaded CV and read it appropriately:

**For .docx files:**
```bash
pandoc /mnt/user-data/uploads/[filename].docx -t markdown
```

**For .pdf files:**
```bash
pdftotext /mnt/user-data/uploads/[filename].pdf -
```

**For other formats:** Use the appropriate tool from `/mnt/skills/public/file-reading/SKILL.md`

Extract all key information:
- Personal information (name, contact details, location)
- Languages and proficiency levels
- Education (degrees, institutions, dates, relevant coursework)
- Technical skills and tools
- Work experience (companies, titles, dates, responsibilities, achievements)
- Projects and certifications
- Any other relevant sections

### Step 2: Analyze and Plan Optimization

Before writing code, identify opportunities to optimize for data roles:

1. **Technical Skills Audit:**
   - Identify existing technical skills (programming languages, tools, platforms)
   - Note implied technical skills from job descriptions (e.g., "analyzed data" → SQL/Excel/Python)
   - Plan how to expand the technical competencies section

2. **Experience Analysis:**
   - For each role, identify quantifiable achievements
   - Look for data-related tasks that can be emphasized
   - Identify technical tools/processes that were likely used but not mentioned
   - Plan how to reframe responsibilities in technical terms

3. **Impact Quantification:**
   - Find or estimate metrics (percentages, time saved, volume processed, accuracy improvements)
   - Plan to add technical context (dataset sizes, processing frequency, automation benefits)

### Step 3: Generate the Harvard-Format CV

Create a Node.js script using the `docx` library. Follow this exact structure:

#### Required Imports and Setup

```javascript
const { Document, Packer, Paragraph, TextRun, Table, TableRow, TableCell, 
        AlignmentType, WidthType, ShadingType, BorderStyle, 
        ExternalHyperlink } = require('docx');
const fs = require('fs');

const border = { style: BorderStyle.SINGLE, size: 1, color: "CCCCCC" };
const borders = { top: border, bottom: border, left: border, right: border };
```

#### Document Structure (Mandatory Sections in Order)

1. **Header Section**
   - Full name in bold, size 22
   - Contact line with pipes: `Tel: [phone] | e-mail: [email] | LinkedIn: [link]`
   - Use `ExternalHyperlink` for LinkedIn/GitHub with underline styling
   - Spacing: after: 240

2. **LANGUAGES Section**
   - Section header: bold, size 22, spacing before: 240, after: 120
   - Use a 2-column table for languages
   - Format: "- [Language] | [Proficiency Level]"
   - Include links to certifications if available

3. **EDUCATION Section**
   - Section header: bold, size 22, spacing before: 240, after: 120
   - For each degree (reverse chronological):
     - Degree title in bold
     - Institution in bold with dates in format: `| (Finished: [date])` or `| (In Progress)`
     - "Relevant courses:" followed by comma-separated list
     - Spacing after: 180 between degrees

4. **CORE TECHNICAL COMPETENCIES Section**
   - Section header: bold, size 22, spacing before: 240, after: 120
   - Use a 3-column table
   - Group technologies logically:
     - Column 1: Programming languages and core data tools
     - Column 2: BI/Visualization tools and platforms
     - Column 3: Cloud platforms, specialized tools, methodologies
   - Each cell has margins: `{ top: 80, bottom: 80, left: 120, right: 120 }`

5. **WORK EXPERIENCE Section**
   - Section header: bold, size 22, spacing before: 240, after: 120
   - For each position (reverse chronological):
     - Company line: `**[Company] | [Location] ([Start Date] -- [End Date/Present])**` (bold, italics)
     - Title line: `**[Job Title]**` (bold, italics)
     - If applicable, client/marketplace line: `*[Context]*` (italics, underline)
     - Bullet points with spacing after: 120
     - Section spacing after last bullet: 240

6. **KEY PROJECTS/ANALYTICS PROJECTS Section** (if applicable)
   - Section header: bold, size 22, spacing before: 240, after: 120
   - Format: `- **[Project Name]:** [Description with technical details and impact]`
   - Spacing after: 120

7. **CERTIFICATIONS/PROFESSIONAL DEVELOPMENT Section**
   - Section header: bold, size 22, spacing before: 240, after: 120
   - Format: `- [Certification Name] ([Issuer], [Year])`
   - Or: `- [Description of relevant training/development]`
   - Spacing after: 60

#### Page Settings

Always use US Letter with 1-inch margins:

```javascript
sections: [{
  properties: {
    page: {
      size: {
        width: 12240,   // US Letter width in DXA
        height: 15840   // US Letter height in DXA
      },
      margin: { top: 1440, right: 1440, bottom: 1440, left: 1440 }
    }
  },
  children: [/* content */]
}]
```

#### Table Configuration

**CRITICAL:** All tables must set both table width AND cell widths:

```javascript
// 2-column table (for languages)
new Table({
  width: { size: 9360, type: WidthType.DXA },
  columnWidths: [4680, 4680],  // Must sum to table width
  rows: [/* rows */]
})

// 3-column table (for technical skills)
new Table({
  width: { size: 9360, type: WidthType.DXA },
  columnWidths: [3120, 3120, 3120],  // Must sum to table width
  rows: [/* rows */]
})

// Cell configuration
new TableCell({
  borders,
  width: { size: [column-width], type: WidthType.DXA },
  margins: { top: 80, bottom: 80, left: 120, right: 120 },
  children: [new Paragraph({ children: [new TextRun("Content")] })]
})
```

### Step 4: Optimize Descriptions for Data Roles

When transforming work experience descriptions, follow these principles:

#### A. Add Technical Context

Transform generic descriptions into technical ones:

**Before:** "Managed customer support cases"
**After:** "Extracted and analyzed customer interaction data from internal databases using SQL and Excel to design predictive models identifying high-callback-probability cases"

**Before:** "Improved team efficiency"
**After:** "Engineered automated reporting systems using Python scripts and HTML/Outlook integration, transforming 2-hour manual productivity audits into 2-minute automated deliveries"

#### B. Quantify Everything

Add metrics wherever possible:
- Percentages (reduced by X%, increased by Y%)
- Volume (processed N records, analyzed M customers)
- Time savings (from X hours to Y minutes)
- Accuracy/precision (achieved Z% accuracy)
- Scale (across N countries, M teams, K systems)

#### C. Emphasize Data Pipeline Work

Highlight any work involving:
- Data extraction, transformation, loading (ETL/ELT)
- Data validation and quality checks
- Database queries and optimization
- Automated reporting
- Dashboard creation
- Data modeling and schema design

#### D. Add Technology Stack Details

When the user likely used specific technologies but didn't mention them, add them explicitly:

**Generic:** "Created reports"
**Specific:** "Developed interactive Power BI dashboards synthesizing compliance KPIs, trend analysis, and risk forecasting"

**Generic:** "Analyzed data"
**Specific:** "Architected data pipelines processing 10,000+ records daily using Python (Pandas, NumPy) and PySpark"

#### E. Use Data Engineering Terminology

Incorporate appropriate technical terms:
- Data pipelines, ETL processes, data warehousing
- Schema design, data modeling, dimensional models
- Data quality, validation, reconciliation
- Predictive modeling, classification, regression
- A/B testing, statistical analysis, hypothesis testing
- Real-time processing, batch processing, streaming
- Cloud platforms, distributed computing
- Version control, CI/CD, automation

#### F. Reframe Job Titles (Subtly)

Add technical emphasis to job titles without changing them:

**Original:** "Senior Compliance Associate"
**Optimized:** "Senior Compliance Associate -- Data Analytics & Automation"

**Original:** "Sales Support Specialist"
**Optimized:** "Sales Support Specialist -- Fraud Analytics & Data Standardization"

### Step 5: Write and Execute the Script

Save the complete Node.js script to `/home/claude/create_harvard_cv.js` and execute:

```bash
cd /home/claude && node create_harvard_cv.js
```

The script should save the output to `/mnt/user-data/outputs/[Name]_Resume_Harvard.docx`

### Step 6: Validate the Document

Always validate the generated document:

```bash
python /mnt/skills/public/docx/scripts/office/validate.py /mnt/user-data/outputs/[Name]_Resume_Harvard.docx
```

If validation fails, check:
- All table widths sum correctly
- All cells have width property set
- No unicode bullet characters (use numbering config instead)
- All hyperlinks are properly formatted

### Step 7: Present to User

Use the `present_files` tool to share the document:

```javascript
present_files({ filepaths: ["/mnt/user-data/outputs/[Name]_Resume_Harvard.docx"] })
```

Provide a brief summary highlighting:
- Main structural changes applied
- Key optimizations made (e.g., "Added quantifiable metrics to 8 bullet points")
- Technical competencies expanded
- Any assumptions made that the user should verify

## Key Optimization Strategies

### For Analytics Roles

Emphasize:
- SQL and database querying
- Data visualization (Power BI, Tableau, etc.)
- Statistical analysis and A/B testing
- Dashboard creation and BI tools
- Stakeholder communication
- KPI tracking and metrics

### For Analytics Engineering Roles

Emphasize:
- Data pipeline development (ETL/ELT)
- Data modeling and schema design
- SQL optimization and query performance
- dbt, Airflow, or similar tools
- Data quality and testing
- Version control and documentation
- Collaboration with data engineers and analysts

### For Data Engineering Roles

Emphasize:
- Data architecture and infrastructure
- Distributed computing (Spark, Hadoop)
- Cloud platforms (AWS, Azure, GCP)
- Real-time and batch processing
- Data warehousing solutions
- API development and integration
- System scalability and performance
- Orchestration and scheduling

## Common Pitfalls to Avoid

1. **Never fabricate experience** - Only optimize what exists; don't invent tools or projects
2. **Don't over-technify non-technical roles** - Keep it credible
3. **Avoid buzzword soup** - Use technical terms naturally, not gratuitously
4. **Don't ignore non-technical strengths** - Leadership, communication, and domain expertise matter
5. **Keep it readable** - Don't sacrifice clarity for technical density
6. **Verify dates and names** - Copy them exactly as provided
7. **Preserve the user's voice** - Optimize, don't completely rewrite

## Final Checklist

Before presenting the CV, verify:

- [ ] All personal information is accurate
- [ ] Dates are in correct format: (Month Year -- Month Year) or (Present)
- [ ] At least 3 quantifiable metrics added to work experience
- [ ] Technical competencies section has 10+ items
- [ ] Job descriptions use technical terminology appropriately
- [ ] All hyperlinks are functional
- [ ] Document validates without errors
- [ ] US Letter page size (12240 x 15840 DXA)
- [ ] Consistent spacing throughout
- [ ] No unicode bullets (use proper numbering config)
- [ ] File saved to /mnt/user-data/outputs/

## Example Transformations

### Generic → Data-Optimized

**Generic:**
"Handled customer complaints and resolved issues efficiently."

**Data-Optimized:**
"Conducted root cause analysis on customer escalation patterns by querying CRM databases and performing statistical analysis, identifying systemic issues that led to a 15% reduction in repeat contacts through process improvements and automated follow-up workflows."

**Generic:**
"Created weekly reports for management."

**Data-Optimized:**
"Architected automated Power BI dashboards integrating data from 5 operational systems, providing real-time visibility into team performance metrics and reducing manual reporting overhead from 6 hours to 15 minutes weekly while enabling data-driven resource allocation decisions."

**Generic:**
"Improved team productivity."

**Data-Optimized:**
"Developed Python-based automation scripts to streamline data validation processes, reducing average task completion time by 62% (from 120 to 45 minutes) and improving data quality through systematic error detection and validation checks."

---

Remember: The goal is to authentically represent the candidate's experience while maximizing the visibility of their data and analytical capabilities. Every optimization should be defensible in an interview.
