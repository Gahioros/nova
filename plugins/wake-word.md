# Plugin — Wake Word "Nova"

## Choix

- **Mot déclencheur** : "Nova" (un seul mot, naturel, comme appeler quelqu'un par son prénom)
- **Genre** : féminin — "elle"
- **Moteur** : OpenWakeWord (custom, modèle entraîné sur "Nova")

## Gestion des faux positifs

Nova gère elle-même les faux positifs sans intervention manuelle.

### 1. Timeout silencieux
Après activation, si aucune voix détectée dans les 3-4s → retour en veille sans action.
```
"Nova" détecté → ding discret → attente 3s → silence → retour veille
```

### 2. Signal d'activation discret
Un son léger (ding) confirme l'activation. L'utilisateur sait qu'elle a entendu :
- Si c'était voulu → on parle
- Si c'était un faux positif → on ignore, elle se rendort toute seule

### 3. Seuil adaptatif
Si trop de faux positifs sur une période (ex: > 3 en 10 min) → OpenWakeWord remonte
automatiquement le seuil de sensibilité pour cette session.

### 4. Détection contexte audio (phase avancée)
Distinguer "Nova" prononcé par l'utilisateur vs "Nova" venant de la TV/musique :
- Analyse du pattern sonore (distance micro, réverbération)
- Apprentissage progressif des sources de faux positifs récurrentes

## Entraînement du modèle custom

OpenWakeWord permet d'entraîner un modèle sur un mot custom avec ~500 samples audio.

```bash
# Générer les samples TTS automatiquement (pas besoin de les enregistrer manuellement)
python train_model.py --word "Nova" --samples 500 --output models/nova.tflite
```

La plupart des modèles custom OpenWakeWord sont entraînés sur des voix TTS synthétiques
— ça suffit pour une bonne détection en conditions réelles.

## Intégration dans le pipeline

```
Micro toujours actif → OpenWakeWord (nova.tflite)
                              ↓ détecté
                         ding discret
                              ↓
                    Whisper STT (3-4s window)
                              ↓ silence → retour veille
                              ↓ voix → LLM → TTS streaming
```

## Statut

- [ ] Générer samples audio "Nova" (TTS automatique)
- [ ] Entraîner modèle OpenWakeWord custom
- [ ] Implémenter timeout silencieux + ding d'activation
- [ ] Intégrer seuil adaptatif
- [ ] Test en conditions réelles (TV allumée, musique, conversation)
