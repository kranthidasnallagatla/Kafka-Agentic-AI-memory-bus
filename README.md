# Agent Memory Bus

A Kafka-powered multi-agent AI system where multiple bots 
share memory so users never have to repeat themselves.

---

## The Problem

Most AI chat agents forget everything after each message.
If a user talks to a billing bot, then asks a tech question,
the second bot has no idea what already happened.
The user has to start over. Every time.

---

## What This Project Does

It connects multiple AI agents through a shared Kafka event 
bus. Every agent reads and writes to the same memory store.
So when a user sends a message, the right agent picks it up —
and already knows the full history of that conversation.

---

## How It Works (Simple Version)

1. User sends a message
2. Orchestrator reads it and decides which agent should reply
3. The chosen agent checks shared memory for prior context
4. Agent calls AWS Bedrock (Claude) and generates a response
5. Response is sent back. Memory is updated for next time.

---

## The Three Agents

- **Billing Agent** — invoices, charges, refunds, subscriptions
- **Tech Agent** — errors, bugs, login issues, app setup
- **Order Agent** — tracking, returns, cancellations, shipping

---

## Important: What This Is and Is Not

This is the **backend engine only**.

There is no chat UI yet. No floating chat bubble. No browser screen.
Right now everything runs in the terminal — messages go in,
responses come out. The actual chat window (what users see)
is Phase 3, coming next.

Think of it this way:
Phase 1 and 2 built the engine.
Phase 3 builds the dashboard so a user can drive it.

---

## Tech Stack

| Layer | Phase 1 (Local) | Phase 2 (Cloud) |
|---|---|---|
| Event Bus | Kafka via Docker | AWS MSK |
| Agent Brain | Keyword matching | AWS Bedrock (Claude 3) |
| Shared Memory | In-memory (Python) | AWS DynamoDB |
| Broker | localhost:9092 | MSK endpoint |

---

## Project Status

- Phase 1 — Done. Local Kafka, working agents, 32 tests passing.
- Phase 2 — Done. Real AI via Bedrock, DynamoDB memory, AWS MSK.
- Phase 3 — Coming. Chat UI, API Gateway, browser interface.
- Phase 4 — Coming. Monitoring, alerts, audit archive.

---

## Tests

47 unit tests across both phases.
No AWS or Docker needed to run them — everything is mocked.

```bash
python tests/test_memory_store.py
python tests/test_agents.py
python tests/test_producer.py
python tests/test_phase2_agents.py
```

---

## Author

Kranthi
