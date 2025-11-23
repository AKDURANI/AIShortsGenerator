# AI Shorts Generator

[![GitHub license](https://img.shields.io/github/license/yourusername/AIShortsGenerator)](LICENSE)
[![Python version](https://img.shields.io/badge/python-3.10%2B-blue)]

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [License](#license)
- [Contributing](#contributing)
- [Acknowledgements](#acknowledgements)

---

## Overview
**AI Shorts Generator** is a Python‑based tool that automatically creates short‑form YouTube videos. It combines OpenAI‑generated narration with AI‑generated background images (via Replicate’s Fooocus API) and assembles them into a video with optional subtitles.

## Features
- **Narration generation** using OpenAI’s `gpt‑3.5‑turbo` model.
- **Image generation** via Replicate’s Fooocus API.
- **Text‑to‑speech** using the RapidAPI TTS service.
- **Video assembly** with OpenCV, including animated text overlays.
- Simple CLI / notebook interface for rapid prototyping.

## Architecture
```
+-------------------+      +-------------------+      +-------------------+
|  Prompt / Source  | ---> |  OpenAI (GPT)     | ---> |  Narration JSON   |
+-------------------+      +-------------------+      +-------------------+
                                 |
                                 v
                         +-------------------+
                         |  Replicate (Fooocus) |
                         +-------------------+
                                 |
                                 v
                         +-------------------+
                         |  Image files (.webp) |
                         +-------------------+
                                 |
                                 v
                         +-------------------+
                         |  TTS (RapidAPI)   |
                         +-------------------+
                                 |
                                 v
                         +-------------------+
                         |  Audio files (.mp3) |
                         +-------------------+
                                 |
                                 v
                         +-------------------+
                         |  OpenCV Video Builder |
                         +-------------------+
```

## Installation
```bash
# Clone the repository (if you haven't already)
git clone https://github.com/yourusername/AIShortsGenerator.git
cd AIShortsGenerator

# Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # on Windows: venv\Scripts\activate

# Install required Python packages
pip install -r requirements.txt
```
If a `requirements.txt` is not present, the core dependencies are:
```bash
pip install openai replicate gtts pydub opencv-python tqdm
```

## Configuration
Create a file named `config.env` (or set environment variables) with the following keys:
```text
OPENAI_API_KEY=your‑openai‑api‑key
REPLICATE_API_TOKEN=your‑replicate‑api‑token
RAPIDAPI_KEY=your‑rapidapi‑key   # for TTS service
```
Load them in your script/notebook:
```python
import os
from dotenv import load_dotenv
load_dotenv('config.env')

openai_api_key = os.getenv('OPENAI_API_KEY')
replicate_token = os.getenv('REPLICATE_API_TOKEN')
rapidapi_key = os.getenv('RAPIDAPI_KEY')
```

## Usage
The easiest way to run the pipeline is through the provided Jupyter notebook:
1. Open `YTAISHORTS_final.ipynb`.
2. Execute the cells sequentially – they will:
   - Generate narration prompts.
   - Call OpenAI for text.
   - Parse the response into a JSON structure.
   - Generate images with Replicate.
   - Synthesize speech via the TTS API.
   - Assemble the final video.

Alternatively, you can call the helper functions directly from a Python script:
```python
from generate import create_from_data, generate

# Assuming `data` is the parsed JSON from OpenAI
create_from_data(data)
```
Make sure the required API keys are set in the environment before running.

## License
This project is licensed under the MIT License – see the `LICENSE` file for details.

## Contributing
Contributions are welcome! Please follow these steps:
1. Fork the repository.
2. Create a feature branch (`git checkout -b feature/awesome-feature`).
3. Write tests (if applicable) and ensure existing tests pass.
4. Submit a pull request with a clear description of your changes.

## Acknowledgements
- **OpenAI** for the powerful language model.
- **Replicate** for the Fooocus image generation API.
- **RapidAPI** for the text‑to‑speech service.
- **OpenCV** for video processing utilities.

---

