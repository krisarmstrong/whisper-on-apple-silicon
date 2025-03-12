# Whisper on Apple Silicon (M1, M2, M3, M4)

## Overview
This repository provides a guide on installing and using OpenAI's Whisper on Apple Silicon Macs (M1, M2, M3, M4) to transcribe and summarize video files. The guide includes installation, optimization, best practices, and troubleshooting.

## Features
- Step-by-step installation guide
- Optimized setup for Apple Silicon (Metal acceleration)
- Transcription of audio/video files
- Summarization using NLP techniques
- Best practices for performance and efficiency

## Installation
1. Install Homebrew (if not installed):
   ```sh
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```
2. Install dependencies:
   ```sh
   brew install ffmpeg git python
   ```
3. Create and activate a virtual environment:
   ```sh
   python3 -m venv whisper-env
   source whisper-env/bin/activate
   ```
4. Install Whisper and dependencies:
   ```sh
   pip install openai-whisper torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cpu
   ```
5. (Optional) Install `faster-whisper` for improved performance:
   ```sh
   pip install faster-whisper
   ```

## Usage
### Transcribing a Video File
1. Convert video to audio:
   ```sh
   ffmpeg -i input_video.mp4 -ac 1 -ar 16000 output_audio.wav
   ```
2. Transcribe using Whisper:
   ```sh
   whisper output_audio.wav --model medium --language English
   ```

### Summarizing the Transcription
1. Install transformers:
   ```sh
   pip install transformers
   ```
2. Use Python for text summarization:
   ```python
   from transformers import pipeline

   def summarize_transcription(file_path):
       with open(file_path, "r") as f:
           text = f.read()
       summarizer = pipeline("summarization")
       summary = summarizer(text, max_length=150, min_length=50, do_sample=False)
       print("Summary:\n", summary[0]['summary_text'])

   summarize_transcription("output_audio.txt")
   ```

## Contributions
We welcome contributions! See [CONTRIBUTIONS.md](CONTRIBUTIONS.md) for details.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Author
**Kris Armstrong**

---
For a detailed step-by-step guide, refer to the full [Whisper macOS Guide](whisper_macos_guide.md).
