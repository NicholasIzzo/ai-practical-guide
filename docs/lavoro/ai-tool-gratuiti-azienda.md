# 🆓 AI Tool Gratuiti per l'Azienda

Raccolta di tool AI **completamente gratuiti** (o con piano free sufficiente per uso aziendale) testati e pronti all'uso. Per ogni tool: cosa fa, come si installa, come si usa — a prova di scemo.

> ✅ = Testato | 🆓 = Gratuito | 🇪🇺 = Dati in EU | 🖥️ = Locale (nessun dato inviato)

---

## 📋 Indice

- [Produttività](#-produttività)
  - [Whisper — Trascrizione audio/video](#1-whisper--trascrizione-audiovideo)
  - [tl;dv — Verbali riunioni automatici](#2-tldv--verbali-riunioni-automatici)
  - [ChatGPT Free — Assistente generale](#3-chatgpt-free--assistente-generale)
  - [Claude Free — Analisi documenti e testi](#4-claude-free--analisi-documenti-e-testi)
  - [Notion AI Free — Knowledge base](#5-notion-ai-free--knowledge-base)
  - [Google Gemini Free — Suite Google](#6-google-gemini-free--suite-google)
  - [Perplexity Free — Ricerca con fonti](#7-perplexity-free--ricerca-con-fonti)
- [Coding e Sviluppo](#-coding-e-sviluppo)
  - [GitHub Copilot Free — Completamento codice](#1-github-copilot-free--completamento-codice)
  - [Codeium — Alternativa Copilot gratuita](#2-codeium--alternativa-copilot-gratuita)
  - [Cursor Free — Editor AI](#3-cursor-free--editor-ai)
  - [Continue.dev — AI locale nel tuo IDE](#4-continuedev--ai-locale-nel-tuo-ide)
  - [Ollama — LLM locale sul PC](#5-ollama--llm-locale-sul-pc)

---

## 📝 Produttività

---

### 1. Whisper — Trascrizione audio/video

| | |
|---|---|
| **Costo** | 🆓 Gratuito |
| **Dati** | 🖥️ Locale — nessun dato inviato |
| **Ideale per** | Verbali riunioni, trascrizione interviste, sottotitoli video |

**Cosa fa:**
Trascrive qualsiasi file audio o video in testo, con supporto eccellente per l'italiano. Gira sul tuo PC, nessun dato esce dall'azienda.

**Installazione (Windows):**

1. Installa Python da [python.org](https://python.org) — spunta "Add to PATH" durante l'installazione
2. Apri il Prompt dei comandi (CMD) come amministratore
3. Esegui:
```bash
pip install openai-whisper
pip install ffmpeg-python
```
4. Scarica FFmpeg da [ffmpeg.org](https://ffmpeg.org/download.html) e aggiungilo al PATH

**Utilizzo base:**
```bash
# Trascrivi un file audio
whisper riunione.mp3 --language it

# Trascrivi con output in formato testo
whisper riunione.mp3 --language it --output_format txt

# Trascrivi un video
whisper presentazione.mp4 --language it --output_format txt
```

**Risultato:** viene creato un file `riunione.txt` con la trascrizione completa.

**Alternativa ancora più semplice — Whisper Desktop (GUI):**
- Scarica [Whisper Desktop](https://github.com/Const-me/Whisper/releases) — nessuna installazione, trascina il file e avvia.

---

### 2. tl;dv — Verbali riunioni automatici

| | |
|---|---|
| **Costo** | 🆓 Piano free: riunioni illimitate |
| **Dati** | 🇪🇺 Server EU disponibile |
| **Ideale per** | Verbali automatici, action items, clip condivisibili |

**Cosa fa:**
Si unisce automaticamente alle tue call Zoom e Google Meet, registra, trascrive e genera un riassunto con action items. Il piano gratuito è sufficiente per uso quotidiano.

**Installazione:**

1. Vai su [tldv.io](https://tldv.io)
2. Clicca **Sign up free** — accedi con Google o email aziendale
3. Collega il tuo calendario Google o Outlook
4. Installa l'estensione Chrome quando richiesto

**Utilizzo:**

1. Pianifica una riunione su Google Meet o Zoom normalmente
2. tl;dv si unisce automaticamente come partecipante "tl;dv Notetaker"
3. A fine call ricevi email con:
   - Trascrizione completa
   - Riassunto AI con punti chiave
   - Action items estratti automaticamente
   - Clip selezionabili da condividere

**Impostazione EU:**
- Vai su Settings → Data Processing → seleziona **EU servers**

---

### 3. ChatGPT Free — Assistente generale

| | |
|---|---|
| **Costo** | 🆓 Piano free con GPT-4o mini |
| **Dati** | ⚠️ Server USA — non inserire dati aziendali riservati |
| **Ideale per** | Email, testi, brainstorming, riassunti, FAQ |

**Cosa fa:**
Assistente AI generale. Eccellente per scrivere email professionali, riassumere testi, rispondere a domande, generare idee.

**Installazione:**

1. Vai su [chat.openai.com](https://chat.openai.com)
2. Clicca **Sign up** — registrazione con email
3. Nessuna installazione richiesta — funziona da browser

**Utilizzo — Esempi pratici:**

```
# Scrivi un'email professionale
"Scrivi un'email professionale per comunicare al cliente 
Rossi SRL un ritardo nella consegna di 3 giorni. 
Tono: formale ma empatico."

# Riassumi un documento
"Riassumi questo testo in 5 punti chiave: [incolla testo]"

# Genera una FAQ
"Crea una FAQ di 10 domande frequenti per un software 
di gestione presenze aziendali"

# Correggi e migliora un testo
"Correggi grammatica e stile di questo testo, 
mantieni il significato: [incolla testo]"
```

**Regola d'oro:** Non incollare mai dati di clienti, contratti, codice sorgente proprietario o informazioni riservate. Usa dati fittizi negli esempi.

---

### 4. Claude Free — Analisi documenti e testi

| | |
|---|---|
| **Costo** | 🆓 Piano free con Claude Sonnet |
| **Dati** | ⚠️ Server USA — non inserire dati riservati |
| **Ideale per** | Analisi PDF, testi lunghi, documentazione tecnica |

**Cosa fa:**
Simile a ChatGPT ma superiore nell'analisi di documenti lunghi e nella scrittura tecnica. Il piano gratuito permette di caricare PDF.

**Installazione:**

1. Vai su [claude.ai](https://claude.ai)
2. Clicca **Sign up** — registrazione con email
3. Funziona da browser, nessuna installazione

**Utilizzo — Esempi pratici:**

```
# Analizza un PDF (carica il file con il bottone allegati)
"Analizza questo documento e dimmi:
1. Punti principali
2. Eventuali criticità
3. Azioni raccomandate"

# Scrivi documentazione tecnica
"Scrivi la documentazione utente per questa procedura: 
[descrivi la procedura]"

# Revisiona un contratto (senza dati reali)
"Analizza questo tipo di clausola contrattuale e 
spiega i rischi potenziali: [incolla clausola anonimizzata]"
```

**Differenza con ChatGPT:** Claude è migliore con testi molto lunghi e mantiene meglio il contesto in conversazioni complesse.

---

### 5. Notion AI Free — Knowledge base

| | |
|---|---|
| **Costo** | 🆓 Piano free Notion (AI limitata, 20 usi/mese) |
| **Dati** | ⚠️ Server USA |
| **Ideale per** | Wiki aziendale, note riunioni, SOP, documentazione |

**Cosa fa:**
Notion è uno spazio di lavoro collaborativo. L'AI integrata aiuta a generare testo, riassumere note e creare strutture di documenti.

**Installazione:**

1. Vai su [notion.so](https://notion.so)
2. Clicca **Get Notion free**
3. Crea un workspace per il team
4. Invita i colleghi via email

**Utilizzo AI in Notion:**

1. In qualsiasi pagina, scrivi `/AI` per aprire il menu AI
2. Oppure seleziona del testo → clicca **Ask AI**

```
Comandi utili:
- "Scrivi un verbale di riunione per questi punti: ..."
- "Crea una SOP per questa procedura: ..."
- "Riassumi questa pagina"
- "Trasforma questi appunti in un documento strutturato"
- "Genera una checklist per questo processo"
```

**Template utili gratuiti:**
- Meeting notes → `/template` → Meeting notes
- Project tracker → `/template` → Project
- Wiki aziendale → `/template` → Company Wiki

---

### 6. Google Gemini Free — Suite Google

| | |
|---|---|
| **Costo** | 🆓 Gratuito con account Google |
| **Dati** | 🇪🇺 Con Google Workspace aziendale |
| **Ideale per** | Integrazione Gmail, Docs, Drive, Fogli |

**Cosa fa:**
AI di Google integrata in tutti i prodotti Google. Se l'azienda usa Gmail e Google Workspace, è la scelta più naturale.

**Installazione:**

1. Vai su [gemini.google.com](https://gemini.google.com)
2. Accedi con il tuo account Google
3. Per integrazione in Gmail/Docs: l'AI è già presente se hai Workspace

**Utilizzo in Gmail:**
- Apri una email → clicca **Aiutami a scrivere** (icona stellina ✨)
- Scrivi cosa vuoi comunicare → genera la bozza

**Utilizzo in Google Docs:**
- Apri un documento → clicca **Aiutami a scrivere** in alto
- Oppure digita `@Gemini` in qualsiasi punto del documento

**Utilizzo in Google Fogli:**
- Clicca su una cella → **Inserisci → Smart chip → @ Gemini**
- Utile per: analisi dati, formule complesse, spiegazioni

---

### 7. Perplexity Free — Ricerca con fonti

| | |
|---|---|
| **Costo** | 🆓 Piano free generoso |
| **Dati** | ⚠️ Server USA |
| **Ideale per** | Ricerca rapida con fonti verificabili, analisi mercato |

**Cosa fa:**
Motore di ricerca AI che risponde con fonti citate. Perfetto quando hai bisogno di informazioni aggiornate con riferimenti verificabili.

**Installazione:**

1. Vai su [perplexity.ai](https://perplexity.ai)
2. Usa senza registrazione oppure Sign up per salvare la cronologia

**Utilizzo:**

```
Esempi di ricerche utili in azienda:
- "Quali sono le normative GDPR aggiornate 2025 per le PMI italiane?"
- "Confronto tra i principali software ERP per aziende 50-100 dipendenti"
- "Come configurare SPF DKIM DMARC per un dominio aziendale"
- "Ultime vulnerabilità CVE per [nome software]"
```

**Vantaggio rispetto a ChatGPT:** mostra sempre le fonti, utile per ricerche che richiedono dati verificabili.

---

## 💻 Coding e Sviluppo

---

### 1. GitHub Copilot Free — Completamento codice

| | |
|---|---|
| **Costo** | 🆓 Piano free: 2000 completamenti/mese, 50 chat/mese |
| **Dati** | ⚠️ Server USA/GitHub |
| **Ideale per** | Completamento codice, spiegazioni, generazione funzioni |

**Cosa fa:**
Suggerisce codice in tempo reale mentre scrivi. Genera funzioni da commenti, spiega codice esistente, aiuta con il debug.

**Installazione in VS Code:**

1. Scarica [VS Code](https://code.visualstudio.com) se non ce l'hai
2. Vai su Extensions (Ctrl+Shift+X)
3. Cerca **GitHub Copilot** → Install
4. Accedi con il tuo account GitHub quando richiesto
5. Se non hai account GitHub: [github.com](https://github.com) → Sign up (gratuito)

**Attivazione piano free:**
1. Vai su [github.com/settings/copilot](https://github.com/settings/copilot)
2. Clicca **Enable Copilot** → seleziona **Free plan**

**Utilizzo:**

```python
# Scrivi un commento e Copilot genera il codice
# Funzione che legge un file CSV e restituisce una lista di dizionari
def leggi_csv(percorso):
    # Copilot completa automaticamente qui
```

**Shortcut utili in VS Code:**
- `Tab` → accetta il suggerimento
- `Esc` → rifiuta il suggerimento
- `Alt+]` → suggerimento successivo
- `Ctrl+I` → apri chat Copilot inline

---

### 2. Codeium — Alternativa Copilot gratuita

| | |
|---|---|
| **Costo** | 🆓 Completamente gratuito (illimitato) |
| **Dati** | ⚠️ Server USA |
| **Ideale per** | Chi vuole Copilot senza limiti mensili |

**Cosa fa:**
Identico a GitHub Copilot ma senza limiti di utilizzo nel piano gratuito. Supporta 70+ linguaggi e tutti i principali IDE.

**Installazione in VS Code:**

1. Vai su Extensions (Ctrl+Shift+X)
2. Cerca **Codeium** → Install
3. Vai su [codeium.com](https://codeium.com) → Sign up gratuito
4. Copia il token API → incollalo in VS Code quando richiesto

**Installazione in JetBrains (IntelliJ, PyCharm, ecc.):**
1. File → Settings → Plugins → Marketplace
2. Cerca **Codeium** → Install → Restart IDE
3. Accedi con le credenziali codeium.com

**Utilizzo:** identico a Copilot — suggerimenti automatici mentre scrivi.

---

### 3. Cursor Free — Editor AI avanzato

| | |
|---|---|
| **Costo** | 🆓 Piano free: 2000 completamenti, 50 richieste lente/mese |
| **Dati** | ⚠️ Server USA |
| **Ideale per** | Chat con il codice, refactoring, debug conversazionale |

**Cosa fa:**
Editor basato su VS Code con AI profonda integrata. Puoi fare domande sul codice in linguaggio naturale, chiedere refactoring, far spiegare blocchi complessi.

**Installazione:**

1. Vai su [cursor.com](https://cursor.com)
2. Clicca **Download** → scegli Windows/Mac/Linux
3. Installa come una normale applicazione
4. Le tue estensioni VS Code vengono importate automaticamente

**Utilizzo — Comandi principali:**

```
Ctrl+K  → Genera o modifica codice selezionato
Ctrl+L  → Apri chat con il codice del progetto
Ctrl+I  → Composer (modifica multipli file)

Esempi di prompt:
- "Spiega cosa fa questa funzione"
- "Refactora questo codice per renderlo più leggibile"  
- "Trova il bug in questo blocco"
- "Scrivi i test unitari per questa funzione"
- "Converti questa funzione da Python 2 a Python 3"
```

---

### 4. Continue.dev — AI locale nel tuo IDE

| | |
|---|---|
| **Costo** | 🆓 Open source, completamente gratuito |
| **Dati** | 🖥️ Locale con Ollama — nessun dato inviato |
| **Ideale per** | Aziende con requisiti privacy, codice proprietario sensibile |

**Cosa fa:**
Estensione VS Code/JetBrains che connette il tuo IDE a modelli AI locali (via Ollama) o cloud. Con Ollama il codice non lascia mai il PC.

**Installazione:**

1. Installa prima **Ollama** (vedi sezione successiva)
2. In VS Code: Extensions → cerca **Continue** → Install
3. Continue si configura automaticamente con Ollama se installato

**Configurazione manuale** (`~/.continue/config.json`):
```json
{
  "models": [
    {
      "title": "Llama 3.1 locale",
      "provider": "ollama",
      "model": "llama3.1"
    }
  ]
}
```

**Utilizzo:** identico a Copilot/Codeium ma tutto gira in locale.

---

### 5. Ollama — LLM locale sul PC

| | |
|---|---|
| **Costo** | 🆓 Open source, gratuito |
| **Dati** | 🖥️ 100% locale — nessun dato inviato |
| **Ideale per** | Aziende con dati sensibili, air-gapped, compliance GDPR stretta |

**Cosa fa:**
Esegue modelli AI (Llama, Mistral, Gemma, ecc.) direttamente sul tuo PC. Nessun dato lascia l'azienda. Richiede almeno 8GB RAM, meglio 16GB.

**Installazione (Windows):**

1. Vai su [ollama.com](https://ollama.com)
2. Clicca **Download** → scarica il file `.exe`
3. Installa normalmente
4. Apri il Prompt dei comandi e scarica un modello:

```bash
# Modello leggero (4GB RAM) — buono per coding
ollama pull llama3.2

# Modello più capace (8GB RAM) — migliore qualità
ollama pull llama3.1

# Modello specializzato per codice
ollama pull codellama

# Modello italiano ottimizzato
ollama pull mistral
```

**Utilizzo da terminale:**
```bash
# Avvia una chat
ollama run llama3.1

# Chiedi qualcosa
>>> Scrivi una funzione Python che legge un CSV
>>> Spiega questo codice: [incolla codice]
>>> /bye  (per uscire)
```

**Utilizzo con interfaccia grafica (consigliato):**

1. Installa **Open WebUI**:
```bash
docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway \
  -v open-webui:/app/backend/data --name open-webui \
  ghcr.io/open-webui/open-webui:main
```
2. Apri il browser su `http://localhost:3000`
3. Interfaccia identica a ChatGPT ma tutto locale

**Requisiti minimi:**
- RAM: 8GB (per modelli 7B), 16GB (per modelli 13B)
- Disco: 5-10GB per modello
- GPU: opzionale ma accelera notevolmente

---

## 📊 Confronto rapido

| Tool | Categoria | Costo | Privacy | Difficoltà setup |
|------|-----------|-------|---------|-----------------|
| Whisper | Produttività | Gratis | 🖥️ Locale | ⭐⭐⭐ Media |
| tl;dv | Produttività | Gratis | 🇪🇺 EU | ⭐ Facile |
| ChatGPT Free | Produttività | Gratis | ⚠️ USA | ⭐ Facile |
| Claude Free | Produttività | Gratis | ⚠️ USA | ⭐ Facile |
| Notion Free | Produttività | Gratis | ⚠️ USA | ⭐⭐ Media |
| Google Gemini | Produttività | Gratis | 🇪🇺 con WS | ⭐ Facile |
| Perplexity | Produttività | Gratis | ⚠️ USA | ⭐ Facile |
| GitHub Copilot | Coding | Gratis | ⚠️ USA | ⭐⭐ Media |
| Codeium | Coding | Gratis | ⚠️ USA | ⭐⭐ Media |
| Cursor | Coding | Gratis | ⚠️ USA | ⭐ Facile |
| Continue.dev | Coding | Gratis | 🖥️ Locale | ⭐⭐⭐ Media |
| Ollama | Coding | Gratis | 🖥️ Locale | ⭐⭐⭐ Media |

---

## 🔒 Note sulla compliance aziendale

- **Dati riservati** (contratti, dati clienti, codice proprietario): usa solo tool **locali** (Whisper, Ollama, Continue.dev) o tool con **DPA aziendale firmato**
- **Uso generico** (email, testi, brainstorming): ChatGPT Free, Claude Free, Gemini sono accettabili
- **Codice aziendale**: preferisci Codeium con privacy mode o GitHub Copilot Business (a pagamento) per uso enterprise
- Prima di adottare qualsiasi tool in produzione, **verifica sempre con il DPO aziendale**

---

*Guida mantenuta da [Nicholas Izzo](https://github.com/NicholasIzzo) — parte di [ai-practical-guide](https://nicholasizzo.github.io/ai-practical-guide/)*
