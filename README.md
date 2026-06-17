# On Track — Funnel Site

All four funnel pages for **On Track** (academic management for grades 6–12, a
program of Be Alright Tutoring) in one project, served under a single domain.
Each page is in its own folder and serves at the matching clean path
automatically — no extra configuration needed.

## Pages & paths

| URL              | Folder        | Page                                   |
|------------------|---------------|----------------------------------------|
| `/`              | (root)        | VSL / landing page (Vidalytics video)  |
| `/form`          | `form/`       | Application form  *(placeholder)*      |
| `/calendar`      | `calendar/`   | Booking calendar  *(placeholder)*      |
| `/thank-you`     | `thank-you/`  | Thank-you page (Meta Pixel pre-wired)  |

## ⚠️ Three things to fill in before launch

1. **Form embed** — in `form/index.html`, replace the dashed placeholder box
   with your On Track form embed (e.g. Typeform). Set its post-submit redirect
   to `/calendar`.
2. **Calendar embed** — in `calendar/index.html`, replace the placeholder box
   inside `#calendar-embed` with your booking embed (Go High Level, Calendly,
   etc.). Set its post-booking redirect to `/thank-you`.
3. **Meta Pixel ID** — in `thank-you/index.html`, replace every `YOUR_PIXEL_ID`
   with your On Track pixel ID. The pixel already fires `PageView` + `Schedule`
   on load, so each thank-you view counts as a scheduled appointment.

Each placeholder is marked with an HTML comment showing exactly what to paste.

## Funnel wiring

- The VSL's "Book a parent consultation" buttons all link to `/form`
  (relative links, so they follow whatever domain the site is served from).
- `/form` → set the form's redirect to `/calendar`.
- `/calendar` → set the calendar's redirect to `/thank-you`.

## Notes

- The logo is an inline SVG (no image file). The only image asset is Dr. Meg's
  photo on the VSL (`assets/img/dr-meg.jpg`).
- The VSL video is a Vidalytics embed loaded from their CDN; the form, calendar,
  and pixel all load from their providers — so an internet connection is
  required for those to appear.

## View locally

Clean URLs like `/form` need a server (opening files directly won't map paths):

```bash
python3 -m http.server 8000
# visit http://localhost:8000  (and /form, /calendar, /thank-you)
```

## Deploy on Vercel

1. Push this repo to GitHub and import it as **one** Vercel project
   (Framework Preset: **Other** — plain static HTML).
2. **Settings → Domains → Add** your subdomain (e.g. `start.bealrighttutoring.org`).
   A domain can belong to only one project, so remove it from any other project
   first.
3. Vercel serves `/`, `/form`, `/calendar`, and `/thank-you` from the matching
   folders automatically.
