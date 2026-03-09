# 🏠 AI in Locale vs Cloud

Quando ha senso usare un modello AI sul proprio hardware invece di usare i servizi cloud come ChatGPT o Claude.

---

## Il concetto

I modelli AI come ChatGPT e Claude girano su server remoti — ogni prompt che invii passa attraverso internet e viene elaborato da server di terze parti.

L'**AI in locale** significa far girare il modello direttamente sul tuo PC o server, senza inviare dati a nessuno.

---

## Quando usare AI in locale

### ✅ Dati sensibili o confidenziali
- Codice sorgente proprietario
- Documenti aziendali riservati
- Dati personali (GDPR)
- Password, configurazioni con credenziali

### ✅ Task ripetitivi ad alto volume
- Elaborare migliaia di documenti
- Script di automazione che chiamano l'AI continuamente
- Pipeline di data processing

### ✅ Nessuna connessione internet
- Ambienti air-gapped
- Server senza accesso esterno
- Uso offline

### ✅ Controllo totale
- Vuoi personalizzare il modello (fine-tuning)
- Vuoi integrazione con sistemi interni
- Vuoi evitare dipendenza da servizi esterni

---

## Quando usare AI cloud

### ✅ Massima qualità
- I modelli cloud (GPT-4o, Claude 3.7, Gemini) sono significativamente più capaci dei modelli locali di dimensioni simili

### ✅ Hardware limitato
- Fare girare un modello capace in locale richiede GPU potente o molta RAM

### ✅ Accesso a internet e dati aggiornati
- I modelli cloud con browsing accedono a informazioni recenti

### ✅ Facilità d'uso
- Nessuna installazione, aggiornamenti automatici

---

## Tool per AI in locale

### Ollama ⭐ Raccomandato

Ollama è il modo più semplice per scaricare ed eseguire modelli open source in locale.

**Installazione (Linux/Mac):**
```bash
curl -fsSL https://ollama.com/install.sh | sh
```

**Installazione (Windows):**
Scarica da [ollama.com](https://ollama.com)

**Uso base:**
```bash
# Scarica e avvia un modello
ollama run llama3

# Avvia Mistral
ollama run mistral

# Lista modelli scaricati
ollama list

# Rimuovi un modello
ollama rm llama3
```

**API compatibile con OpenAI:**
```bash
# Ollama espone un'API su localhost:11434
curl http://localhost:11434/api/generate -d '{
  "model": "llama3",
  "prompt": "Scrivi uno script Bash per monitorare il disco"
}'
```

---

### LM Studio

Interfaccia grafica per scaricare ed eseguire modelli localmente. Ottimo per chi preferisce una UI invece del terminale.

- Download da [lmstudio.ai](https://lmstudio.ai)
- Supporta tutti i modelli GGUF (formato quantizzato)
- Espone API locale compatibile con OpenAI
- Ottimo per testare diversi modelli rapidamente

---

### Docker + Ollama (per homelab)

```yaml
services:
  ollama:
    image: ollama/ollama
    container_name: ollama
    restart: unless-stopped
    ports:
      - "11434:11434"
    volumes:
      - /volume1/docker/ollama:/root/.ollama
    # Per GPU NVIDIA:
    # deploy:
    #   resources:
    #     reservations:
    #       devices:
    #         - driver: nvidia
    #           count: 1
    #           capabilities: [gpu]
```

---

## Modelli consigliati per uso locale

| Modello | RAM necessaria | Punti di forza | Caso d'uso |
|---|---|---|---|
| **Llama 3.2 3B** | 4GB | Veloce, leggero | Task semplici, risposta rapida |
| **Llama 3.1 8B** | 8GB | Buon equilibrio | Uso generale |
| **Llama 3.1 70B** | 40GB+ | Qualità elevata | Richiede GPU potente |
| **Mistral 7B** | 8GB | Ottimo per codice | Coding, script |
| **Mistral Nemo 12B** | 12GB | Multilingue | Italiano e lingue europee |
| **DeepSeek Coder** | 8GB | Specializzato in codice | Sviluppo software |
| **Phi-3 Mini** | 4GB | Compatto e capace | Hardware limitato |
| **Gemma 2 9B** | 10GB | Google, buona qualità | Uso generale |

---

## Requisiti hardware

### Minimo (modelli 7-8B):
- RAM: 16GB (8GB per il modello + 8GB per il sistema)
- CPU: qualsiasi moderno (lento ma funziona)
- Storage: 10-20GB per modello

### Consigliato (modelli 13B):
- RAM: 32GB
- GPU: 8GB VRAM (GTX 1080 / RTX 3060 o superiore)
- Storage: 20-30GB per modello

### Per modelli grandi (70B+):
- RAM: 64GB+
- GPU: 24GB+ VRAM (RTX 3090 / 4090)
- Storage: 40-80GB per modello

> **Nota sul NAS ARM64:** Il Ugreen DH4300 Plus può girare Ollama con modelli piccoli (3B-7B) ma sarà lento — meglio usarlo per API e automazioni notturne, non per chat interattiva.

---

## Integrazione con Open WebUI

Open WebUI è un'interfaccia web simile a ChatGPT che si connette a Ollama.

```yaml
services:
  open-webui:
    image: ghcr.io/open-webui/open-webui:main
    container_name: open-webui
    restart: unless-stopped
    ports:
      - "<PORT>:8080"
    environment:
      - OLLAMA_BASE_URL=http://<NAS_IP>:11434
    volumes:
      - /volume1/docker/open-webui:/app/backend/data
```

Accedi da browser → hai la tua ChatGPT privata in locale.

---

## Confronto finale

| | AI Cloud | AI Locale |
|---|---|---|
| Qualità | ⭐⭐⭐⭐⭐ Eccellente | ⭐⭐⭐ Buona (in crescita) |
| Privacy | ❌ Dati a terzi | ✅ Tutto in locale |
| Costo | Abbonamento / API | Solo elettricità |
| Setup | ✅ Zero | ⚠️ Richiede configurazione |
| Hardware | ✅ Nessuno | ⚠️ RAM/GPU necessari |
| Aggiornamenti | ✅ Automatici | Manuali |
| Offline | ❌ No | ✅ Sì |

---

> 💡 La strategia migliore è ibrida: usa i modelli cloud per task importanti dove serve qualità massima, e modelli locali per automazioni, dati sensibili e task ripetitivi.
