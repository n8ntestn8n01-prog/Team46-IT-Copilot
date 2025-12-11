Project Overview

This project implements an AI-powered IT Support Copilot using n8n. It automates ticket intake from a web form, searches internal knowledge base articles using RAG (Retrieval-Augmented Generation), sends step-by-step resolutions to end users, and escalates unresolved issues into Jira.

How the Workflows Flow

RAG Knowledge Base Indexing

On demand, n8n reads IT support PDFs from Google Drive, extracts the text, generates embeddings with OpenAI, and stores them in a Pinecone vector index.

This keeps the AI search layer in sync with the latest IT knowledge base.

IT Ticket & Self-Service Workflow

When a user submits an IT issue on the website, a webhook in n8n captures the request, generates a unique Ticket ID, and logs it in a Google Sheet.

The issue description is sent to the Pinecone index, which returns the most relevant KB content. OpenAI then converts this into a clean, professional set of troubleshooting steps.

n8n sends the user a formatted HTML email with their ticket details and step-by-step resolution instructions, and posts a notification to Slack for the IT team.

Jira Escalation Workflow

If the user clicks “Escalate Issue” in the email, a second webhook is triggered.

n8n looks up the original ticket in Google Sheets and automatically creates a Jira issue with full context (ticket ID, user details, category, and description).

The user sees a confirmation page, and the IT team continues managing the case directly in Jira.
