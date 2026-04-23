# NOVA — Architecture

## Stack technique

### Matériel

| Rôle | Machine | Statut |
|------|---------|--------|
| Cerveau Nova (LLM) | Framework Desktop 64GB AMD AI Max+ (Linux) | A acheter |
| Domotique | RPI4 — Home Assistant OS | En place |
| Orchestration | RPI5 — n8n, Docker, AdGuard Home | En place |
| Workstation / Claude Code | Moon — WSL2, i9-12900HK, 32GB | En place |
| Présence par pièce | 2x Everything Presence Light + 1x Everything Presence One | A installer |

### Pipeline voix (Phase 1)

```
"Hey Nova" → Wake Word (OpenWakeWord) → STT (Whisper) → LLM 70B Q6 local
                                                              ↓ streaming tokens
                                                         TTS (Kokoro) chunk 1 → 🔊
                                                         TTS (Kokoro) chunk 2 → 🔊
                                                         ...
Latence perçue cible : < 1s (streaming token-by-token)
```

### Pipeline streaming TTS (à implémenter)

```
Thread 1 : Ollama stream API → tokens → accumuler jusqu'à [.,!?] ou ~8 mots → chunk queue
Thread 2 : chunk queue → Kokoro TTS → WAV queue
Thread 3 : WAV queue → aplay / mpv (lecture séquentielle sans gap)
```

### Composants logiciels

| Composant | Outil | Localisation |
|-----------|-------|-------------|
| Agent IA | OpenClaw | Framework Desktop |
| LLM local | Ollama + Qwen3 70B Q6 / Llama3 70B Q6 | Framework Desktop |
| Wake word | OpenWakeWord (custom "Nova") | RPI5 ou ESP32 |
| STT | Wyoming Whisper (large-v3) | Framework Desktop |
| TTS | Kokoro (voix bm_george) | RPI5 (existant) |
| Domotique | Home Assistant | RPI4 |
| Présence | Everything Presence mmWave | 3 pièces |
| Orchestration | n8n | RPI5 |
| Interface Telegram | Alfred (bot existant) | Moon/n8n |
| Surveillance infra | moon-monitoring | Moon |
| Transcription réunions | Scriberr + Meeting Assistant | Moon |

### Présence par pièce — Everything Presence

- **Everything Presence One** (le plus précis) → Bureau (Cédric work zone)
- **Everything Presence Light #1** → Salon
- **Everything Presence Light #2** → Chambre principale

Détection mmWave = personnes immobiles (lire, dormir, travailler) — pas juste le mouvement.

### Confidentialité

```
Profil Cédric (privé)
├── Historique conversation Nova
├── Tracking présence détaillé
├── Calendrier + réunions
├── Knowledge base personnelle (Phase 2)
└── Accès infra (moon-monitoring, Claude Code)

Profil commun (partagé)
├── Contrôle domotique de base
├── Lumières, température, Sonos
└── Scènes communes
```

## Dépendances existantes

- `~/moon-monitoring/` — monitoring infra, ia_memory.md, pending_actions.json
- `~/meeting-assistant/` — Scriberr API, generate_document.py, ma_auto.py
- `~/docker/` — open-webui, Scriberr
- n8n workflows : Alfred (rcFlIHE3QPRkFdhc), Moon Monitoring Actions (hslIAsJIAtSZ8h42)
