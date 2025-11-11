# CV Parsing & Structuring Tool (Mistral + Regex/OCR Hybrid)

`cv_parser.py` is an end-to-end CV/Resume parser that extracts structured information from PDFs and Word documents using a Mistral-based LLM pipeline with robust regex and OCR fallbacks. It outputs a professionally formatted DOCX report matching a reference layout.

## Key Features
- LLM-driven extraction (Mistral via Ollama) returning strict, valid JSON (name, headline, contacts, personal data, education, languages, skills, training, experience).
- Automatic fallbacks: regex, heuristics, and OCR (PyMuPDF + Tesseract) to recover data from complex or image-based CVs.
- Section normalization (e.g., “Work Experience” → “CHRONOLOGICAL EXPERIENCE RECORD”) for consistent outputs across varied CV styles.
- Personal data logic: nationality, birth date, gender, residence. Nationality and gender can be inferred from context when not explicitly stated.
- Language levels normalization (Native, Fluent, Very Good, Good, Fair, Basic).
- DOCX generator with reference-style layout:
  - Right-aligned header box (Name + Role)
  - Ordered sections and colon-aligned key/value tables
  - Footer with hyperlink, “Page X of Y,” and auto “Updated: Mon. YYYY”
  - Customizable page margins
- Batch mode and GUI mode:
  - CLI for automation
  - Tkinter picker when no CLI inputs are provided

## Tech Stack
- Python 3.10+
- Ollama (Mistral)
- PyMuPDF (fitz)
- pytesseract (OCR)
- python-docx
- tkinter

## Installation
```bash
pip install python-docx pymupdf pillow pytesseract
# Install and run Ollama + pull mistral model separately
# Ensure Tesseract is installed on the OS and accessible in PATH
