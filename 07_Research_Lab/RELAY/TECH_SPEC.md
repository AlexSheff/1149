---
id: "8007"
title: "RELAY — Technical Specification"
layer: "07_Research_Lab"
status: concept
version: 0.1
updated: 2026-03-17
author: Founder Alex
---

# RELAY — Technical Specification

4. Product & Technology
4.1  Tech Stack
Layer
Technology
LLM Layer
Anthropic Claude (primary), OpenAI GPT-4o (fallback) via API
Agent Orchestration
LangGraph + custom async task queue
Graph Database
Neo4j — nodes: members, skills, tasks; edges: competency, interest, match history
Messaging Infrastructure
WebSocket + Redis pub/sub for real-time agent events
Backend API
Node.js (Fastify) + Python microservices for ML tasks
Frontend
React (web) + React Native (mobile)
Automation Integration
n8n self-hosted for workflow automation pipelines
Infrastructure
DigitalOcean Kubernetes + Cloudflare CDN + NeonDB (Postgres)


4.2  Agent Architecture
Each RELAY member's agent is implemented as a stateful LLM chain with four functional modules:

Processes all inbound messages, classifies intent (request, query, invitation, spam), and routes accordingly Intake Module
Maintains a rolling summary of the member's recent activity, active tasks, and stated preferences — injected into every LLM prompt Context Module
Executes approved actions: sends responses, submits proposals, requests clarification, escalates to human Action Module
Updates the member's profile graph based on outcomes: accepted/declined requests, completed tasks, user feedback Learning Module

4.3  Privacy & Data Model
RELAY is built on a privacy-first architecture. Member data is never sold to third parties and never used to train models without explicit consent. Key principles:

Agent conversations are encrypted at rest and in transit (AES-256 / TLS 1.3)
Members can export or delete their full data graph at any time
Agent actions are fully auditable via a member-accessible activity log
GDPR, CCPA, and Philippine Data Privacy Act compliance from day one

---

*Tech Spec · Reality Refactor Lab · 1149*
