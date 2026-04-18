# Greenzone SMM Intelligence — Deploy su Netlify

## Struttura progetto

```
greenzone-smm/
├── index.html                  ← App principale
├── netlify.toml                ← Config Netlify
├── netlify/
│   └── functions/
│       └── claude.js           ← Proxy API (serverless)
└── README.md
```

---

## Setup in 5 minuti

### 1. Carica su GitHub

```bash
git init
git add .
git commit -m "Greenzone SMM Intelligence"
git remote add origin https://github.com/TUO-USERNAME/greenzone-smm.git
git push -u origin main
```

### 2. Collega a Netlify

1. Vai su [netlify.com](https://netlify.com) → **Add new site** → **Import from Git**
2. Seleziona il repo GitHub `greenzone-smm`
3. Build command: *(lascia vuoto)*
4. Publish directory: `.`
5. Clicca **Deploy site**

### 3. Aggiungi la API Key (IMPORTANTE)

1. Nel pannello Netlify vai su **Site configuration** → **Environment variables**
2. Clicca **Add a variable**
3. Key: `ANTHROPIC_API_KEY`
4. Value: `sk-ant-api03-...` *(la tua chiave da console.anthropic.com)*
5. Clicca **Save** poi **Trigger deploy** per riavviare

La chiave è protetta — non compare mai nel codice o nel browser.

---

## Come funziona il proxy

```
Browser → /api/claude → netlify.toml redirect → /.netlify/functions/claude.js
                                                          ↓
                                               api.anthropic.com (server-side)
```

Il file `claude.js` gira su server Netlify (Node.js), legge la API key
dalle variabili d'ambiente e la usa per chiamare Anthropic.
Il browser non vede mai la chiave.

---

## Test

Dopo il deploy, apri la tab **"Analisi Target AI"** nell'app.
Clicca **"Test connessione"** — se compare il banner verde ✓ sei pronto.

---

## Costi stimati

| Utilizzo | Costo |
|----------|-------|
| Netlify hosting + functions | **Gratis** (piano Free: 125K invocazioni/mese) |
| API Anthropic Claude Sonnet | ~€ 0,002 per analisi |

Per uso personale/agenzia il piano gratuito Netlify è più che sufficiente.
