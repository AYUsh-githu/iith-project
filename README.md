# ClinIQ

## AI-Powered Clinical PDF → ABDM/NHCX FHIR Bundle Converter

**FHIR Utility for Providers | Open-Source | Claim Submission Use Case**

---

## Problem Context

Hospitals generate **Discharge Summaries** and **Diagnostic Reports** in PDF format.

For interoperability within:

- **ABDM (Ayushman Bharat Digital Mission)**
- **NHCX (National Health Claims Exchange)**

these documents must be converted into:

- Structured **FHIR R4 resources**
- Bundles conforming to **NRCeS-defined NHCX claim submission profiles**

### Current Challenges

- Manual FHIR mapping  
- Custom, document-specific integrations  
- High onboarding cost for HMIS vendors  
- Error-prone and non-scalable workflows  

---

## Objective

Build an **open-source, configuration-driven micro-service** that:

- Accepts clinical PDFs  
- Detects HI Type (Discharge Summary / Diagnostic Report)  
- Extracts structured clinical fields  
- Converts to NHCX-aligned FHIR Bundles  
- Validates against defined profiles  
- Outputs compliant JSON bundles for claim submission  

---

# Our Solution – ClinIQ

ClinIQ is a **frontend-driven AI system powered by Ollama (local LLM)** that converts unstructured PDFs into structured, NHCX-aligned FHIR Bundles.

> ⚡ No separate backend service required  
> ⚡ Fully local LLM inference using Ollama  
> ⚡ Production-ready architecture  
> ⚡ Human-in-the-loop validation  

---

## System Architecture (Current Implementation)

### Architecture Overview

Frontend (React + TypeScript)  
↓  
PDF Parsing Layer (Client-side)  
↓  
Ollama LLM (Local Model Inference)  
↓  
FHIR Mapping Engine (Config-driven)  
↓  
NHCX Validation Layer  
↓  
Export Structured FHIR Bundle  

---

## Key Features

### ✅ 1. AI-Powered Clinical Extraction (Ollama-Based)

- LLM-driven structured JSON extraction  
- Prompt-engineered templates  
- Confidence scoring  
- Works offline (local model)  

---

### ✅ 2. Automatic HI Type Detection

- Discharge Summary  
- Diagnostic Report  

---

### ✅ 3. FHIR R4 Bundle Generation

Auto-maps fields to:

- Patient  
- Encounter  
- Condition  
- Observation  
- DiagnosticReport  
- Composition  

Features:

- Configuration-driven mappings  
- Reusable across HMIS systems  

---

### ✅ 4. NHCX Profile-Aware Validation

- Required field verification  
- Structural validation  
- Resource reference checks  
- Error & warning classification  
- Bundle health score  

---

### ✅ 5. Human-in-the-Loop Review

- Editable extracted fields  
- Regenerate FHIR bundle  
- Revalidate  
- Audit trail of corrections  

---

### ✅ 6. Export

- Download structured FHIR Bundle (JSON)  
- Ready for Claim Submission workflow  

---

## AI Layer – Ollama (Local LLM)

ClinIQ uses **Ollama** for on-device inference instead of cloud APIs.

### Supported Models

| Model    | Use Case        | RAM Requirement |
|----------|----------------|----------------|
| llama3.2 | Fast & balanced | ~8GB          |
| llama3.1 | Higher accuracy | ~16GB         |
| phi3     | Lightweight     | <8GB          |

---

# Installation Guide

## 🔵 Windows

1. Download installer from: https://ollama.com  
2. Install normally  
3. Open Command Prompt:

```bash
ollama pull llama3.2
ollama serve
```

## 🍎 macOS

```bash
curl -fsSL https://ollama.com/install.sh | sh
ollama pull llama3.2
ollama serve
```

## 🐧 Linux

```bash
curl -fsSL https://ollama.com/install.sh | sh
ollama pull llama3.2
ollama serve
```

## Verify Installation

```bash
ollama list
curl http://localhost:11434/api/tags
```

## Test Extraction

```bash
curl http://localhost:11434/api/generate -d '{
  "model": "llama3.2",
  "prompt": "Extract patient name and DOB from: John Doe, DOB 1990-01-01",
  "stream": false
}'
```
---

# Project Setup

## 1️⃣ Clone Repository

```bash
git clone https://github.com/AYUsh-githu/iith-project
cd iith-project
```

## 2️⃣ Install Frontend

```bash
npm install
npm run dev
```

## 3️⃣ Configure AI Endpoint

_Ensure:_

1. **Base URL**: http://localhost:11434

2. Model name matches installed model (e.g., llama3.2)

_If CORS issue:_

```bash
OLLAMA_ORIGINS=* ollama serve
```

---

## Processing Pipeline

1. Upload PDF(s)
2. Extract text
3. Send structured prompt to Ollama
4. Receive JSON output
5. Map to FHIR R4 resources
6. Build FHIR Bundle
7. Validate against NHCX profile
8. Human review 
9. Export JSON bundle

---

## API Interaction (Ollama)

_ClinIQ uses:_

```bash
POST http://localhost:11434/api/generate
```

with structured JSON prompts for deterministic extraction.

---

## Innovation Highlights

- Local LLM-based structured extraction
- NHCX claim submission focused
- Configuration-driven FHIR mapping
- HMIS reusable component
- Zero backend dependency

### Compliance Focus

- FHIR R4 standard resources
- NHCX claim submission profile alignment
- Required field enforcement
- Structured error reporting

---

## Impact

- Reduces manual FHIR conversion effort
- Speeds up NHCX onboarding
- Enables small hospitals to adopt ABDM workflows
- Lowers integration cost for HMIS vendors

---

# Conclusion

ClinIQ transforms static clinical PDFs into structured, interoperable FHIR bundles aligned with ABDM and NHCX standards — enabling faster claim submission, reduced manual effort, and true digital health interoperability.
