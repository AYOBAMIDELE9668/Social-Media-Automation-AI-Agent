# Social-Media-Automation-AI-Agent
This project is a **Social Media Automation Agent** built with **LangGraph** and **Google Gemini 2.5 Flash**.   It can generate engaging social media posts, create hashtags, and reply to comments across multiple platforms.
## Features
- Generate posts for LinkedIn, Twitter, Instagram, Facebook, and YouTube.
- Generate relevant hashtags for posts.
- Automatically draft polite replies to comments.
- Built using LangGraph for workflow automation.
- Powered by Google Gemini 2.5 Flash LLM
- ## Tech Stack
- **Gemini 2.5 Flash**
- **LangGraph**
- **FastAPI**
- **Python 3.11**
- **Docker**

## fastapi_app.py

```python
from fastapi import FastAPI
from pydantic import BaseModel
from main import run_social_agent

app = FastAPI(title="Social Media Automation Agent")

class SocialQuery(BaseModel):
    topic: str
    platform: str = "Twitter"
    comment: str = ""

@app.post("/generate")
def generate_post(data: SocialQuery):
    output = run_social_agent(data.topic, data.platform, data.comment)
    return output

requirements.txt
google-generativeai>=0.23.0
langgraph>=0.1.0
fastapi>=0.110.0
uvicorn>=0.25.0
pydantic>=2.4.0

Dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

ENV GOOGLE_API_KEY=""

CMD ["uvicorn", "fastapi_app:app", "--host", "0.0.0.0", "--port", "8000"]
