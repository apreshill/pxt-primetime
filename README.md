# pxt-primetime

Build multimodal AI applications with Pixeltable. Learn data-centric workflows, semantic search, and content generation using video as an example.

## Prerequisites

- Python 3.10+  
- [uv](https://docs.astral.sh/uv/) - Fast Python package installer (`pip install uv` or `brew install uv`)  
- [ffmpeg](https://ffmpeg.org/) - Required for video processing (`brew install ffmpeg` on macOS, `apt install ffmpeg` on Linux)  

## Setup

1. Clone this repo and navigate to it:

  ```bash
   git clone https://github.com/apreshill/pxt-primetime/tree/main
   cd pxt-primetime
  ```

2. Install all dependencies (uv will automatically create a virtual environment):

  ```bash
   uv sync
  ```

   `uv` creates a `.venv` folder and installs all dependencies.
   **If you already have Pixeltable installed**, `uv sync` will upgrade it to the required version (>=0.5.13) along with all other dependencies.

3. Configure API keys: 

  **Gemini API Key** (required for Act 3):  
  - Get your free API key from [aistudio.google.com](https://aistudio.google.com/apikey)  
  - See [Pixeltable's API key configuration guide](https://docs.pixeltable.com/howto/cookbooks/core/workflow-api-keys) for detailed setup instructions  
  - Set as environment variable:  
    ```bash
    export GEMINI_API_KEY='your-api-key-here'
    ```
  - Or add to `~/.pixeltable/config.toml`:  
    ```toml
    [gemini]
    api_key = "your-api-key-here"
    ```

   **OpenAI API Key** (optional for Act 2):  
  - Only needed if you want faster transcription using OpenAI's Whisper API instead of the local model  
  - Set as environment variable:  
    ```bash
    export OPENAI_API_KEY='your-api-key-here'
    ```

4. Open VS Code/Cursor in this project folder (or reload if already open)

## Dependencies

All dependencies are automatically installed when you run `uv sync` (see Setup section above). This project uses **Pixeltable v0.5.15**. The following is a reference of what gets installed - you don't need to install these manually:

### Core Dependencies

- **pixeltable** (>=0.5.15): Primary library for this project. Provides table, view, and computed column functionality.

### Video Processing

- **opencv-python**: Required for video processing operations
- **scenedetect**: Required for scene boundary detection in videos
- **pytube**: For downloading videos from YouTube (if needed)

### Text Processing & Embeddings

- **sentence-transformers** (>=2.0.0): Required for Hugging Face sentence embeddings
  - Used in: `02_iterating-with-data.ipynb` - creating embedding indexes on transcript text

### Audio Processing & Transcription

- **openai-whisper**: Required for local Whisper transcription (`pxt.functions.whisper.transcribe()`)
  - Used in: `02_iterating-with-data.ipynb` - transcribing audio chunks
- **openai** (optional): For OpenAI Whisper API transcription (`pxt.functions.openai.transcriptions()`)
  - Used in: `02_iterating-with-data.ipynb` - faster transcription alternative (requires API key)
  - Note: Install separately with `uv add openai` if you want to use the OpenAI API instead of local Whisper

### Video Generation

- **google-genai**: Required for Gemini video generation (`pxt.functions.gemini.generate_videos()`)
  - Used in: `03_generate-from-data.ipynb` - generating intro/outro videos using Gemini's Veo model
  - Requires: Gemini API key (free tier available)

### Development

- **ipykernel**: For running Jupyter notebooks
- **jupyter**: For notebook interface

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
  - This confirms you're using this project's environment, not another venv or system Pytho

