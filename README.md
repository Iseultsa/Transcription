**Autrice** : Iseult Séguin Aubé  (Pronom: elle)
**Date** : 25 juillet 2025  
**Licence** : BSD 3-Clause (voir fichier `LICENSE`)

# Description

Ce script a été développé dans un contexte de recherche et permet de **transcrire un fichier audio en texte**, avec **identification automatique des locuteurs (diarisation)**. Particulièrement utile pour la transcription d'entretiens en recherche qualitative. Il a été testé avec succès sur des entretiens en français québécois ainsi qu'en anglais. Formats : .txt, .md (Obsidian) et .docx. 

# Licence et conditions d'utilisation

Le script est distribué sous la licence BSD 3-Clause.  
Vous êtes libres de l'utiliser, le modifier et le redistribuer, à condition de respecter les points suivants :

- Ne pas utiliser le nom de l’autrice (Iseult Séguin Aubé) pour promouvoir des produits dérivés sans autorisation explicite.
- Respecter les licences respectives des bibliothèques utilisées (`whisperx`, `pyannote.audio`, `python-docx`, etc.).

# Remarques

Ce script est fourni "en l’état", sans garantie de maintenance.  
Il est mis à disposition dans un esprit de transparence scientifique et pour faciliter la réutilisation par d’autres chercheuses et chercheurs.

# Technologies utilisées

- **[WhisperX](https://github.com/m-bain/whisperx)** (Apache 2.0)  
  Extension du modèle Whisper d’OpenAI pour un alignement temporel précis et une meilleure gestion des segments.
  
- **[pyannote.audio](https://github.com/pyannote/pyannote-audio)** (MIT)  
  Outil de diarisation automatique basé sur des réseaux de neurones entraînés sur de grandes bases audio.
  
- **[python-docx](https://python-docx.readthedocs.io/en/latest/)** (MIT)  
  Utilisé pour exporter les transcriptions au format Word (.docx), en plus des formats texte et Markdown.
  
- Bibliothèques standards : `os`, `datetime`, `gc`, `torch`, etc.

# Environnement

## Exigences système 
- Python **3.8 ou plus récent**
- **GPU compatible CUDA** (obligatoire — aucun fallback CPU)
- **NVIDIA CUDA Toolkit** et pilotes installés

## Testé sur :
- Windows 11 (64 bits)
- Intel Core i7-11700F, 8 cœurs / 16 threads
- 64 Go de RAM
- NVIDIA GeForce RTX 3060 (12 Go VRAM)
- Python 3.10.18
- Conda 25.5.1
 
# Installation
## Vérification de la version CUDA et de PyTorch
Ce script nécessite un GPU NVIDIA avec support CUDA.  

 ⚠️ Si la version de PyTorch n’est pas compatible avec votre CUDA, WhisperX et pyannote.audio ne fonctionneront pas.

Pour vérifier si votre installation de PyTorch est compatible avec CUDA, lancez les commandes suivantes dans Python :

```python
import torch
print("CUDA disponible :", torch.cuda.is_available())
print("Version CUDA utilisée par PyTorch :", torch.version.cuda)
```

Utilisez ensuite le configurateur officiel de PyTorch pour obtenir la bonne commande d’installation :   [https://pytorch.org/get-started/locally/](https://pytorch.org/get-started/locally/)
   
## Dépendances à installer
Si votre environnement CUDA est correctement configuré (GPU détecté, pilotes installés, PyTorch compatible), vous pouvez installer les dépendances nécessaires avec les commandes suivantes :

```bash
pip install git+https://github.com/m-bain/whisperx.git
pip install pyannote.audio
pip install python-docx
```

### Liens vers les sources officielles

- WhisperX: [https://github.com/m-bain/whisperx](https://github.com/m-bain/whisperx)
   
- pyannote.audio: [https://github.com/pyannote/pyannote-audio](https://github.com/pyannote/pyannote-audio)
   
## Authentification Hugging Face et accès au modèle de diarisation

L’utilisation du modèle `pyannote/speaker-diarization` nécessite une authentification Hugging Face **et l’acceptation explicite des conditions d’accès**.

### Étapes obligatoires :

1. **Créer un compte Hugging Face** (si ce n’est pas déjà fait)  
   https://huggingface.co/join

2. **Générer un token d’accès personnel**  
   https://huggingface.co/settings/tokens

3. **Se connecter dans le terminal avec le token**  
   Cela permet d’enregistrer le token localement :  
   ```bash
   huggingface-cli login
   ```

4. **Accepter les conditions d’utilisation du modèle**  
Le modèle de diarisation utilisé (`pyannote/speaker-diarization`) est soumis à des conditions d'utilisation spécifiques sur Hugging Face.

Même après avoir créé un compte et généré un token d’accès, vous devrez **manuellement accepter les conditions d'accès à plusieurs dépôts** sur Hugging Face.  
Cette étape est **obligatoire** et doit être effectuée **directement sur le site web**.

- https://huggingface.co/pyannote/speaker-diarization
- https://huggingface.co/pyannote/embedding
- https://huggingface.co/pyannote/segmentation  

Même si vous êtes connecté·e avec un token valide, le script échouera si vous n’avez pas accepté les conditions **pour chacun des modèles nécessaires**.  
Cette validation ne peut pas être automatisée : elle doit être effectuée manuellement une fois pour chaque modèle.

# Limitations

- Ce script n’est pas compatible avec une exécution sur CPU : un GPU compatible CUDA est requis. Vous pouvez adapter le code pour le faire fonctionner sans GPU, mais il est important de noter que la diarisation deviendrait alors **très lente** et pourrait limiter l'utilisation du script, notamment sur de longs entretiens.
- La diarisation est toujours activée ; `pyannote.audio` et un token Hugging Face sont donc obligatoires.
- Le script ne fait pas de traitement par lot : un seul fichier à la fois.

---

# English

**Author**: Iseult Séguin Aubé (Pronoun: she)
**Date**: July 25, 2025  
**License**: BSD 3-Clause (see `LICENSE` file)

## Description

This script was developed for research purposes and allows you to **transcribe an audio file into text**, with **automatic speaker identification (diarization)**. It is particularly useful for transcribing interviews in qualitative research. It has been successfully tested on interviews in French (with a Quebec accent) and English. Formats: .txt, .md (Obsidian), and .docx.

## License and terms of use

The script is distributed under the BSD 3-Clause license.  
You are free to use, modify, and redistribute it, provided you comply with the following conditions:

- Do not use the author's name (Iseult Séguin Aubé) to promote derivative products without explicit permission.
- Respect the respective licenses of the libraries used (`whisperx`, `pyannote.audio`, `python-docx`, etc.).

## Notes

This script is provided “as is,” with no guarantee of maintenance.  
It is made available in the spirit of scientific transparency and to facilitate reuse by other researchers.

## Technologies used

- **[WhisperX](https://github.com/m-bain/whisperx)** (Apache 2.0)  
  Extension of OpenAI's Whisper model for precise temporal alignment and better segment management.
  
- **[pyannote.audio](https://github.com/pyannote/pyannote-audio)** (MIT)  
  Automatic diarization tool based on neural networks trained on large audio databases.
  
- **[python-docx](https://python-docx.readthedocs.io/en/latest/)** (MIT)  
  Used to export transcripts to Word (.docx) format, in addition to text and Markdown formats.
  
- Standard libraries: `os`, `datetime`, `gc`, `torch`, etc.

# Environment
## System requirements

- Python **3.8 or newer**
- **CUDA-compatible GPU** (required — no CPU fallback)
- **NVIDIA CUDA Toolkit** and drivers installed

## Tested on:
- Windows 11 (64-bit)
- Intel Core i7-11700F, 8 cores / 16 threads
- 64 GB RAM
- NVIDIA GeForce RTX 3060 (12 GB VRAM)
- Python 3.10.18
- Conda 25.5.1
- 
# Installation
## Checking the CUDA and PyTorch versions
This script requires an NVIDIA GPU with CUDA support.  

 ⚠️ If the PyTorch version is not compatible with your CUDA, WhisperX and pyannote.audio will not work.

To check if your PyTorch installation is compatible with CUDA, run the following commands in Python:

```python
import torch
print("CUDA available:", torch.cuda.is_available())
print("CUDA version used by PyTorch:", torch.version.cuda)
```

Then use the official PyTorch configurator to obtain the correct installation command:   [https://pytorch.org/get-started/locally/](https://pytorch.org/get-started/locally/)
   
## Dependencies to install
If your CUDA environment is correctly configured (GPU detected, drivers installed, PyTorch compatible), you can install the necessary dependencies with the following commands:

```bash
pip install git+https://github.com/m-bain/whisperx.git
pip install pyannote.audio
pip install python-docx
```

### Links to official sources

- WhisperX: [https://github.com/m-bain/whisperx](https://github.com/m-bain/whisperx)
   
- pyannote.audio: [https://github.com/pyannote/pyannote-audio](https://github.com/pyannote/pyannote-audio)
   
## Hugging Face authentication and access to the diarization model

Using the `pyannote/speaker-diarization` model requires Hugging Face authentication **and explicit acceptance of the terms of access**.

### Required steps:

1. **Create a Hugging Face account** (if you haven't already done so)
https://huggingface.co/join

2. **Generate a personal access token**
https://huggingface.co/settings/tokens

3. **Log in to the terminal with the token**  
This allows you to save the token locally:  
```bash
huggingface-cli login
```

4. **Accept the terms of use for the model**  
The diarization model used (`pyannote/speaker-diarization`) is subject to specific terms of use on Hugging Face.

Even after creating an account and generating an access token, you will need to **manually accept the terms of access to several repositories** on Hugging Face.  
This step is **mandatory** and must be done **directly on the website**.

- https://huggingface.co/pyannote/speaker-diarization
- https://huggingface.co/pyannote/embedding
- https://huggingface.co/pyannote/segmentation  

Even if you are logged in with a valid token, the script will fail if you have not accepted the terms and conditions **for each of the required models**.  
This validation cannot be automated: it must be done manually once for each model.

# Limitations

- This script is not compatible with CPU execution: a CUDA-compatible GPU is required. You can adapt the code to work without a GPU, but it is important to note that diarization would then become **very slow** and could limit the use of the script, especially for long interviews.

- Diarization is always enabled; `pyannote.audio` and a Hugging Face token are therefore required.

- The script does not perform batch processing: only one file at a time.