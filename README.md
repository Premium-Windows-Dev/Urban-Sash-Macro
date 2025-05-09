<p align="center">
  <a href="https://premiumwindows.com" target="_blank">
    <img src="images/logo.svg" alt="Premium Windows Logo" width="280">
  </a>
</p>

# Sash Cart Compiler (S.C.C.)

## Why We Need This Program
S.C.C. is a production-side utility tool built specifically for **Premium Windows**. Its primary purpose is to automate the **conversion of decimal-based sash dimensions to fractional measurements** and implement smart cart optimization logic.

Production processes for sashes often involve raw TXT files representing job batches. These files:

* Use decimal lengths that need to be accurately converted to standard fractional units
* Contain barcode groupings and cart/slot assignments that require logic-based reassignment

This tool helps:

* Convert all decimal dimensions to proper fractions rounded to the nearest 1/16
* Apply advanced logic to manage barcoded sash groupings across carts and slots
* Filter out invalid or already-processed files
* Automatically process multiple files with a single action
* Generate new `-SH` formatted output in the correct directory structure
* Display output summaries and diagnostics in a clean UI

---

## Why It Was Refactored
#### The original tool was built around a static dialog GUI with limited flexibility:
### Removed from original version:

* The **window image** that occupied most of the interface space
* A **single input field** with a button to process only **one file at a time**
* The need for a **second button click to amend** the file

### Problems with original architecture:

* UI logic was tightly coupled with processing logic in one large file
* Difficult to scale, maintain, or test
* No timestamping or labeling of processed files in the UI

### Refactoring Goals:

* Modular design: separate the **UI**, **logic**, and **utilities**
* Simplified UX with **one-click processing** for **multiple files**
* Responsive dark theme with centralized stylesheet
* Visible timestamp + output filename tracking
* Prevent accidental overwrites with **confirmation dialogs** and a toggle

---

## Key Updates in This Version
### Structural Changes

* `main.py`: Lightweight launch file
* `ui_main.py`: Full PyQt5 interface code and event wiring
* `processor.py`: File processing logic for sorting, reformatting, and writing
* `utils.py`: Helper functions for file validation and categorization
* `style.qss`: Dark-themed stylesheet for uniform UI aesthetics

### Functionality Added

* Converts all sash dimensions from decimal to fractional form (1/16" increments)
* Intelligent cart reassignment logic based on barcode/slot pairings
* Batch support — process **any number** of files at once
* **Timestamp and output file label** in the processed file list
* **Confirmation dialogs** for overwrite protection
* A dedicated **overwrite checkbox** for user control
* Output section now appears only **after processing** and includes:

  * Job selection panel
  * Output preview pane

### Functionality Removed

* Static image-based window layout
* Manual 1-file-at-a-time entry
* Separate "Amend" logic — replaced with streamlined one-click batch processing

---

## Usage
1. Run the app using `Sash Script V8.exe`
2. Click **Process File(s)** to select one or more `.txt` files
3. Confirm overwrites if needed (or use the checkbox to always overwrite)
4. View output job list and result previews once processed

Each selected file is:

* Filtered for validity
* Auto-converted to a `-SH.txt` version
* Decimal dimensions converted to nearest 1/16 fraction
* Cart assignments modified based on barcode conflict logic
* Time-stamped and listed in the UI

---

## Dependencies
* Python 3.8+
* `PyQt5`

Install with:

```bash
pip install pyqt5
```

---

## Future Ideas
* Add drag-and-drop support

---

## Contact
Developed for internal use by **Premium Windows**. For feature requests, support, or updates: `help@premiumwindows.com`

---

Built for simplicity, efficiency, and daily use on the production floor.
