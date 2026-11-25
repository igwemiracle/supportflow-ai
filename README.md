# SupportFlow AI

An AI-powered customer support management platform for managing support tickets, assisting support agents, and improving customer support operations.

## Status

**Current Phase:** Phase 1: Python Fundamentals and Project Foundation

## Planned Features

- Allow customers to create and track support tickets.
- Enable support agents to manage and respond to customer enquiries.
- Provide administrators with tools to manage users and departments.
- Categorize tickets by priority and issue type.
- Use AI to classify tickets and suggest responses.
- Summarize conversations and identify recurring customer issues.

## Planned Tech Stack

- **Language:** Python
- **Backend Framework:** FastAPI
- **Validation:** Pydantic
- **Database:** PostgreSQL
- **ORM:** SQLAlchemy
- **Migrations:** Alembic
- **Caching:** Redis
- **Background Jobs:** Celery or a similar task queue (to be decided)
- **Testing:** Pytest
- **AI Integration:** OpenAI API / Gemini API
- **Containerization:** Docker
- **Version Control:** Git & GitHub

## Prerequisites

- Python 3.14 (developed and tested on 3.14.6)
- Git

Check your Python version:

```powershell
python --version
```

## Local Setup

Clone the repository:

```powershell
git clone <repository-url>
cd supportflow-ai
```

Create a Python virtual environment:

```powershell
python -m venv .venv
```

Activate the virtual environment (Windows PowerShell):

```powershell
.venv\Scripts\Activate.ps1
```

If PowerShell blocks the script, run this first (it only affects the current window):

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned
```

On macOS/Linux, activate with:

```bash
source .venv/bin/activate
```
