---
name: montage-ffmpeg
description: Couper, assembler, convertir, compresser, recadrer ou sous-titrer une vidéo avec ffmpeg. À utiliser dès qu'un fichier vidéo ou audio doit être transformé en ligne de commande.
---

# Montage avec ffmpeg

## Méthode

1. Vérifier que `ffmpeg` et `ffprobe` existent (`which ffmpeg ffprobe`), sinon les installer.
2. Inspecter la source avant toute commande : `ffprobe -hide_banner -i entrée.mp4`. Noter durée, codecs, résolution, fréquence d'images.
3. Ne jamais écraser l'original. Écrire dans un nouveau fichier.
4. Après la commande, contrôler la durée et la lecture du résultat avec `ffprobe`.

## Commandes courantes

Couper sans ré-encoder (rapide, précision à l'image clé) :

```
ffmpeg -ss 00:01:00 -to 00:02:30 -i entrée.mp4 -c copy sortie.mp4
```

Couper avec précision (ré-encode) :

```
ffmpeg -ss 00:01:00 -to 00:02:30 -i entrée.mp4 -c:v libx264 -preset veryfast -crf 20 -c:a aac sortie.mp4
```

Assembler plusieurs fichiers de mêmes codecs (liste dans `liste.txt`, une ligne `file 'a.mp4'` par fichier) :

```
ffmpeg -f concat -safe 0 -i liste.txt -c copy sortie.mp4
```

Compresser : `-c:v libx264 -preset veryfast -crf 23 -c:a aac -b:a 128k` (plus le CRF est haut, plus le fichier est léger).

Redimensionner à 1080 de hauteur : `-vf scale=-2:1080`.

Format vertical 9:16 depuis une vidéo horizontale : `-vf "crop=ih*9/16:ih,scale=1080:1920"`.

Extraire l'audio : `ffmpeg -i entrée.mp4 -vn -c:a libmp3lame -q:a 2 sortie.mp3`.

Incruster des sous-titres : `-vf subtitles=sous-titres.srt`.

Accélérer ou ralentir : `-filter:v "setpts=0.5*PTS" -filter:a "atempo=2.0"` pour doubler la vitesse.

## Points d'attention

- Placer `-ss` avant `-i` pour une recherche rapide.
- `-c copy` ne permet aucun filtre : dès qu'on recadre, redimensionne ou incruste, il faut ré-encoder.
- Pour assembler des fichiers de codecs ou de résolutions différentes, les ré-encoder d'abord à un format commun.
- Ajouter `-n` pour refuser d'écraser un fichier de sortie existant.
- Dire clairement à la personne quel fichier a été créé et ce qui a changé.
