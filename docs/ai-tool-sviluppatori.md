# 🔧 Tool AI per Sviluppatori e Sistemisti

Panoramica dei principali strumenti AI integrati nel workflow di sviluppo e sistemistica.

---

## Coding assistants (in-IDE)

### GitHub Copilot ⭐
Il più diffuso. Si integra direttamente in VS Code, JetBrains, Neovim e altri editor.

**Cosa fa:**
- Completa il codice mentre scrivi
- Suggerisce funzioni intere basandosi sui commenti
- Risponde a domande sul codice selezionato
- Genera test automaticamente
- Spiega codice esistente

**Costo:** ~10€/mese (incluso in GitHub Education per studenti — **gratis**)

**Attivare GitHub Education:**
Se sei studente universitario puoi ottenere GitHub Copilot gratis tramite [education.github.com](https://education.github.com)

---

### Cursor
Editor basato su VS Code con AI profondamente integrata. Considerato il più potente per il coding AI-assisted.

**Cosa fa in più rispetto a Copilot:**
- Chat con il codice dell'intero progetto come contesto
- Modifica file multipli in una sola istruzione
- Comprende tutta la codebase, non solo il file aperto
- Supporta Claude, GPT-4o e altri modelli

**Costo:** Piano gratuito limitato, ~20€/mese per uso intensivo

---

### Codeium
Alternativa gratuita a GitHub Copilot.

**Cosa fa:**
- Completamento codice simile a Copilot
- Chat con il codice
- Supporto per 70+ linguaggi

**Costo:** Gratis per uso personale

---

## AI per la riga di comando

### Warp Terminal
Terminal con AI integrata. Spiega i comandi, suggerisce cosa fare e debugga direttamente nel terminale.

```
Warp AI: "how do I find all files modified in the last 24 hours?"
→ find . -mtime -1 -type f
```

---

### Shell AI (shell_gpt)
Tool da riga di comando che porta l'AI direttamente nella shell.

```bash
pip install shell-gpt

# Genera un comando
sgpt "trova tutti i file .log più vecchi di 30 giorni in /var/log"
→ find /var/log -name "*.log" -mtime +30

# Esegui direttamente
sgpt --shell "trova tutti i container Docker fermi"
```

---

## AI per documentazione

### Mintlify Doc Writer
Genera automaticamente docstring e commenti per il codice selezionato.

---

### Swimm
Documentazione tecnica che si aggiorna automaticamente quando cambia il codice.

---

## AI per il browser

### Claude / ChatGPT Web
Per uso quotidiano — spiegazioni, documentazione, debug veloce senza aprire l'IDE.

### Perplexity
Motore di ricerca AI. Migliore di Google per domande tecniche specifiche — fornisce risposte con fonti citate.

```
Esempio query Perplexity:
"docker compose healthcheck options 2024"
→ Risposta diretta con esempi, non una lista di link
```

---

## Integrazione AI nelle pipeline

### GitHub Actions + AI
Puoi integrare l'AI nelle GitHub Actions per:
- Code review automatica delle Pull Request
- Generazione automatica di release notes
- Test coverage analysis

```yaml
# Esempio: PR review automatica
- name: AI Code Review
  uses: anc95/ChatGPT-CodeReview@main
  env:
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
    OPENAI_API_KEY: ${{ secrets.OPENAI_API_KEY }}
```

---

### API OpenAI / Anthropic in script Python

```python
import anthropic

client = anthropic.Anthropic(api_key="<API_KEY>")

message = client.messages.create(
    model="claude-sonnet-4-20250514",
    max_tokens=1024,
    messages=[
        {
            "role": "user",
            "content": "Analizza questo log Docker e dimmi se ci sono errori critici: ..."
        }
    ]
)

print(message.content[0].text)
```

**Caso d'uso pratico:** Script che analizza automaticamente i log dei container ogni notte e invia un report su Discord.

---

## Tabella riassuntiva

| Tool | Tipo | Costo | Migliore per |
|---|---|---|---|
| GitHub Copilot | IDE plugin | ~10€/mese (gratis studenti) | Completamento codice quotidiano |
| Cursor | Editor | Gratuito + piani a pagamento | Progetti complessi, refactoring |
| Codeium | IDE plugin | Gratuito | Alternativa gratuita a Copilot |
| Warp | Terminal | Gratuito | Comandi shell con AI |
| shell_gpt | CLI tool | Gratuito (API key) | Automazione da terminale |
| Perplexity | Web | Gratuito + Pro | Ricerca tecnica con fonti |
| Claude Web | Web | Gratuito + Pro | Chat, documentazione, debug |
| Ollama | Locale | Gratuito | Privacy, automazioni, offline |

---

## Setup consigliato per un sistemista

```
Editor:     VS Code + GitHub Copilot (o Cursor)
Terminal:   Warp (o shell_gpt per automazioni)
Ricerca:    Perplexity per domande tecniche
Chat:       Claude per documentazione e ragionamento
Locale:     Ollama per dati sensibili e automazioni
```

---

> 💡 Non cercare il tool perfetto — scegli 2-3 strumenti e impara a usarli bene. La produttività arriva dalla familiarità con pochi tool eccellenti, non dall'avere tutti i tool installati.
