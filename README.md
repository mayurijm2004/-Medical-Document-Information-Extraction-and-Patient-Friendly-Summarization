# -Medical-Document-Information-Extraction-and-Patient-Friendly-Summarization
MediSaarthi AI uses NLP to extract diagnoses, medications, test results, and follow-up instructions from medical reports. It generates concise, patient-friendly summaries while handling abbreviations, preserving the original meaning, and ensuring information remains grounded in the source without unsupported medical claims.
[README.md](https://github.com/user-attachments/files/33657586/README.md)
# MediSaarthi AI 🩺

**An NLP-Based Medical Document Information Extraction, Patient-Friendly Summarization, and Multilingual Voice Accessibility System**

MediSaarthi AI helps patients understand complex medical reports by extracting relevant clinical information, generating concise and patient-friendly summaries, translating summaries into regional languages, and reading them aloud.

> **Disclaimer:** MediSaarthi AI is an educational research prototype. It is not a medical device and does not replace a qualified healthcare professional. Always verify extracted information and consult a clinician for medical decisions.

## Table of Contents
- [Overview](#overview)
- [Problem Statement](#problem-statement)
- [Key Features](#key-features)
- [Technology Stack](#technology-stack)
- [System Workflow](#system-workflow)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Installation and Setup](#installation-and-setup)
- [Using the Application](#using-the-application)
- [Supported Languages](#supported-languages)
- [API Overview](#api-overview)
- [Testing](#testing)
- [Privacy and Safety](#privacy-and-safety)
- [Limitations](#limitations)
- [Future Enhancements](#future-enhancements)
- [Contributing](#contributing)
- [License](#license)

## Overview

Medical reports often contain technical terminology, abbreviations, diagnoses, medication details, laboratory results, and follow-up instructions that may be difficult for patients to understand.

MediSaarthi AI uses Natural Language Processing (NLP) to identify relevant information in medical documents and organize it into a concise, patient-friendly summary. It aims to preserve the original meaning, account for negation and uncertainty, and keep generated information grounded in the source document.

The application also supports multilingual summaries in **English, Hindi, Gujarati, and Marathi**, along with text-to-speech narration so users can listen to a summary in their selected language.

## Problem Statement

Medical reports and healthcare documents often contain technical terminology, abbreviations, test results, medication information, and follow-up instructions that may be difficult for patients to understand. MediSaarthi AI extracts relevant information—including diagnoses documented in the source, medications, test names, and follow-up instructions—and converts it into a concise, patient-friendly summary while preserving the original meaning. The system uses Named Entity Recognition, information extraction, abbreviation handling, and text summarization, with a focus on source grounding and avoiding unsupported medical claims.

## Key Features

- **Medical document processing:** Supports the document formats enabled in the current implementation, including PDF, DOCX, TXT, and supported image files.
- **OCR for scanned reports:** Uses Optical Character Recognition (OCR) to extract text from supported scanned documents and images.
- **Clinical information extraction:** Identifies documented diagnoses, medication details, laboratory tests and results, and follow-up instructions.
- **Negation and uncertainty handling:** Helps distinguish positive findings from negated, suspected, or ruled-out conditions.
- **Abbreviation handling:** Uses abbreviation rules and terminology handling to reduce ambiguity; uncertain terms should be flagged rather than guessed.
- **Patient-friendly summaries:** Organizes extracted information into a concise summary while retaining clinically important details.
- **Source evidence:** Allows users to inspect supporting source text where available.
- **Multilingual summaries:** Offers English, Hindi, Gujarati, and Marathi options, subject to the configured translation service.
- **Voice narration:** Text-to-speech can read the selected-language summary aloud. Available controls may include play, pause, resume, stop, replay, and playback speed.
- **PDF export:** Generates a downloadable summary report where supported by the installed fonts and current configuration.
- **Synthetic sample reports:** Includes fictional reports for demonstration and testing, if retained in the repository.
- **Responsive dashboard:** Provides a dashboard for document input, summary review, and extracted clinical information.

## Technology Stack

| Area | Technologies |
|---|---|
| Frontend | React, TypeScript, Vite |
| UI | CSS |
| Backend | Python, FastAPI |
| API schemas and validation | Pydantic |
| NLP and text processing | spaCy, regular expressions, lexical/rule-based processing |
| Negation handling | NegEx-style rules / configured negation logic |
| PDF text extraction | PyPDF |
| Word document extraction | python-docx |
| OCR | Tesseract OCR, pytesseract |
| PDF generation | ReportLab |
| Translation | Configured translation service/provider (verify provider and configuration in the source code) |
| Text-to-speech | gTTS, if enabled in the current environment |
| Testing | pytest, frontend production build |

> Technology names above reflect the documented project design. Check the actual dependency files and source code before describing every item as enabled in a particular deployment.

## System Workflow

1. **Upload or enter text:** The user uploads a supported medical document or pastes clinical text.
2. **Extract document text:** The backend extracts text from digital documents or uses OCR when configured for scanned documents.
3. **Process with NLP:** Text-processing rules and NLP components identify relevant clinical information.
4. **Preserve context:** Negation, uncertainty, medication details, units, dates, and follow-up instructions are handled as part of the extraction and validation process.
5. **Generate a summary:** The application creates a concise, patient-friendly summary based on available source information.
6. **Translate (optional):** The user selects English, Hindi, Gujarati, or Marathi, subject to translation-provider availability.
7. **Listen (optional):** Text-to-speech generates narration in the selected language when supported.
8. **Review and export:** The user checks the summary and source evidence and exports a PDF where supported.

## Project Structure

The exact structure can vary by implementation. A typical layout is:

```text
medisaarthi-ai/
├── frontend/
│   └── src/
│       ├── components/
│       ├── services/
│       └── ...
├── backend/
│   ├── app/
│   │   ├── api/
│   │   ├── models/
│   │   └── nlp/
│   ├── tests/
│   └── synthetic_data/
│       └── test_samples/
├── docs/
├── research/
├── README.md
└── .gitignore
```

Use the folders and filenames that exist in your actual repository; do not create duplicate directories just to match this example.

## Prerequisites

- Python version compatible with the backend dependencies.
- Node.js and npm compatible with the frontend dependencies.
- Git (optional, for source control).
- Tesseract OCR if scanned-document OCR is required and not already installed.
- Any required translation or TTS provider configuration used by your deployment.

Check the repository's dependency files for the exact supported versions.

## Installation and Setup

The commands below are a general setup guide. Adjust them to match the scripts and dependency files in your repository.

### 1. Clone the repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd medisaarthi-ai
```

Replace `<YOUR_GITHUB_REPOSITORY_URL>` with your actual repository URL.

### 2. Set up the backend

From the repository root, create and activate a virtual environment.

**Windows PowerShell:**

```powershell
cd backend
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

Install dependencies using the dependency file present in the backend. If it contains `requirements.txt`:

```powershell
pip install -r requirements.txt
```

If Tesseract OCR is required, install it separately for your operating system and ensure its executable is available to the application. Installing `pytesseract` alone does not install the Tesseract executable.

Configure environment variables according to the project's actual configuration. Never commit API keys or secrets.

Start the API using the entry point documented by your backend. For example, if `app.main:app` is the correct entry point:

```powershell
uvicorn app.main:app --reload --host 127.0.0.1 --port 8000
```

Open the API documentation at `http://127.0.0.1:8000/docs` when the backend is running on that host and port.

### 3. Set up the frontend

Open a second terminal from the repository root:

```powershell
cd frontend
npm install
npm run dev
```

Open the local URL printed by Vite in the terminal. It is commonly `http://localhost:5173`, but use the actual URL shown by your environment.

For a production build:

```powershell
npm run build
```

### 4. Configure frontend-to-backend communication

Check the frontend API service and Vite configuration to confirm the backend URL or proxy. Use the environment variable names expected by the actual application.

If requests fail, verify that the backend is running, the configured URL is correct, and CORS/proxy settings match the frontend origin.

## Using the Application

1. Start the backend and frontend.
2. Open the frontend in a browser.
3. Upload a supported medical report, select a synthetic sample, or paste clinical text.
4. Start the analysis.
5. Review the extracted diagnoses, medications, laboratory results, and follow-up instructions.
6. Check the patient-friendly summary and supporting source evidence.
7. Select a supported summary language if translation is available.
8. Use the voice player to listen to the selected-language summary if narration is available.
9. Export the summary to PDF if the configured PDF generation and fonts support the selected language.

Use fictional or properly de-identified reports for demonstrations and tests.

## Supported Languages

| Language | Summary translation | Voice narration |
|---|---|---|
| English | Depends on configured translation flow | Depends on configured TTS provider |
| Hindi (हिंदी) | Depends on provider availability | Depends on provider and voice availability |
| Gujarati (ગુજરાતી) | Depends on provider availability | Depends on provider and voice availability |
| Marathi (मराठी) | Depends on provider availability | Depends on provider and voice availability |

Language support depends on the actual configured translation and speech providers. Test each language in the target environment before relying on it. Indic-language PDF export may require Unicode fonts with the correct glyph coverage.

## API Overview

Confirm exact paths in the FastAPI OpenAPI documentation at `/docs`. The following endpoints were referenced in the project implementation notes; verify them against the current source code before use.

| Endpoint | Intended purpose |
|---|---|
| `GET /api/v1/translate/languages` | List supported translation languages |
| `POST /api/v1/translate/summary` | Translate a patient-friendly summary |
| `GET /api/v1/tts/languages` | List supported narration languages |
| `POST /api/v1/tts/synthesize` | Generate speech audio from text |
| `POST /api/v1/tts/narrate-summary` | Generate narration for a summary |
| `GET /api/v1/health` | Health check, if configured |

The actual API routes may differ by version. Use `/docs` as the source of truth for the running backend.

## Testing

Run the tests available in the repository. For a pytest-based backend:

```bash
pytest
```

If tests are located in a specific directory, use the path documented by the project, for example:

```bash
pytest backend/tests -v
```

For frontend validation:

```bash
cd frontend
npm run build
```

Test at least:

- Supported document formats and invalid-file handling.
- Text extraction and OCR behavior.
- Diagnosis, medication, lab, and follow-up extraction.
- Negation and uncertainty preservation.
- Evidence/source grounding.
- Translation failures and unsupported language selections.
- Voice playback, pause/resume, stop, and language switching.
- PDF export, including Indic-script rendering when enabled.
- Responsive behavior and frontend-to-backend connectivity.

Report only test results that were actually run. Passing automated tests does not establish clinical accuracy or medical safety.

## Privacy and Safety

- Use synthetic or properly de-identified documents during development and demonstrations.
- Do not commit patient records, access tokens, API keys, or other sensitive information.
- Avoid logging full medical documents or summaries unnecessarily.
- Check whether translation or TTS providers transmit text to external services before enabling them with sensitive information.
- Preserve the original report's uncertainty, negation, dates, units, medication details, and instructions.
- Do not invent diagnoses, doses, laboratory ranges, or treatment recommendations.
- Treat extracted results and generated translations as potentially imperfect and subject to review.

MediSaarthi AI is intended to improve access to information in medical documents. It does not diagnose disease, prescribe treatment, or replace a healthcare professional.

## Limitations

- OCR quality depends on image clarity, layout, and language.
- Medical terminology and abbreviations can be ambiguous.
- NLP rules may miss information or misclassify context.
- Machine translation can alter medical meaning and must be evaluated carefully.
- Voice quality and language availability depend on the selected TTS provider.
- PDF rendering for Hindi, Gujarati, and Marathi requires suitable Unicode fonts.
- Source grounding reduces unsupported output but does not guarantee correctness.
- The system is an educational prototype and has not been established as clinically validated.

## Future Enhancements

- More regional languages and dialects.
- Improved OCR for low-quality scans and complex tables.
- Clinician-reviewed multilingual evaluation datasets.
- Better terminology and abbreviation management.
- Optional offline translation and speech models.
- Accessibility improvements and additional language-specific voices.
- More robust privacy controls and deployment options.

## Contributing

Contributions are welcome. Before submitting changes:

1. Explain the issue or proposed improvement.
2. Keep clinical claims grounded in source information.
3. Add or update tests.
4. Avoid including real patient information.
5. Update the documentation to match the actual implementation.

## License

Add a `LICENSE` file before publishing this project publicly. Choose a license that matches your institution's and contributors' requirements. Do not claim a license until one has been selected and added.

---

**MediSaarthi AI** — making medical information easier to understand, in the language patients prefer.
