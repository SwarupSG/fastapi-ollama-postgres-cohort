# Explain It Yourself — Written Assignment

You've been answering **Defend-It** out loud. This is the short written version.

Every module is really built around **one key line** — the line that *is* the new idea; everything else is scaffolding. **We give you that line for each module. Your job is simply to explain what it does, in your own words** — the way you'd explain it to a classmate who's stuck.

That's the whole assignment: read the line, understand it, explain it. Eight lines, eight short explanations.

> **How this is handed in.** This is a **graded assignment**. Your instructor gives you an editable copy — **`explain_it_yourself.docx`** — on the learning portal. Fill it in (Word, Google Docs, or Pages) and **upload the completed `.docx` back to the portal** as a single submission by the deadline.

---

## What a good explanation looks like

- **In your own words** — don't copy the README back. Explain it like you're helping a classmate.
- **Say what it does *and* why it matters** — what would be missing or broken without this line?
- **2–4 sentences is plenty.** Short and clear beats long.

You may ask Gemini to *check* your explanation ("is this right?") — but write your own version first.

---

## Module 01 — Hello FastAPI

```python
@app.get("/", response_class=HTMLResponse)   # app/main.py
def index(request: Request):
    ...
```

**Your explanation (2–4 sentences):**



## Module 02 — Post + Pydantic Echo

```python
def ask(payload: AskRequest):   # app/main.py
```

*Focus on `payload: AskRequest` — the type written after the colon.*

**Your explanation (2–4 sentences):**



## Module 03 — Call Ollama

```python
r = client.post(OLLAMA_URL, json={"model": OLLAMA_MODEL, "messages": [...], "stream": False})   # app/main.py
```

**Your explanation (2–4 sentences):**



## Module 04 — System Prompt

```python
{"role": "system", "content": SYSTEM_PROMPT},   # app/main.py — added to the messages list
```

**Your explanation (2–4 sentences):**



## Module 05 — Save to Postgres

```python
cur.execute(
    "INSERT INTO interactions (question, answer, model_name) VALUES (%s, %s, %s)",
    (question, answer, OLLAMA_MODEL),
)   # app/main.py
```

**Your explanation (2–4 sentences):**



## Module 06 — Read History

```python
cur.execute(
    "SELECT ... FROM interactions ORDER BY id DESC LIMIT %s",
    (limit,),
)   # app/main.py
```

**Your explanation (2–4 sentences):**



## Module 07 — Refactor into Layers

The app does exactly what Module 6 did — but the `ask` function became tiny:

```python
answer = call_ollama(question)        # app/main.py
save_interaction(question, answer)
```

*Nothing the app DOES changed. Explain what changed instead — and why that's worth doing.*

**Your explanation (2–4 sentences):**



## Module 08 — Configuration

```python
DATABASE_URL = os.environ["DATABASE_URL"]   # app/database.py
```

**Your explanation (2–4 sentences):**



---

**Submitting — one upload, all eight modules.** When every module is filled in, **upload this completed document (`explain_it_yourself.docx`) to the learning portal** as your single submission. It also doubles as your own revision sheet later — eight lines, the whole app.
