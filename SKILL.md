---
name: mac-horse-quick-setup
description: Standard operating procedure to replicate MAC Horse persona + 7-step capability upgrade on a fresh Hermes instance
version: 1.0
created: 2026-05-16
tags: [setup, replication, template, upgrade]
---

# MAC Horse Quick Setup Guide

## Step 1: Identity (SOUL.md)

Copy the full content from the master machine's SOUL.md to the new machine's corresponding location.

## Step 2: Hindsight Memory

```bash
hermes config set memory.provider hindsight
hermes config set memory.hindsight.mode local_embedded
```

Then add credentials to env file (ask master for values).

## Step 3: Web Scraping

```bash
hermes skills install official/research/scrapling --force
pip install scrapling cloudscraper
```

## Step 4: Document Conversion

```bash
pip install pymupdf4llm markitdown docx2txt python-pptx pdfminer.six
```

## Step 5: Image Generation

```bash
hermes config set image_gen.provider minimax
hermes config set image_gen.model image-01
```

Add credentials to env file (ask master for values).

## Step 6: Cost Transparency

```bash
hermes config set display.show_cost true
```

## Step 7: Workflow Import

```bash
hermes skills install affaan-m/everything-claude-code/hermes-imports --force
```

## Optional: Voice

```bash
hermes config set tts.provider minimax
hermes config set stt.provider minimax
```

## Optional: WeChat Gateway

```bash
hermes gateway setup
# Select 14 -> Weixin / WeChat, confirm Y -> scan QR code
```

## Verification

```bash
hermes memory status
hermes config get image_gen.provider
python3 -c "import fitz; print('OK')"
python3 -c "from pymupdf4llm import to_markdown; print('OK')"
hermes gateway status
```

## Network Note

If GitHub is unreachable:
```bash
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```
