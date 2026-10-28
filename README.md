# reportaclaim

Static website for **reportaclaim.co.uk**: a UK service for drivers whose vehicle was damaged in an accident that wasn't their fault. Visitors report the accident online or by phone, and the team arranges recovery, a like-for-like replacement vehicle and repairs.

## Files

| File | What it is |
|---|---|
| `index.html` | Landing page with all its CSS, JavaScript and icons inline: reg-plate quick start, at-the-scene checklist, how it works, the 5-step claim form, services, excess comparison, FAQ and the help sheet. |
| `hit-and-run.html`, `hit-while-parked.html`, `motorbike-accident.html`, `taxi-and-van-drivers.html` | Guide pages for specific accident types. |
| `guide.css` | Shared styles for the guide pages. |
| `fonts/` | Self-hosted Inter and Inter Tight (latin subset, variable weight). |

There's no build step. Open `index.html` in a browser, or serve the folder with any static host:

```bash
python3 -m http.server 8000
```

## Ad landing links

Add `?type=` to the home page link in each ad group so the headline matches what the visitor searched for:

| Link | Headline starts with |
|---|---|
| `/?type=rear` | Rear-ended? |
| `/?type=side` | Side-swiped? |
| `/?type=parked` | Hit while parked? |
| `/?type=junction` | Hit at a junction? |
| `/?type=hitrun` | Hit and run? |
| `/?type=motorbike` | Motorbike accident? |
| `/?type=taxi` | Taxi or van hit? |

With no `type`, or an unknown one, it reads "Hit by another driver?". The guide pages send visitors to the form with their reg filled in (`?type=…&reg=…`).

## How the claim form works

1. **Fast lane (steps 1–2):** reg, safe to drive, name, mobile, when to call, consent. Sending this submits the claim.
2. **Optional extras (steps 3–4):** offered on the thank-you screen. Accident details, damage, photos, email and insurer go to the same endpoint with the same reference.

## Before launch

Search the code for `TODO` to find each one. They include:

- **Form endpoints** in `index.html`: `CLAIMS_ENDPOINT` receives the claim (`type: "claim"`) and then any extra details (`type: "details"`, same `ref`, with photos as multipart); `CALLBACK_ENDPOINT` takes the "Call me back" form. While they're empty, the forms run in demo mode and nothing is sent.
- **Phone numbers**: the claims line 0808 157 0420 on every page, and the WhatsApp number (currently a reserved 07700 900xxx placeholder).
- **Google Tag Manager**: add the container snippet to `<head>`. The page already pushes conversion events (`start_claim`, `quick_fault`, `claim_step`, `claim_submitted`, `details_submitted`, `call_click`, `landing_type` and others) to `dataLayer`.
- **Legal pages**: privacy notice, cookie policy, terms and complaints procedure currently link to `#`.
- **Domain**: switch the canonical URLs, `og:url` and structured data from `report-a-claim.vercel.app` to `https://reportaclaim.co.uk/`.
- **Reviews**: the reviews are labelled samples for testing. Replace them with genuine ones, ideally Trustpilot's own TrustBox widget (there's a slot marked `TODO` above the cards).
- **Content checks**: real handler photos, the live wait time from the telephony system, and the compliance questions noted in the guide pages.
