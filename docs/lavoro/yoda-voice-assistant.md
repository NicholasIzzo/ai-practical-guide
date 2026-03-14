# 🤖 Yoda — Voice Assistant Locale con AI

> Un assistente vocale completamente locale, zero cloud, zero abbonamenti, costruito con Python, Whisper e Ollama.

## 📋 Panoramica

Yoda è un voice assistant personale che gira interamente sul tuo PC. Nessun dato esce da casa tua — tutto il processing avviene in locale grazie a modelli AI open source.

### Stack Tecnologico

| Componente | Tecnologia | Ruolo |
|---|---|---|
| Speech-to-Text | Whisper small (GPU) | Trascrive la voce in testo |
| LLM | Qwen3.5:2b via Ollama | Risponde alle domande |
| Text-to-Speech | pyttsx3 + Voce Elsa IT | Legge le risposte |
| Domotica | Home Assistant API | Controlla luci e TV |
| Automazione | pyautogui + Selenium | Controlla il PC |

---

## ⚙️ Requisiti Hardware

- **GPU**: NVIDIA con almeno 4GB VRAM (testato su RTX 3060 Ti 8GB)
- **RAM**: 16GB+ consigliati
- **OS**: Windows 10/11
- **Python**: 3.10+

---

## 📦 Installazione

### 1. Installa le dipendenze Python

```bash
pip install faster-whisper sounddevice scipy numpy requests pyttsx3 pvporcupine pyautogui pywin32 pillow psutil selenium playwright pyperclip keyboard mouse
```

### 2. Installa Ollama

Scarica da [https://ollama.com](https://ollama.com) e installa il modello:

```bash
ollama pull qwen3.5:2b
```

### 3. Installa faster-whisper

```bash
pip install faster-whisper
```

### 4. Clona e avvia

```bash
git clone https://github.com/NicholasIzzo/ai-practical-guide
cd ai-practical-guide/tools/yoda
python assistant.py
```

---

## 🗣️ Comandi Vocali

### ⏰ Tempo e Data
- *"Che ore sono?"*
- *"Che giorno è oggi?"*

### 🌤️ Meteo
- *"Che tempo fa a Milano?"*
- *"Meteo Roma"*

### 💡 Domotica (Home Assistant)
- *"Accendi la luce in sala"*
- *"Spegni la luce in cucina"*
- *"Accendi la TV"*
- *"Spegni tutte le luci"*
- *"Batteria telefono"*
- *"Aggiungi alla spesa il latte"*

### 💻 Controllo PC
- *"Apri Chrome"*
- *"Apri Discord"*
- *"Apri Steam"*
- *"Apri VS Code"*
- *"Alza il volume"*
- *"Abbassa il volume"*
- *"Silenzia"*
- *"Fai uno screenshot"*
- *"Quanta RAM uso?"*
- *"Spegni il PC tra 10 minuti"*
- *"Riavvia il PC"*

### 🌐 Siti Web
- *"Vai su YouTube"*
- *"Apri Netflix"*
- *"Vai su GitHub"*
- *"Apri LinkedIn"*
- *"Vai sull'università"* (Unipegaso)
- *"Apri ChatGPT"*
- *"Cerca su YouTube lo-fi music"*
- *"Cerca su Google come installare Python"*

### 🎮 Giochi Steam
- *"Avvia Hogwarts"*
- *"Avvia Days Gone"*
- *"Avvia Stray"*
- *"Avvia PUBG"*

### 📝 Note
- *"Prendi nota: comprare il latte"*
- *"Segna che ho una riunione domani"*
- *"Leggi le mie note"*

### ⏱️ Timer
- *"Metti un timer da 10 minuti"*
- *"Timer 30 secondi"*

### 🎵 Musica
- *"Metti musica lofi"*
- *"Metti la canzone Bohemian Rhapsody"*

### ❌ Chiudi sessione
- *"Arrivederci Yoda"*
- *"Ciao Yoda"*
- *"Chiudi Yoda"*

---

## 🏗️ Architettura

```
Voce
  ↓
Brio 500 / Microfono
  ↓
Whisper small (RTX GPU) → Testo trascritto
  ↓
Python — Intent Detection
  ↓
  ┌─ Ora/Data → datetime (locale, istantaneo)
  ├─ Meteo → Open-Meteo API (gratuita)
  ├─ Note → file .txt locale
  ├─ Timer → threading Python
  ├─ Azioni PC → subprocess / os / pyautogui
  ├─ Siti web → os.system("start url")
  ├─ Domotica → Home Assistant REST API
  └─ Domande generali → Qwen3.5:2b via Ollama
  ↓
Risposta testo
  ↓
pyttsx3 (Voce Elsa IT) → Audio
```

---

## 🔧 Configurazione

Modifica queste variabili in cima ad `assistant.py`:

```python
# Home Assistant
HA_URL = "http://TUO_IP_HA:8123"
HA_TOKEN = "IL_TUO_TOKEN_HA"

# Microfono (device index)
# Per trovarlo: python -c "import sounddevice; print(sounddevice.query_devices())"
device = 3  # Logitech Brio 500

# Modello Ollama
"model": "qwen3.5:2b"  # cambia con qwen3.5:9b per più intelligenza
```

---

## 🚀 Avvio Automatico con Windows

1. Crea `yoda.bat`:
```bat
@echo off
cd C:\Users\tuonome\voice-assistant
pythonw assistant.py
```

2. Copia in:
```
C:\Users\tuonome\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\
```

Ollama si avvia automaticamente — Yoda parte con Windows senza aprire finestre.

---

## 📈 Performance (RTX 3060 Ti 8GB)

| Operazione | Tempo |
|---|---|
| Trascrizione Whisper small | ~0.5-1s |
| Risposta Qwen3.5:2b | ~2-3s |
| Comandi locali (ora, note, luci) | istantaneo |
| **Totale medio** | **~3-4s** |

---

## 🔮 Roadmap

- [ ] Wake word "Yoda" con Porcupine
- [ ] Memoria conversazione (RAG)
- [ ] Integrazione Spotify
- [ ] Promemoria con orario
- [ ] Interfaccia grafica
- [ ] Email vocali via Outlook

---

## 👤 Autore

**Nicholas Izzo** — Sistemista, studente L31 Informatica AI @ Unipegaso  
[LinkedIn](https://www.linkedin.com/in/nicholas-izzo-842797290/) | [GitHub](https://github.com/NicholasIzzo)

> *"Zero cloud. Zero abbonamenti. Solo AI locale."*
