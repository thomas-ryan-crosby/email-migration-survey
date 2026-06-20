# Email Setup Survey

Quick visual survey we send to people after migrating from Rackspace email to Google Workspace, so we know what email app each person uses on each device and can hand them the right setup guide.

Static HTML — no build step, no dependencies. Drop it on any host. Vercel just works.

## What it does

- Explains in plain English what an email app is and why we're asking
- Shows official app icons (Outlook Classic, Outlook New, Apple Mail, Gmail, Yahoo Mail, Samsung Email, Webmail) so non-technical users can recognize what they use
- Asks per-device: business computer, personal computer, phone (type + app), other device
- Asks comfort level + preferred help format
- Collects contact info
- Submits responses by email to **ryan@crosbydevelopment.com** with **harryjr@crosbydevelopment.com** on CC

## Deploy to Vercel

1. Push this repo to GitHub (already done if you're reading this).
2. Go to <https://vercel.com/new> → Import this GitHub repo.
3. Framework preset: **Other**. Root directory: `./`. No build command needed.
4. Click Deploy. Done.

The first time someone submits the form, FormSubmit.co will send an activation email to ryan@crosbydevelopment.com. **You must click the activation link** before any responses come through. Subsequent submissions arrive immediately.

## Changing where responses go

The form action is set in `index.html`:

```html
<form action="https://formsubmit.co/ryan@crosbydevelopment.com" method="POST">
  <input type="hidden" name="_cc" value="harryjr@crosbydevelopment.com">
```

Swap the email in the `action` URL to change the primary recipient. The `_cc` field can take comma-separated emails.

To stop FormSubmit from exposing the email address publicly (and to dodge scrapers), you can switch to a hashed endpoint after the first activation:

1. Submit the form once and confirm the activation email.
2. FormSubmit will give you a random hash, e.g. `https://formsubmit.co/abcd1234efgh5678`.
3. Replace the `action` URL with the hash version.

## Files

```
.
├── index.html          Survey (/)
├── help.html           Setup-guides landing page (/help)
├── icons/              Official app icons (Wikimedia Commons)
│   ├── outlook-classic.svg
│   ├── outlook-new.svg
│   ├── apple-mail.svg
│   ├── gmail.svg
│   ├── yahoo-mail.png
│   └── samsung-email.png
├── guides/             PDF walkthroughs linked from /help
│   ├── apple-mail-first-setup.pdf
│   └── apple-mail-remove-and-re-add.pdf
├── vercel.json         Clean URLs + cache headers
└── README.md
```

## Adding a new setup guide

1. Drop the PDF into `guides/` (use kebab-case filenames).
2. Open `help.html`, find the `coming-soon` card for the matching scenario, and convert it to an `available` card:

```html
<a class="guide-card available" href="guides/your-new-guide.pdf" target="_blank" rel="noopener">
  <div class="icon-frame"><img src="icons/outlook-classic.svg" alt=""></div>
  <div class="title">Outlook (Classic) — first-time setup</div>
  <div class="device">Windows desktop</div>
  <div class="footer-row">
    <span class="badge live">● Ready</span>
    <span class="open-arrow">Open →</span>
  </div>
</a>
```

3. Commit and push — Vercel auto-deploys.

## Icon sources

All app icons are sourced from Wikimedia Commons:

- Gmail: [File:Gmail icon (2020).svg](https://commons.wikimedia.org/wiki/File:Gmail_icon_(2020).svg)
- Outlook (Classic): [File:Microsoft Office Outlook (2018–2024).svg](https://commons.wikimedia.org/wiki/File:Microsoft_Office_Outlook_(2018%E2%80%932024).svg)
- Outlook (New): [File:Microsoft Outlook Icon (2025–present).svg](https://commons.wikimedia.org/wiki/File:Microsoft_Outlook_Icon_(2025%E2%80%93present).svg)
- Apple Mail: [File:Mail (iOS).svg](https://commons.wikimedia.org/wiki/File:Mail_(iOS).svg)
- Yahoo Mail: [File:Yahoo! Mail icon (2013-2019).png](https://commons.wikimedia.org/wiki/File:Yahoo!_Mail_icon_(2013-2019).png)
- Samsung Email: [File:Samsung Email icon.png](https://commons.wikimedia.org/wiki/File:Samsung_Email_icon.png)
