# Document Buffet — Travel Guides
## User & Developer Documentation

---

## What Is Document Buffet?

Document Buffet is a single-file HTML tool for building personalised Mile Zero Tours travel guide documents. You fill in a sidebar, watch a live preview update in real time, then print directly to PDF or download a standalone HTML file.

Each document is made up of **pages** (shown in the left column of the sidebar). Pages can be toggled on/off with a checkbox, reordered with the ▲▼ arrows, and further broken into subsections that can also be toggled individually.

---

## Pages (Default Order)

| # | Page ID | Label | Description |
|---|---------|-------|-------------|
| 1 | `outer-cover` | Outer Cover | Personalised cover with green column, logo, hero image, tour title, dates, prepared-for name and booking number |
| 2 | `cover` | Inner Cover | MZT-branded brochure-style inner cover with price box, included list, hotels panel, and pickup band |
| 3 | `day1` | What to Expect Day 1 | Hero image + editable Day 1 briefing text |
| 4 | `itinerary` | Itinerary | Daily itinerary auto-paginated by content length |
| 5 | `travel-pack` | Travel Pack | MZT travel pack contents (Normal or Short Escape version) |
| 6 | `contact` | Contact | Contacting Mile Zero Tours — intro paragraph + contact card |
| 7 | `ireland-policies` | Tour Policies | Booking, deposit, cancellation policies + contact details |

---

## URL Parameters

Any field can be pre-filled by appending URL parameters to the document URL. Parameters work in the query string (`?param=value`) or the hash (`#param=value`), and multiple can be chained with `&`.

**Example:**
```
DocumentBuffet2.html?oc_name=John+Smith&oc_booking=MZT-1234&coverTitle=Enchanted+Ireland
```

All parameters also support a `_b64` suffix for base64-encoded values (useful for values containing special characters):
```
DocumentBuffet2.html?oc_name_b64=Sm9obiBTbWl0aA==
```

---

### Outer Cover

| Parameter | Field | Example |
|-----------|-------|---------|
| `oc_title` | Tour title (black band) | `The Benelux Tour` |
| `oc_dates` | Dates (black band) | `April 16 – 28, 2026` |
| `oc_guide` | Document type (black band) | `Travel Guide` |
| `oc_name` | Prepared for (green column) | `John & Jane Smith` |
| `oc_booking` | Booking number (green column) | `MZT-00123` |
| `oc_img` | Hero image URL | `https://…/amsterdam.jpg` |
| `oc_logo` | Logo image URL | `https://…/logo.png` |

---

### Inner Cover

| Parameter | Field | Example |
|-----------|-------|---------|
| `coverTitle` | Tour title | `Enchanted Ireland` |
| `coverDates` | Travel dates | `October 4 - 16, 2026` |
| `coverGuideType` | Document type / duration | `13 Days` |
| `coverPreparedFor` | Prepared-for name | `John Smith` |
| `coverBooking` | Booking number | `MZT-00123` |
| `eb` | Early booking discount amount (blank = hide badge) | `$250` |
| `coverLogoSrc` | Logo image URL | `https://…/logo.png` |
| `coverHeroSrc` | Hero image URL | `https://…/ireland.jpg` |

---

### What to Expect — Day 1

| Parameter | Field | Example |
|-----------|-------|---------|
| `day1_img` | Hero image URL | `https://…/canal.jpg` |
| `day1_body` | Full body HTML (replaces all paragraphs) | `<p>Your tour begins…</p>` |

---

### Itinerary

| Parameter | Field | Example |
|-----------|-------|---------|
| `itineraryDays` | Full day-by-day content (textarea value) | See default content |
| `itnImg.1.left` | Page 1 left image URL | `https://…/photo.jpg` |
| `itnImg.1.right` | Page 1 right image URL | `https://…/photo.jpg` |
| `itnImg.2.left` | Page 2 left image URL | — |
| `itnImg.2.right` | Page 2 right image URL | — |
| `itnImg.3.left` | Page 3 left image URL | — |
| `itnImg.3.right` | Page 3 right image URL | — |
| `itnImg.4.left` | Page 4 left image URL | — |
| `itnImg.4.right` | Page 4 right image URL | — |
| `extranote.title` | Extra note title (blank = hidden) | `NOTES ABOUT TRAIN TRAVEL:` |
| `extranote.text` | Extra note body (one bullet per line) | `* Bring your passport` |
| `extranote.type` | Extra note colour style | `yellow` / `green` / `black` |

---

### Travel Pack

| Parameter | Values | Description |
|-----------|--------|-------------|
| `pack_type` | `normal` (default) | Full 5-item pack: Backpack, Luggage Strap, Plastic Tag, Ticket Wallet, Paper Tag |
| `pack_type` | `short` | Short Escape 3-item pack: Plastic Tag, Ticket Wallet, Paper Tag only |

---

### Tour Policies

| Parameter | Field | Example |
|-----------|-------|---------|
| `policiesHeroSrc` | Header image URL | `https://…/landscape.jpg` |

---

### Page Visibility & Order

| Parameter | Description | Example |
|-----------|-------------|---------|
| `pages` | Comma-separated list of page IDs to **include** (all others hidden) | `outer-cover,itinerary,ireland-policies` |
| `order` | Comma-separated list of page IDs to set display order | `outer-cover,cover,day1,itinerary` |
| `page.{id}` | Show (`1`) or hide (`0`) a specific page | `page.travel-pack=0` |
| `section.{pageId}.{sectionId}` | Show or hide a specific subsection | `section.itinerary.itinerary-content=0` |

**Page IDs:** `outer-cover`, `cover`, `day1`, `itinerary`, `travel-pack`, `contact`, `ireland-policies`

---

### Block Overrides

Any `contenteditable` region in the preview can be overridden via URL using `block.{blockId}=<html>`.

| Block ID | Location |
|----------|----------|
| `cover.price` | Inner Cover — price box |
| `cover.included` | Inner Cover — What's Included list |
| `cover.hotels` | Inner Cover — Hotels panel |
| `cover.pickup` | Inner Cover — pickup band |
| `day1.body` | Day 1 — body paragraphs |
| `contact.card` | Contact — address/phone/email card |
| `policies.box` | Tour Policies — policies box |
| `policies.contact` | Tour Policies — contact details |
| `policies.footer` | Tour Policies — footer bar |
| `extranote.content` | Extra Note content (on last itinerary page) |

---

## BYOD — Build Your Own Document

BYOD mode lets you inject entirely custom HTML sections via URL parameters. Add `byod=1` to the URL and then pass sections as `html1`, `html2`, etc.

| Parameter | Description |
|-----------|-------------|
| `byod` | Set to `1` to enable BYOD mode |
| `html1`, `html2`, … | URL-encoded HTML content for each section |
| `tt1`, `tt2`, … | Title for each section (shown in the picker) |
| `ds1`, `ds2`, … | Short description for each section |

When BYOD mode is active, a section picker opens on load so the user can choose which sections to include and in what order.

---

## Editing in the Preview

When **Editing On** is active (toggle in the top bar), the following regions are directly editable by clicking into the preview:

- Inner Cover: price box, included list, hotels panel, pickup band
- Day 1: full body text
- Contact: address/phone/email card
- Tour Policies: policies box, contact details, footer

Edits made this way are stored in memory for the session. To persist them across sessions, export to HTML via the **HTML** button in the sidebar Export panel.

---

## Exporting & Printing

| Action | How |
|--------|-----|
| Print to PDF | Click **Print / PDF** in the top bar — use your browser's Save as PDF option |
| Export HTML | Click **HTML** in the Export panel — downloads a standalone file with all styles and content embedded |
| Reset | Click **Reset** in the Export panel — restores all fields and pages to their defaults |

---

## Bob's Report

Bob's Report (top of the sidebar) automatically checks the document for common issues:

- Duplicate day numbers in the itinerary
- No itinerary days entered
- Day count mismatching the Guide Type field
- Missing tour title or dates
- Booking number still showing a placeholder (`{{BookingNum}}`)
- Prepared-for name still showing "Fullname"
- Empty hotels section
- Itinerary days with very short descriptions

Bob's issues are advisory — the document will still print regardless.
