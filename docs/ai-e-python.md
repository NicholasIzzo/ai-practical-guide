# 🐍 AI e Python — Librerie Essenziali e Primi Progetti

Guida pratica per iniziare a usare l'AI con Python — dalle librerie fondamentali ai primi progetti concreti.

---

## Perché Python per l'AI?

Python è il linguaggio dominante nell'ecosistema AI per tre motivi:
- Sintassi semplice e leggibile
- Librerie mature e ben documentate
- Community enorme con risorse gratuite

Non serve essere esperti di Python per iniziare — basta conoscere le basi.

---

## Setup dell'ambiente

```bash
# Crea un ambiente virtuale (consigliato)
python -m venv ai-env
source ai-env/bin/activate  # Linux/Mac
ai-env\Scripts\activate     # Windows

# Installa le librerie base
pip install openai anthropic python-dotenv
```

### Gestione delle API key con .env
```bash
# Crea file .env (mai committare su Git!)
echo "ANTHROPIC_API_KEY=sk-..." > .env
echo "OPENAI_API_KEY=sk-..." >> .env
echo ".env" >> .gitignore
```

```python
from dotenv import load_dotenv
import os

load_dotenv()
api_key = os.getenv("ANTHROPIC_API_KEY")
```

---

## Le librerie essenziali

### 1. Anthropic SDK — Claude API

```python
import anthropic

client = anthropic.Anthropic()  # legge ANTHROPIC_API_KEY da .env

response = client.messages.create(
    model="claude-sonnet-4-20250514",
    max_tokens=1024,
    messages=[
        {"role": "user", "content": "Spiegami cosa fa questo script Bash: ls -la /etc"}
    ]
)

print(response.content[0].text)
```

---

### 2. OpenAI SDK — GPT API

```python
from openai import OpenAI

client = OpenAI()  # legge OPENAI_API_KEY da .env

response = client.chat.completions.create(
    model="gpt-4o",
    messages=[
        {"role": "system", "content": "Sei un esperto di Linux."},
        {"role": "user", "content": "Come monitoro l'uso della CPU in tempo reale?"}
    ]
)

print(response.choices[0].message.content)
```

---

### 3. Ollama Python — modelli locali

```bash
pip install ollama
```

```python
import ollama

response = ollama.chat(
    model='llama3',
    messages=[
        {'role': 'user', 'content': 'Analizza questo log Docker e dimmi se ci sono errori'}
    ]
)

print(response['message']['content'])
```

---

### 4. LangChain — orchestrazione AI

LangChain permette di costruire pipeline AI complesse — catene di prompt, memoria, agenti.

```bash
pip install langchain langchain-anthropic
```

```python
from langchain_anthropic import ChatAnthropic
from langchain_core.messages import HumanMessage

model = ChatAnthropic(model="claude-sonnet-4-20250514")

response = model.invoke([
    HumanMessage(content="Scrivi uno script Python per monitorare i container Docker")
])

print(response.content)
```

---

### 5. Transformers (HuggingFace) — modelli open source

```bash
pip install transformers torch
```

```python
from transformers import pipeline

# Classificazione del testo
classifier = pipeline("text-classification", model="distilbert-base-uncased-finetuned-sst-2-english")
result = classifier("This Docker configuration is excellent!")
print(result)  # [{'label': 'POSITIVE', 'score': 0.99}]

# Generazione testo con modello locale
generator = pipeline("text-generation", model="gpt2")
result = generator("Il futuro dell'AI è", max_length=50)
print(result[0]['generated_text'])
```

---

## Progetti pratici

### Progetto 1 — Analizzatore di log Docker

```python
import anthropic
import subprocess

def analyze_docker_logs(container_name: str) -> str:
    # Prendi gli ultimi 50 log del container
    result = subprocess.run(
        ["docker", "logs", "--tail", "50", container_name],
        capture_output=True, text=True
    )
    logs = result.stdout + result.stderr

    client = anthropic.Anthropic()
    response = client.messages.create(
        model="claude-sonnet-4-20250514",
        max_tokens=1024,
        messages=[{
            "role": "user",
            "content": f"""Analizza questi log Docker del container '{container_name}'.
            Identifica errori, warning e comportamenti anomali.
            Fornisci un riassunto e suggerimenti per risolvere eventuali problemi.

            LOG:
            {logs}"""
        }]
    )
    return response.content[0].text

# Uso
print(analyze_docker_logs("nginx-proxy-manager"))
```

---

### Progetto 2 — Generatore di documentazione automatica

```python
import anthropic
import sys

def generate_docs(script_path: str) -> str:
    with open(script_path, 'r') as f:
        code = f.read()

    client = anthropic.Anthropic()
    response = client.messages.create(
        model="claude-sonnet-4-20250514",
        max_tokens=2048,
        messages=[{
            "role": "user",
            "content": f"""Genera documentazione tecnica in Markdown per questo script.
            Includi: descrizione, prerequisiti, parametri, esempi d'uso, note importanti.

            SCRIPT:
            {code}"""
        }]
    )
    return response.content[0].text

# Uso: python script.py mio_script.sh
if __name__ == "__main__":
    docs = generate_docs(sys.argv[1])
    print(docs)
    # Salva su file
    with open("DOCS.md", "w") as f:
        f.write(docs)
```

---

### Progetto 3 — Chatbot con memoria per lo studio

```python
import anthropic

client = anthropic.Anthropic()
conversation_history = []

def chat(user_message: str, subject: str = "informatica") -> str:
    conversation_history.append({
        "role": "user",
        "content": user_message
    })

    response = client.messages.create(
        model="claude-sonnet-4-20250514",
        max_tokens=1024,
        system=f"""Sei un tutor universitario esperto di {subject}.
        Rispondi in italiano. Usa esempi pratici.
        Se l'utente sbaglia, correggilo gentilmente spiegando il perché.""",
        messages=conversation_history
    )

    assistant_message = response.content[0].text
    conversation_history.append({
        "role": "assistant",
        "content": assistant_message
    })

    return assistant_message

# Uso interattivo
print("Tutor AI - digita 'exit' per uscire")
while True:
    user_input = input("\nTu: ")
    if user_input.lower() == 'exit':
        break
    response = chat(user_input)
    print(f"\nTutor: {response}")
```

---

## Librerie per casi d'uso specifici

| Libreria | Uso | Installazione |
|---|---|---|
| `anthropic` | Claude API | `pip install anthropic` |
| `openai` | GPT API | `pip install openai` |
| `ollama` | Modelli locali | `pip install ollama` |
| `langchain` | Pipeline e agenti | `pip install langchain` |
| `transformers` | Modelli HuggingFace | `pip install transformers` |
| `sentence-transformers` | Embeddings e similarity | `pip install sentence-transformers` |
| `chromadb` | Vector database | `pip install chromadb` |
| `pytesseract` | OCR con AI | `pip install pytesseract` |
| `whisper` | Speech-to-text | `pip install openai-whisper` |

---

> 💡 Inizia con un progetto piccolo e concreto — come l'analizzatore di log. Impari molto di più costruendo qualcosa di utile che studiando le librerie in astratto.
