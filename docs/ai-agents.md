# 🤖 AI Agents — Cosa Sono e Come Funzionano

Dalle chat AI agli agenti autonomi: come i modelli AI passano dal rispondere domande all'eseguire task complessi in autonomia.

---

## Cos'è un AI Agent?

Un AI Agent è un sistema in cui un LLM non si limita a rispondere — prende decisioni, usa strumenti e completa task multi-step in autonomia.

```
Chat AI tradizionale:
Utente → Domanda → AI → Risposta

AI Agent:
Utente → Obiettivo → Agent → Pianifica → Esegue azioni → Verifica → Risultato
                                │
                          Usa strumenti:
                          - Cerca sul web
                          - Legge/scrive file
                          - Chiama API
                          - Esegue codice
```

---

## Il loop ReAct (Reason + Act)

Il pattern fondamentale degli AI Agent:

```
1. THOUGHT  — "Devo trovare il prezzo attuale di Azure VM"
2. ACTION   — Cerca sul web "Azure VM pricing 2025"
3. OBSERVE  — Risultati della ricerca
4. THOUGHT  — "Ho trovato i prezzi, ora calcolo il costo mensile"
5. ACTION   — Calcola con Python
6. OBSERVE  — Risultato del calcolo
7. THOUGHT  — "Ho tutto quello che serve, rispondo all'utente"
8. ANSWER   — Risposta finale con dati aggiornati
```

---

## Strumenti comuni degli Agent

| Strumento | Cosa fa |
|---|---|
| Web search | Cerca informazioni aggiornate |
| Code interpreter | Esegue codice Python/Bash |
| File system | Legge e scrive file |
| API calls | Interagisce con servizi esterni |
| Database | Interroga database |
| Email/Calendar | Gestisce comunicazioni |
| Browser | Naviga siti web |

---

## Costruire un Agent semplice con Python

### Agent base con tool use (Anthropic)

```python
import anthropic
import subprocess
import json

client = anthropic.Anthropic()

# Definisci gli strumenti disponibili
tools = [
    {
        "name": "execute_bash",
        "description": "Esegue un comando Bash sul sistema e restituisce l'output",
        "input_schema": {
            "type": "object",
            "properties": {
                "command": {
                    "type": "string",
                    "description": "Il comando Bash da eseguire"
                }
            },
            "required": ["command"]
        }
    },
    {
        "name": "read_file",
        "description": "Legge il contenuto di un file",
        "input_schema": {
            "type": "object",
            "properties": {
                "path": {
                    "type": "string",
                    "description": "Il percorso del file da leggere"
                }
            },
            "required": ["path"]
        }
    }
]

def execute_tool(tool_name: str, tool_input: dict) -> str:
    if tool_name == "execute_bash":
        result = subprocess.run(
            tool_input["command"],
            shell=True,
            capture_output=True,
            text=True,
            timeout=30
        )
        return result.stdout + result.stderr

    elif tool_name == "read_file":
        try:
            with open(tool_input["path"], 'r') as f:
                return f.read()
        except Exception as e:
            return f"Errore: {e}"

def run_agent(task: str) -> str:
    messages = [{"role": "user", "content": task}]

    while True:
        response = client.messages.create(
            model="claude-sonnet-4-20250514",
            max_tokens=4096,
            tools=tools,
            messages=messages
        )

        # Se l'agent ha finito
        if response.stop_reason == "end_turn":
            for block in response.content:
                if hasattr(block, 'text'):
                    return block.text

        # Se l'agent vuole usare uno strumento
        if response.stop_reason == "tool_use":
            messages.append({"role": "assistant", "content": response.content})

            tool_results = []
            for block in response.content:
                if block.type == "tool_use":
                    print(f"→ Usando strumento: {block.name}({block.input})")
                    result = execute_tool(block.name, block.input)
                    tool_results.append({
                        "type": "tool_result",
                        "tool_use_id": block.id,
                        "content": result
                    })

            messages.append({"role": "user", "content": tool_results})

# Esempio d'uso
result = run_agent("Controlla quanti container Docker sono in esecuzione e mostrami il loro stato")
print(result)
```

---

## Framework per AI Agent

### LangChain Agents

```python
from langchain_anthropic import ChatAnthropic
from langchain.agents import AgentExecutor, create_tool_calling_agent
from langchain_core.tools import tool
from langchain_core.prompts import ChatPromptTemplate
import subprocess

@tool
def run_command(command: str) -> str:
    """Esegue un comando shell e restituisce l'output."""
    result = subprocess.run(command, shell=True, capture_output=True, text=True)
    return result.stdout + result.stderr

@tool
def check_disk_space(path: str = "/") -> str:
    """Controlla lo spazio disco disponibile."""
    result = subprocess.run(f"df -h {path}", shell=True, capture_output=True, text=True)
    return result.stdout

tools = [run_command, check_disk_space]

model = ChatAnthropic(model="claude-sonnet-4-20250514")
prompt = ChatPromptTemplate.from_messages([
    ("system", "Sei un assistente sistemista. Usa gli strumenti disponibili per completare i task."),
    ("human", "{input}"),
    ("placeholder", "{agent_scratchpad}")
])

agent = create_tool_calling_agent(model, tools, prompt)
executor = AgentExecutor(agent=agent, tools=tools, verbose=True)

result = executor.invoke({"input": "Controlla lo spazio disco e dimmi se ci sono problemi"})
print(result["output"])
```

---

## CrewAI — Multi-Agent

CrewAI permette di creare team di agent che collaborano su task complessi.

```python
from crewai import Agent, Task, Crew

# Definisci gli agenti del team
researcher = Agent(
    role='Ricercatore',
    goal='Trovare informazioni aggiornate su tecnologie cloud',
    backstory='Esperto di ricerca tecnica con attenzione ai dettagli',
    verbose=True
)

writer = Agent(
    role='Scrittore Tecnico',
    goal='Trasformare le informazioni in documentazione chiara',
    backstory='Specializzato in documentazione tecnica italiana',
    verbose=True
)

# Definisci i task
research_task = Task(
    description='Ricerca le ultime novità su Azure AI Services',
    agent=researcher
)

writing_task = Task(
    description='Scrivi una guida pratica basata sulla ricerca effettuata',
    agent=writer
)

# Crea il team e avvia
crew = Crew(agents=[researcher, writer], tasks=[research_task, writing_task])
result = crew.kickoff()
print(result)
```

---

## Casi d'uso pratici per il homelab

### Agent per il monitoring
```
Task: "Controlla tutti i container Docker, identifica quelli con
      RAM > 80%, leggi i loro log recenti e dimmi se c'è qualcosa
      di anomalo. Suggerisci azioni correttive."
```

### Agent per la documentazione automatica
```
Task: "Analizza la cartella /volume1/docker, leggi tutti i
      docker-compose.yml e genera una documentazione aggiornata
      di tutti i servizi in esecuzione con porte, volumi e stato."
```

### Agent per la sicurezza
```
Task: "Controlla i log di fail2ban e nginx delle ultime 24 ore,
      identifica IP sospetti, verifica se sono nella lista di
      blocco e suggerisci regole firewall da aggiungere."
```

---

## Limiti e rischi degli AI Agent

### Cosa può andare storto:
- **Azioni irreversibili** — un agent con accesso al filesystem può cancellare file
- **Loop infiniti** — l'agent continua a riprovare senza riuscire
- **Allucinazioni in azione** — esegue comandi basandosi su informazioni false
- **Escalation di permessi** — l'agent ottiene più accesso del necessario

### Best practice:
- ✅ Sempre human-in-the-loop per azioni critiche
- ✅ Principio del minimo privilegio per i tool
- ✅ Timeout su tutti i task
- ✅ Dry-run mode prima di eseguire azioni reali
- ✅ Logging completo di ogni azione

---

> 💡 Gli AI Agent sono potenti ma vanno usati con cautela. Inizia con agent che leggono e analizzano — aggiungi la capacità di scrivere e agire solo quando sei sicuro del comportamento.
