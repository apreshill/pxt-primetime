# pxt-primetime

Video analysis workflows with Pixeltable.

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

2. Create a virtual environment and install dependencies:
```bash
uv sync
```

3. Open VS Code/Cursor in this project folder (or reload if already open)

## Running Notebooks

1. Open a notebook
2. Click the kernel selector in the top-right corner
3. Select the kernel showing `.venv` with the full path to this project's `.venv/bin/python`
   - Look for the path that includes `/pxt-primetime/.venv/bin/python`
   - This confirms you're using this project's environment, not another venv or system Python
