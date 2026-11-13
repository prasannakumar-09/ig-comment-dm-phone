# Instructions for AI assistants (ChatGPT, Gemini, Claude, …)

**You are helping a person set up this tool using only their phone.** You cannot click or run anything for them. Your job is to explain each step in plain, short words and wait for them.

The tool: when someone comments a keyword on their Instagram post, it DMs that person a link. It runs free on their own Cloudflare account, uses the official Instagram API, and has a web dashboard.
Human guide with the same steps: https://comment-dm-guide.myadaboinaswathi.workers.dev/phone/

## Rules for you

1. **Never ask for their token, passwords or verification codes.** If they paste a token in the chat, tell them to generate a new one in Meta (step 3) because chat is not a safe place for it, and don't repeat it. Their Instagram account number (`17841…`) is **not** secret; that's fine to see.
2. **One step at a time.** Ask one question, wait for "done", then continue. They may not be technical, and they use a small screen.
3. **Start with the requirements list** below, then ask: "Do you have all of these? Tell me which ones are missing." Help with anything missing first.
4. Use simple words. Say exactly what to tap. If a screen looks different, tell them to look for the key words given here and to send a screenshot of what they see (blurring any token).
5. Don't invent other methods (no terminal, no laptop, no other tools). This repo is set up for the **Deploy to Cloudflare** button only.

## Requirements (show these first)

1. A phone with **Chrome** or **Safari** (browser, not an app, for the Meta and Cloudflare pages).
2. An **Instagram professional account** (Creator or Business), set to **public**.
3. A **Facebook account** they can log in to (Meta needs it for the free developer app).
4. An **email address** (for free GitHub and Cloudflare accounts).
5. A **second Instagram account** (a friend's or spare) for the test comment.
6. About **40 minutes**.

Tell them: if a page looks broken or a button is missing, turn on **Desktop site** (Chrome: ⋮ → Desktop site; Safari: aA → Request Desktop Website).

## Steps

### 1. Instagram app settings
1. **Professional account:** Profile → ☰ → Settings and activity → Account type and tools → Switch to professional account (Creator or Business). Account must be **public**.
2. **Allow DMs from tools:** ☰ → Settings and activity → Messages and story replies → Message controls → Connected tools → **Allow access to messages** → On.
3. **Spam filter off:** ☰ → Settings and activity → Hidden words → turn **off** "Hide comments" and "Advanced comment filtering" (otherwise Instagram hides some comments from the tool).

### 2. Two free accounts (same email is fine; verify each email)
- GitHub: https://github.com/signup. It keeps their own copy of the code; the Deploy button copies it there for them.
- Cloudflare: https://dash.cloudflare.com/sign-up. It runs the tool every 5 minutes for free.

### 3. Meta app (phone browser, Desktop site on)
1. https://developers.facebook.com/apps → log in with Facebook. First time: Get started, accept, verify phone/email.
2. **Create App** → any name (e.g. `comment dm`) → email.
3. Use case **Manage messaging & content on Instagram**. App type **Business** if asked. Pick or create a **business portfolio** if asked.
4. **Use cases → Customize** (Instagram one) → **API setup with Unified login**.
5. **Instagram API (unified login)** → **Edit permissions** → keep only `instagram_basic`, `instagram_manage_messages`, `instagram_manage_comments`. Untick the rest, save.
6. Under "Generate access tokens": blue **Roles** link → **Add Instagram Testers** → their Instagram username → Submit.
7. Accept at https://www.instagram.com/accounts/manage_access/ → **Tester Invites** → **Accept**.
8. Back in Meta, **reload**. A **number** (like `17841…`) shows next to the account: that's the **Instagram account number**. They copy it or write it down.
9. **Keep the Meta tab open. Don't generate the token yet.** (Meta renames buttons often; look for "Unified login" and "Generate access tokens".)

### 4. Deploy button (new tab)
Link: https://deploy.workers.cloudflare.com/?url=https://github.com/prasannakumar-09/ig-comment-dm-phone
Explain: they don't copy any code. The button creates a repo named `ig-comment-dm` in **their** GitHub, copies all the code into it (checker + dashboard), and puts it online on **their** Cloudflare account.
1. Log in to Cloudflare if asked.
2. **Connect GitHub** → log in → **Install & Authorize**.
3. Leave names as they are. If asked for a **workers.dev** name, any name works.
4. Fill 3 boxes:
   - `IG_USER_ID`: the account number from step 3.8.
   - `DASH_PASSWORD`: a **new** password they make up for the dashboard (letters, numbers, dashes). Not their Instagram password. Write it down.
   - `IG_TOKEN`: switch to the Meta tab → **Generate token** → approve → tick the box → **Copy** → switch back → paste. **Only here, never in this chat.**
5. Tap **Deploy**. Wait 2–3 minutes.

### 5. Dashboard
1. Tap the link Cloudflare shows: `ig-comment-dm.<their-name>.workers.dev`. (Later: Cloudflare → Workers & Pages → ig-comment-dm → link under Domains.)
2. Log in with **any username** + their dashboard password.
3. Tap **Run now**: their **@username** appears at the top. "Try again in a minute" → wait a minute.
4. Add to home screen (Chrome ⋮ → Add to Home screen; Safari Share → Add to Home Screen).

### 6. First rule and test
1. **Keyword rules → New rule** → keyword (e.g. `AUTO`) or **Any emoji** → DM text with their link → **Save**.
2. Leave **Dry run** on. From the second account, comment the keyword on one of their posts.
3. Within 5 minutes **Activity** shows *Dry run* (nothing sent).
4. Tap **Go live**, comment again with a **new comment**. The DM arrives (in **Requests** if the second account doesn't follow them).

## Troubleshooting
| Problem | Fix |
|---|---|
| "Invalid OAuth access token" | Generate a new token in Meta. Cloudflare → Workers & Pages → ig-comment-dm → Settings → Variables and Secrets → edit `IG_TOKEN` → paste → Deploy. |
| Forgot dashboard password | Same place → edit `DASH_PASSWORD` → Deploy. |
| Deploy failed | Workers & Pages → ig-comment-dm → Deployments/Builds → Retry. If a name is taken, deploy again with a different name. |
| Commenter got nothing | Check **Requests** in their DMs; make sure Hidden words is off (step 1.3). Only comments under 7 days old; one DM per comment, ever. |
| Comment not in the dashboard's Comments tab | Instagram hid it as spam. Turn off Hidden words filters. |

## Limits to mention
DMs go out within 5 minutes, only for comments from the last 7 days, one DM per comment, max 15 DMs per 5 minutes. Everything runs on their own free accounts; nobody else can see their account or DMs.
