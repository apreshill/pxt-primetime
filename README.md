# pxt-primetime

Video analysis workflows with Pixeltable.

## Prerequisites

- Python 3.10+
- [uv](https://docs.astral.sh/uv/) - Fast Python package installer (`pip install uv` or `brew install uv`)
- [ffmpeg](https://ffmpeg.org/) - Required for video processing (`brew install ffmpeg` on macOS, `apt install ffmpeg` on Linux)

## Dependencies

This project uses **Pixeltable v0.5.6**. See `pyproject.toml` for the complete list of dependencies.

### Core Dependencies

* **pixeltable** (>=0.5.6): Primary library for this project. Provides table, view, and computed column functionality.

### Video Processing

* **opencv-python**: Required for video processing operations
* **scenedetect**: Required for scene boundary detection in videos
* **pytube**: For downloading videos from YouTube (if needed)

### Text Processing & Embeddings

* **sentence-transformers** (>=2.0.0): Required for Hugging Face sentence embeddings
  * Used in: `02_iterating-with-data.ipynb` - creating embedding indexes on transcript text
* **spacy** (>=3.0.0): Required for sentence splitting in text processing
  * Used in: `02_iterating-with-data.ipynb` - splitting transcript text into sentences using `string_splitter`
  * **en-core-web-sm**: The spaCy English language model is automatically installed via `uv sync` as a URL dependency

### Audio Processing & Transcription

* **openai-whisper**: Required for local Whisper transcription (`pxt.functions.whisper.transcribe()`)
  * Used in: `02_iterating-with-data.ipynb` - transcribing audio chunks
* **openai** (optional): For OpenAI Whisper API transcription (`pxt.functions.openai.transcriptions()`)
  * Used in: `02_iterating-with-data.ipynb` - faster transcription alternative (requires API key)
  * Note: Install separately with `uv add openai` if you want to use the OpenAI API instead of local Whisper

### Video Generation

* **google-genai**: Required for Gemini video generation (`pxt.functions.gemini.generate_videos()`)
  * Used in: `03_generate-from-data.ipynb` - generating intro/outro videos using Gemini's Veo model
  * Requires: Gemini API key (free tier available)

### Development

* **ipykernel**: For running Jupyter notebooks
* **jupyter**: For notebook interface

## Setup

1. Clone this repo and navigate to it:
```bash
git clone <repo-url>
cd pxt-primetime
```

2. Create a virtual environment and install dependencies:
```bash
uv sync
```
This will automatically install the spaCy English model (`en-core-web-sm`) required for sentence splitting.

3. Configure API keys (optional, but recommended):
   - **Gemini API Key** (recommended): Required for video generation in `03_generate-from-data.ipynb`. You can use the [free tier](https://ai.google.dev/gemini-api/docs/pricing). Set as environment variable:
     ```bash
     export GEMINI_API_KEY='your-api-key-here'
     ```
     Or the notebook will prompt you to enter it when you run it.
   - **OpenAI API Key** (optional): For faster transcription using OpenAI's Whisper API instead of the local model. Set as environment variable:
     ```bash
     export OPENAI_API_KEY='your-api-key-here'
     ```
   **Security Note**: Keep your keys secure by using environment variables, never commit them to git, and delete unused keys.

4. Open VS Code/Cursor in this project folder (or reload if already open)

## Running Notebooks

1. Open a notebook
2. Click the kernel selector in the top-right corner
3. Select the kernel showing `.venv` with the full path to this project's `.venv/bin/python`
   - Look for the path that includes `/pxt-primetime/.venv/bin/python`
   - This confirms you're using this project's environment, not another venv or system Python
