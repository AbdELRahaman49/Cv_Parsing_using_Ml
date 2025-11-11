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

## Usage

CLI (recommended):

python cv_parser.py <files|folders> --recursive --job-title "Mechanical Engineer"


## GUI (fallback):

Run without arguments; a dialog will ask you to choose files or a folder and optionally a job title.

Examples:

# Process a folder recursively and set a Job Title override
python cv_parser.py D:\CVs --recursive --job-title "Electrical Engineer"

# Process specific files
python cv_parser.py D:\CVs\cv1.pdf D:\CVs\cv2.docx

Output

All DOCX reports are saved to:

D:\cvprojfiles\outputs


File naming:

<original_filename>_parsed.docx


If a name collision occurs, an incremental suffix is added.

Notes and Assumptions

Supported inputs: .pdf, .docx, .doc

OCR language default: English (OCR_LANG = "eng")

The “PERSONAL DATA” section renders only: Nationality, Birth Date, Gender, Residence.

If the LLM output is partial or malformed, the script auto-cleans JSON and merges with heuristic extractions.

The script attempts to infer names from the document, email, or filename if missing.

Project Structure (key parts)

Robust section normalization via SECTION_ALIASES

Safe JSON parsing with cleanup (safe_json_loads)

Fallback extractors: personal info, education, languages, experience

DOCX layout helpers for header box, key/value tables, colon-aligned lists, and footer

Batch runner with per-file error handling

Roadmap

Multi-language OCR support

Additional LLM schemas and models

Unit tests and CI

Configurable output templates
