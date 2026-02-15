<h1 align="center">
  <img src="https://img.icons8.com/fluency/96/bank-building.png" width="80" alt="Credit Underwriting"/>
  <br/>
  Credit Underwriting AI Agent
</h1>

<p align="center">
  <strong>AI-Powered Credit Assessment System using LangGraph Agentic Workflow</strong>
  <br/>
  <em>Automated consumer loan underwriting with Human-in-the-Loop review and real-time decision audit trail</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10+-blue?style=flat-square&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/FastAPI-Backend-009688?style=flat-square&logo=fastapi&logoColor=white"/>
  <img src="https://img.shields.io/badge/React_19-Frontend-61DAFB?style=flat-square&logo=react&logoColor=black"/>
  <img src="https://img.shields.io/badge/LangGraph-Agentic_AI-FF6F00?style=flat-square&logo=langchain&logoColor=white"/>
  <img src="https://img.shields.io/badge/Google-Gemini_AI-4285F4?style=flat-square&logo=google&logoColor=white"/>
  <img src="https://img.shields.io/badge/Docker-Deploy-2496ED?style=flat-square&logo=docker&logoColor=white"/>
</p>

<p align="center">
  <a href="#introduction">Introduction</a> •
  <a href="#agentic-workflow">Agentic Workflow</a> •
  <a href="#key-features">Key Features</a> •
  <a href="#demo">Demo</a> •
  <a href="#tech-stack">Tech Stack</a> •
  <a href="#contact">Contact</a>
</p>

---

## Introduction 🚀

**Credit Underwriting AI Agent** is a full-stack application that automates the consumer loan assessment process using an **AI Agent** built on LangGraph. Instead of replacing human judgment, the system **augments** credit officers by automating data gathering, risk calculation, and policy compliance — while keeping humans in the loop for edge cases.

### Why This Project Matters

Traditional credit underwriting in Vietnamese banks faces real operational challenges:

| Challenge | AI Agent Solution |
|-----------|-------------------|
| ⏱️ Manual assessment takes **30-60 minutes** per application | AI completes full assessment in **< 30 seconds** |
| 🧠 Decisions depend on individual officer's experience | **Policy-driven guardrails** ensure 100% consistency |
| 📋 Multiple systems to check (CIC, customer DB, calculators) | Agent **orchestrates 5 tools** automatically |
| ⚠️ Edge cases slip through without review | **Human-in-the-Loop** flags borderline DTI cases |
| 📊 No centralized tracking of assessment history | **Dashboard** with real-time analytics and filters |

### Who Should Use This?

- **Banks & Financial Institutions** looking to automate retail lending
- **Digital Transformation teams** implementing AI in credit operations
- **AI/ML Engineers** studying LangGraph agentic patterns with Human-in-the-Loop
- **Product Managers** building a case for AI adoption in banking workflows

---

## Agentic Workflow 💡

### What Makes This "Agentic"?

Unlike simple chatbots or rule engines, this system uses a **LangGraph state machine** where the AI agent **autonomously decides** which tools to call, in what order, and how to interpret results — following a structured credit policy.

```
START → LLM → [Should Continue?]
               ├── YES → Call Tool → Update Scratchpad → LLM (loop)
               └── NO  → Validate Decision → [Route?]
                                               ├── REVIEW → Human Review → END
                                               └── APPROVED/REJECTED → END
```

### The 5-Step Assessment Process

The agent **must complete all 5 steps** before making a decision (unless an auto-reject condition is triggered):

| Step | Tool | What It Does | Auto-Reject? |
|------|------|-------------|:---:|
| 1️⃣ | `get_customer_info` | Fetch customer profile, verify age (18-60) | ✅ Age out of range |
| 2️⃣ | `get_cic_report` | Check credit score & bad debt history | ✅ CIC < 600 or bad debt |
| 3️⃣ | `calculate_monthly_payment` | Compute monthly installment with risk-based interest rate | ❌ |
| 4️⃣ | `calculate_dti` | Debt-to-Income ratio assessment | ✅ DTI > 50% |
| 5️⃣ | `calculate_max_loan` | Maximum approved loan amount based on income × CIC factor | ❌ |

> [!IMPORTANT]
> **Guardrails Node**: After the agent makes its decision, a `validate_decision` node independently verifies the decision against policy rules. If the LLM's decision conflicts with the data (e.g., approving a bad-debt case), the guardrails **override the LLM** automatically.

---

## Key Features ⚙️

| Feature | How It Works | Impact |
|---------|-------------|--------|
| **LangGraph Agentic AI** | State machine with 5 nodes (LLM → Tool → Scratchpad → Validate → Human Review) | Autonomous multi-step reasoning |
| **Human-in-the-Loop** | Cases with DTI 40-50% auto-pause for human reviewer approval | Balance automation with human judgment |
| **Policy Guardrails** | `validate_decision` node overrides LLM if decision contradicts policy | Prevent AI hallucination in critical decisions |
| **Reasoning Trail** | Every tool call logged as structured audit step with policy reference | Full transparency & compliance |
| **Input Pre-Validation** | Server-side checks (CCCD existence, loan amount/term limits) before AI runs | Fast-fail invalid requests, save API costs |
| **Real-time Dashboard** | Assessment history, decision distribution, filters by date/status | Operational visibility for managers |
| **Conversational Chat** | Continue asking questions about an assessment in natural language | Deeper understanding without re-running |
| **Credit Policy as Code** | Single `CreditPolicy` class as source of truth for all thresholds | Change policy in one file, propagate everywhere |

> [!NOTE]
> **Anti-Hallucination Design**: The AI agent is **not allowed to invent numbers**. Every data point (CIC score, DTI, income) must come from tool calls. The system prompt explicitly forbids fabrication.

---

## Demo 🎬

### 📱 Screenshots

<!-- 📌 REPLACE WITH ACTUAL SCREENSHOTS -->
<p align="center">
  <img src="docs/screenshots/home-assessment.png" alt="Home - Credit Assessment" width="80%"/>
  <br/><em>Home — Submit loan application and receive AI assessment</em>
</p>

<p align="center">
  <img src="docs/screenshots/reasoning-trail.png" alt="Reasoning Trail" width="80%"/>
  <br/><em>Reasoning Trail — Step-by-step audit of AI decision process</em>
</p>

<p align="center">
  <img src="docs/screenshots/dashboard.png" alt="Dashboard Analytics" width="80%"/>
  <br/><em>Dashboard — Assessment analytics with filters and charts</em>
</p>

### 💬 Example Assessment Flow

```
👤 Input:
   - Customer ID: 1001
   - Loan Amount: 200,000,000 VND
   - Term: 24 months

🤖 AI Agent Process:
   Step 1: ✅ Nguyễn Văn A, 35 tuổi, thu nhập 25,000,000 VND/tháng
   Step 2: ✅ CIC = 720 (Tốt), không nợ xấu → Lãi suất 14%/năm
   Step 3: ✅ Tiền trả hàng tháng: 9,614,696 VND
   Step 4: ✅ DTI = 38.5% → PASS (< 40%)
   Step 5: ✅ Hạn mức tối đa: 405,000,000 VND

📋 Decision: APPROVED
   "Khách hàng đạt đủ điều kiện. DTI 38.5% ở mức an toàn.
    Hạn mức 405 triệu > số tiền vay 200 triệu."
```

---

## Credit Policy 📋

The system enforces these configurable thresholds:

| Parameter | Value | Description |
|-----------|-------|-------------|
| Age | 18 - 60 | Eligible borrower age range |
| Loan Amount | 10M - 1.2B VND | Min/max loan amount |
| Loan Term | 6 - 60 months | Up to 5 years |
| CIC Auto-Reject | < 600 | Credit score below threshold |
| DTI Pass | ≤ 40% | Safe debt-to-income ratio |
| DTI Review | 40-50% | Requires human approval |
| DTI Reject | > 50% | Auto-rejected |
| Bad Debt | Group 3, 4, 5 | Auto-rejected immediately |

**Interest Rate by CIC Score:**

| CIC Score | Rating | Interest Rate | Loan Factor |
|-----------|--------|:---:|:---:|
| ≥ 750 | Rất tốt | 12%/year | 1.0x |
| ≥ 700 | Tốt | 14%/year | 0.9x |
| ≥ 650 | Khá | 16%/year | 0.8x |
| ≥ 600 | Trung bình | 18%/year | 0.6x |

---

## Tech Stack 🛠️

| Layer | Technology | Purpose |
|-------|-----------|---------|
| **Frontend** | React 19, TypeScript, TailwindCSS | Modern responsive UI |
| **UI Components** | Radix UI, Shadcn/ui, Framer Motion | Accessible, animated components |
| **Charts** | Recharts | Dashboard visualizations |
| **Backend** | FastAPI, Python 3.10+ | High-performance async API |
| **AI Agent** | LangGraph, LangChain | Stateful agentic workflow |
| **LLM** | Google Gemini | Reasoning & decision-making |
| **Database** | SQLite (aiosqlite) | Assessment history storage |
| **Deployment** | Docker Compose, Google Cloud Run | Production-ready containerization |

---

## Architecture 🏗️

```
┌──────────────────────────────────────────────────────────────┐
│                     FRONTEND (React 19)                      │
│  ┌──────────┐  ┌──────────────┐  ┌────────────────────────┐ │
│  │ LoanForm │  │ ChatInterface│  │ Dashboard (Recharts)   │ │
│  └─────┬────┘  └──────┬───────┘  └───────────┬────────────┘ │
│        │               │                      │              │
└────────┼───────────────┼──────────────────────┼──────────────┘
         │               │                      │
    ─────┼───────────────┼──────────────────────┼───── REST API
         │               │                      │
┌────────┼───────────────┼──────────────────────┼──────────────┐
│        ▼               ▼                      ▼              │
│   POST /assess    POST /chat         GET /dashboard/*        │
│                                                              │
│                  BACKEND (FastAPI)                            │
│  ┌────────────────────────────────────────────────────────┐  │
│  │              LangGraph Agent (State Machine)           │  │
│  │                                                        │  │
│  │  ┌─────┐    ┌───────┐    ┌──────────┐    ┌──────────┐ │  │
│  │  │ LLM │◄──►│ Tools │───►│Scratchpad│───►│ Validate │ │  │
│  │  └─────┘    └───┬───┘    └──────────┘    └────┬─────┘ │  │
│  │                 │                              │       │  │
│  │    ┌────────────┼────────────┐          ┌──────▼─────┐ │  │
│  │    │            │            │          │Human Review│ │  │
│  │    ▼            ▼            ▼          └────────────┘ │  │
│  │ Customer    CIC Report   Calculators                   │  │
│  │   Info      (Score/Debt) (PMT/DTI/Max)                 │  │
│  └────────────────────────────────────────────────────────┘  │
│                         │                                    │
│                    ┌────▼────┐                                │
│                    │ SQLite  │  Assessment History            │
│                    └─────────┘                                │
└──────────────────────────────────────────────────────────────┘
```

---

## API Endpoints 📡

| Method | Endpoint | Description |
|:------:|----------|-------------|
| `GET` | `/health` | Health check |
| `POST` | `/api/v1/assess` | Run full credit assessment |
| `POST` | `/api/v1/chat` | Free-form chat with AI agent |
| `POST` | `/api/v1/review` | Human reviewer submits decision |
| `GET` | `/api/v1/customers` | List customer database |
| `GET` | `/api/v1/customers/{id}` | Customer detail |
| `GET` | `/api/v1/policy` | Credit policy lookup |
| `GET` | `/api/v1/dashboard/stats` | Assessment statistics |
| `GET` | `/api/v1/dashboard/assessments` | Assessment list with filters |

---

## Quick Start 🚀

### Local Development

```bash
# Backend
cd backend
cp .env.example .env          # Add your GOOGLE_API_KEY
pip install -r requirements.txt
uvicorn app.main:app --reload --port 8000

# Frontend
cd frontend
npm install
npm run dev
```

### Docker Compose

```bash
docker-compose up --build
# Backend: http://localhost:8000
# Frontend: http://localhost:8080
```

### Deploy to Google Cloud Run

```bash
export GCP_PROJECT_ID=your-project-id
chmod +x infra/deploy.sh
./infra/deploy.sh
```

---

## About 👨‍💻

<table>
<tr>
<td width="120" align="center">
<img src="https://via.placeholder.com/100/4F46E5/FFFFFF?text=TL" width="80" style="border-radius:50%"/>
</td>
<td>

**Ty Le Van**

Product Manager | Digital Transformation — specializing in AI-powered financial solutions and customer engagement platforms.

</td>
</tr>
</table>

## Contact 📬

<p align="center">
  <a href="mailto:your.email@example.com">
    <img src="https://img.shields.io/badge/Email-Contact-D14836?style=for-the-badge&logo=gmail&logoColor=white"/>
  </a>
  <a href="https://linkedin.com/in/tylevan">
    <img src="https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=for-the-badge&logo=linkedin&logoColor=white"/>
  </a>
  <a href="https://github.com/tylevan">
    <img src="https://img.shields.io/badge/GitHub-Follow-181717?style=for-the-badge&logo=github&logoColor=white"/>
  </a>
</p>

<p align="center">
  Made with ❤️ by <strong>Ty Le Van</strong>
  <br/>
  <sub>© 2026 Credit Underwriting AI Agent</sub>
</p>
