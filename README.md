# reportaclaim

Static website for **reportaclaim.co.uk**: a UK service for drivers whose vehicle was damaged in an accident that wasn't their fault. Visitors report the accident online or by phone, and the team arranges recovery, a like-for-like replacement vehicle and repairs.

## Files

| File | What it is |
|---|---|
| `index.html` | Landing page with all its CSS, JavaScript and icons inline: reg-plate quick start, at-the-scene checklist, how it works, the 5-step claim form, services, excess comparison, FAQ and the help sheet. |
| `hit-and-run.html`, `hit-while-parked.html`, `motorbike-accident.html`, `taxi-and-van-drivers.html` | Guide pages for specific accident types. |
| `guide.css` | Shared styles for the guide pages. |

There's no build step. Open `index.html` in a browser, or serve the folder with any static host:

```bash
python3 -m http.server 8000
```

## Before launch

Search the code for `TODO` to find each one. They include:

- **Form endpoints** in `index.html`: `CLAIMS_ENDPOINT` (full claims), `LEAD_ENDPOINT` (name and number captured at step 2, so a handler can call back if someone drops off) and `CALLBACK_ENDPOINT` (the "Call me back" form). While they're empty, the forms run in demo mode and nothing is sent.
- **Phone numbers**: the claims line 0808 157 0420 on every page, and the WhatsApp number (currently a reserved 07700 900xxx placeholder).
- **Google Tag Manager**: add the container snippet to `<head>`. The page already pushes conversion events (`start_claim`, `claim_step`, `lead_captured`, `claim_submitted`, `call_click` and others) to `dataLayer`.
- **Legal pages**: privacy notice, cookie policy, terms and complaints procedure currently link to `#`.
- **Domain**: switch the canonical URLs, `og:url` and structured data from `report-a-claim.vercel.app` to `https://reportaclaim.co.uk/`.
- **Content checks**: real handler photos, the live wait time from the telephony system, and the compliance questions noted in the guide pages.
