---
name: sous-titres
description: Transcrire une vidéo ou un audio, créer, corriger, découper ou traduire des sous-titres au format SRT ou VTT. À utiliser pour tout travail sur des sous-titres.
---

# Sous-titres et transcription

## Transcrire

1. Extraire l'audio : `ffmpeg -i entrée.mp4 -vn -ac 1 -ar 16000 audio.wav`.
2. Vérifier si un outil de transcription est disponible (`which whisper`, ou un paquet Python comme `faster-whisper`). Si aucun n'est installé, proposer de l'installer ou de travailler à partir d'un texte déjà fourni.
3. Indiquer la langue au lieu de la laisser deviner, et produire un fichier `.srt`.
4. Relire : noms propres, chiffres, termes techniques, homophones.

## Format SRT

```
1
00:00:01,200 --> 00:00:03,800
Première ligne de texte
seconde ligne éventuelle

2
00:00:04,000 --> 00:00:06,500
Bloc suivant
```

Numérotation continue, minutage `HH:MM:SS,mmm`, une ligne vide entre les blocs. Le VTT s'écrit avec un point au lieu de la virgule et commence par `WEBVTT`.

## Règles de lisibilité

- 2 lignes au maximum, environ 42 caractères par ligne.
- Un bloc reste affiché entre 1 et 7 secondes, avec une vitesse de lecture d'environ 17 caractères par seconde au plus.
- Couper aux endroits naturels de la phrase, jamais entre un article et son nom.
- Ne pas faire se chevaucher deux blocs.
- Ne pas texter les bruits sans importance ; noter entre crochets ceux qui comptent, par exemple [rires].

## Traduire

Traduire le sens et le registre, pas mot à mot, en gardant le minutage et la longueur compatibles avec la lecture. Conserver les noms propres. Livrer le fichier traduit à côté de l'original, sans le remplacer.

## Contrôle final

Compter les blocs, vérifier qu'aucun minutage ne se chevauche ni ne dépasse la durée de la vidéo, et lire un extrait au début, au milieu et à la fin.
