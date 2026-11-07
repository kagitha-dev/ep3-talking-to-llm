# Ep 3 · Talking to an LLM with code

Java 17+, Maven, and Ollama running `qwen3.5:4b` locally.

## Before you run

```
ollama pull qwen3.5:4b
```

Ollama must be running (it runs in the background after install). Check with:

```
curl http://localhost:11434
```

## Run each step (from this folder)

```
mvn -q compile
mvn -q exec:java -Dexec.mainClass=airadar.Step1_FirstCall
mvn -q exec:java -Dexec.mainClass=airadar.Step2_Stateless
mvn -q exec:java -Dexec.mainClass=airadar.Step3_SystemPrompt
mvn -q exec:java -Dexec.mainClass=airadar.Step4_TerminalChatbot
mvn -q exec:java -Dexec.mainClass=airadar.Step5_StructuredOutput
```

Or open the folder in IntelliJ and press Run on any `StepN` class.

| Step | File | What it shows |
|---|---|---|
| 1 | `Step1_FirstCall` | Calling an AI is just sending JSON to a URL (raw JSON back) |
| 2 | `Step2_Stateless` | The API forgets between calls; resending history fixes it |
| 3 | `Step3_SystemPrompt` | Same question, with and without a system prompt |
| 4 | `Step4_TerminalChatbot` | A chatbot whose "memory" is a Java list, with token counts |
| 5 | `Step5_StructuredOutput` | AI Radar classifies `feed.json` and writes flashcards as JSON |

`Ollama.java` is a small helper used by steps 2–5. It does exactly what Step 1 does.
Every call sends `"think": false`, `temperature 0` and a fixed `seed`, so retakes give the same output.
