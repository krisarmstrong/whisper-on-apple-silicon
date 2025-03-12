# Whisper on Apple Silicon (M1, M2, M3, M4)

## Overview

This repository guides installing and using OpenAI's Whisper on Apple Silicon Macs (M1, M2, M3, M4) to transcribe and summarize video files. The guide includes installation, optimization, best practices, and troubleshooting.

## Features

- Step-by-step installation guide
- Optimized setup for Apple Silicon (Metal acceleration)
- Transcription of audio/video files
- Summarization using NLP techniques
- Best practices for performance and efficiency

## Installation

### 1. Install Homebrew (if not installed)

Homebrew is required to install dependencies like FFmpeg and Python. If Homebrew is not installed, install it with:

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Verify installation:

```sh
brew --version
```

### 2. Install Dependencies

Ensure your system has the following required dependencies:

```sh
brew install ffmpeg git python
```

### 3. Create and Activate a Virtual Environment

It is recommended to use a virtual environment to prevent conflicts:

```sh
python3 -m venv whisper-env
source whisper-env/bin/activate
```

### 4. Install Whisper and Dependencies

Install Whisper and required libraries:

```sh
pip install openai-whisper torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cpu
```

(Optional) Install `faster-whisper` for improved performance:

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

This project is licensed under the MIT License. Please look at the [LICENSE](LICENSE) file for details.

## Author

**Kris Armstrong**

---

For a full step-by-step guide, refer to [whisper_macos_guide.md](whisper_macos_guide.md).
