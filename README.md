# Instagram comment → DM (phone setup)

Someone comments a keyword on your reel and gets your link in their DMs within 5 minutes. Free, on your own Cloudflare account, using the official Instagram API.

**This version is for people with only a phone.** No laptop, no terminal, no coding.

📱 **Step-by-step phone guide:** <https://prasannakumar-09.github.io/ig-comment-dm-phone/>

[![Deploy to Cloudflare](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/prasannakumar-09/ig-comment-dm-phone)

Follow the guide first (steps 1–3). You need your Instagram account number and token before you tap the button.

Have a laptop? Use the main version instead: <https://github.com/prasannakumar-09/ig-comment-dm>

## What the Deploy button does

- Copies this repo into your own GitHub account.
- Creates the Worker, its storage (KV) and the 5-minute schedule on your own Cloudflare account.
- Asks for 3 values and stores them as encrypted secrets: `IG_USER_ID`, `IG_TOKEN`, `DASH_PASSWORD`.

Nobody else, including whoever shared this, can see your account, token or DMs.
