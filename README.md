# pxt-primetime

Build multimodal AI applications with Pixeltable. Learn data-centric workflows, semantic search, and content generation using video as an example.

## Prerequisites

- Python 3.10+
- [uv](https://docs.astral.sh/uv/) - Fast Python package installer (`pip install uv` or `brew install uv`)
- [ffmpeg](https://ffmpeg.org/) - Required for video processing (`brew install ffmpeg` on macOS, `apt install ffmpeg` on Linux)

## Setup

1. Clone this repo and navigate to it:
```bash
git clone <repo-url>
cd pxt-primetime
```

2. Create a virtual environment and install all dependencies:
```bash
uv sync
```
This will automatically install all dependencies listed above, including the spaCy English model (`en-core-web-sm`) required for sentence splitting.

   **If you already have Pixeltable installed**, `uv sync` will upgrade it to the required version (>=0.5.6) along with all other dependencies.

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

## Dependencies

All dependencies are automatically installed when you run `uv sync` (see Setup section above). This project uses **Pixeltable v0.5.6**. The following is a reference of what gets installed - you don't need to install these manually:

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

## Notebooks

This project contains three progressive notebooks that build on each other. **Run them in order** (Act 1 → Act 2 → Act 3) as each notebook depends on tables and data created in previous notebooks:

- `01_data-centric-workflows.ipynb` - Act 1: Data-centric Workflows
- `02_iterating-with-data.ipynb` - Act 2: Iterating with Data
- `03_generate-from-data.ipynb` - Act 3: Generate New Content from Data

## Running Notebooks

1. Open a notebook
2. Click the kernel selector in the top-right corner
3. Select the kernel showing `.venv` with the full path to this project's `.venv/bin/python`
   - Look for the path that includes `/pxt-primetime/.venv/bin/python`
   - This confirms you're using this project's environment, not another venv or system Python
