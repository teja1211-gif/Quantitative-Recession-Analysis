# Project Setup

## Create environment

```bash
python -m venv .venv
```

### macOS/Linux

```bash
source .venv/bin/activate
```

### Windows

```powershell
.venv\Scripts\activate
```

## Install dependencies

```bash
pip install -r requirements.txt
```

## Start Jupyter

```bash
jupyter notebook
```

## FRED API key

Create a local `.env` file based on `.env.example`.

Do not commit `.env` or any API keys to GitHub.
