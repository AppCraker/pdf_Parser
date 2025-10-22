🧾 Credit Card Statement Parser (Multi-Bank)

This project extracts key financial details from Indian bank credit card statements in PDF format, supporting multiple banks automatically — including Axis Bank, HDFC Bank, ICICI Bank, and IDFC First Bank.

It can detect the issuing bank, parse fields such as card number, billing cycle, due date, total due, available credit, credit limit, name, and rewards, and export the extracted data to Excel.

📦 Features

✅ Automatic bank detection

✅ Works for Axis, HDFC, ICICI, and IDFC First Bank

✅ Extracts:

Name

Card Last 4 Digits

Billing Cycle

Payment Due Date

Total Amount Due

Available Credit

Credit Limit

Reward Points

✅ Fallback to OCR for scanned PDFs

✅ Exports clean Excel (.xlsx) with all fields

🧰 Requirements

The code runs best in Google Colab, which has most dependencies pre-installed.
If you’re running locally, install the required packages:

pip install pdfplumber pytesseract pdf2image pandas openpyxl
sudo apt-get install poppler-utils tesseract-ocr

🚀 How to Use in Colab

Upload the notebook code (your full Python script).

Run all cells.

When prompted, upload your credit-card statement PDF.

The parser will automatically:

Detect which bank it belongs to

Extract structured fields

Display JSON output

Save an Excel file named statement_fields.xlsx

The Excel file will automatically download in Colab.

🧠 Script Overview
Core Functions
Function	Purpose
pdf_to_text()	Extracts text from PDF (uses OCR fallback).
try_parse_date()	Normalizes date formats (e.g., 01-Aug-2018 → 2018-08-01).
extract_name()	Finds the customer’s name (avoids false matches like “REWARDS”).
extract_rewards()	Extracts reward-points or reward-balance values.
parse_axis()	Axis Bank–specific field extraction logic.
parse_hdfc()	HDFC Bank–specific field extraction logic.
parse_icici_idfc()	ICICI / IDFC shared parsing logic.
detect_bank()	Identifies the bank by scanning PDF text.
parse_statement()	Master function — routes to correct parser, returns all fields.
🧾 Sample Output
{
  "bank": "AXIS",
  "fields": {
    "name": "Patnala Vinod Kumar",
    "card_last4": "8002",
    "billing_cycle": "From 14/06/2018 to 13/07/2018",
    "payment_due_date": "2018-08-01",
    "total_due": "13,429.57",
    "available_credit": "34,000.00",
    "credit_limit": "20,570.43",
    "rewards": "1456"
  }
}


The Excel file (statement_fields.xlsx) will contain one row with the same fields.

⚙️ Extending the Parser

To add support for a new bank:

Create a new parse_<bankname>() function using regex patterns.

Add its detection keyword in detect_bank().

Route to the new parser in parse_statement().

🧩 Notes & Limitations

Works best on official PDF statements (not screenshots).

For scanned PDFs, OCR quality may vary — clean scans recommended.

Minor differences in layout between statement versions may need regex tuning
