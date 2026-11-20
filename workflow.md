# BFSI Financial Decision-Making System Workflow

Below is the complete architectural and decision-flow diagram for FinDecision.AI, illustrating user input processing, underwriting scoring, AI decision advisory brokering, and persistent records management.

```mermaid
flowchart TD
    %% User Entry & Preset Profiles
    User([Applicant / Financial Planner]) --> UI[BFSI Dark Glassmorphism Frontend]
    UI --> Presets[Preset Profiles Engine\nPrime, Business, Stressed, HNW]
    Presets -.->|Populate| ProfileState[Reactive Financial Profile State\nIncome, Expenses, Debt, Credit, Tenure]

    %% Real-time Financial Engines (Client-Side)
    subgraph ClientEngines [Client-Side Algorithmic Engines]
        ProfileState --> Val[Validation Engine\nCross-Field FOIR / DTI Sanitization]
        ProfileState --> CalcEMI[EMI Engine\nStandard Banking Formula + 0% Case]
        ProfileState --> Underwrite[Loan Underwriting Scoring Engine\nWeighted 0-100 Multi-Factor Model]
        ProfileState --> CreditDiag[Credit Diagnostic Analyzer\n5-Tier Gauge + Bureau Factor Levers]
    end

    %% UI Displays
    CalcEMI --> EMIDisplay[Donut Chart & Amortization Schedule\nYearly + Monthly Drawdown]
    Underwrite --> LoanDisplay[Eligibility Meter & Score Breakdown\nFOIR Cap & Risk Category]
    CreditDiag --> CreditDisplay[Speedometer Meter & Uplift Actions\n300-850 Bureau Index]

    %% AI Advisory Broker (Server-Side)
    UI -->|Request Advisory| ServerProxy[Express Backend Proxy / Serverless Function\nPOST /api/ai-advisor]
    
    subgraph BackendProxy [Secure Server-Side AI Orchestrator]
        ServerProxy --> KeyCheck{Key Configured?}
        KeyCheck -->|Claude Key Present| Anthropic[Anthropic Claude 3.5 Sonnet\nStrict Underwriting Compliance Prompt]
        KeyCheck -->|Gemini Key Present| Gemini[Google Gemini 2.5 Flash\nStructured JSON Mode]
        KeyCheck -->|No API Key / Error| Heuristic[BFSI Rule-Grounded Decision Engine\nDeterministic Benchmark Guidance]
    end

    Anthropic --> AdvisoryJSON[Structured JSON Assessment]
    Gemini --> AdvisoryJSON
    Heuristic --> AdvisoryJSON

    AdvisoryJSON --> AIDisplay[AI Financial Advisor View\nObservations, Debt Plan, 3-Phase Roadmap]

    %% Records Management & Persistence
    UI -->|Save Scenario Snapshot| SaveAPI[POST /api/save-record]
    SaveAPI --> LocalDB[(Persistent Server Storage\ndata/records.json)]
    SaveAPI --> SheetsCheck{Google Sheets Configured?}
    SheetsCheck -->|Yes| GoogleSheets[(Google Sheets Cloud Database)]
    SheetsCheck -->|No| LocalOnly[Server Cache Persisted]

    %% Export & Workspace Reload
    LocalDB --> RecordsUI[Financial Records View\nSearch, Filter, Delete, Load into Workspace]
    RecordsUI --> CSVExport[Download Audit CSV / JSON]
    RecordsUI -.->|Load Historical Scenario| ProfileState
```
