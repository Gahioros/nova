# NOVA — Vision

> "Hey Nova."

Nova est un assistant personnel local, proactif et privé. Inspiré de Jarvis (Iron Man),
conçu pour anticiper, mémoriser, agir — sans jamais envoyer de données dans le cloud.

## Philosophie

- **Local-first** : tout tourne sur l'infra personnelle (Moon, RPI4/RPI5, Framework Desktop)
- **Proactif** : Nova initie, n'attend pas d'être sollicité
- **Privé** : chaque utilisateur a son propre espace, les données restent chez soi
- **Apprenant** : Nova documente ses propres skills et s'améliore au fil du temps

## Ce que Nova fera

### Phase 1 — Assistant vocal et domestique

- Wake word "Hey Nova" toujours actif (OpenWakeWord custom)
- Pipeline voix fluide < 2s : Whisper STT → LLM local 70B → Kokoro TTS streaming
- Streaming token-by-token : TTS commence avant que le LLM ait fini (latence perçue ~0.5-1s)
- Contrôle domotique via Home Assistant (lumières, température, Sonos, scènes)
- Présence intelligente par pièce (capteurs mmWave Everything Presence)
- Briefing matinal personnalisé (calendrier, météo, rappels, état infra)
- Retour au foyer contextualisé ("Agnes est dans le salon, ta réunion de demain est à 9h")
- Confidentialité par profil : chaque utilisateur a son espace, invisible aux autres
- Intégration Scriberr/Meeting Assistant : contexte réunions accessible à la voix
- Orchestration via n8n + OpenClaw
- Interface Telegram (Alfred existant) en parallèle de la voix

### Phase 2 — 2nd cerveau (Knowledge Base)

- Indexation de toutes les sources personnelles (notes, réunions, articles, repos)
- Wiki compilé automatiquement par LLM (structure Obsidian)
- Q&A contre la knowledge base : "c'est quoi le contexte du projet ARC ?"
- Journalisation passive de la journée → alimente la mémoire long terme
- Apprentissage actif : Nova documente ses nouveaux skills dans sa propre KB

## Inspiration

- Jarvis (Iron Man) — proactivité, personnalité, anticipation
- Karpathy LLM Knowledge Base — wiki compilé par LLM, opéré par LLM
- OpenClaw — framework agentique open-source, 250k+ étoiles GitHub

## Principe de confidentialité

Nova est **personnel**. Le profil Cédric est distinct du profil invité/famille.
Les automatisations, l'historique de présence, le calendrier et la mémoire
de Nova sont accessibles uniquement à leur propriétaire.
