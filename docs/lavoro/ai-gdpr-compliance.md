# AI e GDPR: Guida Pratica per Aziende Italiane

> Come usare strumenti di intelligenza artificiale in azienda senza violare il Regolamento Europeo sulla Privacy.  
> Aggiornato al 2025 — include riferimenti all'AI Act UE.

---

## Indice

1. [Il problema reale](#1-il-problema-reale)
2. [Cosa dice il GDPR sull'AI](#2-cosa-dice-il-gdpr-sullai)
3. [Categorie di dati e rischi](#3-categorie-di-dati-e-rischi)
4. [Cloud vs Self-hosted vs Locale](#4-cloud-vs-self-hosted-vs-locale)
5. [Data Processing Agreement (DPA)](#5-data-processing-agreement-dpa)
6. [Analisi dei tool più usati](#6-analisi-dei-tool-più-usati)
7. [AI Act UE 2024 — cosa cambia](#7-ai-act-ue-2024--cosa-cambia)
8. [Checklist pratica per valutare un tool AI](#8-checklist-pratica-per-valutare-un-tool-ai)
9. [Scenari concreti con risposta](#9-scenari-concreti-con-risposta)
10. [Soluzioni consigliate per PMI italiane](#10-soluzioni-consigliate-per-pmi-italiane)

---

## 1. Il problema reale

Le aziende italiane usano ChatGPT, Copilot e Gemini ogni giorno. Spesso senza sapere:

- Dove finiscono i dati inseriti nei prompt
- Se quei dati vengono usati per addestrare i modelli
- Chi è il responsabile del trattamento
- Cosa succede in caso di data breach

Il GDPR non vieta l'uso dell'AI. Ma impone regole precise su **come**, **dove** e **con quali garanzie** i dati personali vengono trattati.

**Il rischio non è teorico.** Il Garante italiano ha già sanzionato OpenAI nel 2023 (blocco temporaneo di ChatGPT) e ha avviato indagini su diversi vendor AI. Le sanzioni GDPR arrivano fino al **4% del fatturato globale annuo** o 20 milioni di euro.

---

## 2. Cosa dice il GDPR sull'AI

Il GDPR (Regolamento UE 2016/679) non menziona esplicitamente l'AI, ma si applica ogni volta che vengono trattati **dati personali** — ovvero qualsiasi informazione che identifica o rende identificabile una persona fisica.

### Principi chiave applicati all'AI

**Liceità del trattamento (Art. 6)**  
Devi avere una base giuridica per trattare dati con uno strumento AI. Le più comuni in ambito aziendale sono:
- Esecuzione di un contratto
- Legittimo interesse (valutato caso per caso)
- Consenso esplicito dell'interessato

**Minimizzazione dei dati (Art. 5.1.c)**  
Invia al modello AI solo i dati strettamente necessari. Se devi riassumere un contratto, non serve mandare anche i dati anagrafici del cliente.

**Limitazione della finalità (Art. 5.1.b)**  
I dati raccolti per uno scopo non possono essere usati per scopi diversi. Se un vendor AI usa i tuoi prompt per addestrare il modello, questo potrebbe violare il principio.

**Trasparenza (Art. 13-14)**  
Se usi AI per prendere decisioni che riguardano dipendenti o clienti, devi informarli.

**Decisioni automatizzate (Art. 22)**  
Le decisioni basate esclusivamente su trattamento automatizzato (inclusa la profilazione) che producono effetti significativi su una persona sono vietate salvo eccezioni. Esempio: rifiutare un CV solo perché un algoritmo lo ha scartato senza revisione umana.

**Accountability (Art. 5.2)**  
Il titolare del trattamento deve essere in grado di dimostrare la conformità. Tieni traccia di quali tool AI usi, con quali dati e con quale base giuridica.

---

## 3. Categorie di dati e rischi

Non tutti i dati hanno lo stesso livello di protezione. Ecco una mappa pratica.

### Dati che NON dovresti mai inviare a un tool AI cloud senza DPA

| Tipo di dato | Esempi | Rischio |
|---|---|---|
| Dati sanitari | Cartelle cliniche, referti, malattie dipendenti | Art. 9 GDPR — categoria speciale, vietato senza consenso esplicito |
| Dati giudiziari | Precedenti penali, contenziosi | Art. 10 GDPR — trattamento riservato |
| Dati finanziari personali | IBAN, buste paga, estratti conto | Alto rischio di data breach |
| Dati biometrici | Riconoscimento facciale, impronte | Categoria speciale Art. 9 |
| Dati di minori | Qualsiasi dato di persone under 18 | Protezione rafforzata |
| Credenziali di accesso | Password, token, chiavi API | Rischio sicurezza immediato |

### Dati a rischio medio (usare con cautela)

| Tipo di dato | Esempi | Cosa fare |
|---|---|---|
| Dati anagrafici clienti | Nome, email, telefono | Anonimizzare prima di inviare |
| Contratti con terzi | NDA, accordi commerciali | Rimuovere nomi e riferimenti identificativi |
| Email interne | Comunicazioni tra dipendenti | Valutare se necessario, informare i dipendenti |
| Dati HR | Valutazioni performance, stipendi | Solo con DPA e base giuridica chiara |

### Dati generalmente sicuri da usare

- Testi generici senza riferimenti a persone fisiche
- Codice sorgente senza credenziali o dati di produzione
- Documenti pubblici o anonimi
- Dati aggregati e statistici non riconducibili a individui
- Contenuti creativi e brainstorming

---

## 4. Cloud vs Self-hosted vs Locale

La scelta dell'architettura è la decisione più importante dal punto di vista GDPR.

### Tool Cloud (ChatGPT, Claude, Gemini, Copilot)

**Come funziona:** i dati vengono inviati ai server del vendor (spesso USA) e processati lì.

**Rischi GDPR:**
- Trasferimento dati extra-UE (Art. 44-49) — richiede garanzie aggiuntive (Standard Contractual Clauses)
- Il vendor diventa responsabile del trattamento — serve DPA firmato
- Alcuni vendor usano i prompt per addestrare i modelli (controlla sempre le impostazioni)
- In caso di breach, notifica entro 72h al Garante (Art. 33)

**Quando è accettabile:**
- Hai firmato un DPA con il vendor
- Usi piani business/enterprise con data residency EU
- Non invii dati delle categorie a rischio alto
- Hai informato i dipendenti nell'informativa privacy aziendale

---

### Self-hosted su server aziendale o cloud EU

**Come funziona:** il modello gira su un tuo server (on-premise o cloud provider EU come Hetzner, OVH, Azure EU).

**Vantaggi GDPR:**
- I dati non lasciano la tua infrastruttura
- Sei tu il titolare del trattamento, nessun vendor terzo
- Nessun rischio di addestramento non autorizzato
- Data residency garantita in EU

**Esempi di setup:**
- Ollama + Open WebUI su server aziendale
- LLM self-hosted su Azure EU o AWS Frankfurt
- Whisper locale per trascrizione audio

**Quando è la scelta giusta:**
- Tratti dati sensibili o riservati
- Settori regolamentati: sanità, legale, finance, PA
- Vuoi controllo totale e audit trail completo

---

### SaaS con Data Residency EU

**Come funziona:** tool cloud ma con server fisicamente in Europa e contratti conformi GDPR.

**Esempi:**
- Microsoft 365 Copilot con EU Data Boundary
- Google Workspace con elaborazione dati EU
- tl;dv con server EU
- Mistral AI (azienda francese, dati in EU)

**Vantaggi:** facilità d'uso del cloud + garanzie GDPR migliori rispetto ai vendor USA.

---

### Confronto rapido

| Criterio | Cloud US | Cloud EU/SaaS EU | Self-hosted |
|---|---|---|---|
| Facilità d'uso | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ |
| Conformità GDPR | ⚠️ Con DPA | ✅ Con DPA EU | ✅ Nativo |
| Dati sensibili | ❌ Sconsigliato | ⚠️ Valutare | ✅ OK |
| Costo | Basso | Medio | Medio-alto |
| Controllo | Basso | Medio | Totale |
| Audit trail | Limitato | Parziale | Completo |

---

## 5. Data Processing Agreement (DPA)

Il DPA (o Data Processing Agreement, in italiano "accordo sul trattamento dei dati") è il contratto che regola il rapporto tra te (titolare del trattamento) e il vendor AI (responsabile del trattamento).

**È obbligatorio** ogni volta che un fornitore esterno tratta dati personali per tuo conto. Senza DPA, l'uso di tool AI con dati personali è illegittimo ai sensi dell'Art. 28 GDPR.

### Cosa deve contenere un DPA (Art. 28 GDPR)

- Oggetto e durata del trattamento
- Natura e finalità del trattamento
- Tipo di dati personali trattati
- Categorie di interessati
- Obblighi e diritti del titolare
- Garanzie di sicurezza (Art. 32)
- Obbligo di notifica breach entro tempi definiti
- Diritto di audit del titolare
- Divieto di sub-appalto senza autorizzazione
- Cancellazione o restituzione dei dati a fine contratto

### Come trovare il DPA dei vendor principali

| Vendor | DPA disponibile | Note |
|---|---|---|
| OpenAI (ChatGPT) | ✅ Sì | Piani Team/Enterprise — vai su platform.openai.com/privacy |
| Anthropic (Claude) | ✅ Sì | Piani Team/API — claude.ai/legal |
| Google (Gemini/Workspace) | ✅ Sì | Incluso in Google Workspace Business |
| Microsoft (Copilot/365) | ✅ Sì | Microsoft Products and Services DPA |
| Notion AI | ✅ Sì | Richiede piano Business+ |
| ChatGPT Free | ❌ No | Non disponibile per piani gratuiti |

> **Attenzione:** i piani gratuiti generalmente **non includono DPA** e i dati possono essere usati per addestrare i modelli. Per uso aziendale con dati personali, serve sempre un piano business/enterprise.

### Come disattivare l'addestramento sui tuoi dati

**ChatGPT:** Impostazioni → Controlli dati → disattiva "Migliora il modello per tutti"  
**Claude (claude.ai):** I dati delle conversazioni non vengono usati per addestrare i modelli di default nei piani a pagamento  
**Google Gemini Workspace:** Admin console → AI e Machine Learning → disattiva "Aiuta a migliorare i prodotti Google"

---

## 6. Analisi dei tool più usati

### ChatGPT / ChatGPT Team / ChatGPT Enterprise

| Aspetto | Free | Team | Enterprise |
|---|---|---|---|
| DPA disponibile | ❌ | ✅ | ✅ |
| Dati per training | ✅ Sì (default) | ❌ No | ❌ No |
| Data residency EU | ❌ | ❌ | ✅ Opzionale |
| Adatto a dati sensibili | ❌ | ⚠️ | ✅ Con valutazione |
| Costo | Gratis | ~$25/utente/mese | Custom |

**Verdetto:** ChatGPT Free non va usato con dati aziendali personali. Team è accettabile per dati non sensibili con DPA. Enterprise per uso intensivo con dati riservati.

---

### Microsoft 365 Copilot

**Punti di forza GDPR:**
- EU Data Boundary: i dati degli utenti EU restano in EU
- DPA incluso nel contratto Microsoft
- Integrazione con il sistema di permessi di Microsoft 365
- Audit log disponibili
- Copilot non accede a dati a cui l'utente non ha già accesso

**Attenzione:**
- Copilot "vede" tutto ciò a cui l'utente ha accesso in SharePoint/Teams/Outlook — verifica i permessi prima del deploy
- Costo elevato (~€30/utente/mese aggiuntivi)

**Verdetto:** La scelta più sicura per aziende già su Microsoft 365. Conformità GDPR solida.

---

### Google Gemini / Workspace AI

**Punti di forza:**
- DPA incluso in Google Workspace
- Possibilità di disattivare l'uso per training
- Data center EU disponibili

**Attenzione:**
- Le impostazioni di privacy variano tra piano e piano
- Verifica sempre le impostazioni nell'Admin Console
- Gemini Advanced (consumer) non ha le stesse garanzie di Workspace

**Verdetto:** Accettabile per aziende su Google Workspace Business/Enterprise con impostazioni corrette.

---

### Whisper (OpenAI) — Trascrizione audio

**Versione cloud (api.openai.com):** soggetta alle stesse regole di ChatGPT. Con DPA API è accettabile per audio non sensibile.

**Versione locale (whisper.cpp, faster-whisper):** nessun dato esce dal tuo server. La scelta migliore per trascrizione di riunioni con dati riservati, interviste, contenuti medici o legali.

**Verdetto:** Per uso aziendale con contenuti sensibili, usa sempre la versione locale.

---

### GitHub Copilot

**Punti di forza:**
- Copilot Business/Enterprise: DPA disponibile, no training sui tuoi dati
- Filtraggio suggerimenti che corrispondono a codice pubblico

**Attenzione:**
- Non inviare mai credenziali, chiavi API o dati di produzione nel codice
- Copilot individuale (piano base): i tuoi snippet possono essere usati per training

**Verdetto:** Copilot Business è accettabile. Configura `.gitignore` e variabili d'ambiente per evitare di esporre dati sensibili nei prompt.

---

## 7. AI Act UE 2024 — cosa cambia

Il Regolamento sull'Intelligenza Artificiale (AI Act, Regolamento UE 2024/1689) è entrato in vigore il 1° agosto 2024 con applicazione progressiva fino al 2027. Si affianca al GDPR senza sostituirlo.

### Classificazione dei sistemi AI per rischio

**Rischio inaccettabile — VIETATI dal 2 febbraio 2025:**
- Sistemi di social scoring da parte di governi
- Manipolazione subliminale
- Riconoscimento biometrico in tempo reale in spazi pubblici (con eccezioni)
- Sfruttamento delle vulnerabilità di gruppi a rischio

**Rischio alto — Obblighi stringenti:**
Sistemi usati in: infrastrutture critiche, istruzione, occupazione (screening CV, valutazione performance), accesso a servizi essenziali, forze dell'ordine, migrazione, amministrazione della giustizia.

Per questi sistemi è obbligatorio:
- Registrazione in un database EU
- Valutazione della conformità prima del deploy
- Supervisione umana
- Trasparenza verso gli utenti
- Documentazione tecnica dettagliata
- Gestione dei rischi

**Rischio limitato — Obblighi di trasparenza:**
- Chatbot: l'utente deve sapere che sta parlando con un AI
- Deepfake: obbligo di etichettatura
- Sistemi che generano testo su temi di interesse pubblico

**Rischio minimo — Nessun obbligo specifico:**
- Filtri antispam, videogiochi con AI, strumenti di produttività generici

### Cosa significa per le PMI italiane

Se usi AI solo per produttività interna (riassumere documenti, rispondere a email, generare codice), sei probabilmente nella categoria **rischio minimo o limitato** — gli obblighi aggiuntivi rispetto al GDPR sono pochi.

Se usi AI per **decisioni su persone** (screening candidati, valutazione credito, accesso a servizi), rientri nella categoria **rischio alto** con obblighi significativi.

**Date chiave:**
- Febbraio 2025: divieto sistemi rischio inaccettabile
- Agosto 2025: obblighi per modelli AI general purpose (GPAI)
- Agosto 2026: obblighi per sistemi ad alto rischio
- Agosto 2027: obblighi per sistemi AI embedded in prodotti regolamentati

---

## 8. Checklist pratica per valutare un tool AI

Usa questa checklist prima di adottare qualsiasi strumento AI in azienda.

### ✅ Prima dell'adozione

- [ ] Il vendor ha un DPA disponibile e firmabile?
- [ ] I server sono in EU o il vendor offre garanzie equivalenti (SCC)?
- [ ] Il piano scelto esclude l'uso dei dati per training del modello?
- [ ] Ho identificato quali dati personali verranno trattati dal tool?
- [ ] Ho una base giuridica valida per quel trattamento (Art. 6 GDPR)?
- [ ] Il trattamento rientra nelle finalità già dichiarate nell'informativa privacy?
- [ ] Ho aggiornato il Registro dei Trattamenti (Art. 30) con questo nuovo tool?
- [ ] Ho valutato se serve una DPIA (valutazione d'impatto) per rischio alto?

### ✅ Prima del deploy ai dipendenti

- [ ] Ho aggiornato l'informativa privacy per dipendenti e clienti?
- [ ] Ho formato i dipendenti su cosa possono e non possono inserire nel tool?
- [ ] Ho definito una policy aziendale sull'uso degli strumenti AI?
- [ ] Esiste un processo per gestire le richieste degli interessati (accesso, cancellazione)?
- [ ] So come gestire una notifica di data breach dal vendor entro 72h?

### ✅ Uso quotidiano

- [ ] I dipendenti sanno quali categorie di dati NON inserire?
- [ ] Esiste un processo di revisione umana per decisioni che impattano persone?
- [ ] I log di utilizzo sono conservati per eventuali audit?
- [ ] Il vendor viene monitorato per aggiornamenti alla privacy policy?

### ✅ Specifico per sistemi ad alto rischio (AI Act)

- [ ] Il sistema rientra nelle categorie ad alto rischio dell'AI Act?
- [ ] È prevista supervisione umana per le decisioni automatizzate?
- [ ] Il sistema è stato registrato nel database EU (quando applicabile)?
- [ ] La documentazione tecnica è disponibile per eventuali ispezioni?

---

## 9. Scenari concreti con risposta

### "Posso usare ChatGPT Free per riassumere email dei clienti?"

**Risposta: No.**  
Le email dei clienti contengono dati personali. ChatGPT Free non ha DPA e usa i dati per training. Violi l'Art. 28 GDPR (manca il contratto con il responsabile del trattamento) e probabilmente l'Art. 5 (minimizzazione e limitazione finalità).

**Alternativa:** ChatGPT Team/Enterprise con DPA, oppure Claude.ai con piano Team, oppure Ollama in locale.

---

### "Posso usare Whisper per trascrivere le riunioni del CDA?"

**Risposta: Dipende.**  
Whisper via API OpenAI: solo con DPA firmato e se il contenuto non include dati delle categorie speciali.  
Whisper in locale (whisper.cpp): sì, senza limitazioni GDPR — i dati non lasciano il tuo server.

**Consiglio:** per riunioni con contenuti riservati (strategie, dati finanziari, dati HR), usa sempre la versione locale.

---

### "Possiamo usare un tool AI per scremare i CV?"

**Risposta: Con molta cautela.**  
Lo screening automatico di CV rientra nei sistemi ad **alto rischio** dell'AI Act (Art. 6, Allegato III — occupazione). Obblighi: supervisione umana, trasparenza verso i candidati, documentazione tecnica, non discriminazione.

Inoltre, i CV contengono dati personali — serve base giuridica, informativa e DPA con il vendor.

**Consiglio:** usa l'AI come supporto con revisione umana obbligatoria, informa i candidati nell'informativa sul trattamento.

---

### "GitHub Copilot può vedere il codice del nostro gestionale con dati clienti?"

**Risposta: Dipende da come è scritto il codice.**  
Copilot legge il contesto del file aperto. Se il codice contiene dati hardcoded (nomi clienti, ID, IBAN), Copilot li "vede" e li invia ai server Microsoft.

**Soluzione:**
- Non hardcodare mai dati reali nel codice
- Usa variabili d'ambiente e file `.env` (escludi dal repo con `.gitignore`)
- Con Copilot Business hai DPA, ma minimizza comunque i dati nel contesto

---

### "Posso usare l'AI per analizzare i dati di salute dei dipendenti per il welfare aziendale?"

**Risposta: No, senza consenso esplicito.**  
I dati sanitari sono categoria speciale (Art. 9 GDPR). Richiedono consenso esplicito dell'interessato, non solo legittimo interesse. L'analisi automatizzata di questi dati è particolarmente delicata.

**Se vuoi procedere:** consenso esplicito scritto, DPIA obbligatoria, DPA con il vendor, preferibilmente elaborazione locale o su server aziendale.

---

### "Possiamo addestrare un modello custom sui nostri documenti aziendali?"

**Risposta: Sì, ma con attenzione.**  
Se i documenti contengono dati personali (contratti, email, schede clienti), devi:
- Anonimizzare o pseudonimizzare i dati prima del training
- Valutare se serve una DPIA
- Se usi un vendor per il fine-tuning, serve DPA
- Documentare tutto per accountability

**Consiglio:** per RAG (Retrieval Augmented Generation) su documenti interni, un sistema self-hosted (Ollama + Open WebUI + documenti locali) è la scelta più sicura e GDPR-compliant.

---

## 10. Soluzioni consigliate per PMI italiane

### Setup minimo sicuro (budget contenuto)

**Per produttività generica senza dati sensibili:**
- Claude.ai Team o ChatGPT Team — con DPA firmato, training disattivato
- Formare i dipendenti su cosa NON inserire
- Aggiornare informativa e registro trattamenti

**Costo:** ~€20-30/utente/mese

---

### Setup bilanciato (dati aziendali moderatamente sensibili)

- Microsoft 365 Copilot se già su M365 — DPA incluso, EU Data Boundary
- Whisper locale per trascrizioni audio (whisper.cpp o faster-whisper)
- Ollama in locale per analisi documenti riservati

**Costo:** M365 Copilot ~€30/utente/mese aggiuntivi + server locale

---

### Setup completo per dati sensibili (sanità, legale, finance)

- Ollama + Open WebUI su server aziendale o cloud EU dedicato
- Modelli locali: Llama 3.1, Mistral, Phi-3 (nessun dato esce dall'azienda)
- Whisper locale per audio
- Nessun tool cloud per dati delle categorie speciali

**Costo:** server dedicato €50-200/mese, nessun costo per utente aggiuntivo

---

## Risorse utili

- [Garante Privacy italiano](https://www.garanteprivacy.it) — provvedimenti e FAQ su AI
- [EDPB Guidelines on AI](https://www.edpb.europa.eu) — linee guida del Comitato Europeo
- [AI Act testo completo](https://eur-lex.europa.eu/legal-content/IT/TXT/?uri=CELEX:32024R1689) — Gazzetta Ufficiale UE
- [ICO Guidance on AI](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/artificial-intelligence/) — guida pratica UK (applicabile per principi)
- [OpenAI Privacy Portal](https://privacy.openai.com) — gestione dati e DPA
- [Microsoft DPA](https://www.microsoft.com/licensing/docs/view/Microsoft-Products-and-Services-Data-Protection-Addendum-DPA)

---

*Guida redatta a scopo informativo. Non costituisce consulenza legale.  
Per valutazioni specifiche sulla tua situazione aziendale, consulta un DPO o un legale specializzato in privacy.*

---

**Nicholas Izzo** — [nicholasizzo.github.io/ai-practical-guide](https://nicholasizzo.github.io/ai-practical-guide/)
