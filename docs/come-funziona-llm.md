# 🧠 Come Funziona un LLM — Spiegazione Senza Matematica

Capire cosa c'è davvero dietro ChatGPT, Claude e gli altri modelli AI — senza formule, solo intuizioni.

---

## Il punto di partenza: prevedere la parola successiva

Un LLM (Large Language Model) fa una cosa fondamentale:

> **Dato un testo, prevede qual è la parola più probabile che viene dopo.**

È tutto qui. Tutto il resto è conseguenza di questa capacità.

```
Input:  "Il cielo è di colore ___"
Output: "azzurro" (alta probabilità)
        "verde"   (bassa probabilità)
        "pizza"   (probabilità quasi zero)
```

---

## Come impara: il pre-training

Prima di rispondere a qualsiasi domanda, un LLM viene addestrato su enormi quantità di testo — libri, articoli, siti web, codice, forum.

```
Dataset di training:
├── Wikipedia (tutte le lingue)
├── Libri digitalizzati
├── Articoli scientifici
├── Codice sorgente (GitHub)
├── Forum e discussioni
└── Siti web vari
```

**Dimensione tipica:** centinaia di miliardi di parole — più di quello che un essere umano potrebbe leggere in migliaia di vite.

Durante il training, il modello impara a prevedere la parola successiva **miliardi di volte**, correggendo i propri errori ad ogni iterazione. Da questo processo emergono capacità sorprendenti: traduzione, ragionamento, programmazione.

---

## Token: l'unità base

I modelli non elaborano parole intere ma **token** — pezzi di testo che possono essere parole intere, parti di parole o punteggiatura.

```
"intelligenza artificiale"
→ ["intel", "ligen", "za", " arti", "ficiale"]
→ 5 token
```

**Perché i token sono importanti:**
- Il costo API si basa sui token
- Il "context window" è misurato in token
- Lingue diverse hanno densità di token diverse (l'italiano è più "costoso" dell'inglese)

---

## Il Transformer: l'architettura chiave

Tutti i modelli moderni (GPT, Claude, Gemini) usano l'architettura **Transformer**, introdotta da Google nel 2017.

### Il meccanismo di Attention

Il componente più importante è l'**Attention** — permette al modello di capire quale parte del testo è rilevante per ogni parola.

```
Frase: "La banca del fiume era ripida"

Quando elabora "ripida", il modello deve capire
a cosa si riferisce — la "banca" (sponda del fiume) o la "banca" (istituto finanziario)?

L'Attention guarda l'intera frase e capisce che
"fiume" è più rilevante di qualsiasi riferimento bancario.
```

---

## Context Window

La context window è la quantità di testo che il modello può "vedere" e considerare in una volta.

```
Modello con 200k token context window:
├── Può leggere ~150.000 parole in italiano
├── Equivale a circa 600 pagine di testo
└── Tutto rimane "in mente" durante la conversazione
```

**Perché importa:**
- Conversazioni lunghe → più contesto → risposte più pertinenti
- Documenti lunghi possono essere analizzati interamente
- Scade quando la chat diventa troppo lunga (i messaggi vecchi "escono" dalla finestra)

---

## RLHF: da previsore di testo ad assistente utile

Un modello pre-addestrato è bravo a completare testo, ma non necessariamente a essere utile o sicuro. Qui entra **RLHF** (Reinforcement Learning from Human Feedback).

```
1. Pre-training → modello base che prevede testo

2. Supervised Fine-Tuning → addestrato su esempi di
   conversazioni utili scritte da umani

3. Reward Model → addestrato a valutare quale risposta
   è migliore tra due alternative

4. PPO (Reinforcement Learning) → il modello impara
   a massimizzare il punteggio del Reward Model
```

**Risultato:** Un modello che non solo completa testo, ma cerca attivamente di essere utile, accurato e sicuro.

---

## Temperature e parametri

Quando usi un'API, puoi controllare il comportamento del modello con parametri:

### Temperature (0.0 — 1.0)
Controlla quanto è "creativo" o "deterministic" il modello.

```
Temperature 0.0 → sempre la risposta più probabile
                  → deterministico, ripetibile
                  → ottimo per: codice, fatti, analisi

Temperature 0.7 → bilancia creatività e coerenza
                  → ottimo per: testo generale, spiegazioni

Temperature 1.0 → molto creativo, più imprevedibile
                  → ottimo per: brainstorming, scrittura creativa
```

### Max tokens
Limita la lunghezza della risposta.

```python
response = client.messages.create(
    model="claude-sonnet-4-20250514",
    max_tokens=1024,      # Risposta max 1024 token
    temperature=0.3,      # Abbastanza deterministico
    messages=[...]
)
```

---

## Embedding e similarità semantica

Gli LLM possono trasformare il testo in **vettori numerici** (embedding) che rappresentano il significato.

```
"gatto"    → [0.2, 0.8, 0.1, 0.9, ...]
"felino"   → [0.2, 0.7, 0.1, 0.8, ...]  (simile a "gatto")
"automobile" → [0.9, 0.1, 0.7, 0.2, ...] (diverso da "gatto")
```

**Applicazioni pratiche:**
- Ricerca semantica (trova documenti per significato, non parole esatte)
- RAG (Retrieval Augmented Generation) — fai cercare all'AI nei tuoi documenti
- Classificazione automatica di testi

---

## Parametri: quanto è "grande" un modello?

I parametri sono i "pesi" del modello — i valori numerici appresi durante il training.

| Modello | Parametri stimati | Note |
|---|---|---|
| GPT-2 (2019) | 1.5B | Modello storico, open source |
| Llama 3.1 8B | 8B | Ottimo in locale |
| Llama 3.1 70B | 70B | Richiede GPU potente |
| GPT-4 | ~1.8T (stimato) | Non confermato da OpenAI |
| Claude 3.7 | Non divulgato | Anthropic non pubblica i dettagli |

**Più parametri = più capace?** Non necessariamente. L'architettura, i dati di training e il fine-tuning contano quanto le dimensioni.

---

## Allucinazioni: perché l'AI inventa cose

Le allucinazioni sono risposte plausibili ma false generate dal modello.

**Perché succede:**
- Il modello ottimizza per la plausibilità, non per la verità
- Non ha accesso a dati in tempo reale
- Se non sa qualcosa, "interpola" in modo convincente

**Come mitigarle:**
- Chiedi sempre le fonti per fatti specifici
- Usa modelli con web search per informazioni recenti
- Verifica sempre dati critici (date, numeri, nomi)
- RAG: fornisci tu i documenti di riferimento

---

## Limitazioni fondamentali

| Limitazione | Descrizione |
|---|---|
| **Knowledge cutoff** | Non conosce eventi dopo una certa data |
| **Allucinazioni** | Può generare informazioni false con sicurezza |
| **Context window** | Non ricorda conversazioni passate |
| **No stato** | Ogni chiamata API è indipendente |
| **Ragionamento numerico** | Debolezze in calcoli complessi |
| **Consistenza** | Può contraddirsi tra risposte diverse |

---

> 💡 Capire come funziona un LLM ti aiuta a usarlo meglio — sai quando fidarti, quando verificare e come strutturare i prompt per ottenere risultati ottimali.
