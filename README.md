# BFSI Financial Decision-Making Web Platform (FinDecision.AI)

A production-ready, responsive, dark-glassmorphism AI-powered Banking, Financial Services, and Insurance (BFSI) web platform designed to assist applicants in understanding loan eligibility, credit score diagnostics, EMI affordability, cash-flow stress testing, and structured financial planning.

---

## 🌟 Core Modules

1. **User Financial Profile & Executive Dashboard**
   - Real-time aggregation of income, expenses, obligations, and credit score.
   - Immediate calculated metrics: Debt-to-Income (DTI), Fixed Obligation to Income Ratio (FOIR), Net Disposable Income, and Emergency Reserve Buffer.
   - Instant pre-loaded scenario profiles (Prime Salaried, Self-Employed Business, Early-Career Stressed, High-Net-Worth Investor).

2. **Loan Eligibility Underwriting Engine**
   - Multi-factor algorithmic scoring model (0–100 scale) weighing Credit Score (35%), DTI (25%), Income Stability (15%), Employment Profile (10%), Age/Tenure Alignment (10%), and Desired Loan Affordability (5%).
   - Transparent factor contribution breakdown and risk tier classification (`Low Risk`, `Moderate Risk`, `High Risk`, `Critical Risk`).
   - Maximum institutional borrowing capacity estimation based on institutional 50% FOIR cap.

3. **Credit Health & Factor Diagnostic Analyzer**
   - Interactive semi-circular gauge meter visualizing 5 credit bureau tiers:
     - **Poor (300–579)**
     - **Fair (580–669)**
     - **Good (670–739)**
     - **Very Good (740–799)**
     - **Excellent (800–850)**
   - Granular breakdown of key credit levers: Payment History (35%), Credit Utilization (30%), Account Age (15%), Credit Inquiries (10%), and Debt Burden (10%).
   - Automated identification of credit headwinds and actionable score uplift strategies.

4. **Real-Time EMI & Amortization Calculator**
   - Standard retail banking formula:
     $$\text{EMI} = \frac{P \cdot r \cdot (1+r)^n}{(1+r)^n - 1}$$
   - Zero-interest promotional loan handler ($\text{EMI} = P / n$).
   - Interactive Donut chart displaying Principal vs. Interest percentages.
   - Dual-view amortization repayment schedules: Yearly Summary and Monthly Installment drawdown.

5. **AI Financial Advisor & Decision Insights**
   - Server-brokered AI advisory using Google Gemini or Anthropic Claude with strict regulatory safety prompts.
   - Rule-grounded BFSI heuristic fallback engine ensuring zero downtime when external AI APIs are offline.
   - Structured decision assessment covering:
     - Executive Financial Summary
     - Spending & Cash Flow Observations
     - Debt Optimization & Mitigation Guidance
     - Credit Score Improvement Checklist
     - Safe FOIR Affordability Limits
     - 3-Phase Chronological Action Plan (Immediate 30d, Medium 3-6mo, Long-term 6-12mo).

6. **Financial Records Management & Google Sheets Sync**
   - Server-persisted audit trail of financial scenarios.
   - Automatic background synchronization to Google Sheets when configured.
   - One-click export to CSV and formatted JSON.
   - "Load into Workspace" capability to reload historical scenarios.

7. **Regulatory Compliance & Privacy-by-Design**
   - Embedded Privacy Notice Modal and Underwriting Methodology Modal.
   - Zero collection or storage of sensitive PII (no SSNs, no banking passwords, no account credentials).
   - Clear disclosure that results are educational estimates and not guaranteed lender approvals.

---

## 🛠 Tech Stack & Architecture

- **Frontend Framework**: React 19 + TypeScript + Vite
- **Styling**: Tailwind CSS with custom dark glassmorphism design tokens (`#070B14`, `#0D1320`, `#141C2E`, `#6366F1`, `#06B6D4`, `#10B981`)
- **Icons**: Lucide React
- **Backend API**: Node.js + Express
- **AI Integration**:
  - `@google/genai` (Gemini 2.5 Flash / Pro)
  - Anthropic Claude 3.5 Sonnet (optional via `ANTHROPIC_API_KEY`)
  - Grounded deterministic heuristic fallback
- **Persistence**: Server-side JSON storage with Google Sheets REST sync
- **Deployment Targets**: Cloud Run, Netlify, Vercel

---

## 🚀 Getting Started

### 1. Environment Configuration

Copy `.env.example` to `.env` and provide any desired credentials:

```bash
cp .env.example .env
```

```env
# Optional: Anthropic Claude API Key for AI Advisor
ANTHROPIC_API_KEY=""

# Google Gemini API Key (automatically injected in AI Studio)
GEMINI_API_KEY="your-gemini-key"

# Optional: Google Sheets Integration
GOOGLE_SHEET_ID=""
GOOGLE_SERVICE_ACCOUNT_EMAIL=""
GOOGLE_PRIVATE_KEY=""
```

*Note: The platform works completely out-of-the-box even without API keys thanks to its built-in BFSI heuristic underwriting engine.*

### 2. Install Dependencies

```bash
npm install
```

### 3. Run Development Server

```bash
npm run dev
```

Opens the unified Express + Vite development environment on `http://localhost:3000`.

### 4. Run Financial Engine Tests

```bash
npm run test
```

Executes test suites verifying EMI formulas, zero-interest edge cases, loan eligibility weighting, and form validations.

### 5. Build for Production

```bash
npm run build
npm start
```

---

## ⚖️ Regulatory & Underwriting Disclaimer

All calculations, eligibility metrics, risk categorizations, and AI recommendations provided by this application are for **educational and informational purposes only**. They do not constitute:
- A formal loan sanction, binding credit offer, or commitment to lend.
- A regulated credit score pulled from authorized bureaus.
- Formal legal, tax, or investment advice.

Actual loan approval, interest rates, loan margins, and tenure are determined exclusively by regulated financial institutions following full documentation verification and formal credit underwriting.

## 📚 Project Documentation

[📄 View Chetan Patil's Project Documentation](https://docs.google.com/gview?embedded=1&url=https://raw.githubusercontent.com/yashrajshembde-ctrl/AI-Powered-Personal-Finance-Advisor/main/Docs1/BSFI-MONEYMIND-AI_Documentation_Chetan_Patil.docx)
