# Bar Code

**Scan QR codes and barcodes, and see everything hidden inside them.**

### 🔗 Live site: <https://barcodelens.vercel.app>

Point it at a code — from a photo or your camera — and it shows you the raw contents
*and* what they actually mean, without ever opening the link.

No server, no upload, no account. Images and video never leave your device.

---

## What it does

**Reads** QR codes, EAN-13, EAN-8, UPC-A, UPC-E, Code 128, Code 39, Code 93,
ITF, Codabar, Data Matrix, Aztec and PDF417 — from a dropped photo or a live camera.

**Explains** what it found. A QR code is only text; the meaning comes from the prefix
it starts with. Bar Code unpacks the common conventions:

| Code contains | What you get told |
|---|---|
| `https://…` | Protocol, domain, path, port, and every tracking parameter listed separately |
| `WIFI:…` | Network name, security type, and **the password in plain text** |
| `BEGIN:VCARD` | Name, organisation, job title, phone, email, address |
| `BEGIN:VEVENT` | Event title, start, end, location |
| `geo:…` | Latitude, longitude, altitude |
| `SMSTO:…` | Recipient number and the pre-written message |
| `mailto:…` | Address, domain, subject, body |
| 13 digits | Product number, country prefix, and whether the **check digit is valid** |

**Makes** QR codes too — type anything, pick how much damage it should survive,
download it as a PNG, then scan your own code back to prove it works.

---

## Why "without opening it" matters

A QR code on a poster, a parking meter, or a restaurant table looks identical whether
it points somewhere sensible or somewhere nasty. You cannot read a QR code with your
eyes, so normally you find out where it goes *after* your phone has already gone there.

This tool shows you the full address first. That is the entire point of the breakdown
panel — read it, then decide.

It also makes a second thing visible: a WiFi QR code carries the password as ordinary
readable text. Anyone who photographs that card on the café wall has your password.
Useful to know before you print one.

---

## Built-in samples

Six of them, generated in your browser and decoded by the same reader — so what you
scan is a genuine working code, not a picture of one:

WiFi network · Website link with tracking parameters · Contact card · Map location ·
**a real EAN-13 product barcode** (encoded here, check digit and all) · plain text.

Click one, or drag it onto the drop box.

---

## How it works under the hood

| Piece | What it is |
|---|---|
| Reading | [ZXing](https://github.com/zxing-js/library) multi-format reader, WebAssembly-free JS build |
| Camera | `decodeFromVideoDevice` — continuous scanning off the live stream |
| QR making | [qrcode-generator](https://github.com/kazuhikoarase/qrcode-generator) |
| EAN-13 sample | Encoded from scratch in this repo — L/G/R symbol tables, parity from the first digit, computed check digit |
| Privacy | Everything runs client-side; no image ever leaves the browser |

---

## Running it locally

Single HTML file, no build step. It needs a real web server, because browsers
restrict loading scripts on `file://` URLs.

```bash
git clone https://github.com/jawadhasuna/Bar-Code
cd Bar-Code
python -m http.server 8000
```

Then open <http://localhost:8000>.

## Deploying

Any static host works. This repo is set up for [Vercel](https://vercel.com) —
import it and deploy, no configuration needed.

---

## Origin

Ported from `bar1.py` and `bar2.py`, two Python + Tkinter prototypes using OpenCV
and pyzbar. The scanning, the QR generation and the "hidden info" analysis all made
the crossing.

**What did not:** the inventory and price-lookup feature. It stored products in a
local SQLite database, and a site with no server has nowhere to keep that. Adding it
back means adding a backend — a real decision, not an oversight.

## Licence

MIT
