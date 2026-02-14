## AI-Powered Certificate Verification System

End-to-end project: OCR + forgery detection + database match + optional QR/blockchain.

### Structure
- `backend/` — FastAPI server and utilities
- `frontend/` — Simple HTML UI
- `database/` — Place genuine and fake images here (e.g., `cert1.png`, `fake_cert1.png`)
- `uploads/` — Saved uploads
- `scripts/` — Demo scripts and workflow diagram generator
- `blockchain/` — Hash registry (`registry.json`)
- `assets/` — Workflow image

### Setup (Windows PowerShell)
```powershell
python -m venv .venv
. .venv\Scripts\Activate.ps1
pip install -r backend/requirements.txt
```

### Run Backend
```powershell
uvicorn backend.app:app --reload --port 8000
```

### Frontend
Open `frontend/index.html` in a browser (or Live Server). Set API URL if different.

### Demo
```powershell
# Build registry from database/ images
python scripts/build_registry.py

# Verify an image
python scripts/demo_verify.py --input database/cert1.png --use-registry

# Generate workflow diagram
python scripts/generate_workflow_diagram.py
```

### Notes
- OCR uses EasyOCR; falls back to Tesseract if available.
- Forgery check uses SSIM and region edges for seal/sign/photo heuristics.
- Valid if close DB match and no tampering; fake if labeled fake or tampering detected.
