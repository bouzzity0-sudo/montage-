# montage-studio

Plugin pour travailler la vidéo de l'idée à la livraison, en français.

## Skills

| Skill | Rôle |
|---|---|
| `scenario-storyboard` | Logline, synopsis, séquencier, scènes et storyboard plan par plan |
| `montage-ffmpeg` | Couper, assembler, convertir, compresser et recadrer avec ffmpeg |
| `sous-titres` | Transcrire, créer, corriger et traduire des sous-titres SRT ou VTT |
| `prompts-generation` | Prompts cohérents pour générer des images ou des vidéos depuis un storyboard |

## Structure

```
.claude-plugin/plugin.json
skills/
  scenario-storyboard/SKILL.md
  montage-ffmpeg/SKILL.md
  sous-titres/SKILL.md
  prompts-generation/SKILL.md
```

Le montage demande `ffmpeg` et `ffprobe` sur la machine. La transcription demande un outil de reconnaissance vocale tel que Whisper.
