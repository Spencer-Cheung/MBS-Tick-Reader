# MBS Tick OCR Reader

An OCR-based mortgage-backed securities (MBS) pricing reader built with Python, OpenCV, and EasyOCR.

This project extracts MBS pricing information from screenshots and converts the data into structured, Excel-ready datasets.

---

# Overview

Mortgage-backed securities pricing is commonly distributed through screenshots, pricing sheets, or image-based market snapshots. Manually entering this information into Excel is repetitive, time-consuming, and prone to human error.

This project automates that workflow by:

- Reading MBS pricing screenshots
- Detecting product headers and coupon information
- Extracting month labels and tick values
- Cleaning OCR misreads
- Converting pricing into decimal format
- Exporting structured results into Excel-ready tables

The objective is not perfect OCR recognition, but a workflow enhancement tool capable of dramatically reducing manual keystrokes and review time.

---

# Supported Products

Currently supported products include:

- UMBS
- GNMAII

Example formats:

```text
UMBS 6.0
UMBS 6.5
GNMAII 5.5
```

---

# Supported Pricing Formats

The OCR pipeline supports multiple MBS pricing structures.

## Standard Price Format

```text
101-14/20
95-02/20+
101-26/03+
```

## Split Tick Format

```text
101-14
/20
```

## Half Tick Support

```text
101-14+
/03+
```

---

# Decimal Conversion Examples

| Raw Price | Decimal Price |
|---|---|
| 101-14/20 | 101.625 |
| 95-02/20+ | 95.640625 |

---

# OCR Pipeline

## 1. Image Preprocessing

Images are prepared using OpenCV before OCR execution.

Processing includes:

- Upscaling
- Grayscale conversion
- Binary thresholding
- Contrast enhancement

These preprocessing steps improve OCR consistency when working with screenshots or compressed images.

---

## 2. OCR Detection

EasyOCR detects and extracts:

- Product headers
- Coupon values
- Month labels
- Price values
- Tick values

---

## 3. OCR Cleanup & Normalization

Regex-based normalization logic corrects common OCR misreads.

Examples:

| OCR Output | Corrected Value |
|---|---|
| 7120 | /20 |
| T20 | /20 |
| 107+ | /07+ |

This cleanup layer is critical because OCR engines frequently struggle with financial pricing notation.

---

## 4. Structured Parsing

After cleanup, extracted values are parsed into structured datasets.

The parser associates:

- Product type
- Coupon
- Month label
- Price
- Tick value
- Decimal representation

Final outputs are returned as Pandas DataFrames for downstream analysis or Excel integration.

---

# Technologies Used

- Python
- EasyOCR
- OpenCV
- Pandas
- NumPy
- Pillow
- Regex

---

# Example Workflow

## Input

```text
UMBS 6.5
May/Jun 101-14/20
```

## Output

| Product | Coupon | Month | Price | Decimal Price |
|---|---|---|---|---|
| UMBS | 6.5 | May/Jun | 101-14/20 | 101.625 |

---

# Project Structure

```text
project/
│
├── images/
├── output/
├── notebooks/
├── config_example.py
├── requirements.txt
└── README.md
```

---

# Installation

Install dependencies:

```bash
pip install -r requirements.txt
```

Example requirements:

```text
easyocr
opencv-python
pandas
numpy
```

---

# Usage

Run the OCR pipeline:

```bash
python run_ocr.py
```

Or execute the notebook version through:

- Jupyter Notebook
- VS Code
- Deepnote

---

# Limitations

OCR performance depends heavily on:

- Image quality
- Compression artifacts
- Font clarity
- Screenshot scaling
- Cropping consistency

Certain edge cases may still require manual review.

This project should be viewed as a workflow efficiency tool rather than a perfect OCR replacement.

---

# Future Improvements

Potential enhancements include:

- YOLO-based object detection
- Improved table segmentation
- Dynamic row detection
- Additional MBS product support
- Real-time monitoring workflows
- Interactive review UI
- Confidence scoring

---

# Data Privacy

This repository contains code logic only.

No proprietary loan data, confidential pricing information, internal systems, credentials, or company-specific datasets are included.

All file paths and configurations have been generalized for public release.

---

# Author

Spencer Cheung

Version 1.0
