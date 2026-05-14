# Before Class — Setup Checklist

For two back-to-back courses:

1. **Local LLM Question Log** (FastAPI) — everything runs **LOCALLY** on your laptop: Python, the Postgres database, and the LLM (Ollama with `llama3.2`).
2. **Bedtime Story Generator** — everything runs in the **CLOUD**: Gemini API for the LLM, Render for the FastAPI backend + managed Postgres, Vercel for the frontend.

Setup below is the union for both. Items marked 🧸 apply to the bedtime course only.

Gemini API key creation is done together in class — §7 has the step-by-step for reference.

Tick each box as you finish it.

---

## 1. Accounts (sign up — no installs yet)

- [ ] **GitHub** — <https://github.com/signup>. Pick a sensible username. Turn on two-factor authentication when prompted.
- [ ] **Google** — <https://accounts.google.com/signup>. Skip if you already have one.
- [ ] **Claude** (Anthropic) — <https://claude.ai>. Free tier.
- [ ] **Perplexity** — <https://www.perplexity.ai>. Free tier.
- [ ] **ChatGPT** (OpenAI) — <https://chatgpt.com>. Free tier.
- [ ] 🧸 **Render** — <https://render.com>. Sign up using your GitHub account. Free Postgres on Render expires 30 days after creation.
- [ ] 🧸 **Vercel** — <https://vercel.com/signup>. Sign up using your GitHub account. Free Hobby tier.

## 2. GitHub mobile app (for two-factor authentication)

- [ ] iOS — <https://apps.apple.com/app/github/id1477376905>
- [ ] Android — <https://play.google.com/store/apps/details?id=com.github.android>
- [ ] Sign in with your GitHub account.
- [ ] Approve "use this device for two-factor authentication" when the app prompts.

## 3. AI partner apps (install all four)

- [ ] Claude — <https://claude.ai/download>
- [ ] ChatGPT — <https://chatgpt.com> → top-right menu → Download. Also on App Store / Play Store.
- [ ] Gemini — <https://gemini.google.com>. Sign in with your Google account. Mobile: iOS App Store / Google Play, search "Google Gemini".
- [ ] Perplexity — <https://www.perplexity.ai> → look for the Download link.

## 4. Tools

### 4.1 Python 3.12 (or 3.11)

- [ ] Download — <https://www.python.org/downloads/>. Use 3.12.x or 3.11.x. Do not use 3.10 or earlier.

**macOS**
- [ ] Double-click the `.pkg` and follow the prompts.
- [ ] Verify: `python3 --version` → `Python 3.12.x` or `3.11.x`.

**Windows**
- [ ] On the **first installer screen**, tick **"Add python.exe to PATH"** before clicking Install. (It is unchecked by default.)
- [ ] Verify: `python --version` → `Python 3.12.x` or `3.11.x`.

### 4.2 Postgres 17

**macOS**
- [ ] `brew install postgresql@17`
- [ ] `brew services start postgresql@17`
- [ ] `psql -d postgres -c "CREATE USER postgres WITH PASSWORD 'postgres' SUPERUSER;"`
- [ ] Verify: `pg_isready -h localhost` → `accepting connections`

**Windows**
- [ ] Download EnterpriseDB installer — <https://www.enterprisedb.com/downloads/postgres-postgresql-downloads>. Pick **17.x** (do not pick 18).
- [ ] Run the installer. When prompted for the `postgres` superuser password, enter `postgres`.
- [ ] At the end, close "Stack Builder" without selecting anything.
- [ ] Add Postgres to your User PATH:
  - Open Windows Settings → System → About → Advanced system settings → **Environment Variables**.
  - Under **User variables**, click the row called `Path` and click **Edit** (do NOT click **New** — that creates a separate variable).
  - Click **New** in the edit dialog and add `C:\Program Files\PostgreSQL\17\bin`.
  - Click OK on every dialog to save.
  - Close every open PowerShell window and reopen one fresh.
- [ ] Verify in the fresh PowerShell window: `pg_isready -h localhost` → `accepting connections`

### 4.3 Ollama + the `llama3.2` model

- [ ] Install Ollama — <https://ollama.com/download>
  - **macOS:** download the `.dmg`, drag to Applications. Requires macOS 14 Sonoma or later.
  - **Windows:** download and run the `.exe` installer.
- [ ] Pull the model (≈ 2 GB download):
  ```bash
  ollama pull llama3.2
  ```
- [ ] Verify:
  ```bash
  curl -s -X POST http://localhost:11434/api/chat \
    -H "Content-Type: application/json" \
    -d '{"model":"llama3.2","messages":[{"role":"user","content":"hi"}],"stream":false}' \
    | head -3
  ```
  Expected: a JSON response with a `message` field.

### 4.4 Git

**macOS**
- [ ] Pre-installed. Verify: `git --version`.

**Windows**
- [ ] Download — <https://git-scm.com/download/win>
- [ ] Run the installer. Accept defaults EXCEPT at the **"Adjusting your PATH environment"** screen — pick the **middle option** ("Git from the command line and also from 3rd-party software").

### 4.5 GitHub CLI (`gh`)

This is the tool Antigravity uses to authenticate to GitHub for push and pull.

**macOS**
- [ ] `brew install gh`
- [ ] Verify: `gh --version`

**Windows**
- [ ] In PowerShell (run as a normal user): `winget install --id GitHub.cli`
  - Or download the `.msi` installer from <https://cli.github.com/>
- [ ] Close every open PowerShell window and reopen one fresh.
- [ ] Verify: `gh --version`

## 5. Google Antigravity (IDE)

### 5.1 Install and sign in

- [ ] Download — <https://antigravity.google>
- [ ] Install. Requires macOS 12+ or Windows 10+.
- [ ] Sign in with your Google account.
- [ ] In the right-hand chat panel, type `hello` and press Enter. Confirm Gemini replies.

### 5.2 Connect Antigravity to GitHub (so Gemini can push and pull from chat)

- [ ] Open Antigravity's **integrated terminal** — top menu **View → Terminal**, or keyboard `Ctrl+` `` ` `` (backtick).
- [ ] In the integrated terminal, run:
  ```bash
  gh auth login
  ```
- [ ] Answer the interactive prompts in this exact order:
  - **What account do you want to log into?** → `GitHub.com`
  - **What is your preferred protocol for Git operations on this host?** → `HTTPS`
  - **Authenticate Git with your GitHub credentials?** → `Yes`
  - **How would you like to authenticate GitHub CLI?** → `Login with a web browser`
- [ ] The terminal prints an **8-character one-time code** (e.g. `XXXX-XXXX`). Copy it.
- [ ] A browser tab opens at <https://github.com/login/device>. If it does not open automatically, open the URL manually in your browser.
- [ ] Paste the 8-character code in the browser. Click **Continue**.
- [ ] Approve the permissions GitHub requests.
- [ ] Your phone buzzes — open the GitHub mobile app and tap **Approve**.
- [ ] Back in the Antigravity terminal, you should see `✓ Authentication complete` and `✓ Configured git protocol`.

After this, `git push` from Antigravity's terminal (and Gemini-driven git commands from the chat panel) work without further prompts. ([source](https://cli.github.com/manual/gh_auth_login), [source](https://antigravitylab.net/en/articles/tips/antigravity-git-ssh-github-authentication-fix))

### 5.3 Confirm Gemini can push code from chat

- [ ] In your terminal (outside Antigravity), create a sandbox:
  ```bash
  mkdir ~/antigravity-test
  cd ~/antigravity-test
  echo "hello" > note.txt
  git init
  git add .
  git commit -m "first"
  ```
  Windows (PowerShell): replace `~` with `$HOME`.
- [ ] Open the `antigravity-test` folder in Antigravity (**File → Open Folder**).
- [ ] In the Gemini chat panel, paste exactly:
  > *"Add a line 'world' to note.txt, commit the change, create a new public GitHub repo for this folder under my account, and push."*
- [ ] Gemini should run the commands directly in the integrated terminal — `gh repo create`, `git remote add`, `git push -u origin main`.
- [ ] Open your GitHub profile in a browser. Confirm the new `antigravity-test` repo exists with two commits.
- [ ] If Gemini only prints commands as text for you to copy-paste instead of running them, message the instructor before class.
- [ ] (Optional cleanup) Delete the test repo afterward: `gh repo delete <your-username>/antigravity-test --yes`

## 6. Clone the cohort repo and verify

### 6.1 Pick a path

**macOS / Linux**
- [ ] Any reasonable location, e.g. `~/code/` or `~/dev/`.

**Windows**
- [ ] Use a short, OneDrive-free path. Do NOT clone into `Documents`, `Desktop`, or anywhere under `OneDrive`.
- [ ] Create `C:\dev\` (or `C:\code\`) if it doesn't exist:
  ```powershell
  mkdir C:\dev
  cd C:\dev
  ```

### 6.2 Clone + database + verify

- [ ] Clone:
  ```bash
  git clone https://github.com/SwarupSG/fastapi-ollama-postgres-cohort.git
  cd fastapi-ollama-postgres-cohort
  ```
  When git prompts you to authenticate, your phone will buzz — approve in the GitHub mobile app.
- [ ] Create the database:
  - macOS / Linux: `createdb llm_question_log`
  - Windows (PowerShell): `createdb -U postgres llm_question_log`
- [ ] Apply the schema (both platforms):
  ```bash
  psql -d llm_question_log -f sql/001_create_interactions.sql
  ```
- [ ] Run the verify script:
  - macOS / Linux: `./scripts/verify_setup.sh`
  - Windows: `.\scripts\verify_setup.ps1`
- [ ] Confirm 8 green ✓ lines ending with **"All checks passed. You're ready for Module 1."**

### 6.3 🧸 Bedtime cohort repo

- [ ] From the same parent folder you used in §6.1 (e.g. `~/code/` on macOS, `C:\dev\` on Windows), clone the bedtime cohort:
  ```bash
  git clone https://github.com/SwarupSG/bedtime-story-generator-cohort.git
  cd bedtime-story-generator-cohort
  ```
- [ ] Bedtime-specific setup (database, schema, `.env` file, Gemini API key) is covered in the first bedtime session — no further action required pre-class beyond §1–§5 above.

## 7. 🧸 Gemini API key (done together in class)

Reference only — created live in the first bedtime session.

1. Open <https://aistudio.google.com/apikey>.
2. Sign in with the same Google account you used for Antigravity.
3. Accept the Terms of Service. AI Studio creates a default Google Cloud project and an API key in one step. No billing setup needed for free-tier use.
4. Copy the key. It starts with `AIza...`.
5. Save it in a password manager. Do not paste it into chats, take screenshots of it, or commit it to a public repo.
6. Verify the key works (substitute `<YOUR_KEY>`):
   ```bash
   curl -s "https://generativelanguage.googleapis.com/v1beta/models?key=<YOUR_KEY>" | head -5
   ```
   Expected: a JSON list of models.
7. Free-tier rate limits for your account — <https://aistudio.google.com/rate-limit>.

## 8. 🧸 Connect Render and Vercel to GitHub

### Render ↔ GitHub

- [ ] Sign in — <https://dashboard.render.com>
- [ ] Top right: **+ New** → **Web Service**.
- [ ] Click the **GitHub** card → approve the OAuth permissions.
- [ ] Back out (no deploy yet).

### Vercel ↔ GitHub

- [ ] Sign in — <https://vercel.com/dashboard>
- [ ] Top right: **Add New** → **Project**.
- [ ] Click **Install** under the GitHub heading → approve the OAuth permissions.
- [ ] Back out (no project yet).

## 9. Final check (night before the first session)

Run all five. All must pass.

- [ ] `python --version` (Windows) or `python3 --version` (macOS) → `3.11.x` or `3.12.x`
- [ ] `pg_isready -h localhost` → `accepting connections`
- [ ] Ollama smoke curl (from §4.3) → JSON response with a `message` field
- [ ] From inside your cohort clone: `./scripts/verify_setup.sh` (macOS) or `.\scripts\verify_setup.ps1` (Windows) → 8 green ✓
- [ ] Open the cohort folder in Antigravity. Type `what's in this folder?` in the Gemini chat panel. Gemini replies with a directory listing.

## 10. If anything fails

1. Open the cohort folder in Antigravity. Paste the failing command and its error into the Gemini chat panel. Gemini has `AGENTS.md` loaded and will walk you through the fix.
2. If Gemini's fix doesn't work, post a screenshot of the failing command and error in the cohort async help channel.
3. The live session is the last resort. Arrive ready.
