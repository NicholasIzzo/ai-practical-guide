# 🖥️ AI per Sistemisti

Come usare l'intelligenza artificiale nel lavoro quotidiano di un sistemista — script, debug, documentazione e automazione.

---

## Perché l'AI è utile per i sistemisti

L'AI non sostituisce il sistemista — amplifica quello che già sai fare. Con l'AI puoi:

- Scrivere script in metà tempo
- Capire errori sconosciuti in secondi
- Generare documentazione automaticamente
- Imparare nuove tecnologie più velocemente
- Automatizzare task ripetitivi

---

## 1. Scrittura di Script

### Bash
**Prompt efficace:**
```
Scrivi uno script Bash che monitora l'utilizzo del disco su /volume1 e invia
un alert su Discord via webhook se supera l'80%. Lo script deve girare come
cron job ogni ora.
```

**Cosa aspettarsi:** Script completo con gestione errori, commenti e istruzioni per il cron job.

**Tip:** Specifica sempre:
- Il sistema operativo (Ubuntu, Debian, ecc.)
- La versione se rilevante
- Come vuoi ricevere gli alert
- Dove verrà eseguito lo script

---

### Python
**Prompt efficace:**
```
Scrivi uno script Python che legge le metriche da Prometheus via API REST,
filtra i servizi con uptime < 99% nell'ultimo giorno e genera un report
in formato Markdown.
```

---

### PowerShell
**Prompt efficace:**
```
Scrivi uno script PowerShell che controlla tutti i servizi Windows in stato
"Stopped" su una lista di server remoti e li riavvia automaticamente,
loggando ogni operazione su file.
```

---

## 2. Debug di Errori

Incolla l'errore direttamente nel prompt — l'AI è bravissima a interpretare log e stack trace.

**Prompt efficace:**
```
Ho questo errore in Docker. Il container nginx-proxy-manager non si avvia.
Cosa significa e come lo risolvo?

[incolla qui l'output di: docker logs nginx-proxy-manager]
```

**Tip per il debug:**
- Includi sempre il contesto (quale servizio, quale OS, cosa stavi facendo)
- Incolla l'intero log, non solo la riga dell'errore
- Chiedi anche una spiegazione del perché è successo, non solo come risolvere

---

## 3. Interpretare Log di Sistema

**Prompt efficace:**
```
Analizza questi log di sistema e dimmi se c'è qualcosa di anomalo,
con particolare attenzione a errori, warning e tentativi di accesso falliti:

[incolla i log]
```

---

## 4. Documentazione Automatica

L'AI è eccellente per documentare configurazioni esistenti.

**Prompt efficace:**
```
Leggi questo docker-compose.yml e genera una documentazione in Markdown
che spieghi cosa fa ogni servizio, le porte esposte, i volumi e le
variabili d'ambiente. Il tono deve essere tecnico ma comprensibile.

[incolla il docker-compose.yml]
```

---

## 5. Configurazioni e File

### Nginx / NPM
```
Scrivi una configurazione Nginx per fare reverse proxy verso un'applicazione
Node.js su porta 3000, con SSL, rate limiting a 100 req/min e header
di sicurezza (HSTS, X-Frame-Options, CSP).
```

### Docker Compose
```
Scrivi un docker-compose.yml per Nextcloud con MariaDB come database,
Redis per la cache, e Nginx come reverse proxy. Includi health checks
e restart policy.
```

### Prometheus
```
Scrivi una regola di alerting per Prometheus che si attiva quando:
- CPU > 90% per più di 5 minuti
- RAM disponibile < 10%
- Un container Docker si riavvia più di 3 volte in 10 minuti
```

---

## 6. Spiegazione di Concetti Tecnici

L'AI è un ottimo "rubber duck" per capire tecnologie nuove.

**Prompt efficace:**
```
Spiegami come funziona il DNS split-horizon in un homelab con Pihole,
con un esempio pratico di configurazione. Sono un sistemista ma non ho
mai configurato DNS split-horizon prima.
```

---

## 7. Review del Codice

**Prompt efficace:**
```
Fai una code review di questo script Bash. Cerca:
- Bug e problemi logici
- Problemi di sicurezza
- Miglioramenti di performance
- Casi limite non gestiti

[incolla lo script]
```

---

## 8. Conversione tra Tecnologie

**Prompt efficace:**
```
Converti questo script Bash in Python mantenendo la stessa logica.
Usa solo librerie standard, niente dipendenze esterne.

[incolla lo script Bash]
```

---

## Workflow consigliato

```
Problema/Task
    │
    ▼
Descrivi il contesto all'AI (OS, versioni, obiettivo)
    │
    ▼
Chiedi una soluzione con spiegazione
    │
    ▼
Testa la soluzione
    │
    ├── Funziona → documenta e salva il prompt per usi futuri
    │
    └── Non funziona → incolla l'errore all'AI e itera
```

---

## Prompt Templates per Sistemisti

Salva questi template e adattali al tuo caso:

### Template debug:
```
Ho un problema con [SERVIZIO] su [OS/VERSIONE].
Contesto: [cosa stavi facendo]
Errore: [incolla errore]
Cosa ho già provato: [tentativi precedenti]
Dimmi la causa e come risolvere.
```

### Template script:
```
Scrivi uno script [BASH/PYTHON/POWERSHELL] che:
- Fa: [obiettivo principale]
- Gira su: [OS e versione]
- Input: [cosa riceve]
- Output: [cosa deve produrre]
- Gestione errori: [come comportarsi in caso di errore]
Aggiungi commenti al codice.
```

### Template documentazione:
```
Genera documentazione tecnica per [COSA].
Pubblico: [sistemisti / principianti / team]
Formato: Markdown
Includi: prerequisiti, passi di installazione, configurazione, troubleshooting comune.
```

---

## Limiti da conoscere

- **Knowledge cutoff** — i modelli hanno una data limite di conoscenza. Per tecnologie molto recenti, verifica sempre la documentazione ufficiale
- **Allucinazioni** — l'AI può inventare comandi o opzioni che non esistono. Testa sempre prima di usare in produzione
- **Sicurezza** — non incollare mai password, token, chiavi private o dati sensibili nel prompt
- **Versioni** — specifica sempre la versione del software — le API e i comandi cambiano tra versioni

---

> 💡 L'AI è il migliore collega che non si stufa mai di rispondere alle domande. Usala per imparare, non solo per copiare — chiedi sempre una spiegazione, non solo la soluzione.
