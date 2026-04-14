---
name: harvard-cv-formatter
description: "Transform any resume/CV into Harvard Business School format optimized for data analytics, analytics engineering, and data engineering roles. Trigger when user: uploads a CV, mentions 'Harvard format', 'data analytics CV', 'optimize resume for data roles', or wants to improve their resume. Handles complete workflow: read source CV, restructure content, optimize descriptions with technical terminology and metrics, generate professional .docx file."
compatibility: "Requires: docx (npm install -g docx), pandoc"
---

# Harvard CV Formatter for Data Professionals

## Overview

This skill transforms any resume/CV into Harvard Business School format, optimized for data roles. It maintains truthfulness while reframing experience to emphasize technical skills, quantifiable impact, and data-driven work.

## Critical: Complete Code Template

Claude MUST follow this EXACT code structure. This is a complete, working example that generates proper Harvard format CVs.

### Complete Node.js Script Template

```javascript
const { Document, Packer, Paragraph, TextRun, Table, TableRow, TableCell, 
        AlignmentType, WidthType, ShadingType, BorderStyle, 
        ExternalHyperlink } = require('docx');
const fs = require('fs');

// Define borders - use for ALL tables
const border = { style: BorderStyle.SINGLE, size: 1, color: "CCCCCC" };
const borders = { top: border, bottom: border, left: border, right: border };

const doc = new Document({
  styles: {
    default: { 
      document: { 
        run: { font: "Calibri", size: 22 } // 11pt default
      } 
    },
  },
  sections: [{
    properties: {
      page: {
        size: {
          width: 12240,   // US Letter width in DXA
          height: 15840   // US Letter height in DXA
        },
        margin: { top: 1440, right: 1440, bottom: 1440, left: 1440 } // 1 inch margins
      }
    },
    children: [
      // ===== HEADER SECTION =====
      new Paragraph({
        children: [
          new TextRun({
            text: "Full Name Here",
            bold: true,
            size: 22
          })
        ],
        spacing: { after: 120 }
      }),
      
      // ===== CONTACT LINE =====
      new Paragraph({
        children: [
          new TextRun({ text: "Tel: (+XXX) XXXX-XXXX | e-mail: email@example.com | LinkedIn: " }),
          new ExternalHyperlink({
            children: [
              new TextRun({
                text: "LinkedIn Profile",
                style: "Hyperlink",
                underline: {}
              })
            ],
            link: "https://linkedin.com/in/profile"
          })
        ],
        spacing: { after: 240 }
      }),
      
      // ===== LANGUAGES SECTION =====
      new Paragraph({
        children: [
          new TextRun({
            text: "LANGUAGES",
            bold: true,
            size: 22
          })
        ],
        spacing: { before: 240, after: 120 }
      }),
      
      // Languages table - 2 columns
      new Table({
        width: { size: 9360, type: WidthType.DXA },
        columnWidths: [4680, 4680],
        rows: [
          new TableRow({
            children: [
              new TableCell({
                borders,
                width: { size: 4680, type: WidthType.DXA },
                margins: { top: 80, bottom: 80, left: 120, right: 120 },
                children: [
                  new Paragraph({
                    children: [
                      new TextRun({ text: "- English | Advanced (C1)" })
                    ]
                  })
                ]
              }),
              new TableCell({
                borders,
                width: { size: 4680, type: WidthType.DXA },
                margins: { top: 80, bottom: 80, left: 120, right: 120 },
                children: [
                  new Paragraph({
                    children: [
                      new TextRun({ text: "- Spanish | Native" })
                    ]
                  })
                ]
              })
            ]
          })
        ]
      }),
      
      // ===== EDUCATION SECTION =====
      new Paragraph({
        children: [
          new TextRun({
            text: "EDUCATION",
            bold: true,
            size: 22
          })
        ],
        spacing: { before: 240, after: 120 }
      }),
      
      new Paragraph({
        children: [
          new TextRun({
            text: "Bachelor's Degree | Major Name",
            bold: true
          })
        ],
        spacing: { after: 60 }
      }),
      
      new Paragraph({
        children: [
          new TextRun({
            text: "University Name | (Finished: Month Year)",
            bold: true
          })
        ],
        spacing: { after: 60 }
      }),
      
      new Paragraph({
        children: [
          new TextRun({
            text: "Relevant courses: Course 1, Course 2, Course 3, Course 4."
          })
        ],
        spacing: { after: 180 }
      }),
      
      // ===== CORE TECHNICAL COMPETENCIES =====
      new Paragraph({
        children: [
          new TextRun({
            text: "CORE TECHNICAL COMPETENCIES",
            bold: true,
            size: 22
          })
        ],
        spacing: { before: 240, after: 120 }
      }),
      
      // Tech competencies table - 3 columns
      new Table({
        width: { size: 9360, type: WidthType.DXA },
        columnWidths: [3120, 3120, 3120],
        rows: [
          new TableRow({
            children: [
              new TableCell({
                borders,
                width: { size: 3120, type: WidthType.DXA },
                margins: { top: 80, bottom: 80, left: 120, right: 120 },
                children: [
                  new Paragraph({
                    children: [
                      new TextRun({ text: "Python (Pandas, NumPy)" })
                    ]
                  })
                ]
              }),
              new TableCell({
                borders,
                width: { size: 3120, type: WidthType.DXA },
                margins: { top: 80, bottom: 80, left: 120, right: 120 },
                children: [
                  new Paragraph({
                    children: [
                      new TextRun({ text: "Power BI / Tableau" })
                    ]
                  })
                ]
              }),
              new TableCell({
                borders,
                width: { size: 3120, type: WidthType.DXA },
                margins: { top: 80, bottom: 80, left: 120, right: 120 },
                children: [
                  new Paragraph({
                    children: [
                      new TextRun({ text: "AWS / Azure Cloud Platforms" })
                    ]
                  })
                ]
              })
            ]
          }),
          new TableRow({
            children: [
              new TableCell({
                borders,
                width: { size: 3120, type: WidthType.DXA },
                margins: { top: 80, bottom: 80, left: 120, right: 120 },
                children: [
                  new Paragraph({
                    children: [
                      new TextRun({ text: "SQL (PostgreSQL, MySQL)" })
                    ]
                  })
                ]
              }),
              new TableCell({
                borders,
                width: { size: 3120, type: WidthType.DXA },
                margins: { top: 80, bottom: 80, left: 120, right: 120 },
                children: [
                  new Paragraph({
                    children: [
                      new TextRun({ text: "Excel (Advanced Analytics)" })
                    ]
                  })
                ]
              }),
              new TableCell({
                borders,
                width: { size: 3120, type: WidthType.DXA },
                margins: { top: 80, bottom: 80, left: 120, right: 120 },
                children: [
                  new Paragraph({
                    children: [
                      new TextRun({ text: "Data Pipelines / ETL" })
                    ]
                  })
                ]
              })
            ]
          })
        ]
      }),
      
      // ===== WORK EXPERIENCE =====
      new Paragraph({
        children: [
          new TextRun({
            text: "WORK EXPERIENCE",
            bold: true,
            size: 22
          })
        ],
        spacing: { before: 240, after: 120 }
      }),
      
      // Company line
      new Paragraph({
        children: [
          new TextRun({
            text: "Company Name | City, Country (Month Year -- Month Year)",
            bold: true,
            italics: true
          })
        ],
        spacing: { after: 60 }
      }),
      
      // Job title line
      new Paragraph({
        children: [
          new TextRun({
            text: "Job Title -- Technical Emphasis",
            bold: true,
            italics: true
          })
        ],
        spacing: { after: 120 }
      }),
      
      // Bullet point 1 - NOTE: alignment is JUSTIFIED
      new Paragraph({
        alignment: AlignmentType.JUSTIFIED,
        children: [
          new TextRun({
            text: "- Architected and maintained end-to-end data pipelines processing 10,000+ records daily using Python (Pandas, NumPy) and PySpark, enabling automated monitoring and reducing manual review time by 45% while ensuring data quality across operations."
          })
        ],
        spacing: { after: 120 }
      }),
      
      // Bullet point 2
      new Paragraph({
        alignment: AlignmentType.JUSTIFIED,
        children: [
          new TextRun({
            text: "- Developed predictive classification models leveraging Machine Learning algorithms and RegEx pattern matching to identify high-risk records, achieving 92% precision and preventing issues before reaching customers."
          })
        ],
        spacing: { after: 120 }
      }),
      
      // Last bullet has spacing of 240
      new Paragraph({
        alignment: AlignmentType.JUSTIFIED,
        children: [
          new TextRun({
            text: "- Designed interactive Power BI dashboards synthesizing KPIs, trend analysis, and forecasting that informed executive decision-making and resource allocation across international operations."
          })
        ],
        spacing: { after: 240 }
      }),
      
      // ===== CERTIFICATIONS =====
      new Paragraph({
        children: [
          new TextRun({
            text: "CERTIFICATIONS & PROFESSIONAL DEVELOPMENT",
            bold: true,
            size: 22
          })
        ],
        spacing: { before: 240, after: 120 }
      }),
      
      new Paragraph({
        children: [
          new TextRun({
            text: "- Certification Name (Issuing Organization, Year)"
          })
        ],
        spacing: { after: 60 }
      }),
      
      new Paragraph({
        children: [
          new TextRun({
            text: "- Another Certification (Organization, Year)"
          })
        ],
        spacing: { after: 60 }
      })
    ]
  }]
});

// Generate the document
Packer.toBuffer(doc).then(buffer => {
  fs.writeFileSync("/mnt/user-data/outputs/Name_Resume_Harvard.docx", buffer);
  console.log("Document created successfully!");
});
```

## Critical Formatting Rules

### 1. Table Configuration (MUST BE EXACT)

**Languages table (2 columns):**
```javascript
new Table({
  width: { size: 9360, type: WidthType.DXA },
  columnWidths: [4680, 4680],  // MUST sum to 9360
  rows: [...]
})
```

**Technical competencies table (3 columns):**
```javascript
new Table({
  width: { size: 9360, type: WidthType.DXA },
  columnWidths: [3120, 3120, 3120],  // MUST sum to 9360
  rows: [...]
})
```

**Every TableCell MUST have:**
```javascript
new TableCell({
  borders,  // Already defined at top
  width: { size: [column-width], type: WidthType.DXA },
  margins: { top: 80, bottom: 80, left: 120, right: 120 },
  children: [new Paragraph({ children: [new TextRun("text")] })]
})
```

### 2. Text Alignment Rules

**ONLY use JUSTIFIED alignment for work experience bullet points:**
```javascript
// ✅ CORRECT - Work experience bullets
new Paragraph({
  alignment: AlignmentType.JUSTIFIED,
  children: [new TextRun({ text: "- Bullet point text..." })]
})

// ❌ WRONG - Do NOT use JUSTIFIED for:
// - Name
// - Contact line
// - Section headers
// - Company/title lines
// - Certifications
```

### 3. Spacing Standards

```javascript
// After name
spacing: { after: 120 }

// After contact line
spacing: { after: 240 }

// Section headers
spacing: { before: 240, after: 120 }

// Work experience bullets
spacing: { after: 120 }

// Last bullet of each job
spacing: { after: 240 }

// Between education entries
spacing: { after: 180 }

// Certifications
spacing: { after: 60 }
```

### 4. Work Experience Format

**Exact structure for each position:**

```javascript
// 1. Company line (bold + italics, NO alignment)
new Paragraph({
  children: [
    new TextRun({
      text: "Company | Location (Start Date -- End Date or Present)",
      bold: true,
      italics: true
    })
  ],
  spacing: { after: 60 }
}),

// 2. Job title line (bold + italics, NO alignment)
new Paragraph({
  children: [
    new TextRun({
      text: "Job Title -- Technical Specialization",
      bold: true,
      italics: true
    })
  ],
  spacing: { after: 120 }
}),

// 3. Bullet points (JUSTIFIED alignment, spacing 120)
new Paragraph({
  alignment: AlignmentType.JUSTIFIED,
  children: [new TextRun({ text: "- First bullet..." })],
  spacing: { after: 120 }
}),

new Paragraph({
  alignment: AlignmentType.JUSTIFIED,
  children: [new TextRun({ text: "- Second bullet..." })],
  spacing: { after: 120 }
}),

// 4. Last bullet (spacing 240)
new Paragraph({
  alignment: AlignmentType.JUSTIFIED,
  children: [new TextRun({ text: "- Last bullet..." })],
  spacing: { after: 240 }
})
```

## Workflow

### Step 1: Read Source CV

```bash
# For .docx
pandoc /mnt/user-data/uploads/filename.docx -t markdown

# For .pdf
pdftotext /mnt/user-data/uploads/filename.pdf -
```

Extract: name, contact, languages, education, skills, experience, projects, certifications.

### Step 2: Create the Script

Using the **complete template above**, replace:
- "Full Name Here" → Actual name
- Contact information → Real contact info
- Languages → User's languages with proficiency levels
- Education → User's degrees (reverse chronological)
- Technical competencies → User's tech skills (organized in 3 columns)
- Work experience → User's jobs (reverse chronological)
- Certifications → User's certifications

**For each work experience position**, create:
1. Company line
2. Job title line (add technical emphasis if optimizing for data roles)
3. 3-6 bullet points with optimizations
4. Last bullet gets spacing: { after: 240 }

### Step 3: Optimize Descriptions

Transform bullets to emphasize data work:

**Generic → Data-Optimized:**
- "Created reports" → "Developed automated Power BI dashboards reducing reporting time from 6 hours to 15 minutes weekly"
- "Improved efficiency" → "Architected data pipelines processing 10,000+ records daily using Python, reducing manual processing by 45%"
- "Analyzed issues" → "Conducted root cause analysis using SQL queries and statistical methods, identifying patterns that reduced incidents by 22%"

**Add quantification:**
- Percentages (reduced by X%, improved by Y%)
- Volume (N records, M customers, K transactions)
- Time (from X hours to Y minutes)
- Scale (across N countries, M teams)

**Add technical tools when applicable:**
- If they created reports → likely used Excel, Power BI, or Tableau
- If they analyzed data → likely used SQL, Python, or Excel
- If they automated processes → likely used Python, VBA, or PowerShell

### Step 4: Execute Script

```bash
cd /home/claude && node create_harvard_cv.js
```

Output: `/mnt/user-data/outputs/Name_Resume_Harvard.docx`

### Step 5: Validate

```bash
python /mnt/skills/public/docx/scripts/office/validate.py /mnt/user-data/outputs/Name_Resume_Harvard.docx
```

### Step 6: Present

```javascript
present_files({ filepaths: ["/mnt/user-data/outputs/Name_Resume_Harvard.docx"] })
```

## Common Mistakes to Avoid

❌ **WRONG - Using JUSTIFIED on company/title lines:**
```javascript
new Paragraph({
  alignment: AlignmentType.JUSTIFIED,  // ❌ NO!
  children: [new TextRun({ text: "Company | Location", bold: true, italics: true })]
})
```

✅ **CORRECT - No alignment on company/title lines:**
```javascript
new Paragraph({
  children: [new TextRun({ text: "Company | Location", bold: true, italics: true })],
  spacing: { after: 60 }
})
```

❌ **WRONG - Table cell without width:**
```javascript
new TableCell({
  borders,
  // Missing width! ❌
  margins: { top: 80, bottom: 80, left: 120, right: 120 },
  children: [...]
})
```

✅ **CORRECT - Table cell with width:**
```javascript
new TableCell({
  borders,
  width: { size: 3120, type: WidthType.DXA },  // ✅ Required!
  margins: { top: 80, bottom: 80, left: 120, right: 120 },
  children: [...]
})
```

## Non-Negotiable Rules

1. **US Letter page size:** 12240 x 15840 DXA with 1-inch margins
2. **Table widths MUST sum correctly:** 2-col: [4680, 4680], 3-col: [3120, 3120, 3120]
3. **Every table cell needs width property**
4. **JUSTIFIED only for work experience bullets**
5. **Never use unicode bullets** - always use "- " as plain text
6. **All links must use ExternalHyperlink**
7. **Font: Calibri, size 22 (11pt)**
8. **Never fabricate experience** - only optimize what exists

## Success Checklist

Before presenting the CV, verify:

- [ ] Name and contact are correct
- [ ] All dates formatted as (Month Year -- Month Year)
- [ ] At least 3 quantifiable metrics in work experience
- [ ] Technical competencies has 10+ items
- [ ] All hyperlinks work
- [ ] Document validates without errors
- [ ] JUSTIFIED alignment ONLY on work experience bullets
- [ ] Company/title lines have NO alignment property
- [ ] All table cells have width property
- [ ] Table column widths sum to 9360
- [ ] Spacing values are correct
- [ ] No unicode bullets (only "- " plain text)
