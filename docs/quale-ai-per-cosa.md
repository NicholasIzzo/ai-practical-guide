# 🧠 Quale AI usare per cosa

Guida pratica alla scelta del modello AI giusto in base al caso d'uso. Aggiornata a marzo 2026.

---

## I principali modelli disponibili

| Modello | Azienda | Accesso | Punti di forza |
|---|---|---|---|
| **Claude 3.5 / 3.7** | Anthropic | claude.ai / API | Ragionamento, scrittura, codice, contesti lunghi |
| **GPT-4o** | OpenAI | chatgpt.com / API | Multimodale, ampiamente integrato |
| **Gemini 2.0** | Google | gemini.google.com / API | Integrazione Google, contesti lunghissimi |
| **Llama 3** | Meta | Open source / Ollama | Gratuito, eseguibile in locale |
| **Mistral** | Mistral AI | mistral.ai / API | Leggero, ottimo in locale |
| **DeepSeek R1** | DeepSeek | deepseek.com / API | Ragionamento matematico, open source |
| **GitHub Copilot** | Microsoft/OpenAI | VS Code / IDE | Completamento codice in tempo reale |

---

## Per caso d'uso

### ✍️ Scrittura e documenti
**Migliore: Claude**
- Documenti tecnici, guide, relazioni
- Rispetta il tono e lo stile richiesto
- Gestisce contesti molto lunghi senza perdere coerenza

**Alternativa: GPT-4o**
- Buono per testi creativi e marketing

---

### 💻 Coding e sviluppo
**Migliore: Claude 3.7 / GPT-4o**
- Debug di codice complesso
- Spiegazione di errori
- Refactoring e ottimizzazione

**Per completamento in tempo reale: GitHub Copilot / Cursor**
- Suggerisce codice mentre scrivi
- Integrato direttamente nell'IDE

**Per progetti complessi con ragionamento: DeepSeek R1**
- Eccellente per algoritmi e matematica
- Open source, eseguibile in locale

---

### 🖥️ Sistemistica e IT
**Migliore: Claude**
- Scrittura di script Bash, Python, PowerShell
- Spiegazione di log e errori di sistema
- Documentazione tecnica
- Configurazioni Docker, YAML, nginx

**Vedi anche:** [AI per sistemisti](ai-per-sistemisti.md)

---

### 📊 Analisi dati e ricerca
**Migliore: Gemini 2.0 / GPT-4o**
- Contesti lunghissimi per analizzare documenti
- Integrazione con Google Sheets / Docs
- Upload di file CSV e PDF per analisi

---

### 🎨 Immagini e contenuti multimediali
**Migliore: GPT-4o (con DALL-E) / Midjourney**
- Generazione di immagini
- Analisi di immagini (OCR, descrizione)
- GPT-4o può vedere e descrivere screenshot

---

### 🔒 Privacy e uso offline
**Migliore: Llama 3 / Mistral (via Ollama)**
- Nessun dato inviato a server esterni
- Eseguibile completamente in locale
- Gratuito senza limiti di utilizzo

**Vedi anche:** [AI in locale vs cloud](ai-locale-vs-cloud.md)

---

### 🧮 Matematica e ragionamento logico
**Migliore: DeepSeek R1 / Claude 3.7**
- Problemi matematici complessi
- Ragionamento step-by-step
- Dimostrazione di teoremi

---

### 🌐 Ricerca e informazioni aggiornate
**Migliore: Gemini / GPT-4o con browsing / Claude con web search**
- Informazioni recenti (dopo il knowledge cutoff)
- Ricerca su internet in tempo reale
- Sintesi di articoli e notizie

---

## Tabella riassuntiva

| Caso d'uso | Prima scelta | Alternativa |
|---|---|---|
| Scrittura tecnica | Claude | GPT-4o |
| Debug codice | Claude 3.7 | GPT-4o |
| Coding in IDE | GitHub Copilot | Cursor |
| Sistemistica / script | Claude | GPT-4o |
| Analisi dati / PDF | Gemini 2.0 | GPT-4o |
| Generazione immagini | DALL-E 3 / Midjourney | Stable Diffusion |
| Uso offline / privacy | Llama 3 (Ollama) | Mistral |
| Matematica avanzata | DeepSeek R1 | Claude 3.7 |
| Ricerca web | Gemini / GPT-4o | Claude web search |
| Testi creativi | Claude | GPT-4o |

---

## Consigli pratici

**Non esiste "il modello migliore in assoluto"** — ogni modello ha i suoi punti di forza. La strategia giusta è:

1. Usa **Claude** come modello principale per scrittura, codice e ragionamento
2. Usa **Gemini** quando devi analizzare documenti lunghi o vuoi integrazione Google
3. Usa **Ollama + Llama/Mistral** per task ripetitivi o dati sensibili che non vuoi inviare al cloud
4. Usa **GitHub Copilot** mentre programmi per suggerimenti in tempo reale

---

> ⚠️ I modelli AI evolvono rapidamente — questo documento viene aggiornato periodicamente. Controlla la data dell'ultimo aggiornamento prima di fare scelte importanti.
