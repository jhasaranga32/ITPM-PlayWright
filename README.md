# Singlish Transliteration Accuracy Testing

Playwright-based Python automation for testing the **Chat Sinhala** transliteration function at [pixelssuite.com/chat-translator](https://www.pixelssuite.com/chat-translator).

This project contains **50 negative test cases** (inputs where the system fails to correctly convert chat-style Singlish into Sinhala), covering all **24 Singlish input types** defined in the assignment.

---

## 📁 Project Structure

```
test_automation/
├── test_automation.py              # Main Playwright automation script
├── Assignment 1 - Test cases.xlsx  # Excel file with 50 test cases (TC ID, Input, Expected, Actual, Status)
└── README.md                       # This file
```

> **Note:** There is no `requirements.txt` or `create_excel.py` in this project.  
> The Excel file is already pre-filled with all 50 test cases. Just install dependencies and run.

---

## ✅ Prerequisites

- **Python 3.11 or 3.12** — [Download](https://www.python.org/downloads/)
- **pip** (bundled with Python; if missing, run `python get-pip.py`)
- **Google Chrome** or Chromium (Playwright installs Chromium automatically)

---

## 📦 Installation (One-Time)

Open a terminal in this project folder (`test_automation/`) and run:

```bash
# Step 1: Install Playwright
pip install playwright

# Step 2: Install openpyxl (for reading/writing Excel)
pip install openpyxl

# Step 3: Install Playwright browser (Chromium)
playwright install chromium
```

> If `pip` is not found, run `python get-pip.py` first, then retry Step 1.

---

## ▶️ Running the Automation

```bash
python test_automation.py ^
  --excel "Assignment 1 - Test cases.xlsx" ^
  --url "https://www.pixelssuite.com/chat-translator" ^
  --wait-ms 5000 ^
  --type-delay-ms 80 ^
  --slow-mo-ms 200 ^
  --save-every 1 ^
  --keep-open
```

### Command-Line Arguments

| Argument | Default | Description |
|---|---|---|
| `--excel` | Auto-detected | Path to the Excel test cases file |
| `--sheet` | `" Test cases"` | Sheet name inside the Excel file |
| `--url` | pixelssuite URL | URL of the Chat Sinhala translator |
| `--wait-ms` | `5000` | Milliseconds to wait after clicking Transliterate |
| `--retries` | `8` | Retries to detect output change |
| `--retry-wait-ms` | `1000` | Delay between retries (ms) |
| `--type-delay-ms` | `30` | Delay between keystrokes (ms) |
| `--timeout-ms` | `60000` | Max wait for page/element to load |
| `--slow-mo-ms` | `0` | Playwright slow-motion delay (ms) |
| `--save-every` | `0` | Save Excel every N test cases (`1` = after each) |
| `--keep-open` | flag | Keep browser open after tests finish |
| `--headless` | flag | Run browser in headless mode (no visible UI) |
| `--output` | Same as `--excel` | Output Excel file path (defaults to input file) |

---

## 📊 How It Works

1. **Opens** the Chromium browser and navigates to the Chat Sinhala translator.
2. **Reads** each row from the Excel file (columns: Input, Expected output).
3. **Types** the Singlish input into the left textarea.
4. **Clicks** the `Transliterate` button.
5. **Waits** for the Sinhala output to appear in the right textarea.
6. **Compares** actual output vs. expected output → writes `PASS` or `FAIL` to the `Status` column.
7. **Saves** results back to the same Excel file.

---

## 📋 Excel File Structure

The file `Assignment 1 - Test cases.xlsx` contains the sheet **` Test cases`** with these columns:

| Column | Description |
|--------|-------------|
| Test Case ID | Unique ID — format `Neg_XXXX` |
| Input length type | `S` (Short) or `M` (Medium) |
| Input | Singlish input string |
| Expected output | Correct Sinhala translation |
| Actual output | Auto-filled by the script |
| Status | Auto-filled: `PASS` / `FAIL` |

