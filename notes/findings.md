# Reverse Engineering Findings

## Objective

The objective of this project was to reverse engineer Xtime scheduling APIs and integrate them with a Retell AI voice agent using a custom Next.js middleware orchestration layer.

The integration workflow demonstrates:
- endpoint discovery
- authentication pattern extraction
- middleware orchestration
- AI-agent integration
- request persistence

---

# Reverse Engineering Process

Chrome DevTools Network inspection was used to:
- capture Xtime API traffic
- inspect request payloads
- analyze authentication parameters
- identify endpoint structures

The following elements were extracted:
- tokenId
- recaptchaToken
- vehicle metadata
- service metadata
- appointment availability requests

---

# Successfully Mapped Endpoints

## 1. customerVehicles

Purpose:
Retrieve customer vehicle information.

Authentication Inputs:
- tokenId
- email
- recaptchaToken

Observed Behavior:
- tightly coupled to CAPTCHA validation
- dependent on frontend-generated session state

---

## 2. getFirstAvailability

Purpose:
Retrieve first available appointment slots.

Inputs:
- tokenId
- vehicle information
- service metadata
- selected date

Observed Behavior:
- endpoint returns scheduling availability data
- requires structured service payloads

---

# Authentication Findings

The Xtime scheduling workflow relies heavily on:
- tokenized customer identification
- Google reCAPTCHA validation
- browser-originated session state

The production workflow appears protected using:
- CAPTCHA verification
- session cookies
- anti-bot protections
- frontend-originated request coupling

These protections prevent naive replay attacks outside browser-originated sessions.

---

# Middleware Architecture

The Next.js middleware acts as an orchestration layer between:
- Retell AI
- Xtime APIs
- Supabase logging

Primary middleware routes:
- /api/schedule-xtime
- /api/retell-webhook

---

# Middleware Flow

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

# Retell AI Findings

Retell AI was integrated using custom function calling and webhook-based orchestration.

The AI agent:
- collects scheduling information conversationally
- invokes middleware endpoints
- triggers Xtime API workflows
- returns structured responses

Ngrok was used during development for webhook exposure and local testing.

---

# Supabase Logging

Supabase was used to persist:
- customer email
- requested service
- Xtime response status
- raw API responses
- timestamps

This enables:
- request tracing
- debugging
- middleware verification
- orchestration visibility

---

# Postman Testing

Postman was used to:
- replay captured requests
- validate middleware endpoints
- inspect response payloads
- verify orchestration flows

Testing included:
- direct middleware testing
- Xtime endpoint validation
- Retell webhook integration

---

# Key Technical Challenges

## CAPTCHA Dependency

The Xtime workflow is strongly dependent on:
- reCAPTCHA validation
- browser session state
- frontend token generation

This limits direct API replay outside authenticated browser contexts.

---

## Session Coupling

Several requests appeared tightly coupled to:
- frontend browser sessions
- cookie state
- request timing
- generated tokens

---

## Appointment Creation Protections

The production appointment scheduling flow appears protected through:
- CAPTCHA validation
- session validation
- anti-bot protection mechanisms

As a result, the project focuses primarily on:
- endpoint mapping
- orchestration workflows
- middleware integration
- AI-agent integration
- scheduling flow simulation

---

# Conclusion

The project successfully demonstrates:
- reverse engineered Xtime API workflows
- middleware orchestration
- Retell AI integration
- Supabase persistence
- conversational AI scheduling architecture

The resulting system provides a working prototype for AI-assisted vehicle service scheduling workflows.