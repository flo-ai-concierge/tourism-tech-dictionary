# reportlab — Programmatic PDF Generation

## What it is
A Python library for generating PDF documents entirely in code. Instead of designing a PDF in a visual tool like InDesign or Word and exporting it, you write Python that draws text, shapes, colors, tables, and images at precise coordinates. The output is a pixel-perfect, print-ready PDF.

## Basic pattern
```python
from reportlab.lib.pagesizes import letter
from reportlab.pdfgen import canvas
from reportlab.platypus import SimpleDocTemplate, Table, Paragraph, Spacer
from reportlab.lib.styles import getSampleStyleSheet

doc = SimpleDocTemplate("output.pdf", pagesize=letter)
story = []
styles = getSampleStyleSheet()

story.append(Paragraph("Hello, World", styles["Heading1"]))
story.append(Spacer(1, 12))
story.append(Table([["Name", "Price"], ["Chef Mo", "Contact for quote"]]))

doc.build(story)
```

## Two ways to use reportlab

| Mode | API | Best for |
|---|---|---|
| Low-level Canvas | `canvas.Canvas()` | Pixel-precise layouts, custom shapes, absolute positioning |
| High-level Platypus | `SimpleDocTemplate` + flowables | Multi-page documents that flow naturally (paragraphs, tables) |

**Platypus** (Paragraph Layout and Typesetting PAge Composition System) handles page breaks, line wrapping, and multi-page flow automatically. Use it when content length is variable.

**Canvas** gives you exact control — you draw at `(x, y)` coordinates from the bottom-left. Use it for fixed, designed layouts.

## Key Platypus elements
- `Paragraph(text, style)` — styled text block (supports basic HTML tags like `<b>`, `<i>`)
- `Spacer(width, height)` — vertical whitespace
- `Table(data, colWidths, style)` — tabular data with borders, colors, alignment
- `KeepTogether([...flowables])` — forces a group of elements to stay on the same page (critical for card-style layouts — prevents a header from stranding on one page while its body is on the next)
- `PageBreak()` — force a new page

## Tourism translation
Think of reportlab as a professional print shop's layout software. You write a precise spec: "the header is teal, 1.5 inches tall, the title is 24pt bold in charcoal, each vendor gets a card with a brown left border." The library executes the spec and hands you a camera-ready PDF — no human designer needed.

It's the difference between telling a graphic designer exactly what you want vs. designing it yourself in code. reportlab is the coded version: precise, repeatable, automatable.

## When to use it
- Branded internal documents generated from database data (vendor sheets, price lists, reports)
- Guest-facing PDFs (booking confirmations, welcome letters, invoices)
- Any PDF whose content comes from a database or API — static design tools can't pull live data

## Install
```bash
pip install reportlab
```

## Gotcha
reportlab coordinates originate from the **bottom-left** of the page (like a math graph). Most designers think top-down. When using Canvas mode, `y=0` is the bottom — so `y=letter[1]-72` puts you 1 inch from the top. Platypus handles this for you; Canvas does not.

## Learned from
FLOHOM FLOx Guest Experiences PDF (May 6, 2026). Vendor reference sheet for Missy — 5 private chefs, 3 massage providers, nail salon, laundry service, yoga warning. Two-page PDF with FLOHOM brand colors (charcoal/teal/brown/cream), `KeepTogether` cards to prevent split vendor entries across pages, and a per-page callback for the teal header bar and footer.

FLOHOM GRVA Contracts (May 14, 2026). Used Platypus to re-generate two fully formatted 6-page independent contractor agreements after a new clause (Section 3.7 — QUO phone support) was required post-signature. `HRFlowable` used for horizontal dividers between articles, `Table` for the compensation schedule, `ParagraphStyle` for heading/body/bullet variants.
