# 🖥️ AI in Locale — Hardware, Modelli e Setup per IT Aziendali

Guida tecnica completa per eseguire modelli AI direttamente sull'infrastruttura aziendale. Nessun dato esce dalla rete, compliance GDPR nativa, costi prevedibili.

> 🖥️ = Locale | ✅ = Testato | 💶 = Costo indicativo | 🔒 = GDPR compliant by design

---

## 📋 Indice

- [Perché AI in locale](#-perché-ai-in-locale)
- [Requisiti hardware](#-requisiti-hardware)
- [Scelta del modello](#-scelta-del-modello)
- [Stack software](#-stack-software)
- [Setup Ollama](#-setup-ollama-il-modo-più-veloce)
- [Setup con Docker](#-setup-con-docker-produzione)
- [Interfaccia utente — Open WebUI](#-interfaccia-utente--open-webui)
- [Integrazione IDE — Continue.dev](#-integrazione-ide--continuedev)
- [Hardware consigliato per aziende](#-hardware-consigliato-per-aziende)
- [Benchmark e confronto modelli](#-benchmark-e-confronto-modelli)
- [Costi totali stimati](#-costi-totali-stimati)
- [Troubleshooting](#-troubleshooting)

---

## 🔒 Perché AI in locale

| Criterio | Cloud (ChatGPT, Claude) | Locale (Ollama, LM Studio) |
|----------|------------------------|---------------------------|
| Privacy dati | ⚠️ Dati a server terzi | ✅ Dati mai escono dalla rete |
| GDPR | ⚠️ DPA richiesto | ✅ Compliant by design |
| Costo a lungo termine | 💶 ~€20-100/mese/utente | 💶 Hardware una tantum |
| Qualità modelli | ✅ Frontier (GPT-5, Claude) | ⚠️ Leggermente inferiore |
| Disponibilità offline | ❌ Richiede internet | ✅ Funziona air-gapped |
| Latenza | ~500ms-2s | ~100ms-500ms (con GPU) |
| Personalizzazione | ❌ Limitata | ✅ Fine-tuning possibile |

**Quando scegliere il locale:**
- Dati sensibili (medici, legali, finanziari, HR)
- Ambienti air-gapped o con policy di sicurezza stringenti
- Volume alto di richieste (costo cloud diventa elevato)
- Requisiti di latenza bassa (integrazione in applicativi interni)

---

## 🔧 Requisiti hardware

### Concetti base

I modelli AI si misurano in **parametri (B = miliardi)**. Più parametri = più capace ma più pesante.

La regola pratica per la RAM:
```
RAM necessaria ≈ parametri × 0.6 GB  (quantizzazione 4-bit)
RAM necessaria ≈ parametri × 2 GB    (quantizzazione 8-bit, qualità migliore)

Esempi:
- Llama 3.2 3B  → ~2GB RAM (4-bit) — molto leggero
- Llama 3.1 8B  → ~5GB RAM (4-bit) — bilanciato
- Llama 3.1 70B → ~40GB RAM (4-bit) — potente, server richiesto
- Mistral 7B    → ~4GB RAM (4-bit) — ottimo per italiano
```

### Configurazioni minime per uso aziendale

#### 🟢 Configurazione Entry — 1-5 utenti simultanei

```
CPU:  Intel Core i5/i7 gen 10+ o AMD Ryzen 5/7
RAM:  16GB DDR4 (minimo), 32GB consigliato
GPU:  Integrata (lenta) o NVIDIA GTX 1660 (6GB VRAM)
SSD:  100GB liberi per modelli
OS:   Ubuntu Server 22.04 LTS / Windows Server / Windows 11

Modelli supportati: fino a 8B parametri
Velocità generazione: ~5-15 token/sec (CPU), ~20-40 token/sec (GPU)
Costo hardware: €300-800 (ricondizionato) / €800-1500 (nuovo)
```

#### 🟡 Configurazione Standard — 5-20 utenti simultanei

```
CPU:  Intel Core i9 gen 12+ o AMD Ryzen 9 / Xeon entry
RAM:  64GB DDR4/DDR5
GPU:  NVIDIA RTX 3090 (24GB VRAM) o RTX 4090 (24GB VRAM)
SSD:  500GB NVMe per modelli
OS:   Ubuntu Server 22.04 LTS

Modelli supportati: fino a 34B parametri in GPU, 70B in CPU offload
Velocità generazione: ~40-80 token/sec
Costo hardware: €2.500-5.000
```

#### 🔴 Configurazione Server — 20+ utenti, uso produzione

```
CPU:  AMD EPYC o Intel Xeon Scalable (multi-core)
RAM:  128-256GB ECC DDR5
GPU:  2x NVIDIA A100 40GB o RTX 6000 Ada (48GB VRAM) o
      NVIDIA L40S (48GB VRAM) — migliore rapporto prezzo/performance
SSD:  2TB NVMe in RAID
OS:   Ubuntu Server 22.04 LTS
Rete: 10GbE consigliato

Modelli supportati: 70B+ parametri, multi-utente
Velocità generazione: ~100-200 token/sec
Costo hardware: €15.000-40.000
```

### GPU — Quale scegliere

```
Budget limitato (fino a €500):
  NVIDIA RTX 3060 12GB VRAM — ottimo entry, modelli fino a 13B
  NVIDIA RTX 3070 8GB VRAM  — meno VRAM, più veloce su modelli piccoli

Budget medio (€500-1500):
  NVIDIA RTX 3090 24GB VRAM — best value per AI locale
  NVIDIA RTX 4070 Ti 12GB   — efficiente, buona velocità

Budget alto (€1500+):
  NVIDIA RTX 4090 24GB VRAM — top consumer, ~80 token/sec su 13B
  NVIDIA RTX 6000 Ada 48GB  — workstation, modelli 34B in VRAM

Enterprise/Server:
  NVIDIA A100 40/80GB       — data center, costo €10.000+
  NVIDIA L40S 48GB          — buon compromesso costo/performance
  NVIDIA H100 80GB          — top di gamma, €30.000+
```

**Nota:** Le GPU AMD (RX 7900 XTX) funzionano con ROCm su Linux ma il supporto è meno stabile. Consigliato NVIDIA per produzione.

---

## 🧠 Scelta del modello

### Modelli consigliati per uso aziendale (italiano)

| Modello | Parametri | RAM (4-bit) | Italiano | Coding | Uso ideale |
|---------|-----------|-------------|----------|--------|------------|
| Llama 3.2 3B | 3B | ~2GB | ⭐⭐⭐ | ⭐⭐ | PC deboli, risposta rapida |
| Mistral 7B | 7B | ~4GB | ⭐⭐⭐⭐ | ⭐⭐⭐ | Produttività generale |
| Llama 3.1 8B | 8B | ~5GB | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | Bilanciato, consigliato |
| Gemma 2 9B | 9B | ~6GB | ⭐⭐⭐ | ⭐⭐⭐ | Alternativa Google |
| Llama 3.1 70B | 70B | ~40GB | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | Server, qualità elevata |
| Codellama 13B | 13B | ~8GB | ⭐⭐ | ⭐⭐⭐⭐⭐ | Solo coding |
| Qwen 2.5 14B | 14B | ~9GB | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | Coding + produttività |

### Modelli specializzati

```bash
# Coding
ollama pull codellama:13b      # Meta, ottimizzato per codice
ollama pull qwen2.5-coder:14b  # Alibaba, eccellente su coding

# Italiano / multilingua
ollama pull mistral:7b         # Ottimo italiano
ollama pull llama3.1:8b        # Buon italiano, bilanciato

# Documenti lunghi (context window ampia)
ollama pull llama3.1:70b       # 128K context window
ollama pull mistral:7b         # 32K context window

# Embedding (per RAG/ricerca semantica)
ollama pull nomic-embed-text   # Embedding documenti aziendali
```

---

## 🛠️ Stack software

```
┌─────────────────────────────────────────────────┐
│  Utenti (browser / IDE / API)                   │
├─────────────────────────────────────────────────┤
│  Open WebUI  (interfaccia ChatGPT-like)         │
│  Continue.dev (integrazione IDE)                 │
├─────────────────────────────────────────────────┤
│  Ollama  (runtime modelli — API REST :11434)    │
├─────────────────────────────────────────────────┤
│  Modelli GGUF  (Llama, Mistral, Codellama...)   │
├─────────────────────────────────────────────────┤
│  Hardware  (CPU + GPU NVIDIA)                   │
└─────────────────────────────────────────────────┘
```

---

## ⚡ Setup Ollama (il modo più veloce)

### Installazione Linux (Ubuntu Server)

```bash
# 1. Installa Ollama
curl -fsSL https://ollama.com/install.sh | sh

# 2. Verifica installazione
ollama --version

# 3. Scarica un modello
ollama pull llama3.1:8b

# 4. Test rapido
ollama run llama3.1:8b "Ciao, presentati in italiano"

# 5. Abilita accesso dalla rete locale (per altri PC)
# Modifica il servizio systemd
sudo systemctl edit ollama
```

Aggiungi nel file che si apre:
```ini
[Service]
Environment="OLLAMA_HOST=0.0.0.0:11434"
```

```bash
# Riavvia il servizio
sudo systemctl daemon-reload
sudo systemctl restart ollama

# Verifica che sia in ascolto
curl http://localhost:11434/api/tags
```

### Installazione Windows

```powershell
# Scarica da ollama.com oppure via winget
winget install Ollama.Ollama

# Riavvia il terminale, poi scarica un modello
ollama pull llama3.1:8b

# Test
ollama run llama3.1:8b
```

### Comandi Ollama utili

```bash
# Lista modelli scaricati
ollama list

# Scarica modello
ollama pull <modello>

# Rimuovi modello
ollama rm <modello>

# Info su un modello
ollama show llama3.1:8b

# API REST — chat
curl http://localhost:11434/api/chat -d '{
  "model": "llama3.1:8b",
  "messages": [{"role": "user", "content": "Ciao"}],
  "stream": false
}'

# API REST — completamento
curl http://localhost:11434/api/generate -d '{
  "model": "llama3.1:8b",
  "prompt": "Scrivi una email professionale",
  "stream": false
}'
```

---

## 🐳 Setup con Docker (produzione)

### docker-compose.yml — Stack completo

```yaml
version: '3.8'

services:
  ollama:
    image: ollama/ollama:latest
    container_name: ollama
    restart: unless-stopped
    ports:
      - "11434:11434"
    volumes:
      - ollama_data:/root/.ollama
    # Abilita GPU NVIDIA (rimuovi se non disponibile)
    deploy:
      resources:
        reservations:
          devices:
            - driver: nvidia
              count: all
              capabilities: [gpu]
    environment:
      - OLLAMA_HOST=0.0.0.0

  open-webui:
    image: ghcr.io/open-webui/open-webui:main
    container_name: open-webui
    restart: unless-stopped
    ports:
      - "3000:8080"
    volumes:
      - open_webui_data:/app/backend/data
    environment:
      - OLLAMA_BASE_URL=http://ollama:11434
      - WEBUI_SECRET_KEY=<CHIAVE-SEGRETA-CASUALE>
      - DEFAULT_MODELS=llama3.1:8b
      - ENABLE_SIGNUP=false  # Disabilita registrazione pubblica
    depends_on:
      - ollama

volumes:
  ollama_data:
  open_webui_data:
```

### Avvio

```bash
# Avvia lo stack
docker compose up -d

# Verifica che i container girino
docker compose ps

# Scarica il modello nel container
docker exec ollama ollama pull llama3.1:8b

# Log in tempo reale
docker compose logs -f

# Stop
docker compose down
```

### Supporto GPU NVIDIA in Docker

```bash
# 1. Installa NVIDIA Container Toolkit
curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | \
  sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg

curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
  sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
  sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list

sudo apt-get update && sudo apt-get install -y nvidia-container-toolkit

# 2. Configura Docker
sudo nvidia-ctk runtime configure --runtime=docker
sudo systemctl restart docker

# 3. Test
docker run --rm --gpus all nvidia/cuda:12.0-base-ubuntu22.04 nvidia-smi
```

---

## 🌐 Interfaccia utente — Open WebUI

Open WebUI fornisce un'interfaccia identica a ChatGPT ma completamente locale.

### Funzionalità principali

- **Chat multi-modello** — cambia modello al volo
- **Gestione utenti** — crea account per ogni dipendente
- **Ruoli e permessi** — admin, user, read-only
- **RAG integrato** — carica documenti aziendali per ricerca semantica
- **Cronologia conversazioni** — salvata localmente
- **API compatibile OpenAI** — integrazione con tool esistenti

### Configurazione utenti (admin)

```
1. Apri http://<IP-SERVER>:3000
2. Prima registrazione = account admin
3. Settings → Admin Panel → Users
4. Disabilita signup pubblico: Admin → Settings → General → 
   "Enable New Sign Ups" → OFF
5. Crea account manualmente per ogni utente
```

### Caricamento documenti aziendali (RAG)

```
1. Workspace → Documents → Upload
2. Carica PDF, DOCX, TXT con documentazione aziendale
3. Nella chat: "#" → seleziona documento → fai domande sul contenuto

Esempi:
- Carica manuale procedure ISO → chiedi "qual è la procedura per X"
- Carica contratti tipo → chiedi "quali sono le clausole di rescissione"
- Carica documentazione tecnica → chiedi "come si configura Y"
```

---

## 💻 Integrazione IDE — Continue.dev

### Installazione VS Code

```bash
# Via marketplace VS Code
# Extensions → cerca "Continue" → Install

# Oppure via CLI
code --install-extension continue.continue
```

### Configurazione `~/.continue/config.json`

```json
{
  "models": [
    {
      "title": "Llama 3.1 8B (locale)",
      "provider": "ollama",
      "model": "llama3.1:8b",
      "apiBase": "http://localhost:11434"
    },
    {
      "title": "Codellama 13B (coding)",
      "provider": "ollama",
      "model": "codellama:13b",
      "apiBase": "http://localhost:11434"
    }
  ],
  "tabAutocompleteModel": {
    "title": "Autocomplete",
    "provider": "ollama",
    "model": "llama3.2:3b",
    "apiBase": "http://localhost:11434"
  },
  "embeddingsProvider": {
    "provider": "ollama",
    "model": "nomic-embed-text",
    "apiBase": "http://localhost:11434"
  }
}
```

### Shortcut Continue.dev

```
Ctrl+I   → Genera/modifica codice selezionato
Ctrl+L   → Chat con contesto del file aperto
Ctrl+Shift+L → Aggiungi selezione al contesto chat
Tab      → Accetta suggerimento autocomplete
```

---

## 💰 Hardware consigliato per aziende

### Opzione 1 — Server dedicato ricondizionato (budget)

```
Hardware:
  Dell PowerEdge R730 / HP ProLiant DL380 G9 (ricondizionato)
  CPU: 2x Intel Xeon E5-2680 v4 (28 core totali)
  RAM: 128GB DDR4 ECC
  Storage: 2x 1TB SSD SATA
  GPU: NVIDIA RTX 3090 24GB (aggiunta)

Costo stimato: €1.500-2.500 (server) + €700-900 (GPU)
Totale: ~€2.200-3.400

Capacità: 5-15 utenti simultanei, modelli fino a 34B
```

### Opzione 2 — Workstation dedicata (bilanciata)

```
Hardware:
  CPU: AMD Ryzen 9 7950X (16 core)
  RAM: 64GB DDR5
  GPU: NVIDIA RTX 4090 24GB VRAM
  Storage: 1TB NVMe PCIe 4.0
  Case: Torre workstation

Costo stimato: €3.500-4.500

Capacità: 10-20 utenti simultanei, modelli fino a 34B in GPU
Consumo: ~350W carico pieno
```

### Opzione 3 — Server GPU enterprise

```
Hardware:
  CPU: AMD EPYC 7443 (24 core)
  RAM: 256GB ECC DDR4
  GPU: 2x NVIDIA L40S 48GB VRAM
  Storage: 4x 2TB NVMe in RAID 10
  Rack: 2U server

Costo stimato: €25.000-35.000

Capacità: 50+ utenti simultanei, modelli 70B in GPU
Uptime: 99.9% con ridondanza
```

### Consumo energetico (costo annuo corrente)

```
Workstation RTX 4090 (350W carico):
  Ore/anno accesa: 8.760h
  kWh/anno: 350W × 8.760h = 3.066 kWh
  Costo (~€0.25/kWh): ~€766/anno

Server L40S x2 (600W carico):
  kWh/anno: 600W × 8.760h = 5.256 kWh
  Costo: ~€1.314/anno

Risparmio vs cloud (20 utenti × €20/mese × 12):
  Cloud cost: €4.800/anno
  Break-even workstation: ~6 mesi
```

---

## 📊 Benchmark e confronto modelli

### Velocità generazione (token/sec) per hardware

| Modello | CPU only (i9) | RTX 3090 | RTX 4090 | A100 40GB |
|---------|--------------|----------|----------|-----------|
| Llama 3.2 3B | 15-25 t/s | 80-120 t/s | 120-180 t/s | 200+ t/s |
| Llama 3.1 8B | 5-10 t/s | 40-60 t/s | 60-90 t/s | 120-150 t/s |
| Mistral 7B | 6-12 t/s | 45-65 t/s | 70-100 t/s | 130-160 t/s |
| Llama 3.1 70B | 1-2 t/s | N/A (VRAM) | N/A (VRAM) | 20-40 t/s |
| Codellama 13B | 3-6 t/s | 25-35 t/s | 40-55 t/s | 80-100 t/s |

*Valori approssimativi — variano in base a quantizzazione e contesto*

### Qualità vs modelli cloud (scala 1-10)

| Task | GPT-4o | Claude 3.5 | Llama 3.1 70B | Llama 3.1 8B | Mistral 7B |
|------|--------|------------|---------------|--------------|------------|
| Testo italiano | 9.5 | 9.5 | 8.5 | 7.5 | 7.5 |
| Coding | 9.5 | 9.5 | 8.5 | 7.5 | 7.0 |
| Analisi documenti | 9.5 | 9.5 | 8.0 | 7.0 | 6.5 |
| Ragionamento | 9.5 | 9.5 | 8.0 | 6.5 | 6.0 |
| Velocità | 7.0 | 7.0 | 6.0 | 8.5 | 9.0 |

---

## 💶 Costi totali stimati

### Scenario A — PMI 10 utenti

```
Hardware (workstation RTX 4090):     €4.000
Energia (€766/anno):                 €766/anno
Manutenzione (stima):                €200/anno
Software (Ollama + Open WebUI):      €0
─────────────────────────────────────────────
Anno 1:                              €4.966
Anno 2+:                             €966/anno

Alternativa cloud (10 utenti × €20):
  €2.400/anno → break-even ~2.5 anni
```

### Scenario B — Azienda 50 utenti

```
Hardware (server L40S x2):           €30.000
Energia (€1.314/anno):               €1.314/anno
Manutenzione:                        €1.000/anno
─────────────────────────────────────────────
Anno 1:                              €32.314
Anno 2+:                             €2.314/anno

Alternativa cloud (50 utenti × €20):
  €12.000/anno → break-even ~3 anni
  Vantaggio: dati mai escono, zero rischio GDPR
```

---

## 🔧 Troubleshooting

### Ollama non risponde

```bash
# Controlla stato servizio
sudo systemctl status ollama

# Riavvia
sudo systemctl restart ollama

# Log errori
sudo journalctl -u ollama -f

# Verifica porta
ss -tlnp | grep 11434
```

### GPU non rilevata

```bash
# Verifica driver NVIDIA
nvidia-smi

# Se non funziona, reinstalla driver
sudo apt-get install nvidia-driver-535

# Verifica in Ollama
ollama run llama3.1:8b
# Cerca "GPU layers" nell'output — deve essere > 0
```

### Modello lento (gira su CPU invece di GPU)

```bash
# Controlla quanti layer vanno in GPU
ollama run llama3.1:8b
# Output iniziale mostra: "GPU layers: X/32"
# Se X=0 → tutto su CPU → problema driver o VRAM insufficiente

# Forza numero di layer GPU
OLLAMA_GPU_LAYERS=32 ollama run llama3.1:8b
```

### Out of memory (VRAM insufficiente)

```bash
# Usa versione più quantizzata (meno qualità, meno VRAM)
ollama pull llama3.1:8b-instruct-q4_0   # 4-bit, minima VRAM
ollama pull llama3.1:8b-instruct-q8_0   # 8-bit, qualità migliore

# Oppure modello più piccolo
ollama pull llama3.2:3b
```

### Open WebUI non si connette a Ollama

```bash
# Verifica che Ollama accetti connessioni esterne
curl http://<IP-SERVER>:11434/api/tags

# Se timeout: Ollama è in ascolto solo su localhost
# Imposta OLLAMA_HOST=0.0.0.0 (vedi sezione setup)

# In Docker: verifica network
docker network inspect bridge
docker logs open-webui | grep -i ollama
```

---

## 🔒 Checklist sicurezza per deploy aziendale

```
□ Ollama non esposto su internet (solo LAN o VPN)
□ Open WebUI con autenticazione obbligatoria
□ Signup pubblico disabilitato in Open WebUI
□ Backup volumi Docker configurato
□ Firewall: porta 11434 accessibile solo da subnet interna
□ HTTPS abilitato (tramite reverse proxy + cert interno)
□ Log rotazione configurata
□ Monitoraggio uptime (Prometheus/Grafana o simile)
□ Policy aziendale AI documentata e distribuita
□ Utenti formati su limiti e uso corretto del sistema
```

---

*Guida tecnica mantenuta da [Nicholas Izzo](https://github.com/NicholasIzzo) — parte di [ai-practical-guide](https://nicholasizzo.github.io/ai-practical-guide/)*
