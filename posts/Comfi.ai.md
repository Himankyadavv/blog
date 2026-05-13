
### Version 1.0 | May 2026 | Confidential

---
## 1. Product Vision & Overview

### What is comfi.ai?

**comfi.ai** is a voice-first AI mental wellness companion designed for Gen Z users. It functions as an always-available, judgment-free AI "therapist" that users can talk to about anything — anxiety, relationships, academic pressure, identity, burnout, or just daily life stress — through natural, flowing voice conversations.

Unlike traditional therapy apps that feel clinical and sterile, comfi.ai speaks the user's language. It uses Gen Z slang, casual tone, cultural references, and empathetic but real-talk responses to make emotional support feel less like therapy and more like talking to a trusted friend who genuinely gets it.

### Core Problem Being Solved

- Mental health support is expensive, inaccessible, and stigmatized
- Gen Z is the most mentally stressed generation yet least likely to seek professional help
- Existing therapy apps feel "too formal" and disconnected from how young people actually communicate
- There is a massive gap between needing to vent/talk and having a safe space to do it

### Mission Statement

> "Making mental wellness feel less mid and more like a real convo — for real."

---

## 2. Target Audience & User Personas

### Primary Target: Gen Z (Ages 16–27)

**Persona 1 — "Zara, 19"**

- College student dealing with academic pressure and social anxiety
- Doesn't want to "bother" friends with her problems
- Afraid of judgment; wants to vent without consequences
- Uses TikTok, Discord, Spotify daily
- Needs: low-friction emotional outlet, casual tone, 24/7 availability

**Persona 2 — "Kai, 23"**

- Recent grad, struggling with career uncertainty and quarter-life crisis
- Tried therapy once but found it "too awkward"
- Highly digital-native; comfortable with AI
- Needs: someone to help him process thoughts, not give textbook advice

**Persona 3 — "Priya, 17"**

- High schooler dealing with family pressure and identity questions
- Parents don't "get it"
- Needs: safe, private, non-judgmental space to be heard

### Secondary Target: Millennials (Ages 28–35)

- Users who want an emotional outlet between therapy sessions
- People in therapy deserts (regions with no local therapists)

---

## 3. Core Features & Functionality

### 3.1 Voice Conversation (Primary Feature)

- Real-time, two-way voice conversation with the AI
- Push-to-talk OR hands-free continuous listening mode
- AI responds in voice using an emotionally expressive TTS engine
- Natural pacing — the AI doesn't rush; knows when to pause and when to probe
- Conversation memory: the AI remembers past sessions and references them naturally
- Example AI response style:
    
    > _"okay wait, that's actually a lot to be carrying rn. like, no cap, what you're feeling makes total sense. can you tell me more about what happened?"_
    

### 3.2 Tone & Personality Engine

- Multiple AI "vibes" the user can choose from:
    - **comfi (default)** — warm, chill, Gen Z casual, uses light slang
    - **real talk** — more direct, calls things out, no sugarcoating
    - **big sis/bro energy** — protective, older-sibling vibe
    - **hype mode** — uplifting, motivational, high energy
- Tone adapts dynamically based on the emotional direction of the conversation
- Slang is contextual — never forced or overdone

### 3.3 Session Modes

- **Vent Mode** — user just talks, AI listens and validates. No advice unless asked.
- **Talk It Out** — collaborative problem exploration; AI asks guided questions
- **Reality Check** — user describes a situation, AI gives an honest, grounded perspective
- **Daily Check-In** — quick 2–3 min emotional temperature check every day
- **Crisis Calm** — gentle de-escalation mode for high-distress moments

### 3.4 Mood & Progress Tracker

- Users log their mood after each session (emoji-based, low friction)
- Visual mood trend graphs over time (weekly, monthly views)
- AI surfaces patterns: "yo, I noticed you've been feeling low on Sundays a lot — wanna talk about why?"
- Personalized reflection prompts based on mood history

### 3.5 Journal (Voice-to-Text)

- Users can record voice journal entries
- AI auto-transcribes and optionally summarizes key emotional themes
- Private, encrypted; not fed into AI training

### 3.6 Safety & Crisis Protocol

- Automatic detection of high-risk language (self-harm, suicidal ideation)
- Compassionate, non-alarming response; gently offers crisis hotline resources
- One-tap access to crisis lines (iCall, Vandrevala Foundation, iCall for India; 988 for USA)
- AI never diagnoses, prescribes, or replaces professional care — always clarified

### 3.7 Personalization & Memory

- User profile builds over time (not shared, fully private)
- AI remembers: recurring themes, coping strategies that helped, preferred tone
- "It's been a while since we talked about your roommate situation — how's that going?"

### 3.8 Onboarding Flow

- Conversational onboarding (not form-based) — the AI introduces itself through voice
- User sets tone preference, comfort topics, and hard boundaries (topics they don't want to discuss)
- Optional: link to Spotify for mood-based music recommendations post-session

---

## 4. Technical Architecture

### High-Level System Architecture



### Conversation Memory Architecture

- Short-term memory: maintained within active session via conversation context window
- Long-term memory: key emotional themes, events, and patterns extracted and stored as vector embeddings in Pinecone
- On session start, relevant memories are retrieved and injected into the system prompt
- PII stripped before vector storage; only semantic meaning retained

---

## 5. Tech Stack & Tools

### Frontend

|Layer|Technology|Reason|
|---|---|---|
|Framework|React (PWA) + React Native (mobile)|Cross-platform, fast, large ecosystem|
|Styling|TailwindCSS + Framer Motion|Fast styling + smooth animations|
|Voice Capture|WebRTC / MediaRecorder API|Real-time audio in browser|
|State Management|Zustand|Lightweight, simple|
|Real-time comms|WebSocket (Socket.io)|Low-latency two-way audio stream|
|Audio Visualization|Web Audio API|Waveform animations|

### Backend

|Layer|Technology|Reason|
|---|---|---|
|Runtime|Node.js (v20+)|Non-blocking I/O for real-time audio|
|Framework|Fastify|Faster than Express, schema validation|
|API Type|REST + WebSocket|REST for data; WS for audio streaming|
|Auth|Supabase Auth / Auth0|OAuth, social login, JWT|
|Queue|BullMQ + Redis|Background jobs, audio processing|
|ORM|Prisma|Type-safe DB queries|

### AI / Voice Pipeline

|Component|Primary Tool|Fallback|
|---|---|---|
|Speech-to-Text|Deepgram Nova-2|OpenAI Whisper|
|LLM (reasoning)|Claude 3.5 Sonnet / GPT-4o|Gemini 1.5 Pro|
|Text-to-Speech|ElevenLabs (Turbo v2)|Cartesia Sonic|
|Vector Memory|Pinecone|Weaviate|
|Orchestration|LangChain.js|Custom pipeline|
|Emotion Detection|Hume AI (voice emotion)|Sentiment analysis layer|

### Database & Storage

|Service|Use Case|
|---|---|
|PostgreSQL (via Supabase)|Users, sessions, mood logs, settings|
|Redis (Upstash)|Session cache, rate limiting, pub/sub|
|Pinecone|Long-term conversation memory vectors|
|AWS S3 / Cloudflare R2|Encrypted audio & journal storage|

### Infrastructure & DevOps

|Tool|Purpose|
|---|---|
|Vercel|Frontend hosting & edge functions|
|Railway / Render|Backend API hosting|
|Docker|Containerization|
|GitHub Actions|CI/CD pipeline|
|Sentry|Error tracking|
|PostHog|Product analytics|
|Cloudflare|CDN, DDoS protection|

---

## 6. AI & Voice Pipeline

### Conversation Flow (Real-Time)

```
User speaks
    ↓
Audio captured via WebRTC (chunk streaming)
    ↓
Streamed to Deepgram → live transcription
    ↓
Transcript + conversation history → LLM (Claude/GPT-4o)
    ↓
LLM streams text response
    ↓
Text streamed to ElevenLabs TTS → audio chunks
    ↓
Audio chunks streamed back to user in real-time
    ↓
AI "speaks" while still generating (sub-2s latency target)
```

### System Prompt Design (Sample)

```
You are comfi — a Gen Z AI mental wellness companion. 
You speak casually, warmly, and use light Gen Z language 
(no cap, fr, lowkey, slay, vibe, etc.) but NEVER overdo it. 
You are empathetic, non-judgmental, and genuinely curious 
about the user's inner world.

Rules:
- NEVER diagnose, prescribe, or act as a licensed therapist
- NEVER dismiss emotions or toxic-positivity ("just be happy!")
- If crisis language detected, pivot gently to safety resources
- Ask one question at a time; don't overwhelm
- Mirror the user's energy: if they're calm, be calm; if distressed, be grounded
- Personalize using memory: [USER_MEMORY_CONTEXT]

Current tone mode: {TONE_MODE}
User emotional baseline today: {MOOD_CHECK_IN}
```

### Latency Optimization

- First-token streaming from LLM → TTS pipeline starts before full response is generated
- Deepgram's live streaming API: ~300ms STT latency
- ElevenLabs Turbo: ~400ms first audio chunk
- Total target end-to-end: **under 1.5 seconds** response latency

### Emotion Detection Layer

- Hume AI analyzes voice prosody for emotional signals (distress, calm, sadness, frustration)
- Emotional state passed as context to LLM system prompt
- Allows AI to adapt tone in real-time even when words say "I'm fine"

---

## 7. UI/UX Design Direction

### Design Philosophy

**"Soft tech"** — feels more like a cozy app than a medical tool. Think: dark mode first, soft gradients, rounded everything, calming animations.

### Color Palette

- Primary: Deep lavender `#7C6FF7`
- Secondary: Warm coral `#FF6B6B`
- Background: Near-black `#0F0F14`
- Surface: Dark slate `#1A1A24`
- Text: Off-white `#F0EEF8`
- Accent: Mint green `#6DFFC7` (for positive moments)

### Key Screens

1. **Landing / Onboarding** — animated gradient, one CTA: "start your first session"
2. **Voice Session Screen** — full-screen, minimal UI; animated waveform orb as the AI "face"; subtle breathing animation when AI is listening
3. **Session Mode Selector** — card-swipe or tap interface pre-session
4. **Mood Dashboard** — soft gradient charts, mood emoji history, AI-generated insight cards
5. **Journal** — clean, voice-first with transcript view toggle
6. **Settings / Profile** — tone selector, privacy controls, session history

### Microinteractions

- AI orb pulses when speaking, ripples when listening
- Haptic feedback on mobile (session start/end)
- Smooth scene transitions using Framer Motion
- Typing-style animation when AI text appears (in text fallback mode)

### Accessibility

- High-contrast mode
- Font size scaling
- Text fallback if voice is unavailable
- Screen reader compatibility (ARIA labels on all key elements)

---

## 8. Security, Privacy & Compliance

### Data Privacy Principles

- **No selling of data** — ever. This is foundational to trust.
- **End-to-end encryption** on all audio and journal content
- **User data deletion** on request (GDPR Article 17 compliant)
- Audio recordings deleted from servers after transcription (configurable by user)
- All AI training explicitly opted-out of for user conversation data

### Compliance Requirements

|Region|Standard|
|---|---|
|India|DPDP Act 2023 (Digital Personal Data Protection)|
|EU|GDPR|
|USA|CCPA; HIPAA-adjacent best practices (not a covered entity but following principles)|
|Global|ISO 27001 aspirational target|

### Authentication & Security

- OAuth 2.0 + social login (Google, Apple)
- JWT access tokens (15 min expiry) + refresh tokens
- Rate limiting per user and per IP
- All API calls authenticated; WebSocket connections verified
- No PII in vector memory — semantic content only
- Regular penetration testing (quarterly)

### Mental Health Specific Safeguards

- Clear product disclaimer: "comfi.ai is not a licensed therapist or medical service"
- Crisis detection keyword list maintained by clinical advisor
- Mandatory safety resources display if crisis signals detected
- Option to add emergency contact notified in extreme distress scenarios (opt-in)
- Age gate: under-16 users must have parental consent flow

---

## 9. Future Enhancement Ideas

### Phase 2 Features

- **AI Persona Customization** — users design their AI companion (name, voice, avatar personality)
- **Group Circles** — anonymous peer support rooms moderated by AI
- **Therapist Connect** — warm handoff from AI to human therapists when needed
- **Spotify / Apple Music Integration** — AI recommends songs based on emotional state post-session
- **AI Letters** — AI writes a reflective letter summarizing the user's growth over a month

### Phase 3 Features

- **Wearable Integration** — connect with Garmin/Apple Watch for heart rate context
- **Sleep Mode** — 5-minute pre-sleep wind-down voice session
- **AR Avatar** — optional 3D AI companion face in augmented reality (Vision Pro / mobile AR)
- **Multilingual Support** — Hindi, Spanish, Tagalog, Portuguese (high Gen Z population languages)
- **Family Plan** — shared dashboard for families to collectively track wellness (privacy-controlled)

### AI Capabilities Roadmap

- Multi-modal sessions: analyze user facial expressions via camera (opt-in)
- Proactive check-ins: AI initiates check-in based on mood pattern anomalies
- CBT/DBT module: structured therapy technique walkthroughs guided by AI
- Dream journaling analysis: user describes dreams; AI explores emotional themes
- AI-generated personalized affirmations (voice, delivered morning/night)

---

## 10. Monetization Strategy

### Freemium Model

**Free Tier**

- 3 voice sessions per week (up to 10 mins each)
- Basic mood tracker
- 1 AI tone option
- 7-day conversation memory

**comfi+ (Paid — ₹299/month or $4.99/month)**

- Unlimited voice sessions
- All 4 tone modes
- Full mood analytics + insights
- 90-day conversation memory
- Voice journal with transcription
- Priority response speed

**comfi Pro (₹699/month or $9.99/month)**

- Everything in comfi+
- Unlimited memory
- AI-generated monthly wellness reports
- Early access to new features
- Custom AI companion name/voice

### B2B (Future Revenue)

- **Campus Wellness** — license to universities and colleges for student mental health programs
- **Corporate Wellness** — employee mental health benefit package
- **Therapist Tools** — "comfi for Therapists" — AI session prep and between-session support tool

---

## 11. Development Phases & Roadmap

### Phase 0 — Discovery & Setup (Weeks 1–3)

- Finalize tech stack decisions
- Set up monorepo (Turborepo)
- Configure CI/CD pipelines
- Set up Supabase project and schema
- Build proof-of-concept voice pipeline (STT → LLM → TTS loop)

### Phase 1 — MVP (Weeks 4–12)

- User auth (sign up / login / Google OAuth)
- Onboarding flow (conversational)
- Core voice session (Vent Mode + Talk It Out)
- Basic AI persona (comfi default tone)
- Mood check-in post session (emoji log)
- Session history list
- Basic safety protocol (crisis keyword detection)
- Mobile-responsive web app (PWA)

### Phase 2 — Growth (Weeks 13–22)

- All 4 tone modes
- Mood dashboard and trend graphs
- Voice journal with transcription
- Long-term memory (Pinecone)
- Push notifications (daily check-in reminders)
- Subscription payments (Razorpay for India / Stripe for global)
- Android and iOS app (React Native)

### Phase 3 — Scale (Weeks 23–36)

- Emotion detection layer (Hume AI)
- AI persona customization
- Multilingual support (Hindi first)
- Therapist Connect feature
- B2B campus wellness pilot
- Performance optimization for 10k+ concurrent users

---

## 12. Risk Assessment

|Risk|Likelihood|Impact|Mitigation|
|---|---|---|---|
|User in crisis receives inadequate support|Medium|Very High|Robust crisis detection + always-on hotline links; clinical advisor review of prompts|
|AI gives harmful advice|Medium|High|System prompt guardrails; never allow diagnosis/prescription; regular red-team testing|
|Regulatory scrutiny (mental health app)|Medium|High|Legal counsel; clear "not therapy" disclaimers; DPDP/GDPR compliance from day 1|
|Voice latency makes experience poor|Medium|High|Multi-region infra; streaming pipeline; fallback to text mode|
|Data breach of sensitive conversations|Low|Very High|E2E encryption; minimal data retention; security audits|
|AI tone feels inauthentic / cringe|High|Medium|Regular tone testing with Gen Z users; A/B test slang usage; keep AI humble|
|User over-reliance on AI instead of seeking real help|Medium|High|Actively encourage professional help; limit session duration; wellness resources always visible|

---

## 13. Team & Resource Requirements

### Core Team (MVP Phase)

|Role|Responsibilities|
|---|---|
|Full-Stack Engineer (x2)|Backend API, frontend React, voice pipeline integration|
|AI/ML Engineer (x1)|Prompt engineering, LangChain orchestration, memory system|
|UI/UX Designer (x1)|Design system, screen designs, interaction design|
|Product Manager (x1)|Roadmap, user research, prioritization|
|Clinical Advisor (part-time)|Safety protocol review, prompt guidelines, crisis response design|

### External Dependencies

- Deepgram API account (STT)
- ElevenLabs API account (TTS)
- Anthropic API (Claude) or OpenAI API
- Supabase project (auth + database)
- Pinecone account (vector memory)
- Hume AI account (emotion detection — Phase 2)
- Razorpay + Stripe (payments — Phase 2)

### Monthly Infrastructure Cost Estimate (MVP)

|Service|Estimated Cost (USD/month)|
|---|---|
|Supabase (Pro)|$25|
|Deepgram API (1000 sessions × 10 min)|~$100|
|ElevenLabs (Turbo, 500k chars)|~$99|
|Claude / OpenAI API|~$150–300|
|Pinecone (Starter)|$70|
|Vercel (Pro)|$20|
|Railway / Render|$25|
|Redis (Upstash)|$10|
|**Total MVP Estimate**|**~$500–650/month**|

---

## Appendix: comfi.ai Brand Voice Guide

### DO say:

- "no cap, that sounds really hard"
- "okay, I hear you — and fr that makes sense"
- "lowkey, I think what you're feeling is valid"
- "let's unpack that a lil bit"

### DON'T say:

- "I understand your emotional state" (too clinical)
- "That must be challenging" (too formal)
- Overuse slang every sentence (feels performative)
- Give unsolicited advice in Vent Mode

### Tone Calibration Principles

1. Match the user's energy — don't bring high energy to a low moment
2. Validate before you explore — always acknowledge before asking questions
3. One question at a time — never stack multiple questions
4. Stay curious, not clinical — "tell me more" over "describe your symptoms"
5. Real talk when needed — don't gaslight with positivity

---

_Document prepared for internal use. All product decisions subject to revision based on user research and technical feasibility assessments._

_comfi.ai — because mental health should feel lowkey, not loaded._``