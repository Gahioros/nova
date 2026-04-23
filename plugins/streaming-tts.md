# Plugin — Streaming TTS

## Concept

Réduire la latence perçue de Nova de ~3-5s à ~0.5-1s en démarrant la synthèse vocale
avant que le LLM ait fini de générer sa réponse complète.

## Architecture (3 threads)

```python
# Thread 1 : LLM stream → chunks
def stream_to_chunks(ollama_stream):
    buffer = ""
    for token in ollama_stream:
        buffer += token
        # Découper sur fin de phrase ou ~8 mots
        if re.search(r'[.!?,;]', buffer) or len(buffer.split()) >= 8:
            chunk_queue.put(buffer)
            buffer = ""
    if buffer:
        chunk_queue.put(buffer)

# Thread 2 : chunks → WAV (Kokoro)
def chunks_to_wav():
    while True:
        chunk = chunk_queue.get()
        wav = kokoro_synthesize(chunk)  # ~0.2-0.3s
        audio_queue.put(wav)

# Thread 3 : WAV → lecture séquentielle
def play_audio():
    while True:
        wav = audio_queue.get()
        play(wav)  # sans gap entre les morceaux
```

## Latence cible

```
LLM génère chunk 1 (~0.3s) → TTS chunk 1 (~0.2s) → lecture commence
Latence perçue : ~0.5s
(pendant ce temps : LLM génère chunk 2, TTS chunk 2...)
```

## Dépendances

- Ollama streaming API : `POST /api/generate` avec `stream: true`
- Kokoro TTS (déjà sur RPI5) ou déplacer sur Framework Desktop
- `sounddevice` ou `pyaudio` pour lecture sans gap

## Statut

- [ ] Prototype Python standalone
- [ ] Intégration OpenClaw comme plugin
- [ ] Test latence réelle sur Framework Desktop 64GB
