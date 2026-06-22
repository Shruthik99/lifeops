# LifeOps

A personal operations system for tracking recurring habits, logging task completion, generating reports, and producing AI-assisted reflections and insights.

LifeOps combines:

- Google Calendar for scheduling
- Streamlit for the user interface
- CSV-based memory tracking
- Local AI models (via Ollama) for reflections and insights

The goal is simple:

> Define recurring tasks, complete them daily, track consistency over time, and periodically review performance.

---

<img width="1389" height="705" alt="image" src="https://github.com/user-attachments/assets/9dc8dfe8-8687-4531-b26c-3e6f1924f008" />


# Features

## Scheduling

- Daily tasks
- Weekly tasks
- Every N days tasks
- Every N weeks tasks
- Monthly tasks

Tasks are synced to Google Calendar with reminders.

---

## Daily Check-In

Each day, LifeOps shows the tasks due for that day.

For every task you can mark:

- Completed
- Missed

The system prevents duplicate submissions for the same task on the same day.

---

## Memory Tracking

All task outcomes are recorded locally.

Generated files:

```text
memory/
├── task_history.csv
├── completed_tasks.csv
└── missed_tasks.csv
```

Example:

```csv
date,task,status
2026-06-21,Face Pack,completed
2026-06-21,Wash Water Bottle,missed
```

---

## Reporting

LifeOps automatically generates:

### Monthly Report

Includes:

- Completed tasks
- Missed tasks
- Completion rate
- Most completed habit
- Most missed habit
- Consistency score

---

### Reflection Report

Generated using a local LLM.

Focuses on:

- What went well
- What went poorly
- Strongest habit
- Weakest habit
- Lessons learned
- Next month focus

---

### Insights Report

Generated using a local LLM.

Focuses on:

- Habit trends
- Observable patterns
- Schedule recommendations
- Priority improvements

---

## Dashboard

The dashboard provides:

- Completion rate
- Consistency score
- Completed count
- Missed count
- Recent activity
- Insights preview

---

# Tech Stack

## Backend

- Python

## Scheduling

- Google Calendar API

## Frontend

- Streamlit

## Storage

- CSV files

## AI

- Ollama
- Qwen 2.5

---

# Project Structure

```text
lifeops-agent/

├── agents/
│   ├── monthly_report_agent.py
│   ├── reflection_agent.py
│   └── insights_agent.py
│
├── memory/
│   ├── task_history.csv
│   ├── completed_tasks.csv
│   └── missed_tasks.csv
│
├── reports/
│   ├── monthly_report.txt
│   ├── reflection_report.txt
│   └── insights_report.txt
│
├── pages/
│   ├── Daily_Checkin.py
│   ├── Analytics.py
│   ├── History.py
│   ├── Reports.py
│   └── Insights.py
│
├── auth.py
├── calendar_engine.py
├── config.py
├── dashboard.py
├── due_tasks.py
├── duplicate_checker.py
├── duplicate_submission_checker.py
├── lifeops_pipeline.py
├── memory_engine.py
├── recurrence.py
├── scheduler.py
├── tasks.json
├── theme.py
│
├── requirements.txt
└── README.md
```

---

# Setup

## 1. Clone Repository

```bash
git clone <your-repo-url>
cd lifeops-agent
```

---

## 2. Create Virtual Environment

### Windows

```bash
python -m venv venv

venv\Scripts\activate
```

### Mac/Linux

```bash
python -m venv venv

source venv/bin/activate
```

---

## 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

# Google Calendar Setup

Create a Google Cloud project.

Enable:

```text
Google Calendar API
```

Download:

```text
credentials.json
```

Place it in the project root.

```text
lifeops-agent/
├── credentials.json
```

Run:

```bash
python auth.py
```

This generates:

```text
token.json
```

---

# Ollama Setup

Install Ollama:

https://ollama.com

Pull the model:

```bash
ollama pull qwen2.5:7b-instruct-q4_K_M
```

Verify:

```bash
ollama run qwen2.5:7b-instruct-q4_K_M
```

---

# Configuration

Update:

```python
config.py
```

Example:

```python
TIMEZONE = "America/New_York"

CALENDAR_ID = "primary"
```

---

# Define Your Tasks

Edit:

```text
tasks.json
```

Example:

```json
[
  {
    "name": "Check Emails",
    "type": "daily",
    "time": "10:00",
    "duration_minutes": 10,
    "reminder_before_minutes": 120
  },

  {
    "name": "Face Pack",
    "type": "weekly",
    "day": "MONDAY",
    "time": "19:00",
    "duration_minutes": 20,
    "reminder_before_minutes": 120
  }
]
```

Supported recurrence types:

```text
daily
weekly
every_n_days
every_n_weeks
monthly
```

---

# Sync Tasks To Google Calendar

Run:

```bash
python calendar_engine.py
```

This creates recurring events in Google Calendar.

Duplicate protection prevents creating the same recurring task multiple times.

---

# Run LifeOps

Start Streamlit:

```bash
streamlit run dashboard.py
```

Pages:

```text
Dashboard
Daily Check-In
Analytics
History
Reports
Insights
```

---

# Daily Workflow

1. Complete your scheduled tasks.
2. Open Daily Check-In.
3. Mark tasks as Completed or Missed.
4. Save Check-In.

LifeOps will automatically:

```text
Update memory
Generate monthly report
Generate reflection report
Generate insights report
```

---

# Example Output

Monthly Report

```text
Completed Tasks: 25
Missed Tasks: 5

Completion Rate: 83.33%

Most Completed Habit:
Face Pack

Most Missed Habit:
Wash Water Bottle

Consistency Score:
83/100
```

---

# Privacy

LifeOps stores data locally.

Data remains on your machine unless you choose to upload or sync it elsewhere.

Files stored locally:

```text
memory/
reports/
token.json
```

---

# Limitations

Current version:

- Uses CSV files instead of a database
- Supports a single user
- AI insights depend on the quality of historical data
- Requires Google Calendar configuration
- Requires Ollama for local AI-generated reports

---

# Future Improvements

Potential extensions:

- SQLite/PostgreSQL storage
- Multi-user support
- Streak tracking
- Habit scoring models
- Email summaries
- Mobile-friendly UI
- Additional AI agents

---

# Why This Project Exists

Many habit trackers focus on recording activity.

LifeOps focuses on a simple workflow:

```text
Plan
→ Execute
→ Record
→ Reflect
→ Improve
```

The project was built as a lightweight personal operations system that runs locally and can be customized by editing a single `tasks.json` file.

---
