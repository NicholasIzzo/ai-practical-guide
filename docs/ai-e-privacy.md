# 🔒 AI e Privacy — GDPR, Dati e Uso Consapevole

Cosa succede ai tuoi dati quando usi i servizi AI, cosa dice il GDPR e come usare l'AI in modo consapevole.

---

## Cosa succede ai tuoi dati?

Quando invii un prompt a un servizio AI cloud, i tuoi dati percorrono questo percorso:

```
Il tuo dispositivo
    │ (HTTPS cifrato)
    ▼
Server del provider (OpenAI, Anthropic, Google)
    │
    ├── Elaborazione del prompt
    ├── Logging per sicurezza e debug
    └── Potenziale uso per migliorare il modello*

*dipende dai ToS e dalle impostazioni dell'account
```

---

## Cosa dicono i principali provider

### Anthropic (Claude)
- I dati delle conversazioni API **non vengono usati** per il training di default
- Le conversazioni su claude.ai **possono essere usate** per migliorare i modelli, salvo opt-out
- Conservazione dei dati: politica disponibile su anthropic.com/privacy
- Sede: USA → trasferimento dati extra-UE

### OpenAI (ChatGPT)
- Account gratuito: conversazioni usate per training di default (opt-out disponibile)
- Account Plus/API: opt-out più semplice
- Enterprise: nessun uso per training
- Sede: USA

### Google (Gemini)
- Account personale: dati usati per migliorare i servizi Google
- Google Workspace: condizioni aziendali più stringenti
- Sede: USA

### Come fare opt-out:
- **Claude:** Impostazioni → Privacy → Data Usage
- **ChatGPT:** Impostazioni → Controlli dati → Migliora i modelli per tutti
- **Gemini:** myaccount.google.com → Dati e privacy

---

## GDPR e AI: cosa devi sapere

Il GDPR (Regolamento Generale sulla Protezione dei Dati) si applica all'uso di AI quando tratti dati personali di cittadini UE.

### Quando sei un "titolare del trattamento":
Se usi AI nella tua azienda o per elaborare dati di terzi, sei responsabile del trattamento anche se usi servizi di terzi come OpenAI.

**Obblighi pratici:**
- Informare gli interessati che i loro dati vengono elaborati con AI
- Avere una base giuridica per il trattamento
- Non inviare dati sensibili senza adeguate garanzie
- Verificare che il provider abbia clausole contrattuali standard per trasferimenti extra-UE

### Dati sensibili da non inviare mai a LLM cloud:
- Codice fiscale, carta di identità
- Dati sanitari
- Dati bancari
- Dati di minori
- Informazioni legalmente riservate

---

## Provider europei e alternative privacy-first

### Mistral AI (Francia) 🇫🇷
- Modelli open source e API
- Server in Europa
- Più favorevole al GDPR rispetto ai provider USA
- Modelli: Mistral 7B, Mixtral, Mistral Large

### Aleph Alpha (Germania) 🇩🇪
- Focalizzato su enterprise europeo
- Server in Germania
- Compliance GDPR nativa

### AI in locale (massima privacy)
La soluzione più sicura per dati sensibili:
```bash
# Ollama — nessun dato lascia il tuo server
ollama run llama3
# Tutto rimane su 192.168.x.x
```

---

## Pseudonimizzazione prima dell'invio

Se devi inviare dati personali a un LLM cloud, pseudonimizza prima:

```python
import re

class DataAnonymizer:
    def __init__(self):
        self.mappings = {}
        self.counter = 0

    def anonymize(self, text: str) -> str:
        # Sostituisci email
        emails = re.findall(r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b', text)
        for email in emails:
            if email not in self.mappings:
                self.mappings[email] = f"EMAIL_{self.counter}"
                self.counter += 1
            text = text.replace(email, self.mappings[email])

        # Sostituisci nomi propri (semplificato)
        # In produzione usa una libreria NER come spaCy

        return text

    def restore(self, text: str) -> str:
        reverse = {v: k for k, v in self.mappings.items()}
        for placeholder, original in reverse.items():
            text = text.replace(placeholder, original)
        return text

# Uso
anon = DataAnonymizer()
safe_text = anon.anonymize("Mario Rossi (mario.rossi@azienda.it) ha un problema con...")
response = call_ai(safe_text)
final_response = anon.restore(response)
```

---

## AI Act — La Nuova Legge Europea sull'AI

L'**EU AI Act** (in vigore dal 2024, applicazione graduale fino al 2027) classifica i sistemi AI per livello di rischio:

| Rischio | Esempi | Obblighi |
|---|---|---|
| **Inaccettabile** | Social scoring, manipolazione subliminale | **Vietato** |
| **Alto** | AI in sanità, giustizia, recruitment | Requisiti severi, certificazione |
| **Limitato** | Chatbot, deepfake | Obbligo di trasparenza |
| **Minimo** | Filtri spam, AI nei videogiochi | Nessun obbligo specifico |

**Per l'uso quotidiano:** ChatGPT, Claude, Gemini rientrano nella categoria "limitato" — devono solo essere trasparenti sul fatto che l'utente sta interagendo con un'AI.

---

## Checklist per uso consapevole dell'AI

**Prima di inviare:**
- [ ] Questo testo contiene dati personali?
- [ ] Contiene informazioni riservate o aziendali?
- [ ] Ho letto i ToS del provider riguardo all'uso dei dati?
- [ ] È necessario inviarlo al cloud o posso usare un modello locale?

**Account e impostazioni:**
- [ ] Ho fatto opt-out dal training dei dati dove possibile
- [ ] Uso account separati per uso personale e professionale
- [ ] Conosco dove trovare i miei dati per esercitare i diritti GDPR (accesso, cancellazione)

**Per uso aziendale:**
- [ ] Ho una DPA (Data Processing Agreement) con il provider
- [ ] Ho informato gli interessati dell'uso dell'AI
- [ ] Ho una base giuridica per il trattamento

---

## I tuoi diritti GDPR sui dati AI

Come cittadino UE hai diritto a:

- **Accesso** — richiedere quali dati ha il provider su di te
- **Cancellazione** — richiedere la cancellazione delle tue conversazioni
- **Portabilità** — esportare i tuoi dati
- **Opposizione** — opporti all'uso dei tuoi dati per il training

**Come esercitarli:**
- OpenAI: privacy.openai.com
- Anthropic: privacy@anthropic.com
- Google: myaccount.google.com/data-and-privacy

---

> 💡 La privacy nell'AI non è un ostacolo — è un vantaggio competitivo. Chi sa usare l'AI in modo conforme e consapevole costruisce fiducia con clienti e partner.
