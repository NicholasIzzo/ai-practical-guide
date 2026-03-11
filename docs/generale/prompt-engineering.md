# ✍️ Prompt Engineering — Come Scrivere Prompt Efficaci

Guida pratica per ottenere risultati migliori dai modelli AI attraverso prompt ben strutturati.

---

## Cos'è il Prompt Engineering?

Il prompt è l'input che dai all'AI. La qualità dell'output dipende quasi sempre dalla qualità del prompt.

```
Prompt vago    → risposta generica e poco utile
Prompt preciso → risposta specifica e immediatamente utilizzabile
```

Non è magia — è comunicazione chiara.

---

## Le 5 regole base

### 1. Dai contesto
L'AI non sa chi sei o cosa stai facendo. Dirglielo migliora subito i risultati.

```
❌ "Scrivi uno script per il backup"

✅ "Sono un sistemista con un NAS Ugreen che gira su Linux.
   Scrivi uno script Bash per fare backup incrementale della cartella
   /volume1/docker su un disco USB montato in /mnt/backup"
```

---

### 2. Specifica il formato dell'output
Se vuoi Markdown, JSON, una tabella, un elenco — dillo esplicitamente.

```
❌ "Confronta Docker e Podman"

✅ "Confronta Docker e Podman in una tabella Markdown con queste colonne:
   feature, Docker, Podman. Includi: installazione, rootless, compose support,
   sicurezza, compatibilità"
```

---

### 3. Assegna un ruolo all'AI
Dire all'AI che "persona" deve interpretare migliora la qualità delle risposte in contesti tecnici.

```
✅ "Sei un esperto di sicurezza Linux con 10 anni di esperienza.
   Analizza questo script e trovami tutti i problemi di sicurezza."

✅ "Sei un docente universitario di informatica. Spiegami il concetto
   di containerizzazione come se fossi uno studente al primo anno."
```

---

### 4. Usa esempi (few-shot prompting)
Mostrare esempi di input/output desiderato è uno dei modi più efficaci per guidare l'AI.

```
✅ "Converti questi comandi Docker in docker-compose.yml.

Esempio:
Input: docker run -d --name pihole -p 53:53 pihole/pihole
Output:
services:
  pihole:
    image: pihole/pihole
    container_name: pihole
    ports:
      - '53:53'

Ora converti questo:
docker run -d --name vaultwarden -p 8080:80 vaultwarden/server"
```

---

### 5. Chiedi ragionamento step-by-step
Per problemi complessi, chiedere all'AI di ragionare passo per passo migliora l'accuratezza.

```
✅ "Devo configurare un reverse proxy con NPM per Vaultwarden con HTTPS
   via certificato Tailscale. Ragiona step-by-step e dimmi ogni passaggio
   con i comandi esatti."
```

---

## Tecniche avanzate

### Chain of Thought
Chiedi all'AI di mostrare il suo ragionamento prima di dare la risposta finale.

```
"Prima di rispondere, analizza il problema e spiega il tuo ragionamento.
Poi dai la soluzione."
```

### Iterazione
Non fermarti al primo output — raffina il risultato con follow-up.

```
Primo prompt: "Scrivi uno script per monitorare i container Docker"
Follow-up 1:  "Aggiungi la notifica via Discord webhook"
Follow-up 2:  "Aggiungi gestione degli errori e logging su file"
Follow-up 3:  "Ora ottimizzalo per girare su ARM64"
```

### Negative prompting
Dichiara esplicitamente cosa NON vuoi.

```
"Scrivi la documentazione per questo script. Non usare bullet point,
scrivi in forma di paragrafi. Non includere esempi ovvi. Non ripetere
concetti già spiegati."
```

### Prompt di sistema (System prompt)
Se usi l'AI tramite API, il system prompt imposta il comportamento globale del modello.

```python
system_prompt = """
Sei un assistente tecnico specializzato in Linux e Docker.
Rispondi sempre in italiano.
Fornisci sempre i comandi esatti con le opzioni complete.
Se non sei sicuro di qualcosa, dillo esplicitamente.
"""
```

---

## Errori comuni

### Prompt troppo vago
```
❌ "Come faccio il backup?"
✅ "Come faccio il backup automatico di /volume1/docker su Backblaze B2
   usando rclone su Ubuntu Server 22.04, con schedule giornaliero alle 2:00?"
```

### Troppe richieste in un prompt
```
❌ "Spiegami Docker, scrivi uno script di backup, confronta RAID 1 e RAID 5
   e dimmi quali container installare sul NAS"

✅ Dividi in prompt separati — uno per ogni task
```

### Non specificare il livello tecnico
```
❌ "Spiegami come funziona Kubernetes"
✅ "Spiegami Kubernetes come se fossi un sistemista che conosce Docker
   ma non ha mai usato orchestratori di container"
```

---

## Template pronti all'uso

### Spiega un concetto:
```
Spiegami [CONCETTO] in modo chiaro e pratico.
Il mio livello: [principiante/intermedio/avanzato]
Contesto: [perché ne ho bisogno]
Includi un esempio reale.
```

### Scrivi codice:
```
Scrivi [LINGUAGGIO] che fa [OBIETTIVO].
Sistema: [OS e versione]
Vincoli: [limitazioni, librerie disponibili, ecc.]
Stile: [commentato / production-ready / semplice e leggibile]
```

### Risolvi un problema:
```
Ho questo problema: [descrizione]
Sistema: [ambiente]
Errore: [messaggio di errore o comportamento inatteso]
Ho già provato: [tentativi]
Cosa devo fare?
```

### Genera documentazione:
```
Genera documentazione per [COSA].
Formato: Markdown
Pubblico: [tecnico / non tecnico]
Lunghezza: [breve / dettagliata]
Includi: [sezioni specifiche]
```

---

## Confronto tra stili di prompt

| Stile | Esempio | Quando usarlo |
|---|---|---|
| **Diretto** | "Scrivi uno script Bash per..." | Task tecnici chiari |
| **Con ruolo** | "Sei un esperto di sicurezza..." | Analisi, review, consulenza |
| **Step-by-step** | "Ragiona passo per passo..." | Problemi complessi |
| **Con esempi** | "Esempio input/output..." | Formattazione precisa |
| **Iterativo** | Raffinamenti successivi | Output complessi |

---

> 💡 Il prompt engineering non è una scienza esatta — è una skill che si affina con la pratica. Salva i prompt che funzionano bene e costruisci la tua libreria personale.
