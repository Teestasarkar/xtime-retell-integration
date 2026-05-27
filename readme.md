# Xtime + Retell AI Integration Middleware

This project demonstrates a reverse-engineered integration workflow between Retell AI and Xtime scheduling APIs using a Next.js middleware layer and Supabase logging.

The system simulates an AI-powered vehicle service scheduling assistant capable of:
- retrieving customer vehicle information
- retrieving appointment availability
- orchestrating middleware requests
- logging scheduling activity
- integrating with Retell AI voice agents

---

# Tech Stack

- Next.js
- TypeScript
- Supabase
- Retell AI
- Postman
- Ngrok

---

# Features

- Reverse engineered Xtime scheduling APIs
- Customer vehicle lookup using Xtime endpoints
- Appointment availability retrieval
- Next.js middleware orchestration layer
- Retell AI custom function integration
- Supabase request and booking logging
- Postman collection for endpoint testing
- Dynamic service handling through AI agent inputs
- Ngrok-based local webhook exposure for Retell integration

---

# Architecture

Retell AI Voice Agent
        ↓
Custom Function Call
        ↓
/api/retell-webhook
        ↓
/api/schedule-xtime
        ↓
Xtime APIs
        ↓
Supabase Logging

---

# Project Structure

```plaintext
app/
 └── api/
      ├── schedule-xtime/
      │    └── route.ts
      │
      └── retell-webhook/
           └── route.ts

lib/
 ├── xtime.ts
 └── supabase.ts

screenshots/
postman/
notes/
```

---

# Reverse Engineered Xtime Endpoints

The following Xtime endpoints were successfully identified and tested:

## Customer Vehicle Lookup

```plaintext
/customerVehicles
```

Used for retrieving customer vehicle information using:
- tokenId
- email
- recaptchaToken

---

## Appointment Availability

```plaintext
/getFirstAvailability
```

Used for retrieving first available appointment slots using:
- tokenId
- service metadata
- vehicle information

---

# Retell AI Integration

A Retell AI voice agent was integrated using custom function calling.

The agent:
1. Collects customer scheduling information
2. Invokes the Retell webhook endpoint
3. Forwards requests into the Next.js middleware
4. Retrieves customer vehicle and appointment availability data
5. Logs responses into Supabase

Ngrok was used during development to expose localhost endpoints securely for webhook testing.

---

# Middleware Endpoints

## /api/schedule-xtime

Core middleware route responsible for:
- calling Xtime APIs
- orchestrating scheduling workflows
- returning structured responses
- persisting logs into Supabase

---

## /api/retell-webhook

Retell-specific orchestration layer responsible for:
- receiving Retell function calls
- parsing conversational inputs
- forwarding requests into scheduling middleware

---

# Supabase Logging

Supabase is used to persist:
- customer email
- requested service
- Xtime response status
- raw API responses
- timestamps

This enables request tracing and debugging for scheduling workflows.

---

# Local Development

## Install dependencies

```bash
npm install
```

---

## Run development server

```bash
npm run dev
```

---

## Start ngrok

```bash
npx ngrok http 3000
```

---

# Environment Variables

Create a `.env.local` file:

```env
NEXT_PUBLIC_SUPABASE_URL=YOUR_SUPABASE_URL
NEXT_PUBLIC_SUPABASE_ANON_KEY=YOUR_SUPABASE_ANON_KEY
```

---

# Postman Testing

A Postman collection was created to:
- validate middleware routes
- replay Xtime requests
- inspect API responses
- test orchestration flows

---

# Current Limitations

- Xtime production endpoints appear tightly coupled with browser sessions, CAPTCHA validation, and tokenized requests.
- Full production-grade appointment creation was not fully automated due to anti-bot protections.
- The project currently demonstrates orchestration, endpoint mapping, middleware integration, and AI-agent workflows in a development/testing environment.

---

# Screenshots

The `screenshots/` folder contains:
- Retell AI integration screenshots
- Xtime network captures
- Postman testing
- Supabase logging
- Middleware execution flows

---

# Assignment Deliverables Covered

- Reverse engineered Xtime API endpoints
- Postman request collection
- Next.js middleware orchestration
- Retell AI integration
- Supabase persistence layer
- Working integration architecture

---

# Author

Teesta Sarkar  
