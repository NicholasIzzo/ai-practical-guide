# AI a lavoro — Tool pratici e casi d'uso reali

> L'AI non sostituisce il tuo lavoro. Elimina le parti noiose di esso.

Questa guida raccoglie i tool AI più utili in ambito lavorativo, con casi d'uso concreti, confronto tra piani gratuiti e a pagamento, e — soprattutto — flussi di lavoro completi che puoi applicare da subito.

---

## 1. Call e riunioni

Le riunioni sono il posto dove le ore di lavoro vanno a morire. L'AI può trascrivere, riassumere e estrarre i punti d'azione in automatico — senza che tu debba prendere appunti.

### Whisper (OpenAI) — locale e gratuito

Whisper è il modello di trascrizione vocale di OpenAI, open source e utilizzabile in locale. Non manda nulla al cloud, funziona su qualsiasi lingua incluso l'italiano.

**Come si usa:**
```bash
pip install openai-whisper
whisper riunione.mp3 --language Italian --model medium
```

**Output:** file `.txt` e `.srt` con la trascrizione completa.

**Caso d'uso:** Registri la call con OBS o con il registratore del telefono, esegui Whisper, ottieni la trascrizione in 2-3 minuti. Poi la incolli in Claude o ChatGPT e chiedi il riassunto.

**Limite:** richiede un minimo di setup tecnico. Non è un'app con interfaccia grafica.

**Piano:** gratuito, open source, gira in locale.

---

### Otter.ai

Servizio web che si collega direttamente a Google Meet, Zoom e Microsoft Teams. Trascrive in tempo reale durante la call e genera automaticamente un riassunto con i punti chiave.

**Caso d'uso:** entri in una call di lavoro, Otter partecipa come bot silenzioso, al termine hai trascrizione + riassunto + action items pronti.

**Piano gratuito:** 300 minuti al mese, trascrizione in tempo reale, riassunti base.
**Piano Pro:** ~17€/mese, minuti illimitati, integrazione calendario, esportazione.

**Limite:** il bot che entra in call può dare fastidio ad alcuni partecipanti. La qualità sull'italiano è buona ma non perfetta.

---

### tl;dv

Simile a Otter ma con un focus più forte sui momenti chiave — puoi "clippare" parti della trascrizione e condividerle come snippet.

**Caso d'uso:** hai una call con un cliente, tl;dv registra e ti permette di taggare i momenti importanti durante la riunione stessa. Utile per non dover riascoltare tutto.

**Piano gratuito:** registrazioni illimitate su Zoom e Google Meet, trascrizioni in 30+ lingue.
**Piano Pro:** ~20€/mese, riassunti AI avanzati, integrazioni CRM.

---

### Fireflies.ai

Il più completo della categoria — trascrizione, riassunto, ricerca full-text su tutte le call passate, integrazioni con Slack, Notion, HubSpot.

**Piano gratuito:** trascrizioni illimitate, storage limitato, riassunti base.
**Piano Business:** ~19€/mese per utente.

**Limite:** il piano gratuito ha storage ridotto, non adatto a chi fa molte call al giorno.

---

## 2. Documenti e testi

### Riassumere PDF lunghi

Hai un documento di 80 pagine da leggere entro domani. Con l'AI ci metti 5 minuti.

**Con Claude:**
1. Carica il PDF direttamente nella chat
2. Chiedi: *"Riassumi questo documento in massimo 10 punti chiave. Per ogni punto indica la pagina di riferimento."*
3. Se vuoi approfondire: *"Dimmi di più sul punto 4, cosa dice esattamente?"*

**Con ChatGPT:**
Stesso flusso — supporta upload PDF diretto nei piani gratuiti e a pagamento.

**Con Copilot (Microsoft 365):**
Se il PDF è in SharePoint o OneDrive, Copilot lo legge direttamente dall'interno di Word o Teams.

---

### Gestire email

**Caso d'uso 1 — rispondere a email complesse:**
Copi il testo dell'email ricevuta, incolli in Claude con il prompt: *"Scrivi una risposta professionale a questa email. Tono: diretto ma cordiale. Obiettivo: chiedere una proroga di 3 giorni."*

**Caso d'uso 2 — riassumere thread lunghi:**
Copi l'intero thread email e chiedi: *"Riassumi questa conversazione in 5 righe. Qual è il punto aperto che richiede una mia risposta?"*

**Caso d'uso 3 — scrivere email da zero:**
*"Scrivi un'email a un cliente per comunicare un ritardo nella consegna del progetto. Il ritardo è di 1 settimana. Motivo: problemi tecnici imprevisti. Tono: professionale, trasparente, propositivo."*

---

### Analizzare report e dati

Se hai un CSV o un foglio Excel con dati, puoi caricarlo in ChatGPT (Advanced Data Analysis) o Claude e chiedere analisi, grafici e interpretazioni in linguaggio naturale.

**Caso d'uso:** *"Ho allegato il report vendite del trimestre. Quali prodotti hanno avuto il calo maggiore? Quali correlazioni vedi con il periodo dell'anno?"*

---

## 3. Codice e automazione

### GitHub Copilot

Si integra direttamente in VS Code, JetBrains e altri IDE. Completa il codice in tempo reale, genera funzioni da commenti in linguaggio naturale, spiega blocchi di codice esistenti.

**Caso d'uso per sistemisti:**
Scrivi un commento come `# Script bash che monitora l'uso della CPU ogni 5 minuti e manda un alert se supera l'80%` e Copilot genera lo script completo.

**Piano:** gratuito per studenti e open source, ~10€/mese altrimenti.

---

### Cursor

Editor di codice basato su VS Code con AI integrata a livello profondo. Puoi selezionare una parte di codice e chiedergli di riscriverla, spiegarla o debuggarla in linguaggio naturale.

**Caso d'uso:** hai uno script Python che non funziona — selezioni il blocco con l'errore, premi `Ctrl+K` e scrivi *"questo script dovrebbe leggere un CSV e filtrare le righe con valore > 100, ma crasha qui — perché?"*

**Piano:** gratuito con limiti, ~20€/mese per uso intenso.

---

### Claude per documentazione tecnica

Claude è particolarmente bravo a generare documentazione da codice esistente — README, commenti inline, wiki interni.

**Caso d'uso:** *"Leggi questo docker-compose.yml e scrivi una documentazione in italiano che spieghi a un nuovo collega cosa fa ogni servizio, quali porte espone e come avviarlo."*

---

## 4. Flussi di lavoro completi

Qui sta il vero valore — non i tool singoli, ma come si collegano tra loro.

---

### Flusso 1 — Dal meeting al verbale in 10 minuti

**Scenario:** hai una call di lavoro di un'ora con il team.

1. **Durante la call:** avvii la registrazione con OBS (gratuito) o il registratore integrato di Teams/Meet
2. **Dopo la call:** esegui Whisper sulla registrazione → ottieni la trascrizione in `.txt`
3. **In Claude:** incolli la trascrizione e chiedi:
   *"Genera un verbale professionale da questa trascrizione. Includi: partecipanti menzionati, argomenti discussi, decisioni prese, action items con responsabile se citato."*
4. **Risultato:** verbale pronto da inviare in 2 minuti

**Costo:** €0 — Whisper è gratuito, Claude ha piano gratuito.

---

### Flusso 2 — Onboarding documenti aziendali

**Scenario:** sei nuovo in un'azienda o in un progetto e hai 200 pagine di documentazione da leggere.

1. Raccogli tutti i PDF in una cartella
2. Caricali uno alla volta in Claude chiedendo per ognuno: *"Dammi i 5 punti chiave di questo documento in bullet point"*
3. Costruisci un documento riassuntivo personale con tutti i punti raccolti
4. Quando hai una domanda specifica, torna al PDF originale e chiedi a Claude di approfondire

**Tempo risparmiato:** ore di lettura ridotte a decine di minuti.

---

### Flusso 3 — Preparazione a una riunione importante

**Scenario:** hai un meeting con un cliente o un manager su un argomento tecnico complesso.

1. Scrivi in Claude: *"Devo presentare [argomento] a [tipo di pubblico]. Genera 10 domande difficili che potrebbero farmi e le risposte ideali."*
2. Chiedi anche: *"Quali sono i punti deboli di questa proposta? Come potrei rispondere alle obiezioni più comuni?"*
3. Usa le risposte per prepararti — arrivi alla riunione con le contromisure già pronte

---

### Flusso 4 — Automazione report settimanale

**Scenario:** ogni settimana devi scrivere un report sullo stato del tuo lavoro.

1. Tieni un file di testo durante la settimana con appunti veloci — anche disorganizzati
2. Il venerdì incolli tutto in Claude con: *"Trasforma questi appunti in un report settimanale professionale. Struttura: attività completate, problemi riscontrati, prossimi passi."*
3. Rivedi e manda — 5 minuti invece di 30

---

## Tabella di confronto

| Tool | Gratuito | Caso d'uso principale | Limite principale |
|---|---|---|---|
| Whisper | Sì — locale | Trascrizione audio/video | Setup tecnico richiesto |
| Otter.ai | Parziale (300 min/mese) | Call in tempo reale | Bot visibile in call |
| tl;dv | Sì (illimitato base) | Clip e snippet da call | Funzioni avanzate a pagamento |
| Fireflies | Parziale (storage limitato) | Call + integrazioni CRM | Storage ridotto nel free |
| Claude | Sì (con limiti) | Testi, PDF, documentazione | Limite messaggi nel free |
| ChatGPT | Sì (con limiti) | Testi, dati, immagini | GPT-4o limitato nel free |
| GitHub Copilot | Sì (studenti/open source) | Completamento codice in IDE | A pagamento per uso professionale |
| Cursor | Parziale | Coding con AI profonda | Costoso per uso intenso |
| Copilot M365 | No (~30€/mese) | Office, Teams, SharePoint | Solo ecosistema Microsoft |

---

## Conclusione

Il pattern che si ripete in tutti questi flussi è sempre lo stesso: **registra o raccogli → dai in pasto all'AI → rivedi e manda**.

Non devi usare tutti questi tool. Scegli uno per categoria e usalo bene:
- **Call:** Whisper se sei tecnico, tl;dv se vuoi qualcosa di immediato
- **Testi e documenti:** Claude o ChatGPT — entrambi ottimi, prova entrambi
- **Codice:** GitHub Copilot se usi già VS Code, Cursor se vuoi qualcosa di più potente

Il tempo che risparmi nelle prime due settimane ripaga qualsiasi abbonamento.

---

*Guida parte di [AI Practical Guide](https://github.com/NicholasIzzo/ai-practical-guide) — open source, in italiano.*
