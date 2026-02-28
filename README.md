# ClinIQ

## Clinical Documents to FHIR Structured Data Converter  
**Problem Statement 2 – NHCX Hackathon 2026**

AI-Powered PDF → ABDM/NHCX Aligned FHIR Bundle Generator  
Claim Submission Use Case | Open-Source | Configuration-Driven

---

# 1️. Brief Functional Scope

ClinIQ is an AI-powered system that converts unstructured clinical PDFs into structured, NHCX-aligned FHIR R4 bundles for Claim Submission workflows under ABDM.

### Functional Capabilities

- Accepts clinical PDFs (Discharge Summary / Diagnostic Report)
- Automatically detects HI Type
- Extracts structured clinical fields using local LLM
- Maps extracted data to FHIR R4 resources
- Generates NHCX-aligned FHIR Bundles
- Performs profile-aware validation
- Allows human-in-the-loop corrections
- Exports compliant JSON bundle for claim submission

### Target Stakeholders

- Hospitals
- HMIS Vendors
- ABDM / NHCX Ecosystem Participants

---

# 2️. High-Level Architecture

## Architecture Overview

Frontend (React + TypeScript)  
↓  
PDF Parsing Layer (Client-Side)  
↓  
Ollama Local LLM (Structured Extraction)  
↓  
FHIR Mapping Engine (Configuration-Driven)  
↓  
NHCX Profile Validation Layer  
↓  
FHIR Bundle Export (JSON)

---

## Core Processing Flow

1. Upload PDF  
2. Parse and normalize document  
3. AI-based structured extraction  
4. HI Type detection  
5. FHIR resource mapping  
6. Bundle construction  
7. Profile-aware validation  
8. Human correction (if needed)  
9. Export compliant FHIR JSON  

---

# 3️. Tools and Libraries Used

## 🔓 Open Source Tools

### Frontend
- React
- TypeScript
- TailwindCSS
- Framer Motion

### AI & Processing
- Ollama (Local LLM runtime)
- llama3.2 / llama3.1 / phi3 models
- PDF parsing libraries (client-side JavaScript)

### Standards & Protocols
- FHIR R4 Specification
- NHCX Profile Guidelines

---

## 🔒 Closed Source Tools

- None used in core architecture  
- No paid cloud LLM APIs  
- No proprietary backend frameworks  

⚠️ All clinical data processing is done locally. No PHI leaves the system.

---

# 4️. Dependencies

### System Requirements

- Node.js (v18+ recommended)
- npm
- Ollama installed locally
- Minimum 8 GB RAM (for llama3.1)

### AI Model Requirements

| Model    | RAM Required | Recommended Use |
|----------|-------------|----------------|
| llama3.2 | ~8GB        | Balanced performance |
| llama3.1 | ~16GB       | Higher accuracy |
| phi3     | <8GB        | Lightweight systems |

---

# 5️. Setup Instructions

## Step 1 – Install Ollama

### Windows
1. Download from https://ollama.com
2. Install normally
3. Open Command Prompt:

```bash
ollama pull llama3.2
ollama serve
```

### macOS

```bash
curl -fsSL https://ollama.com/install.sh | sh
ollama pull llama3.2
ollama serve
```

### Linux

```bash
curl -fsSL https://ollama.com/install.sh | sh
ollama pull llama3.2
ollama serve
```

### Verify Installation

```bash
ollama list
curl http://localhost:11434/api/tags
```

---

## Step 2 – Clone Repository

```bash
git clone https://github.com/AYUsh-githu/iith-project
cd iith-project
```

---

## Step 3 – Install Frontend

```bash
npm install
npm run dev
```

---

## Step 4 – Configure AI Endpoint

_Ensure:_

1. **Base URL**: http://localhost:11434

2. Model name matches installed model (e.g., llama3.2)

_If CORS issue:_

```bash
OLLAMA_ORIGINS=* ollama serve
```

---

# 6️. Implementation Details

## 6.1 Document Processing Layer

- Client-side PDF parsing
- Text normalization
- Section detection heuristics
- Pre-processing before AI extraction

---

## 6.2 AI Structured Extraction

- Local inference using Ollama
- Deterministic JSON prompting
- Schema-constrained output format
- Low temperature for structured reliability

Example Extracted Output:

```json
{
  "patient": {
    "name": "John Doe",
    "dob": "1990-01-01",
    "gender": "male"
  },
  "diagnosis": [
    {
      "code": "I10",
      "description": "Hypertension"
    }
  ]
}
```
---

## 6.3 HI Type Detection

- Context-based classification
- Determines:
  - Discharge Summary
  - Diagnostic Report
 
---

## 6.4 FHIR Mapping Engine

- Configuration-driven mapping system:
  - JSON mapping schema
  - Field-to-resource transformation
  - Deterministic resource ID generation
  - Internal reference linking

- Supported FHIR Resources:
  - Patient
  - Encounter
  - Condition
  - Observation
  - DiagnosticReport
  - Composition
 
---

## 6.5 Bundle Construction

- Composition as root resource
- Internal references validated
- Resource linkage enforcement
- NHCX claim submission alignment

---

## 6.6 Validation Engine

Performs:

- Required field validation
- Structural integrity checks
- Cardinality validation
- Resource reference validation
- Severity classification (Error / Warning / Info)
- Bundle health score calculation

---

## 6.7 Human-in-the-Loop Layer

- Editable extracted fields
- Regenerate bundle
- Revalidate instantly
- Ensures final compliance before export

--- 

# 7️. Innovation & Impact

- Zero cloud PHI exposure
- Template-agnostic extraction
- Configuration-driven extensibility
- Faster NHCX onboarding
- Scalable across HMIS platforms
- Enables small hospitals to adopt ABDM workflows

---

# 8. Security & Compliance Justification

## 8.1 PHI Protection Strategy

- All AI inference runs locally using Ollama
- No external cloud LLM APIs
- No third-party PHI transmission
- Operates within a hospital network environment

Result:

✔ Zero external PHI exposure  
✔ No dependency on paid API services  
✔ Compliant with data minimization principles  

---

## 8.2 Standards Compliance

ClinIQ aligns with:

- FHIR R4 Specification
- NRCeS-defined NHCX Claim Submission Profiles
- ABDM Interoperability Guidelines

Compliance enforcement includes:

- Required field validation
- Cardinality constraints
- Resource type enforcement
- Bundle structural integrity checks
- Internal reference verification

---

## 8.3 Validation Framework

Each generated bundle undergoes:

- Structural validation
- Profile constraint validation
- Resource reference validation
- Severity categorization (Error / Warning / Info)

Bundles receive a **Health Score**, indicating readiness for submission.

---

## 8.4 Secure Architecture Design

- No backend exposure
- No database storage of PHI (prototype mode)
- Local execution only
- Config-driven logic reduces custom coding errors

---


# 9. Generalization Capability

Since the model was tested on:

- Organizer-provided sample PDFs
- Separate unseen submission input data

ClinIQ demonstrates:

✔ Template-agnostic extraction  
✔ Robust layout handling  
✔ Consistent FHIR mapping across formats  
✔ Stable validation performance  

---

ClinIQ successfully processed both official datasets without requiring document-specific rule changes.

---

# 10. Conclusion

ClinIQ bridges the gap between unstructured clinical PDFs and ABDM/NHCX-compliant structured FHIR data exchange.

It enables faster claim submission, reduces manual workload, and lowers the technical barrier for hospitals entering the NHCX ecosystem.
