# 📄 Harvard CV Formatter

> Creado por **Gerald Peña** — Ayudando a profesionales a conseguir roles en datos con un CV moderno e impactante.

Turn your CV into a clean, professional Harvard-style resume optimized for data roles. Works entirely in English output, no matter what language your original CV is in.

---

## 🚀 How to Use (30 seconds)

1. Install the skill (see below)
2. Open Claude
3. The skill will greet you and ask you to upload your CV
4. Upload your CV (PDF, Word, or text)
5. Done — your CV will be rewritten automatically in English, Harvard format

---

## ⚙️ How to Install

### Easy way (recommended)

1. Download `harvard-cv-formatter.skill`
2. Open Claude
3. Go to **Settings → Skills**
4. Click **Install Skill**
5. Upload the file

### From GitHub (manual)

```bash
git clone https://github.com/geraldyita/harvard-cv-formatter.git
cp -r harvard-cv-formatter ~/.claude/skills/user/
```

Restart Claude after installing.

---

## 📊 What You Get

- Clean Harvard-style CV in English
- Better descriptions of your experience with data-focused language
- More technical wording (SQL, Python, dashboards, ETL, etc.)
- Clear impact metrics (time saved, % improvements, scale)
- **Technical skills diagnosis** — the skill evaluates your current toolset and suggests what to learn next

---

## 🩺 Technical Diagnosis

After generating your CV, the skill gives you honest, friendly feedback:

| Your tools | What it tells you |
|---|---|
| No data tools | Suggests learning SQL as a first step |
| Excel only | Encourages adding SQL next |
| Excel + SQL | Recommends Power BI or Tableau |
| SQL + Python or BI tool | No advice needed — just optimizes |
| Full stack (SQL + Python + BI + Cloud) | Focuses on maximizing impact metrics |

---

## 🔄 Example

**Before:**
> Helped with reports

**After:**
> Built Power BI dashboards integrating data from 5 operational systems, reducing manual reporting overhead from 6 hours to 15 minutes weekly while enabling data-driven resource allocation decisions.

---

## ⚠️ Important

This tool does **not invent experience**.

It only:
- Improves how your work is described
- Translates and rewrites your CV content in English
- Makes your CV stronger for data roles

---

## 🧠 How It Works

1. Reads your CV (.pdf, .docx, .txt, etc.)
2. Diagnoses your technical profile (5 levels)
3. Rewrites content using data-focused language, quantifiable metrics, and Harvard structure
4. Outputs a ready-to-use `.docx` file in English
5. Delivers a friendly summary of what changed + what to learn next (if applicable)

---

## 📁 Project Structure

```
harvard-cv-formatter/
├── README.md
├── SKILL.md
├── harvard-cv-formatter.skill
├── example-1-customer-service-to-analytics.md
└── example-2-compliance-to-analytics-engineering.md
```

---

## 🎯 Who This Is For

- People moving into data roles (Analytics, Analytics Engineering, Data Engineering and Digital Marketing Roles)
- Analysts who want to sound more technical
- Anyone working with data, even if it's not in their title
- Spanish speakers applying to international or English-speaking companies

---

## ✅ Summary

1. Install the skill
2. Upload your CV
3. Get a professional, data-focused resume in English — plus a mini roadmap if you need to grow your technical skills
