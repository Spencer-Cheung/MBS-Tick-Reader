# MBS Tick OCR Reader

Version 2.0

An OCR-driven Mortgage-Backed Securities (MBS) market data extraction pipeline built with Python, OpenCV, EasyOCR, and Pandas.

This project converts MBS pricing screenshots into structured, Excel-ready datasets while maintaining a stable reporting framework even when market snapshots contain missing months, missing coupons, or inconsistent layouts.

---

# Overview

Mortgage-backed securities pricing is commonly distributed through screenshots, trading screens, and image-based market snapshots.

Manually entering this information into spreadsheets is:

- Time consuming
- Repetitive
- Error prone
- Difficult to scale

This project automates the extraction process by reading screenshots and transforming pricing information into structured datasets suitable for reporting, analysis, and downstream workflows.

The primary objective is not perfect OCR accuracy.

The primary objective is to create a stable and repeatable workflow that dramatically reduces manual data entry while preserving data integrity.

---

# Key Features

## Dynamic Month Detection

The system automatically identifies available settlement months from the market screenshot.

## Static Reporting Framework

Version 2.0 introduces a static reporting structure that prevents month shifting and preserves reporting consistency even when months or coupons are missing.

## Placeholder Row Generation

Version 2.0 automatically creates placeholder records when expected month/coupon combinations are not present.

Benefits:

- Consistent output structure
- Easier Excel integration
- Reliable downstream reporting
- No month shifting issues

Blank data is preferred over incorrectly shifted data.

## X-Coordinate Security Mapping

Version 2.0 maps securities using image positioning rather than simple OCR ordering, preventing security misclassification when layouts shift.

---

# Supported Securities

Currently supported:

- UMBS
- GNMAII

---

# Supported Pricing Formats

## Standard Format

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

# Decimal Price Conversion

| Raw Price | Decimal Price |
|------------|------------|
| 101-14/20 | 101.625 |
| 95-02/20+ | 95.640625 |
| 101-26/03+ | 101.828125 |

---

# OCR Pipeline

## Step 1 — Image Preprocessing

- Image upscaling
- Grayscale conversion
- Binary thresholding
- Contrast enhancement
- Noise reduction

## Step 2 — OCR Detection

EasyOCR extracts:

- Product headers
- Coupon values
- Month labels
- Price values
- Tick values

## Step 3 — OCR Cleanup

Regex normalization corrects common OCR errors.

Examples:

| OCR Output | Corrected |
|------------|------------|
| 7120 | /20 |
| T20 | /20 |
| 107+ | /07+ |
| 703 | /03 |
| 705+ | /05+ |

## Step 4 — Structured Parsing

Detected values are associated with:

- Security
- Coupon
- Settlement Month
- Raw Price
- Tick Value
- Decimal Price

## Step 5 — Framework Stabilization

Version 2.0 introduces a final validation stage:

- Detect expected months
- Build static framework
- Insert placeholders
- Preserve month order
- Prevent row shifting

---

# Technologies Used

- Python
- EasyOCR
- OpenCV
- Pandas
- NumPy
- Pillow
- Regular Expressions (Regex)
- Jupyter Notebook

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
├── README.md
└── run_ocr.py
```

---

# Installation

```bash
pip install -r requirements.txt
```

---

# Usage

```bash
python run_ocr.py
```

Supported environments:

- Jupyter Notebook
- VS Code
- Deepnote

---

# Limitations

OCR accuracy remains dependent on:

- Screenshot quality
- Compression artifacts
- Font rendering
- Cropping consistency
- Image scaling

Version 2.0 focuses on output stability rather than attempting to eliminate all OCR errors.

---

# Future Improvements

- CNN-based OCR replacement
- YOLO object detection
- Confidence scoring
- Automated screenshot ingestion
- Interactive validation interface
- Additional MBS product support
- Real-time market monitoring
- Historical pricing database integration

---

# Data Privacy

This repository contains code only.

No proprietary pricing information, confidential loan data, internal systems, credentials, or company-specific datasets are included.

All paths, examples, screenshots, and configurations have been generalized for public release.

---

# Lessons Learned

> Garbage In, Garbage Out.

Financial screenshots are inherently inconsistent.

Rather than forcing perfect OCR accuracy, Version 2.0 focuses on building a stable framework that preserves structure even when source images contain missing months, missing coupons, or OCR imperfections.

In production reporting, a blank value is preferable to a shifted value.

---

# Author

Spencer Cheung

Version 2.0

2026
