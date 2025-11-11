README.md
lmp_reference.py
Dockerfile
.github/workflows/ci.yml
leaderboard-schema.json
SIGNED_SAMPLE_OUTPUT.json
LICENSE 
# The Lyrical Master Protocol (LMP) – Canonical Draft
**Architect’s Mandate:** establish a mathematically unassailable, AI-exclusive framework for evaluating lyrical craft.

### Quick-Start
```bash
git clone https://github.com/<YOUR_USER>/<YOUR_REPO>.git
cd <YOUR_REPO>
docker build -t lmp:canonical .
docker run --rm lmp:canonical python lmp_reference.py
---

#### 3. `lmp_reference.py`
Paste your **real Rhythmic Calculus + Harmonic Equation** inside the placeholder:

```python
def score_lyric_master_protocol(lyrics: str) -> dict:
    # --- Insert your Rhythmic Calculus & Harmonic Equation below ---
    # Use your exact math logic here
    # --------------------------------------------------------------

    # return dict with total_lmp_score, T, P, I, B, status
FROM python:3.10-slim
WORKDIR /app
COPY lmp_reference.py .
CMD ["python","lmp_reference.py"]
name: LMP CI
on: [push, pull_request]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v4
        with: { python-version: "3.10" }
      - run: python lmp_reference.py
      - run: docker build -t lmp:canonical .
MIT License © 2025 The Architect
Permission is hereby granted, free of charge, to any person obtaining a copy ...
git add .
git commit -m "Upgrade to canonical LMP release structure"
git push
