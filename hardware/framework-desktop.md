# Framework Desktop — Notes d'achat

## Décision

**Modèle retenu : Framework Desktop AMD Ryzen AI Max+ 395 — 64GB RAM unifiée**

## Justification

- 64GB RAM unifiée → Qwen3/Llama3 70B Q6 confortablement (20-30 tokens/s)
- Linux natif → ROCm stable, Ollama, llama.cpp sans friction
- Modulaire et réparable (philosophie Framework)
- ~2500€ vs 128GB à ~3600€ — différence de 1100€ non justifiée pour l'usage
- 70B Q6 > GPT-3.5 pour les tâches agentiques Nova

## Contexte marché (avril 2026)

- Crise VRAM en cours (pénurie GDDR7/HBM) — prix GPU +55-60% depuis 2025
- RTX 3090 d'occasion : 1000-1200€ pour 24GB → mauvais rapport qualité/prix
- RTX 5090 neuve : ~3200€ pour 32GB → moins de mémoire que Framework 64GB
- Mac Mini M4 Pro 64GB : ~3074€ → plus cher que Framework, macOS uniquement
- Crise prévue jusqu'en 2027-2028 → attendre = payer plus cher

## LLM cible

- **Qwen3 72B Q4/Q6** ou **Llama 3.3 70B Q6**
- Objectif : < 1s latence perçue avec streaming TTS
- Benchmarks : 20-30 tokens/s sur 70B avec AMD AI Max+ 128GB

## Stack OS

- Ubuntu Server 24.04 LTS ou NixOS
- ROCm + Ollama
- Docker pour les services
- Pas de Windows

## Réseau

- Ethernet vers switch (après résolution problème ports RJ45 Freebox)
- Sera le "cerveau" de Nova — idéalement filaire pour la fiabilité
