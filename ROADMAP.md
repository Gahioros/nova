# NOVA — Roadmap

## Phase 0 — Fondations (avant achat hardware) ✅ partiel

- [x] Alfred : Claude Code via Telegram, session continue par chat_id
- [x] Kokoro TTS sur RPI5 (voix bm_george)
- [x] Wyoming Whisper sur RPI5 (STT)
- [x] Ollama sur Moon + RPI5 (petits modèles)
- [x] Home Assistant + intégration Ollama
- [x] n8n orchestration
- [x] Scriberr + Meeting Assistant
- [ ] Installer les capteurs Everything Presence (2x Light + 1x One)
- [ ] Explorer OpenClaw sur infra actuelle (Telegram + petits modèles)

## Phase 1 — Assistant vocal fluide

**Prérequis hardware** : Framework Desktop 64GB AMD AI Max+ (Linux)

- [ ] Installer Framework Desktop (Ubuntu Server / NixOS)
- [ ] Ollama + Qwen3 70B Q6 ou Llama3 70B Q6
- [ ] Déployer OpenClaw sur Framework Desktop
- [ ] Implémenter streaming TTS (plugin OpenClaw)
  - Ollama stream API → chunks → Kokoro → queue audio
  - Latence cible < 1s perçue
- [ ] OpenWakeWord custom "Hey Nova"
- [ ] Intégrer Everything Presence dans HA (présence par pièce)
- [ ] Automatisations contextuelles par personne/pièce
- [ ] Briefing matinal personnalisé
- [ ] Intégration Sonos contextuelle
- [ ] Profil confidentialité Cédric vs profil partagé
- [ ] Intégration Meeting Assistant → contexte réunions accessible à la voix

## Phase 2 — 2nd cerveau

- [ ] Choisir frontend (Obsidian)
- [ ] Pipeline ingest : articles, notes, réunions Scriberr, repos → raw/
- [ ] LLM compile wiki .md (structure, backlinks, articles par concept)
- [ ] Index auto-maintenu pour Q&A sans RAG
- [ ] Q&A contre la knowledge base via Nova voix
- [ ] Journalisation passive journalière → alimente la KB
- [ ] Linting KB : détection incohérences, connexions manquantes

## Phase 3 — Proactivité avancée

- [ ] Anticipation déplacements (calendrier + trafic)
- [ ] Mode absent automatique (présence + sécurité)
- [ ] Apprentissage actif : Nova documente ses propres skills
- [ ] Vision avec Frigate (reconnaissance personnes, alertes)
- [ ] Contrôle navigateur / tâches web (OpenClaw browser control)

## Décisions en attente

- [ ] Achat Framework Desktop 64GB (~2500€) — timing : dès que budget OK
- [ ] Architecture réseau (switch non managé vs UniFi UCG-Max) — impact sur placement des capteurs
